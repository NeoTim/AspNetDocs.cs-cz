---
title: Zobrazení v ASP.NET Core MVC
author: ardalis
description: Zjistěte, jak zpracovat zobrazení prezentace dat aplikace a interakce uživatelů v ASP.NET Core MVC.
ms.author: riande
ms.date: 12/12/2017
uid: mvc/views/overview
ms.openlocfilehash: 6c5b4d7b89ac07a85b5aad626e37855de98064eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069448"
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="4bd9f-103">Zobrazení v ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="4bd9f-103">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="4bd9f-104">Podle [Steve Smith](https://ardalis.com/) a [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="4bd9f-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4bd9f-105">Tento dokument popisuje zobrazení použít v aplikacích ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-105">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="4bd9f-106">Informace o stránky Razor, naleznete v tématu [Úvod do stránky Razor](xref:razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-106">For information on Razor Pages, see [Introduction to Razor Pages](xref:razor-pages/index).</span></span>

<span data-ttu-id="4bd9f-107">V modelu Model-View-Controller (MVC) *zobrazení* aplikace data prezentace a uživatelské interakce zpracovává.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-107">In the Model-View-Controller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="4bd9f-108">Zobrazení je šablonu HTML s vloženými [kód Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-108">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="4bd9f-109">Kód Razor je kód, který komunikuje s kódu HTML, který vytvoří webovou stránku, která je odeslána do klienta.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-109">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="4bd9f-110">V ASP.NET Core MVC se zobrazeními *.cshtml* soubory, které používají [programovací jazyk C#](/dotnet/csharp/) v kódu Razor.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-110">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="4bd9f-111">Obvykle jsou seskupené zobrazit soubory do složky s názvem pro jednotlivé aplikace [řadiče](xref:mvc/controllers/actions).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-111">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="4bd9f-112">Složky jsou uložené v *zobrazení* složku v kořenovém adresáři aplikace:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-112">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Zobrazení složky řešení Průzkumníka Visual Studio je otevřený a nabízí domovské složky otevřete zobrazení soubory About.cshtml Contact.cshtml a Index.cshtml](overview/_static/views_solution_explorer.png)

<span data-ttu-id="4bd9f-114">*Domů* kontroleru je reprezentována *Domů* složky uvnitř *zobrazení* složky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-114">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="4bd9f-115">*Domů* složka obsahuje zobrazení pro *o*, *kontakt*, a *Index* webové stránky (domovské stránky).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-115">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="4bd9f-116">Když si uživatel vyžádá jednu z těchto tří webových stránek, akce kontroleru v *Domů* řadič určit, který tři zobrazení, které se používá k sestavení a vrátit na webové stránce uživateli.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-116">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="4bd9f-117">Použití [rozložení](xref:mvc/views/layout) k zajištění konzistentní webové části a omezení opakování kódu.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-117">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="4bd9f-118">Rozložení často obsahují záhlaví, prvky navigace a nabídky a zápatí.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-118">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="4bd9f-119">Záhlaví a zápatí obvykle obsahuje často používaný kód pro mnoho prvků metadata a odkazy na skript a styl prostředky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-119">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="4bd9f-120">Rozložení umožňuje vyhnout se tento často používaný kód v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-120">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="4bd9f-121">[Částečná zobrazení](xref:mvc/views/partial) snížení dojde k duplikaci kódu pomocí správy opakovaně použitelné součásti zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-121">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="4bd9f-122">Například je užitečné pro Autor životopis na webu, blogu, který se zobrazí několik zobrazení částečného zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-122">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="4bd9f-123">Vytváření životopis je běžné zobrazení obsahu a nevyžaduje, aby kód provést, aby vytvoření obsahu pro webovou stránku.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-123">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="4bd9f-124">Autor životopis obsah je dostupný zobrazením vazby modelu samostatně, takže použití částečné zobrazení pro tento typ obsahu je ideální.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-124">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="4bd9f-125">[Zobrazení komponenty](xref:mvc/views/view-components) jsou podobná částečné zobrazení, umožňují omezení opakování kódu, ale jsou vhodné pro zobrazení obsahu, který vyžaduje kód pro spuštění na serveru k vykreslení na webovou stránku.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-125">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="4bd9f-126">Zobrazení komponenty jsou užitečné, když vykreslovaný obsah vyžaduje interakci databáze, například pro webovou stránku nákupní košík.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-126">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="4bd9f-127">Komponenty zobrazení nejsou omezeni na vazby modelu, aby bylo možné generovat výstup webové stránky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-127">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="4bd9f-128">Výhody použití zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-128">Benefits of using views</span></span>

