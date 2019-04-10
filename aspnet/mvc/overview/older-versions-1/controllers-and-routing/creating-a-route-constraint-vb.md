---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Vytvoření omezení trasy (VB) | Dokumentace Microsoftu
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak prohlížeč požaduje shoda tras tak, že vytvoříte omezení trasy s regulárními výrazy.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 8c7b2274ff396f222382488ed877599e86ae5b99
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412681"
---
# <a name="creating-a-route-constraint-vb"></a><span data-ttu-id="6eb63-103">Vytvoření omezení trasy (VB)</span><span class="sxs-lookup"><span data-stu-id="6eb63-103">Creating a Route Constraint (VB)</span></span>

<span data-ttu-id="6eb63-104">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6eb63-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6eb63-105">V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak prohlížeč požaduje shoda tras tak, že vytvoříte omezení trasy s regulárními výrazy.</span><span class="sxs-lookup"><span data-stu-id="6eb63-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>


<span data-ttu-id="6eb63-106">Pomocí omezení trasy omezte požadavků prohlížeče, které odpovídají konkrétní trasy.</span><span class="sxs-lookup"><span data-stu-id="6eb63-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="6eb63-107">Regulární výraz můžete použít k určení omezení trasy.</span><span class="sxs-lookup"><span data-stu-id="6eb63-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="6eb63-108">Představte si například, kterou jste definovali trasy v informacích 1 v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="6eb63-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

**<span data-ttu-id="6eb63-109">Listing 1 - Global.asax.vb</span><span class="sxs-lookup"><span data-stu-id="6eb63-109">Listing 1 - Global.asax.vb</span></span>**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="6eb63-110">Výpis 1 obsahuje trasa s názvem produktu.</span><span class="sxs-lookup"><span data-stu-id="6eb63-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="6eb63-111">Trasy produktu můžete použít k mapování požadavků prohlížeče ProductController součástí výpis 2.</span><span class="sxs-lookup"><span data-stu-id="6eb63-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

**<span data-ttu-id="6eb63-112">Výpis 2 - Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="6eb63-112">Listing 2 - Controllers\ProductController.vb</span></span>**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="6eb63-113">Všimněte si, že akce Details() vystavené kontroler produktu přijímá jeden parametr s názvem productId.</span><span class="sxs-lookup"><span data-stu-id="6eb63-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="6eb63-114">Tento parametr je parametr celé číslo.</span><span class="sxs-lookup"><span data-stu-id="6eb63-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="6eb63-115">Trasy definované v informacích 1 se shodují s některým z následujících adres URL:</span><span class="sxs-lookup"><span data-stu-id="6eb63-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="6eb63-116">/ Produktu/23</span><span class="sxs-lookup"><span data-stu-id="6eb63-116">/Product/23</span></span>
- <span data-ttu-id="6eb63-117">/ Produktu/7</span><span class="sxs-lookup"><span data-stu-id="6eb63-117">/Product/7</span></span>

<span data-ttu-id="6eb63-118">Bohužel trasy se taky shodovat následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="6eb63-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="6eb63-119">/ Produktu/Bla</span><span class="sxs-lookup"><span data-stu-id="6eb63-119">/Product/blah</span></span>
- <span data-ttu-id="6eb63-120">/ Produktu/apple</span><span class="sxs-lookup"><span data-stu-id="6eb63-120">/Product/apple</span></span>

<span data-ttu-id="6eb63-121">Protože akce Details() očekává jako parametr celé číslo, požadavku, který obsahuje něco jiného než celočíselnou hodnotu způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="6eb63-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="6eb63-122">Například pokud do prohlížeče zadáte adresu URL /Product/apple pak zobrazí se chybová stránka na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="6eb63-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>


[![T<span data-ttu-id="6eb63-123">Dialogové okno Nový projekt he]</span><span class="sxs-lookup"><span data-stu-id="6eb63-123">he New Project dialog box]</span></span>(creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)

<span data-ttu-id="6eb63-124">**Obrázek 01**: Stránka rozbalit zobrazuje ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6eb63-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>


<span data-ttu-id="6eb63-125">Co vlastně chcete udělat, je odpovídá pouze adresy URL, které obsahují productId správné celé číslo.</span><span class="sxs-lookup"><span data-stu-id="6eb63-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="6eb63-126">Omezení můžete použít při definování trasy omezovat adresy URL, které odpovídají trasy.</span><span class="sxs-lookup"><span data-stu-id="6eb63-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="6eb63-127">Upravené trasy produktu ve výpisu 3 obsahuje omezení regulárního výrazu, který odpovídá jen celá čísla.</span><span class="sxs-lookup"><span data-stu-id="6eb63-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

**<span data-ttu-id="6eb63-128">Listing 3 - Global.asax.vb</span><span class="sxs-lookup"><span data-stu-id="6eb63-128">Listing 3 - Global.asax.vb</span></span>**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="6eb63-129">\D+ regulárního výrazu odpovídá jedné nebo více celých čísel.</span><span class="sxs-lookup"><span data-stu-id="6eb63-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="6eb63-130">Vlivem tohoto omezení trasy produkt tak, aby odpovídala následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="6eb63-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="6eb63-131">/ Produkt/3</span><span class="sxs-lookup"><span data-stu-id="6eb63-131">/Product/3</span></span>
- <span data-ttu-id="6eb63-132">/ Produktu/8999</span><span class="sxs-lookup"><span data-stu-id="6eb63-132">/Product/8999</span></span>

<span data-ttu-id="6eb63-133">Ale ne následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="6eb63-133">But not the following URLs:</span></span>

- <span data-ttu-id="6eb63-134">/ Produktu/apple</span><span class="sxs-lookup"><span data-stu-id="6eb63-134">/Product/apple</span></span>
- <span data-ttu-id="6eb63-135">/ Produktu</span><span class="sxs-lookup"><span data-stu-id="6eb63-135">/Product</span></span>

<span data-ttu-id="6eb63-136">Tyto požadavky prohlížeče bude zpracován adresou jiné cestě nebo, pokud nejsou žádné odpovídající trasy *prostředek se nenašel* se vrátí chyba.</span><span class="sxs-lookup"><span data-stu-id="6eb63-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6eb63-137">[Předchozí](creating-custom-routes-vb.md)
> [další](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6eb63-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
