---
title: "Création d’un Package NuGet avec les outils multiplateformes"
description: "Découvrez comment créer un package NuGet avec la commande « dotnet pack »."
keywords: .NET, .NET Core, NuGet
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2f0415c1-110b-433d-87c1-ae3d543a8844
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9e5c762de0a14407c92c9752edc9619caa07d500
ms.contentlocale: fr-fr
ms.lasthandoff: 07/28/2017

---

# <a name="how-to-create-a-nuget-package-with-cross-platform-tools"></a>Création d’un Package NuGet avec les outils multiplateformes

> [!NOTE]
> Voici des exemples de ligne de commande avec Unix.  La commande `dotnet pack` montrée ici fonctionne de la même façon sur Windows.

Pour .NET Core 1.0, les bibliothèques doivent être distribuées sous forme de packages NuGet.  Il s’agit en fait de la façon dont toutes les bibliothèques .NET Standard sont distribuées et consommées.  Cette opération est plus facile avec la commande `dotnet pack`.

Imaginez que vous venez d’écrire une nouvelle bibliothèque que vous voulez distribuer via NuGet.  Pour cela, vous pouvez créer un package NuGet avec les outils multiplateformes.  L’exemple suivant suppose une bibliothèque nommée **SuperAwesomeLibrary** ciblant `netstandard1.0`.

Si vous avez des dépendances transitives (c’est-à-dire dans le cas d’un projet qui dépend d’un autre projet), vous devez veiller à restaurer les packages pour toute votre solution avec la commande `dotnet restore` avant de créer un package NuGet.  Si vous ne le faites pas, la commande `dotnet pack` ne fonctionne pas correctement.

Après avoir vérifié que les packages sont restaurés, vous pouvez accéder au répertoire où se trouve une bibliothèque :

`$ cd src/SuperAwesomeLibrary`

Il s’agit d’une seule commande à partir de la ligne de commande :
    
`$ dotnet pack`

Votre dossier `/bin/Debug` doit maintenant ressembler à ceci :

```
$ ls bin/Debug

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

Notez que ceci génère un package qui peut être débogué.  Si vous voulez générer un package NuGet avec des fichiers binaires compilés, tout ce que vous devez faire est d’ajouter le commutateur `-c`/`--configuration` et d’utiliser `release` comme argument.

`$ dotnet pack --configuration release`

Votre dossier `/bin` a désormais un dossier `release` contenant votre package NuGet avec les fichiers binaires compilés :

```
$ ls bin/release

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

Vous avez maintenant les fichiers nécessaires pour publier un package NuGet !

## <a name="dont-confuse-dotnet-pack-with-dotnet-publish"></a>Ne confondez pas `dotnet pack` et `dotnet publish`

Il est important de noter qu’à aucun moment, la commande `dotnet publish` n’est impliquée.  La commande `dotnet publish` est destinée au déploiement des applications avec toutes leurs dépendances dans le même regroupement, et non pas à la génération d’un package NuGet à distribuer et à consommer via NuGet.

