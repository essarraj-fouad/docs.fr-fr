---
title: "Atténuation : AuthorizationContext par défaut"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6cfeee63-b148-429a-a7e6-6fe9b0cb7610
caps.latest.revision: 3
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 48363d0f8e515b703e49761a763379566e217844
ms.contentlocale: fr-fr
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-default-authorizationcontext"></a>Atténuation : AuthorizationContext par défaut
L’implémentation du <xref:System.IdentityModel.Policy.AuthorizationContext> retourné par un appel à la méthode <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29> avec un argument `null``authorizationPolicies` a changé dans le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].  
  
## <a name="impact"></a>Impact  
 Dans de rares cas, les applications WCF qui utilisent l'authentification personnalisée peuvent voir les différences de comportement.  
  
## <a name="mitigation"></a>Atténuation  
 Vous pouvez restaurer le comportement précédent de deux manières :  
  
-   Recompiler l'application pour cibler une version antérieure du .NET Framework autre que 4.6. Pour les services hébergés dans IIS, utilisez l'élément `<httpRuntime targetFramework="x.x" />` pour cibler une version antérieure du .NET Framework.  
  
-   Ajoutez la ligne suivante à la section `<appSettings>` de votre fichier app.config :  
  
    ```xml  
    <add key="appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext" value="true" />  
    ```  
  
## <a name="see-also"></a>Voir aussi  
 [Modifications de reciblage](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)

