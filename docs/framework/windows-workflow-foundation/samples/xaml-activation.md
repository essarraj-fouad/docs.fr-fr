---
title: "XAML Activation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 486760e2-bb10-4ed5-8c02-fe7472498d2d
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# XAML Activation
Cet exemple montre comment héberger un workflow déclaratif dans IIS.C'est un workflow de base appelé `EchoService` qui comporte une opération.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page de téléchargement pour télécharger tous les exemples [!INCLUDE[wf1](../../../../includes/wf1-md.md)] et [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WF\Basic\Services\XAMLActivation`  
  
#### Pour configurer, générer et exécuter l'exemple  
  
1.  Ouvrez la solution XAMLActivation.sln dans [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Générez la solution en appuyant sur **F5**.  
  
3.  Exécutez WcfTestClient.exe.À partir d'une invite de commandes, tapez ce qui suit :  
  
    1.  cd %SystemDrive%\\Program Files\\Microsoft Visual Studio 10.0\\Common7\\IDE  
  
    2.  Exécutez WcfTestClient.exe.  
  
4.  Définissez l'adresse du service sur WcfTestClient.exe en appuyant sur CTRL\+MAJ\+A et en affectant à l'adresse du service la valeur http:\/\/localhost:56133\/Service.xamlx.  
  
5.  Effectuez l'opération Echo pour tester le service.  
  
6.  Déployez le service dans IIS en utilisant DeployToIIS.Bat dans une invite de commandes avec des privilèges d'administrateur.  
  
7.  Mettez à jour l'adresse de service dans le client en spécifiant http:\/\/localhost\/XAMLActivation\/Service.xamlx et testez à nouveau le service à l'aide de WcfTestClient.exe.