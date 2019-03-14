---
title: Vytvořte svoji první aplikaci součásti syntaxe Razor
author: guardrex
description: Vytvoření podrobné Razor komponent aplikace a seznamte se základními koncepty součásti syntaxe Razor.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070870"
---
# <a name="build-your-first-razor-components-app"></a><span data-ttu-id="9c2eb-103">Vytvořte svoji první aplikaci součásti syntaxe Razor</span><span class="sxs-lookup"><span data-stu-id="9c2eb-103">Build your first Razor Components app</span></span>

<span data-ttu-id="9c2eb-104">Podle [Daniel Roth](https://github.com/danroth27) a [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="9c2eb-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="9c2eb-105">V tomto kurzu se dozvíte, jak vytvářet aplikace s komponentami Razor a ukazuje základní koncepty součásti syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-105">This tutorial shows you how to build an app with Razor Components and demonstrates basic Razor Components concepts.</span></span> <span data-ttu-id="9c2eb-106">Můžete využívat tento kurz pomocí obou součásti Razor na základě projektu (podporované v .NET Core 3.0 nebo novější) nebo pomocí aplikace project na základě Blazor (podporované v budoucích verzích .NET Core).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-106">You can enjoy this tutorial using either a Razor Components-based project (supported in .NET Core 3.0 or later) or using a Blazor-based project (supported in a future release of .NET Core).</span></span>

<span data-ttu-id="9c2eb-107">Pro prostředí pomocí technologie ASP.NET Core Razor součásti (*doporučuje*):</span><span class="sxs-lookup"><span data-stu-id="9c2eb-107">For an experience using ASP.NET Core Razor Components (*recommended*):</span></span>

* <span data-ttu-id="9c2eb-108">Postupujte podle pokynů v <xref:razor-components/get-started> k vytvoření projektu založeného na součásti syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-108">Follow the guidance in <xref:razor-components/get-started> to create a Razor Components-based project.</span></span>
* <span data-ttu-id="9c2eb-109">Pojmenujte projekt `RazorComponents`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-109">Name the project `RazorComponents`.</span></span>
* <span data-ttu-id="9c2eb-110">Řešení pro více projektů je vytvořen z šablony Razor komponenty.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-110">A multi-project solution is created from the Razor Components template.</span></span> <span data-ttu-id="9c2eb-111">Projekt součásti Razor je generován jako *RazorComponents.App*.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-111">The Razor Components project is generated as *RazorComponents.App*.</span></span>

<span data-ttu-id="9c2eb-112">Pro prostředí pomocí Blazor:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-112">For an experience using Blazor:</span></span>

* <span data-ttu-id="9c2eb-113">Postupujte podle pokynů v <xref:spa/blazor/get-started> k vytvoření projektu založeného na Blazor.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-113">Follow the guidance in <xref:spa/blazor/get-started> to create a Blazor-based project.</span></span>
* <span data-ttu-id="9c2eb-114">Pojmenujte projekt `Blazor`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-114">Name the project `Blazor`.</span></span>
* <span data-ttu-id="9c2eb-115">Řešení jednoho projektu je vytvořen z šablony Blazor.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-115">A single-project solution is created from the Blazor template.</span></span>

<span data-ttu-id="9c2eb-116">[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([stažení](xref:index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="9c2eb-117">Naleznete v následujících tématech pro požadavky:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-117">See the following topics for prerequisites:</span></span>

## <a name="build-components"></a><span data-ttu-id="9c2eb-118">Sestavení komponent</span><span class="sxs-lookup"><span data-stu-id="9c2eb-118">Build components</span></span>

1. <span data-ttu-id="9c2eb-119">Přejděte do všech tří stránek vaší aplikace: Domů čítač a načíst data.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-119">Browse to each of the app's three pages: Home, Counter, and Fetch data.</span></span> <span data-ttu-id="9c2eb-120">Tyto stránky jsou implementovány v souborech Razor v *stránky* složky: *Index.cshtml*, *Counter.cshtml*, a *FetchData.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-120">These pages are implemented by Razor files in the *Pages* folder: *Index.cshtml*, *Counter.cshtml*, and *FetchData.cshtml*.</span></span>

1. <span data-ttu-id="9c2eb-121">Na stránce čítače, vyberte **klikněte na mě** tlačítka se zvýší čítač bez aktualizace stránky.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-121">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="9c2eb-122">Zvyšování hodnoty čítače na webové stránce obvykle vyžaduje zadání jazyka JavaScript, ale součásti Razor poskytuje lepší přístup pomocí C#.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-122">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

1. <span data-ttu-id="9c2eb-123">Vyzkoušení implementace čítač součástí *Counter.cshtml* souboru.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-123">Examine the implementation of the Counter component in the *Counter.cshtml* file.</span></span>

   <span data-ttu-id="9c2eb-124">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-124">*Pages/Counter.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   <span data-ttu-id="9c2eb-125">Uživatelské rozhraní komponenty čítač je definován v jazyce HTML.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-125">The UI of the Counter component is defined using HTML.</span></span> <span data-ttu-id="9c2eb-126">Dynamické vykreslování logiku (například smyčky, podmíněné příkazy, výrazy) přidána pomocí vložený C# syntaxe volá [Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-126">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="9c2eb-127">Značka jazyka HTML a C# logiku vykreslení se převedou na třídu komponenty v okamžiku sestavení.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-127">The HTML markup and C# rendering logic are converted into a component class at build time.</span></span> <span data-ttu-id="9c2eb-128">Název generované třídy .NET odpovídá názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-128">The name of the generated .NET class matches the file name.</span></span>

   <span data-ttu-id="9c2eb-129">Členy třídy komponenty jsou definovány v `@functions` bloku.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-129">Members of the component class are defined in a `@functions` block.</span></span> <span data-ttu-id="9c2eb-130">V `@functions` blokovat, stav komponent (vlastnosti, pole) a metody jsou určené pro zpracování událostí nebo definování dalších součástí logiky.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-130">In the `@functions` block, component state (properties, fields) and methods are specified for event handling or for defining other component logic.</span></span> <span data-ttu-id="9c2eb-131">Tyto členy, se použije jako součást logiky komponenty vykreslování a pro zpracování událostí.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-131">These members are then used as part of the component's rendering logic and for handling events.</span></span>

   <span data-ttu-id="9c2eb-132">Když **klikněte na mě** výběru tlačítka:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-132">When the **Click me** button is selected:</span></span>

   * <span data-ttu-id="9c2eb-133">Součást čítače zaregistrované `onclick` obslužná rutina volána ( `IncrementCount` metoda).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-133">The Counter component's registered `onclick` handler is called (the `IncrementCount` method).</span></span>
   * <span data-ttu-id="9c2eb-134">Součást čítače obnoví jeho vykreslení stromu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-134">The Counter component regenerates its render tree.</span></span>
   * <span data-ttu-id="9c2eb-135">Nový vykreslovací stromu je ve srovnání s předchozím histogramem.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-135">The new render tree is compared to the previous one.</span></span>
   * <span data-ttu-id="9c2eb-136">Se použijí pouze změny do modelu Document Object Model (DOM).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-136">Only modifications to the Document Object Model (DOM) are applied.</span></span> <span data-ttu-id="9c2eb-137">Počet zobrazených se aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-137">The displayed count is updated.</span></span>

1. <span data-ttu-id="9c2eb-138">Upravit C# logiky součást čítače aby přírůstek počtu dvou místo jednoho.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-138">Modify the C# logic of the Counter component to make the count increment by two instead of one.</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. <span data-ttu-id="9c2eb-139">Znovu sestavte a spusťte aplikaci, aby se změny projevily.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-139">Rebuild and run the app to see the changes.</span></span> <span data-ttu-id="9c2eb-140">Vyberte **klikněte na mě** tlačítko a zvýší čítač ve dvou.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-140">Select the **Click me** button, and the counter increments by two.</span></span>

## <a name="use-components"></a><span data-ttu-id="9c2eb-141">Použití komponent</span><span class="sxs-lookup"><span data-stu-id="9c2eb-141">Use components</span></span>

<span data-ttu-id="9c2eb-142">Zahrnout součásti do jiné součásti pomocí syntaxe HTML.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-142">Include a component into another component using an HTML-like syntax.</span></span>

1. <span data-ttu-id="9c2eb-143">Přidat součást čítače pro součást aplikace indexu (Domovská stránka) tak, že přidáte `<Counter />` – element pro součást indexu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-143">Add the Counter component to the app's Index (home page) component by adding a `<Counter />` element to the Index component.</span></span>

   <span data-ttu-id="9c2eb-144">Pokud používáte Blazor pro toto prostředí, průzkum výzvy součásti (`<SurveyPrompt>` element) je v komponentě indexu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-144">If you're using Blazor for this experience, a Survey Prompt component (`<SurveyPrompt>` element) is in the Index component.</span></span> <span data-ttu-id="9c2eb-145">Nahraďte `<SurveyPrompt>` křížkem `<Counter>` elementu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-145">Replace the `<SurveyPrompt>` element with the `<Counter>` element.</span></span>

   <span data-ttu-id="9c2eb-146">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-146">*Pages/Index.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. <span data-ttu-id="9c2eb-147">Znovu sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-147">Rebuild and run the app.</span></span> <span data-ttu-id="9c2eb-148">Domovská stránka obsahuje vlastní čítače.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-148">The home page has its own counter.</span></span>

## <a name="component-parameters"></a><span data-ttu-id="9c2eb-149">Parametry komponenty</span><span class="sxs-lookup"><span data-stu-id="9c2eb-149">Component parameters</span></span>

<span data-ttu-id="9c2eb-150">Součástí mohou mít také parametry.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-150">Components can also have parameters.</span></span> <span data-ttu-id="9c2eb-151">Parametry komponenty jsou definovány pomocí vlastnosti neveřejné na komponentní třída dekorován `[Parameter]`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-151">Component parameters are defined using non-public properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="9c2eb-152">Atributy můžete zadat argumenty pro komponentu v kódu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-152">Use attributes to specify arguments for a component in markup.</span></span>

1. <span data-ttu-id="9c2eb-153">Aktualizace komponenty `@functions` C# kódu:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-153">Update the component's `@functions` C# code:</span></span>

   * <span data-ttu-id="9c2eb-154">Přidat `IncrementAmount` vlastnost upravené pomocí `[Parameter]` atribut.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-154">Add a `IncrementAmount` property decorated with the `[Parameter]` attribute.</span></span>
   * <span data-ttu-id="9c2eb-155">Změnit `IncrementCount` metoda se má použít `IncrementAmount` při zvýšit hodnotu `currentCount`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-155">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

   <span data-ttu-id="9c2eb-156">*Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-156">*Pages/Counter.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. <span data-ttu-id="9c2eb-157">Zadejte `IncrementAmount` parametr v komponentě domovské `<Counter>` pomocí atributu element.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-157">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span> <span data-ttu-id="9c2eb-158">Nastavte hodnotu čítače přírůstku deset.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-158">Set the value to increment the counter by ten.</span></span>

   <span data-ttu-id="9c2eb-159">*Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-159">*Pages/Index.cshtml*:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. <span data-ttu-id="9c2eb-160">Načtěte tuto stránku.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-160">Reload the page.</span></span> <span data-ttu-id="9c2eb-161">Domovská stránka čítače se zvýší o hodnotu deset pokaždé, když **klikněte na mě** výběru tlačítka.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-161">The home page counter increments by ten each time the **Click me** button is selected.</span></span> <span data-ttu-id="9c2eb-162">Čítače na *čítač* stránce zvýší o jedna.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-162">The counter on the *Counter* page increments by one.</span></span>

## <a name="route-to-components"></a><span data-ttu-id="9c2eb-163">Směrovat do komponenty</span><span class="sxs-lookup"><span data-stu-id="9c2eb-163">Route to components</span></span>

<span data-ttu-id="9c2eb-164">`@page` Direktiv v horní části *Counter.cshtml* soubor Určuje, že tato součást je koncový bod směrování.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-164">The `@page` directive at the top of the *Counter.cshtml* file specifies that this component is a routing endpoint.</span></span> <span data-ttu-id="9c2eb-165">Součást čítače zpracovává požadavky odeslané na `/Counter`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-165">The Counter component handles requests sent to `/Counter`.</span></span> <span data-ttu-id="9c2eb-166">Bez `@page` direktiv, komponenta nebude zpracovávat směrování žádostí, ale součást je stále možné ostatními komponentami.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-166">Without the `@page` directive, the component doesn't handle routed requests, but the component can still be used by other components.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="9c2eb-167">Injektáž závislostí</span><span class="sxs-lookup"><span data-stu-id="9c2eb-167">Dependency injection</span></span>

<span data-ttu-id="9c2eb-168">Služby zaregistrované v kontejneru aplikace služby jsou k dispozici na komponenty prostřednictvím [injektáž závislostí (DI)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-168">Services registered in the app's service container are available to components via [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="9c2eb-169">Vložit do součástí s použitím služby `@inject` směrnice.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-169">Inject services into a component using the `@inject` directive.</span></span>

<span data-ttu-id="9c2eb-170">Prozkoumat direktivy FetchData součásti (*Pages/FetchData.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-170">Examine the directives of the FetchData component (*Pages/FetchData.cshtml*).</span></span> <span data-ttu-id="9c2eb-171">`@inject` Směrnice slouží k vložení instance `WeatherForecastService` služby do komponenty:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-171">The `@inject` directive is used to inject the instance of the `WeatherForecastService` service into the component:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

<span data-ttu-id="9c2eb-172">`WeatherForecastService` Není registrován jako [singleton](xref:fundamentals/dependency-injection#service-lifetimes), takže jedna instance služby je k dispozici v rámci aplikace.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-172">The `WeatherForecastService` service is registered as a [singleton](xref:fundamentals/dependency-injection#service-lifetimes), so one instance of the service is available throughout the app.</span></span>

<span data-ttu-id="9c2eb-173">Komponenta FetchData používá vložený služby jako `ForecastService`, k načtení pole `WeatherForecast` objekty:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-173">The FetchData component uses the injected service, as `ForecastService`, to retrieve an array of `WeatherForecast` objects:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

<span data-ttu-id="9c2eb-174">A [ @foreach ](/dotnet/csharp/language-reference/keywords/foreach-in) smyčky se použije k vykreslení každou prognózy instanci jako řadu data o počasí v tabulce:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-174">A [@foreach](/dotnet/csharp/language-reference/keywords/foreach-in) loop is used to render each forecast instance as a row in the table of weather data:</span></span>

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a><span data-ttu-id="9c2eb-175">Vytvoření seznamu úkolů</span><span class="sxs-lookup"><span data-stu-id="9c2eb-175">Build a todo list</span></span>

<span data-ttu-id="9c2eb-176">Přidejte novou stránku do aplikace, která implementuje seznam úkolů.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-176">Add a new page to the app that implements a simple todo list.</span></span>

1. <span data-ttu-id="9c2eb-177">Přidat prázdný soubor *stránky* složku s názvem *Todo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-177">Add an empty file to the *Pages* folder named *Todo.cshtml*.</span></span>

1. <span data-ttu-id="9c2eb-178">Na stránce zadejte počáteční značky:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-178">Provide the initial markup for the page:</span></span>

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. <span data-ttu-id="9c2eb-179">Přidáte stránku Todo do navigačního panelu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-179">Add the Todo page to the navigation bar.</span></span>

   <span data-ttu-id="9c2eb-180">Komponenta NavMenu (*Shared/NavMenu.csthml*) se používá v rozložení aplikace.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-180">The NavMenu component (*Shared/NavMenu.csthml*) is used in the app's layout.</span></span> <span data-ttu-id="9c2eb-181">Rozložení jsou komponenty, které umožňují, aby se zabránilo duplicitě obsahu v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-181">Layouts are components that allow you to avoid duplication of content in the app.</span></span> <span data-ttu-id="9c2eb-182">Další informace naleznete v tématu <xref:razor-components/layouts>.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-182">For more information, see <xref:razor-components/layouts>.</span></span>

   <span data-ttu-id="9c2eb-183">Přidat `<NavLink>` Todo stránky tak, že přidáte následující značky položky seznamu níže existující položky seznamu v *Shared/NavMenu.csthml* souboru:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-183">Add a `<NavLink>` for the Todo page by adding the following list item markup below the existing list items in the *Shared/NavMenu.csthml* file:</span></span>

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. <span data-ttu-id="9c2eb-184">Znovu sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-184">Rebuild and run the app.</span></span> <span data-ttu-id="9c2eb-185">Na stránce Nový Todo potvrďte, že odkaz na stránku Todo funguje.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-185">Visit the new Todo page to confirm that the link to the Todo page works.</span></span>

1. <span data-ttu-id="9c2eb-186">Přidat *TodoItem.cs* souboru do kořenového adresáře projektu k uložení třídu, která představuje položku seznamu úkolů.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-186">Add a *TodoItem.cs* file to the root of the project to hold a class that represents a todo item.</span></span> <span data-ttu-id="9c2eb-187">Pomocí následujících C# kód `TodoItem` třídy:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-187">Use the following C# code for the `TodoItem` class:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. <span data-ttu-id="9c2eb-188">Vraťte se do komponenty Todo (*Todo.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="9c2eb-188">Return to the Todo component (*Todo.cshtml*):</span></span>

   * <span data-ttu-id="9c2eb-189">Přidání pole pro úloh, ať už v `@functions` bloku.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-189">Add a field for the todos in an `@functions` block.</span></span> <span data-ttu-id="9c2eb-190">Todo součásti používá toto pole pro uchování stavu pro seznam úkolů.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-190">The Todo component uses this field to maintain the state of the todo list.</span></span>
   * <span data-ttu-id="9c2eb-191">Přidat neuspořádaný seznam značek a `foreach` smyčky k vykreslení každé položky todo jako položku seznamu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-191">Add unordered list markup and a `foreach` loop to render each todo item as a list item.</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. <span data-ttu-id="9c2eb-192">Aplikace vyžaduje pro přidání do seznamu úloh, ať už prvky uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-192">The app requires UI elements for adding todos to the list.</span></span> <span data-ttu-id="9c2eb-193">Přidání textového zadání a tlačítka v seznamu níže:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-193">Add a text input and a button below the list:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. <span data-ttu-id="9c2eb-194">Znovu sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-194">Rebuild and run the app.</span></span> <span data-ttu-id="9c2eb-195">Když **přidat todo** se vybere tlačítko, nic se nestane, protože obslužná rutina události není svázanou tlačítka.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-195">When the **Add todo** button is selected, nothing happens because an event handler isn't wired up to the button.</span></span>

1. <span data-ttu-id="9c2eb-196">Přidat `AddTodo` metodu pro součást Todo a zaregistrujte ho pro tlačítko klikne pomocí `onclick` atribut:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-196">Add an `AddTodo` method to the Todo component and register it for button clicks using the `onclick` attribute:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   <span data-ttu-id="9c2eb-197">`AddTodo` C# Metoda je volána při výběru tlačítka.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-197">The `AddTodo` C# method is called when the button is selected.</span></span>

1. <span data-ttu-id="9c2eb-198">Pokud chcete získat název nové položky seznamu úkolů, přidejte `newTodo` řetězec pole a navázat jej na hodnotu text input pomocí `bind` atribut:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-198">To get the title of the new todo item, add a `newTodo` string field and bind it to the value of the text input using the `bind` attribute:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. <span data-ttu-id="9c2eb-199">Aktualizace `AddTodo` způsob, jak přidat `TodoItem` se zadaným názvem do seznamu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-199">Update the `AddTodo` method to add the `TodoItem` with the specified title to the list.</span></span> <span data-ttu-id="9c2eb-200">Smazat hodnotu textového zadání tak, že nastavíte `newTodo` na prázdný řetězec:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-200">Clear the value of the text input by setting `newTodo` to an empty string:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. <span data-ttu-id="9c2eb-201">Znovu sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-201">Rebuild and run the app.</span></span> <span data-ttu-id="9c2eb-202">Přidání některých úloh, ať už do seznamu k testování nového kódu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-202">Add some todos to the todo list to test the new code.</span></span>

1. <span data-ttu-id="9c2eb-203">Text nadpisu pro každou položku seznamu úkolů lze upravovat a zaškrtávací políčko může pomoci udržovat přehled o dokončené položky uživatele.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-203">The title text for each todo item can be made editable and a check box can help the user keep track of completed items.</span></span> <span data-ttu-id="9c2eb-204">Přidat vstup zaškrtněte políčko u každé položky todo a její hodnotu na vytvoření vazby `IsDone` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-204">Add a check box input for each todo item and bind its value to the `IsDone` property.</span></span> <span data-ttu-id="9c2eb-205">Změna `@todo.Title` do `<input>` prvek vázán na `@todo.Title`:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-205">Change `@todo.Title` to an `<input>` element bound to `@todo.Title`:</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. <span data-ttu-id="9c2eb-206">Chcete-li ověřit, že tyto hodnoty jsou vázány, aktualizujte `<h1>` záhlaví zobrazíte počet nesplněné položky seznamu úkolů nejsou kompletní (`IsDone` je `false`).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-206">To verify that these values are bound, update the `<h1>` header to show a count of the number of todo items that aren't complete (`IsDone` is `false`).</span></span>

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. <span data-ttu-id="9c2eb-207">Dokončené komponenty Todo (*Todo.cshtml*):</span><span class="sxs-lookup"><span data-stu-id="9c2eb-207">The completed Todo component (*Todo.cshtml*):</span></span>

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. <span data-ttu-id="9c2eb-208">Znovu sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-208">Rebuild and run the app.</span></span> <span data-ttu-id="9c2eb-209">Přidání položky seznamu úkolů k testování nového kódu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-209">Add todo items to test the new code.</span></span>

## <a name="publish-and-deploy-the-app"></a><span data-ttu-id="9c2eb-210">Publikování a nasazení aplikace</span><span class="sxs-lookup"><span data-stu-id="9c2eb-210">Publish and deploy the app</span></span>

<span data-ttu-id="9c2eb-211">Publikování aplikace, najdete v článku <xref:host-and-deploy/razor-components/index#publish-the-app>.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-211">To publish the app, see <xref:host-and-deploy/razor-components/index#publish-the-app>.</span></span>
