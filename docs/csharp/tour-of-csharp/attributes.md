---
title: "Attributs C# - Visite guidée du langage C#"
description: "Découvrir la programmation déclarative à l’aide des attributs en C#"
keywords: .NET, csharp
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 753bcfe2-7ddd-4487-9513-ba70937fc8e9
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5f290b2cb7074d0b442d5971e5e08a0f6cac55ac
ms.contentlocale: fr-fr
ms.lasthandoff: 07/28/2017

---

# <a name="attributes"></a>Attributs

Les types, membres et autres entités d’un programme C# prennent en charge les modificateurs qui contrôlent certains aspects de leur comportement. Par exemple, l’accessibilité d’une méthode est contrôlée à l’aide des modificateurs `public`, `protected`, `internal` et `private`. C# généralise cette fonctionnalité pour que les types d’informations déclaratives définis par l’utilisateur puissent être associés aux entités de programme et récupérés au moment de l’exécution. Les programmes spécifient ces informations déclaratives supplémentaires en définissant et en utilisant les ***attributs***.

L’exemple suivant déclare un attribut `HelpAttribute` qui peut être placé sur des entités de programme pour fournir des liens vers leur documentation associée.

[!code-csharp[AttributeDefined](../../../samples/snippets/csharp/tour/attributes/Program.cs#L3-L20)]

Toutes les classes d’attributs dérivent de la classe de base @System.Attribute fournie par la bibliothèque standard. Les attributs peuvent être appliqués en donnant leur nom, ainsi que les éventuels arguments, à l’intérieur de crochets juste avant la déclaration associée. Si le nom d’un attribut se termine en `Attribute`, cette partie du nom peut être omise lorsque l’attribut est référencé. Par exemple, l’attribut `HelpAttribute` peut être utilisé comme suit.

[!code-csharp[AttributeApplied](../../../samples/snippets/csharp/tour/attributes/Program.cs#L22-L28)]

Cet exemple joint un `HelpAttribute` à la classe `Widget`. Il ajoute un autre `HelpAttribute` à la méthode `Display` dans la classe. Les constructeurs publics d’une classe d’attributs contrôlent les informations qui doivent être fournies lorsque l’attribut est joint à une entité de programme. Des informations supplémentaires peuvent être fournies en référençant les propriétés en lecture-écriture publiques de la classe d’attributs (comme la référence à la propriété `Topic`, précédemment).

Lorsqu’un attribut particulier est demandé par réflexion, le constructeur de la classe d’attributs est appelé avec les informations fournies dans la source du programme, et l’instance d’attribut qui en résulte est retournée. Si des informations supplémentaires ont été fournies via les propriétés, ces propriétés sont définies sur les valeurs données avant que le renvoi de l’instance de l’attribut.

>[!div class="step-by-step"]
[Précédent](delegates.md)

