---
title: "Forum Aux Questions | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 252ed666-0679-4eea-b71b-2f14117ef443
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Forum Aux Questions
Les sections suivantes fournissent des réponses à quelques problèmes courants que vous êtes susceptible de rencontrer lors de l'implémentation de [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  
  
 D'autres problèmes sont traités dans [Résolution des problèmes](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md).  
  
## Impossible de se connecter  
 Q.  Je ne peux pas me connecter à ma base de données.  
  
 Un fichier .  Vérifiez que votre chaîne de connexion est correcte et que votre instance [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] s'exécute.  Notez également que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] requiert l'activation du protocole Named Pipes.  Pour plus d'informations, consultez [Apprentissage par les procédures pas à pas](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
## Modifications de la base de données perdues  
 Q.  J'ai apporté une modification à des données dans la base de données, mais lorsque j'exécute de nouveau mon application, cette modification a disparu.  
  
 Un fichier .  Assurez\-vous que vous appelez <xref:System.Data.Linq.DataContext.SubmitChanges%2A> pour enregistrer les résultats dans la base de données.  
  
## Connexion à la base de données : durée de l'ouverture  
 Q.  Pendant combien de temps ma connexion à la base de données reste\-t\-elle ouverte ?  
  
 Un fichier .  Une connexion reste généralement ouverte jusqu'à ce que vous utilisiez les résultats de la requête.  Si vous prévoyez que le traitement de tous les résultats risque de prendre du temps et que vous n'êtes pas opposé à la mise en cache des résultats, appliquez <xref:System.Linq.Enumerable.ToList%2A> à la requête.  Dans les scénarios courants où chaque objet est traité une seule fois, le modèle de diffusion en continu est supérieur à la fois dans `DataReader` et [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 Les détails exacts d'utilisation de la connexion dépendent des éléments suivants :  
  
-   l'état de la connexion si le <xref:System.Data.Linq.DataContext> est généré avec un objet de connexion ;  
  
-   les paramètres de chaîne de connexion \(par exemple, activation de MARS \(Multiple Active Result Sets\)\).  Pour plus d'informations, consultez [Ensembles de résultats actifs multiples \(MARS\)](../../../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md).  
  
## Mise à jour sans interrogation  
 Q.  Est\-ce que je peux mettre à jour des données de table sans interroger d'abord la base de données ?  
  
 Un fichier .  Bien que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ne comporte pas de commandes de mise à jour reposant sur un jeu, vous pouvez utiliser l'une des techniques suivantes pour effectuer une mise à jour sans exécuter de requête préalable :  
  
-   Utilisez <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> pour envoyer le code SQL.  
  
-   Créez une nouvelle instance de l'objet et initialisez toutes les valeurs actuelles \(champs\) qui affectent la mise à jour.  Puis attachez l'objet au <xref:System.Data.Linq.DataContext> à l'aide de <xref:System.Data.Linq.Table%601.Attach%2A> et modifiez le champ que vous souhaitez changer.  
  
## Résultats de requête inattendus  
 Q.  Ma requête retourne des résultats inattendus.  Comment vérifier ce qui se produit ?  
  
 Un fichier .  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fournit plusieurs outils permettant d'inspecter le code SQL qu'il génère.  L'un des plus importants est <xref:System.Data.Linq.DataContext.Log%2A>.  Pour plus d'informations, consultez [Prise en charge du débogage](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md).  
  
## Résultats de procédure stockée inattendus  
 Q.  J'ai une procédure stockée dont la valeur de retour est calculée par `MAX()`.  Lorsque je fais glisser la procédure stockée vers la surface [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)], la valeur de retour n'est pas correcte.  
  
 Un fichier .  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fournit deux manières de retourner des valeurs générées par la base de données au moyen de procédures stockées :  
  
-   en nommant le résultat de sortie ;  
  
-   en spécifiant explicitement un paramètre de sortie.  
  
 Un exemple de sortie incorrecte est fourni ci\-dessous.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ne pouvant pas mapper les résultats, il retourne toujours 0 :  
  
 `create procedure proc2`  
  
 `as`  
  
 `begin`  
  
 `select max(i) from t where name like 'hello'`  
  
 `end`  
  
 Un exemple de sortie correcte à l'aide d'un paramètre de sortie est fourni ci\-dessous :  
  
 `create procedure proc2`  
  
 `@result int OUTPUT`  
  
 `as`  
  
 `select @result = MAX(i) from t where name like 'hello'`  
  
 `go`  
  
 Un exemple de sortie correcte à l'aide du nommage du résultat de sortie est fourni ci\-dessous :  
  
 `create procedure proc2`  
  
 `as`  
  
 `begin`  
  
 `select nax(i) AS MaxResult from t where name like 'hello'`  
  
 `end`  
  
 Pour plus d'informations, consultez [Personnalisation d'opérations à l'aide de procédures stockées](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md).  
  
## Erreurs de sérialisation  
 Q.  Lorsque je tente d'effectuer une sérialisation, j'obtiens l'erreur suivante : "Le type 'System.Data.Linq.ChangeTracker\+StandardChangeTracker' ...  n'est pas marqué comme sérialisable.".  
  
 Un fichier .  La génération de code dans [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] prend en charge la sérialisation <xref:System.Runtime.Serialization.DataContractSerializer>.  Elle ne prend pas en charge <xref:System.Xml.Serialization.XmlSerializer> ni <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.  Pour plus d'informations, consultez [Sérialisation](../../../../../../docs/framework/data/adonet/sql/linq/serialization.md).  
  
## Plusieurs fichiers DBML  
 Q.  Lorsque j'ai plusieurs fichiers DBML qui partagent des tables en commun, j'obtiens une erreur du compilateur.  
  
 Un fichier .  Attribuez aux propriétés **Context Namespace** et **Entity Namespace** du [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] une valeur distincte pour chaque fichier DBML.  Cette approche permet d'éliminer la collision de nom et d'espace de noms.  
  
## Éviter la définition explicite des valeurs générées par une base de données pour l'insertion ou la mise à jour  
 Q.  J'ai une table de base de données comportant une colonne `DateCreated` qui a comme valeur par défaut SQL `Getdate()`.  Lorsque j'essaie d'insérer un nouvel enregistrement à l'aide de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], la valeur devient `NULL`.  Il me semble qu'elle devrait être la valeur par défaut de la base de données.  
  
 Un fichier .  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] gère automatiquement cette situation pour les colonnes identity \(incrémentation automatique\), rowguidcol \(GUID généré par la base de données\) et timestamp.  Dans les autres cas, vous devez définir manuellement les propriétés <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>\=`true` et <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A>\=<xref:System.Data.Linq.Mapping.AutoSync>\/<xref:System.Data.Linq.Mapping.AutoSync>\/<xref:System.Data.Linq.Mapping.AutoSync>.  
  
