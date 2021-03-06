---
title: Ressources dans des applications de bureau
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
- deploying applications [.NET Framework], resources
- application resources
- resource files
- satellite assemblies
- localization
- packaging application resources
- localizing resources
ms.assetid: 8ad495d4-2941-40cf-bf64-e82e85825890
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 95ca72a6da8def7c98a978650c60a27722141527
ms.contentlocale: fr-fr
ms.lasthandoff: 09/05/2017

---
# <a name="resources-in-desktop-apps"></a>Ressources dans des applications de bureau
Presque toutes les applications d'une qualité de niveau "production" doivent utiliser des ressources. Une ressource est une donnée non exécutable qui est déployée logiquement avec une application. Une ressource peut être affichée dans une application sous la forme de messages d'erreur ou comme faisant partie de l'interface utilisateur. Les ressources peuvent contenir des données sous plusieurs formes, telles que des chaînes, des images et des objets rendus persistants. (Pour écrire des objets persistants dans un fichier de ressources, les objets doivent être sérialisables.) Le stockage de vos données dans un fichier de ressources vous permet de changer les données sans avoir à recompiler l'intégralité de votre application. Il vous permet également de stocker des données dans un emplacement unique, et élimine la nécessité d'avoir recours à des données codées en dur stockées dans plusieurs emplacements.  
  
 .NET Framework fournit une prise en charge complète pour la création et la localisation des ressources dans des applications de bureau. De plus, .NET Framework prend en charge un modèle simple pour la compression et le déploiement de ces ressources localisées dans des applications de bureau.  
  
 Pour plus d’informations sur les ressources ASP.NET, voir [Vue d’ensemble des ressources des pages Web ASP.NET](http://msdn.microsoft.com/library/0936b3b2-9e6e-4abe-9c06-364efef9dbbd) dans le Centre de développement Internet Explorer.  
  
 Les applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] utilisent un autre modèle de ressource d'applications de bureau et stockent leurs ressources dans unique fichier d'index de ressource de package (PRI). Pour plus d’informations sur les ressources des applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], voir [Création et récupération de ressources dans les applications Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=241674) dans le centre de développement Windows.  
  
## <a name="creating-and-localizing-resources"></a>Créer et localiser les ressources  
 Dans une application non localisée, vous pouvez utiliser des fichiers de ressources comme référentiel pour les données d'application, notamment pour les chaînes qui auraient pu être codées en dur dans plusieurs emplacements de code source. En règle générale, vous créez des ressources sous forme de fichier texte (.txt) ou de fichiers XML (.resx), et vous utilisez [Resgen.exe (Resource File Generator)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) pour les compiler dans des fichiers binaires .resources. Ces fichiers peuvent être incorporés dans le fichier exécutable de l'application par un compilateur de langage. Pour plus d’informations sur la création des ressources, consultez [Création de fichiers de ressources](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md).  
  
 Vous pouvez également localiser les ressources de votre application pour des cultures spécifiques. Cela vous permet de générer des versions localisées (traduites) de vos applications. Lorsque vous développez une application qui utilise des ressources localisées, vous indiquez une culture qui sert de culture neutre ou de secours dont les ressources sont utilisées si aucune ressource appropriée n'est disponible. En général, les ressources de la culture neutre sont stockées dans le fichier exécutable de l'application. Les ressources restantes pour les cultures individuelles localisées sont stockées dans des assemblys satellites autonomes. Pour plus d’informations, consultez [Création d’assemblys satellites](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md).  
  
## <a name="packaging-and-deploying-resources"></a>Empaquetage et déploiement de ressources  
 Vous déployez des ressources localisées d’application dans les [assemblys satellites](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md). Un assembly satellite contient les ressources d'une culture unique ; il ne contient aucun code d'application. Dans le modèle de déploiement d'assembly satellite, vous créez une application avec un assembly par défaut (qui est généralement l'assembly principal) et un assembly satellite pour chaque culture que l'application prend en charge. Dans la mesure où les assemblys satellites ne font pas partie de l'assembly principal, vous pouvez facilement remplacer ou mettre à jour les ressources correspondant à une culture spécifique sans remplacer l'assembly principal de l'application.  
  
 Il est important de déterminer avec précision les ressources qui composent l'assembly de ressources par défaut d'une application. Dans la mesure où il fait partie de l’assembly principal, toute modification apportée vous contraint à remplacer cet assembly. Si vous ne fournissez pas une ressource par défaut, une exception sera levée au moment où le [processus de secours pour les ressources](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md) tente de la localiser. Dans une application bien conçue, l'utilisation de ressources ne doit pas renvoyer d'exception.  
  
 Pour plus d’informations, consultez l’article [Empaquetage et déploiement de ressources](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
## <a name="retrieving-resources"></a>Récupération de ressources  
 Au moment de l'exécution, une application charge les ressources localisées appropriées sur une base par thread, selon la culture spécifiée par la propriété <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>. Cette valeur de propriété est dérivée comme suit :  
  
-   En assignant directement un objet <xref:System.Globalization.CultureInfo> qui représente la culture localisée à la propriété <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName>.  
  
-   Si une culture n'est pas explicitement assignée, en extrayant la culture d'interface utilisateur par défaut du thread de la propriété <xref:System.Globalization.CultureInfo.DefaultThreadCurrentUICulture%2A?displayProperty=fullName>.  
  
-   Si une culture d'interface utilisateur par défaut du thread n'est pas explicitement assignée, en extrayant la culture de l'utilisateur actuel sur l'ordinateur local en appelant la fonction Windows `GetUserDefaultUILanguage`.  
  
 Pour plus d'informations sur la façon dont la culture d'interface utilisateur actuelle est définie, consultez les pages de référence <xref:System.Globalization.CultureInfo> et <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>.  
  
 Vous pouvez ensuite extraire des ressources pour la culture de l'interface utilisateur actuelle ou pour une culture spécifique en utilisant la classe <xref:System.Resources.ResourceManager?displayProperty=fullName>. Bien que la classe <xref:System.Resources.ResourceManager> soit la plus fréquemment utilisée pour extraire des ressources dans les applications de bureau, l'espace de noms <xref:System.Resources?displayProperty=fullName> contient les types supplémentaires que vous pouvez utiliser pour récupérer des ressources. Elles incluent notamment :  
  
-   La classe <xref:System.Resources.ResourceReader>, qui vous permet d'énumérer des ressources incorporées dans un assembly ou stockées dans un fichier .resources binaire. C'est utile lorsque vous ne connaissez pas les noms exacts des ressources disponibles au moment de l'exécution.  
  
-   La classe <xref:System.Resources.ResXResourceReader>, qui permet d'accéder aux ressources d'un fichier XML (.resx).  
  
-   La classe <xref:System.Resources.ResourceSet>, qui vous permet de récupérer les ressources d'une culture spécifique sans observer les règles de secours. Les ressources peuvent être stockées dans un assembly ou un fichier .resources binaire. Vous pouvez également développer une implémentation de <xref:System.Resources.IResourceReader> qui vous permet d'utiliser la classe <xref:System.Resources.ResourceSet> pour récupérer les ressources d'une autre source.  
  
-   La classe <xref:System.Resources.ResXResourceSet>, qui permet de récupérer tous les éléments dans un fichier de ressources XML en mémoire.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Globalization.CultureInfo>   
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>   
 [Application Essentials](../../../docs/standard/application-essentials.md)   
 [Création de fichiers de ressources](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [Empaquetage et déploiement de ressources](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)   
 [Création d’assemblys satellites](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)   
 [Récupération de ressources](../../../docs/framework/resources/retrieving-resources-in-desktop-apps.md)

