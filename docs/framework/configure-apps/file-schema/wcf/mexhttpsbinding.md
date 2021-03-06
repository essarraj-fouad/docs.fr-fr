---
title: "&lt;mexHttpsBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2ed3774-78b9-4a15-b79b-655f1ad68b86
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;mexHttpsBinding&gt;
Spécifie les paramètres pour une liaison utilisée dans le cadre de l'échange de messages WS\-MetadataExchange \(WS\-MEX\) sur HTTPS.  
  
## Syntaxe  
  
```  
  
<mexHttpsBinding>  
   <binding   
       closeTimeout="TimeSpan"   
       name="string"   
       openTimeout="TimeSpan"   
       receiveTimeout="TimeSpan"  
       sendTimeout="TimeSpan">  
   </binding>  
</mexHttpsBinding>  
```  
  
## Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### Attributs  
  
|Attribut|Description|  
|--------------|-----------------|  
|`closeTimeout`|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération de fermeture.  Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>.  La valeur par défaut est 00:01:00.|  
|`name`|Chaîne qui contient le nom de configuration de la liaison.  Cette valeur doit être unique car elle permet d'identifier la liaison.  Chaque liaison porte un `name` et a un attribut `namespace` qui l'identifient de façon unique dans les métadonnées du service.  De plus, ce nom est unique parmi les liaisons du même type.  Depuis [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], les liaisons et les comportements ne sont pas obligés d'avoir un nom.  Pour plus d'informations sur la configuration par défaut, ainsi que sur les comportements et les liaisons sans nom, consultez [Configuration simplifiée](../../../../../docs/framework/wcf/simplified-configuration.md) et [Configuration simplifiée pour WCF Services](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération d'ouverture.  Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>.  La valeur par défaut est 00:01:00.|  
|`receiveTimeout`|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération de réception.  Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>.  La valeur par défaut est 00:10:00.|  
|`sendTimeout`|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération d'envoi.  Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>.  La valeur par défaut est 00:01:00.|  
  
### Éléments enfants  
 Aucun  
  
### Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<liaisons\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Cet élément conserve une collection de liaisons standard et personnalisées.|  
  
## Notes  
 Cette liaison est essentiellement une liaison `WSHttpBinding` qui prend en charge la sécurité au niveau du transport à l'aide de certificats.  Pour plus d'informations sur la configuration et l'utilisation de ce type de point de terminaison de métadonnées, consultez [Comment : configurer une liaison WS\-Metadata Exchange personnalisée](../../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md) et [Procédure : récupérer des métadonnées sur une liaison non\-MEX](../../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md), ainsi que l'exemple [Point de terminaison de métadonnées sécurisé personnalisée](../../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md).  
  
## Voir aussi  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings.CreateMexHttpsBinding%2A>   
 <xref:System.ServiceModel.Configuration.MexHttpsBindingElement>   
 [Comment : publier les métadonnées d'un service à l'aide d'un fichier de configuration](../../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [Publication et récupération de métadonnées sur une liaison personnalisée](../../../../../docs/framework/wcf/extending/publishing-and-retrieving-metadata-over-a-custom-binding.md)   
 [Comment : configurer une liaison WS\-Metadata Exchange personnalisée](../../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)   
 [Procédure : récupérer des métadonnées sur une liaison non\-MEX](../../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)   
 [Point de terminaison de métadonnées sécurisé personnalisée](../../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)   
 [Métadonnées](../../../../../docs/framework/wcf/feature-details/metadata.md)   
 [Liaisons](../../../../../docs/framework/wcf/bindings.md)   
 [Configuration des liaisons fournies par le système](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/fr-fr/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<liaison\>](../../../../../docs/framework/misc/binding.md)