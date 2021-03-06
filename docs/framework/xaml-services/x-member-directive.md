---
title: "x:Member Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d8394ef-644c-4331-b6c5-be855d392980
caps.latest.revision: 5
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 5
---
# x:Member Directive
Déclare un membre XAML dans le balisage.  
  
## Utilisation d'éléments objet XAML  
  
```  
  
<object x:Class="className">  
  <x:Members>  
    <x:Member Name="propertyName"/>  
    additionalMembers  
  </x:Members>  
</object>  
```  
  
## Valeurs XAML  
  
|||  
|-|-|  
|`className`|Nom de la classe de stockage ou de la classe partielle pour la production XAML.|  
|`memberName`|Nom de membre de la propriété définie.|  
  
## Notes  
 Dans l'implémentation des services XAML .NET Framework,  `x:Member` n'a pas de stockage de type direct, mais est pris en charge par la classe <xref:System.Windows.Markup.MemberDefinition>.  Dans un flux de nœud XAML, un élément `x:Member` est représenté en tant que membre nommé `Member`, à partir de l'espace de noms XAML du langage XAML.  Le membre `Member` contient les attributs déclarés par le balisage.  
  
 La signification de `Name` et `Type` n’est pas attribuée au niveau des services XAML .NET Framework.  Elles est stockée dans le flux de nœud XAML initial sous forme de valeur de chaîne, afin d’être interprétée ultérieurement selon les règles pouvant être imposées par les infrastructures spécifiques.  La signification peut s'aligner sur celle d'un nom et d'un type XAML, ou être valide uniquement dans un système de type de stockage, selon l'implémentation.  
  
 Pour pouvoir utiliser `x:Members` afin de spécifier des définitions de membre dans le balisage, les membres doivent être associés à une classe modifiable.  Dans le modèle prévu, `x:Members` existe en tant que membre d'un type qui spécifie un objet `x:Class`.  Toutefois, le mécanisme permettant d'associer des types et des membres ou de générer des définitions de membre dynamique n'est pas pris en charge au niveau des services XAML .NET Framework.  En revanche, chaque infrastructure dispose de modèles d'application qui prennent en charge les définitions de membre XAML.  Généralement, les actions de génération MSBUILD qui balisent\-compilent le XAML et, soit lui intègre du code\-behind, soit produisent des assemblys purement XAML, sont nécessaires pour prendre en charge cette fonctionnalité.  
  
## X:Property pour Windows Workflow Foundation  
 Pour Windows Workflow Foundation, `x:Property` définit les membres d'une activité personnalisée entièrement composée en XAML ou des membres dynamiques définis en XAML pour un ActivityDesigner avec code\-behind.  L'objet `x:Class` doit également être spécifié sur l'élément racine de la production XAML.  Cela n'est pas obligatoire dans le cadre des services XAML .NET Framework, mais le devient quand la production XAML est chargée par les actions de génération MSBUILD qui prennent en charge les activités personnalisées et le XAML de Windows Workflow Foundation en général.  Windows Workflow Foundation n'utilise pas le nom de type XAML pur comme valeur prévue pour l'attribut `Type` de `x:Property` et utilise à la place une convention qui n'est pas documentée ici.  Pour plus d'informations, consultez [Création avec DynamicActivity](http://msdn.microsoft.com/library/dd807392.aspx).