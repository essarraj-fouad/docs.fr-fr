---
title: "Sessions and Queues | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47d7c5c2-1e6f-4619-8003-a0ff67dcfbd6
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# Sessions and Queues
Cet exemple montre comment envoyer et recevoir un ensemble de messages connexes dans une communication en file d'attente sur le transport \(Message Queuing ou MSMQ\).Cet exemple utilise la liaison `netMsmqBinding`.Le service est une application console auto\-hébergée qui vous permet d'observer le service qui reçoit les messages mis en file d'attente.  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération correspondant à cet exemple figurent en fin de rubrique.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page \(éventuellement en anglais\) des [exemples Windows Communication Foundation \(WCF\) et Windows Workflow Foundation \(WF\) pour .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Session`  
  
 Dans le cadre d'une communication en file d'attente, le client communique avec le service à l'aide d'une file d'attente.Cela signifie que le client envoie ses messages à cette file d'attente.Le service reçoit ensuite ces messages de la file d'attente.Par conséquent, dans le cadre d'une communication en file d'attente, il n'est pas nécessaire que le service et le client s'exécutent simultanément.  
  
 Quelquefois, un client envoie un ensemble de messages connexes dans un groupe.Lorsque les messages doivent être traités ensemble ou dans un ordre spécifié, une file d'attente peut être utilisée pour les regrouper, afin qu'ils soient traités par une application de réception unique.Cela est particulièrement important lorsqu'il existe plusieurs applications de réception sur un groupe de serveurs et qu'il est nécessaire de garantir qu'un groupe de messages sera traité par la même application de réception.Les sessions mises en file d'attente sont un mécanisme utilisé pour envoyer et recevoir un ensemble de messages connexes qui doivent être traités en une fois.Les sessions mises en file d'attente requièrent qu'une transaction expose ce modèle.  
  
 Dans l'exemple, le client envoie plusieurs messages au service dans le cadre d'une session, dans une étendue de transaction unique.  
  
 Le contrat de service est `IOrderTaker`, qui définit un service monodirectionnel pouvant être utilisé avec des files d'attente.Le <xref:System.ServiceModel.SessionMode> utilisé dans le contrat illustré dans l'exemple de code suivant indique que les messages font partie de la session.  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required)]  
public interface IOrderTaker  
{  
    [OperationContract(IsOneWay = true)]  
    void OpenPurchaseOrder(string customerId);  
  
    [OperationContract(IsOneWay = true)]  
    void AddProductLineItem(string productId, int quantity);  
  
    [OperationContract(IsOneWay = true)]  
    void EndPurchaseOrder();  
}  
  
```  
  
 Le service définit des opérations de service de manière à ce que la première opération s'inscrive dans une transaction mais ne complète pas automatiquement la transaction.Les opérations suivantes s'inscrivent également dans la même transaction mais ne se complètent pas automatiquement.La dernière opération de la session complète automatiquement la transaction.Donc, la même transaction est utilisée pour plusieurs appels d'opération dans le contrat de service.Si chacune des opérations lève une exception, la transaction est restaurée et la session est remise dans la file d'attente.À l'achèvement réussi de la dernière opération, la transaction est validée.Le service utilise `PerSession` comme <xref:System.ServiceModel.InstanceContextMode> pour recevoir tous les messages dans une session sur la même instance du service.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class OrderTakerService : IOrderTaker  
{  
    PurchaseOrder po;  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                 TransactionAutoComplete = false)]  
    public void OpenPurchaseOrder(string customerId)  
    {  
        Console.WriteLine("Creating purchase order");  
        po = new PurchaseOrder(customerId);  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                  TransactionAutoComplete = false)]  
    public void AddProductLineItem(string productId, int quantity)  
    {  
        po.AddProductLineItem(productId, quantity);  
        Console.WriteLine("Product " + productId + " quantity " +   
                            quantity + " added to purchase order");  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                  TransactionAutoComplete = true)]  
    public void EndPurchaseOrder()  
    {  
       Console.WriteLine("Purchase Order Completed");  
       Console.WriteLine();  
       Console.WriteLine(po.ToString());  
    }  
}  
```  
  
 Le service est auto\-hébergé.Lors de l'utilisation du transport MSMQ, la file d'attente utilisée doit être créée au préalable.Cela peut s'effectuer manuellement ou via le code.Dans cet exemple, le service contient le code <xref:System.Messaging> pour vérifier l'existence de la file d'attente et la crée si besoin.Le nom de la file d'attente est lu depuis le fichier de configuration à l'aide de la classe <xref:System.Configuration.ConfigurationManager.AppSettings%2A>.  
  
```  
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Get MSMQ queue name from app settings in configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
  
    // Create a ServiceHost for the OrderTakerService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderTakerService)))  
    {  
        // Open the ServiceHost to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
  
        // Close the ServiceHost to shutdown the service.  
        serviceHost.Close();   
    }  
}  
```  
  
 Le nom de la file d'attente MSMQ est spécifié dans la section appSettings du fichier de configuration.Le point de terminaison pour le service est défini dans la section system.serviceModel du fichier de configuration et spécifie la liaison `netMsmqBinding`.  
  
```  
<appSettings>  
  <!-- Use appSetting to configure MSMQ queue name. -->  
  <add key="queueName" value=".\private$\ServiceModelSamplesSession" />  
</appSettings>  
  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.OrderTakerService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      ...  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesSession"  
                binding="netMsmqBinding"  
                contract="Microsoft.ServiceModel.Samples.IOrderTaker" />  
      ...  
    </service>  
  </services>  
  ...  
<system.serviceModel>  
  
```  
  
 Le client crée une étendue de transaction.Tous les messages dans la session sont envoyés à la file d'attente dans l'étendue de transaction, traitée comme une unité atomique dans laquelle tous les messages réussissent ou échouent.La transaction est validée en appelant <xref:System.Transactions.TransactionScope.Complete%2A>.  
  
