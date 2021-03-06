---
title: "Proc&#233;dure pas &#224; pas&#160;: utilisation de proc&#233;dures stock&#233;es uniquement (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecde4bf2-fa4d-4252-b5e4-96a46b9e097d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Proc&#233;dure pas &#224; pas&#160;: utilisation de proc&#233;dures stock&#233;es uniquement (C#)
Cette procédure pas à pas fournit un scénario [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] de base de bout en bout pour accéder aux données en exécutant des procédures stockées uniquement.  Cette approche est souvent utilisée par les administrateurs de base de données pour limiter les moyens d'accès au magasin de données.  
  
> [!NOTE]
>  Vous pouvez également utiliser des procédures stockées dans les applications [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] pour substituer le comportement par défaut, plus particulièrement pour les processus `Create`, `Update` et `Delete`.  Pour plus d'informations, consultez [Personnalisation des opérations d'insertion, de mise à jour et de suppression](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
  
 Dans cette procédure pas à pas, vous utiliserez deux méthodes mappées aux procédures stockées dans l'exemple de base de données Northwind : CustOrdersDetail et CustOrderHist.  Le mappage se produit lorsque vous exécutez l'outil en ligne de commande SQLMetal pour générer un fichier C\#.  Pour plus d'informations, consultez la section Composants requis par la suite dans cette procédure pas à pas.  
  
 Cette procédure pas à pas ne s'appuie pas sur le [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)].  Les développeurs qui utilisent [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] peuvent également utiliser le [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] pour implémenter les fonctionnalités de procédure stockée.  Consultez [LINQ to SQL Tools dans Visual Studio](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md).  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Cette procédure pas à pas a été écrite à l'aide des paramètres de développement Visual C\#.  
  
## Composants requis  
 Elle requiert les éléments suivants :  
  
-   Les fichiers sont stockés dans un dossier dédié, c:\\linqtest7.  Vous devez créer ce dossier avant de commencer la procédure pas à pas.  
  
-   Exemple de base de données Northwind.  
  
     Si cette base de données n'est pas disponible sur votre ordinateur de développement, vous pouvez la télécharger à partir du site de téléchargement Microsoft.  Pour obtenir des instructions, consultez [Téléchargement d'exemples de bases de données](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  Après avoir téléchargé la base de données, copiez le fichier northwnd.mdf dans le dossier c:\\linqtest7.  
  
-   Fichier de code C\# généré à partir de la base de données Northwind.  
  
     Cette procédure pas à pas a été écrite à l'aide de l'outil SQLMetal, avec la ligne de commande suivante :  
  
     **sqlmetal \/code:"c:\\linqtest7\\northwind.cs" \/language:csharp "c:\\linqtest7\\northwnd.mdf" \/sprocs \/functions \/pluralize**  
  
     Pour plus d'informations, consultez [SqlMetal.exe \(outil de génération de code\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Vue d'ensemble  
 Cette procédure pas à pas se compose de six tâches principales :  
  
-   Configuration de la solution [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dans [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Ajout de l'assembly System.Data.Linq au projet.  
  
-   Ajout du fichier de code de base de données au projet.  
  
-   Création d'une connexion à la base de données.  
  
-   Configuration de l'interface utilisateur.  
  
-   Exécution et test de l'application.  
  
## Création d'une solution LINQ to SQL  
 Au cours de cette première tâche, vous allez créer une solution [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] qui contient les références nécessaires pour générer et exécuter un projet [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
#### Pour créer une solution LINQ to SQL  
  
1.  Dans le menu **Fichier** de [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
2.  Dans le volet **Types de projets** de la boîte de dialogue **Nouveau projet**, cliquez sur **Visual C\#**.  
  
3.  Dans le volet **Modèles**, cliquez sur **Application Windows Forms**.  
  
4.  Dans la zone **Nom**, tapez SprocOnlyApp.  
  
5.  Dans la zone **Emplacement**, vérifiez où vous souhaitez stocker vos fichiers projet.  
  
6.  Cliquez sur **OK**.  
  
     Le Concepteur Windows Forms s'ouvre.  
  
## Ajout de la référence à l'assembly LINQ to SQL  
 L'assembly [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] n'est pas inclus dans le modèle Application Windows Forms standard.  Vous devrez ajouter l'assembly vous\-même, comme expliqué dans les étapes suivantes :  
  
#### Pour ajouter System.Data.Linq.dll  
  
1.  Dans l'**Explorateur de solutions**, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Ajouter une référence**.  
  
2.  Dans la boîte de dialogue **Ajouter une référence**, cliquez sur **.NET**, sur l'assembly System.Data.Linq, puis sur **OK**.  
  
     L'assembly est ajouté au projet.  
  
## Ajout du fichier de code Northwind au projet  
 Ces étapes supposent que vous avez utilisé l'outil SQLMetal pour générer un fichier de code à partir de l'exemple de base de données Northwind.  Pour plus d'informations, consultez la section Composants requis au début de cette procédure pas à pas.  
  
#### Pour ajouter le fichier de code Northwind au projet  
  
1.  Dans le menu **Projet**, cliquez sur **Ajouter un élément existant**.  
  
2.  Dans la boîte de dialogue **Ajouter un élément existant**, accédez à c:\\linqtest7\\northwind.cs, puis cliquez sur **Ajouter**.  
  
     Le fichier northwind.cs est ajouté au projet.  
  
## Création d'une connexion à une base de données  
 Au cours de cette étape, vous allez définir la connexion à l'exemple de base de données Northwind.  Cette procédure pas à pas utilise "c:\\linqtest7\\northwnd.mdf" comme chemin d'accès.  
  
#### Pour créer la connexion de base de données  
  
1.  Dans l'**Explorateur de solutions**, cliquez avec le bouton droit sur **Form1.cs**, puis cliquez sur **Afficher le code**.  
  
2.  Tapez le code suivant dans la classe `Form1` :  
  
     [!code-csharp[DLinqWalk4CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#1)]  
  
## Configuration de l'interface utilisateur.  
 Au cours de cette tâche, vous configurez une interface afin que les utilisateurs puissent exécuter des procédures stockées pour accéder aux données dans la base de données.  Dans les applications que vous développez avec cette procédure pas à pas, les utilisateurs peuvent accéder aux données dans la base de données uniquement en utilisant les procédures stockées incorporées dans l'application.  
  
#### Pour configurer l'interface utilisateur  
  
1.  Revenez dans le Concepteur Windows Forms **Form1.cs\[Design\]**.  
  
2.  Dans le menu **Affichage**, cliquez sur **Boîte à outils**.  
  
     La boîte à outils s'ouvre.  
  
    > [!NOTE]
    >  Cliquez sur la punaise **Masquer automatiquement** pour garder la boîte à outils ouverte pendant que vous effectuez les autres étapes de cette section.  
  
3.  Faites glisser deux boutons, deux zones de texte et deux étiquettes de la boîte à outils sur **Form1**.  
  
     Disposez les contrôles comme dans l'illustration associée.  Développez **Form1** afin que les contrôles s'ajustent facilement.  
  
4.  Cliquez avec le bouton droit sur **label1**, puis cliquez sur **Propriétés**.  
  
5.  Modifiez la propriété **Text** de **label1** en **Enter OrderID:**.  
  
6.  De la même façon pour **label2**, modifiez la propriété **Text** de **label2** en **Enter CustomerID:**.  
  
7.  De la même façon, modifiez la propriété **Text** de **button1** en **Order Details**.  
  
8.  Modifiez la propriété **Text** de **button2** en **Order History**.  
  
     Élargissez les contrôles boutons afin que tout le texte soit visible.  
  
#### Pour gérer des clics de bouton  
  
1.  Double\-cliquez sur **Order Details** sur **Form1** pour ouvrir le gestionnaire d'événements button1 dans l'éditeur de code.  
  
2.  Tapez le code suivant dans le gestionnaire d'événements `button1` :  
  
     [!code-csharp[DLinqWalk4CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#2)]  
  
3.  Double\-cliquez maintenant sur **button2** sur **Form1** pour ouvrir le gestionnaire `button2`.  
  
4.  Tapez le code suivant dans le gestionnaire d'événements `button2` :  
  
     [!code-csharp[DLinqWalk4CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#3)]  
  
## Test de l'application  
 Vous allez maintenant tester votre application.  Notez que votre contact avec le magasin de données est limité aux actions que les deux procédures stockées peuvent accepter.  Ces actions consistent à retourner les produits inclus pour n'importe quel orderID que vous entrez ou à retourner un historique des produits commandés pour n'importe quel CustomerID que vous entrez.  
  
#### Pour tester l'application  
  
1.  Appuyez sur F5 pour démarrer le débogage.  
  
     Form1 s'affiche.  
  
2.  Dans la zone **Enter OrderID**, tapez `10249`, puis cliquez sur **Order Details**.  
  
     Un message répertorie les produits inclus dans la commande 10249.  
  
     Cliquez sur **OK** pour fermer le message.  
  
3.  Dans la zone **Enter CustomerID**, tapez `ALFKI`, puis cliquez sur **Order History**.  
  
     Le message qui apparaît répertorie l'historique des commandes pour le client ALFKI.  
  
     Cliquez sur **OK** pour fermer le message.  
  
4.  Dans la zone **Enter OrderID**, tapez `123`, puis cliquez sur **Order Details**.  
  
     Le message suivant s'affiche : « Aucun résultat ».  
  
     Cliquez sur **OK** pour fermer le message.  
  
5.  Dans le menu **Déboguer**, cliquez sur **Arrêter le débogage**.  
  
     La session de débogage s'arrête.  
  
6.  Si vous avez terminé les tests, vous pouvez cliquer sur **Fermer le projet** dans le menu **Fichier** et enregistrer votre projet lorsque vous êtes invité à le faire.  
  
## Étapes suivantes  
 Vous pouvez améliorer ce projet en apportant des modifications.  Par exemple, vous pouvez répertorier les procédures stockées disponibles dans une zone de liste et demander à l'utilisateur de sélectionner les procédures à exécuter.  Vous pouvez également transmettre en continu la sortie des rapports dans un fichier texte.  
  
## Voir aussi  
 [Apprentissage par les procédures pas à pas](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)   
 [Procédures stockées](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)