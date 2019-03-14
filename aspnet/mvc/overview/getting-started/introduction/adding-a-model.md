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
ms.openlocfilehash: 3b9d84ae757eac6cc2a1ae8f7857244adff50d7c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077308"
---
<a name="adding-a-model"></a><span data-ttu-id="26655-102">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="26655-102">Adding a Model</span></span>
====================
<span data-ttu-id="26655-103">Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="26655-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="26655-104">V této části přidáte některé třídy pro správu filmy v databázi.</span><span class="sxs-lookup"><span data-stu-id="26655-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="26655-105">Tyto třídy bude &quot;modelu&quot; součástí aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="26655-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="26655-106">Budete používat technologii .NET Framework přístup k datům označované jako [Entity Framework](https://docs.microsoft.com/ef/) definovat a využívat tyto třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="26655-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="26655-107">Entity Framework (často označované jako EF) podporuje vývoj paradigma volá *Code First*.</span><span class="sxs-lookup"><span data-stu-id="26655-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="26655-108">Kód nejprve umožňuje vytvořit objekty modelu napsáním jednoduché třídy.</span><span class="sxs-lookup"><span data-stu-id="26655-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="26655-109">(Jedná se také označuje jako POCO třídy, z &quot;prostý staré objekty CLR.&quot;) Potom můžete mít databázi vytvořené v reálném čase ze třídy, která umožňuje pracovní postupy s velmi čistá a rychlý vývoj.</span><span class="sxs-lookup"><span data-stu-id="26655-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="26655-110">Pokud je nutné nejprve vytvořit databázi, můžete stále postupovat podle tohoto kurzu se dozvíte o vývoj aplikací MVC a EF.</span><span class="sxs-lookup"><span data-stu-id="26655-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="26655-111">Potom postupujte podle vlastní Fizmakens [ASP.NET generování uživatelského rozhraní](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) kurzu, které zahrnuje i první postup databáze.</span><span class="sxs-lookup"><span data-stu-id="26655-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="26655-112">Přidání třídy modelu</span><span class="sxs-lookup"><span data-stu-id="26655-112">Adding Model Classes</span></span>

<span data-ttu-id="26655-113">V **Průzkumníka řešení**, klikněte pravým tlačítkem myši *modely* složky, vyberte **přidat**a pak vyberte **třídy**.</span><span class="sxs-lookup"><span data-stu-id="26655-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="26655-114">Zadejte *třídy* název &quot;filmu&quot;.</span><span class="sxs-lookup"><span data-stu-id="26655-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="26655-115">Následujících pět vlastnosti, které chcete přidat `Movie` třídy:</span><span class="sxs-lookup"><span data-stu-id="26655-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="26655-116">Použijeme `Movie` pro reprezentaci filmy v databázi.</span><span class="sxs-lookup"><span data-stu-id="26655-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="26655-117">Každá instance `Movie` objektu bude odpovídat řádek do tabulky databáze a každou vlastnost `Movie` třídy bude mapovat na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="26655-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="26655-118">Poznámka: Chcete-li použít System.Data.Entity a související třídy, je potřeba nainstalovat [balíček NuGet Entity Framework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="26655-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="26655-119">Pomocí následujícího odkazu pro další pokyny.</span><span class="sxs-lookup"><span data-stu-id="26655-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="26655-120">Ve stejném souboru přidejte následující `MovieDBContext` třídy:</span><span class="sxs-lookup"><span data-stu-id="26655-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="26655-121">`MovieDBContext` Třída reprezentuje kontext databáze filmů Entity Framework, která zpracovává načítání, ukládání a aktualizaci `Movie` třídy instancí v databázi.</span><span class="sxs-lookup"><span data-stu-id="26655-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="26655-122">`MovieDBContext` Je odvozen od `DbContext` základní třída poskytované rozhraním Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="26655-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="26655-123">Pokud chcete mít možnost odkazovat `DbContext` a `DbSet`, budete muset přidat následující `using` příkazu v horní části souboru:</span><span class="sxs-lookup"><span data-stu-id="26655-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="26655-124">Můžete to provést tak, že ručně přidáte na pomocí příkazu, nebo můžete najeďte myší červené podtržení čáry, klikněte na tlačítko `Show potential fixes` a klikněte na tlačítko `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="26655-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="26655-125">Poznámka: Několik nevyužité `using` příkazy byly odebrány.</span><span class="sxs-lookup"><span data-stu-id="26655-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="26655-126">Visual Studio zobrazí šedě nepoužité závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="26655-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="26655-127">Můžete odebrat nepoužité závislé součásti podržením ukazatele nad šedé závislosti, klikněte na tlačítko `Show potential fixes` a klikněte na tlačítko **odebrat nepoužité řetězce.**</span><span class="sxs-lookup"><span data-stu-id="26655-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="26655-128">Nakonec jsme přidali modelu (M v MVC).</span><span class="sxs-lookup"><span data-stu-id="26655-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="26655-129">V další části budete pracovat s připojovací řetězec databáze.</span><span class="sxs-lookup"><span data-stu-id="26655-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="26655-130">[Předchozí](adding-a-view.md)
> [další](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="26655-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
