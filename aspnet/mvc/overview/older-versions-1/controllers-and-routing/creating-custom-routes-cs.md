---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Vytváření vlastních tras (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542752"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="828fe-104">Vytváření vlastních tras (C#)</span><span class="sxs-lookup"><span data-stu-id="828fe-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="828fe-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="828fe-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="828fe-106">Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="828fe-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="828fe-107">V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="828fe-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="828fe-108">V tomto kurzu se dozvíte, jak přidat vlastní trasu do ASP.NET aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="828fe-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="828fe-109">Dozvíte se, jak upravit výchozí směrovací tabulku v souboru Global.asax s vlastní trasou.</span><span class="sxs-lookup"><span data-stu-id="828fe-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="828fe-110">Pro mnoho jednoduchých ASP.NET aplikací mvc jednoduché, bude výchozí směrovací tabulka fungovat v pohodě.</span><span class="sxs-lookup"><span data-stu-id="828fe-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="828fe-111">Můžete však zjistit, že máte specializované potřeby směrování.</span><span class="sxs-lookup"><span data-stu-id="828fe-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="828fe-112">V takovém případě můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="828fe-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="828fe-113">Představte si například, že vytváříte blogovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="828fe-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="828fe-114">Můžete chtít zpracovat příchozí požadavky, které vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="828fe-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="828fe-115">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="828fe-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="828fe-116">Když uživatel zadá tento požadavek, chcete vrátit položku blogu, která odpovídá datu 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="828fe-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="828fe-117">Chcete-li zpracovat tento typ požadavku, musíte vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="828fe-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="828fe-118">Soubor Global.asax v seznamu 1 obsahuje novou vlastní trasu s názvem Blog, která zpracovává požadavky, které vypadají jako /Archive/*datum zadání*.</span><span class="sxs-lookup"><span data-stu-id="828fe-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="828fe-119">**Výpis 1 - Global.asax (s vlastní trasou)**</span><span class="sxs-lookup"><span data-stu-id="828fe-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="828fe-120">Pořadí tras, které přidáte do tabulky tras, je důležité.</span><span class="sxs-lookup"><span data-stu-id="828fe-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="828fe-121">Naše nová vlastní trasa blogu je přidána před existující výchozí trasu.</span><span class="sxs-lookup"><span data-stu-id="828fe-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="828fe-122">Pokud jste stornovat pořadí, pak výchozí trasa vždy dostane volána namísto vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="828fe-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="828fe-123">Vlastní blog směrování odpovídá všechny požadavky, které začínají /Archive/.</span><span class="sxs-lookup"><span data-stu-id="828fe-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="828fe-124">Takže odpovídá všem následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="828fe-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="828fe-125">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="828fe-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="828fe-126">/Archiv/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="828fe-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="828fe-127">/Archiv/jablko</span><span class="sxs-lookup"><span data-stu-id="828fe-127">/Archive/apple</span></span>

<span data-ttu-id="828fe-128">Vlastní trasa mapuje příchozí požadavek na řadič s názvem Archive a vyvolá akci Entry().</span><span class="sxs-lookup"><span data-stu-id="828fe-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="828fe-129">Při volání Entry() metoda je volána, datum zadání je předán jako parametr s názvem entryDate.</span><span class="sxs-lookup"><span data-stu-id="828fe-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="828fe-130">Vlastní trasu blogu můžete použít s ovladačem v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="828fe-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="828fe-131">**Výpis 2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="828fe-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="828fe-132">Všimněte si, že Entry() metoda v Výpis 2 přijímá parametr typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="828fe-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="828fe-133">Rozhraní MVC je dostatečně inteligentní, aby automaticky převádí datum zadání z adresy URL na hodnotu DateTime.</span><span class="sxs-lookup"><span data-stu-id="828fe-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="828fe-134">Pokud parametr data zadání z adresy URL nelze převést na DateTime, je vyvolána chyba (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="828fe-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="828fe-135">**Obrázek 1 – Chyba z převodu parametru**</span><span class="sxs-lookup"><span data-stu-id="828fe-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="828fe-136">[![Dialogové okno New Project (Nový projekt)](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="828fe-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="828fe-137">**Obrázek 01**: Chyba při převodu parametru[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-custom-routes-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="828fe-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="828fe-138">Souhrn</span><span class="sxs-lookup"><span data-stu-id="828fe-138">Summary</span></span>

<span data-ttu-id="828fe-139">Cílem tohoto kurzu bylo ukázat, jak můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="828fe-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="828fe-140">Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global.asax, který představuje položky blogu.</span><span class="sxs-lookup"><span data-stu-id="828fe-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="828fe-141">Diskutovali jsme o tom, jak mapovat požadavky na položky blogu na řadič s názvem ArchiveController a akce řadiče s názvem Entry().</span><span class="sxs-lookup"><span data-stu-id="828fe-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="828fe-142">[Předchozí](aspnet-mvc-controllers-overview-cs.md)
> [další](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="828fe-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
