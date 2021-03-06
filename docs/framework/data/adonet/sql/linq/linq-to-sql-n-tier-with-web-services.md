---
title: "Applications multicouches LINQ to SQL avec les services Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Applications multicouches LINQ to SQL avec les services Web
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] est spécialement conçu pour être utilisé sur la couche intermédiaire d'une couche Data Access faiblement couplée telle qu'un service Web.  Si la couche Présentation est une page Web ASP.NET, vous utilisez le contrôle serveur Web <xref:System.Web.UI.WebControls.LinqDataSource> pour gérer le transfert de données entre l'interface utilisateur et [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sur la couche intermédiaire.  Si la couche de présentation n'est pas une page ASP.NET, la couche intermédiaire et la couche de présentation doivent exécuter des tâches supplémentaires pour gérer la sérialisation et la désérialisation des données.  
  
## Configuration de LINQ to SQL sur la couche intermédiaire  
 Dans un service Web ou une application multicouche, la couche intermédiaire contient le contexte des données et les classes d'entité.  Vous pouvez créer ces classes manuellement, ou à l'aide de SQLMetal.exe ou d'[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)], comme décrit dans une autre partie de la documentation.  Au moment du design, vous pouvez choisir de rendre les classes d'entité sérialisables.  Pour plus d'informations, consultez [Procédure : rendre les entités sérialisables](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md).  Vous avez également la possibilité de créer un ensemble de classes distinct qui encapsule les données à sérialiser, puis de le projeter en types sérialisables lorsque vous retournez les données dans vos requêtes [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  
  
 Vous définissez ensuite l'interface avec les méthodes que les clients appelleront pour extraire, insérer et mettre à jour les données.  Ces méthodes d'interface encapsulent vos requêtes [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  Vous pouvez utiliser tout type de mécanisme de sérialisation pour gérer les appels de méthode distants et la sérialisation de données.  La seule contrainte à respecter est la suivante : si votre modèle objet comporte des relations circulaires ou bidirectionnelles, comme entre Customers et Orders dans le modèle objet Northwind standard, vous devez utiliser un sérialiseur qui le prend en charge.  The Windows Communication Foundation \(WCF\) <xref:System.Runtime.Serialization.DataContractSerializer> prend en charge les relations bidirectionnelles, mais ce n'est pas le cas de XmlSerializer qui est utilisé avec des services Web autres que WCF. Si vous choisissez d'utiliser le XmlSerializer, vous devez vous assurer que votre modèle objet ne comporte pas de relations cycliques.  
  
 Pour plus d'informations sur Windows Communication Foundation, consultez [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../Topic/Windows%20Communication%20Foundation%20Services%20and%20WCF%20Data%20Services%20in%20Visual%20Studio.md).  
  
 Implémentez vos règles métier ou toute autre logique spécifique au domaine en utilisant les classes et méthodes partielles sur <xref:System.Data.Linq.DataContext> et les classes d'entité pour le raccordement aux événements d'exécution de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Pour plus d'informations, consultez [Implémentation de la logique métier multicouche](../../../../../../docs/framework/data/adonet/sql/linq/implementing-business-logic-linq-to-sql.md).  
  
## Définition des types sérialisables  
 Le niveau client ou la couche Présentation doit comporter des définitions de type pour les classes qu'elle recevra de la couche intermédiaire.  Ces types peuvent être les classes d'entité elles\-mêmes ou des classes spéciales qui encapsulent uniquement certains champs des classes d'entité pour la communication à distance.  Dans tous les cas, la manière dont la couche de présentation acquiert ces définitions de type est totalement indifférente pour [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Par exemple, la couche de présentation peut utiliser WCF pour générer les types automatiquement, ou elle peut posséder une copie d'une DLL dans laquelle ces types sont définis, ou elle peut simplement définir sa propre version des types.  
  
## Récupération et insertion de données  
 La couche intermédiaire définit une interface qui spécifie la manière dont la couche Présentation accède aux données.  Par exemple, `GetProductByID(int productID)` ou `GetCustomers()`.  Sur la couche intermédiaire, le corps de méthode crée en général une nouvelle instance du <xref:System.Data.Linq.DataContext>, exécute une requête sur une ou plusieurs de ses tables.  La couche intermédiaire retourne ensuite le résultat sous la forme de <xref:System.Collections.Generic.IEnumerable%601>, où `T` est une classe d'entité ou un autre type utilisé pour la sérialisation.  La couche Présentation n'envoie ni ne reçoit jamais directement de variables de requête vers la couche intermédiaire ou à partir de celle\-ci.  Les deux couches échangent des valeurs, des objets et des collections de données concrètes.  Après qu'elle a reçu une collection, la couche Présentation peut utiliser [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] to Objects pour effectuer des requêtes si nécessaire.  
  
 Lors de l'insertion de données, la couche Présentation peut générer un nouvel objet et l'envoyer à la couche intermédiaire, ou peut donner à la couche intermédiaire l'instruction de créer l'objet d'après les valeurs qu'elle fournit.  En général, la récupération et l'insertion de données dans les applications multicouches ne diffèrent pas beaucoup du processus exécuté dans les applications à deux couches.  Pour plus d’informations, consultez [Interrogation de la base de données](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md) et [Apport et soumission de modifications de données](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md).  
  
## Suivi des modifications pour les mises à jour et les suppressions  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] prend en charge l'accès concurrentiel optimiste selon les horodatages \(également nommés RowVersions\) et les valeurs d'origine.  Si les tables de base de données contiennent des horodatages, les mises à jour et les suppressions requièrent peu de tâches supplémentaires sur la couche intermédiaire et la couche Présentation.  Toutefois, si vous devez utiliser des valeurs d'origine pour les contrôles d'accès concurrentiel optimiste, la couche Présentation est chargée du suivi de ces valeurs et de leur renvoi en cas de mises à jour.  En effet, les modifications apportées aux entités sur la couche Présentation ne sont pas suivies sur la couche intermédiaire.  En fait, la récupération initiale d'une entité et sa mise à jour éventuelle sont généralement effectuées par deux instances entièrement distinctes du <xref:System.Data.Linq.DataContext>.  
  
 Plus le nombre des modifications effectuées par la couche Présentation est élevé, plus le suivi de ces modifications et leur renvoi sur la couche intermédiaire sont complexes.  L'implémentation d'un mécanisme permettant de communiquer les modifications est entièrement à la charge de l'application.  La seule exigence est que les valeurs d'origine requises pour les contrôles d'accès concurrentiel optimiste doivent être fournies à [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 Pour plus d'informations, consultez [Récupération de données et opérations CUD dans les applications multicouches \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md).  
  
## Voir aussi  
 [Applications multicouches et distantes avec LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [NIB: LinqDataSource Web Server Control Overview](http://msdn.microsoft.com/fr-fr/104cfc3f-7385-47d3-8a51-830dfa791136)