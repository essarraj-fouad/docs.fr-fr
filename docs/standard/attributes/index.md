---
title: "Extension des métadonnées à l'aide des attributs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata, extending
- attributes [.NET Framework], metadata
- elements [.NET Framework], attributes
- common language runtime, attributes
- annotating programming elements
- keyword-like descriptive declarations
- runtime, attributes
- extending metadata
ms.assetid: 30386922-1e00-4602-9ebf-526b271a8b87
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c2c8db8b200e38c87d5b79ba3bf6a870bf6640c7
ms.contentlocale: fr-fr
ms.lasthandoff: 09/05/2017

---
# <a name="extending-metadata-using-attributes"></a>Extension des métadonnées à l'aide des attributs
Le common language runtime vous permet d’ajouter des déclarations descriptives de type mot clé, appelées attributs, pour annoter les éléments de programmation comme des types, des champs, des méthodes et des propriétés. Quand vous compilez votre code pour le runtime, il est converti en langage MSIL (Microsoft Intermediate Language) et placé dans un fichier exécutable portable avec des métadonnées générées par le compilateur. Les attributs vous permettent de placer des informations descriptives supplémentaires dans les métadonnées, qui peuvent être extraites à l'aide des services de réflexion du runtime. Le compilateur crée des attributs quand vous déclarez des instances de classes spéciales qui dérivent de <xref:System.Attribute?displayProperty=fullName>.  
  
 Le .NET Framework utilise des attributs pour différentes raisons et pour résoudre un certain nombre de problèmes. Les attributs décrivent comment sérialiser les données, spécifient des caractéristiques qui sont utilisées pour appliquer la sécurité et limitent les optimisations du compilateur juste-à-temps (JIT) pour que le code reste facile à déboguer. Les attributs peuvent également enregistrer le nom d'un fichier ou l'auteur du code, ou bien contrôler la visibilité des contrôles et des membres pendant le développement des formulaires.  
  
## <a name="related-topics"></a>Rubriques connexes  
  
|Titre|Description|  
|-----------|-----------------|  
|[Application des attributs](../../../docs/standard/attributes/applying-attributes.md)|Décrit comment appliquer un attribut à un élément de votre code.|  
|[Écriture des attributs personnalisés](../../../docs/standard/attributes/writing-custom-attributes.md)|Décrit comment concevoir des classes d'attributs personnalisés.|  
|[Récupération des informations stockées dans les attributs](../../../docs/standard/attributes/retrieving-information-stored-in-attributes.md)|Décrit comment récupérer des attributs personnalisés pour le code qui est chargé dans le contexte d'exécution.|  
|[Métadonnées et composants autodescriptifs](../../../docs/standard/metadata-and-self-describing-components.md)|Fournit une vue d'ensemble des métadonnées et décrit comment elles sont implémentées dans un fichier exécutable portable du .NET Framework.|  
|[Guide pratique pour charger des assemblys dans le contexte de réflexion uniquement](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|Explique comment récupérer les informations des attributs personnalisés dans le contexte de réflexion uniquement.|  
  
## <a name="reference"></a>Référence  
 <xref:System.Attribute?displayProperty=fullName>

