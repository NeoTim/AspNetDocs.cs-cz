---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Vytváření vlastních tras (C#) | Dokumentace Microsoftu
author: microsoft
description: Zjistěte, jak přidat vlastní trasy pro aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak změnit výchozí směrovací tabulka v souboru Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 7b7324c9e0518697c0978b96b0123cb44133722b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418934"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="f9513-104">Vytváření vlastních tras (C#)</span><span class="sxs-lookup"><span data-stu-id="f9513-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="f9513-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f9513-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f9513-106">Zjistěte, jak přidat vlastní trasy pro aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f9513-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="f9513-107">V tomto kurzu se dozvíte, jak změnit výchozí směrovací tabulka v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="f9513-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="f9513-108">V tomto kurzu se dozvíte, jak přidat vlastní trasy pro aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f9513-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="f9513-109">Zjistíte, jak změnit výchozí směrovací tabulka v souboru Global.asax s vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="f9513-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="f9513-110">Pro mnoho jednoduché aplikace ASP.NET MVC bude výchozí směrovací tabulka fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="f9513-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="f9513-111">Však můžete zjistit, že používáte specializovaný směrování potřebám.</span><span class="sxs-lookup"><span data-stu-id="f9513-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="f9513-112">V takovém případě můžete vytvořit vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="f9513-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="f9513-113">Představte si například, že vytváříte aplikaci blogu.</span><span class="sxs-lookup"><span data-stu-id="f9513-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="f9513-114">Můžete chtít zpracovat příchozí požadavky, které vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="f9513-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="f9513-115">/ Archivu/12 – 25-2009</span><span class="sxs-lookup"><span data-stu-id="f9513-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="f9513-116">Když uživatel zadá tento požadavek, chcete vrátit blogu, který odpovídá na datum 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="f9513-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="f9513-117">Aby bylo možné zpracovávat tento typ požadavku, je potřeba vytvořit vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="f9513-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="f9513-118">Výpis 1 soubor Global.asax obsahuje novou vlastní trasu s názvem blogu, které zpracovává požadavky, které mají tvar /Archive/*datum položky*.</span><span class="sxs-lookup"><span data-stu-id="f9513-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

**<span data-ttu-id="f9513-119">Výpis 1 - Global.asax (s vlastní směrování)</span><span class="sxs-lookup"><span data-stu-id="f9513-119">Listing 1 - Global.asax (with custom route)</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="f9513-120">Je důležité pořadí tras, které přidáte do směrovací tabulky.</span><span class="sxs-lookup"><span data-stu-id="f9513-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="f9513-121">Před existující výchozí trasa se přidá naši novou vlastní trasu blogu.</span><span class="sxs-lookup"><span data-stu-id="f9513-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="f9513-122">Pokud je obrácený pořadí, pak výchozí trasu vždy bude zavolána místo vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="f9513-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="f9513-123">Vlastní Blog trasa odpovídá všechny požadavky, které začíná/archivu /.</span><span class="sxs-lookup"><span data-stu-id="f9513-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="f9513-124">Ano splňuje všechna následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="f9513-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="f9513-125">/ Archivu/12 – 25-2009</span><span class="sxs-lookup"><span data-stu-id="f9513-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="f9513-126">/ Archivu/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="f9513-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="f9513-127">/ Archivu/apple</span><span class="sxs-lookup"><span data-stu-id="f9513-127">/Archive/apple</span></span>

<span data-ttu-id="f9513-128">Vlastní trasy příchozí požadavek se mapuje na kontroler s názvem Archiv a vyvolá akci Entry().</span><span class="sxs-lookup"><span data-stu-id="f9513-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="f9513-129">Při volání metody Entry() datum položky se předá jako parametr s názvem entryDate.</span><span class="sxs-lookup"><span data-stu-id="f9513-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="f9513-130">Blog vlastní trasy můžete použít u kontroleru v zobrazení 2.</span><span class="sxs-lookup"><span data-stu-id="f9513-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

**<span data-ttu-id="f9513-131">Výpis 2 - ArchiveController.cs</span><span class="sxs-lookup"><span data-stu-id="f9513-131">Listing 2 - ArchiveController.cs</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="f9513-132">Všimněte si, že metoda Entry() ve výpisu 2 přijímá parametr typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="f9513-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="f9513-133">Architektura MVC je dostatečně inteligentní, aby automaticky převést datum položky z adresy URL na hodnotu data a času.</span><span class="sxs-lookup"><span data-stu-id="f9513-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="f9513-134">Je-li parametr vstupní data z adresy URL nelze převést na typ DateTime, je vyvolána k chybě (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="f9513-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

**<span data-ttu-id="f9513-135">Obrázek 1 – Chyba z převodu parametru</span><span class="sxs-lookup"><span data-stu-id="f9513-135">Figure 1 - Error from converting parameter</span></span>**


[![T<span data-ttu-id="f9513-136">Dialogové okno Nový projekt he]</span><span class="sxs-lookup"><span data-stu-id="f9513-136">he New Project dialog box]</span></span>(creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

<span data-ttu-id="f9513-137">**Obrázek 01**: Chyba z převodu parametru ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="f9513-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="f9513-138">Souhrn</span><span class="sxs-lookup"><span data-stu-id="f9513-138">Summary</span></span>

<span data-ttu-id="f9513-139">Cílem tohoto kurzu bylo ukazují, jak můžete vytvořit vlastní trasy.</span><span class="sxs-lookup"><span data-stu-id="f9513-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="f9513-140">Jste zjistili, jak přidat vlastní trasy do směrovací tabulky v souboru Global.asax, která představuje dostupné zápisy z blogu.</span><span class="sxs-lookup"><span data-stu-id="f9513-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="f9513-141">Jsme probírali jak mapovat požadavky na zápisy z blogu řadič ArchiveController a s názvem Entry() akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="f9513-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f9513-142">[Předchozí](aspnet-mvc-controllers-overview-cs.md)
> [další](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f9513-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
