---
title: "Configuration simplifi&#233;e pour WCF Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e39ec25-18a3-4fdc-b6a3-9dfafbd60112
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Configuration simplifi&#233;e pour WCF Services
Cet exemple montre comment implémenter et configurer un service et un client classiques à l'aide de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Cet exemple constitue la base de tous les autres exemples de technologie de base.  
  
 Ce service, qui expose un point de terminaison permettant de communiquer avec le service, utilise la configuration simplifiée de [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)].Avant [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)], le point de terminaison est généralement défini dans un fichier de configuration \(Web.config\), comme le montre l'exemple de code de configuration suivant.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright ©) Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Samples.GettingStarted.CalculatorService"  
               behaviorConfiguration="CalculatorServiceBehavior">  
        <endpoint address="" binding="basicHttpBinding" contract="ICalculator"/>  
        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Dans [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)], l'élément `<service>` est facultatif.Lorsqu'un service ne définit pas de points de terminaison, un point de terminaison est ajouté au service pour chaque adresse de base et contrat implémentés.L'adresse de base est ajoutée au nom du contrat pour déterminer le point de terminaison et la liaison est déterminée par le schéma d'adresse.L'exemple de code suivant montre un fichier de configuration simplifié.Tel qu'il est configuré, le service est accessible à l'adresse http:\/\/localhost\/servicemodelsamples\/service.svc par un client sur le même ordinateur.Pour que les clients installés sur des ordinateurs distants puissent accéder au service, un nom de domaine complet doit être spécifié au lieu de localhost.Par défaut, le service n'expose pas de métadonnées.Comme tel, le service active le comportement <xref:System.ServiceModel.Description.ServiceMetadataBehavior>.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright © Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### Pour utiliser cet exemple  
  
1.  Assurez\-vous d'avoir effectué la [Procédure d'installation unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer la solution, suivez les instructions indiquées dans [Génération des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Exécutez l'exemple en procédant comme suit :  
  
    1.  Cliquez avec le bouton droit sur le projet **Service**, sélectionnez **Définir comme projet de démarrage** et appuyez sur **Ctrl\+F5**.  
  
    2.  Attendez le message de la console confirmant le bon fonctionnement du service.  
  
    3.  Cliquez avec le bouton droit sur le projet **Client**, sélectionnez **Définir comme projet de démarrage** et appuyez sur **Ctrl\+F5**.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page \(éventuellement en anglais\) des [exemples Windows Communication Foundation \(WCF\) et Windows Workflow Foundation \(WF\) pour .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WCF\Basic\Services\ConfigSimplificationIn40`  
  
## Voir aussi  
 [Exemples de gestion AppFabric](http://go.microsoft.com/fwlink/?LinkId=193960)   
 [Configuration simplifiée](../../../../docs/framework/wcf/simplified-configuration.md)