```  
//Create a transaction scope.  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
{  
    // Create a client with given client endpoint configuration.  
    OrderTakerClient client = new OrderTakerClient("OrderTakerEndpoint");  
    // Open a purchase order.  
    client.OpenPurchaseOrder("somecustomer.com");  
    Console.WriteLine("Purchase Order created");  
  
    // Add product line items.  
    Console.WriteLine("Adding 10 quantities of blue widget");  
    client.AddProductLineItem("Blue Widget", 10);  
  
    Console.WriteLine("Adding 23 quantities of red widget");  
    client.AddProductLineItem("Red Widget", 23);  
  
    // Close the purchase order.  
    Console.WriteLine("Closing the purchase order");  
    client.EndPurchaseOrder();  
  
    //Closing the client gracefully closes the connection and cleans up resources.  
    client.Close();                  
  
    // Complete the transaction.  
    scope.Complete();  
}  
  
```  
  
> [!NOTE]
>  Vous pouvez utiliser une seule transaction pour tous les messages dans la session et tous les messages dans la session doit être envoyés avant de valider la transaction.La fermeture du client entraîne la fermeture de la session.Par conséquent, le client doit être fermé avant que la transaction soit terminée pour envoyer tous les messages dans la session à la file d'attente.  
  
 Lorsque vous exécutez l'exemple, les activités du client et du service s'affichent dans leurs fenêtres de console respectives.Vous pouvez voir le service recevoir des messages du client.Appuyez sur ENTER dans chaque fenêtre de console pour arrêter le service et le client.Notez qu'en raison de l'utilisation de la mise en file d'attente, il n'est pas nécessaire que le service et le client s'exécutent simultanément.Vous pouvez exécuter le client, l'arrêter, puis démarrer le service et il recevra encore ses messages.  
  
 Sur le client.  
  
```  
Purchase Order created  
Adding 10 quantities of blue widget  
Adding 23 quantities of red widget  
Closing the purchase order  
  
Press <ENTER> to terminate client.  
```  
  
 Sur le service.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Creating purchase order  
Product Blue Widget quantity 10 added to purchase order  
Product Red Widget quantity 23 added to purchase order  
Purchase Order Completed  
  
Purchase Order: 7c86fef0-2306-4c51-80e6-bcabcc1a6e5e  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 10 of Blue Widget @unit price: $2985  
                Order LineItem: 23 of Red Widget @unit price: $156  
        Total cost of this order: $33438  
        Order status: Pending  
```  
  
### Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez\-vous d'avoir effectué la [Procédure d'installation unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l'édition C\#, C\+\+ ou Visual Basic .NET de la solution, suivez les instructions indiquées dans [Génération des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Pour exécuter l'exemple dans une configuration à un ou plusieurs ordinateurs, suivez les instructions indiquées dans [Exécution des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Avec <xref:System.ServiceModel.NetMsmqBinding>, la sécurité du transport est activée par défaut.Il existe deux propriétés pertinentes pour la sécurité de transport MSMQ, à savoir <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> et <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>`.` Par défaut, le mode d'authentification a la valeur `Windows` et le niveau de protection a la valeur `Sign`.Pour que MSMQ fournisse la fonction d'authentification et de signature, il doit faire partie d'un domaine et l'option d'intégration d'Active Directory doit être installée pour MSMQ.Si vous exécutez cet exemple sur un ordinateur qui ne satisfait pas ces critères vous recevez une erreur.  
  
### Pour exécuter l'exemple sur un ordinateur joint à un groupe de travail ou sans intégration Active Directory  
  
1.  Si votre ordinateur ne fait pas partie d'un domaine ou ne dispose pas de l'intégration Active Directory, désactivez la sécurité de transport en affectant au mode d'authentification et niveau de protection la valeur `None` comme indiqué dans l'exemple de configuration suivant.  
  
    ```  
    <system.serviceModel>  
      <services>  
        <service name="Microsoft.ServiceModel.Samples.OrderTakerService"  
                 behaviorConfiguration="OrderTakerServiceBehavior">  
          <host>  
            <baseAddresses>  
              <add baseAddress=  
             "http://localhost:8000/ServiceModelSamples/service"/>  
            </baseAddresses>  
          </host>  
          <!-- Define NetMsmqEndpoint -->  
          <endpoint  
              address=  
            "net.msmq://localhost/private/ServiceModelSamplesSession"  
              binding="netMsmqBinding"  
              bindingConfiguration="Binding1"  
           contract="Microsoft.ServiceModel.Samples.IOrderTaker" />  
          <!-- The mex endpoint is exposed at-->      
          <!--http://localhost:8000/ServiceModelSamples/service/mex. -->  
          <endpoint address="mex"  
                    binding="mexHttpBinding"  
                    contract="IMetadataExchange" />  
        </service>  
      </services>  
  
      <bindings>  
        <netMsmqBinding>  
          <binding name="Binding1">  
            <security mode="None" />  
          </binding>  
        </netMsmqBinding>  
      </bindings>  
  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="OrderTakerServiceBehavior">  
              <serviceMetadata httpGetEnabled="True"/>  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    ```  
  
2.  Assurez\-vous de modifier la configuration sur le serveur et le client avant d'exécuter l'exemple.  
  
    > [!NOTE]
    >  L'affectation de `None` au mode de sécurité revient à affecter `None` à la sécurité <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> et `Message`.  
  
## Voir aussi