<span data-ttu-id="4bd9f-129">Zobrazení nápovědy k navázání [oddělení oblastí zájmu](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) v rámci aplikace MVC oddělením značky uživatelského rozhraní od jiných částí aplikace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-129">Views help to establish [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="4bd9f-130">Podle SoC návrh umožňuje aplikaci modulární, který poskytuje několik výhod:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-130">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="4bd9f-131">Aplikace je snazší Údržba, protože je líp uspořádané.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-131">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="4bd9f-132">Zobrazení jsou obecně seskupené podle funkcí aplikace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-132">Views are generally grouped by app feature.</span></span> <span data-ttu-id="4bd9f-133">Díky tomu je snazší najít související zobrazení při práci na funkci.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-133">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="4bd9f-134">Součástí aplikace jsou volně vázány.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-134">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="4bd9f-135">Můžete vytvářet a aktualizovat zobrazení aplikace nezávisle na součásti obchodní logiku a data access.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-135">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="4bd9f-136">Zobrazení aplikace můžete změnit bez nutnosti nutně aktualizovat ostatní části aplikace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-136">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="4bd9f-137">Je snazší testování části uživatelského rozhraní aplikace, protože zobrazení jsou samostatné jednotky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-137">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="4bd9f-138">Kvůli lepší organizaci je méně pravděpodobné, že omylem opakováním části uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-138">Due to better organization, it's less likely that you'll accidentally repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="4bd9f-139">Vytvoření zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-139">Creating a view</span></span>

<span data-ttu-id="4bd9f-140">Zobrazení, které jsou specifické pro určitý kontroler vytvářejí *zobrazení / [parametr ControllerName]* složky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-140">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="4bd9f-141">Zobrazení, která jsou sdílena mezi řadiče jsou umístěny v *zobrazení/Shared* složky.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-141">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="4bd9f-142">Vytvoření zobrazení, přidejte nový soubor a poskytněte stejný název jako akcí k přidruženému kontroleru se *.cshtml* příponu souboru.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-142">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="4bd9f-143">Vytvoření zobrazení, která odpovídá *o* v akci *Domů* vytvoření kontroleru, *About.cshtml* ve *zobrazení Domů*složky:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-143">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="4bd9f-144">*Razor* značek začíná `@` symbol.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-144">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="4bd9f-145">Spusťte příkazy jazyka C# tak, že C# kódu v rámci [bloky kódu Razor](xref:mvc/views/razor#razor-code-blocks) nastavit ve složených závorkách (`{ ... }`).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-145">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="4bd9f-146">Příklad najdete v sekci přiřazení "O" `ViewData["Title"]` uvedené výše.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-146">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="4bd9f-147">Můžete jednoduše odkazující na hodnotu s zobrazit hodnoty v kódu HTML `@` symbol.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-147">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="4bd9f-148">Zobrazit obsah `<h2>` a `<h3>` prvků uvedených výše.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-148">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="4bd9f-149">Zobrazit obsah výše uvedené je pouze část celé webové stránky, které je vykresleno pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-149">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="4bd9f-150">Zbývající rozložení stránky a dalších běžných aspektů zobrazení jsou uvedeny v dalších souborů zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-150">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="4bd9f-151">Další informace najdete v tématu [rozložení tématu](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-151">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="4bd9f-152">Jak určit kontrolerů zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-152">How controllers specify views</span></span>

