---
title: "S&#233;curisation des messages &#224; l&#39;aide de la s&#233;curit&#233; de transport | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9029771a-097e-448a-a13a-55d2878330b8
caps.latest.revision: 21
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 21
---
# S&#233;curisation des messages &#224; l&#39;aide de la s&#233;curit&#233; de transport
Cette section traite de la sécurité de transport Message Queuing \(MSMQ\) que vous pouvez utiliser pour sécuriser des messages envoyés vers une file d'attente.  
  
> [!NOTE]
>  Avant de lire cette rubrique, il est recommandé de lire [Concepts relatifs à la sécurité](../../../../docs/framework/wcf/feature-details/security-concepts.md).  
  
 L'illustration suivante fournit un modèle conceptuel de la communication mise en file d'attente à l'aide de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Cette illustration et la terminologie sont utilisées pour expliquer les concepts de sécurité de transport.  
  
 ![Diagramme des applications en file d'attente](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Distributed\-Queue\-Figure")  
  
 Lors de l'envoi de messages en file d'attente à l'aide de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] avec <xref:System.ServiceModel.NetMsmqBinding>, le message [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] est joint en tant que corps du message MSMQ.La sécurité de transport sécurise le message MSMQ entier \(en\-têtes de message ou propriétés MSMQ et le corps du message\).Étant donné qu'il s'agit du corps du message MSMQ, l'utilisation de la sécurité de transport sécurise également le message [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Le concept clé de la sécurité de transport est que le client doit satisfaire certaines conditions de sécurité pour envoyer le message dans la file d'attente cible.Cela diffère de la sécurité de message, où le message est sécurisé pour l'application qui reçoit le message.  
  
 La sécurité de transport à l'aide de <xref:System.ServiceModel.NetMsmqBinding> et <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> a un impact sur la manière dont les messages MSMQ sont sécurisés en transit entre la file d'attente de transmission et la file d'attente cible, où le terme « sécurisé » implique les éléments suivants :  
  
-   Signature du message afin de s'assurer qu'il n'est pas falsifié.  
  
-   Chiffrement du message afin de s'assurer qu'il ne peut pas être vu ou falsifié.Cela est recommandé mais facultatif.  
  
-   Le gestionnaire de files d'attente cibles qui identifie l'expéditeur du message pour le non\-rejet.  
  
 Dans MSMQ, quelle que soit l'authentification, la file d'attente cible possède une liste de contrôle d'accès \(ACL, Access Control List\) afin de vérifier si le client est autorisé à envoyer le message à la file d'attente cible.Il est également vérifié si l'application réceptrice est autorisée à recevoir le message depuis la file d'attente cible.  
  
## Propriétés de la sécurité de transport MSMQ WCF  
 MSMQ utilise la sécurité Windows pour l'authentification.Il utilise l'identificateur de sécurité Windows \(SID\) pour identifier le client et utilise le service d'annuaire Active Directory comme autorité de certification lors de l'authentification du client.Cela requiert que MSMQ soit installé avec l'intégration Active Directory.Le SID de domaine Windows étant utilisé pour identifier le client, cette option de sécurité est explicite uniquement lorsque le client et le service font partie du même domaine Windows.  
  
 MSMQ permet également de joindre un certificat au message qui n'est pas inscrit auprès d'Active Directory.Dans ce cas, il s'assure que le message a été signé à l'aide du certificat joint.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fournit ces deux options dans le cadre de la sécurité de transport MSMQ ; elles constituent la pierre angulaire de la sécurité de transport.  
  
 Par défaut, la sécurité de transport est activée.  
  
 Étant donné ces principes de base, les sections suivantes détaillent les propriétés de sécurité de transport fournies avec <xref:System.ServiceModel.NetMsmqBinding> et <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>.  
  
#### Mode d'authentification MSMQ  
 Le <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> indique s'il faut utiliser la sécurité de domaine Windows ou une sécurité externe basée sur certificat pour sécuriser le message.Dans les deux modes d'authentification, le canal de transport de mise en file d'attente [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilise le `CertificateValidationMode` spécifié dans la configuration du service.Le mode de validation de certificat spécifie le mécanisme utilisé pour vérifier la validation du certificat.  
  
 Lorsque la sécurité de transport est activée, le paramètre par défaut est <xref:System.ServiceModel.MsmqAuthenticationMode>.  
  
#### Mode d'authentification de domaine Windows  
 L'utilisation de la sécurité Windows requiert l'intégration Active Directory.Le mode de sécurité du transport par défaut utilisé est <xref:System.ServiceModel.MsmqAuthenticationMode>.Lorsqu'il est défini, le canal [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] joint le SID Windows au message MSMQ et utilise son certificat interne obtenu à partir d'Active Directory.MSMQ utilise ce certificat interne pour sécuriser le message.Le gestionnaire de files d'attente de réception utilise Active Directory pour rechercher un certificat correspondant afin d'authentifier le client et vérifie que le SID correspond également à celui du client.Cette étape d'authentification est exécutée si un certificat, généré en interne en mode d'authentification `WindowsDomain` ou généré de manière externe en mode d'authentification `Certificate`, est joint au message même si la file d'attente cible n'est pas marquée comme nécessitant l'authentification.  
  
> [!NOTE]
>  Lorsque vous créez une file d'attente, vous pouvez marquer la file d'attente comme file d'attente authentifiée pour indiquer que la file d'attente nécessite l'authentification des clients envoyant des messages à la file d'attente.Cela garantit qu'aucun message non authentifié n'est accepté dans la file d'attente.  
  
 Le système vérifie également si le SID joint au message figure dans la liste ACL de la file d'attente cible afin de s'assurer que le client est autorisé à envoyer des messages à la file d'attente.  
  
#### Mode d'authentification de certificat  
 L'utilisation du mode d'authentification de certificat ne requiert pas l'intégration Active Directory.En fait, dans certains cas, par exemple lorsque MSMQ est installé en mode de groupe de travail \(sans intégration Active Directory\) ou lors de l'utilisation du protocole de transfert SRMP \(SOAP Reliable Messaging Protocol\) pour envoyer des messages à la file d'attente, seul <xref:System.ServiceModel.MsmqAuthenticationMode> fonctionne.  
  
 Lors de l'envoi d'un message [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] avec <xref:System.ServiceModel.MsmqAuthenticationMode>, le canal [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ne joint pas de SID Windows au message MSMQ.La liste ACL de file d'attente cible doit autoriser l'accès utilisateur `Anonymous` pour l'envoi vers la file d'attente.Le gestionnaire de files d'attente de réception vérifie si le message MSMQ a été signé avec le certificat mais n'exécute pas d'authentification.  
  
 Le certificat avec ses informations de revendications et d'identité est rempli dans le <xref:System.ServiceModel.ServiceSecurityContext> par le canal de transport de mise en file d'attente [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Le service peut utiliser ces informations pour exécuter sa propre authentification de l'expéditeur.  
  
### Niveau de protection MSMQ  
 Le niveau de protection spécifie comment protéger le message MSMQ afin de s'assurer qu'il n'est pas falsifié.Il est spécifié dans la propriété <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>.La valeur par défaut est <xref:System.Net.Security.ProtectionLevel>.  
  
#### Niveau de protection « Signature »  
 Le message MSMQ est signé à l'aide du certificat généré en interne lors de l'utilisation du mode d'authentification `WindowsDomain` ou d'un certificat généré en externe lors de l'utilisation du mode d'authentification `Certificate`.  
  
#### Niveau de protection « Signature et chiffrement »  
 Le message MSMQ est signé à l'aide du certificat généré en interne lors de l'utilisation du mode d'authentification `WindowsDomain` ou d'un certificat généré en externe lors de l'utilisation du mode d'authentification `Certificate`.  
  
 Outre la signature du message, le message MSMQ est chiffré à l'aide de la clé publique du certificat obtenue à partir d'Active Directory qui appartient au gestionnaire de files d'attente de réception qui héberge la file d'attente cible.Le gestionnaire de files d'attente d'émission garantit que le message MSMQ est chiffré en transit.Le gestionnaire de files d'attente de réception déchiffre le message MSMQ à l'aide de la clé privée de son certificat interne et stocke le message dans la file d'attente \(s'il est authentifié et autorisé\) en texte clair.  
  
> [!NOTE]
>  Pour chiffrer le message, l'accès Active Directory est requis \(la propriété`UseActiveDirectory` de <xref:System.ServiceModel.NetMsmqBinding> doit avoir la valeur `true`\) et peut être utilisé avec <xref:System.ServiceModel.MsmqAuthenticationMode> et <xref:System.ServiceModel.MsmqAuthenticationMode>.  
  
#### Niveau de protection « Aucun »  
 Ce niveau est utilisé lorsque <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> a la valeur <xref:System.Net.Security.ProtectionLevel>.Cela ne peut pas être une valeur valide pour d'autres modes d'authentification.  
  
> [!NOTE]
>  Si le message MSMQ est signé, MSMQ vérifie si le message est signé avec le certificat joint \(interne ou externe\) quel que soit l'état de la file d'attente, autrement dit file d'attente authentifiée ou non.  
  
### Algorithme de chiffrement MSMQ  
 L'algorithme de chiffrement spécifie l'algorithme à utiliser pour chiffrer le message MSMQ sur le câble.Cette propriété est utilisée uniquement si <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> a la valeur <xref:System.Net.Security.ProtectionLevel>.  
  
 Les algorithmes pris en charge sont `RC4Stream` et `AES` et la valeur par défaut est `RC4Stream`.  
  
 Vous pouvez utiliser l'algorithme `AES` uniquement si MSMQ 4.0 est installé sur l'expéditeur.De plus, la file d'attente cible doit également être hébergée sur MSMQ 4.0.  
  
### Algorithme de hachage MSMQ  
 L'algorithme de hachage spécifie l'algorithme utilisé pour créer une signature numérique du message MSMQ.Le gestionnaire de files d'attente de réception utilise ce même algorithme pour authentifier le message MSMQ.Cette propriété est utilisée uniquement si <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> a la valeur <xref:System.Net.Security.ProtectionLevel> ou <xref:System.Net.Security.ProtectionLevel>.  
  
 Les algorithmes pris en charge sont `MD5`, `SHA1`, `SHA256` et `SHA512`.La valeur par défaut est `SHA1`.  
  
## Voir aussi  
 [Message Queuing](http://msdn.microsoft.com/fr-fr/ff917e87-05d5-478f-9430-0f560675ece1)   
 [Concepts relatifs à la sécurité](../../../../docs/framework/wcf/feature-details/security-concepts.md)   
 [Sécurisation des services et des clients](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)