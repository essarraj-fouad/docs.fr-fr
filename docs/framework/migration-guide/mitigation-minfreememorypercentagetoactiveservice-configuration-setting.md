---
title: "Atténuation : paramètre de configuration minFreeMemoryPercentageToActiveService"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7875f26-0da8-4afe-9846-7a21778f757b
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f7f228890476d45517a21bc09806538139c5e389
ms.contentlocale: fr-fr
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-minfreememorypercentagetoactiveservice-configuration-setting"></a>Atténuation : paramètre de configuration minFreeMemoryPercentageToActiveService
Dans [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], une exception est levée si la mémoire disponible sur le serveur web est inférieure au pourcentage spécifié par le paramètre de configuration [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md). Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], ce paramètre a été ignoré.  
  
## <a name="impact"></a>Impact  
 Dans la plupart des cas, l’impact du réglage du paramètre [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) est souhaitable : il améliore la stabilité du système en prévenant les exceptions <xref:System.OutOfMemoryException> qui peuvent se produire quand un service Windows Communication Foundation (WCF) est démarré sur un système ayant une mémoire contrainte.  
  
 Toutefois, dans certains cas, un service qui démarrait correctement peut ne plus démarrer. Dans ce cas, un message d'erreur détaillé s'affiche :  
  
```console
Memory gates checking failed because the free memory (nnnn bytes) is less than nn% of total memory. As a result, the service will not be available for incoming requests. To resolve this, either reduce the load on the machine or adjust the value of minFreeMemoryPercentageToActivateService on the serviceHostingEnvironment config element.
```
  
## <a name="mitigation"></a>Atténuation  
 Pour rétablir le comportement précédent où le paramètre [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) a été ignoré, modifiez le fichier Web.config comme suit :  
  
```xml
<serviceHostingEnvironment multipleSiteBindingsEnabled="true"   
                           minFreeMemoryPercentageToActivateService="0">  
   <serviceActivations>  
   ...  
   </serviceActivations>  
</serviceHostingEnvironment>  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Modifications du runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)

