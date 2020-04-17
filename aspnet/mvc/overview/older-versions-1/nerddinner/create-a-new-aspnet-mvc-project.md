---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Vytvoření nového projektu ASP.NET MVC | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 1 ukazuje, jak umístit základní strukturu aplikace NerdDinner na místě.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541478"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="633fa-103">Vytvoření nového projektu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="633fa-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="633fa-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="633fa-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="633fa-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="633fa-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="633fa-106">Toto je krok 1 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="633fa-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="633fa-107">Krok 1 ukazuje, jak umístit základní strukturu aplikace NerdDinner na místě.</span><span class="sxs-lookup"><span data-stu-id="633fa-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="633fa-108">Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="633fa-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="633fa-109">NerdDinner Krok 1:&gt;Soubor- Nový projekt</span><span class="sxs-lookup"><span data-stu-id="633fa-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="633fa-110">Začneme naše aplikace NerdDinner výběrem **file-new&gt;project** položky nabídky v rámci aplikace Visual Studio 2008 nebo zdarma Visual Web Developer 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="633fa-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="633fa-111">Tím se zobrazí dialogové okno Nový projekt.</span><span class="sxs-lookup"><span data-stu-id="633fa-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="633fa-112">Chcete-li vytvořit novou aplikaci ASP.NET MVC, vybereme uzel "Web" na levé straně dialogového okna a pak zvolíme šablonu projektu "ASP.NET MVC Web Application" vpravo:</span><span class="sxs-lookup"><span data-stu-id="633fa-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="633fa-113">*Důležité: Ujistěte se, že jste stáhli a nainstalovali ASP.NET MVC - jinak se nezobrazí v dialogovém okně Nový projekt. V2 Instalační služby [webové platformy Společnosti Microsoft](https://www.microsoft.com/web/downloads/platform.aspx) můžete použít, pokud jste jej ještě nenainstalovali&gt;(ASP.NET MVC je k dispozici v části "Rozhraní webové platformy a runtimes").*</span><span class="sxs-lookup"><span data-stu-id="633fa-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="633fa-114">Pojmenujeme nový projekt, který vytvoříme "NerdDinner" a poté jej vytvoříte kliknutím na tlačítko "ok".</span><span class="sxs-lookup"><span data-stu-id="633fa-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="633fa-115">Po kliknutí na tlačítko "ok" Visual Studio vyvolá další dialogové okno, které nás vyzve k volitelně vytvořit projekt testování částí pro novou aplikaci také.</span><span class="sxs-lookup"><span data-stu-id="633fa-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="633fa-116">Tento projekt testování částí nám umožňuje vytvářet automatizované testy, které ověřují funkčnost a chování naší aplikace (něco, co budeme pokrývat, jak to udělat později v tomto kurzu).</span><span class="sxs-lookup"><span data-stu-id="633fa-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="633fa-117">Rozbalovací seznam "Test Framework" ve výše uvedeném dialogovém okně je naplněn všemi dostupnými ASP.NET šablonprojektů projektu testování částí MVC nainstalovaných v počítači.</span><span class="sxs-lookup"><span data-stu-id="633fa-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="633fa-118">Verze lze stáhnout pro NUnit, MBUnit a XUnit.</span><span class="sxs-lookup"><span data-stu-id="633fa-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="633fa-119">Integrované visual studio testování jednotky rozhraní je také podporována.</span><span class="sxs-lookup"><span data-stu-id="633fa-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="633fa-120">*Poznámka: Visual Studio Unit Test Framework je k dispozici pouze s Visual Studio 2008 Professional a vyšší verze. Pokud používáte vs 2008 Standard Edition nebo Visual Web Developer 2008 Express, budete muset stáhnout a nainstalovat nunit, MBUnit nebo XUnit rozšíření pro ASP.NET MVC, aby se toto dialogové okno zobrazí. Dialogové okno se nezobrazí, pokud nejsou nainstalovány žádné testovací architektury.*</span><span class="sxs-lookup"><span data-stu-id="633fa-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="633fa-121">Použijeme výchozí název "NerdDinner.Tests" pro testovací projekt, který vytvoříme, a použijeme možnost rozhraní "Visual Studio Unit Test".</span><span class="sxs-lookup"><span data-stu-id="633fa-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="633fa-122">Po kliknutí na tlačítko "ok" Visual Studio vytvoří řešení pro nás se dvěma projekty v něm - jeden pro naši webovou aplikaci a jeden pro naše testování částí:</span><span class="sxs-lookup"><span data-stu-id="633fa-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="633fa-123">Zkoumání struktury adresáře NerdDinner</span><span class="sxs-lookup"><span data-stu-id="633fa-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="633fa-124">Když vytvoříte novou aplikaci ASP.NET MVC pomocí sady Visual Studio, automaticky přidá do projektu několik souborů a adresářů:</span><span class="sxs-lookup"><span data-stu-id="633fa-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="633fa-125">ASP.NET projekty MVC mají ve výchozím nastavení šest adresářů nejvyšší úrovně:</span><span class="sxs-lookup"><span data-stu-id="633fa-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="633fa-126">**Adresář**</span><span class="sxs-lookup"><span data-stu-id="633fa-126">**Directory**</span></span> | <span data-ttu-id="633fa-127">**Účel**</span><span class="sxs-lookup"><span data-stu-id="633fa-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="633fa-128">**/Kontrolory**</span><span class="sxs-lookup"><span data-stu-id="633fa-128">**/Controllers**</span></span> | <span data-ttu-id="633fa-129">Kde umístit Controller třídy, které zpracovávají požadavky URL</span><span class="sxs-lookup"><span data-stu-id="633fa-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="633fa-130">**/Modely**</span><span class="sxs-lookup"><span data-stu-id="633fa-130">**/Models**</span></span> | <span data-ttu-id="633fa-131">Kam umístit třídy, které představují a manipulovat s daty</span><span class="sxs-lookup"><span data-stu-id="633fa-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="633fa-132">**/Zobrazení**</span><span class="sxs-lookup"><span data-stu-id="633fa-132">**/Views**</span></span> | <span data-ttu-id="633fa-133">Kam umístit soubory šablon uživatelského počítače, které jsou zodpovědné za vykreslování výstupu</span><span class="sxs-lookup"><span data-stu-id="633fa-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="633fa-134">**/Skripty**</span><span class="sxs-lookup"><span data-stu-id="633fa-134">**/Scripts**</span></span> | <span data-ttu-id="633fa-135">Kam vložíte soubory a skripty knihovny JavaScriptu (.js)</span><span class="sxs-lookup"><span data-stu-id="633fa-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="633fa-136">**/Obsah**</span><span class="sxs-lookup"><span data-stu-id="633fa-136">**/Content**</span></span> | <span data-ttu-id="633fa-137">Kam vložíte CSS a obrazové soubory a další nedynamický/nejavascriptový obsah</span><span class="sxs-lookup"><span data-stu-id="633fa-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="633fa-138">**/Data\_aplikace**</span><span class="sxs-lookup"><span data-stu-id="633fa-138">**/App\_Data**</span></span> | <span data-ttu-id="633fa-139">Kde ukládáte datové soubory, které chcete číst/zapisovat.</span><span class="sxs-lookup"><span data-stu-id="633fa-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="633fa-140">ASP.NET MVC tuto strukturu nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="633fa-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="633fa-141">Ve skutečnosti vývojáři pracující na velkých aplikacích obvykle rozdělí aplikaci na příčku více projektů, aby byla lépe zvládnutelná (například: třídy datového modelu často přejdou do projektu samostatné knihovny tříd z webové aplikace).</span><span class="sxs-lookup"><span data-stu-id="633fa-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="633fa-142">Výchozí struktura projektu však poskytuje pěknou výchozí konvenci adresářů, kterou můžeme použít k udržení našich aplikací v čistotě.</span><span class="sxs-lookup"><span data-stu-id="633fa-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="633fa-143">Když rozbalíme adresář /Controllers, zjistíme, že Visual Studio přidalo do projektu ve výchozím nastavení dvě třídy řadiče – HomeController a AccountController:</span><span class="sxs-lookup"><span data-stu-id="633fa-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="633fa-144">Když rozbalíme adresář /Views, najdeme tři podadresáře – /Home, /Account a /Shared – a ve výchozím nastavení byly do projektu přidány také několik souborů šablon:</span><span class="sxs-lookup"><span data-stu-id="633fa-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="633fa-145">Když jsme se rozbalit / Obsah a / Skripty adresáře, najdeme Site.css soubor, který se používá k stylu všech HTML na webu, stejně jako JavaScript knihovny, které mohou povolit ASP.NET AJAX a jQuery podporu v rámci aplikace:</span><span class="sxs-lookup"><span data-stu-id="633fa-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="633fa-146">Když jsme se rozšířit NerdDinner.Tests projektu najdeme dvě třídy, které obsahují testy částí pro naše třídy kontroleru:</span><span class="sxs-lookup"><span data-stu-id="633fa-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="633fa-147">Tyto výchozí soubory přidané visual studio nám poskytují základní strukturu pro pracovní aplikaci - kompletní s domovskou stránkou, o stránce, přihlašovacími / odhlašovacími / registračními stránkami účtu a neošetřenou chybovou stránkou (všechny kabelové a pracující po vybalení z krabice).</span><span class="sxs-lookup"><span data-stu-id="633fa-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="633fa-148">Spuštění aplikace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="633fa-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="633fa-149">Projekt můžeme spustit výběrem **ladicího systému-&gt;Start Ladění** nebo **Ladění-&gt;Start bez ladění** položek nabídky:</span><span class="sxs-lookup"><span data-stu-id="633fa-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="633fa-150">Tím se spustí předdefinovaný ASP.NET webový server, který je dodáván s Visual Studio, a spustí te naši aplikaci:</span><span class="sxs-lookup"><span data-stu-id="633fa-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="633fa-151">Níže je domovská stránka pro náš nový projekt (URL: "/"), když běží:</span><span class="sxs-lookup"><span data-stu-id="633fa-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="633fa-152">Kliknutím na kartu "O aplikaci" se zobrazí ostránce (URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="633fa-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="633fa-153">Kliknutím na odkaz "Přihlásit se" vpravo nahoře nás přeneseme na přihlašovací stránku (URL: "/Account/LogOn")</span><span class="sxs-lookup"><span data-stu-id="633fa-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="633fa-154">Pokud nemáme přihlašovací účet, můžeme kliknout na odkaz registru (URL: "/Account/Register") a vytvořit si ho:</span><span class="sxs-lookup"><span data-stu-id="633fa-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="633fa-155">Kód pro implementaci výše uvedené funkce domů, o aplikaci a odhlášení / registrace byl přidán ve výchozím nastavení, když jsme vytvořili náš nový projekt.</span><span class="sxs-lookup"><span data-stu-id="633fa-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="633fa-156">Použijeme ji jako výchozí bod naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="633fa-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="633fa-157">Testování aplikace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="633fa-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="633fa-158">Pokud používáme Professional Edition nebo vyšší verzi sady Visual Studio 2008, můžeme použít integrovanou podporu testování částí IDE v rámci sady Visual Studio k testování projektu:</span><span class="sxs-lookup"><span data-stu-id="633fa-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="633fa-159">Výběrem jedné z výše uvedených možností se otevře podokno "Výsledky testů" v rámci integrovaného rozhraní IDE a poskytnete nám stav vyhovění/selhání v testech 27 jednotek zahrnutých v našem novém projektu, které pokrývají vestavěné funkce:</span><span class="sxs-lookup"><span data-stu-id="633fa-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="633fa-160">Později v tomto kurzu budeme hovořit více o automatizované testování a přidat další testy částí, které pokrývají funkce aplikace, které implementujeme.</span><span class="sxs-lookup"><span data-stu-id="633fa-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="633fa-161">Další krok</span><span class="sxs-lookup"><span data-stu-id="633fa-161">Next Step</span></span>

<span data-ttu-id="633fa-162">Nyní máme základní strukturu aplikací na místě.</span><span class="sxs-lookup"><span data-stu-id="633fa-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="633fa-163">Nyní [vytvoříme databázi pro ukládání dat našich aplikací](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="633fa-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="633fa-164">[Předchozí](introducing-the-nerddinner-tutorial.md)
> [další](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="633fa-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
