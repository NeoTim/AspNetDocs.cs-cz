---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: Začínáme se specifikací OWIN a Katana | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 5b5ecfcc7561e3e7bc13e1c8819a548e73ae1ab3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408092"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="4b2ee-102">Začínáme se specifikací OWIN a sadou Katana</span><span class="sxs-lookup"><span data-stu-id="4b2ee-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="4b2ee-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4b2ee-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4b2ee-104">[Otevřete Web Interface pro .NET (OWIN)](http://owin.org/) definuje abstrakce mezi .NET webové servery a webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="4b2ee-105">Oddělením webový server z aplikace OWIN usnadňuje vytvoření middleware pro vývoj webových aplikací .NET.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="4b2ee-106">Navíc OWIN usnadňuje port webové aplikace do jiných hostitelů&#8212;například samoobslužné hostování ve službě Windows nebo jiný proces.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="4b2ee-107">OWIN je specifikace vlastnictví komunity, ne implementace.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="4b2ee-108">Projektu Katana je sada součástí OWIN open source vyvinutý microsoftem.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="4b2ee-109">Obecný přehled o OWIN a Katana, naleznete v tématu [Přehled projektu Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="4b2ee-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="4b2ee-110">V tomto článku můžu se rovnou do kódu, abyste mohli začít.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="4b2ee-111">Tento kurz používá [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), ale můžete také použít Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="4b2ee-112">Některé z kroků se liší v sadě Visual Studio 2012, který jsem mějte na paměti následující.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="4b2ee-113">Hostování specifikace OWIN ve službě IIS</span><span class="sxs-lookup"><span data-stu-id="4b2ee-113">Host OWIN in IIS</span></span>

<span data-ttu-id="4b2ee-114">V této části budeme hostovat zde OWIN ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="4b2ee-115">Tato možnost poskytuje flexibilitu a skládání kanál OWIN spolu s sadě až po zralé funkcí služby IIS.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="4b2ee-116">Použití této možnosti spuštění aplikace OWIN v kanálu požadavku ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="4b2ee-117">Nejprve vytvořte nový projekt webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="4b2ee-118">(V sadě Visual Studio 2012, použijte typ projektu prázdná webová aplikace ASP.NET.)</span><span class="sxs-lookup"><span data-stu-id="4b2ee-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="4b2ee-119">V **nový projekt ASP.NET** dialogového okna, vyberte **prázdný** šablony.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="4b2ee-120">Přidání balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="4b2ee-120">Add NuGet Packages</span></span>

<span data-ttu-id="4b2ee-121">Dále přidejte požadované balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="4b2ee-122">Z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4b2ee-123">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="4b2ee-124">Přidejte třídu pro spuštění</span><span class="sxs-lookup"><span data-stu-id="4b2ee-124">Add a Startup Class</span></span>

<span data-ttu-id="4b2ee-125">Dále přidejte třídy pro spuštění OWIN.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="4b2ee-126">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **přidat**a pak vyberte **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="4b2ee-127">V **přidat novou položku** dialogového okna, vyberte **třída Owin Startup**.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="4b2ee-128">Další informace o konfiguraci třída při spuštění najdete v tématu [rozpoznání spouštěcí třídy OWIN](owin-startup-class-detection.md).</span><span class="sxs-lookup"><span data-stu-id="4b2ee-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="4b2ee-129">Přidejte následující kód, který `Startup1.Configuration` metody:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="4b2ee-130">Tento kód přidá do kanálu OWIN implementovány jako funkce, která přijímá jednoduché část middleware **Microsoft.Owin.IOwinContext** instance.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="4b2ee-131">Když server přijme požadavek HTTP, vyvolá se v kanálu OWIN middleware.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="4b2ee-132">Middleware nastaví typ obsahu pro odpověď a zapíše text odpovědi.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="4b2ee-133">Šablona třídy OWIN Startup je k dispozici v sadě Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="4b2ee-134">Pokud používáte sadu Visual Studio 2012, stačí přidat novou prázdnou třídu s názvem `Startup1`a vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="4b2ee-135">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4b2ee-135">Run the Application</span></span>

<span data-ttu-id="4b2ee-136">Stisknutím klávesy F5 spusťte ladění.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="4b2ee-137">Visual Studio se otevře okno prohlížeče a `http://localhost:*port*/`.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="4b2ee-138">Na stránce by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="4b2ee-139">Hostování na vlastním serveru OWIN v konzolové aplikaci</span><span class="sxs-lookup"><span data-stu-id="4b2ee-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="4b2ee-140">Je snadno převést tuto aplikaci ze služby IIS hostování až po samoobslužné hostování ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="4b2ee-141">S hostování IIS IIS funguje jako HTTP server a jako proces, který je hostitelem služby.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="4b2ee-142">Hostování na vlastním vaše aplikace vytvoří procesu a používá **HttpListener** třídu jako HTTP server.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="4b2ee-143">V sadě Visual Studio vytvořte novou konzolovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="4b2ee-144">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="4b2ee-145">Přidat `Startup1` třídy do projektu z části 1 tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="4b2ee-146">Není nutné upravovat této třídy.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-146">You don't need to modify this class.</span></span>

<span data-ttu-id="4b2ee-147">Implementace aplikace `Main` metodu následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="4b2ee-148">Když spustíte aplikaci konzoly, spustí se server naslouchá na `http://localhost:9000`.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="4b2ee-149">Když přejdete na tuto adresu ve webovém prohlížeči, se zobrazí stránka "Hello world".</span><span class="sxs-lookup"><span data-stu-id="4b2ee-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="4b2ee-150">Přidat OWIN diagnostiky</span><span class="sxs-lookup"><span data-stu-id="4b2ee-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="4b2ee-151">Balíček Microsoft.Owin.Diagnostics obsahuje middleware, který zachytává neošetřené výjimky a zobrazí stránku HTML s podrobnosti o chybě.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="4b2ee-152">Podobně jako chybová stránka technologie ASP.NET, který se někdy označuje jako funkce v této stránky "[žlutý obrazovky smrti](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span><span class="sxs-lookup"><span data-stu-id="4b2ee-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="4b2ee-153">Podobně jako YSOD chybová stránka Katana je užitečné při vývoji, ale je dobrým zvykem zakázat v provozním režimu.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="4b2ee-154">K instalaci balíčku diagnostiky ve vašem projektu, zadejte následující příkaz v okně konzoly Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="4b2ee-155">Změnit kód ve vašich `Startup1.Configuration` metodu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4b2ee-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="4b2ee-156">Teď pomocí kombinace kláves CTRL + F5 spusťte aplikaci bez ladění, tak, aby Visual Studio nebudou porušovat na výjimku.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="4b2ee-157">Aplikace se chová stejně jako dříve, dokud přejdete na `http://localhost/fail`, kdy aplikace vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="4b2ee-158">Middleware chybové stránky, se zachytit výjimku a zobrazí stránku HTML s informacemi o chybě.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="4b2ee-159">Můžete kliknout na karty se můžete podívat zásobníku, řetězec dotazu, soubory cookie, hlavička požadavku a proměnných prostředí OWIN.</span><span class="sxs-lookup"><span data-stu-id="4b2ee-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="4b2ee-160">Další kroky</span><span class="sxs-lookup"><span data-stu-id="4b2ee-160">Next Steps</span></span>

- [<span data-ttu-id="4b2ee-161">Rozpoznání spouštěcí třídy OWIN</span><span class="sxs-lookup"><span data-stu-id="4b2ee-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="4b2ee-162">Použití rozhraní OWIN k samoobslužnému hostování webového rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4b2ee-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="4b2ee-163">Použití rozhraní OWIN k samoobslužnému hostování SignalR</span><span class="sxs-lookup"><span data-stu-id="4b2ee-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
