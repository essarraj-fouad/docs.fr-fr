---
title: "Vue d&#39;ensemble d&#39;ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Vue d&#39;ensemble d&#39;ADO.NET
ADO.NET propose un accès cohérent à des sources de données, telles que SQL Server et XML, ainsi qu'à des sources de données exposées via OLE DB et ODBC.  Des applications grand public de partage de données peuvent utiliser ADO.NET pour se connecter à des sources de données et extraire, manipuler et mettre à jour les données qu'elles contiennent.  
  
 ADO.NET sépare l'accès aux données de leur manipulation en composants distincts qui peuvent être utilisés individuellement ou en tandem.  ADO.NET comprend des fournisseurs de données .NET Framework pour la connexion à une base de données, l'exécution de commandes et l'extraction de résultats.  Ces résultats sont traités directement, placés dans un objet <xref:System.Data.DataSet> ADO.NET pour pouvoir être exposés à l'utilisateur de manière adéquate, combinés aux données de différentes sources ou passées entre couches.  L'objet `DataSet`peut également être utilisé indépendamment d'un fournisseur de données .NET Framework pour gérer des données locales pour l'application ou provenant de XML.  
  
 Les classes ADO.NET se trouvent dans System.Data.dll et sont intégrées aux classes XML de System.Xml.dll.  Pour obtenir un exemple de code permettant de se connecter à une base de données, d'en récupérer des données et de les afficher dans une fenêtre de console, consultez [Exemples de code ADO.NET](../../../../docs/framework/data/adonet/ado-net-code-examples.md).  
  
 ADO.NET offre aux développeurs écrivant du code managé une fonctionnalité similaire à celle offerte aux développeurs de COM \(Component Object Model\) natif par ActiveX Data Objects \(ADO\).  Nous vous recommandons d'utiliser ADO.NET, pas ADO, pour accéder aux données dans vos applications .NET.  
  
 ADO.NET fournit la méthode la plus directe d'accès aux données dans le .NET Framework.  Pour un niveau supérieur d'abstraction permettant aux applications de travailler sur un modèle conceptuel au lieu du modèle de stockage sous\-jacent, consultez le [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md).  
  
 **Déclaration de confidentialité** : Les assemblys System.Data.dll, System.Data.Design.dll, System.Data.OracleClient.dll, System.Data.SqlXml.dll, System.Data.Linq.dll, System.Data.SqlServerCe.dll et System.Data.DataSetExtensions.dll ne distinguent pas les données privées de l'utilisateur des données non privées.  Ces assemblys ne collectent pas les données privées d'un utilisateur, ne les stockent pas et ne les transportent pas.  Toutefois, les applications tierces peuvent collecter, stocker ou transporter les données privées d'un utilisateur à l'aide de ces assemblys.  
  
## Dans cette section  
 [Architecture ADO.NET](../../../../docs/framework/data/adonet/ado-net-architecture.md)  
 Propose une vue d'ensemble de l'architecture et des composants d'ADO.NET.  
  
 [Options et directives concernant la technologie ADO.NET](../../../../docs/framework/data/adonet/ado-net-technology-options-and-guidelines.md)  
 Décrit les produits et les technologies livrés avec la plateforme de données d'entité \(Entity Data Platform\).  
  
 [LINQ et ADO.NET](../../../../docs/framework/data/adonet/linq-and-ado-net.md)  
 Décrit comment les requêtes LINQ \(Language\-Integrated Query\) sont implémentées dans ADO.NET et propose des liens vers les rubriques associées.  
  
 [Fournisseur de données .NET Framework](../../../../docs/framework/data/adonet/data-providers.md)  
 Propose une vue d'ensemble du design du fournisseur de données .NET Framework et des fournisseurs de données .NET Framework inclus dans ADO.NET.  
  
 [Datasets ADO.NET](../../../../docs/framework/data/adonet/ado-net-datasets.md)  
 Fournit une vue d'ensemble du design et des composants du `DataSet`.  
  
 [Exécution côte à côte dans ADO.NET](../../../../docs/framework/data/adonet/side-by-side-execution.md)  
 Présente les différences des versions successives d'ADO.NET et leur incidence sur l'exécution côte à côte et la compatibilité des applications.  
  
 [Exemples de code ADO.NET](../../../../docs/framework/data/adonet/ado-net-code-examples.md)  
 Fournit des exemples de code qui récupèrent des données à l'aide des fournisseurs de données ADO.NET.  
  
## Rubriques connexes  
 [Nouveautés dans ADO.NET](../../../../docs/framework/data/adonet/whats-new.md)  
 Introduit des fonctions nouvelles dans [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)].  
  
 [Sécurisation des applications ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 Décrit des pratiques de codage sécurisées dans ADO.NET.  
  
 [Mappages de types de données dans ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)  
 Décrit les mappages de types de données entre les fournisseurs de données .NET Framework et les types de données .NET Framework.  
  
 [Extraction et modification de données dans ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 Explique comment se connecter à une source de données, récupérer des données et modifier des données, notamment  des `DataReaders` et des `DataAdapters`.  
  
## Voir aussi  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Accès aux données dans Visual Studio](../Topic/Accessing%20data%20in%20Visual%20Studio.md)   
 [Fournisseurs managés ADO.NET et Centre de développement de DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)