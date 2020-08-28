---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Přidání modelu | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045114"
---
# <a name="adding-a-model"></a>Přidání modelu

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

V této části přidáte některé třídy pro správu filmů v databázi. Tyto třídy budou &quot; &quot; součástí modelu aplikace ASP.NET MVC.

K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako [Entity Framework](https://docs.microsoft.com/ef/) . Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*. Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd. (Tyto třídy jsou také známé jako třídy POCO z &quot; objektů CLR ve starém Old. &quot; ) Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup. Pokud je nutné nejprve vytvořit databázi, můžete postupovat podle tohoto kurzu, kde se dozvíte o vývoji aplikací MVC a EF. Pak můžete postupovat podle vlastního kurzu Fizmakens [ASP.NET pro generování uživatelského rozhraní](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , který se zabývá prvním přístupem k databázi.

## <a name="adding-model-classes"></a>Přidávání tříd modelu

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.

![](adding-a-model/_static/image1.png)

Zadejte název *třídy* &quot; video &quot; .

Do třídy přidejte následující pět vlastností `Movie` :

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Třídu využijeme `Movie` k reprezentaci filmů v databázi. Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.

Poznámka: aby bylo možné použít System. data. entity a související třídu, je nutné nainstalovat [balíček Entity Framework NuGet](https://www.nuget.org/packages/EntityFramework/). Další pokyny získáte pomocí odkazu.

Do stejného souboru přidejte následující `MovieDBContext` třídu:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`Třída představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci `Movie` instancí třídy v databázi. Je `MovieDBContext` odvozen ze `DbContext` základní třídy poskytnuté Entity Framework.

Aby bylo možné odkazovat na `DbContext` a `DbSet` , je nutné přidat do `using` horní části souboru následující příkaz:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

To můžete provést ručním přidáním příkazu Using, nebo můžete ukazatel myši umístit na červené klikaté čáry, kliknout `Show potential fixes` a kliknout na `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Poznámka: odebrali jsme několik nepoužitých `using` příkazů. Visual Studio zobrazí nepoužívané závislosti jako šedé. Nepoužívané závislosti můžete odebrat tak, že najedete myší na šedé závislosti, kliknete `Show potential fixes` a kliknete na **Odebrat nepoužité direktivy using.**

![](adding-a-model/_static/image3.png)

Nakonec jsme přidali model (M v MVC). V další části budete pracovat s připojovacím řetězcem databáze.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md) 
>  [Další](creating-a-connection-string.md)
