---
title: "MSMQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9fca29f-fa44-4ec4-bb48-b10800694500
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# MSMQ
Dans une application MSMQ, aucune activité supplémentaire n'est transférée du canal mis en file d'attente vers MSMQ et de MSMQ vers le canal mis en file d'attente.  
  
 De plus, l'ID de message MSMQ et l'ID de message SOAP \(ainsi que l'ID d'activité, s'il existe\) sont suivis dans le cadre des suivis de canaux mis en file d'attente lors d'une opération d'envoi.  
  
 L'ID de message MSMQ et l'ID de message SOAP \(ainsi que l'ID d'activité, s'il existe\) sont suivis dans le cadre des suivis de canaux mis en file d'attente lors d'une opération de réception.  
  
 Les transferts requis au cours de l'opération de réception sont exécutés de la même façon que tout autre transport \(réception d'octets\-\>traitement du message\-\>opération\).