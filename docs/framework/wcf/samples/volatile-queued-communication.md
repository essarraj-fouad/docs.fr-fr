---
title: "Volatile Queued Communication | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d012f64-51c7-41d0-8e18-c756f658ee3d
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Volatile Queued Communication
Cet exemple montre comment procéder à la communication de messages volatils mis en file d'attente sur le transport MSMQ \(Message Queuing\).Il utilise <xref:System.ServiceModel.NetMsmqBinding>.Dans le cas présent, le service est une application console auto\-hébergée qui vous permet d'observer le service qui reçoit les messages mis en file d'attente.  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent en fin de rubrique.  
  
 Dans le cadre d'une communication en file d'attente, le client communique avec le service à l'aide d'une file d'attente.Cela signifie que le client envoie ses messages à cette file d'attente.Le service reçoit ensuite ces messages de la file d'attente.Par conséquent, il n'est pas nécessaire que le service et le client s'exécutent simultanément pour communiquer à l'aide d'une file d'attente.  
  
 Lorsque vous envoyez un message sans assurances, MSMQ fait seulement de son mieux pour remettre le message, contrairement aux assurances Exactly Once selon lesquelles MSMQ garantit que le message est remis ou, s'il ne peut pas être remis, vous fait savoir que le message ne peut pas être remis.  
  
 Dans certains scénarios, vous pouvez envoyer un message volatil sans assurances sur une file d'attente, lorsque la remise en temps opportun est plus importante que la perte des messages.Les messages volatils ne survivent pas aux pannes du gestionnaire de files d'attente.Par conséquent si le gestionnaire de files d'attente tombe en panne, la file d'attente non transactionnelle utilisée pour stocker des messages volatils survit mais pas les messages eux\-mêmes car ils ne sont pas stockés sur le disque.  
  
> [!NOTE]
>  Vous ne pouvez pas envoyer de messages volatils sans assurances dans l'étendue d'une transaction à l'aide de MSMQ.Vous devez également créer une file d'attente non transactionnelle pour envoyer des messages volatils.  
  
 Le contrat de service dans cet exemple est `IStockTicker`, qui définit les services unidirectionnels les mieux adaptés à une utilisation avec mise en file d'attente.  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
public interface IStockTicker  
{  
    [OperationContract(IsOneWay = true)]  
    void StockTick(string symbol, float price);  
}  
  
```  
  
 L'opération de service affiche le symbole de cotation et le cours des titres boursiers, comme le montre l'exemple de code suivant :  
  
```  
public class StockTickerService : IStockTicker  
{  
    public void StockTick(string symbol, float price)  
    {  
        Console.WriteLine("Stock Tick {0}:{1} ", symbol, price);  
     }  
     …  
}  
  
```  
  
 Le service est auto\-hébergé.Lors de l'utilisation du transport MSMQ, la file d'attente utilisée doit être créée au préalable.Cela peut s'effectuer manuellement ou via le code.Dans cet exemple, le service contient du code pour vérifier pour l'existence de la file d'attente et la créer si besoin.Le nom de la file d'attente est lu depuis le fichier de configuration.L'adresse de base est utilisée par l'[Outil Service Model Metadata Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) pour générer le proxy pour le service.  
  
```  
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Get MSMQ queue name from app settings in configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName);  
  
    // Create a ServiceHost for the StockTickerService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(StockTickerService)))  
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
  
> [!NOTE]
>  Le nom de la file d'attente comprend un point \(.\) pour l'ordinateur local et des barre obliques inverses dans son chemin d'accès lors de la création d'une file d'attente à l'aide de <xref:System.Messaging>.L'adresse du point de terminaison [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] spécifie un modèle net.msmq: et utilise « localhost » pour l'ordinateur local et des barres obliques dans son chemin d'accès.  
  
 Les assurances et la durabilité ou la volatilité des messages sont également spécifiées dans la configuration.  
  
```  
<appSettings>  
  <!-- use appSetting to configure MSMQ queue name -->  
  <add key="queueName" value=".\private$\ServiceModelSamplesVolatile" />  
</appSettings>  
  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.StockTickerService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
    ...  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"  
                binding="netMsmqBinding"  
                bindingConfiguration="volatileBinding"   
                contract="Microsoft.ServiceModel.Samples.IStockTicker" />  
    ...  
          </service>  
  </services>  
  
  <bindings>  
    <netMsmqBinding>  
      <binding name="volatileBinding"   
             durable="false"  
           exactlyOnce="false"/>  
    </netMsmqBinding>  
  </bindings>  
  ...  
</system.serviceModel>  
  
```  
  
 Étant donné que l'exemple envoie des messages mis en file d'attente en utilisant une file d'attente non transactionnelle, les messages traités ne peuvent pas être envoyés à la file d'attente.  
  
