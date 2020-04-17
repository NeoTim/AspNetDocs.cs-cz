---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: Začínáme s AJAX Control Toolkit (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Naučte se vše, co potřebujete vědět, abyste mohli začít používat ajax control toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543558"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="29f32-103">Začínáme se sadou nástrojů AJAX Control Toolkit (VB)</span><span class="sxs-lookup"><span data-stu-id="29f32-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="29f32-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="29f32-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="29f32-105">Naučte se vše, co potřebujete vědět, abyste mohli začít používat ajax control toolkit.</span><span class="sxs-lookup"><span data-stu-id="29f32-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="29f32-106">Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatných ovládacích prvků, které můžete použít ve svých ASP.NET aplikacích.</span><span class="sxs-lookup"><span data-stu-id="29f32-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="29f32-107">V tomto kurzu se dozvíte, jak stáhnout sadu nástrojů AJAX Control Toolkit a přidat ovládací prvky sady nástrojů do sady nástrojů Visual Studio/Visual Web Developer Express.</span><span class="sxs-lookup"><span data-stu-id="29f32-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="29f32-108">Stažení sady nástrojů ajax control</span><span class="sxs-lookup"><span data-stu-id="29f32-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="29f32-109">[AJAX Control Toolkit](http://devexpress.com/act) je open source projekt vyvinutý členy ASP.NET komunity a ASP.NET týmu.</span><span class="sxs-lookup"><span data-stu-id="29f32-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="29f32-110">[![Stažení sady nástrojů ajax control](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="29f32-111">**Obrázek 01**: Stažení AJAX Control Toolkit[(Klikněte pro zobrazení full-size image)](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="29f32-112">Po stažení souboru je třeba soubor odblokovat.</span><span class="sxs-lookup"><span data-stu-id="29f32-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="29f32-113">Klikněte pravým tlačítkem myši na soubor, vyberte Vlastnosti a klikněte na tlačítko **Odblokovat** (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="29f32-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="29f32-114">[![Odblokování souboru ZIP sady NÁSTROJŮ ovládacího prvku AJAX](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="29f32-115">**Obrázek 02**: Odblokování AJAX Control Toolkit ZIP soubor[(Klikněte pro zobrazení full-size image)](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="29f32-116">Po odblokování souboru můžete rozbalit soubor: Klikněte pravým tlačítkem myši na soubor a vyberte volbu **Rozbalit vše.**</span><span class="sxs-lookup"><span data-stu-id="29f32-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="29f32-117">Nyní jsme připraveni přidat sadu nástrojů do sady nástrojů Visual Studio/Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="29f32-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="29f32-118">Přidání sady nástrojů AJAX Control Toolkit do sady nástrojů</span><span class="sxs-lookup"><span data-stu-id="29f32-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="29f32-119">Nejjednodušší způsob, jak použít sadu nástrojů AJAX Control Toolkit, je přidat sadu nástrojů do sady nástrojů Visual Studio/Visual Web Developer (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="29f32-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="29f32-120">Tímto způsobem můžete jednoduše přetáhnout ovládací prvek sady nástrojů na stránku, když jej chcete použít.</span><span class="sxs-lookup"><span data-stu-id="29f32-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="29f32-121">[![V sadě nástrojů se zobrazí sada nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="29f32-122">**Obrázek 03**: Ajax Control Toolkit se objeví v sadě[nástrojů(Klikněte pro zobrazení obrázku v plné velikosti)](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="29f32-123">Nejprve je třeba přidat kartu AJAX Control Toolkit do sady nástrojů.</span><span class="sxs-lookup"><span data-stu-id="29f32-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="29f32-124">Postupujte následovně.</span><span class="sxs-lookup"><span data-stu-id="29f32-124">Follow these steps.</span></span>

1. <span data-ttu-id="29f32-125">Vytvořte nový ASP.NET web výběrem možnosti menu Soubor, Nový web.</span><span class="sxs-lookup"><span data-stu-id="29f32-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="29f32-126">Poklepáním na soubor Default.aspx v okně Průzkumník řešení otevřete soubor v editoru.</span><span class="sxs-lookup"><span data-stu-id="29f32-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="29f32-127">Klikněte pravým tlačítkem myši na panel nástrojů pod kartou Obecné a vyberte možnost nabídky **Přidat kartu** (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="29f32-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="29f32-128">Zadejte novou kartu s názvem AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="29f32-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="29f32-129">[![Přidání nové karty](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="29f32-130">**Obrázek 04**: Přidání nové karty[(Kliknutím zobrazíte obrázek v plné velikosti)](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="29f32-131">Dále je třeba přidat ovládací prvky AJAX Control Toolkit na novou kartu. Postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="29f32-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="29f32-132">Klepněte pravým tlačítkem myši pod kartu Ajax Control Toolkit a vyberte volbu nabídky **Zvolit položky (viz obrázek 5).**</span><span class="sxs-lookup"><span data-stu-id="29f32-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="29f32-133">Přejděte do umístění, kde jste rozbalili sadu nástrojů AJAX Control Toolkit, a vyberte sestavu AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="29f32-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="29f32-134">[![Výběr položek, které chcete přidat do panelu nástrojů](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="29f32-135">**Obrázek 05**: Vyberte položky, které chcete přidat do panelu nástrojů([Kliknutím zobrazíte obrázek v plné velikosti)](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="29f32-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="29f32-136">Po dokončení těchto kroků se v sadě nástrojů zobrazí všechny ovládací prvky sady nástrojů.</span><span class="sxs-lookup"><span data-stu-id="29f32-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="29f32-137">Upgrade na novou verzi sady nástrojů</span><span class="sxs-lookup"><span data-stu-id="29f32-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="29f32-138">Pokud jste používali starší verzi sady Toolkit a nyní potřebujete přejít na novější verzi, postupujte podle následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="29f32-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="29f32-139">Binární soubory – Odstraňte starou verzi sestavení AjaxControlToolkit.dll ze složky Bin webu.</span><span class="sxs-lookup"><span data-stu-id="29f32-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="29f32-140">Položky panelu nástrojů - Odstraňte kartu AJAX Control Toolkit a postupujte podle výše uvedených kroků a znovu vytvořte kartu s novou verzí sestavení AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="29f32-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="29f32-141">[Předchozí](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [další](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="29f32-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
