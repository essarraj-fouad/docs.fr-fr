---
title: nonComVisibleBaseClass (MDA)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- visible classes
- managed debugging assistants (MDAs), COM visible classes
- nonComVisibleBaseClass MDA
- COM visible classes
- QueryInterface call failures
- MDAs (managed debugging assistants), COM visible classes
ms.assetid: 9ec1af27-604b-477e-9ee2-e833eb10d3ce
caps.latest.revision: 9
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7f6da0e4a2046ac80a35894383f732eb266b8459
ms.contentlocale: fr-fr
ms.lasthandoff: 08/21/2017

---
# <a name="noncomvisiblebaseclass-mda"></a>nonComVisibleBaseClass (MDA)
L'Assistant Débogage managé (MDA) `nonComVisibleBaseClass` est activé quand un appel `QueryInterface` est effectué par du code natif ou non managé sur le wrapper CCW (COM Callable Wrapper) d'une classe managée visible par COM qui dérive d'une classe de base qui ne l'est pas.  L'appel `QueryInterface` provoque l'activation de l'Assistant Débogage managé uniquement dans les cas où l'appel demande l'interface de classe ou l'interface `IDispatch` par défaut de la classe managée visible par COM.  L'Assistant Débogage managé n'est pas activé si `QueryInterface` concerne une interface explicite à laquelle est appliqué l'attribut <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> et qui est implémentée explicitement par la classe visible par COM.  
  
## <a name="symptoms"></a>Symptômes  
 Un appel `QueryInterface` effectué à partir du code natif échoue (erreur COR_E_INVALIDOPERATION HRESULT).  L'erreur HRESULT peut être due au refus des appels `QueryInterface` par le runtime, provoquant ainsi l'activation de cet Assistant Débogage managé.  
  
## <a name="cause"></a>Cause  
 Pour éviter des problèmes de version potentiels, le runtime n'autorise pas les appels `QueryInterface` pour l'interface de classe ou l'interface `IDispatch` par défaut d'une classe visible par COM dérivant d'une classe qui n'est pas visible par COM.  Si, par exemple, des membres publics étaient ajoutés à la classe de base non visible par COM, les clients COM existants utilisant la classe dérivée pourraient être interrompus, car la table vtable de la classe dérivée qui contient les membres de la classe de base serait modifiée.  Les interfaces explicites exposées à COM ne rencontrent pas ce problème dans la mesure où elles n'incluent pas les membres de base des interfaces de vtable.  
  
## <a name="resolution"></a>Résolution  
 N'exposez pas l'interface de classe. Définissez une interface explicite et appliquez-lui l'attribut <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>.  
  
## <a name="effect-on-the-runtime"></a>Effet sur le runtime  
 Cet Assistant Débogage managé n'a aucun effet sur le CLR.  
  
## <a name="output"></a>Sortie  
 La sortie ci-dessous est un exemple de message qui est retourné après un appel `QueryInterface` effectué sur une classe `Derived` visible par COM dérivant d'une classe `Base` non visible par COM.  
  
```  
A QueryInterface call was made requesting the class interface of COM   
visible managed class 'Derived'. However since this class derives from   
non COM visible class 'Base', the QueryInterface call will fail. This   
is done to prevent the non COM visible base class from being   
constrained by the COM versioning rules.   
```  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <nonComVisibleBaseClass />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnostic d’erreurs avec les Assistants Débogage managé](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Marshaling d’interopérabilité](../../../docs/framework/interop/interop-marshaling.md)

