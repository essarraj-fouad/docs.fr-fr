---
title: "1012 - StartExecuteActivityWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29e9b1c6-c5d7-4b58-b59d-a06a923d3c80
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1012 - StartExecuteActivityWorkItem
## Propriétés  
  
|||  
|-|-|  
|ID|1012|  
|Mots clés|WFRuntime|  
|Niveau|Verbose|  
|Canal|Microsoft\-Windows\-Application Server\-Applications\/Débogage|  
  
## Description  
 Indique qu'un ExecuteActivityWorkItem démarre l'exécution.  
  
## Message  
 Début de l'exécution d'un ExecuteActivityWorkItem pour l'activité « %1 », DisplayName : « %2 », InstanceId : « %3 ».  
  
## Détails  
  
|Nom d'élément de données|Type d'élément de données|Description|  
|------------------------------|-------------------------------|-----------------|  
|Activité|xs:string|Nom de type de l'activité.|  
|DisplayName|xs:string|Nom complet de l'activité.|  
|InstanceId|xs:string|ID d'instance de l'activité.|  
|AppDomain|xs:string|Chaîne retournée par AppDomain.CurrentDomain.FriendlyName.|