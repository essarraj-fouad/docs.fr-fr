---
title: "Comment&#160;: afficher l&#39;aide contextuelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Aide F1, dans des boîtes de dialogue"
  - "formulaires, afficher l'aide"
  - "Aide, ajouter aux boîtes de dialogue"
  - "Aide, aide contextuelle"
  - "HelpProvider (composant Windows Forms)"
  - "boîtes de dialogue modales, aide contextuelle"
  - "aide contextuelle"
  - "Windows Forms, afficher l'aide"
ms.assetid: 218aa81e-e87e-4d67-af05-11627bbdce3b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Comment&#160;: afficher l&#39;aide contextuelle
L'une des manières d'afficher l'Aide sur Windows Forms consiste à utiliser le bouton **Aide** situé sur le côté droit de la barre de titre, accessible via la propriété <xref:System.Windows.Forms.Form.HelpButton%2A>.  Ce type d'affichage de l'aide convient parfaitement aux boîtes de dialogue.  Les boîtes de dialogue modales \(affichées avec la méthode <xref:System.Windows.Forms.Form.ShowDialog%2A>\) ont des difficultés à afficher les systèmes d'aide externes, car elles doivent être fermées pour que le focus puisse basculer vers une autre fenêtre.  En outre, l'utilisation du bouton **Aide** exige qu'aucun bouton **Réduire** ou **Agrandir** ne soit affiché dans la barre de titre.  Il s'agit d'une convention standard pour les boîtes de dialogue, alors que les formulaires possèdent généralement des boutons **Réduire** et **Agrandir**.  
  
 Sachez que vous pouvez également utiliser le composant <xref:System.Windows.Forms.HelpProvider> pour lier des contrôles à des fichiers d'un système d'aide, même si vous avez implémenté l'aide contextuelle.  Pour plus d'informations, consultez [Fourniture d'aide dans une application Windows](../../../../docs/framework/winforms/advanced/how-to-provide-help-in-a-windows-application.md).  
  
> [!NOTE]
>  Les boîtes de dialogue et les commandes de menu qui s'affichent peuvent être différentes de celles qui sont décrites dans l'aide, en fonction de vos paramètres actifs ou de l'édition utilisée.  Pour modifier vos paramètres, choisissez **Importation et exportation de paramètres** dans le menu **Outils**.  Pour plus d'informations, consultez [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/fr-fr/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Pour afficher une aide contextuelle  
  
1.  Faites glisser un composant [HelpProvider](../../../../docs/framework/winforms/controls/helpprovider-component-windows-forms.md) de la boîte à outils vers votre formulaire.  
  
     Il sera placé dans la barre d'état en bas du Concepteur Windows Forms.  
  
2.  Dans la fenêtre Propriétés, affectez la valeur `true` à la propriété <xref:System.Windows.Forms.Form.HelpButton%2A>.  Ceci affichera un bouton avec un point d'interrogation sur le côté droit de la barre de titre du formulaire.  
  
3.  Pour que le <xref:System.Windows.Forms.Form.HelpButton%2A> soit affiché, il faut que les propriétés <xref:System.Windows.Forms.Form.MinimizeBox%2A> et <xref:System.Windows.Forms.Form.MaximizeBox%2A> du formulaire aient la valeur `false`, que la propriété <xref:System.Windows.Forms.Form.ControlBox%2A> ait la valeur `true` et que la propriété <xref:System.Windows.Forms.Form.FormBorderStyle%2A> ait l'une des valeurs suivantes : <xref:System.Windows.Forms.FormBorderStyle>, <xref:System.Windows.Forms.FormBorderStyle>, <xref:System.Windows.Forms.FormBorderStyle> ou <xref:System.Windows.Forms.FormBorderStyle>.  
  
4.  Sélectionnez le contrôle pour lequel vous souhaitez afficher l'aide sur votre formulaire et définissez la chaîne d'aide dans la fenêtre Propriétés.  Il s'agit de la chaîne de texte qui sera affichée dans une fenêtre similaire à une [info\-bulle](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md).  
  
5.  Appuyez sur **F5**.  
  
6.  Appuyez sur le bouton **Aide** dans la barre de titre et cliquez sur le contrôle sur lequel vous avez défini la chaîne d'aide.  
  
## Voir aussi  
 [Affichage sous forme d'info\-bulles de l'aide relative aux contrôles](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md)   
 [Intégration de l'aide d'utilisateur dans les Windows Forms](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Windows Forms](../../../../docs/framework/winforms/index.md)