---
title: Guide pratique pour effectuer une compilation conditionnelle avec Trace et Debug
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- trace compiler options
- trace statements
- compiling source code, trace statements
- tracing [.NET Framework], enabling or disabling
- tracing [.NET Framework], compiling conditionally
- TRACE directive
- conditional compilation, tracing code
ms.assetid: 56d051c3-012c-42c1-9a58-7270edc624aa
caps.latest.revision: 11
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ee67d687b52bd911597fb99e6f1316e8a9cf5fe0
ms.contentlocale: fr-fr
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-compile-conditionally-with-trace-and-debug"></a>Guide pratique pour effectuer une compilation conditionnelle avec Trace et Debug
Quand vous déboguez une application pendant le développement, les sorties de débogage et de traçage sont dirigées vers la fenêtre de sortie dans Visual Studio. Toutefois, pour inclure les fonctionnalités de suivi dans une application déployée, vous devez compiler vos applications instrumentées en activant la directive de compilateur **TRACE**. De cette façon, le code de traçage peut être compilé dans la version commerciale de votre application. Si vous n’activez pas la directive **TRACE**, tout le code de suivi est ignoré pendant la compilation et n’est pas inclus dans le code exécutable que vous déployez.  
  
 Les méthodes de traçage et de débogage sont associées à des attributs conditionnels. Par exemple, si l’attribut conditionnel pour le suivi a la valeur **true**, toutes les instructions de suivi sont incluses dans un assembly (fichier .exe ou .dll compilé) ; si l’attribut conditionnel **Trace** a la valeur **false**, les instructions de suivi ne sont pas incluses.  
  
 Vous pouvez activer l’attribut conditionnel **Trace** ou **Debug**, les deux ou aucun pour une build. Par conséquent, il existe quatre types de build : **Debug**, **Trace**, les deux ou aucun. Certaines versions release pour un déploiement de production peuvent n’en contenir aucun, mais la plupart des builds contiennent les deux.  
  
 Vous pouvez spécifier les paramètres du compilateur pour votre application de plusieurs façons :  
  
-   Pages de propriétés  
  
-   Ligne de commande  
  
-   **#CONST** (pour Visual Basic) et **#define** (pour C#)  
  
### <a name="to-change-compile-settings-from-the-property-pages-dialog-box"></a>Pour modifier les paramètres de compilation dans la boîte de dialogue des pages de propriétés  
  
1.  Cliquez avec le bouton droit sur le nœud du projet dans l’**Explorateur de solutions**.  
  
2.  Choisissez **Propriétés** dans le menu contextuel.  
  
    -   En Visual Basic, cliquez sur l’onglet **Compiler** dans le volet gauche de la page de propriétés, puis sur le bouton **Options avancées de compilation** pour afficher la boîte de dialogue **Paramètres avancés du compilateur**. Cochez les cases des paramètres du compilateur que vous voulez activer. Décochez les cases des paramètres que vous voulez désactiver.  
  
    -   En C#, cliquez sur l’onglet **Générer** dans le volet gauche de la page de propriétés, puis cochez les cases des paramètres du compilateur que vous voulez activer. Décochez les cases des paramètres que vous voulez désactiver.  
  
### <a name="to-compile-instrumented-code-using-the-command-line"></a>Pour compiler du code instrumenté à l'aide de la ligne de commande  
  
1.  Définissez un commutateur de compilateur conditionnel sur la ligne de commande. Le compilateur devra contenir du code de traçage ou de débogage dans l'exécutable.  
  
     Par exemple, l'instruction de compilateur suivante entrée sur la ligne de commande inclut le code de traçage dans un fichier exécutable compilé :  
  
     Pour Visual Basic : **vbc /r:System.dll /d:TRACE=TRUE /d:DEBUG=FALSE MyApplication.vb**  
  
     Pour C# : **csc /r:System.dll /d:TRACE /d:DEBUG=FALSE MyApplication.cs**  
  
    > [!TIP]
    >  Pour compiler plusieurs fichiers d’application, insérez un espace entre les noms de fichiers, par exemple **MyApplication1.vb MyApplication2.vb MyApplication3.vb** ou **MyApplication1.cs MyApplication2.cs MyApplication3.cs**.  
  
     La signification des directives de compilation conditionnelle utilisées dans les exemples ci-dessus est la suivante :  
  
    |Directive|Signification|  
    |---------------|-------------|  
    |`vbc`|compilateur Visual Basic|  
    |`csc`|Compilateur C#|  
    |`/r:`|Référence un assembly externe (EXE ou DLL)|  
    |`/d:`|Définit un symbole de compilation conditionnelle|  
  
    > [!NOTE]
    >  Vous devez écrire TRACE ou DEBUG en majuscules. Pour plus d'informations sur les commandes de compilation conditionnelle, entrez `vbc /?` (pour Visual Basic) ou `csc /?` (pour C#) à l'invite de commandes. Pour plus d’informations, consultez [Génération à partir de la ligne de commande](~/docs/csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) (C#) ou [Appel du compilateur de ligne de commande](~/docs/visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md) (Visual Basic).  
  
### <a name="to-perform-conditional-compilation-using-const-or-define"></a>Pour effectuer une compilation conditionnelle à l'aide de #CONST ou #define  
  
1.  Tapez l'instruction appropriée pour votre langage de programmation en haut du fichier de code source.  
  
    |Langage|Instruction du langage|Résultat|  
    |--------------|---------------|------------|  
    |**Visual Basic**|**#CONST TRACE = true**|Active le traçage|  
    ||**#CONST TRACE = false**|Désactive le traçage|  
    ||**#CONST DEBUG = true**|Active le débogage|  
    ||**#CONST DEBUG = false**|Désactive le débogage|  
    |**C#**|**#define TRACE**|Active le traçage|  
    ||**#undef TRACE**|Désactive le traçage|  
    ||**#define DEBUG**|Active le débogage|  
    ||**#undef DEBUG**|Désactive le débogage|  
  
### <a name="to-disable-tracing-or-debugging"></a>Pour désactiver le traçage ou le débogage  
  
1.  Supprimez la directive de compilateur de votre code source.  
  
     \- ou -  
  
2.  Commentez la directive de compilateur.  
  
    > [!NOTE]
    >  Quand vous êtes prêt pour la compilation, vous pouvez choisir **Générer** dans le menu **Générer**, ou utiliser la méthode de ligne de commande, mais sans taper **d:** pour définir les symboles de compilation conditionnelle.  
  
## <a name="see-also"></a>Voir aussi  
 [Suivi et instrumentation d’applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [Guide pratique pour créer, initialiser et configurer des commutateurs de suivi](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md)   
 [Commutateurs de traçage](../../../docs/framework/debug-trace-profile/trace-switches.md)   
 [Écouteurs de suivi](../../../docs/framework/debug-trace-profile/trace-listeners.md)   
 [Guide pratique pour ajouter des instructions de suivi au code d’application](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [Guide pratique pour définir des variables d’environnement pour la ligne de commande Visual Studio](~/docs/csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)   
 [Guide pratique : appeler le compilateur de ligne de commande](~/docs/visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)

