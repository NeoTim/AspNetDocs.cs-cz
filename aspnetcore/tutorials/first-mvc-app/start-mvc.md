---
title: Začínáme s ASP.NET Core MVC
author: rick-anderson
description: Zjistěte, jak začít pracovat s ASP.NET Core MVC.
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: c09c06f55c4179e9e2174f0063ab7387b7e4c31b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076435"
---
# <a name="get-started-with-aspnet-core-mvc"></a><span data-ttu-id="a9d36-103">Začínáme s ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="a9d36-103">Get started with ASP.NET Core MVC</span></span>

<span data-ttu-id="a9d36-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a9d36-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="a9d36-105">V tomto kurzu se naučíte se základy vytváření webovou aplikaci ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="a9d36-105">This tutorial teaches the basics of building an ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="a9d36-106">Aplikaci spravuje databáze filmů produktů.</span><span class="sxs-lookup"><span data-stu-id="a9d36-106">The app manages a database of movie titles.</span></span> <span data-ttu-id="a9d36-107">Získáte informace o následujících postupech:</span><span class="sxs-lookup"><span data-stu-id="a9d36-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9d36-108">Vytvoření webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="a9d36-108">Create a web app.</span></span>
> * <span data-ttu-id="a9d36-109">Přidat a generování uživatelského rozhraní modelu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-109">Add and scaffold a model.</span></span>
> * <span data-ttu-id="a9d36-110">Práce s databází.</span><span class="sxs-lookup"><span data-stu-id="a9d36-110">Work with a database.</span></span>
> * <span data-ttu-id="a9d36-111">Přidáte vyhledávání a ověřování.</span><span class="sxs-lookup"><span data-stu-id="a9d36-111">Add search and validation.</span></span>

<span data-ttu-id="a9d36-112">Na konci budete mít aplikaci, která můžete spravovat a zobrazit data o filmech.</span><span class="sxs-lookup"><span data-stu-id="a9d36-112">At the end, you have an app that can manage and display movie data.</span></span>

[!INCLUDE[](~/includes/mvc-intro/download.md)]

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="a9d36-113">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="a9d36-113">Create a web app</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a9d36-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9d36-114">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="a9d36-115">Ze sady Visual Studio, vyberte **soubor > Nový > projekt**.</span><span class="sxs-lookup"><span data-stu-id="a9d36-115">From Visual Studio, select  **File > New > Project**.</span></span>

