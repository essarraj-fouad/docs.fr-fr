---
title: "1021 - ScheduleBookmarkWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e0da311-b219-4637-9460-90cdafcc4ecd
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1021 - ScheduleBookmarkWorkItem
## Propriétés  
  
|||  
|-|-|  
|ID|1021|  
|Mots clés|WFRuntime|  
|Niveau|Verbose|  
|Canal|Microsoft\-Windows\-Application Server\-Applications\/Débogage|  
  
## Description  
 Indique qu'un BookmarkWorkItem a été planifié.  
  
## Message  
 BookmarkWorkItem a été planifié pour l'activité « %1 », DisplayName : « %2 », InstanceId : « %3 ». BookmarkName : %4, BookmarkScope : %5.  
  
## Détails  
  
|Nom d'élément de données|Type d'élément de données|Description|  
|------------------------------|-------------------------------|-----------------|  
|Activité|xs:string|Nom de type de l'activité.|  
|DisplayName|xs:string|Nom complet de l'activité.|  
|InstanceId|xs:string|ID d'instance de l'activité.|  
|BookmarkName|xs:string|Nom du signet.|  
|BookmarkScope|xs:string|Portée du signet.|  
|AppDomain|xs:string|Chaîne retournée par AppDomain.CurrentDomain.FriendlyName.|