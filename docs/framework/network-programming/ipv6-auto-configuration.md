---
title: IPv6, configuration automatique
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 581c1d21-1013-43a3-bf3e-2d9ead62b79c
caps.latest.revision: 5
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c46d4b8f6b9e3620c313e9737b556a6050da0126
ms.contentlocale: fr-fr
ms.lasthandoff: 08/21/2017

---
# <a name="ipv6-auto-configuration"></a>IPv6, configuration automatique
Un objectif important du protocole IPv6 est de prendre en charge le Plug-and-Play des nœuds. Autrement dit, vous devez pouvoir connecter un nœud à un réseau IPv6 et obtenir sa configuration automatique sans intervention humaine.  
  
## <a name="type-of-auto-configuration"></a>Type de configuration automatique  
 Le protocole IPv6 prend en charge les types de configuration automatique suivants :  
  
-   **Configuration automatique avec état**. Ce type de configuration nécessite un certain degré d’intervention humaine, car le protocole DHCP pour serveur IPv6 (DHCPv6) est nécessaire à l’installation et à l’administration des nœuds. Le serveur DHCPv6 conserve une liste des nœuds auxquels il fournit des informations de configuration. Elle gère également les informations d’état pour que le serveur connaisse la durée d’utilisation de chaque adresse et le moment auquel elles sont susceptibles d’être de nouveau disponibles en vue de leur réaffectation.  
  
-   **Configuration automatique sans état**. Ce type de configuration convient aux particuliers et aux petites entreprises. Dans ce cas, chaque hôte détermine ses adresses à partir du contenu des annonces de routeur reçues. Si vous utilisez la norme IEEE EUI-64 pour définir la partie de l’adresse correspondant à l’ID réseau, il est très probable que l’adresse d’hôte de la liaison soit unique.  
  
 Quelle que soit la manière dont l’adresse est déterminée, le nœud doit vérifier que son adresse potentielle est unique sur la liaison locale. Pour cela, un message de sollicitation de voisin est envoyé à l’adresse potentielle. Si le nœud reçoit une réponse, il sait que l’adresse est déjà utilisée et doit donc trouver une autre adresse.  
  
## <a name="ipv6-mobility"></a>Mobilité IPv6  
 La prolifération des appareils mobiles a créé un nouveau besoin, qui est celui de pouvoir changer d’emplacement de manière arbitraire sur un réseau Internet IPv6 tout en maintenant les connexions existantes. Pour fournir cette fonctionnalité, un nœud mobile reçoit une adresse racine à laquelle il est toujours joignable. Lorsque le nœud mobile se trouve à la racine, il se connecte à la liaison racine et utilise son adresse racine. Lorsque le nœud mobile ne se trouve pas à la racine, un agent interne (généralement, un routeur) relaie les messages entre le nœud mobile et les nœuds avec lesquels il communique.  
  
## <a name="see-also"></a>Voir aussi  
 [Protocole Internet version 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Sockets](../../../docs/framework/network-programming/sockets.md)

