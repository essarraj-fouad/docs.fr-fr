---
title: "résoudre les chargements d'assemblys"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET Framework], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0fe3347c640b7e99487d630cbfac97e774bda7bb
ms.contentlocale: fr-fr
ms.lasthandoff: 07/28/2017

---
# <a name="resolving-assembly-loads"></a>résoudre les chargements d'assemblys
Le .NET Framework fournit l’événement <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> pour les applications qui nécessitent un meilleur contrôle du chargement d’assembly. En gérant cet événement, votre application peut charger un assembly dans le contexte de chargement à l’extérieur des chemins de détection normaux, sélectionner la version d’assembly à charger parmi plusieurs, émettre un assembly dynamique et le retourner, etc. Cette rubrique fournit des instructions sur la gestion de l’événement <xref:System.AppDomain.AssemblyResolve>.  
  
> [!NOTE]
>  Pour résoudre les chargements d’assemblys dans le contexte ReflectionOnly, utilisez l’événement <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=fullName> à la place.  
  
## <a name="how-the-assemblyresolve-event-works"></a>Fonctionnement de l’événement AssemblyResolve  
 Quand vous inscrivez un gestionnaire pour l’événement <xref:System.AppDomain.AssemblyResolve>, le gestionnaire est appelé chaque fois que le runtime ne peut pas établir de liaison à un assembly par nom. Par exemple, l’appel des méthodes suivantes à partir du code utilisateur peut provoquer le déclenchement de l’événement <xref:System.AppDomain.AssemblyResolve> :  
  
-   surcharge de méthode <xref:System.AppDomain.Load%2A?displayProperty=fullName> ou <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> dont le premier argument est une chaîne qui représente le nom complet de l’assembly à charger (autrement dit, la chaîne retournée par la propriété <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName>) ;  
  
-   surcharge de méthode <xref:System.AppDomain.Load%2A?displayProperty=fullName> ou <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> dont le premier argument est un objet <xref:System.Reflection.AssemblyName> qui identifie l’assembly à charger ;  
  
-   surcharge de méthode <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName> ;  
  
-   surcharge de méthode <xref:System.AppDomain.CreateInstance%2A?displayProperty=fullName> ou <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=fullName> qui instancie un objet dans un autre domaine d’application.  
  
### <a name="what-the-event-handler-does"></a>Rôle du gestionnaire d’événements  
 Le gestionnaire de l’événement <xref:System.AppDomain.AssemblyResolve> reçoit le nom complet de l’assembly à charger dans la propriété <xref:System.ResolveEventArgs.Name%2A?displayProperty=fullName>. Si le gestionnaire ne reconnaît pas le nom de l’assembly, il retourne la valeur Null (`Nothing` en Visual Basic, `nullptr` en Visual C++).  
  
 Si le gestionnaire reconnaît le nom de l’assembly, il peut charger et retourner un assembly qui satisfait la requête. La liste suivante décrit des exemples de scénarios.  
  
-   Si le gestionnaire connaît l’emplacement d’une version de l’assembly, il peut charger l’assembly à l’aide de la méthode <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> ou <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName>, et retourner l’assembly chargé si l’opération réussit.  
  
-   Si le gestionnaire a accès à une base de données d’assemblys stockés sous la forme de tableaux d’octets, il peut charger un tableau d’octets à l’aide de l’une des surcharges de méthode <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> qui acceptent un tableau d’octets.  
  
-   Le gestionnaire peut générer un assembly dynamique et le retourner.  
  
