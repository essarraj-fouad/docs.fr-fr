---
title: "Impl&#233;mentation de m&#233;thode dans les contr&#244;les personnalis&#233;s | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "contrôles utilisateur (Windows Forms), implémentation de la méthode"
  - "contrôles personnalisés (Windows Forms), la surcharge de méthodes"
  - "contrôles personnalisés (Windows Forms), implémentation de la méthode"
  - "méthodes (Windows Forms)"
  - "méthodes (Windows Forms), contrôles personnalisés"
ms.assetid: 35d14fca-4bb4-4a27-8211-1f7a98ea27de
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Impl&#233;mentation de m&#233;thode dans les contr&#244;les personnalis&#233;s
Une méthode est implémentée dans un contrôle comme dans tout autre composant.  
  
 En Visual Basic, si une méthode est nécessaire pour retourner une valeur, elle est implémentée en tant que `Public Function`. Si aucune valeur n'est retournée, elle est implémentée en tant que `Public Sub`. Les méthodes sont déclarées à l'aide de la syntaxe suivante :  
  
```vb  
Public Function ConvertMatterToEnergy(Matter as Integer) As Integer  
   ' Conversion code goes here.  
End Function  
```  
  
 Les fonctions doivent spécifier un type de retour, tel qu'entier, chaîne, objet, etc., car elles retournent une valeur. Le cas échéant, vous devez également spécifier les arguments acceptés par les procédures `Function` ou `Sub`.  
  
 C# ne fait aucune différence entre les fonctions et les procédures, contrairement à Visual Basic. Une méthode retourne une valeur ou `void`. La syntaxe permettant de déclarer une méthode publique C# est la suivante :  
  
```csharp  
public int ConvertMatterToEnergy(int matter)  
{  
   // Conversion code goes here.  
}  
```  
  
 Quand vous déclarez une méthode, déclarez tous ses arguments en tant que types de données explicites, si possible. Les arguments qui acceptent des références d'objet doivent être déclarés comme des types de classe spécifiques : par exemple, `As Widget` au lieu d'`As Object`. En Visual Basic, le paramètre `Option Strict` par défaut applique automatiquement cette règle.  
  
 Les arguments typés permettent au compilateur de détecter de nombreuses erreurs au cours du développement, plutôt qu'au moment de l'exécution. Le compilateur détecte systématiquement les erreurs, tandis que le test au moment de l'exécution est du même niveau qu'une suite de tests.  
  
## <a name="overloaded-methods"></a>Méthodes surchargées  
 Si vous voulez permettre aux utilisateurs que vous contrôlez de fournir des combinaisons différentes de paramètres à une méthode, offrez plusieurs surcharges de la méthode, à l'aide de types de données explicites. Évitez la création de paramètres déclarés `As Object` qui peuvent contenir tout type de données, car cela peut générer des erreurs qui ne seraient pas détectées pendant le test.  
  
> [!NOTE]
>  Le type de données universel du Common Language Runtime est `Object` plutôt que `Variant`. `Variant` a été supprimé du langage.  
  
 Par exemple, la méthode `Spin` d'un hypothétique contrôle `Widget` peut permettre la spécification directe de la direction et de la vitesse de rotation, ou la spécification d'un autre objet `Widget` à partir duquel le moment cinétique doit être absorbé :  
  
```vb  
Overloads Public Sub Spin( _  
   ByVal SpinDirection As SpinDirectionsEnum, _  
   ByVal RevolutionsPerSecond As Double)  
   ' Implementation code here.  
End Sub  
Overloads Public Sub Spin(ByVal Driver As Widget) _  
   ' Implementation code here.  
End Sub  
```  
  
```csharp  
public void Spin(SpinDirectionsEnum spinDirection, double revolutionsPerSecond)  
{  
   // Implementation code here.  
}  
  
public void Spin(Widget driver)  
{  
   // Implementation code here.  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Événements](../../../../docs/standard/events/index.md)   
 [Propriétés dans les contrôles Windows Forms](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)