---
title: "Suivi personnalis&#233; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Suivi personnalis&#233;
Cet exemple montre comment créer un participant de suivi personnalisé et écrire le contenu des données de suivi sur la console.De plus, il montre comment émettre des objets <xref:System.Activities.Tracking.CustomTrackingRecord> remplis avec des données définies par l'utilisateur.Le participant de suivi basé sur la console filtre les objets <xref:System.Activities.Tracking.TrackingRecord> émis par le workflow à l'aide d'un objet de modèle de suivi créé dans le code.  
  
## Détails de l'exemple  
 [!INCLUDE[wf](../../../../includes/wf-md.md)] fournit une infrastructure de suivi permettant de suivre l'exécution d'une instance de workflow.Le runtime de suivi implémente une instance de workflow pour émettre des événements liés au cycle de vie du workflow, des événements des activités de workflow et des événements de suivi personnalisé.Le tableau suivant détaille les composants principaux de l'infrastructure de suivi.  
  
|Composant|Description|  
|---------------|-----------------|  
|Runtime de suivi|Fournit l'infrastructure permettant d'émettre des enregistrements de suivi.|  
|Participants de suivi|Consomme les enregistrements de suivi.[!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)] est fourni avec un participant de suivi qui écrit les enregistrements de suivi sous la forme d'événements Suivi d'événements pour Windows \(ETW, Event Tracing for Windows\).|  
|Modèle de suivi|Mécanisme de filtrage qui permet à un participant de suivi de s'abonner à un sous\-ensemble des enregistrements de suivi émis à partir d'une instance de workflow.|  
  
 Le tableau suivant détaille les enregistrements de suivi émis par le runtime du workflow.  
  
|Enregistrement de suivi|Description|  
|-----------------------------|-----------------|  
|Enregistrements de suivi d'instance du workflow.|Décrit le cycle de vie de l'instance de workflow.Par exemple, un enregistrement d'instance est émis lorsque le workflow démarre ou se termine.|  
|Enregistrements de suivi d'état d'activité.|Détaille l'exécution de l'activité.Ces enregistrements indiquent l'état d'une activité de workflow, par exemple lorsqu'une activité est planifiée, lorsque l'activité se termine ou lorsqu'une erreur est générée.|  
|Enregistrement de reprise de signet.|Émis chaque fois qu'un signet au sein d'une instance de workflow est repris.|  
|Enregistrements de suivi personnalisé.|Un auteur de workflow peut créer des enregistrements de suivi personnalisé et les émettre dans l'activité personnalisée.|  
  
 Le participant de suivi s'abonne à un sous\-ensemble des objets <xref:System.Activities.Tracking.TrackingRecord> émis à l'aide de modèles de suivi.Un modèle de suivi contient des requêtes de suivi qui permettent de s'abonner à un type d'enregistrement de suivi particulier.Les modèles de suivi peuvent être spécifiés dans le code ou dans la configuration.  
  
### Participant de suivi personnalisé  
 L'API de participant de suivi permet d'étendre du runtime de suivi avec un participant de suivi fourni par l'utilisateur, qui peut inclure une logique personnalisée permettant de gérer les objets <xref:System.Activities.Tracking.TrackingRecord> émis par le runtime de workflow.  
  
 Pour écrire un participant de suivi, l'utilisateur doit implémenter <xref:System.Activities.Tracking.TrackingParticipant>.Plus précisément, la méthode <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> doit être implémentée par le participant personnalisé.Cette méthode est appelée lorsqu'un <xref:System.Activities.Tracking.TrackingRecord> est émis par le runtime de workflow.  
  
```csharp  
public abstract class TrackingParticipant  
{  
    protected TrackingParticipant();  
  
    public virtual TrackingProfile TrackingProfile { get; set; }  
    public abstract void Track(TrackingRecord record, TimeSpan timeout);  
}  
  
```  
  
 Le participant de suivi complet est implémenté dans le fichier ConsoleTrackingParticipant.cs. L'exemple de code suivant est la méthode <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> pour le participant de suivi personnalisé.  
  