> [!NOTE]
>  Le gestionnaire doit charger l’assembly dans le contexte LoadFrom, dans le contexte de chargement ou sans contexte. Si le gestionnaire charge l’assembly dans le contexte ReflectionOnly à l’aide de la méthode <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=fullName> ou <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=fullName>, la tentative de chargement ayant déclenché l’événement <xref:System.AppDomain.AssemblyResolve> échoue.  
  
 Il appartient au gestionnaire d’événements de retourner un assembly approprié. Le gestionnaire peut analyser le nom complet de l’assembly demandé en passant la valeur de propriété <xref:System.ResolveEventArgs.Name%2A?displayProperty=fullName> au constructeur <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29>. À compter du [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], le gestionnaire peut utiliser la propriété <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName> pour déterminer si la requête actuelle est une dépendance d’un autre assembly. Ces informations permettent d’identifier un assembly qui satisfait la dépendance.  
  
 Le gestionnaire d’événements peut retourner une version de l’assembly différente de celle qui a été demandée.  
  
 Dans la plupart des cas, l’assembly qui est retourné par le gestionnaire apparaît dans le contexte de chargement, indépendamment du contexte dans lequel le gestionnaire le charge. Par exemple, si le gestionnaire utilise la méthode <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> pour charger un assembly dans le contexte LoadFrom, l’assembly apparaît dans le contexte de chargement quand le gestionnaire le retourne. Toutefois, dans le cas suivant, l’assembly apparaît sans contexte quand le gestionnaire le retourne :  
  
-   le gestionnaire charge un assembly sans contexte ;  
  
-   la propriété <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName> n’a pas la valeur Null ;  
  
-   l’assembly demandeur (c’est-à-dire, l’assembly retourné par la propriété <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName>) a été chargé sans contexte.  
  
 Pour plus d’informations sur les contextes, consultez la surcharge de méthode <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=fullName>.  
  
 Vous pouvez charger plusieurs versions du même assembly dans le même domaine d’application. Cette pratique n’est pas recommandée, car elle peut entraîner des problèmes d’assignation de type. Consultez [Bonnes pratiques pour le chargement d’assemblys](../../../docs/framework/deployment/best-practices-for-assembly-loading.md).  
  
### <a name="what-the-event-handler-should-not-do"></a>Ce que le gestionnaire d’événements ne doit pas faire  
 La règle principale pour gérer l’événement <xref:System.AppDomain.AssemblyResolve> est que vous ne devez pas essayer de retourner un assembly que vous ne reconnaissez pas. Quand vous écrivez le gestionnaire, vous devez avoir connaissance des assemblys qui peuvent provoquer le déclenchement de l’événement. Votre gestionnaire doit retourner Null pour d’autres assemblys.  
  
> [!IMPORTANT]
>  À compter du [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], l’événement <xref:System.AppDomain.AssemblyResolve> est déclenché pour les assemblys satellites. Ce changement affecte un gestionnaire d’événements qui a été écrit pour une version antérieure du .NET Framework, si le gestionnaire tente de résoudre toutes les requêtes de chargement d’assembly. Les gestionnaires d’événements qui ignorent les assemblys non reconnus ne sont pas affectés par ce changement : ils retournent la valeur Null et les mécanismes de secours normaux sont suivis.  
  
 Durant le chargement d’un assembly, le gestionnaire d’événements ne doit pas utiliser les surcharges de méthode <xref:System.AppDomain.Load%2A?displayProperty=fullName> et <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> qui peuvent provoquer le déclenchement de l’événement <xref:System.AppDomain.AssemblyResolve> de manière récursive, car cela peut provoquer un dépassement de capacité de la pile. (Consultez la liste fournie plus haut dans cette rubrique.) Cela se produit même si vous fournissez la gestion des exceptions pour la demande de chargement, car aucune exception n’est levée tant que tous les gestionnaires d’événements ne sont pas retournés. Le code suivant provoque donc un dépassement de capacité de la pile si `MyAssembly` est introuvable :  
  
 [!code-cpp[AssemblyResolveRecursive#1](../../../samples/snippets/cpp/VS_Snippets_CLR/assemblyresolverecursive/cpp/example.cpp#1)] [!code-csharp[AssemblyResolveRecursive#1](../../../samples/snippets/csharp/VS_Snippets_CLR/assemblyresolverecursive/cs/example.cs#1)] [!code-vb[AssemblyResolveRecursive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/assemblyresolverecursive/vb/example.vb#1)]  
  
## <a name="see-also"></a>Voir aussi  
 [Bonnes pratiques pour le chargement d’assemblys](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)   
 [Utilisation des domaines d’application](../../../docs/framework/app-domains/use.md)

