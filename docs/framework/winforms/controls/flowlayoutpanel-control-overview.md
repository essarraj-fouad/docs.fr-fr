---
title: "Vue d&#39;ensemble du contr&#244;le FlowLayoutPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "FlowLayoutPanel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "FlowLayoutPanel (contrôle Windows Forms), à propos du contrôle FlowLayoutPanel"
  - "formulaires, présentation dynamique"
  - "disposition (Windows Forms), dynamique"
  - "Windows Forms, présentation dynamique"
ms.assetid: 3883e024-f5a0-456d-9c27-b4dfa1cc9045
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Vue d&#39;ensemble du contr&#244;le FlowLayoutPanel
Le contrôle <xref:System.Windows.Forms.FlowLayoutPanel> réorganise son contenu dans un sens de flux horizontal ou vertical.  Vous pouvez encapsuler le contenu du contrôle d'une ligne à la suivante ou d'une colonne à la suivante.  Vous pouvez également ajuster plutôt qu'encapsuler son contenu.  
  
 Vous pouvez spécifier le sens du flux en définissant la valeur de la propriété <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>.  Le contrôle <xref:System.Windows.Forms.FlowLayoutPanel> inverse correctement son sens du flux dans les dispositions de droite à gauche \(RTL, Right\-to\-Left\).  Vous pouvez également spécifier si le contenu du contrôle <xref:System.Windows.Forms.FlowLayoutPanel> est encapsulé ou coupé en définissant la valeur de la propriété <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A>.  
  
 Le contrôle <xref:System.Windows.Forms.FlowLayoutPanel> prend automatiquement une dimension adaptée à son contenu quand vous affectez la valeur `true` à la propriété <xref:System.Windows.Forms.Control.AutoSize%2A>.  Il fournit également une propriété **FlowBreak** à ses contrôles enfants.  L'affectation de la valeur `true` à la propriété FlowBreak fait en sorte que le contrôle <xref:System.Windows.Forms.FlowLayoutPanel> cesse de disposer les contrôles dans le sens du flux actuel et qu'il encapsule à la ligne ou la colonne suivante.  
  
 Tout contrôle Windows Forms peut être un enfant du contrôle <xref:System.Windows.Forms.FlowLayoutPanel>, y compris d'autres instances de <xref:System.Windows.Forms.FlowLayoutPanel>.  Avec cette fonctionnalité, vous pouvez construire des dispositions sophistiquées qui s'adaptent aux dimensions de votre formulaire au moment de l'exécution.  
  
 Consultez également [Procédure pas à pas : organisation des contrôles dans les Windows Forms à l'aide d'un FlowLayoutPanel](http://msdn.microsoft.com/library/z9w7ek2f%20\(v=vs.110\)).  
  
## Voir aussi  
 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [FlowLayoutPanel, contrôle](../../../../docs/framework/winforms/controls/flowlayoutpanel-control-windows-forms.md)