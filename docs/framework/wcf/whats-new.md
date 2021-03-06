---
title: "Nouveaut&#233;s dans Windows Communication Foundation&#160;4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF [WCF], nouveautés"
  - "Windows Communication Foundation [WCF], nouveautés"
ms.assetid: 7e93fe73-af93-46b5-9f63-32f761ee40cf
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Nouveaut&#233;s dans Windows Communication Foundation&#160;4.5
Cette rubrique présente les nouvelles fonctionnalités de [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].  
  
## Fonctionnalités de simplification de WCF  
 Beaucoup de travail a été effectué pour faciliter le développement et la gestion des applications WCF 4.5.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Fonctionnalités de simplification de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).  
  
### Prise en charge du modèle asynchrone basé sur les tâches  
 Par défaut, la fonctionnalité Ajouter une référence de service génère des méthodes d'opération de service asynchrone retournant des tâches.Cette opération est effectuée pour les méthodes synchrones et asynchrones.Cela vous permet d'appeler les opérations de service de façon asynchrone à l'aide du modèle de programmation asynchrone basé sur les tâches.Lorsque vous appelez la méthode de proxy générée, WCF construit un objet Tâche pour représenter l'opération asynchrone et retourne cette tâche.La tâche se termine lorsque l'opération se termine. Si vous implémentez une opération asynchrone, vous pouvez l'implémenter en tant qu'opération asynchrone basée sur les tâches.Pour plus d'informations, consultez [Opérations synchrones et asynchrones](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
### Fichiers de configuration générés simplifiés  
 Lorsque vous ajoutez une référence de service dans Visual Studio ou utilisez l'outil SvcUtil.exe, un fichier de configuration client est généré.Dans les versions antérieures de WCF, ces fichiers de configuration contenaient la valeur de chaque propriété de liaison et ce, même si sa valeur était la valeur par défaut.Dans WCF 4.5, les fichiers de configuration générés contiennent uniquement les propriétés de liaison qui ont une valeur non définie par défaut.  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Fonctionnalités de simplification de WCF](../../../docs/framework/wcf/wcf-simplification-features.md)  
  
### Développement Contrat en premier  
 WCF prend désormais en charge le développement Contrat en premier.L'outil svcutl.exe a un commutateur \/serviceContract qui vous permet de générer le service et les contrats de données à partir d'un document WSDL.  
  
### Ajouter une référence de service d'un projet de sous\-ensemble portable  
 Les projets portables du sous\-ensemble permettent aux programmeurs d'assembly .NET de maintenir une arborescence source unique et le système de génération tout en prenant en charge plusieurs plateformes .NET \(de bureau, Silverlight, Windows Phone et XBOX\).Les projets portables du sous\-ensemble référencent uniquement les bibliothèques portables .NET qui sont un assembly .NET Framework pouvant être utilisé sur toute plateforme principale .NET.L'expérience du développeur est identique à celle de l'ajout d'une référence de service dans une autre application cliente WCF.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Ajouter une référence de service à un projet de sous\-ensemble portable](../../../docs/framework/wcf/add-service-reference-in-a-portable-subset-project.md).  
  
### Modification de la valeur par défaut pour le mode de compatibilité ASP.NET  
 WCF fournit le mode de compatibilité ASP.NET pour accorder aux développeurs l'accès total aux fonctionnalités dans le pipeline HTTP ASP.NET lors de l'écriture des services WCF.Pour utiliser ce mode, vous devez affecter la valeur True à l'attribut `aspNetCompatibilityEnabled` dans la section [\<serviceHostingEnvironment\>](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) du fichier web.config.De plus, la propriété `RequirementsMode` de tout service dans cet appDomain sur son <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> doit avoir la valeur <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> ou <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>.Par défaut, <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> a la valeur <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][What's New in Windows Communication Foundation](../../../docs/framework/wcf/whats-new.md) et [Services WCF et ASP.NET](../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).  
  
