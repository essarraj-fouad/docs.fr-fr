---
title: "Message Security Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
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
  - "WS Security"
ms.assetid: d2221d1c-c9cb-48d1-b044-a3b4445c7f05
caps.latest.revision: 34
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 34
---
# Message Security Windows
Cet exemple illustre comment configurer une liaison <xref:System.ServiceModel.WSHttpBinding> pour permettre l'utilisation de la sécurité de niveau message avec authentification Windows.  Cet exemple est basé sur [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md).  Dans cet exemple, le service est hébergé dans les services IIS \(Internet Information Services\) et le client est une application console \(.exe\).  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
 La sécurité par défaut de l'élément [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) correspond à la sécurité de niveau message à l'aide de l'authentification Windows.  Dans cet exemple, les fichiers de configuration affectent explicitement à l'attribut `mode` du [\<sécurité\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md) la valeur `Message` et à l'attribut `clientCredentialType` la valeur `Windows`.  Ces valeurs correspondent aux valeurs par défaut de cette liaison. Cependant, elles ont été configurées de manière explicite, ainsi qu'en témoigne l'exemple de configuration suivant, afin d'illustrer leur utilisation.  
  
```  
<bindings>  
    <wsHttpBinding>  
        <binding>  
            <security mode="Message">  
                <message clientCredentialType="Windows"/>  
            </security>  
        </binding>  
    </wsHttpBinding>  
</bindings>  
```  
  
 La configuration du point de terminaison du client se compose d'une adresse absolue pour le point de terminaison du service, de la liaison et du contrat.  La liaison du client est configurée avec le `securityMode` et le `authenticationMode` appropriés.  
  
```  
  
<system.serviceModel>  
  <client>  
    <endpoint address=  
            "http://localhost/servicemodelsamples/service.svc"   
            binding="wsHttpBinding"   
            bindingConfiguration="Binding1"   
            contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <!--   
      <!--The default security for the WSHttpBinding is-->  
      <!--Message security using Windows authentication. -->  
      <!--This configuration explicitly defines the security mode -->  
      <!--as Message and the clientCredentialType as Windows  -->  
      <!--for demonstration purposes. -->  
      <binding name="Binding1">  
        <security mode="Message">  
          <message clientCredentialType="Windows"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
</system.serviceModel>  
  
```  
  
 Le code source du service a été modifié afin d'illustrer comment le <xref:System.ServiceModel.OperationContext.ServiceSecurityContext%2A> peut être utilisé afin d'accéder à l'identité de l'appelant.  
  
```  
public string GetCallerIdentity()  
{  
    // The Windows identity of the caller can be accessed on the ServiceSecurityContext.WindowsIdentity.  
    return OperationContext.Current.ServiceSecurityContext.WindowsIdentity.Name;  
}  
  
```  
  
 Lorsque vous exécutez l'exemple, les demandes et réponses d'opération s'affichent dans la fenêtre de console du client.  La première méthode appelée, `GetCallerIdentity`, retourne le nom de l'identité de l'appelant au client.  Appuyez sur ENTER dans la fenêtre de console pour arrêter le client.  
  
### Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez\-vous d'avoir effectué la procédure indiquée à la section [Procédure d'installation unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l'édition C\# ou Visual Basic .NET de la solution, conformez\-vous aux instructions figurant dans [Génération des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Pour exécuter l'exemple dans une configuration à un ou plusieurs ordinateurs, conformez\-vous aux instructions figurant dans [Exécution des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Voir aussi