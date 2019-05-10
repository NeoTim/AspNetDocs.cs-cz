---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: Vytvoření Kontroleru (VB) | Dokumentace Microsoftu
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak přidat řadič do aplikace ASP.NET MVC.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123629"
---
# <a name="creating-a-controller-vb"></a><span data-ttu-id="c0ff8-103">Vytvoření kontroleru (VB)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-103">Creating a Controller (VB)</span></span>

<span data-ttu-id="c0ff8-104">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c0ff8-105">V tomto kurzu Stephen Walther ukazuje, jak přidat řadič do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="c0ff8-106">Cílem tohoto kurzu je vysvětlují, jak vytvořit nové technologie ASP.NET MVC řadiče.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="c0ff8-107">Zjistíte, jak vytvořit kontrolery, pomocí nabídky přidat kontroler Visual Studio a tím, že ručně vytvoříte soubor třídy.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="c0ff8-108">Použití přidání Kontroleru nabídky</span><span class="sxs-lookup"><span data-stu-id="c0ff8-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="c0ff8-109">Klikněte pravým tlačítkem na složku řadiče v okně Průzkumník řešení Visual Studio a vybrat je nejjednodušší způsob, jak vytvořit nový řadič **přidat, řadič** nabídky (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="c0ff8-110">Výběrem této možnosti se otevře **přidat kontroler** dialogového okna (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="c0ff8-111">[![Dialogové okno Nový projekt](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-111">[![The New Project dialog box](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span></span>

<span data-ttu-id="c0ff8-112">**Obrázek 01**: Přidání nového řadiče ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c0ff8-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-vb/_static/image2.png))</span></span>

<span data-ttu-id="c0ff8-113">[![Dialogové okno Nový projekt](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-113">[![The New Project dialog box](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span></span>

<span data-ttu-id="c0ff8-114">**Obrázek 02**: Dialogové okno Přidat kontroler ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="c0ff8-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-vb/_static/image4.png))</span></span>

<span data-ttu-id="c0ff8-115">Všimněte si, že první část názvu kontroleru je zvýrazněn **přidat kontroler** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="c0ff8-116">Každý název kontroleru musí končit příponou *řadič*.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="c0ff8-117">Můžete například vytvořit řadič s názvem *ProductController* , ale ne řadič s názvem *produktu*.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="c0ff8-118">Pokud vytvoříte kontroler, který nebyl nalezen *řadič* příponu pak nebudete mít k vyvolání kontroleru.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="c0ff8-119">Neumožňuje tuto--mohu jste plýtvat nespočet hodin život označíte tuto chybu.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="c0ff8-120">**Výpis 1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="c0ff8-120">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

<span data-ttu-id="c0ff8-121">Vždy byste měli vytvořit řadiče ve složce řadiče.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="c0ff8-122">V opačném případě budete porušení konvence ASP.NET MVC a jinými vývojáři budou mít obtížnější čas pochopení vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="c0ff8-123">Metody akce generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="c0ff8-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="c0ff8-124">Když vytvoříte řadič, máte možnost automaticky vygenerovat metody akce vytvoření, aktualizace a podrobnosti (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="c0ff8-125">Pokud vyberete tuto možnost je vygenerována třída kontroleru v zobrazení 2.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="c0ff8-126">[![Automatické vytváření metody akce](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-126">[![Creating action methods automatically](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span></span>

<span data-ttu-id="c0ff8-127">**Obrázek 03**: Vytvoření metody akce automaticky ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c0ff8-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-vb/_static/image6.png))</span></span>

<span data-ttu-id="c0ff8-128">**Výpis 2 - Controllers\CustomerController.vb**</span><span class="sxs-lookup"><span data-stu-id="c0ff8-128">**Listing 2 - Controllers\CustomerController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

<span data-ttu-id="c0ff8-129">Tyto vygenerované metody jsou metody zástupných procedur.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-129">These generated methods are stub methods.</span></span> <span data-ttu-id="c0ff8-130">Je nutné přidat skutečné logiku pro vytváření, aktualizaci a zobrazení podrobností pro zákazníka sami.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="c0ff8-131">Ale se zakázaným inzerováním metody poskytují dobrý výchozí bod.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="c0ff8-132">Vytvoření třídy Kontroleru</span><span class="sxs-lookup"><span data-stu-id="c0ff8-132">Creating a Controller Class</span></span>

<span data-ttu-id="c0ff8-133">Kontroler ASP.NET MVC je jenom třídy.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="c0ff8-134">Pokud dáváte přednost, můžete ignorovat generování uživatelského rozhraní vhodné sady Visual Studio kontroleru a ručně vytvořit třídu kontroleru.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="c0ff8-135">Postupujte podle těchto kroků:</span><span class="sxs-lookup"><span data-stu-id="c0ff8-135">Follow these steps:</span></span>

1. <span data-ttu-id="c0ff8-136">Klikněte pravým tlačítkem na složku řadiče a vyberte možnost nabídky **přidat, nová položka** a vyberte **třídy** šablony (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="c0ff8-137">Pojmenujte novou třídu PersonController.vb a klikněte na tlačítko **přidat** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-137">Name the new class PersonController.vb and click the **Add** button.</span></span>
3. <span data-ttu-id="c0ff8-138">Upravte soubor výsledné třídy tak, aby třída dědí ze základní třídy System.Web.Mvc.Controller (viz seznam 3).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="c0ff8-139">[![Vytvoření nové třídy](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-139">[![Creating a new class](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span></span>

<span data-ttu-id="c0ff8-140">**Obrázek 04**: Vytvoření nové třídy ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="c0ff8-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-vb/_static/image8.png))</span></span>

<span data-ttu-id="c0ff8-141">**Výpis 3 - Controllers\PersonController.vb**</span><span class="sxs-lookup"><span data-stu-id="c0ff8-141">**Listing 3 - Controllers\PersonController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

<span data-ttu-id="c0ff8-142">Kontroler v informacích 3 poskytuje jednu akci s názvem Index(), který vrátí řetězec "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="c0ff8-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="c0ff8-143">Tato akce kontroleru můžete vyvolat spuštěním vaší aplikace a požaduje adresu URL takto:</span><span class="sxs-lookup"><span data-stu-id="c0ff8-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="c0ff8-144">Vývojový Server ASP.NET používá náhodný port číslo (například 40071).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="c0ff8-145">Při zadávání adresy URL pro vyvolání kontroleru, budete muset zadat číslo správný port.</span><span class="sxs-lookup"><span data-stu-id="c0ff8-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="c0ff8-146">Je-li určit číslo portu, najedete myší na ikonu pro vývojový Server ASP.NET v oznamovací oblasti Windows (vpravo dole na obrazovce).</span><span class="sxs-lookup"><span data-stu-id="c0ff8-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="c0ff8-147">[Předchozí](adding-dynamic-content-to-a-cached-page-vb.md)
> [další](creating-an-action-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c0ff8-147">[Previous](adding-dynamic-content-to-a-cached-page-vb.md)
[Next](creating-an-action-vb.md)</span></span>