### Valeurs par défaut pour le nouveau transport  
 Afin de simplifier la configuration, plusieurs valeurs de propriété de transport par défaut ont été modifiées.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Fonctionnalités de simplification de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).  
  
### XmlDictionaryReaderQuotas  
 <xref:System.Xml.XmlDictionaryReaderQuotas> contient des valeurs de quota configurables pour les lecteurs du dictionnaire XML qui limitent la quantité de mémoire utilisée par un encodeur lors de la création d'un message.Bien que ces quotas soient configurables, les valeurs par défaut ont changé pour réduire le risque qu'un développeur doivent les définir explicitement.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Fonctionnalités de simplification de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).  
  
### Validation de configuration WCF  
 Dans le cadre du processus de génération dans Visual Studio, les fichiers de configuration WCF sont maintenant validés pour les attributs définis dans le projet.Une liste d'erreurs ou d'avertissements de validation s'affiche dans Visual Studio si la validation échoue.  
  
### Info\-bulles de l'éditeur XML  
 Pour aider les développeurs de services WCF nouveaux et existants à configurer leurs services, l'Éditeur XML de Visual Studio fournit maintenant des info\-bulles pour chaque élément de configuration et ses propriétés qui fait partie du fichier de configuration du service.  
  
## Améliorations de la diffusion en continu  
 Ajout de la prise en charge de la diffusion en continu asynchrone là où le côté expéditeur ne bloque pas les threads si le côté destinataire ne lit pas ou n'est pas lent dans la lecture, ce qui accroît l'extensibilité.Suppression de la limitation de mise en mémoire tampon des messages lorsqu'un client envoie un message transmis en continu à un service WCF hébergé par IIS.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Fonctionnalités de simplification de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).  
  
## Simplifier l'exposition d'un point de terminaison sur HTTPS avec IIS  
 Un mappage de protocole HTTPS a été ajouté pour simplifier l'exposition d'un point de terminaison sur HTTPS.Pour activer un point de terminaison HTTPS, assurez\-vous que votre site Web dispose d'une liaison HTTPS et d'un certificat SSL configurés, puis activez HTTPS pour le répertoire virtuel qui héberge le service.Si les métadonnées sont activées pour le service, elles seront également exposées via HTTPS.  
  
## Génération d'un seul document WSDL  
 Certaines piles de traitement WSDL tierces ne peuvent pas traiter les documents WSDL qui dépendent d'autres documents via un xsd:import.WCF vous permet maintenant de spécifier que toutes les informations WSDL doivent être retournées dans un document unique.Pour demander un seul document WSDL, ajoutez « ?singleWSDL » à l'URI lorsque vous demandez des métadonnées de service.  
  
## Prise en charge de WebSocket  
 WebSockets est une technologie qui fournit la véritable communication bidirectionnelle sur les ports 80 et 443 avec des caractéristiques de performances semblables à TCP.Deux nouvelles liaisons ont été ajoutées pour prendre en charge les communications via un transport WebSocket.<xref:System.ServiceModel.NetHttpBinding> et <xref:System.ServiceModel.NetHttpsBinding>.Pour plus d'informations, consultez [Liaisons fournies par le système](../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Valeurs par défaut pour le nouveau transport  
 Le tableau suivant décrit les paramètres qui ont changé et où trouver des informations supplémentaires.  
  
