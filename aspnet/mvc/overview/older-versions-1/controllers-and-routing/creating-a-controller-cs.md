---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: Vytvoření kontroleru (C#) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete přidat kontroler do aplikace ASP.NET MVC.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e3d0bae7f07410637c2b06c500d94a02c821f5c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544077"
---
# <a name="creating-a-controller-c"></a><span data-ttu-id="fb59a-103">Vytvoření kontroleru (C#)</span><span class="sxs-lookup"><span data-stu-id="fb59a-103">Creating a Controller (C#)</span></span>

<span data-ttu-id="fb59a-104">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="fb59a-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="fb59a-105">V tomto kurzu Stephen Walther ukazuje, jak můžete přidat kontroler do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fb59a-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="fb59a-106">Cílem tohoto kurzu je vysvětlit, jak můžete vytvářet nové řadiče ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fb59a-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="fb59a-107">Naučíte se, jak vytvořit řadiče pomocí možnosti nabídky přidat řadič sady Visual Studio a vytvořit soubor třídy ručně.</span><span class="sxs-lookup"><span data-stu-id="fb59a-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="fb59a-108">Použití možnosti nabídky přidat řadič</span><span class="sxs-lookup"><span data-stu-id="fb59a-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="fb59a-109">Nejjednodušší způsob, jak vytvořit nový kontroler, je kliknout pravým tlačítkem myši na složku řadiče v okně Visual Studio Průzkumník řešení a vybrat možnost nabídky **Přidat, řadič** (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="fb59a-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="fb59a-110">Po výběru této možnosti nabídky se otevře dialogové okno **Přidat řadič** (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="fb59a-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="fb59a-111">[![dialogového okna Nový projekt](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fb59a-111">[![The New Project dialog box](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span></span>

<span data-ttu-id="fb59a-112">**Obrázek 01**: Přidání nového kontroleru ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fb59a-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>

<span data-ttu-id="fb59a-113">[![dialogového okna Nový projekt](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fb59a-113">[![The New Project dialog box](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span></span>

<span data-ttu-id="fb59a-114">**Obrázek 02**: dialogové okno Přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="fb59a-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>

<span data-ttu-id="fb59a-115">Všimněte si, že první část názvu kontroleru je zvýrazněna v dialogovém okně **Přidat řadič** .</span><span class="sxs-lookup"><span data-stu-id="fb59a-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="fb59a-116">Každý název kontroleru musí končit příponou *řadiče*.</span><span class="sxs-lookup"><span data-stu-id="fb59a-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="fb59a-117">Můžete například vytvořit kontrolér s názvem *ProductController* , ale ne kontroler s názvem *Product*.</span><span class="sxs-lookup"><span data-stu-id="fb59a-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="fb59a-118">Pokud vytvoříte kontroler, ve kterém chybí přípona *kontroleru* , nebudete moct tento kontroler vyvolat.</span><span class="sxs-lookup"><span data-stu-id="fb59a-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="fb59a-119">Tento postup neprovádějte – po této chybě už nedošlo k dlouhé hodinám svého životního cyklu.</span><span class="sxs-lookup"><span data-stu-id="fb59a-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="fb59a-120">**Výpis 1 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="fb59a-120">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="fb59a-121">Vždy byste měli vytvořit řadiče ve složce Controllers.</span><span class="sxs-lookup"><span data-stu-id="fb59a-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="fb59a-122">Jinak budete porušovat konvence ASP.NET MVC a další vývojáři budou mít obtížnější pochopit svou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fb59a-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="fb59a-123">Metody akcí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="fb59a-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="fb59a-124">Při vytváření kontroleru máte možnost automaticky generovat metody akcí vytvořit, aktualizovat a podrobnosti (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="fb59a-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="fb59a-125">Vyberete-li tuto možnost, je vygenerována třída Controller v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="fb59a-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="fb59a-126">[Automatické vytváření metod akcí ![](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fb59a-126">[![Creating action methods automatically](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span></span>

<span data-ttu-id="fb59a-127">**Obrázek 03**: automatické vytváření metod akcí ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="fb59a-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>

<span data-ttu-id="fb59a-128">**Výpis 2 – Controllers\CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="fb59a-128">**Listing 2 - Controllers\CustomerController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="fb59a-129">Tyto generované metody jsou zástupné metody.</span><span class="sxs-lookup"><span data-stu-id="fb59a-129">These generated methods are stub methods.</span></span> <span data-ttu-id="fb59a-130">Musíte přidat skutečnou logiku pro vytváření, aktualizaci a zobrazování podrobností pro zákazníka sami.</span><span class="sxs-lookup"><span data-stu-id="fb59a-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="fb59a-131">Ale metody zástupných procedur poskytují dobrý počáteční bod.</span><span class="sxs-lookup"><span data-stu-id="fb59a-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="fb59a-132">Vytvoření třídy kontroleru</span><span class="sxs-lookup"><span data-stu-id="fb59a-132">Creating a Controller Class</span></span>

<span data-ttu-id="fb59a-133">Kontroler MVC ASP.NET je pouze třída.</span><span class="sxs-lookup"><span data-stu-id="fb59a-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="fb59a-134">Pokud budete chtít, můžete ignorovat praktické generování uživatelského rozhraní kontroleru sady Visual Studio a vytvořit třídu kontroleru ručně.</span><span class="sxs-lookup"><span data-stu-id="fb59a-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="fb59a-135">Postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="fb59a-135">Follow these steps:</span></span>

1. <span data-ttu-id="fb59a-136">Klikněte pravým tlačítkem na složku řadiče a vyberte možnost nabídky **Přidat, nová položka** a vyberte šablonu **třídy** (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="fb59a-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="fb59a-137">Pojmenujte novou třídu PersonController.cs a klikněte na tlačítko **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="fb59a-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="fb59a-138">Upravte výsledný soubor třídy tak, aby třída dědila ze třídy Base System. Web. Mvc. Controller (viz výpis 3).</span><span class="sxs-lookup"><span data-stu-id="fb59a-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="fb59a-139">[![vytvoření nové třídy](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fb59a-139">[![Creating a new class](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span></span>

<span data-ttu-id="fb59a-140">**Obrázek 04**: vytvoření nové třídy ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="fb59a-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>

<span data-ttu-id="fb59a-141">**Výpis 3 – Controllers\PersonController.cs**</span><span class="sxs-lookup"><span data-stu-id="fb59a-141">**Listing 3 - Controllers\PersonController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="fb59a-142">Kontroler v seznamu 3 zpřístupňuje jednu akci s názvem index (), která vrací řetězec "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="fb59a-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="fb59a-143">Tuto akci kontroleru můžete vyvolat spuštěním aplikace a vyžádáním adresy URL, jako je následující:</span><span class="sxs-lookup"><span data-stu-id="fb59a-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="fb59a-144">ASP.NET Development Server používá náhodné číslo portu (například 40071).</span><span class="sxs-lookup"><span data-stu-id="fb59a-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="fb59a-145">Když zadáváte adresu URL pro vyvolání kontroleru, budete muset zadat správné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="fb59a-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="fb59a-146">Číslo portu můžete určit tak, že najedete myší na ikonu pro vývojový server ASP.NET v oznamovací oblasti systému Windows (dole vpravo na obrazovce).</span><span class="sxs-lookup"><span data-stu-id="fb59a-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="fb59a-147">[Předchozí](adding-dynamic-content-to-a-cached-page-cs.md)
> [Další](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fb59a-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
