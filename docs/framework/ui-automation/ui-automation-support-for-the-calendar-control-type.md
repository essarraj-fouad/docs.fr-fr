---
title: "UI Automation Support for the Calendar Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, Calendar control type"
  - "Calendar control type"
  - "control types, Calendar"
ms.assetid: e91a7393-a7f9-4838-a1a6-857438b24bc9
caps.latest.revision: 26
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 26
---
# UI Automation Support for the Calendar Control Type
> [!NOTE]
>  Cette documentation s'adresse aux développeurs .NET Framework qui souhaitent utiliser les classes [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] managées définies dans l'espace de noms <xref:System.Windows.Automation>. Pour obtenir les dernières informations sur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consultez [API Windows Automation : UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Cette rubrique fournit des informations sur la prise en charge d’[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] pour le type de contrôle Calendar. Dans [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], un type de contrôle est un ensemble de conditions qu’un contrôle doit respecter pour pouvoir utiliser la propriété <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Ces conditions incluent des recommandations spécifiques pour l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], les valeurs de propriété [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], les modèles de contrôle et les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 Les contrôles Calendar permettent à un utilisateur de déterminer facilement la date et de sélectionner d’autres dates.  
  
 Les sections suivantes définissent l’arborescence, les propriétés, les modèles de contrôle et les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] requis pour le type de contrôle Calendar. Les spécifications [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] s’appliquent à tous les contrôles calendar, qu’il s’agisse de [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], de [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] ou de [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Arborescence UI Automation requise  
 Le tableau suivant représente l’affichage de contrôle et l’affichage de contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] concernant les contrôles calendar et décrit ce que peut contenir chaque affichage. Pour plus d’informations sur l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consultez [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Affichage de contrôle|Affichage de contenu|  
|---------------------------|--------------------------|  
|Calendrier<br /><br /> <ul><li>DataGrid<br /><br /> <ul><li>Header \(0 ou 1\)</li><li>HeaderItem \(0 ou 7 ; la quantité dépend du nombre de jours affichés dans les colonnes\)</li><li>ListItem \(la quantité dépend du nombre de jours affichés\)</li><li>Button \(0 ou 2 ; pour paginer l’affichage du calendrier\)</li></ul></li></ul>|Calendrier<br /><br /> -   ListItem \(la quantité dépend du nombre de jours affichés\)|  
  
 Les contrôles calendar peuvent être représentés sous différentes formes dans l’interface utilisateur. Les seuls contrôles qui sont sûrs d’être dans l’affichage de contrôle de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sont les contrôles datagrid, header, header item et list item.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Propriétés UI Automation requises  
 Le tableau suivant répertorie les propriétés [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] dont la valeur ou la définition est particulièrement adaptée aux contrôles calendar. Pour plus d’informations sur les propriétés [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consultez [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Propriété [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valeur|Remarques|  
|-------------------------------------------------------------------------------------|------------|---------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Consultez les remarques.|La valeur de cette propriété doit être unique dans tous les contrôles d’une application.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Consultez les remarques.|Rectangle externe qui contient l’ensemble du contrôle.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Consultez les remarques.|Pris en charge s’il existe un rectangle englobant. Si les points du rectangle englobant ne sont pas tous interactifs et que vous effectuez un test de positionnement spécialisé, vous devez substituer et fournir une zone interactive.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Calendrier|Cette valeur est la même pour toutes les infrastructures [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Le contrôle calendar est toujours inclus dans l’affichage de contenu de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Le contrôle calendar est toujours inclus dans l’affichage de contrôle de l’arborescence [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Consultez les remarques.|Si le contrôle peut recevoir le focus clavier, il doit prendre en charge cette propriété.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Consultez les remarques.|Étiquette du contrôle de document. En générale, le titre du document est utilisé.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|« calendrier »|Chaîne localisée correspondant au type de contrôle Calendar.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Consultez les remarques.|Le contrôle calendar tient généralement son nom de la date du jour.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Modèles de contrôle UI Automation requis  
 Le tableau suivant répertorie les modèles de contrôle [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par tous les contrôles calendar. Pour plus d’informations sur les modèles de contrôle, consultez [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Modèle de contrôle\/Propriété de modèle|Prise en charge|Remarques|  
|---------------------------------------------|---------------------|---------------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|Oui|Le contrôle calendar prend toujours en charge le modèle Grid car les jours d’un mois sont des éléments qui peuvent être parcourus de manière spatiale.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|Selon le cas|La plupart des contrôles calendar prennent en charge le retournement de l’affichage par page. Le modèle Scroll est recommandé pour prendre en charge la navigation de pagination.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Selon le cas|La plupart des contrôles calendar conservent un jour, un mois ou une année spécifique en tant que sélection du sous\-élément. Certains calendriers peuvent être sélectionnés plusieurs fois et d’autres ne peuvent être sélectionnés qu’une seule fois.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|Oui|Le contrôle calendar dispose toujours d’un en\-tête dans sa sous\-arborescence pour les jours de la semaine ; le modèle Table doit donc être pris en charge.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Non|Le modèle de contrôle Value n’est pas nécessaire pour les contrôles calendar car vous ne pouvez pas définir directement la valeur sur le contrôle. Si une date spécifique est associée au contrôle, les informations doivent être fournies par le modèle de contrôle Selection.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Événements UI Automation requis  
 Le tableau suivant répertorie les événements [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] qui doivent être pris en charge par tous les contrôles calendar. Pour plus d’informations sur les événements, consultez [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Événement [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Prise en charge|Remarques|  
|-------------------------------------------------------------------------------------|---------------------|---------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obligatoire|Aucune|  
|Événement de modification de propriété <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obligatoire|Aucune|  
|Événement de modification de propriété <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obligatoire|Aucune|  
|Événement de modification de propriété <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obligatoire|Aucune|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|Obligatoire|Aucune|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obligatoire|Aucune|  
|Événement de modification de propriété <xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty>.|Selon le cas|Aucune|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|Événement de modification de propriété <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty>.|Selon le cas|Si le contrôle prend en charge le modèle de contrôle Scroll, il doit prendre en charge cet événement.|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Obligatoire|Aucune|  
  
## Voir aussi  
 <xref:System.Windows.Automation.ControlType.Calendar>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)