```csharp  
protected override void Track(TrackingRecord record, TimeSpan timeout)  
{  
    ...             
    WorkflowInstanceRecord workflowInstanceRecord = record as WorkflowInstanceRecord;  
    if (workflowInstanceRecord != null)  
    {  
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,  
            " Workflow InstanceID: {0} Workflow instance state: {1}",  
            record.InstanceId, workflowInstanceRecord.State));  
    }  
  
    ActivityStateRecord activityStateRecord = record as ActivityStateRecord;  
    if (activityStateRecord != null)  
    {  
        IDictionary<String, object> variables = activityStateRecord.Variables;  
        StringBuilder vars = new StringBuilder();  
  
        if (variables.Count > 0)  
        {  
            vars.AppendLine("\n\tVariables:");  
            foreach (KeyValuePair<string, object> variable in variables)  
            {     
                vars.AppendLine(String.Format(  
                    "\t\tName: {0} Value: {1}", variable.Key, variable.Value));  
            }  
        }  
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,  
            " :Activity DisplayName: {0} :ActivityInstanceState: {1} {2}",  
                activityStateRecord.Activity.Name, activityStateRecord.State,  
            ((variables.Count > 0) ? vars.ToString() : String.Empty)));  
    }  
  
    CustomTrackingRecord customTrackingRecord = record as CustomTrackingRecord;  
  
    if ((customTrackingRecord != null) && (customTrackingRecord.Data.Count > 0))  
    {  
        ...  
    }  
    Console.WriteLine();  
  
}  
  
```  
  
 L'exemple de code suivant ajoute le participant de console au demandeur de workflow.  
  
```csharp  
ConsoleTrackingParticipant customTrackingParticipant = new ConsoleTrackingParticipant()  
{  
    ...  
    // The tracking profile is set here, refer to Program.CS  
...  
}  
  
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());  
invoker.Extensions.Add(customTrackingParticipant);  
  
```  
  
### Émission d'enregistrements de suivi personnalisé  
 Cet exemple illustre également la possibilité d'émettre des objets <xref:System.Activities.Tracking.CustomTrackingRecord> à partir d'une activité de workflow personnalisée :  
  
-   Les objets <xref:System.Activities.Tracking.CustomTrackingRecord> sont créés et remplis avec les données définies par l'utilisateur qui doivent être émises avec l'enregistrement.  
  
-   <xref:System.Activities.Tracking.CustomTrackingRecord> est émis en appelant la méthode de suivi de <xref:System.Activities.ActivityContext>.  
  
 L'exemple suivant montre comment émettre des objets <xref:System.Activities.Tracking.CustomTrackingRecord> dans une activité personnalisée.  
  
```csharp  
// Create the Custom Tracking Record  
CustomTrackingRecord customRecord = new CustomTrackingRecord("OrderIn")  
{  
    Data =   
    {  
        {"OrderId", 200},  
        {"OrderDate", "20 Aug 2001"}  
    }  
};  
  
// Emit custom tracking record  
context.Track(customRecord);  
  
```  
  
#### Pour utiliser cet exemple  
  
1.  À l'aide de [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], ouvrez le fichier solution CustomTrackingSample.sln.  
  
2.  Pour générer la solution, appuyez sur Ctrl\+Maj\+B.  
  
3.  Pour exécuter la solution, appuyez sur Ctrl\+F5.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur.Recherchez le répertoire \(par défaut\) suivant avant de continuer.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n'existe pas, rendez\-vous sur la page \(éventuellement en anglais\) des [exemples Windows Communication Foundation \(WCF\) et Windows Workflow Foundation \(WF\) pour .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<LecteurInstall>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## Voir aussi  
 [Exemples d'analyse AppFabric](http://go.microsoft.com/fwlink/?LinkId=193959)