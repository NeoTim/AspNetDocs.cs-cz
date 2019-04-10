---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Zjistěte, jak vytvářet testy částí pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, jestli akce kontroleru vrátí sloupce části...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 1193d7dc6fc29dfdac5637c9391a82f9f3566073
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59407728"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="60f1f-104">Vytváření testů jednotek pro aplikace ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="60f1f-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="60f1f-105">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="60f1f-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="60f1f-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="60f1f-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="60f1f-107">Zjistěte, jak vytvářet testy částí pro akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="60f1f-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="60f1f-108">V tomto kurzu Stephen Walther ukazuje, jak otestovat, jestli akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sady dat nebo vrátí jiný typ výsledku akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="60f1f-109">Cílem tohoto kurzu je předvést, jak psát testy jednotek pro kontrolery v ASP.NET MVC aplikace.</span><span class="sxs-lookup"><span data-stu-id="60f1f-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="60f1f-110">Pojednává o vytváření tří různých typů testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="60f1f-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="60f1f-111">Zjistíte, jak prohlížeč vrácené akcí kontroleru testů, jak testovat zobrazení dat vrácených akce kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="60f1f-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="60f1f-112">Vytvoření Kontroleru v rámci testu</span><span class="sxs-lookup"><span data-stu-id="60f1f-112">Creating the Controller under Test</span></span>

<span data-ttu-id="60f1f-113">Začněme vytvořením kontroleru, který chceme otestovat.</span><span class="sxs-lookup"><span data-stu-id="60f1f-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="60f1f-114">Kontroler, s názvem `ProductController`, je obsažen v informacích 1.</span><span class="sxs-lookup"><span data-stu-id="60f1f-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

**<span data-ttu-id="60f1f-115">Výpis 1 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-115">Listing 1 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="60f1f-116">`ProductController` Obsahuje dvě metody akce s názvem `Index()` a `Details()`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="60f1f-117">Obě metody akce vracejí zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-117">Both action methods return a view.</span></span> <span data-ttu-id="60f1f-118">Všimněte si, že `Details()` akce přijme parametr s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="60f1f-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="60f1f-119">Testování zobrazení vrácený Kontroleru</span><span class="sxs-lookup"><span data-stu-id="60f1f-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="60f1f-120">Představte si, že chceme otestovat, zda je či není `ProductController` vrátí z druhého zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="60f1f-121">Chceme, abyste měli jistotu, že `ProductController.Details()` akce je volána, vrátí se zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="60f1f-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="60f1f-122">Testovací třídy v informacích 2 obsahuje testování částí pro testování zobrazení vrácených `ProductController.Details()` akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

**<span data-ttu-id="60f1f-123">Výpis 2 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-123">Listing 2 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="60f1f-124">Třída v informacích 2 zahrnuje testovací metodu s názvem `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="60f1f-125">Tato metoda obsahuje tři řádky kódu.</span><span class="sxs-lookup"><span data-stu-id="60f1f-125">This method contains three lines of code.</span></span> <span data-ttu-id="60f1f-126">První řádek kódu vytvoří novou instanci třídy `ProductController` třídy.</span><span class="sxs-lookup"><span data-stu-id="60f1f-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="60f1f-127">Druhý řádek kódu vyvolá kontroleru `Details()` metody akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="60f1f-128">Nakonec poslední řádek kódu kontroly, zda zobrazení vrácené `Details()` akce je zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="60f1f-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="60f1f-129">`ViewResult.ViewName` Vlastnost představuje název zobrazení, které vrácený řadič.</span><span class="sxs-lookup"><span data-stu-id="60f1f-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="60f1f-130">Jeden velký upozornění o testování této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="60f1f-130">One big warning about testing this property.</span></span> <span data-ttu-id="60f1f-131">Existují dva způsoby, že řadič lze vrátit zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="60f1f-132">Kontroler explicitně lze vrátit zobrazení takto:</span><span class="sxs-lookup"><span data-stu-id="60f1f-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="60f1f-133">Název zobrazení, případně lze odvodit z název akce kontroleru takto:</span><span class="sxs-lookup"><span data-stu-id="60f1f-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="60f1f-134">Tato akce kontroleru vrátí také zobrazení s názvem `Details`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="60f1f-135">Název zobrazení je však odvozen z názvu akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="60f1f-136">Pokud chcete zobrazit název testu, pak musíte explicitně vrátit název zobrazení z akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="60f1f-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="60f1f-137">Můžete spustit testování částí v informacích 2 zadáním kombinace kláves **Ctrl-R, A** nebo kliknutím **spustit všechny testy v řešení** tlačítko (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="60f1f-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="60f1f-138">Pokud je test úspěšný, zobrazí se vám okně Výsledky testu na obrázku 2.</span><span class="sxs-lookup"><span data-stu-id="60f1f-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


[![R<span data-ttu-id="60f1f-139">Zrušit všechny testy v řešení]</span><span class="sxs-lookup"><span data-stu-id="60f1f-139">un All Tests in Solution]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

<span data-ttu-id="60f1f-140">**Obrázek 01**: Spustit všechny testy v řešení ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="60f1f-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


[![S<span data-ttu-id="60f1f-141">uccess!]</span><span class="sxs-lookup"><span data-stu-id="60f1f-141">uccess!]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

