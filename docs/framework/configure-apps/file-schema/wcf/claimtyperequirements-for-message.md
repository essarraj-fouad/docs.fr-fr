---
title: "&lt;claimTypeRequirements&gt; de &lt;message&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f95c5ecd-abb6-4b77-a6d7-a38727f4a142
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;claimTypeRequirements&gt; de &lt;message&gt;
Spécifie une collection de types de revendications requis.  
  
 La collection est utilisée par le service pour spécifier toutes les revendications obligatoires et facultatives qui doivent se trouver dans le jeton émis que le client utilise pour accéder au service.  Le service expose les types de revendication obligatoires dans les métadonnées si la publication WSDL est activée mais WCF ne requiert pas que le jeton émis contienne les types de revendication spécifiés.  Les services qui souhaitent appliquer l'obligation de présence des types de revendication obligatoires doivent le faire à l'aide de la stratégie d'autorisation.  
  
 Sur les clients fédérés, cette collection contient la liste des revendications obligatoires et facultatives envoyée au service d'émission de jeton de sécurité dans la demande de jeton émis du client.  
  
## Voir aussi  
 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>   
 <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>