## Plusieurs options de chargement de données  
 Q.  Puis\-je spécifier des options de chargement supplémentaires sans remplacer la première ?  
  
 Un fichier .  Oui.  La première n'est pas remplacée, comme dans l'exemple suivant :  
  
```vb  
Dim dlo As New DataLoadOptions()  
dlo.LoadWith(Of Order)(Function(o As Order) o.Customer)  
dlo.LoadWith(Of Order)(Function(o As Order) o.OrderDetails)  
```  
  
```csharp  
DataLoadOptions dlo = new DataLoadOptions();  
dlo.LoadWith<Order>(o => o.Customer);  
dlo.LoadWith<Order>(o => o.OrderDetails);  
```  
  
## Erreurs lors de l'utilisation de SQL Compact 3.5  
 Q.  J'obtiens une erreur lorsque je fais glisser des tables hors d'une base de données [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)].  
  
 Un fichier .  Le [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] ne prend pas en charge [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)], alors que c'est le cas du runtime [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Dans ce cas, vous devez créer vos propres classes d'entité et ajouter les attributs appropriés.  
  
## Erreurs dans les relations d'héritage  
 Q.  J'ai utilisé la forme de l'héritage de la boîte à outils dans [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] pour connecter deux entités, mais j'obtiens des erreurs.  
  
 Un fichier .  Il ne suffit pas de créer la relation.  Vous devez fournir des informations telles que la colonne du discriminateur, la valeur du discriminateur de la classe de base et la valeur du discriminateur de la classe dérivée.  
  
## Modèle de fournisseur  
 Q.  Un modèle de fournisseur public est\-il disponible ?  
  
 Un fichier .  Aucun modèle de fournisseur public n'est disponible.  Actuellement, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] prend en charge uniquement [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] et [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)].  
  
## Attaques par injection de code SQL  
 Q.  Comment [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] est\-il protégé contre les attaques par injection de code SQL ?  
  
 Un fichier .  L'injection de code SQL est un risque significatif pour les requêtes SQL traditionnelles formées par la concaténation de l'entrée d'utilisateur.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] évite cette injection en utilisant <xref:System.Data.SqlClient.SqlParameter> dans les requêtes.  L'entrée d'utilisateur est transformée en valeurs de paramètre.  Cette technique empêche l'utilisation de commandes malveillantes à partir de l'entrée d'utilisateur.  
  
## Modification de l'indicateur de lecture seule dans les fichiers DBML  
 Q.  Comment faire pour éliminer les accesseurs Set de certaines propriétés lorsque je crée un modèle à partir d'un fichier DBML ?  
  
 Un fichier .  Effectuez la procédure suivante pour ce scénario avancé :  
  