<span data-ttu-id="60f1f-142">**Obrázek 02**: Úspěch!</span><span class="sxs-lookup"><span data-stu-id="60f1f-142">**Figure 02**: Success!</span></span> <span data-ttu-id="60f1f-143">([Kliknutím ji zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="60f1f-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="60f1f-144">Testování zobrazení dat vrácených Kontroleru</span><span class="sxs-lookup"><span data-stu-id="60f1f-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="60f1f-145">Kontroler MVC předá data k zobrazení pomocí nástroje s názvem *`View Data`*.</span><span class="sxs-lookup"><span data-stu-id="60f1f-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="60f1f-146">Představte si například, že chcete zobrazit podrobnosti pro konkrétní produkt při vyvolání `ProductController Details()` akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="60f1f-147">V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předejte instanci `Details` zobrazení s využitím `View Data`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="60f1f-148">Upravené `ProductController` výpis 3 zahrnuje aktualizovanou `Details()` akci, která vrací produktu.</span><span class="sxs-lookup"><span data-stu-id="60f1f-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

**<span data-ttu-id="60f1f-149">Výpis 3 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-149">Listing 3 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="60f1f-150">Nejprve je potřeba `Details()` akce vytvoří novou instanci třídy `Product` třídu, která představuje přenosný počítač.</span><span class="sxs-lookup"><span data-stu-id="60f1f-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="60f1f-151">Další, instance `Product` třídy je předán jako druhý parametr `View()` metody.</span><span class="sxs-lookup"><span data-stu-id="60f1f-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="60f1f-152">Můžete napsat jednotkové testy k ověření, zda je očekávaná data obsažená v zobrazení data.</span><span class="sxs-lookup"><span data-stu-id="60f1f-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="60f1f-153">Testování jednotek v testech výpis 4, zda produktu představující přenosný počítač je vrácena při volání `ProductController Details()` metody akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

**<span data-ttu-id="60f1f-154">Část 4 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-154">Listing 4 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="60f1f-155">V informacích 4 `TestDetailsView()` metoda otestováním zobrazení dat vrácených volání `Details()` metody.</span><span class="sxs-lookup"><span data-stu-id="60f1f-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="60f1f-156">`ViewData` Vystavena jako vlastnost na `ViewResult` vrátil vyvoláním `Details()` metody.</span><span class="sxs-lookup"><span data-stu-id="60f1f-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="60f1f-157">`ViewData.Model` Vlastnost obsahuje produkt předána do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="60f1f-158">Test jednoduše ověří, zda produktu obsažené v zobrazení dat má název přenosném počítači.</span><span class="sxs-lookup"><span data-stu-id="60f1f-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="60f1f-159">Testování výsledek akce vrácené Kontroleru</span><span class="sxs-lookup"><span data-stu-id="60f1f-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="60f1f-160">Složitější akce kontroleru může vrátit různé typy výsledků akcí v závislosti na hodnoty parametrů předaných pracovnímu akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="60f1f-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="60f1f-161">Akce kontroleru vrátit různé typy výsledků akcí, včetně `ViewResult`, `RedirectToRouteResult`, nebo `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="60f1f-162">Například upravené `Details()` vrátí v informacích 5 akci `Details` zobrazit při předání platný kód product Id akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="60f1f-163">Pokud předáte neplatné Id produktu – Id s hodnotou, menší než 1 – budete přesměrováni `Index()` akce.</span><span class="sxs-lookup"><span data-stu-id="60f1f-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

**<span data-ttu-id="60f1f-164">Výpis 5 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-164">Listing 5 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="60f1f-165">Můžete otestovat chování `Details()` akce s testováním částí v informacích 6.</span><span class="sxs-lookup"><span data-stu-id="60f1f-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="60f1f-166">Testování částí v informacích 6 ověřuje, že budete přesměrováni na `Index` zobrazovat, když se Id s hodnotou -1 je předána `Details()` metody.</span><span class="sxs-lookup"><span data-stu-id="60f1f-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

**<span data-ttu-id="60f1f-167">Výpis 6 –</span><span class="sxs-lookup"><span data-stu-id="60f1f-167">Listing 6 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="60f1f-168">Při volání `RedirectToAction()` metoda akce kontroleru, akce kontroleru vrátí `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="60f1f-169">Test zkontroluje, jestli `RedirectToRouteResult` přesměruje uživatele na kontroler akce s názvem `Index`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="60f1f-170">Souhrn</span><span class="sxs-lookup"><span data-stu-id="60f1f-170">Summary</span></span>

<span data-ttu-id="60f1f-171">V tomto kurzu jste zjistili, jak vytvářet testy částí pro akce řadiče MVC.</span><span class="sxs-lookup"><span data-stu-id="60f1f-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="60f1f-172">Nejdřív jste zjistili, jak ověřit, jestli je akce kontroleru vrácený z druhého zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="60f1f-173">Naučili jste se použít `ViewResult.ViewName` vlastnost ověřte název zobrazení.</span><span class="sxs-lookup"><span data-stu-id="60f1f-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="60f1f-174">Dále jsme se zaměřili na tom, jak můžete otestovat obsah `View Data`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="60f1f-175">Jste zjistili, jak zkontrolovat, zda byl vrácen správný produkt v `View Data` po volání metody akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="60f1f-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="60f1f-176">Nakonec jsme zmínili, jak můžete zkontrolovat, jestli se z akce kontroleru vrátí různé typy výsledků akcí.</span><span class="sxs-lookup"><span data-stu-id="60f1f-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="60f1f-177">Jste zjistili, jak chcete otestovat, jestli kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="60f1f-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="60f1f-178">Next</span><span class="sxs-lookup"><span data-stu-id="60f1f-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