```  
// Create a client.  
Random r = new Random(137);  
  
StockTickerClient client = new StockTickerClient();  
  
float price = 43.23F;  
for (int i = 0; i < 10; i++)  
{  
    float increment = 0.01f * (r.Next(10));  
    client.StockTick("zzz" + i, price + increment);  
}  
  
//Closing the client gracefully cleans up resources.  
client.Close();  
  
```  
  
 Lorsque vous exécutez l'exemple, les activités du client et du service s'affichent à la fois sur la console du service et du client.Vous pouvez voir le service recevoir des messages du client.Appuyez sur ENTER dans chaque fenêtre de console pour arrêter le service et le client.Notez qu'en raison de l'utilisation de la mise en file d'attente, il n'est pas nécessaire que le service et le client s'exécutent simultanément.Vous pouvez exécuter le client, l'arrêter, puis démarrer le service et il recevra encore ses messages.  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Stock Tick zzz0:43.25  
Stock Tick zzz1:43.23  
Stock Tick zzz2:43.28  
Stock Tick zzz3:43.3  
Stock Tick zzz4:43.23  
Stock Tick zzz5:43.25  
Stock Tick zzz6:43.25  
Stock Tick zzz7:43.24  
Stock Tick zzz8:43.32  
Stock Tick zzz9:43.3  
```  
  
### Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez\-vous d'avoir effectué la procédure indiquée à la section [Procédure d'installation unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l'édition C\# ou Visual Basic .NET de la solution, suivez les instructions indiquées dans [Génération des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Pour exécuter l'exemple dans une configuration à un ou plusieurs ordinateurs, suivez les instructions indiquées dans [Exécution des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Avec <xref:System.ServiceModel.NetMsmqBinding>, la sécurité du transport est activée par défaut.Il y a deux propriétés pertinentes pour la sécurité de transport MSMQ, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> et <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>`.` Par défaut, le mode d'authentification a la valeur `Windows` et le niveau de protection a la valeur `Sign`.Pour que MSMQ fournisse la fonction d'authentification et de signature, il doit faire partie d'un domaine et l'option d'intégration d'Active Directory doit être installée pour MSMQ.Si vous exécutez cet exemple sur un ordinateur qui ne satisfait pas ces critères vous recevez une erreur.  
  
### Pour exécuter l'exemple sur un ordinateur joint à un groupe de travail ou sans intégration Active Directory  
  
1.  Si votre ordinateur ne fait pas partie d'un domaine ou ne dispose pas de l'intégration Active Directory, désactivez la sécurité de transport en affectant au mode d'authentification et au niveau de protection la valeur `None` comme indiqué dans l'exemple de code de configuration suivant :  
  
    ```  
    <system.serviceModel>  
        <services>  
          <service name="Microsoft.ServiceModel.Samples.StockTickerService"  
                   behaviorConfiguration="StockTickerServiceBehavior">  
            <host>  
              <baseAddresses>  
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
              </baseAddresses>  
            </host>  
  
            <!-- Define NetMsmqEndpoint -->  
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"  
                      binding="netMsmqBinding"  
                      bindingConfiguration="volatileBinding"   
                      contract="Microsoft.ServiceModel.Samples.IStockTicker" />  
            <!-- the mex endpoint is explosed at http://localhost:8000/ServiceModelSamples/service/mex -->  
            <endpoint address="mex"  
                      binding="mexHttpBinding"  
                      contract="IMetadataExchange" />  
  
          </service>  
        </services>  
  
        <bindings>  
          <netMsmqBinding>  
            <binding name="volatileBinding"   
                  durable="false"  
                  exactlyOnce="false">  
              <security mode="None" />  
            </binding>  
          </netMsmqBinding>  
        </bindings>  
  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="StockTickerServiceBehavior">  
              <serviceMetadata httpGetEnabled="True"/>  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
  
    ```  
  
2.  Assurez\-vous de modifier la configuration sur le serveur et le client avant d'exécuter l'exemple.  
  
    > [!NOTE]
    >  L'affectation de `None` à `security mode` revient à affecter `None` à la sécurité <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> et `Message`.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page \(éventuellement en anglais\) des [exemples Windows Communication Foundation \(WCF\) et Windows Workflow Foundation \(WF\) pour .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Volatile`  
  
## Voir aussi