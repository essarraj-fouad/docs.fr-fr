---
title: "Comment&#160;: appeler des op&#233;rations de fa&#231;on asynchrone &#224; l&#39;aide d&#39;une fabrication de canal | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Comment&#160;: appeler des op&#233;rations de fa&#231;on asynchrone &#224; l&#39;aide d&#39;une fabrication de canal
Cette rubrique décrit comment un client peut accéder de façon asynchrone à une opération de service lors de l'utilisation d'une application cliente basée sur <xref:System.ServiceModel.ChannelFactory%601>.  \(Lors de l'utilisation d'un objet <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName> pour appeler un service, vous pouvez utiliser le modèle d'appel asynchrone commandé par événement.  Pour plus d'informations, consultez [Comment : appeler des opérations de service de façon asynchrone](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).  Pour plus d'informations sur l'utilisation du modèle d'appel asynchrone basé sur événement, consultez [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md).  
  
 Le service dans cette rubrique implémente l'interface `ICalculator`.  Le client peut appeler les opérations sur cette interface de façon asynchrone, ce qui signifie que des opérations telles que `Add` sont divisées en deux méthodes : `BeginAdd` et `EndAdd`, la première initiant l'appel et la seconde récupérant le résultat au terme de l'opération.  Pour obtenir un exemple illustrant comment implémenter une opération de façon asynchrone dans un service, consultez [Comment : implémenter une opération de service asynchrone](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md).  Pour plus d'informations sur les opérations synchrones et asynchrones, consultez [Opérations synchrones et asynchrones](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
## Procédure  
  
#### Pour appeler des opérations de service WCF de façon asynchrone  
  
1.  Exécutez l'outil [Outil Service Model Metadata Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) en définissant l'option `/async` tel qu'affichée dans la commande suivante.  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
  
    ```  
  
     Cela génère une version cliente asynchrone du contrat de service pour l'opération.  
  
2.  Créez une fonction de rappel à appeler au terme de l'opération asynchrone en vous conformant à l'exemple de code suivant.  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3.  Pour accéder de façon asynchrone à une opération de service, créez le client, puis appelez la méthode `Begin[Operation]` \(par exemple, `BeginAdd`\) et spécifiez une fonction de rappel en vous conformant à l'exemple de code suivant.  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     Lors de l'exécution de la fonction de rappel, le client appelle la méthode `End<operation>` \(par exemple, `EndAdd`\) pour récupérer le résultat.  
  
## Exemple  
 Le service utilisé avec le code client utilisé dans la procédure précédente implémente l'interface `ICalculator` comme affiché dans le code suivant.  Du côté service, les opérations `Add` et `Subtract` du contrat sont appelées de façon synchrone par le temps d'exécution [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], bien que les étapes clientes précédentes soient appelées de façon asynchrone sur le client.  Les opérations `Multiply` et `Divide` sont utilisées pour appeler de façon asynchrone le service du côté service, même si le client les appelle de façon synchrone.  Cet exemple affecte la propriété <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> à `true`.  Ce paramètre de propriété, ainsi que l'implémentation du modèle asynchrone du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] indiquent au temps d'exécution d'appeler l'opération de façon asynchrone.  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
  
## Voir aussi  
 [Service Contract: Asynchronous Sample](http://msdn.microsoft.com/fr-fr/833db946-f511-4f64-a26f-2759a11217c7)