1.  Dans le fichier .dbml, modifiez la propriété en changeant l'indicateur <xref:System.Data.Linq.ITable.IsReadOnly%2A> en `True`.  
  
2.  Ajoutez une classe partielle.  Créez un constructeur avec des paramètres pour les membres en lecture seule.  
  
3.  Vérifiez la valeur par défaut de <xref:System.Data.Linq.Mapping.UpdateCheck> \(<xref:System.Data.Linq.Mapping.UpdateCheck>\) pour déterminer si elle convient pour votre application.  
  
    > [!CAUTION]
    >  Si vous utilisez [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] dans [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], vos modifications peuvent être remplacées.  
  
## APTCA  
 Q.  System.Data.Linq est\-il marqué pour être utilisé par du code d'un niveau de confiance partiel ?  
  
 Un fichier .  Oui, l'assembly System.Data.Linq.dll figure parmi ces assemblys [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] marqués par l'attribut <xref:System.Security.AllowPartiallyTrustedCallersAttribute>.  Sans ce marquage, les assemblys contenus dans [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] sont conçus uniquement pour être utilisés par du code d'un niveau de confiance suffisant.  
  
 Le scénario principal dans [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] pour l'autorisation des appelants d'un niveau de confiance partiel consiste à permettre l'accès de l'assembly [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] à partir des applications Web, où la configuration de la *confiance* est Moyenne.  
  
## Mappage de données à partir de plusieurs tables  
 Q.  Les données de mon entité proviennent de plusieurs tables.  Comment faire pour les mapper ?  
  
 Un fichier .  Vous pouvez créer une vue dans une base de données et mapper l'entité à la vue.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] génère pour les vues le même SQL que pour les tables.  
  
> [!NOTE]
>  L'utilisation des vues dans ce scénario comporte des limitations.  Cette technique est plus sûre lorsque les opérations exécutées sur <xref:System.Data.Linq.Table%601> sont prises en charge par la vue sous\-jacente.  Vous êtes le seul à connaître les opérations prévues.  Par exemple, la plupart des applications sont en lecture seule, et un autre nombre important d'applications exécutent des opérations `Create`\/`Update`\/`Delete` uniquement à l'aide de procédures stockées sur des vues.  
  
## Regroupement de connexions  
 Q.  Existe\-t\-il une construction pouvant aider au regroupement <xref:System.Data.Linq.DataContext> ?  
  
 Un fichier .  N'essayez pas de réutiliser des instances de <xref:System.Data.Linq.DataContext>.  Chaque <xref:System.Data.Linq.DataContext> gère l'état \(y compris un cache d'identité\) d'une session de modification\/requête particulière.  Pour obtenir des nouvelles instances basées sur l'état actuel de la base de données, utilisez un nouveau <xref:System.Data.Linq.DataContext>.  
  
 Vous pouvez néanmoins utiliser le pool de connexions [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] sous\-jacent.  Pour plus d'informations, consultez [Regroupement de connexions SQL Server \(ADO.NET\)](../../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
## Le second DataContext n'est pas mis à jour  
 Q.  J'ai utilisé une instance de <xref:System.Data.Linq.DataContext> pour stocker des valeurs dans la base de données.  Toutefois, un second <xref:System.Data.Linq.DataContext> sur la même base de données ne reflète pas les valeurs mises à jour.  La seconde instance <xref:System.Data.Linq.DataContext> paraît retourner des valeurs mises en cache.  
  
 Un fichier .  Ce comportement est inhérent à la conception.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] continue à retourner les mêmes instances\/valeurs que vous avez vues dans la première instance.  Lorsque vous effectuez des mises à jour, vous utilisez l'accès concurrentiel optimiste.  Les données d'origine sont utilisées pour effectuer la comparaison avec l'état actuel de la base de données afin de vérifier qu'il n'a en fait pas été modifié.  S'il a été modifié, un conflit se produit et votre application doit le résoudre.  L'une des options de votre application consiste à réinitialiser l'état d'origine à l'état actuel de la base de données et à retenter la mise à jour.  Pour plus d'informations, consultez [Procédure : gérer les conflits de changement](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
 Vous pouvez également attribuer à <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> la valeur false, ce qui désactive la mise en cache et le suivi des modifications.  Vous pouvez ensuite extraire les valeurs les plus récentes chaque fois que vous exécutez une requête.  
  
## Impossible d'appeler SubmitChanges en mode lecture seule  
 Q.  Lorsque j'essaie d'appeler <xref:System.Data.Linq.DataContext.SubmitChanges%2A> en mode lecture seule, j'obtiens une erreur.  
  
 Un fichier .  Le mode lecture seule désactive la capacité du contexte à suivre les modifications.  
  
## Voir aussi  
 [Reference](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)   
 [Résolution des problèmes](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md)   
 [Sécurité dans LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md)