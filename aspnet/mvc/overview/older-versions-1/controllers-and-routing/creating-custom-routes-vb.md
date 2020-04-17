---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Vytváření vlastních tras (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542739"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="414d8-104">Vytváření vlastních tras (VB)</span><span class="sxs-lookup"><span data-stu-id="414d8-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="414d8-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="414d8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="414d8-106">Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="414d8-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="414d8-107">V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="414d8-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="414d8-108">V tomto kurzu se dozvíte, jak přidat vlastní trasu do ASP.NET aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="414d8-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="414d8-109">Dozvíte se, jak upravit výchozí směrovací tabulku v souboru Global.asax s vlastní trasou.</span><span class="sxs-lookup"><span data-stu-id="414d8-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="414d8-110">V ASP.NET aplikací MVC bude výchozí směrovací tabulka fungovat dobře.</span><span class="sxs-lookup"><span data-stu-id="414d8-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="414d8-111">Můžete však zjistit, že máte specializované potřeby směrování.</span><span class="sxs-lookup"><span data-stu-id="414d8-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="414d8-112">V takovém případě můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="414d8-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="414d8-113">Představte si například, že vytváříte blogovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="414d8-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="414d8-114">Můžete chtít zpracovat příchozí požadavky, které vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="414d8-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="414d8-115">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="414d8-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="414d8-116">Když uživatel zadá tento požadavek, chcete vrátit položku blogu, která odpovídá datu 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="414d8-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="414d8-117">Chcete-li zpracovat tento typ požadavku, musíte vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="414d8-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="414d8-118">Soubor Global.asax v seznamu 1 obsahuje novou vlastní trasu s názvem Blog, která zpracovává požadavky, které vypadají jako /Archive/*datum zadání*.</span><span class="sxs-lookup"><span data-stu-id="414d8-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="414d8-119">**Výpis 1 - Global.asax (s vlastní trasou)**</span><span class="sxs-lookup"><span data-stu-id="414d8-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="414d8-120">Pořadí tras, které přidáte do tabulky tras, je důležité.</span><span class="sxs-lookup"><span data-stu-id="414d8-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="414d8-121">Naše nová vlastní trasa blogu je přidána před existující výchozí trasu.</span><span class="sxs-lookup"><span data-stu-id="414d8-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="414d8-122">Pokud jste stornovat pořadí, pak výchozí trasa vždy dostane volána namísto vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="414d8-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="414d8-123">Vlastní blog směrování odpovídá všechny požadavky, které začínají /Archive/.</span><span class="sxs-lookup"><span data-stu-id="414d8-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="414d8-124">Takže odpovídá všem následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="414d8-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="414d8-125">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="414d8-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="414d8-126">/Archiv/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="414d8-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="414d8-127">/Archiv/jablko</span><span class="sxs-lookup"><span data-stu-id="414d8-127">/Archive/apple</span></span>

<span data-ttu-id="414d8-128">Vlastní trasa mapuje příchozí požadavek na řadič s názvem Archive a vyvolá akci Entry().</span><span class="sxs-lookup"><span data-stu-id="414d8-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="414d8-129">Při volání Entry() metoda je volána, datum zadání je předán jako parametr s názvem entryDate.</span><span class="sxs-lookup"><span data-stu-id="414d8-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="414d8-130">Vlastní trasu blogu můžete použít s ovladačem v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="414d8-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="414d8-131">**Výpis 2 - ArchiveController.vb**</span><span class="sxs-lookup"><span data-stu-id="414d8-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="414d8-132">Všimněte si, že Entry() metoda v Výpis 2 přijímá parametr typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="414d8-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="414d8-133">Rozhraní MVC je dostatečně inteligentní, aby automaticky převádí datum zadání z adresy URL na hodnotu DateTime.</span><span class="sxs-lookup"><span data-stu-id="414d8-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="414d8-134">Pokud parametr data zadání z adresy URL nelze převést na DateTime, je vyvolána chyba (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="414d8-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="414d8-135">**Obrázek 1 – Chyba z převodu parametru**</span><span class="sxs-lookup"><span data-stu-id="414d8-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="414d8-136">[![Dialogové okno New Project (Nový projekt)](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="414d8-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="414d8-137">**Obrázek 01**: Chyba při převodu parametru[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-custom-routes-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="414d8-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="414d8-138">Souhrn</span><span class="sxs-lookup"><span data-stu-id="414d8-138">Summary</span></span>

<span data-ttu-id="414d8-139">Cílem tohoto kurzu bylo ukázat, jak můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="414d8-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="414d8-140">Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global.asax, který představuje položky blogu.</span><span class="sxs-lookup"><span data-stu-id="414d8-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="414d8-141">Diskutovali jsme o tom, jak mapovat požadavky na položky blogu na řadič s názvem ArchiveController a akce řadiče s názvem Entry().</span><span class="sxs-lookup"><span data-stu-id="414d8-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="414d8-142">[Předchozí](asp-net-mvc-controller-overview-vb.md)
> [další](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="414d8-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
