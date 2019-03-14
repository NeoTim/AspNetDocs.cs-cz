---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Začínáme s AJAX Control Toolkit (C#) | Dokumentace Microsoftu
author: microsoft
description: Přečtěte si všechno, co potřebujete vědět, abyste mohli začít používat sadou nástrojů AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ecf716b78a789ca72e8b35e0be3e1fd0b957052
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074386"
---
<a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="16a6b-103">Začínáme se sadou nástrojů AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="16a6b-103">Get Started with the AJAX Control Toolkit (C#)</span></span>
====================
<span data-ttu-id="16a6b-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="16a6b-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="16a6b-105">Přečtěte si všechno, co potřebujete vědět, abyste mohli začít používat sadou nástrojů AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="16a6b-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="16a6b-106">Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatné ovládací prvky, které můžete použít ve svých aplikacích technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16a6b-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="16a6b-107">V tomto kurzu se dozvíte, jak stáhnout sadou nástrojů AJAX Control Toolkit a přidání ovládacích prvků nástrojů do vašich nástrojů Visual Studio nebo Visual Web Developer Express.</span><span class="sxs-lookup"><span data-stu-id="16a6b-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="16a6b-108">Stahuje se sadou nástrojů AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="16a6b-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="16a6b-109">[Sadou nástrojů AJAX Control Toolkit](http://devexpress.com/act) projekt open source vyvinutý členy komunity technologie ASP.NET a tým ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16a6b-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


<span data-ttu-id="16a6b-110">[![Stahuje se sadou nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16a6b-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="16a6b-111">**Obrázek 01**: Stahuje se sadou nástrojů AJAX Control Toolkit ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="16a6b-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="16a6b-112">Po stažení souboru, budete muset odblokovat soubor.</span><span class="sxs-lookup"><span data-stu-id="16a6b-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="16a6b-113">Klikněte pravým tlačítkem na soubor, vyberte vlastnosti a klikněte na tlačítko **Odblokovat** tlačítko (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="16a6b-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


<span data-ttu-id="16a6b-114">[![Odblokování souboru ZIP se sada nástrojů AJAX ovládacího prvku](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="16a6b-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="16a6b-115">**Obrázek 02**: Odblokování souboru ZIP se sada nástrojů AJAX ovládacího prvku ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="16a6b-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="16a6b-116">Po odblokování ho mohli rozbalit soubor: Klikněte pravým tlačítkem na soubor a vyberte **Extrahovat vše** nabídky.</span><span class="sxs-lookup"><span data-stu-id="16a6b-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="16a6b-117">Nyní jsme připraveni přidat sadu nástrojů do panelu nástrojů Visual Studio nebo Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="16a6b-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="16a6b-118">Přidávání do panelu nástrojů AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="16a6b-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="16a6b-119">Přidat sadu nástrojů do vašich nástrojů Visual Studio nebo Visual Web Developer je nejjednodušší způsob, jak používat sadou nástrojů AJAX Control Toolkit (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="16a6b-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="16a6b-120">Tímto způsobem můžete jednoduše přetáhnout toolkit ovládacího prvku do stránky Pokud chcete použít.</span><span class="sxs-lookup"><span data-stu-id="16a6b-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


<span data-ttu-id="16a6b-121">[![Sada nástrojů AJAX Control Toolkit se zobrazí v panelu nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="16a6b-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="16a6b-122">**Obrázek 03**: V panelu nástrojů zobrazí se sadou nástrojů AJAX Control Toolkit ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="16a6b-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="16a6b-123">Nejprve budete muset přidat kartu sadou nástrojů AJAX Control Toolkit do panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="16a6b-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="16a6b-124">Postupujte podle těchto kroků.</span><span class="sxs-lookup"><span data-stu-id="16a6b-124">Follow these steps.</span></span>

1. <span data-ttu-id="16a6b-125">Vytvoření nového webu ASP.NET tak, že vyberete možnost nabídky soubor, nový web.</span><span class="sxs-lookup"><span data-stu-id="16a6b-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="16a6b-126">Klikněte dvakrát na Default.aspx v okně Průzkumník řešení otevřete soubor v editoru.</span><span class="sxs-lookup"><span data-stu-id="16a6b-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="16a6b-127">Panel pod na kartě Obecné klikněte pravým tlačítkem a vyberte možnost nabídky **přidat kartu** (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="16a6b-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="16a6b-128">Zadejte novou kartu s názvem sadou nástrojů AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="16a6b-128">Enter a new tab named AJAX Control Toolkit.</span></span>


<span data-ttu-id="16a6b-129">[![Přidání nové karty](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="16a6b-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="16a6b-130">**Obrázek 04**: Přidání nové karty ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="16a6b-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="16a6b-131">Dále je třeba k přidávání ovládacích prvků AJAX Control Toolkit na nové kartě. Postupujte podle těchto kroků:</span><span class="sxs-lookup"><span data-stu-id="16a6b-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="16a6b-132">Klikněte pravým tlačítkem na pod kartě sadou nástrojů AJAX Control Toolkit a vyberte možnost nabídky **zvolit položky (viz obrázek 5)**.</span><span class="sxs-lookup"><span data-stu-id="16a6b-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="16a6b-133">Přejděte do umístění, kde rozzipoval. Sada nástrojů AJAX Control Toolkit a vyberte AjaxControlToolkit.dll sestavení.</span><span class="sxs-lookup"><span data-stu-id="16a6b-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


<span data-ttu-id="16a6b-134">[![Zvolte položky, které chcete přidat do panelu nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="16a6b-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="16a6b-135">**Obrázek 05**: Zvolte položky, které chcete přidat do panelu nástrojů ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="16a6b-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="16a6b-136">Po dokončení těchto kroků všechny ovládací prvky nástrojů se zobrazí ve vašich dovedností.</span><span class="sxs-lookup"><span data-stu-id="16a6b-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="16a6b-137">Upgrade na novou verzi sady nástrojů</span><span class="sxs-lookup"><span data-stu-id="16a6b-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="16a6b-138">Pokud byly pomocí starší verze sady nástrojů a teď potřebujete přesunout do novější verze jsou doporučené kroky:</span><span class="sxs-lookup"><span data-stu-id="16a6b-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="16a6b-139">Binární soubory – odstranit starou verzi AjaxControlToolkit.dll sestavení ze složky koše vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="16a6b-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="16a6b-140">Položky panelu nástrojů – odstranit kartu sadou nástrojů AJAX Control Toolkit a postupujte podle výše uvedené kroky a znovu vytvořit na kartu s novou verzi AjaxControlToolkit.dll sestavení.</span><span class="sxs-lookup"><span data-stu-id="16a6b-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="16a6b-141">Next</span><span class="sxs-lookup"><span data-stu-id="16a6b-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
