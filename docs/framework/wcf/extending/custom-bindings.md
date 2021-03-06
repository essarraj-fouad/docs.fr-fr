---
title: "Liaisons personnalis&#233;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Windows Communication Foundation, configuration"
  - "Windows Communication Foundation, points de terminaison"
ms.assetid: 58532b6d-4eea-4a4f-854f-a1c8c842564d
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Liaisons personnalis&#233;es
Vous pouvez utiliser la classe <xref:System.ServiceModel.Channels.CustomBinding> lorsque l'une des liaisons fournies par le système ne répond pas aux spécifications de votre service.Toutes les liaisons sont construites à partir d'un ensemble ordonné d'éléments de liaison.Les liaisons personnalisées peuvent être construites à partir d'un jeu d'éléments de liaison fournis par le système ou peuvent inclure des éléments de liaison personnalisés définis par l'utilisateur.Vous pouvez utiliser des éléments de liaison personnalisés pour activer, par exemple, l'utilisation de nouveaux transports ou encodeurs au niveau d'un point de terminaison de service.Pour obtenir des exemples fonctionnels, consultez [Custom Binding Samples](http://msdn.microsoft.com/fr-fr/657e8143-beb0-472d-9cfe-ed1a19c2ab08).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
## Construction d'une liaison personnalisée  
 Une liaison personnalisée est construite à l'aide du constructeur <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> à partir d'éléments de liaison « empilés » dans un ordre spécifique :  
  
-   Au sommet de cette pile se trouve une classe <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> facultative qui autorise les transactions de flux.  
  
-   L'élément suivant est une classe <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> facultative qui fournit une session et des mécanismes de classement tel que défini dans la spécification WS\-ReliableMessaging.Une session peut traverser les intermédiaires SOAP et de transport.  
  
-   L'élément suivant est une classe <xref:System.ServiceModel.Channels.SecurityBindingElement> facultative qui fournit des fonctionnalités de sécurité telles que l'autorisation, l'authentification, la protection et la confidentialité.  
  
-   Vous trouverez ensuite une classe <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> facultative qui permet de disposer d'une communication en duplex bidirectionnelle avec un protocole de transport qui ne prend pas en charge la communication en duplex en mode natif, comme HTTP.  
  
-   Vous trouverez ensuite une classe <xref:System.ServiceModel.Channels.OneWayBindingElement> facultative qui fournit une communication unidirectionnelle.  
  
-   Puis, vous trouverez un élément de liaison de sécurité de flux de données facultatif qui peut être l'un des éléments suivants.  
  
    -   <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
-   L'élément suivant est un message obligatoire encodant l'élément de liaison.Vous pouvez utiliser votre propre encodeur de message ou l'une des trois liaisons d'encodage de message :  
  
    -   <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>  
  
 Au bas de la pile se trouve un élément de transport obligatoire.Vous pouvez utiliser votre propre transport ou l'un des éléments de liaison de transport suivants fournis par [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] :  
  
-   <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.PeerTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>  
  
-   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>  
  
-   <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>  
  
 Le tableau suivant récapitule les options de chaque couche.  
  
|Couche|Options|Obligatoire|  
|------------|-------------|-----------------|  
|Transactions|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|Non|  
|Fiabilité|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|Non|  
|Sécurité|<xref:System.ServiceModel.Channels.SecurityBindingElement>|Non|  
|Encodage|Texte, binaire, MTOM \(Message Transmission Optimization Mechanism\), personnalisé|Oui|  
|Transport|TCP, HTTP, HTTPS, canaux nommés \(également appelés IPC\), P2P \(Peer\-to\-Peer\), Message Queuing \(également appelé MSMQ\), Custom|Oui|  
  
 De plus, vous pouvez définir vos propres éléments de liaison et les insérer entre chacune des couches définies précédentes.  
  
## Voir aussi  
 [Vue d'ensemble de la création de points de terminaison](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Utilisation de liaisons pour configurer des services et des clients](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Liaisons fournies par le système](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [Comment : personnaliser une liaison fournie par le système](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)   
 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Liaison personnalisée](../../../../docs/framework/wcf/samples/custom-binding.md)