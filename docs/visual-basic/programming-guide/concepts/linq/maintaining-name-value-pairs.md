---
title: Maintenance de paires nom-valeur (Visual Basic) | Documents Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 57ac2072-d9f5-432b-84f0-a889c62fd813
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 54db297ecd39e37492dcf8bb4de4f64476662670
ms.lasthandoff: 03/13/2017


---
# <a name="maintaining-namevalue-pairs-visual-basic"></a>Maintenance de paires nom/valeur (Visual Basic)
De nombreuses applications doivent maintenir des informations qu'il est préférable de conserver sous forme de paires nom/valeur. Il peut s'agir d'informations de configuration ou de paramètres globaux. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] contient des méthodes qui facilitent la maintenance d'un ensemble de paires nom/valeur. Vous pouvez conserver les informations en tant qu'attributs ou en tant qu'ensemble d'éléments enfants.  
  
 L'une des différences est qu'il ne peut y avoir qu'un seul attribut avec un nom donné pour un élément. Cette limitation ne s'applique pas aux éléments enfants.  
  
## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue et SetElementValue  
 Les deux méthodes qui facilitent la conservation nom/valeur sont de paires <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>et <xref:System.Xml.Linq.XElement.SetElementValue%2A>.</xref:System.Xml.Linq.XElement.SetElementValue%2A> </xref:System.Xml.Linq.XElement.SetAttributeValue%2A> Ces deux méthodes ont une sémantique similaire.  
  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>peut ajouter, modifier ou supprimer des attributs d’un élément.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>avec un nom d’un attribut qui n’existe pas, la méthode crée un nouvel attribut et l’ajoute à l’élément spécifié.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>avec un nom d’un attribut existant et avec certains spécifié le contenu, le contenu de l’attribut est remplacé par le contenu spécifié.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>avec un nom d’un attribut et spécifiez null pour le contenu, l’attribut est supprimé de son parent.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
 <xref:System.Xml.Linq.XElement.SetElementValue%2A>peut ajouter, modifier ou supprimer des éléments enfants d’un élément.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetElementValue%2A>avec un nom d’un élément enfant qui n’existe pas, la méthode crée un nouvel élément et l’ajoute à l’élément spécifié.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetElementValue%2A>avec un nom d’un élément existant et avec certains spécifié le contenu, le contenu de l’élément est remplacé par le contenu spécifié.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Si vous appelez <xref:System.Xml.Linq.XElement.SetElementValue%2A>avec un nom d’un élément existant et spécifiez une valeur null pour le contenu, l’élément est supprimé de son parent.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
## <a name="example"></a>Exemple  
 L'exemple suivant crée un élément sans attribut. Il utilise ensuite le <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>pour créer et gérer une liste de paires nom/valeur.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as attributes.  
root.SetAttributeValue("Top", 22)  
root.SetAttributeValue("Left", 20)  
root.SetAttributeValue("Bottom", 122)  
root.SetAttributeValue("Right", 300)  
root.SetAttributeValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
  
' Replace the value of Top.  
root.SetAttributeValue("Top", 10)  
Console.WriteLine(root)  
  
' Remove DefaultColor.  
root.SetAttributeValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
```  
  
 Cet exemple génère la sortie suivante :  
  
```  
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" />  
```  
  
## <a name="example"></a>Exemple  
 L'exemple suivant crée un élément sans élément enfant. Il utilise ensuite le <xref:System.Xml.Linq.XElement.SetElementValue%2A>pour créer et gérer une liste de paires nom/valeur.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as elements.  
root.SetElementValue("Top", 22)  
root.SetElementValue("Left", 20)  
root.SetElementValue("Bottom", 122)  
root.SetElementValue("Right", 300)  
root.SetElementValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Replace the value of Top.  
root.SetElementValue("Top", 10)  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Remove DefaultColor.  
root.SetElementValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
  
```  
  
 Cet exemple génère la sortie suivante :  
  
```  
<Root>  
  <Top>22</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
</Root>  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A></xref:System.Xml.Linq.XElement.SetAttributeValue%2A>   
 <xref:System.Xml.Linq.XElement.SetElementValue%2A></xref:System.Xml.Linq.XElement.SetElementValue%2A>   
 [Modification d’arborescences XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
