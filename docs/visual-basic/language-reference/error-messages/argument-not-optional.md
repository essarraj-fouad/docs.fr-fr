---
title: "Argument not optional (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID449"
dev_langs: 
  - "VB"
ms.assetid: 76e7bcf3-24ed-4cd5-945b-b98f1c76944b
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Argument not optional (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Le nombre et les types d'arguments doivent correspondre à ceux qui sont attendus.  Soit le nombre d'arguments est incorrect, soit un argument omis n'est pas facultatif.  Un argument ne peut être omis de l'appel à une procédure définie par l'utilisateur que s'il a été déclaré `Optional` dans la définition de procédure.  
  
### Pour corriger cette erreur  
  
1.  Fournissez tous les arguments nécessaires.  
  
2.  Assurez\-vous que les arguments omis sont facultatifs.  S'ils ne le sont pas, fournissez l'argument dans l'appel ou déclarez le paramètre `Optional` dans la définition.  
  
## Voir aussi  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)