---
title: "Biblioth&#232;que d&#39;activit&#233;s | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5323e9d4-71d6-47eb-bfa6-31feac62044d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Biblioth&#232;que d&#39;activit&#233;s
Cette section contient des exemples qui illustrent des activités personnalisées avancées dans [!INCLUDE[wf](../../../../includes/wf-md.md)].  
  
## Dans cette section  
 [Activité de stratégie dans .NET Framework 4.5](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md)  
 Montre comment l'activité Policy4 permet que des objets <xref:System.Workflow.Activities.Rules.RuleSet> de [!INCLUDE[wf2](../../../../includes/wf2-md.md)] dans [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF 3.5\) soient utilisés dans [!INCLUDE[wf2](../../../../includes/wf2-md.md)] dans [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF 4.5\) directement à l'aide du moteur de règles fourni dans WF 3.5.  
  
 [Activité personnalisée pour commuter une plage de valeurs](../../../../docs/framework/windows-workflow-foundation/samples/custom-activity-to-switch-on-a-range-of-values.md)  
 Montre comment créer une activité personnalisée qui étend l'utilisation d'un <xref:System.Activities.Statements.Switch%601>.  
  
 [Activité LINQ to Objects](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-objects-activity.md)  
 Montre comment créer une activité pour utiliser LINQ to Objects pour interroger des éléments d'une collection.  
  
 [LINQ to SQL](../../../../docs/framework/windows-workflow-foundation/samples/linq-to-sql-sample.md)  
 Montre comment créer une activité pour utiliser des entités de requêtes LINQ to SQL de tables dans des bases de données SQL Server.  
  
 [Utilisation de l'activité InvokePowerShell](../../../../docs/framework/windows-workflow-foundation/samples/using-the-invokepowershell-activity.md)  
 Montre comment appeler des commandes Windows PowerShell à l'aide de l'activité InvokePowerShell.  
  
 [Activité RangeEnumeration](../../../../docs/framework/windows-workflow-foundation/samples/rangeenumeration-activity.md)  
 Montre comment créer une activité personnalisée qui itère au sein d'une collection de nombres.  
  
 [Activités d'expression régulière](../../../../docs/framework/windows-workflow-foundation/samples/regular-expression-activities.md)  
 Montre comment créer un ensemble d'activités qui exposent la fonctionnalité d'expression régulière de l'espace de noms <xref:System.Text.RegularExpressions>.  
  
 [Activité personnalisée SendMail](../../../../docs/framework/windows-workflow-foundation/samples/sendmail-custom-activity.md)  
 Montre comment créer une activité personnalisée dérivée de <xref:System.Activities.AsyncCodeActivity> pour envoyer du courrier à l'aide de SMTP afin de l'utiliser dans une application de workflow.  
  
 [Activité For](../../../../docs/framework/windows-workflow-foundation/samples/for-activity.md)  
 Montre comment générer une activité personnalisée qui hérite de <xref:System.Activities.NativeActivity> et l'utilise dans un workflow pour itérer au sein d'une plage de valeurs.  
  
 [Activité Wait For Input](../../../../docs/framework/windows-workflow-foundation/samples/wait-for-input-activity.md)  
 Montre comment créer des signets nommés dans un workflow.  
  
 [ParallelForEach limité](../../../../docs/framework/windows-workflow-foundation/samples/throttled-parallel-foreach.md)  
 Montre comment l'activité `ThrottleParallelForEach` est semblable à l'activité <xref:System.Activities.Statements.ParallelForEach%601> hormis le seul fait qu'elle permet la définition d'un facteur de concurrence pour restreindre le nombre de branches simultanées à exécuter.  
  
 [Activités d'entités](../../../../docs/framework/windows-workflow-foundation/samples/entity-activities.md)  
 Montre comment utiliser ADO.NET Entity Framework avec [!INCLUDE[wf2](../../../../includes/wf2-md.md)] pour simplifier l'accès aux données.  
  
 [Activités d'accès aux bases de données](../../../../docs/framework/windows-workflow-foundation/samples/database-access-activities.md)  
 Montre comment créer des activités qui permettent d'utiliser [ADO.NET](http://go.microsoft.com/fwlink/?LinkId=166081) pour accéder à des bases de données afin de récupérer ou de modifier des informations.  
  
 [Activité CommentOut](../../../../docs/framework/windows-workflow-foundation/samples/commentout-activity.md)  
 Montre comment écrire une activité personnalisée qui supprime d'autres activités du chemin d'exécution, en les transformant en fait en commentaire.  
  
 [Activité de stratégie externalisée dans .NET Framework 4.5](../../../../docs/framework/windows-workflow-foundation/samples/externalized-policy-activity-in-net-framework-4-5.md)  
 Montre comment l'activité ExternalizedPolicy4 permet que des objets <xref:System.Workflow.Activities.Rules.RuleSet> existants de [!INCLUDE[wf2](../../../../includes/wf2-md.md)] dans [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF 3.5\) soient exécutés dans [!INCLUDE[wf2](../../../../includes/wf2-md.md)] dans [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF 4.5\) directement à l'aide du moteur de règles fourni dans WF 3.5.  
  
 [Activité NoPersistScope](../../../../docs/framework/windows-workflow-foundation/samples/nopersistscope-activity.md)  
 Montre comment manipuler un état non sérialisable et pouvant être supprimé dans un workflow.  
  
 [ForEach non générique](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-foreach.md)  
 Montre comment créer une version non générique de l'activité <xref:System.Activities.Statements.ForEach%601>.  
  
 [ParallelForEach non générique](../../../../docs/framework/windows-workflow-foundation/samples/non-generic-parallelforeach.md)  
 Montre comment créer une version non générique de l'activité <xref:System.Activities.Statements.ParallelForEach%601>.  
  
 [Obtenir WorkflowInstanceId](../../../../docs/framework/windows-workflow-foundation/samples/get-workflowinstanceid.md)  
 Montre comment utiliser l'activité personnalisée `GetWorkflowInstanceId` pour retourner l'ID d'instance de workflow.