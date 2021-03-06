---
title: "LINQ to SQL avec des applications client-serveur fortement coupl&#233;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e083d805-dcf6-459d-b9af-9ef0563f2dd7
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# LINQ to SQL avec des applications client-serveur fortement coupl&#233;es
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] peut être utilisé sur la couche intermédiaire avec des clients intelligents fortement couplés sur la couche Présentation.  Dans les scénarios qui impliquent l'accès aux données en lecture seule, aucun contrôle d'accès concurrentiel ni accès concurrentiel optimiste avec horodatages, la complexité n'est guère supérieure à celle des scénarios sans accès à distance.  Toutefois, lorsqu'une base de données requiert des contrôles d'accès concurrentiel optimiste avec les valeurs d'origine, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ne fournit pas le niveau de prise en charge pour l'aller\-retour \(round\-trip\) de données que vous trouvez dans DataSets.  Toutefois, une couche intermédiaire [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] peut échanger des données avec les clients sur toutes les plateformes.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dans [!INCLUDE[vs_orcas_long](../../../../../../includes/vs-orcas-long-md.md)] ne fournit aucune infrastructure pour le suivi de l'état des entités après leur sérialisation sur un client.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] active des architectures orientées service où les interactions entre les couches Données et Présentation sont faibles et relativement atomiques, mais n'exécute aucun aller\-retour des valeurs d'origine.  Par conséquent, si vous souhaitez utiliser un client intelligent fortement couplé avec [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] et qu'une base de données utilise l'accès concurrentiel optimiste avec les valeurs d'origine, vous devrez implémenter votre propre mécanisme pour communiquer les modifications entre la couche présentation et la couche intermédiaire.  Il incombe au concepteur de systèmes de décider s'il convient de consentir ce petit effort supplémentaire en échange des avantages fournis par [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sur la couche intermédiaire.  En revanche, si la base de données comporte des horodatages, il n'est pas nécessaire de disposer d'une logique de suivi des modifications personnalisée.  
  
## Voir aussi  
 [Applications multicouches et distantes avec LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [Applications multicouches LINQ to SQL avec les services Web](../../../../../../docs/framework/data/adonet/sql/linq/linq-to-sql-n-tier-with-web-services.md)   
 [Utilisation de groupes de données dans des applications multicouches](../Topic/Work%20with%20datasets%20in%20n-tier%20applications.md)