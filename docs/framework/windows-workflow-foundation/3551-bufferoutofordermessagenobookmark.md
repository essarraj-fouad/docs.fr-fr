---
title: "3551 - BufferOutOfOrderMessageNoBookmark | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7930d6c4-c843-4a83-933a-cecd71b80d1e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3551 - BufferOutOfOrderMessageNoBookmark
## Propriétés  
  
|||  
|-|-|  
|ID|3551|  
|Mots clés|WFServices|  
|Niveau|Information|  
|Canal|Microsoft\-Windows\-Application Server\-Applications\/Analyse|  
  
## Description  
 Indique qu'une reprise de signet a échoué.  Une autre tentative d'opération de réception en mémoire tampon sera faite lorsque l'instance de service sera prête à traiter cette opération.  
  
## Message  
 Impossible d'effectuer actuellement l'opération « %2 » sur l'instance de service « %1 ».  Une autre tentative sera faite lorsque l'instance de service sera prête à traiter cette opération.  
  
## Détails  
  
|Nom d'élément de données|Type d'élément de données|Description|  
|------------------------------|-------------------------------|-----------------|  
|OperationName|xs:string|Nom de l'opération.|  
|ServiceInstanceId|xs:string|ID de l'instance du service.|  
|AppDomain|xs:string|Chaîne retournée par AppDomain.CurrentDomain.FriendlyName.|