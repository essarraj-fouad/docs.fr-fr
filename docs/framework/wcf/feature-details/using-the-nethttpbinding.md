---
title: "Utilisation de NetHttpBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe134acf-ceca-49de-84a9-05a37e3841f1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Utilisation de NetHttpBinding
<xref:System.ServiceModel.NetHttpBinding> est une liaison conçue pour consommer des services HTTP ou WebSocket et utilise l'encodage binaire par défaut.  <xref:System.ServiceModel.NetHttpBinding> détecte si elle est utilisée avec un contrat demande\-réponse ou un contrat duplex et modifie son comportement pour le faire correspondre \- elle utilise HTTP pour les contrats de demande\-réponse et WebSockets pour les contrats duplex.  Vous pouvez substituer ce comportement au moyen du paramètre <xref:System.ServiceModel.NetHttpBinding.WebSocketTransportUsage%2A> :  
  
1.  Toujours \- Force l'utilisation de WebSockets même pour les contrats de demande\-réponse.  
  
2.  Jamais \- Empêche l'utilisation de WebSockets.  Toute tentative d'utiliser un contrat duplex avec ce paramètre entraîne une exception.  
  
3.  WhenDuplex \- Il s'agit de la valeur par défaut et elle se comporte de la façon décrite ci\-dessus.  
  
 <xref:System.ServiceModel.NetHttpBinding> prend en charge les sessions fiables en mode HTTP et en mode WebSocket.  Les sessions en mode WebSocket sont fournies par le transport.  
  
> [!WARNING]
>  Si vous utilisez <xref:System.ServiceModel.NetHttpBinding> et le TransferMode de la liaison a la valeur TransferMode.Streamed, les grands flux peuvent provoquer un interblocage et le dépassement du délai d'attente de l'appel.  Pour contourner ce problème, envoyez de plus petits messages ou utilisez TransferMode.Buffered.  
  
## Configuration d'un service de façon à utiliser NetHttpBinding  
 <xref:System.ServiceModel.NetHttpBinding> peut être configuré de la même façon que toute autre liaison.  L'extrait de code suivant de configuration montre comment configurer un service WCF avec <xref:System.ServiceModel.NetHttpBinding>.  
  
```xml  
<system.serviceModel>  
    <services>  
      <service name="WcfService1.Service1">  
        <endpoint address=""  
                  binding="netHttpBinding"  
                  contract="WcfService1.IService1"/>  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
    <bindings>  
      <netHttpBinding>  
        <binding name="My_NetHttpBindingConfig">  
          <webSocketSettings transportUsage="WhenDuplex"/>  
        </binding>  
      </netHttpBinding>  
    </bindings>  
    <!- ... -->   
  </system.serviceModel>  
```  
  
 L'extrait de code suivant montre comment ajouter <xref:System.ServiceModel.NetHtttpBinding> dans le code.  
  
```csharp  
ServiceHost svchost = new ServiceHost(typeof(Service1), baseAddress);  
            NetHttpBinding binding = new NetHttpBinding();  
            svchost.AddServiceEndpoint(typeof(IService1), binding, address);   
        }  
```  
  
## Voir aussi  
 [Configuration de liaisons pour les services](../../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)   
 [Liaisons](../../../../docs/framework/wcf/feature-details/bindings.md)   
 [Liaisons fournies par le système](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [Services duplex](../../../../docs/framework/wcf/feature-details/duplex-services.md)