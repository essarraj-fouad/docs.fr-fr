---
title: "Gestion des erreurs dans une activit&#233; Flowchart &#224; l&#39;aide de TryCatch | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50922964-bfe0-4ba8-9422-0e7220d514fd
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Gestion des erreurs dans une activit&#233; Flowchart &#224; l&#39;aide de TryCatch
Cet exemple montre comment l'activité <xref:System.Activities.Statements.TryCatch> peut être utilisée dans une activité de flux de contrôle complexe.  
  
 Dans cet exemple, un code promotionnel et un nombre d'enfants sont passés en tant que variables à une activité <xref:System.Activities.Statements.Flowchart> qui calcule une remise basée sur des formules qui correspondent au code promotionnel.L'exemple inclut les versions du code impératif et du concepteur de workflow de l'exemple.  
  
 Le tableau suivant décrit en détail les variables pour l'activité `CreateFlowchartWithFaults`.  
  
|Paramètres|Description|  
|----------------|-----------------|  
|promoCode|Code promotionnel.Type : chaîne<br /><br /> Valeurs possibles avec la description entre parenthèses :<br /><br /> -   Single \(Célibataire\)<br />-   MNK \(Marié sans enfant\)<br />-   MWK \(Marié avec enfants\)|  
|numKids|Nombre d'enfants.Type : int|  
  
 L'activité `CreateFlowchartWithFaults` utilise une activité <xref:System.Activities.Statements.FlowSwitch%601> qui active l'argument `promoCode` et calcule la remise à l'aide de la formule suivante.  
  
|Valeur de `promoCode`|Remise \(%\)|  
|---------------------------|------------------|  
|Single|10|  
|MNK|15|  
|MWK|15 \+ \(1 – 1\/`numberOfKids`\)\*10 **Note:**  Potentiellement, ce calcul peut lever un <xref:System.DivideByZeroException>.Par conséquent, le calcul de la remise est inclus dans un wrapper dans une activité <xref:System.Activities.Statements.TryCatch> qui intercepte l'exception <xref:System.DivideByZeroException> et définit la remise à zéro.|  
  
#### Pour utiliser cet exemple  
  
1.  À l'aide de [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], ouvrez le fichier solution FlowchartWithFaultHandling.sln.  
  
2.  Pour générer la solution, appuyez sur Ctrl\+Maj\+B.  
  
3.  Pour exécuter la solution, appuyez sur F5.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page \(éventuellement en anglais\) des [exemples Windows Communication Foundation \(WCF\) et Windows Workflow Foundation \(WF\) pour .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WF\Basic\Built-InActivities\FlowChartWithFaultHandling`  
  
## Voir aussi  
 [Workflows d'organigramme](../../../../docs/framework/windows-workflow-foundation//flowchart-workflows.md)   
 [Exceptions](../../../../docs/framework/windows-workflow-foundation//exceptions.md)