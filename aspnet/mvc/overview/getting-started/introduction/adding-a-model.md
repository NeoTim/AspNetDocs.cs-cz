---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Přidání modelu | Dokumentace Microsoftu
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0221539f5e468faacf3e38374452c0cc2a7d31d3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59398745"
---
# <a name="adding-a-model"></a>Přidání modelu

Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](sample/code-location.md)]

V této části přidáte některé třídy pro správu filmy v databázi. Tyto třídy bude &quot;modelu&quot; součástí aplikace ASP.NET MVC.

Budete používat technologii .NET Framework přístup k datům označované jako [Entity Framework](https://docs.microsoft.com/ef/) definovat a využívat tyto třídy modelu. Entity Framework (často označované jako EF) podporuje vývoj paradigma volá *Code First*. Kód nejprve umožňuje vytvořit objekty modelu napsáním jednoduché třídy. (Jedná se také označuje jako POCO třídy, z &quot;prostý staré objekty CLR.&quot;) Potom můžete mít databázi vytvořené v reálném čase ze třídy, která umožňuje pracovní postupy s velmi čistá a rychlý vývoj. Pokud je nutné nejprve vytvořit databázi, můžete stále postupovat podle tohoto kurzu se dozvíte o vývoj aplikací MVC a EF. Potom postupujte podle vlastní Fizmakens [ASP.NET generování uživatelského rozhraní](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) kurzu, které zahrnuje i první postup databáze.

## <a name="adding-model-classes"></a>Přidání třídy modelu

V **Průzkumníka řešení**, klikněte pravým tlačítkem myši *modely* složky, vyberte **přidat**a pak vyberte **třídy**.

![](adding-a-model/_static/image1.png)

Zadejte *třídy* název &quot;filmu&quot;.

Následujících pět vlastnosti, které chcete přidat `Movie` třídy:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Použijeme `Movie` pro reprezentaci filmy v databázi. Každá instance `Movie` objektu bude odpovídat řádek do tabulky databáze a každou vlastnost `Movie` třídy bude mapovat na sloupec v tabulce.

Poznámka: Chcete-li použít System.Data.Entity a související třídy, je potřeba nainstalovat [balíček NuGet Entity Framework](https://www.nuget.org/packages/EntityFramework/). Pomocí následujícího odkazu pro další pokyny.

Ve stejném souboru přidejte následující `MovieDBContext` třídy:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` Třída reprezentuje kontext databáze filmů Entity Framework, která zpracovává načítání, ukládání a aktualizaci `Movie` třídy instancí v databázi. `MovieDBContext` Je odvozen od `DbContext` základní třída poskytované rozhraním Entity Framework.

Pokud chcete mít možnost odkazovat `DbContext` a `DbSet`, budete muset přidat následující `using` příkazu v horní části souboru:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Můžete to provést tak, že ručně přidáte na pomocí příkazu, nebo můžete najeďte myší červené podtržení čáry, klikněte na tlačítko `Show potential fixes` a klikněte na tlačítko `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Poznámka: Několik nevyužité `using` příkazy byly odebrány. Visual Studio zobrazí šedě nepoužité závislé součásti. Můžete odebrat nepoužité závislé součásti podržením ukazatele nad šedé závislosti, klikněte na tlačítko `Show potential fixes` a klikněte na tlačítko **odebrat nepoužité řetězce.**

![](adding-a-model/_static/image3.png)

Nakonec jsme přidali modelu (M v MVC). V další části budete pracovat s připojovací řetězec databáze.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md)
> [další](creating-a-connection-string.md)