|Property|On|Nouvelle valeur par défaut|Pour plus d'informations, consultez|  
|--------------|--------|--------------------------------|-----------------------------------------|  
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30 secondes|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|  
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|12 \* nombre de processeurs|<xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|  
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 \* nombre de processeurs pour le transport<br /><br /> 4 \* nombre de processeurs pour SMSvcHost.exe|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> [Configuring the Net.TCP Port Sharing Service](http://msdn.microsoft.com/fr-fr/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0)|  
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 \* nombre de processeurs|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|  
|receiveTimeout|SMSvcHost.exe|30 secondes|[Configuring the Net.TCP Port Sharing Service](http://msdn.microsoft.com/fr-fr/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0)|  
  
## Info\-bulles de l'éditeur XML  
 Pour aider les développeurs de services WCF nouveaux et existants à configurer leurs services, l'Éditeur XML de Visual Studio fournit maintenant des info\-bulles pour chaque élément de configuration et ses propriétés qui fait partie du fichier de configuration du service.  
  
## Configuration de services WCF dans le code  
 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] permet aux développeurs de configurer des services dans les fichiers de configuration ou du code.Les fichiers de configuration sont utiles lorsqu'un service doit être configuré après avoir été déployé.Lorsqu'il utilise des fichiers de configuration, un professionnel de l'informatique doit uniquement mettre à jour le fichier de configuration, aucune recompilation n'est nécessaire.Les fichiers de configuration, toutefois, peuvent être complexes et difficiles à gérer.Il n'existe aucune prise en charge du débogage de fichiers de configuration et les éléments de configuration sont référencés par des noms. La création de fichiers de configuration est donc susceptible d'engendrer des erreurs et difficile.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] vous permet également de configurer des services dans le code.Dans les versions antérieures de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(4.0 ou version antérieure\) configurer des services dans le code était simple dans les scénarios auto\-hébergés ; la classe <xref:System.ServiceModel.ServiceHost> vous autorisait à configurer les points de terminaison et les comportements avant d'appeler ServiceHost.Open.Dans les scénarios hébergés sur le Web, toutefois, vous n'avez pas accès à la classe <xref:System.ServiceModel.ServiceHost>.Pour configurer un service hébergé sur le Web vous deviez créer un <xref:System.ServiceModel.ServiceHostFactory> qui créait le <xref:System.ServiceModel.ServiceHost> et effectuait la configuration nécessaire.Depuis le .NET 4.5, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] offre un moyen plus simple de configurer des services auto\-hébergés et hébergés sur le Web dans le code.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Configuration de services WCF dans le code](../../../docs/framework/wcf/configuring-wcf-services-in-code.md).  
  
## Mise en cache de ChannelFactory  
 Les applications clientes WCF utilisent la classe <xref:System.ServiceModel.ChannelFactory%601> pour créer un canal de communication avec un service WCF.La création d'instances <xref:System.ServiceModel.ChannelFactory%601> entraîne une certaine charge, car elle comporte les opérations suivantes :  
  
1.  Construction de l'arborescence <xref:System.ServiceModel.Description.ContractDescription>  
  
2.  Refléter tous les types CLR requis  
  
3.  Construction de la pile de canaux  
  
4.  Suppression de ressources  
  
 Pour réduire cette surcharge, WCF peut mettre en cache les fabriques de canaux lorsque vous utilisez un proxy du client WCF.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Fabrication de canal et mise en cache](../../../docs/framework/wcf/feature-details/channel-factory-and-caching.md).  
  
## Compression et encodeur binaire  
 Depuis WCF 4.5, l'encodeur binaire WCF ajoute la prise en charge de la compression.Le type de compression est configuré avec la propriété <xref:System.ServiceModel.Channels.BinaryMessageEncodingElement.CompressionFormat%2A>.Le client et le service doivent configurer la propriété <xref:System.ServiceModel.Channels.BinaryMessageEncodingElement.CompressionFormat%2A>.La compression fonctionnera pour les protocoles HTTP, HTTPS et TCP.Si un client détermine l'utilisation de la compression, mais le service ne la prend pas en charge, une exception de protocole est levée indiquant une incompatibilité de protocole.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Sélection d'un encodeur de message](../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)  
  
## UDP  
 La prise en charge a été ajoutée pour un transport UDP qui permet aux développeurs d'écrire des services qui utilisent la messagerie de type « déclenché et oublié » \(fire and forget\).Un client envoie un message à un service et n'attend aucune réponse de ce dernier.  
  