![Soubor > Nový > Projekt](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="a9d36-117">Dokončení **nový projekt** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="a9d36-117">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="a9d36-118">V levém podokně vyberte **.NET Core**</span><span class="sxs-lookup"><span data-stu-id="a9d36-118">In the left pane, select **.NET Core**</span></span>
* <span data-ttu-id="a9d36-119">V prostředním podokně vyberte **webová aplikace ASP.NET Core (.NET Core)**</span><span class="sxs-lookup"><span data-stu-id="a9d36-119">In the center pane, select **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="a9d36-120">Pojmenujte projekt "MvcMovie" (je třeba název projektu "MvcMovie", takže při kopírování kódu bude odpovídat oboru názvů.)</span><span class="sxs-lookup"><span data-stu-id="a9d36-120">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="a9d36-121">Vyberte **OK**</span><span class="sxs-lookup"><span data-stu-id="a9d36-121">select **OK**</span></span>

![<span data-ttu-id="a9d36-122">Dialogové okno Nový projekt, .net core v levém podokně, web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a9d36-122">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="a9d36-123">Dokončení **nové základní webové aplikace ASP.NET (.NET Core) – MvcMovie** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="a9d36-123">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="a9d36-124">V poli verze selektoru rozevíracího seznamu vyberte **2.2 technologie ASP.NET Core**</span><span class="sxs-lookup"><span data-stu-id="a9d36-124">In the version selector drop-down box select **ASP.NET Core 2.2**</span></span>
* <span data-ttu-id="a9d36-125">Vyberte **webová aplikace (Model-View-Controller)**</span><span class="sxs-lookup"><span data-stu-id="a9d36-125">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="a9d36-126">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9d36-126">select **OK**.</span></span>

![<span data-ttu-id="a9d36-127">Dialogové okno Nový projekt, .net core v levém podokně, web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a9d36-127">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="a9d36-128">Visual Studio používá výchozí šablonu pro projekt MVC, který jste právě vytvořili.</span><span class="sxs-lookup"><span data-stu-id="a9d36-128">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="a9d36-129">Zadáním názvu projektu a výběr několika možností Teď máte funkční aplikaci.</span><span class="sxs-lookup"><span data-stu-id="a9d36-129">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="a9d36-130">Toto je základní počáteční projekt a je dobrým začátkem.</span><span class="sxs-lookup"><span data-stu-id="a9d36-130">This is a basic starter project, and it's a good place to start.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a9d36-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a9d36-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="a9d36-132">Kurz předpokládá familarity s VS Code.</span><span class="sxs-lookup"><span data-stu-id="a9d36-132">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="a9d36-133">Zobrazit [Začínáme s VS Code](https://code.visualstudio.com/docs) a [nápovědy Visual Studio Code](#visual-studio-code-help) Další informace.</span><span class="sxs-lookup"><span data-stu-id="a9d36-133">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span>

* <span data-ttu-id="a9d36-134">Otevřít [integrovaný terminál](https://code.visualstudio.com/docs/editor/integrated-terminal).</span><span class="sxs-lookup"><span data-stu-id="a9d36-134">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="a9d36-135">Změňte adresář (`cd`) do složky, která bude obsahovat projektu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-135">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="a9d36-136">Spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="a9d36-136">Run the following command:</span></span>

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * <span data-ttu-id="a9d36-137">Zobrazí se dialogové okno s **'MvcMovie' chybí požadované prostředky pro sestavení a ladění. Přidat?**</span><span class="sxs-lookup"><span data-stu-id="a9d36-137">A dialog box appears with **Required assets to build and debug are missing from 'MvcMovie'. Add them?**</span></span>  <span data-ttu-id="a9d36-138">Vyberte **Ano**</span><span class="sxs-lookup"><span data-stu-id="a9d36-138">Select **Yes**</span></span>

  * <span data-ttu-id="a9d36-139">`dotnet new mvc -o MvcMovie`: vytvoří nový projekt ASP.NET Core MVC v *MvcMovie* složky.</span><span class="sxs-lookup"><span data-stu-id="a9d36-139">`dotnet new mvc -o MvcMovie`: creates a new ASP.NET Core MVC project in the *MvcMovie* folder.</span></span>
  * <span data-ttu-id="a9d36-140">`code -r MvcMovie`: Načtení *MvcMovie.csproj* soubor projektu ve Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a9d36-140">`code -r MvcMovie`: Loads the *MvcMovie.csproj* project file in Visual Studio Code.</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a9d36-141">Visual Studio pro Mac</span><span class="sxs-lookup"><span data-stu-id="a9d36-141">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="a9d36-142">Vyberte **souboru** > **nové řešení**.</span><span class="sxs-lookup"><span data-stu-id="a9d36-142">Select **File** > **New Solution**.</span></span>

  ![macOS nové řešení](~/tutorials/first-web-api-mac/_static/sln.png)

* <span data-ttu-id="a9d36-144">Vyberte **aplikace .NET Core** > **ASP.NET Core** > **webové aplikace ASP.NET Core (MVC)** > **Další**.</span><span class="sxs-lookup"><span data-stu-id="a9d36-144">Select **.NET Core App** > **ASP.NET Core** > **ASP.NET Core Web App (MVC)** > **Next**.</span></span>

  ![macOS dialogové okno nového projektu](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* <span data-ttu-id="a9d36-146">V **nakonfigurovat nové technologie ASP.NET Core webové rozhraní API** dialogového okna, přijměte výchozí nastavení **Cílová architektura** z \**.NET Core 2.2*.</span><span class="sxs-lookup"><span data-stu-id="a9d36-146">In the **Configure your new ASP.NET Core Web API** dialog, accept the default **Target Framework** of \**.NET Core 2.2*.</span></span>

* <span data-ttu-id="a9d36-147">Pojmenujte projekt **MvcMovie**a pak vyberte **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="a9d36-147">Name the project **MvcMovie**, and then select **Create**.</span></span>

---  
<!-- End of VS tabs -->

### <a name="run-the-app"></a><span data-ttu-id="a9d36-148">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="a9d36-148">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a9d36-149">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9d36-149">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="a9d36-150">Vyberte **Ctrl-F5** ke spuštění aplikace v režimu bez ladění.</span><span class="sxs-lookup"><span data-stu-id="a9d36-150">Select **Ctrl-F5** to run the app in non-debug mode.</span></span>

[!INCLUDE[](~/includes/trustCertVS.md)]

* <span data-ttu-id="a9d36-151">Visual Studio spustí [služby IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) a spustí aplikaci.</span><span class="sxs-lookup"><span data-stu-id="a9d36-151">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="a9d36-152">Všimněte si, že do adresního řádku ukazuje `localhost:port#` a nemít něco podobného `example.com`.</span><span class="sxs-lookup"><span data-stu-id="a9d36-152">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="a9d36-153">Důvodem je, že `localhost` je standardní název hostitele místního počítače.</span><span class="sxs-lookup"><span data-stu-id="a9d36-153">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="a9d36-154">Když Visual Studio vytvoří webový projekt, náhodný port se používá pro webový server.</span><span class="sxs-lookup"><span data-stu-id="a9d36-154">When Visual Studio creates a web project, a random port is used for the web server.</span></span>
* <span data-ttu-id="a9d36-155">Spuštění aplikace pomocí kombinace kláves Ctrl + F5 (bez ladění režim) umožňuje provádět změny kódu, uložte soubor, aktualizujte prohlížeč a zobrazení změn kódu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-155">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="a9d36-156">Mnoho vývojářů dávají přednost používání režimu bez ladění k rychlému spusťte aplikaci a podívejte se na změny.</span><span class="sxs-lookup"><span data-stu-id="a9d36-156">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="a9d36-157">Spustíte ji v ladění nebo v režimu bez ladění z **ladění** položky nabídky:</span><span class="sxs-lookup"><span data-stu-id="a9d36-157">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

  ![Ladění nabídky](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="a9d36-159">Můžete ladit aplikaci tak, že vyberete **služby IIS Express** tlačítko</span><span class="sxs-lookup"><span data-stu-id="a9d36-159">You can debug the app by selecting the **IIS Express** button</span></span>

  ![Služba IIS Express](start-mvc/_static/iis_express.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a9d36-161">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a9d36-161">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="a9d36-162">Stisknutím kláves Ctrl + F5 ke spuštění bez ladicího programu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-162">Press Ctrl+F5 to run without the debugger.</span></span>

[!INCLUDE[](~/includes/trustCertVSC.md)]

  <span data-ttu-id="a9d36-163">Visual Studio Code spuštění spustí [Kestrel](xref:fundamentals/servers/kestrel), spustí se prohlížeč a přejde na `https://localhost:5001`.</span><span class="sxs-lookup"><span data-stu-id="a9d36-163">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `https://localhost:5001`.</span></span> <span data-ttu-id="a9d36-164">Zobrazí se panel Adresa `localhost:port:5001` a nemít něco podobného `example.com`.</span><span class="sxs-lookup"><span data-stu-id="a9d36-164">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="a9d36-165">Důvodem je, že `localhost` je standardní název hostitele místního počítače.</span><span class="sxs-lookup"><span data-stu-id="a9d36-165">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="a9d36-166">Localhost slouží pouze webové požadavky z místního počítače.</span><span class="sxs-lookup"><span data-stu-id="a9d36-166">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="a9d36-167">Spuštění aplikace pomocí kombinace kláves Ctrl + F5 (bez ladění režim) umožňuje provádět změny kódu, uložte soubor, aktualizujte prohlížeč a zobrazení změn kódu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-167">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="a9d36-168">Mnoho vývojářů dávají přednost používání režimu bez ladění a aktualizujte stránku, podívejte se na změny.</span><span class="sxs-lookup"><span data-stu-id="a9d36-168">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a9d36-169">Visual Studio pro Mac</span><span class="sxs-lookup"><span data-stu-id="a9d36-169">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="a9d36-170">Vyberte **spustit** > **spustit bez ladění** aplikaci spustit.</span><span class="sxs-lookup"><span data-stu-id="a9d36-170">Select **Run** > **Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="a9d36-171">Visual Studio pro Mac spustí [Kestrel](xref:fundamentals/servers/index#kestrel) serveru, spustí se prohlížeč a přejde na `http://localhost:port`, kde *port* je číslo portu náhodně vybrané.</span><span class="sxs-lookup"><span data-stu-id="a9d36-171">Visual Studio for Mac starts [Kestrel](xref:fundamentals/servers/index#kestrel) server, launches a browser, and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span>

[!INCLUDE[](~/includes/trustCertMac.md)]

* <span data-ttu-id="a9d36-172">Zobrazí se panel Adresa `localhost:port#` a nemít něco podobného `example.com`.</span><span class="sxs-lookup"><span data-stu-id="a9d36-172">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="a9d36-173">Důvodem je, že `localhost` je standardní název hostitele místního počítače.</span><span class="sxs-lookup"><span data-stu-id="a9d36-173">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="a9d36-174">Když Visual Studio vytvoří webový projekt, náhodný port se používá pro webový server.</span><span class="sxs-lookup"><span data-stu-id="a9d36-174">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="a9d36-175">Při spuštění aplikace se zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="a9d36-175">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="a9d36-176">Spustíte ji v ladění nebo v režimu bez ladění z **spustit** nabídky.</span><span class="sxs-lookup"><span data-stu-id="a9d36-176">You can launch the app in debug or non-debug mode from the **Run** menu.</span></span>

------

* <span data-ttu-id="a9d36-177">Vyberte **přijmout** souhlas sledování.</span><span class="sxs-lookup"><span data-stu-id="a9d36-177">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="a9d36-178">Tato aplikace nesleduje osobní údaje.</span><span class="sxs-lookup"><span data-stu-id="a9d36-178">This app doesn't track personal information.</span></span> <span data-ttu-id="a9d36-179">Tento kód vygenerovanou šablonu obsahuje prostředky, které vám pomohou splnit [obecného Regulation (GDPR)](xref:security/gdpr).</span><span class="sxs-lookup"><span data-stu-id="a9d36-179">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![Index nebo Domovská stránka](start-mvc/_static/privacy.png)

  <span data-ttu-id="a9d36-181">Následující obrázek znázorňuje aplikaci po přijetí sledování:</span><span class="sxs-lookup"><span data-stu-id="a9d36-181">The following image shows the app after accepting tracking:</span></span>

  ![Index nebo Domovská stránka](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

<span data-ttu-id="a9d36-183">V další části tohoto kurzu přečtěte si o MVC a začít psát kód.</span><span class="sxs-lookup"><span data-stu-id="a9d36-183">In the next part of this tutorial, you learn about MVC and start writing some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a9d36-184">Next</span><span class="sxs-lookup"><span data-stu-id="a9d36-184">Next</span></span>](adding-controller.md)  