<span data-ttu-id="4bd9f-153">Zobrazení jsou obvykle vrácená z akce, jako je [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), což je typ [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-153">Views are typically returned from actions as a [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="4bd9f-154">Můžete vytvořit a vrátí metodu akce `ViewResult` přímo, ale neprovádí běžně.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-154">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="4bd9f-155">Protože většina řadičů dědit z [řadič](/dotnet/api/microsoft.aspnetcore.mvc.controller), jednoduše použít `View` pomocnou metodu se vraťte `ViewResult`:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-155">Since most controllers inherit from [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="4bd9f-156">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-156">*HomeController.cs*</span></span>

[!code-csharp[](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="4bd9f-157">Po návratu tato akce *About.cshtml* zobrazení je znázorněno v předchozí části se vykreslí jako na následující webové stránce:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-157">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![O stránku zpracovanou v prohlížeči Microsoft Edge](overview/_static/about-page.png)

<span data-ttu-id="4bd9f-159">`View` Pomocná metoda má několik přetížení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-159">The `View` helper method has several overloads.</span></span> <span data-ttu-id="4bd9f-160">Volitelně můžete zadat:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-160">You can optionally specify:</span></span>

* <span data-ttu-id="4bd9f-161">Explicitní zobrazení vrátit:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-161">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="4bd9f-162">A [modelu](xref:mvc/models/model-binding) k předání do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-162">A [model](xref:mvc/models/model-binding) to pass to the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="4bd9f-163">Zobrazení a modelu:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-163">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="4bd9f-164">Zobrazení zjišťování</span><span class="sxs-lookup"><span data-stu-id="4bd9f-164">View discovery</span></span>

<span data-ttu-id="4bd9f-165">Po návratu akce zobrazení, proces se nazývá *zobrazení zjišťování* probíhá.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-165">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="4bd9f-166">Tento proces Určuje soubor, který zobrazení se používá na základě názvu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-166">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="4bd9f-167">Výchozí chování `View` – metoda (`return View();`) je vrátit zobrazení s názvem, ze kterého je volána metoda akce.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-167">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="4bd9f-168">Například *o* `ActionResult` název metody kontroleru se používá k zobrazení souboru s názvem vyhledat *About.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-168">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="4bd9f-169">Nejprve, modul runtime hledá v *zobrazení / [parametr ControllerName]* složku pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-169">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="4bd9f-170">Pokud se nenajde odpovídající zobrazení, hledá *Shared* složku pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-170">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="4bd9f-171">Nebude vadit, když se implicitně vrátit `ViewResult` s `return View();` nebo explicitně předávat název zobrazení, který má `View` metodu s `return View("<ViewName>");`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-171">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="4bd9f-172">V obou případech zobrazení zjišťování vyhledá odpovídající soubor zobrazení v tomto pořadí:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-172">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="4bd9f-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="4bd9f-174">*Views/Shared/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-174">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="4bd9f-175">Místo názvu zobrazení lze zadat cestu k souboru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-175">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="4bd9f-176">Pokud se používá absolutní cesta od kořenové aplikace (volitelně můžete od verze "/" nebo "~ /"), *.cshtml* rozšíření je nutné zadat:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-176">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="4bd9f-177">Můžete také použít relativní cestu k určení zobrazení v různých adresářích bez *.cshtml* rozšíření.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-177">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="4bd9f-178">Uvnitř `HomeController`, můžete se vrátit *Index* zobrazení vaší *spravovat* zobrazení s relativní cestou:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-178">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="4bd9f-179">Podobně můžete určit aktuální adresář konkrétní řadič se ". /" předpona:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-179">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="4bd9f-180">[Částečná zobrazení](xref:mvc/views/partial) a [zobrazení součástí](xref:mvc/views/view-components) pomocí mechanismů zjišťování podobný (ale nejsou identické).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-180">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="4bd9f-181">Můžete přizpůsobit výchozí konvence pro způsob zobrazení se nachází v rámci aplikace s použitím vlastní [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-181">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="4bd9f-182">Zobrazení zjišťování spoléhá na hledání zobrazit soubory podle názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-182">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="4bd9f-183">Pokud podkladový systém souborů je velká a malá písmena, zobrazit názvy jsou pravděpodobně malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-183">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="4bd9f-184">Z důvodu kompatibility v operačních systémech rozlišovat velikost písmen mezi kontroleru a akce názvy a přidružené zobrazení složek a souborů.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-184">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="4bd9f-185">Pokud narazíte na chybu při práci se systémem souborů s rozlišením velkých nebyl nalezen soubor zobrazení, potvrzení, že malých a velkých písmen odpovídá mezi požadované zobrazení souboru a název souboru skutečné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-185">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="4bd9f-186">Dodržíte osvědčený postup uspořádání struktura souborů pro zobrazení tak, aby odrážely vztahy mezi kontrolerů, akce a zobrazení udržovatelnost a srozumitelnější.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-186">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="4bd9f-187">Předání dat pro zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-187">Passing data to views</span></span>

<span data-ttu-id="4bd9f-188">Předejte data do zobrazení pomocí několik přístupů:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-188">Pass data to views using several approaches:</span></span>

* <span data-ttu-id="4bd9f-189">Data se silnými typy: viewmodel</span><span class="sxs-lookup"><span data-stu-id="4bd9f-189">Strongly typed data: viewmodel</span></span>
* <span data-ttu-id="4bd9f-190">Slabě typovaná dat</span><span class="sxs-lookup"><span data-stu-id="4bd9f-190">Weakly typed data</span></span>
  * <span data-ttu-id="4bd9f-191">`ViewData` (`ViewDataAttribute`)</span><span class="sxs-lookup"><span data-stu-id="4bd9f-191">`ViewData` (`ViewDataAttribute`)</span></span>
  * `ViewBag`

### <a name="strongly-typed-data-viewmodel"></a><span data-ttu-id="4bd9f-192">Dat silného typu (viewmodel)</span><span class="sxs-lookup"><span data-stu-id="4bd9f-192">Strongly typed data (viewmodel)</span></span>

<span data-ttu-id="4bd9f-193">Se nejrobustnější zadává [modelu](xref:mvc/models/model-binding) typ v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-193">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="4bd9f-194">Tento model se často označuje jako *viewmodel*.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-194">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="4bd9f-195">Předejte instanci typu viewmodel do zobrazení z akce.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-195">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="4bd9f-196">Použití viewmodel k předávání dat k zobrazení umožňuje zobrazit výhod *silné* kontroly typu.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-196">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="4bd9f-197">*Silné typování* (nebo *silného typu*) znamená, že všechny proměnné a konstanty má typ, který explicitně definovány (například `string`, `int`, nebo `DateTime`).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-197">*Strong typing* (or *strongly typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="4bd9f-198">Platnost typy používané v zobrazení je zaškrtnuté políčko v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-198">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="4bd9f-199">[Visual Studio](https://www.visualstudio.com/vs/) a [Visual Studio Code](https://code.visualstudio.com/) seznam členů tříd se silnými typy použití funkce volána [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-199">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="4bd9f-200">Pokud chcete zobrazit vlastnosti viewmodel, zadejte název proměnné pro viewmodel následovaných tečkou (`.`).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-200">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="4bd9f-201">To vám umožňuje napsat kód rychleji s menším množstvím chyb.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-201">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="4bd9f-202">Zadat pomocí modelu `@model` směrnice.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-202">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="4bd9f-203">Použití modelu s `@Model`:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-203">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="4bd9f-204">K poskytnutí modelu pro zobrazení, předává kontroleru je jako parametr:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-204">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="4bd9f-205">Neexistují žádná omezení na typy modelů, které zadáte do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-205">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="4bd9f-206">Doporučujeme používat modely viewmodels prostý staré CLR objektů POCO s minimální nebo nulovou chování (metody) definované.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-206">We recommend using Plain Old CLR Object (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="4bd9f-207">Obvykle jsou tříd viewmodel buď uloženy v *modely* složku nebo samostatné *modely ViewModels* složku v kořenovém adresáři aplikace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-207">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="4bd9f-208">*Adresu* viewmodel použitých v příkladu výše je viewmodel POCO, uloží se do souboru s názvem *Address.cs*:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-208">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

<span data-ttu-id="4bd9f-209">Nic neumožňuje použití stejné třídy pro viewmodel typů a typů modelu vaší firmy.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-209">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="4bd9f-210">Použití samostatných modelů však umožňuje zobrazení se liší od obchodní logiku a data nezávisle na sobě přístupu k částem vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-210">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="4bd9f-211">Oddělení modely a modely viewmodels také nabízí výhody zabezpečení při použití modelů [vazby modelu](xref:mvc/models/model-binding) a [ověření](xref:mvc/models/validation) pro data odesílaná do aplikace uživatelem.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-211">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>

<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-viewdata-attribute-and-viewbag"></a><span data-ttu-id="4bd9f-212">Slabě typované data (ViewData, atribut ViewData a objekt ViewBag)</span><span class="sxs-lookup"><span data-stu-id="4bd9f-212">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>

<span data-ttu-id="4bd9f-213">`ViewBag` *není k dispozici v stránky Razor.*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-213">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4bd9f-214">Kromě zobrazení se silnými typy, zobrazení je k dispozici přístup k *slabě typované* (také nazývané *volně psaný*) shromažďování dat o.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-214">In addition to strongly typed views, views have access to a *weakly typed* (also called *loosely typed*) collection of data.</span></span> <span data-ttu-id="4bd9f-215">Na rozdíl od silné typy *slabé typy* (nebo *dojde ke snížení typy*) znamená, že je nemusíte deklarovat explicitně typu dat, které používáte.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-215">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="4bd9f-216">Shromažďování dat o slabě typované můžete použít pro předávání malých objemů dat do a z kontrolerů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-216">You can use the collection of weakly typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="4bd9f-217">Předávání dat mezi...</span><span class="sxs-lookup"><span data-stu-id="4bd9f-217">Passing data between a ...</span></span>                        | <span data-ttu-id="4bd9f-218">Příklad</span><span class="sxs-lookup"><span data-stu-id="4bd9f-218">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="4bd9f-219">Kontrolerem a zobrazením</span><span class="sxs-lookup"><span data-stu-id="4bd9f-219">Controller and a view</span></span>                             | <span data-ttu-id="4bd9f-220">Naplnění rozevíracího seznamu s daty.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-220">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="4bd9f-221">Zobrazení a [rozložení zobrazení](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="4bd9f-221">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="4bd9f-222">Nastavení  **\<title >** obsahu elementu v zobrazení rozložení ze zobrazení souboru.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-222">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="4bd9f-223">[Částečné zobrazení](xref:mvc/views/partial) a zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-223">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="4bd9f-224">Widget, který zobrazuje data založená na webové stránce, která uživatel si vyžádal.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-224">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="4bd9f-225">Tato kolekce může být odkazováno prostřednictvím buď `ViewData` nebo `ViewBag` vlastnosti kontrolerů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-225">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="4bd9f-226">`ViewData` Vlastnost je slovník slabě typované objekty.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-226">The `ViewData` property is a dictionary of weakly typed objects.</span></span> <span data-ttu-id="4bd9f-227">`ViewBag` Vlastnost představuje obálku kolem `ViewData` poskytující dynamické vlastnosti pro základní `ViewData` kolekce.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-227">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="4bd9f-228">`ViewData` a `ViewBag` jsou vyřešeny dynamicky za běhu.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-228">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="4bd9f-229">Protože nenabízejí kontrolu typu za kompilace, obě jsou obecně více náchylné než při použití viewmodel.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-229">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="4bd9f-230">Z tohoto důvodu někteří vývojáři dáváte přednost minimálně nebo vůbec `ViewData` a `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-230">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>

<a name="VD"></a>

<span data-ttu-id="4bd9f-231">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-231">**ViewData**</span></span>

<span data-ttu-id="4bd9f-232">`ViewData` je [objektu ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) přistupuje prostřednictvím objektu `string` klíče.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-232">`ViewData` is a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="4bd9f-233">Řetězcová data můžete ukládat a používat přímo bez nutnosti přetypování, ale musíte přetypovat jiné `ViewData` hodnot na konkrétní typy objektu při jejich extrakci.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-233">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="4bd9f-234">Můžete použít `ViewData` k předání dat z řadiče, zobrazeními a v zobrazeních, včetně [částečná zobrazení](xref:mvc/views/partial) a [rozložení](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-234">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="4bd9f-235">Tady je příklad, který nastavuje hodnoty pozdrav a adresy `ViewData` v akci:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-235">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="4bd9f-236">Práce s daty v zobrazení:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-236">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4bd9f-237">**Atribut viewData**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-237">**ViewData attribute**</span></span>

<span data-ttu-id="4bd9f-238">Další možností, které používá [objektu ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) je [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-238">Another approach that uses the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) is [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="4bd9f-239">Upravené vlastnosti v kontrolerech a modelech stránky Razor pomocí `[ViewData]` hodnoty uložené a načten ze slovníku.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-239">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the dictionary.</span></span>

<span data-ttu-id="4bd9f-240">V následujícím příkladu obsahuje kontroler Home `Title` vlastnost upravené pomocí `[ViewData]`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-240">In the following example, the Home controller contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="4bd9f-241">`About` Metody nastavuje název o zobrazení:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-241">The `About` method sets the title for the About view:</span></span>

```csharp
public class HomeController : Controller
{
    [ViewData]
    public string Title { get; set; }

    public IActionResult About()
    {
        Title = "About Us";
        ViewData["Message"] = "Your application description page.";

        return View();
    }
}
```

<span data-ttu-id="4bd9f-242">V zobrazení o přístup `Title` vlastnost jako vlastnost modelu:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-242">In the About view, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="4bd9f-243">Název je v rozložení pro čtení ze slovníku ViewData:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-243">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

<span data-ttu-id="4bd9f-244">**Objekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-244">**ViewBag**</span></span>

<span data-ttu-id="4bd9f-245">`ViewBag` *není k dispozici v stránky Razor.*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-245">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4bd9f-246">`ViewBag` je [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) poskytující dynamické přístup k objektům, které jsou uložené v `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-246">`ViewBag` is a [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="4bd9f-247">`ViewBag` může být vhodnější pro práci s, protože nevyžaduje přetypování.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-247">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="4bd9f-248">Následující příklad ukazuje, jak používat `ViewBag` s stejný výsledek jako při použití `ViewData` výše:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-248">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="4bd9f-249">**Použití slovníku ViewData a objekt ViewBag současně**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-249">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="4bd9f-250">`ViewBag` *není k dispozici v stránky Razor.*</span><span class="sxs-lookup"><span data-stu-id="4bd9f-250">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="4bd9f-251">Protože `ViewData` a `ViewBag` odkazovat na stejnou základní `ViewData` kolekce, je možné použít jak `ViewData` a `ViewBag` a kombinovat a párovat mezi nimi při čtení a zápisu hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-251">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="4bd9f-252">Sada s použitím názvu `ViewBag` a popis použití `ViewData` v horní části *About.cshtml* zobrazení:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-252">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="4bd9f-253">Čtení vlastností, ale reverse použití `ViewData` a `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-253">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="4bd9f-254">V *_Layout.cshtml* soubor, pomocí názvu získat `ViewData` a získat popis použití `ViewBag`:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-254">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="4bd9f-255">Mějte na paměti, že řetězce nevyžadují přetypování pro `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-255">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="4bd9f-256">Můžete použít `@ViewData["Title"]` bez přetypování.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-256">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="4bd9f-257">Použitím `ViewData` a `ViewBag` ve stejný čas funguje, jako kombinace a porovnávání čtení a zápis do vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-257">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="4bd9f-258">Vykreslení následující značky:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-258">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="4bd9f-259">**Souhrnné informace o rozdílech mezi ViewData a objekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-259">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="4bd9f-260">`ViewBag` není k dispozici v stránky Razor.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-260">`ViewBag` isn't available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="4bd9f-261">Je odvozen od [objektu ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), takže má slovníkové vlastnosti, které mohou být užitečné, například `ContainsKey`, `Add`, `Remove`, a `Clear`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-261">Derives from [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="4bd9f-262">Klíče ve slovníku jsou řetězce, proto je povolen prázdný znak.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-262">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="4bd9f-263">Příklad: `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="4bd9f-263">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="4bd9f-264">Jakýkoli typ jiný než `string` musíte přetypovat v zobrazení a použití `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-264">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="4bd9f-265">Je odvozen od [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), takže umožňuje vytváření dynamických vlastností pomocí zápisu s tečkou (`@ViewBag.SomeKey = <value or object>`), a není nutná žádná přetypování.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-265">Derives from [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="4bd9f-266">Syntaxe `ViewBag` umožňuje rychlejší pro přidání do kontrolerů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-266">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="4bd9f-267">Jednodušší kontrola hodnot null.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-267">Simpler to check for null values.</span></span> <span data-ttu-id="4bd9f-268">Příklad: `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="4bd9f-268">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="4bd9f-269">**Použití slovníku ViewData nebo objekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="4bd9f-269">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="4bd9f-270">Obě `ViewData` a `ViewBag` jsou rovnoměrně platný přístupy k předání malé množství dat mezi kontrolerů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-270">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="4bd9f-271">Volba používané podle předvoleb.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-271">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="4bd9f-272">Můžete kombinovat a párovat `ViewData` a `ViewBag` objekty, ale kód je jednodušší číst a spravovat s jedním z přístupů používány konzistentně.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-272">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="4bd9f-273">Oba přístupy jsou vyřešené dynamicky za běhu a proto náchylná k způsobující chyby za běhu.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-273">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="4bd9f-274">Některé vývojové týmy jim vyhnout.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-274">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="4bd9f-275">Dynamické zobrazení</span><span class="sxs-lookup"><span data-stu-id="4bd9f-275">Dynamic views</span></span>

<span data-ttu-id="4bd9f-276">Zobrazení, která není deklarovat modelu zadejte pomocí `@model` , ale dostatek instanci modelu předaný k nim (například `return View(Address);`) můžete odkazovat na instanci vlastnosti dynamicky:</span><span class="sxs-lookup"><span data-stu-id="4bd9f-276">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="4bd9f-277">Tato funkce nabízí flexibilitu, ale nenabízí ochrany kompilace ani IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-277">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="4bd9f-278">Pokud vlastnost neexistuje, webové stránky generování nezdaří za běhu.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-278">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="4bd9f-279">Další zobrazení funkcí</span><span class="sxs-lookup"><span data-stu-id="4bd9f-279">More view features</span></span>

<span data-ttu-id="4bd9f-280">[Pomocné rutiny značky](xref:mvc/views/tag-helpers/intro) umožňují snadno přidat chování na straně serveru k existující značky HTML.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-280">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="4bd9f-281">Použití pomocných rutin značek Polly nemusíte psát vlastní kód nebo pomocné rutiny v rámci zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-281">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="4bd9f-282">Pomocné rutiny značek se použijí jako atributy prvků HTML a jsou ignorovány ve editorů, které nelze zpracovat.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-282">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="4bd9f-283">To umožňuje upravit a vykreslení zobrazení kódu v různých nástrojů.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-283">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="4bd9f-284">Generování vlastní značky HTML lze nastavit pomocí mnoho integrovaných pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-284">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="4bd9f-285">Složitější logiku uživatelského rozhraní může být zpracována [komponenty zobrazení](xref:mvc/views/view-components).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-285">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="4bd9f-286">Zobrazení komponenty poskytují stejné SoC tohoto řadiče a nabídnout zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-286">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="4bd9f-287">Odstraňují potřebu akcemi a zobrazeními, které pracují s daty používá společné prvky uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4bd9f-287">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="4bd9f-288">Stejně jako mnoho dalších aspektů ASP.NET Core, zobrazení podporu [injektáž závislostí](xref:fundamentals/dependency-injection), umožní službám být [vloženy do zobrazení](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="4bd9f-288">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>