## Prise en charge de plusieurs authentifications  
 La prise en charge a été ajoutée pour prendre en charge plusieurs modes d'authentification, tels que pris en charge par IIS, sur un point de terminaison unique WCF lorsque vous utilisez le transport et la sécurité de transport HTTP.IIS vous permet d'activer plusieurs modes d'authentification sur un répertoire virtuel, cette fonctionnalité permet à un seul point de terminaison WCF de prendre en charge plusieurs modes d'authentification activés pour le répertoire virtuel où le service WCF est hébergé.  
  
## Prise en charge IDN  
 La prise en charge a été ajoutée pour tenir compte des services WCF avec des noms IDN \(Internationalized Domain Names\).Pour plus d'informations, consultez [WCF et IDN \(Internationalized Domain Names\)](../../../docs/framework/wcf/feature-details/wcf-and-internationalized-domain-names.md).  
  
## HttpClient  
 Une nouvelle classe appelée <xref:System.Net.Http.HttpClient> a été ajoutée pour faciliter l'utilisation des requêtes HTTP.Pour plus d'informations, consultez [Rendre les applications sociales et associées à des services HTTP](http://go.microsoft.com/fwlink/?LinkId=231886) et [Exemple de client HTTP](http://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664).  
  
## Configuration Intellisense  
 Les valeurs d'attribut dans les fichiers de configuration des attributs personnalisés définis dans le projet prennent désormais en charge Intellisense pour une utilisation rapide et correcte des configurations.  
  
## Info\-bulles de configuration  
 Les éléments et les attributs [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] ont maintenant des info\-bulles dans l'éditeur XML afin d'identifier plus facilement et plus précisément l'objectif de l'élément ou de l'attribut.  
  
## Coller les données sous forme de classes  
 Dans un projet WCF, les types de données définis en XML \(tels que ceux exposés dans un service\) peuvent être collés directement dans une page de codes.Le type XML sera collé comme type CLR.Pour plus d'informations, consultez [Génération de classes de type de données à partir de XML](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md).  
  
## WebServiceHost et points de terminaison par défaut  
 Dans Visual Studio 2010, WebServiceHost a automatiquement créé un point de terminaison par défaut, que vous ayez ou non spécifié explicitement un point de terminaison.Dans Visual Studio 2012 WebServiceHost créera un seul point de terminaison par défaut si aucun point de terminaison n'est explicitement ajouté.Si votre client attend le point de terminaison par défaut, ajoutez un point de terminaison et faites pointer le client vers ce dernier.Sinon, indiquez à WCF de rétablir le comportement précédent en ajoutant le paramètre suivant au fichier de configuration de l'application  
  
```xml  
<appSettings>  
    <add key="wcf:webservicehost:enableautomaticendpointscompatability" value="true"/>  
  </appSettings>  
  
```  
  
## IHttpCookieContainerManager  
 Cette interface, exposée par <xref:System.ServiceModel.Channels.HttpChannelFactory>, facilite l'utilisation des cookies côté client.Lorsque AllowCookies a la valeur True sur la liaison, accédez aux cookies à l'aide du code suivant :  
  
```csharp  
IHttpCookieContainerManager cookieManager = factory.GetProperty<IHttpCookieContainerManager>();   
System.Net.CookieContainer container = cookieManager.CookieContainer;  
  
```  
  
 Vous pouvez ensuite récupérer ou définir les cookies à partir de <xref:System.Net.CookieContainer>.Lorsque AllowCookies a la valeur False, vous pouvez extraire manuellement les cookies à l'aide de <xref:System.ServiceModel.OperationContext> et les envoyer dans d'autres requêtes à l'aide d'un autre <xref:System.ServiceModel.OperationContext> ou d'un inspecteur de message.L'interface IHttpCookieContainerManager vous permet d'authentifier un utilisateur avec un service et d'utiliser le cookie d'authentification retourné par ce service pour l'authentifier auprès d'autres services.