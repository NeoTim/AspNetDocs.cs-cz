---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Vytváření vlastních tras (VB) | Microsoft Docs
author: microsoft
description: Naučte se přidávat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se naučíte, jak změnit výchozí směrovací tabulku v souboru Global. asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601295"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="fe994-104">Vytváření vlastních tras (VB)</span><span class="sxs-lookup"><span data-stu-id="fe994-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="fe994-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fe994-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fe994-106">Naučte se přidávat vlastní trasy do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe994-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="fe994-107">V tomto kurzu se naučíte, jak změnit výchozí směrovací tabulku v souboru Global. asax.</span><span class="sxs-lookup"><span data-stu-id="fe994-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="fe994-108">V tomto kurzu se dozvíte, jak přidat vlastní trasu do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe994-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="fe994-109">Naučíte se, jak upravit výchozí směrovací tabulku v souboru Global. asax pomocí vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="fe994-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="fe994-110">V aplikacích ASP.NET MVC bude výchozí směrovací tabulka fungovat přesně přesně.</span><span class="sxs-lookup"><span data-stu-id="fe994-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="fe994-111">Můžete ale zjistit, že máte specializované požadavky na směrování.</span><span class="sxs-lookup"><span data-stu-id="fe994-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="fe994-112">V takovém případě můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="fe994-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="fe994-113">Představte si například, že vytváříte aplikaci blogu.</span><span class="sxs-lookup"><span data-stu-id="fe994-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="fe994-114">Můžete chtít zpracovat příchozí požadavky, které vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="fe994-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="fe994-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="fe994-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="fe994-116">Když uživatel zadá tuto žádost, budete chtít vrátit položku blogu, která odpovídá datu 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="fe994-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="fe994-117">Aby bylo možné tento typ žádosti zpracovat, je nutné vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="fe994-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="fe994-118">Soubor Global. asax v seznamu 1 obsahuje novou vlastní trasu s názvem blog, která zpracovává požadavky, které vypadají jako/Archive/*Datum vstupu*.</span><span class="sxs-lookup"><span data-stu-id="fe994-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="fe994-119">**Výpis 1-Global. asax (s vlastním směrováním)**</span><span class="sxs-lookup"><span data-stu-id="fe994-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="fe994-120">Pořadí tras, které přidáte do směrovací tabulky, je důležité.</span><span class="sxs-lookup"><span data-stu-id="fe994-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="fe994-121">Do existující výchozí trasy se přidá nová vlastní trasa blogu.</span><span class="sxs-lookup"><span data-stu-id="fe994-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="fe994-122">Pokud jste objednávku přeměnili, bude se výchozí trasa místo vlastní trasy volat vždy.</span><span class="sxs-lookup"><span data-stu-id="fe994-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="fe994-123">Vlastní trasa blogu odpovídá všem žádostem, které začínají na/Archive/.</span><span class="sxs-lookup"><span data-stu-id="fe994-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="fe994-124">Proto odpovídá všem následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="fe994-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="fe994-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="fe994-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="fe994-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="fe994-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="fe994-127">/Archive/apple</span><span class="sxs-lookup"><span data-stu-id="fe994-127">/Archive/apple</span></span>

<span data-ttu-id="fe994-128">Vlastní trasa mapuje příchozí požadavek na kontroler s názvem Archive a vyvolá akci entry ().</span><span class="sxs-lookup"><span data-stu-id="fe994-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="fe994-129">Při volání metody entry () se datum položky předává jako parametr s názvem entryDate.</span><span class="sxs-lookup"><span data-stu-id="fe994-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="fe994-130">Můžete použít vlastní trasu blogu s řadičem v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="fe994-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="fe994-131">**Výpis 2-ArchiveController. vb**</span><span class="sxs-lookup"><span data-stu-id="fe994-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="fe994-132">Všimněte si, že metoda Entry () v seznamu 2 přijímá parametr typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="fe994-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="fe994-133">Rozhraní MVC je dostatečně inteligentní, aby bylo možné převést datum zadání z adresy URL na hodnotu DateTime automaticky.</span><span class="sxs-lookup"><span data-stu-id="fe994-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="fe994-134">Pokud nelze parametr data entry z adresy URL převést na typ DateTime, je vyvolána chyba (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="fe994-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="fe994-135">**Obrázek 1 – Chyba při převádění parametru**</span><span class="sxs-lookup"><span data-stu-id="fe994-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="fe994-136">[![dialogového okna Nový projekt](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fe994-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="fe994-137">**Obrázek 01**: Chyba při převádění parametru ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fe994-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="fe994-138">Souhrn</span><span class="sxs-lookup"><span data-stu-id="fe994-138">Summary</span></span>

<span data-ttu-id="fe994-139">Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní trasu.</span><span class="sxs-lookup"><span data-stu-id="fe994-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="fe994-140">Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global. asax, který představuje položky blogu.</span><span class="sxs-lookup"><span data-stu-id="fe994-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="fe994-141">Probrali jsme, jak mapovat požadavky na položky blogu na kontroler s názvem ArchiveController a akci kontroleru s názvem entry ().</span><span class="sxs-lookup"><span data-stu-id="fe994-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fe994-142">[Předchozí](asp-net-mvc-controller-overview-vb.md)
> [Další](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fe994-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
