---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET a webové nástroje pro poznámky k verzi sady Visual Studio 2013 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET a webových nástrojů pro Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543493"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="43a18-103">ASP.NET a webové nástroje pro Visual Studio 2013 – poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="43a18-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="43a18-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="43a18-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="43a18-105">Tento dokument popisuje vydání ASP.NET a webových nástrojů pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43a18-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="43a18-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="43a18-106">Contents</span></span>

- [<span data-ttu-id="43a18-107">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="43a18-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="43a18-108">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="43a18-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="43a18-109">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="43a18-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="43a18-110">Nové funkce v ASP.NET a webových nástrojích pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="43a18-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="43a18-111">Jedna ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="43a18-112">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="43a18-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="43a18-113">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="43a18-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="43a18-114">Browser Link</span><span class="sxs-lookup"><span data-stu-id="43a18-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="43a18-115">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43a18-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="43a18-116">Podpora webových aplikací služby Azure App Service ve Visual Studiu</span><span class="sxs-lookup"><span data-stu-id="43a18-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="43a18-117">Vylepšení publikování webu</span><span class="sxs-lookup"><span data-stu-id="43a18-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="43a18-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="43a18-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="43a18-119">ASP.NET – webové formuláře</span><span class="sxs-lookup"><span data-stu-id="43a18-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="43a18-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="43a18-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="43a18-121">Rozhraní API pro ASP.NET Web 2</span><span class="sxs-lookup"><span data-stu-id="43a18-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="43a18-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="43a18-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="43a18-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="43a18-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="43a18-124">Součásti Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="43a18-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="43a18-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="43a18-126">ASP.NET Břitva 3</span><span class="sxs-lookup"><span data-stu-id="43a18-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="43a18-127">ASP.NET pozastavení aplikace</span><span class="sxs-lookup"><span data-stu-id="43a18-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="43a18-128">Známé problémy a nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="43a18-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="43a18-129">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="43a18-129">Installation Notes</span></span>

<span data-ttu-id="43a18-130">ASP.NET a webových nástrojů pro Visual Studio 2013 jsou dodávány v hlavním instalačním programu a lze je stáhnout [zde](https://www.asp.net/downloads).</span><span class="sxs-lookup"><span data-stu-id="43a18-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="43a18-131">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="43a18-131">Documentation</span></span>

<span data-ttu-id="43a18-132">Výukové programy a další informace o ASP.NET a webových nástrojích pro visual studio 2013 jsou k dispozici na [webu ASP.NET](https://www.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="43a18-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="43a18-133">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="43a18-133">Software Requirements</span></span>

<span data-ttu-id="43a18-134">ASP.NET a webových nástrojů vyžaduje Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43a18-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="43a18-135">Nové funkce v ASP.NET a webových nástrojích pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="43a18-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="43a18-136">Následující části popisují funkce, které byly zavedeny ve verzi.</span><span class="sxs-lookup"><span data-stu-id="43a18-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="43a18-137">Jedna ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-137">One ASP.NET</span></span>

<span data-ttu-id="43a18-138">S vydáním Visual Studia 2013 jsme udělali krok ke sjednocení prostředí s používáním ASP.NET technologií, takže můžete snadno kombinovat ty, které chcete.</span><span class="sxs-lookup"><span data-stu-id="43a18-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="43a18-139">Můžete například zahájit projekt pomocí mvc a snadno přidat stránky webových formulářů do projektu později nebo ve windows web oválná síť API v projektu webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="43a18-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="43a18-140">Jedním ASP.NET je především o tom, aby bylo pro vás jako vývojáře snazší dělat věci, které máte rádi v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="43a18-141">Bez ohledu na to, jakou technologii si vyberete, můžete mít jistotu, že stavíte na důvěryhodném základním rámci One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="43a18-142">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="43a18-142">New Web Project Experience</span></span>

<span data-ttu-id="43a18-143">Vylepšili jsme možnosti vytváření nových webových projektů v sadě Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43a18-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="43a18-144">V dialogovém **okně Nový ASP.NET webový projekt** můžete vybrat požadovaný typ projektu, nakonfigurovat libovolnou kombinaci technologií (webové formuláře, MVC, webové rozhraní API), nakonfigurovat možnosti ověřování a přidat projekt testování částí.</span><span class="sxs-lookup"><span data-stu-id="43a18-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![Nový projekt ASP.NET](release-notes/_static/image1.png)

<span data-ttu-id="43a18-146">Nové dialogové okno umožňuje změnit výchozí možnosti ověřování pro mnoho šablon.</span><span class="sxs-lookup"><span data-stu-id="43a18-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="43a18-147">Pokud například vytvoříte projekt ASP.NET webových formulářů, můžete vybrat některou z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="43a18-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="43a18-148">Bez ověřování</span><span class="sxs-lookup"><span data-stu-id="43a18-148">No Authentication</span></span>
- <span data-ttu-id="43a18-149">Individuální uživatelské účty (ASP.NET členství nebo přihlášení poskytovatele mno žití)</span><span class="sxs-lookup"><span data-stu-id="43a18-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="43a18-150">Organizační účty (Služba Active Directory v internetové aplikaci)</span><span class="sxs-lookup"><span data-stu-id="43a18-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="43a18-151">Ověřování systému Windows (služba Active Directory v intranetové aplikaci)</span><span class="sxs-lookup"><span data-stu-id="43a18-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![Možnosti ověřování](release-notes/_static/image2.png)

<span data-ttu-id="43a18-153">Další informace o novém procesu vytváření webových projektů naleznete [v tématu Vytváření ASP.NET webových projektů v sadě Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="43a18-154">Další informace o nových možnostech ověřování naleznete [v tématu ASP.NET identity](#TOC8) dále v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="43a18-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="43a18-155">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="43a18-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="43a18-156">ASP.NET generování uživatelského rozhraní je rozhraní pro generování kódu pro ASP.NET webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="43a18-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="43a18-157">Usnadňuje přidání často používaný kód do projektu, který spolupracuje s datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="43a18-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="43a18-158">V předchozích verzích sady Visual Studio bylo lešení omezeno na ASP.NET projekty MVC.</span><span class="sxs-lookup"><span data-stu-id="43a18-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="43a18-159">V sadě Visual Studio 2013 teď můžete používat přisychávací období pro všechny ASP.NET projektu, včetně webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="43a18-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="43a18-160">Visual Studio 2013 aktuálně nepodporuje generování stránek pro projekt webových formulářů, ale stále můžete použít generování uživatelského formuláře s webovými formuláři přidáním závislostí MVC do projektu.</span><span class="sxs-lookup"><span data-stu-id="43a18-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="43a18-161">Podpora generování stránek pro webové formuláře bude přidána v budoucí aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="43a18-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="43a18-162">Při použití uživatelského přilechrápění zajišťujeme, že jsou v projektu nainstalovány všechny požadované závislosti.</span><span class="sxs-lookup"><span data-stu-id="43a18-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="43a18-163">Pokud například začnete s projektem ASP.NET webových formulářů a potom pomocí uživatelského rozhraní přidáte řadič webového rozhraní API, budou do projektu automaticky přidány požadované balíčky nuget a odkazy.</span><span class="sxs-lookup"><span data-stu-id="43a18-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="43a18-164">Chcete-li přidat uživatelské rozhraní MVC do projektu webových formulářů, přidejte **novou položku scaffolded a** v dialogovém okně vyberte **závislosti MVC 5.**</span><span class="sxs-lookup"><span data-stu-id="43a18-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="43a18-165">Existují dvě možnosti pro lešení MVC; Minimální a plná.</span><span class="sxs-lookup"><span data-stu-id="43a18-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="43a18-166">Pokud vyberete Minimální, do projektu se přidají pouze balíčky NuGet a odkazy pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="43a18-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="43a18-167">Pokud vyberete možnost Úplné, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="43a18-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="43a18-168">Podpora asynchronních řadičů lešení používá nové asynchronní funkce z entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="43a18-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="43a18-169">Další informace a kurzy naleznete [v tématu ASP.NET Přehled lešení](aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="43a18-170">Odkaz na prohlížeč – kanál SignalR mezi prohlížečem a visual studio</span><span class="sxs-lookup"><span data-stu-id="43a18-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="43a18-171">Nová funkce [Odkaz prohlížeče](using-browser-link.md) umožňuje připojit více prohlížečů k sadě Visual Studio a aktualizovat je všem klepnutím na tlačítko na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="43a18-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="43a18-172">K vývojovému webu můžete připojit více prohlížečů, včetně mobilních emulátorů, a kliknutím na aktualizovat aktualizovat všechny prohlížeče najednou.</span><span class="sxs-lookup"><span data-stu-id="43a18-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="43a18-173">Odkaz prohlížeče také zveřejňuje rozhraní API, které vývojářům umožňuje psát rozšíření odkazu prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="43a18-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="43a18-174">Povolením vývojářům využít rozhraní API odkazu prohlížeče, je možné vytvořit velmi pokročilé scénáře, které překračuje hranice mezi Visual Studio a libovolný prohlížeč, který je připojen.</span><span class="sxs-lookup"><span data-stu-id="43a18-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="43a18-175">Web Essentials využívá rozhraní API k vytvoření integrovaného prostředí mezi aplikací Visual Studio a vývojářskými nástroji prohlížeče, vzdálenými mobilními emulátory a mnoha dalšími.</span><span class="sxs-lookup"><span data-stu-id="43a18-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="43a18-176">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43a18-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="43a18-177">Visual Studio 2013 obsahuje nový editor HTML pro soubory Razor a soubory HTML ve webových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="43a18-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="43a18-178">Nový editor HTML poskytuje jedno jednotné schéma založené na HTML5.</span><span class="sxs-lookup"><span data-stu-id="43a18-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="43a18-179">Má automatické dokončení ortézy, jQuery UI a AngularJS atribut IntelliSense, atribut IntelliSense Seskupení, ID a název třídy Intellisense a další vylepšení, včetně lepšího výkonu, formátování a SmartTags.</span><span class="sxs-lookup"><span data-stu-id="43a18-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="43a18-180">Následující snímek obrazovky ukazuje použití bootstrap atribut IntelliSense v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="43a18-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![Intellisense v editoru HTML](release-notes/_static/image4.png)

<span data-ttu-id="43a18-182">Visual Studio 2013 také přichází s vestavěnými editory CoffeeScript a LESS.</span><span class="sxs-lookup"><span data-stu-id="43a18-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="43a18-183">Méně editor je dodáván se všemi skvělými funkcemi z editoru CSS a má specifický Intellisense pro proměnné a mixiny ve všech dokumentech LESS v řetězci. @import</span><span class="sxs-lookup"><span data-stu-id="43a18-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="43a18-184">Podpora webových aplikací služby Azure App Service ve Visual Studiu</span><span class="sxs-lookup"><span data-stu-id="43a18-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="43a18-185">Ve Visual Studiu 2013 s sadou Azure SDK pro .NET 2.2 můžete pomocí **Průzkumníka serveru** pracovat přímo se vzdálenými webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="43a18-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="43a18-186">Můžete se přihlásit ke svému účtu Azure, vytvářet nové webové aplikace, konfigurovat aplikace, zobrazovat protokoly v reálném čase a další.</span><span class="sxs-lookup"><span data-stu-id="43a18-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="43a18-187">Brzy po vydání sady SDK 2.2 budete moct běžet v režimu ladění vzdáleně v Azure.</span><span class="sxs-lookup"><span data-stu-id="43a18-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="43a18-188">Většina nových funkcí pro Azure App Service Web Apps funguje taky ve Visual Studiu 2012 při instalaci aktuální verze sady Azure SDK pro .NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="43a18-189">Další informace najdete v následujících materiálech:</span><span class="sxs-lookup"><span data-stu-id="43a18-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="43a18-190">Vytvoření webové aplikace ASP.NET ve službě Azure App Service</span><span class="sxs-lookup"><span data-stu-id="43a18-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="43a18-191">Poradce při potížích s webovou aplikací ve službě Azure App Service pomocí Visual Studia</span><span class="sxs-lookup"><span data-stu-id="43a18-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="43a18-192">Vylepšení publikování webu</span><span class="sxs-lookup"><span data-stu-id="43a18-192">Web Publish Enhancements</span></span>

<span data-ttu-id="43a18-193">Visual Studio 2013 obsahuje nové a vylepšené funkce publikování webu.</span><span class="sxs-lookup"><span data-stu-id="43a18-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="43a18-194">Zde je několik z nich:</span><span class="sxs-lookup"><span data-stu-id="43a18-194">Here are a few of them:</span></span>

- <span data-ttu-id="43a18-195">Snadno [automatizujte šifrování souborů Web.config](https://go.microsoft.com/fwlink/?LinkId=325529).</span><span class="sxs-lookup"><span data-stu-id="43a18-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="43a18-196">(Tento odkaz a následující dva bod dokumentace na MSDN, které nemusí být k dispozici až pozdě v den na 10/17.)</span><span class="sxs-lookup"><span data-stu-id="43a18-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="43a18-197">Snadno [automatizujte přepychaplikace aplikace během nasazení](https://go.microsoft.com/fwlink/?LinkId=325530).</span><span class="sxs-lookup"><span data-stu-id="43a18-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="43a18-198">Nakonfigurujte nasazení webu tak, aby [místo naposledy změněného data](https://go.microsoft.com/fwlink/?LinkId=325531) používalo kontrolní součet souborů pro určení, které soubory mají být zkopírovány na server.</span><span class="sxs-lookup"><span data-stu-id="43a18-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="43a18-199">Rychle publikujte jednotlivé vybrané soubory (včetně web.config) při použití metod publikování ftp nebo systému souborů a také při nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="43a18-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="43a18-200">Další informace o nasazení ASP.NET webu naleznete [na webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).</span><span class="sxs-lookup"><span data-stu-id="43a18-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="43a18-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="43a18-201">NuGet 2.7</span></span>

<span data-ttu-id="43a18-202">NuGet 2.7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány na [NuGet 2.7 Poznámky k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="43a18-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="43a18-203">Tato verze NuGet také odstraňuje potřebu poskytnout výslovný souhlas pro nuget je funkce obnovení balíčku ke stažení balíčky.</span><span class="sxs-lookup"><span data-stu-id="43a18-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="43a18-204">Souhlas (a přidružené zaškrtávací políčko v dialogu předvoleb NuGet) je nyní udělena instalací NuGet.</span><span class="sxs-lookup"><span data-stu-id="43a18-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="43a18-205">Nyní balíček obnovit prostě funguje ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="43a18-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="43a18-206">ASP.NET – webové formuláře</span><span class="sxs-lookup"><span data-stu-id="43a18-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="43a18-207">Jedna ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-207">One ASP.NET</span></span>

<span data-ttu-id="43a18-208">Šablony projektů Webových formulářů se bezproblémově integrují s novým prostředím One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="43a18-209">Do projektu webových formulářů můžete přidat podporu mvc a webového rozhraní API a ověřování můžete nakonfigurovat pomocí průvodce vytvořením projektu One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="43a18-210">Další informace naleznete v [tématu Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="43a18-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="43a18-211">ASP.NET Identity</span></span>

<span data-ttu-id="43a18-212">Šablony projektu Webových formulářů podporují novou architekturu identity ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="43a18-213">Kromě toho šablony nyní podporují vytvoření intranetového projektu webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="43a18-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="43a18-214">Další informace naleznete v [tématu Metody ověřování](creating-web-projects-in-visual-studio.md#auth) v **tématu Creating ASP.NET Web Projects in Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="43a18-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="43a18-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="43a18-215">Bootstrap</span></span>

<span data-ttu-id="43a18-216">Šablony webových formulářů používají [Bootstrap](http://twitter.github.io/bootstrap/) k zajištění elegantního a citlivého vzhledu a pocitu, který můžete snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="43a18-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="43a18-217">Další informace najdete [v tématu Bootstrap v šablonách webového projektu sady Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="43a18-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="43a18-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="43a18-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="43a18-219">Jedna ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-219">One ASP.NET</span></span>

<span data-ttu-id="43a18-220">Šablony projektu Web MVC se bezproblémově integrují s novým prostředím One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="43a18-221">Projekt MVC můžete přizpůsobit a nakonfigurovat ověřování pomocí průvodce vytvořením projektu One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a18-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="43a18-222">Úvodní výukový program pro ASP.NET MVC 5 lze nalézt na [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="43a18-223">Informace o inovaci projektů MVC 4 na MVC 5 naleznete [v tématu Jak upgradovat ASP.NET mvc 4 a projekt webového rozhraní API pro ASP.NET MVC 5 a Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="43a18-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="43a18-224">ASP.NET Identity</span></span>

<span data-ttu-id="43a18-225">Šablony projektu MVC byly aktualizovány tak, aby používaly ASP.NET identity pro ověřování a správu identit.</span><span class="sxs-lookup"><span data-stu-id="43a18-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="43a18-226">Výukový program s ověřováním na Facebooku a Google a novým rozhraním API pro členství najdete na stránce [Vytvoření aplikace ASP.NET MVC 5 s Facebookem a Google OAuth2 a přihlášením k OpenID](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) a [vytvoření ASP.NET aplikace MVC s auth a SQL DB a nasazení mapp služby Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="43a18-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="43a18-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="43a18-227">Bootstrap</span></span>

<span data-ttu-id="43a18-228">Šablona projektu MVC byla aktualizována tak, aby používala [Bootstrap,](http://getbootstrap.com/) aby poskytovala elegantní a citlivý vzhled a pocit, který můžete snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="43a18-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="43a18-229">Další informace najdete [v tématu Bootstrap v šablonách webového projektu sady Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="43a18-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="43a18-230">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="43a18-230">Authentication filters</span></span>

<span data-ttu-id="43a18-231">Filtry ověřování jsou nový druh filtru v ASP.NET MVC, které běží před filtry autorizace v kanálu ASP.NET MVC a umožňují zadat logiku ověřování na akci, na řadič nebo globálně pro všechny řadiče.</span><span class="sxs-lookup"><span data-stu-id="43a18-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="43a18-232">Ověřování filtruje pověření procesu v požadavku a poskytují odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="43a18-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="43a18-233">Filtry ověřování mohou také přidávat výzvy ověřování v reakci na neoprávněné požadavky.</span><span class="sxs-lookup"><span data-stu-id="43a18-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="43a18-234">Přepsání filtru</span><span class="sxs-lookup"><span data-stu-id="43a18-234">Filter overrides</span></span>

<span data-ttu-id="43a18-235">Nyní můžete přepsat, které filtry platí pro danou metodu akce nebo kontroleru zadáním přepsání filtru.</span><span class="sxs-lookup"><span data-stu-id="43a18-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="43a18-236">Přepsání filtrů určuje sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo řadič).</span><span class="sxs-lookup"><span data-stu-id="43a18-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="43a18-237">To umožňuje konfigurovat filtry, které platí globálně, ale pak vyloučit určité globální filtry z použití na konkrétní akce nebo řadiče.</span><span class="sxs-lookup"><span data-stu-id="43a18-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="43a18-238">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="43a18-238">Attribute routing</span></span>

<span data-ttu-id="43a18-239">ASP.NET MVC nyní podporuje atribut směrování, a to díky [http://attributerouting.net](http://attributerouting.net)příspěvku Tim McCall, autor .</span><span class="sxs-lookup"><span data-stu-id="43a18-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="43a18-240">Pomocí směrování atributů můžete zadat trasy anotací vašich akcí a kontrolorů.</span><span class="sxs-lookup"><span data-stu-id="43a18-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="43a18-241">Rozhraní API pro ASP.NET Web 2</span><span class="sxs-lookup"><span data-stu-id="43a18-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="43a18-242">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="43a18-242">Attribute routing</span></span>

<span data-ttu-id="43a18-243">ASP.NET Web API nyní podporuje směrování atributů, [http://attributerouting.net](http://attributerouting.net)a to díky příspěvku TimMcCall, autor .</span><span class="sxs-lookup"><span data-stu-id="43a18-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="43a18-244">Pomocí směrování atributů můžete zadat trasy webového rozhraní API tak, že opatříte své akce a ovladače takto:</span><span class="sxs-lookup"><span data-stu-id="43a18-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="43a18-245">Směrování atributů poskytuje větší kontrolu nad identifikátory URI ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="43a18-246">Hierarchii prostředků můžete například snadno definovat pomocí jediného řadiče rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="43a18-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="43a18-247">Směrování atributů také poskytuje vhodnou syntaxi pro určení volitelných parametrů, výchozích hodnot a omezení trasy:</span><span class="sxs-lookup"><span data-stu-id="43a18-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="43a18-248">Další informace o směrování atributů naleznete [v tématu Směrování atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="43a18-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="43a18-249">OAuth 2.0</span></span>

<span data-ttu-id="43a18-250">Šablony projektu webového rozhraní API a jednostránkové aplikace nyní podporují autorizaci pomocí oauth 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="43a18-251">OAuth 2.0 je rámec pro autorizaci přístupu klienta k chráněným prostředkům.</span><span class="sxs-lookup"><span data-stu-id="43a18-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="43a18-252">Funguje to pro různé klienty, včetně prohlížečů a mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="43a18-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="43a18-253">Podpora pro OAuth 2.0 je založena na novém bezpečnostním middlewaru poskytovaném komponentami Microsoft OWIN pro ověřování nosičů a implementaci role autorizačního serveru.</span><span class="sxs-lookup"><span data-stu-id="43a18-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="43a18-254">Alternativně lze klienty autorizovat pomocí autorizačního serveru organizace, jako je Azure Active Directory nebo ADFS v systému Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="43a18-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="43a18-255">Vylepšení OData</span><span class="sxs-lookup"><span data-stu-id="43a18-255">OData Improvements</span></span>

<span data-ttu-id="43a18-256">**Podpora pro $select, $expand, $batch a $value**</span><span class="sxs-lookup"><span data-stu-id="43a18-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="43a18-257">ASP.NET Web API OData má nyní plnou podporu pro $select, $expand a $value.</span><span class="sxs-lookup"><span data-stu-id="43a18-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="43a18-258">Můžete také použít $batch pro dávkování požadavků a zpracování sad změn.</span><span class="sxs-lookup"><span data-stu-id="43a18-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="43a18-259">Volby $select a $expand umožňují změnit tvar dat vrácených z koncového bodu OData.</span><span class="sxs-lookup"><span data-stu-id="43a18-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="43a18-260">Další informace naleznete [v tématu Představujeme $select a $expand podporu ve webovém rozhraní API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="43a18-261">**Lepší rozšiřitelnost**</span><span class="sxs-lookup"><span data-stu-id="43a18-261">**Improved extensibility**</span></span>

<span data-ttu-id="43a18-262">OData formatters jsou nyní rozšiřitelné.</span><span class="sxs-lookup"><span data-stu-id="43a18-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="43a18-263">Můžete přidat metadata položky Atom, podporovat pojmenované položky datových proudů a mediálních odkazů, přidávat poznámky instancí a přizpůsobit způsob generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="43a18-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="43a18-264">**Podpora bez typů**</span><span class="sxs-lookup"><span data-stu-id="43a18-264">**Type-less support**</span></span>

<span data-ttu-id="43a18-265">Nyní můžete vytvářet služby OData bez nutnosti definovat typy CLR pro typy entit.</span><span class="sxs-lookup"><span data-stu-id="43a18-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="43a18-266">Místo toho vaše řadiče OData můžete trvat nebo vrátit instance **IEdmObject**, které jsou OData formatters serializovat/deserializovat.</span><span class="sxs-lookup"><span data-stu-id="43a18-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="43a18-267">**Opětovné použití existujícího modelu**</span><span class="sxs-lookup"><span data-stu-id="43a18-267">**Reuse an existing model**</span></span>

<span data-ttu-id="43a18-268">Pokud již máte existující datový model entity (EDM), můžete jej nyní znovu použít přímo, místo toho, abyste museli vytvořit nový.</span><span class="sxs-lookup"><span data-stu-id="43a18-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="43a18-269">Například pokud používáte entity Framework, můžete použít EDM, který EF staví pro vás.</span><span class="sxs-lookup"><span data-stu-id="43a18-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="43a18-270">Dávkování požadavku</span><span class="sxs-lookup"><span data-stu-id="43a18-270">Request Batching</span></span>

<span data-ttu-id="43a18-271">Dávkování požadavku kombinuje více operací do jednoho požadavku HTTP POST, aby se snížil síťový provoz a poskytlo hladší a méně upovídané uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="43a18-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="43a18-272">ASP.NET webové rozhraní API nyní podporuje několik strategií pro dávkování požadavků:</span><span class="sxs-lookup"><span data-stu-id="43a18-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="43a18-273">Použijte $batch koncový bod služby OData.</span><span class="sxs-lookup"><span data-stu-id="43a18-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="43a18-274">Balíček více požadavků do jednoho vícedílného požadavku MIME.</span><span class="sxs-lookup"><span data-stu-id="43a18-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="43a18-275">Použijte vlastní formát dávkování.</span><span class="sxs-lookup"><span data-stu-id="43a18-275">Use a custom batching format.</span></span>

<span data-ttu-id="43a18-276">Chcete-li povolit dávkování požadavků, jednoduše přidejte do konfigurace webového rozhraní API trasu s obslužnou rutinou dávkování:</span><span class="sxs-lookup"><span data-stu-id="43a18-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="43a18-277">Můžete také řídit, zda požadavky nebo provedeny postupně nebo v libovolném pořadí.</span><span class="sxs-lookup"><span data-stu-id="43a18-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="43a18-278">Přenosný ASP.NET webový klient API</span><span class="sxs-lookup"><span data-stu-id="43a18-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="43a18-279">Nyní můžete pomocí ASP.NET webového rozhraní API vytvářet přenosné knihovny tříd, které fungují v aplikacích pro Windows Store a Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="43a18-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="43a18-280">Můžete také vytvořit přenosné formatters, které lze sdílet mezi klientem a serverem.</span><span class="sxs-lookup"><span data-stu-id="43a18-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="43a18-281">Vylepšená testovatelnost</span><span class="sxs-lookup"><span data-stu-id="43a18-281">Improved Testability</span></span>

<span data-ttu-id="43a18-282">Webové rozhraní API 2 usnadňuje testování částí řadičů rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="43a18-283">Stačí vytvořit instanci řadiče rozhraní API pomocí zprávy požadavku a konfigurace a potom zavolat metodu akce, kterou chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="43a18-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="43a18-284">Je také snadné zesměšňovat **UrlHelper** třídy, pro metody akce, které provádějí generování propojení.</span><span class="sxs-lookup"><span data-stu-id="43a18-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="43a18-285">IhttpActionResult</span><span class="sxs-lookup"><span data-stu-id="43a18-285">IHttpActionResult</span></span>

<span data-ttu-id="43a18-286">Nyní můžete implementovat IHttpActionResult zapouzdřit výsledek metody akce webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="43a18-287">IHttpActionResult vrácený z metody akce webového rozhraní API je proveden ASP.NET zaběhu webového rozhraní API k vytvoření výsledné zprávy odpovědi.</span><span class="sxs-lookup"><span data-stu-id="43a18-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="43a18-288">IHttpActionResult lze vrátit z libovolné akce webového rozhraní API pro zjednodušení testování částí implementace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="43a18-289">Pro pohodlí je po vybalení z krabice k dispozici řada implementací IHttpActionResult včetně výsledků pro vrácení konkrétních stavových kódů, formátovaného obsahu nebo odpovědí vyjednaných obsahem.</span><span class="sxs-lookup"><span data-stu-id="43a18-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="43a18-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="43a18-290">HttpRequestContext</span></span>

<span data-ttu-id="43a18-291">Nový **HttpRequestContext** sleduje jakýkoli stav, který je vázán na požadavek, ale není okamžitě k dispozici z požadavku.</span><span class="sxs-lookup"><span data-stu-id="43a18-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="43a18-292">Můžete například použít **HttpRequestContext** k získání dat trasy, jistiny přidružené k požadavku, klientského certifikátu, **UrlHelper** a kořenové virtuální cesty.</span><span class="sxs-lookup"><span data-stu-id="43a18-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="43a18-293">Můžete snadno vytvořit **HttpRequestContext** pro účely testování částí.</span><span class="sxs-lookup"><span data-stu-id="43a18-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="43a18-294">Vzhledem k tomu, že objekt zabezpečení pro požadavek je tok s požadavkem namísto spoléhání se na **Thread.CurrentPrincipal**, jistiny je nyní k dispozici po celou dobu životnosti požadavku, zatímco je v kanálu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="43a18-295">CORS</span><span class="sxs-lookup"><span data-stu-id="43a18-295">CORS</span></span>

<span data-ttu-id="43a18-296">Díky dalšímu skvělému příspěvku brocka Allena nyní ASP.NET plně podporuje Sdílení žádostí o cross origin (CORS).</span><span class="sxs-lookup"><span data-stu-id="43a18-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="43a18-297">Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu.</span><span class="sxs-lookup"><span data-stu-id="43a18-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="43a18-298">[CORS](http://www.w3.org/TR/cors/) je standard W3C, který umožňuje serveru uvolnit zásady stejného původu.</span><span class="sxs-lookup"><span data-stu-id="43a18-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="43a18-299">Pomocí CORS server může explicitně povolit některé požadavky napříč původy při odmítnutí jiných.</span><span class="sxs-lookup"><span data-stu-id="43a18-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="43a18-300">Webové rozhraní API 2 nyní podporuje CORS, včetně automatického zpracování požadavků kontroly před výstupem.</span><span class="sxs-lookup"><span data-stu-id="43a18-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="43a18-301">Další informace naleznete [v tématu Povolení požadavků na příčný původ v ASP.NET webovérozhraní API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="43a18-302">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="43a18-302">Authentication Filters</span></span>

<span data-ttu-id="43a18-303">Filtry ověřování jsou nový druh filtru v ASP.NET webovérozhraní API, které běží před filtry autorizace v kanálu webového rozhraní API ASP.NET a umožňují zadat logiku ověřování pro každou akci, na řadič nebo globálně pro všechny řadiče.</span><span class="sxs-lookup"><span data-stu-id="43a18-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="43a18-304">Ověřování filtruje pověření procesu v požadavku a poskytují odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="43a18-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="43a18-305">Filtry ověřování mohou také přidávat výzvy ověřování v reakci na neoprávněné požadavky.</span><span class="sxs-lookup"><span data-stu-id="43a18-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="43a18-306">Přepsání filtru</span><span class="sxs-lookup"><span data-stu-id="43a18-306">Filter Overrides</span></span>

<span data-ttu-id="43a18-307">Nyní můžete přepsat, které filtry platí pro danou metodu akce nebo řadič, zadáním přepsání filtru.</span><span class="sxs-lookup"><span data-stu-id="43a18-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="43a18-308">Přepsání filtrů určuje sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo řadič).</span><span class="sxs-lookup"><span data-stu-id="43a18-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="43a18-309">To umožňuje přidat globální filtry, ale potom vyloučit některé z konkrétních akcí nebo řadičů.</span><span class="sxs-lookup"><span data-stu-id="43a18-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="43a18-310">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-310">OWIN Integration</span></span>

<span data-ttu-id="43a18-311">ASP.NET Web API nyní plně podporuje OWIN a lze jej spustit na libovolném hostiteli schopném OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="43a18-312">Součástí je také **filtr HostAuthenticationFilter,** který poskytuje integraci se systémem ověřování OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="43a18-313">S integrací OWIN můžete samoobslužné webové rozhraní API ve vlastním procesu spolu s dalšími middleware OWIN, jako je SignalR.</span><span class="sxs-lookup"><span data-stu-id="43a18-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="43a18-314">Další informace naleznete [v tématu Použití rozhraní OWIN k vlastnímu hostiteli ASP.NET webovérozhraní API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="43a18-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="43a18-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="43a18-316">Následující části popisují funkce signalr 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="43a18-317">Postaveno na OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="43a18-318">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="43a18-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="43a18-319">Podpora mezi doménami</span><span class="sxs-lookup"><span data-stu-id="43a18-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="43a18-320">Podpora iOS a Android přes MonoTouch a MonoDroid</span><span class="sxs-lookup"><span data-stu-id="43a18-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="43a18-321">Přenosný klient .NET</span><span class="sxs-lookup"><span data-stu-id="43a18-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="43a18-322">Nový balíček samohostitele</span><span class="sxs-lookup"><span data-stu-id="43a18-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="43a18-323">Zpětně kompatibilní podpora serveru</span><span class="sxs-lookup"><span data-stu-id="43a18-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="43a18-324">Byla odebrána podpora serveru pro rozhraní .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="43a18-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="43a18-325">Odeslání zprávy seznamu klientů a skupin</span><span class="sxs-lookup"><span data-stu-id="43a18-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="43a18-326">Odeslání zprávy konkrétnímu uživateli</span><span class="sxs-lookup"><span data-stu-id="43a18-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="43a18-327">Lepší podpora zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="43a18-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="43a18-328">Snadnější testování částí hubů</span><span class="sxs-lookup"><span data-stu-id="43a18-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="43a18-329">Zpracování chyb javascriptu</span><span class="sxs-lookup"><span data-stu-id="43a18-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="43a18-330">Příklad upgradu existujícího projektu 1.x na SignalR 2.0 naleznete v [tématu Upgrade signalr 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="43a18-331">Postaveno na OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-331">Built on OWIN</span></span>

<span data-ttu-id="43a18-332">SignalR 2.0 je kompletně postaven na [OWIN (Otevřené webové rozhraní pro .NET)](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="43a18-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="43a18-333">Tato změna umožňuje proces nastavení signalr mnohem konzistentnější mezi webhostované a samostatně hostované aplikace SignalR, ale také vyžaduje řadu změn rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="43a18-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="43a18-334">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="43a18-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="43a18-335">Z důvodu kompatibility se standardy OWIN `MapSignalR`byly tyto metody přejmenovány na .</span><span class="sxs-lookup"><span data-stu-id="43a18-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="43a18-336">`MapSignalR`volána bez parametrů bude mapovat `MapHubs` všechny rozbočovače (stejně jako ve verzi 1.x); chcete-li mapovat jednotlivé objekty **PersistentConnection,** zadejte typ připojení jako parametr typu a rozšíření adresy URL pro připojení jako první argument.</span><span class="sxs-lookup"><span data-stu-id="43a18-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="43a18-337">Metoda `MapSignalR` je volána ve třídě spuštění Owin.</span><span class="sxs-lookup"><span data-stu-id="43a18-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="43a18-338">Visual Studio 2013 obsahuje novou šablonu pro spouštěcí třídu Owin; Chcete-li použít tuto šablonu, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="43a18-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="43a18-339">Klikněte pravým tlačítkem myši na projekt</span><span class="sxs-lookup"><span data-stu-id="43a18-339">Right-click on the project</span></span>
2. <span data-ttu-id="43a18-340">Vybrat **přidat**, **novou položku...**</span><span class="sxs-lookup"><span data-stu-id="43a18-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="43a18-341">Vyberte **třídu Owin Startup**.</span><span class="sxs-lookup"><span data-stu-id="43a18-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="43a18-342">Pojmenujte novou třídu **Startup.cs**.</span><span class="sxs-lookup"><span data-stu-id="43a18-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="43a18-343">Ve **webové aplikaci** je pak do `MapSignalR` Owinova spouštěcího procesu přidána třída spuštění Owin pomocí položky v uzlu nastavení aplikace souboru Web.Config, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="43a18-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="43a18-344">V **samoobslužné aplikaci**je třída Startup předána jako parametr typu `WebApp.Start` metody.</span><span class="sxs-lookup"><span data-stu-id="43a18-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="43a18-345">**Mapování rozbočovačů a připojení v SignalR 1.x (z globálního souboru aplikace ve webové aplikaci):**</span><span class="sxs-lookup"><span data-stu-id="43a18-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="43a18-346">**Mapování rozbočovačů a připojení v SignalR 2.0 (ze souboru třídy Owin Startup):**</span><span class="sxs-lookup"><span data-stu-id="43a18-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="43a18-347">V **samoobslužné aplikaci**je třída Startup předána jako parametr typu pro metodu, `WebApp.Start` jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="43a18-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="43a18-348">Podpora mezi doménami</span><span class="sxs-lookup"><span data-stu-id="43a18-348">Cross-Domain Support</span></span>

<span data-ttu-id="43a18-349">V SignalR 1.x byly požadavky mezi doménami řízeny jedním příznakem EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="43a18-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="43a18-350">Tento příznak řídil požadavky JSONP i CORS.</span><span class="sxs-lookup"><span data-stu-id="43a18-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="43a18-351">Pro větší flexibilitu byla veškerá podpora CORS odebrána ze serverové součásti SignalR (javascriptoví klienti stále používají CORS normálně, pokud je zjištěno, že prohlížeč podporuje) a pro podporu těchto scénářů byl zpřístupněn nový middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="43a18-352">V SignalR 2.0, Pokud JSONP je požadováno na straně klienta (pro podporu požadavků mezi doménami `HubConfiguration` ve `true`starších prohlížečích), bude nutné povolit explicitně nastavením `EnableJSONP` na objekt , jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="43a18-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="43a18-353">JSONP je ve výchozím nastavení zakázán, protože je méně bezpečný než CORS.</span><span class="sxs-lookup"><span data-stu-id="43a18-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="43a18-354">Chcete-li přidat nový middleware CORS v SignalR 2.0, přidejte knihovnu `Microsoft.Owin.Cors` do projektu a zavolejte `UseCors` před middleware SignalR, jak je znázorněno v části níže.</span><span class="sxs-lookup"><span data-stu-id="43a18-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="43a18-355">**Přidání programu Microsoft.Owin.Cors do projektu**: Chcete-li nainstalovat tuto knihovnu, spusťte v konzole Správce balíčků následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="43a18-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="43a18-356">Tento příkaz přidá verzi balíčku 2.0.0 do projektu.</span><span class="sxs-lookup"><span data-stu-id="43a18-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="43a18-357">**Volání UseCors**</span><span class="sxs-lookup"><span data-stu-id="43a18-357">**Calling UseCors**</span></span>

<span data-ttu-id="43a18-358">Následující fragmenty kódu ukazují, jak implementovat připojení mezi doménami v signalr 1.x a 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="43a18-359">**Implementace požadavků mezi doménami v SignalR 1.x (z globálního souboru aplikace)**</span><span class="sxs-lookup"><span data-stu-id="43a18-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="43a18-360">**Implementace požadavků mezi doménami v signalr 2.0 (ze souboru kódu Jazyka C#)**</span><span class="sxs-lookup"><span data-stu-id="43a18-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="43a18-361">Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="43a18-362">Tato ukázka `Map` `RunSignalR` kódu `MapSignalR`používá a místo , tak, aby middleware CORS běží pouze pro požadavky SignalR, které `MapSignalR`vyžadují podporu CORS (spíše než pro všechny provozy na cestě určené v .) `Map` lze také použít pro jakýkoli jiný middleware, který je třeba spustit pro konkrétní předponu URL, spíše než pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="43a18-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="43a18-363">Podpora iOS a Android přes MonoTouch a MonoDroid</span><span class="sxs-lookup"><span data-stu-id="43a18-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="43a18-364">Byla přidána podpora pro klienty iOS a Android pomocí komponent MonoTouch a MonoDroid z [knihovny Xamarin](https://xamarin.com/).</span><span class="sxs-lookup"><span data-stu-id="43a18-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="43a18-365">Další informace o jejich použití naleznete v tématu [Použití součástí Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span><span class="sxs-lookup"><span data-stu-id="43a18-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="43a18-366">Tyto součásti budou k dispozici v [obchodě Xamarin,](https://store.xamarin.com/) jakmile bude k dispozici verze SignalR RTW.</span><span class="sxs-lookup"><span data-stu-id="43a18-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="43a18-367">### Přenosný klient .NET</span><span class="sxs-lookup"><span data-stu-id="43a18-367">### Portable .NET client</span></span>

<span data-ttu-id="43a18-368">Pro lepší usnadnění vývoje napříč platformami byli klienti Silverlight, WinRT a Windows Phone nahrazeni jediným přenosným klientem .NET, který podporuje následující platformy:</span><span class="sxs-lookup"><span data-stu-id="43a18-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="43a18-369">NET 4,5</span><span class="sxs-lookup"><span data-stu-id="43a18-369">NET 4.5</span></span>
- <span data-ttu-id="43a18-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="43a18-370">Silverlight 5</span></span>
- <span data-ttu-id="43a18-371">WinRT (.NET pro aplikace pro Windows Store)</span><span class="sxs-lookup"><span data-stu-id="43a18-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="43a18-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="43a18-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="43a18-373">Nový balíček samohostitele</span><span class="sxs-lookup"><span data-stu-id="43a18-373">New Self-Host Package</span></span>

<span data-ttu-id="43a18-374">Nyní je balíček NuGet, který usnadňuje zahájení s vlastním hostitelem SignalR (aplikace SignalR, které jsou hostovány v procesu nebo jiné aplikaci, spíše než hostované na webovém serveru).</span><span class="sxs-lookup"><span data-stu-id="43a18-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="43a18-375">Chcete-li upgradovat projekt vlastního hostitele vytvořený pomocí signalr 1.x, odeberte balíček Microsoft.AspNet.SignalR.Owin a přidejte balíček Microsoft.AspNet.SignalR.SelfHost.</span><span class="sxs-lookup"><span data-stu-id="43a18-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="43a18-376">Další informace o tom, jak začít s balíčkem s vlastním hostitelem, naleznete [v tématu Výuka: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="43a18-377">Zpětně kompatibilní podpora serveru</span><span class="sxs-lookup"><span data-stu-id="43a18-377">Backward-compatible server support</span></span>

<span data-ttu-id="43a18-378">V předchozích verzích SignalR, verze balíčku SignalR používané v klientovi a server musí být identické.</span><span class="sxs-lookup"><span data-stu-id="43a18-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="43a18-379">Za účelem podpory aplikací s tlustou klientskou službou, které by bylo obtížné aktualizovat, aplikace SignalR 2.0 nyní podporuje použití novější verze serveru se starším klientem.</span><span class="sxs-lookup"><span data-stu-id="43a18-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="43a18-380">**Poznámka: SignalR 2.0 nepodporuje servery postavené se staršími verzemi s novějšími klienty.**</span><span class="sxs-lookup"><span data-stu-id="43a18-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="43a18-381">Byla odebrána podpora serveru pro rozhraní .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="43a18-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="43a18-382">SignalR 2.0 snížil podporu pro interoperabilitu serveru s rozhraním .NET 4.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="43a18-383">.NET 4.5 musí být použit se servery SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="43a18-384">Stále existuje klient .NET 4.0 pro SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="43a18-385">Odeslání zprávy seznamu klientů a skupin</span><span class="sxs-lookup"><span data-stu-id="43a18-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="43a18-386">V SignalR 2.0 je možné odeslat zprávu pomocí seznamu ID klienta a skupiny.</span><span class="sxs-lookup"><span data-stu-id="43a18-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="43a18-387">Následující fragmenty kódu ukazují, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="43a18-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="43a18-388">**Odeslání zprávy seznamu klientů a skupin pomocí programu PersistentConnection**</span><span class="sxs-lookup"><span data-stu-id="43a18-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="43a18-389">**Odeslání zprávy seznamu klientů a skupin pomocí hubů**</span><span class="sxs-lookup"><span data-stu-id="43a18-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="43a18-390">Odeslání zprávy konkrétnímu uživateli</span><span class="sxs-lookup"><span data-stu-id="43a18-390">Sending a message to a specific user</span></span>

<span data-ttu-id="43a18-391">Tato funkce umožňuje uživatelům určit, co userId je založena na IRequest prostřednictvím nového rozhraní IUserIdProvider:</span><span class="sxs-lookup"><span data-stu-id="43a18-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="43a18-392">**Rozhraní IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="43a18-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="43a18-393">Ve výchozím nastavení bude existovat implementace, která používá IPrincipal.Identity.Name uživatele jako uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="43a18-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="43a18-394">V rozbočovačích budete moci odesílat zprávy těmto uživatelům prostřednictvím nového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="43a18-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="43a18-395">**Použití rozhraní Clients.User API**</span><span class="sxs-lookup"><span data-stu-id="43a18-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="43a18-396">Lepší podpora zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="43a18-396">Better Error Handling Support</span></span>

<span data-ttu-id="43a18-397">Uživatelé nyní mohou vyvolat **HubException** z libovolného vyvolání centra.</span><span class="sxs-lookup"><span data-stu-id="43a18-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="43a18-398">Konstruktor **HubException** může trvat zprávu řetězce a objekt další data chyb.</span><span class="sxs-lookup"><span data-stu-id="43a18-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="43a18-399">SignalR bude automaticky serializovat výjimku a odeslat klientovi, kde bude použit k odmítnutí nebo selhání vyvolání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="43a18-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="43a18-400">Zobrazit **podrobné hub výjimky** nastavení nemá žádný vliv na **HubException** odesílázpět klientovi nebo ne; je vždy odeslána.</span><span class="sxs-lookup"><span data-stu-id="43a18-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="43a18-401">**Kód na straně serveru demonstrující odesílání hubexception klientovi**</span><span class="sxs-lookup"><span data-stu-id="43a18-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="43a18-402">**Kód klienta JavaScriptu demonstrující odpověď na hubexception odeslaný ze serveru**</span><span class="sxs-lookup"><span data-stu-id="43a18-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="43a18-403">**Kód klienta .NET demonstrující odpověď na hubexception odeslaný ze serveru**</span><span class="sxs-lookup"><span data-stu-id="43a18-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="43a18-404">Snadnější testování částí hubů</span><span class="sxs-lookup"><span data-stu-id="43a18-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="43a18-405">SignalR 2.0 obsahuje `IHubCallerConnectionContext` rozhraní volané na rozbočovače, které usnadňuje vytváření falešných vyvolání na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="43a18-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="43a18-406">Následující fragmenty kódu ukazují použití tohoto rozhraní s oblíbenými testovacími postroji [xUnit.net](https://github.com/xunit/xunit) a [moq](https://code.google.com/p/moq/).</span><span class="sxs-lookup"><span data-stu-id="43a18-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="43a18-407">**Jednotkové testování SignalR s xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="43a18-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="43a18-408">**Testování částí SignalR s moq**</span><span class="sxs-lookup"><span data-stu-id="43a18-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="43a18-409">Zpracování chyb javascriptu</span><span class="sxs-lookup"><span data-stu-id="43a18-409">JavaScript error handling</span></span>

<span data-ttu-id="43a18-410">V SignalR 2.0 všechny chyby JavaScript zpracování zpětná volání vrátit javascriptové chybové objekty namísto nezpracovaných řetězců.</span><span class="sxs-lookup"><span data-stu-id="43a18-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="43a18-411">To umožňuje SignalR toku bohatší informace o obslužné rutiny chyb.</span><span class="sxs-lookup"><span data-stu-id="43a18-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="43a18-412">Můžete získat vnitřní výjimku `source` z vlastnosti chyby.</span><span class="sxs-lookup"><span data-stu-id="43a18-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="43a18-413">**Kód klienta JavaScriptu, který zpracovává výjimku Start.Fail**</span><span class="sxs-lookup"><span data-stu-id="43a18-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="43a18-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="43a18-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="43a18-415">Nový systém členství v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="43a18-416">ASP.NET Identity je nový systém členství pro ASP.NET aplikace.</span><span class="sxs-lookup"><span data-stu-id="43a18-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="43a18-417">ASP.NET Identity usnadňuje integraci dat profilu specifického pro uživatele s daty aplikací.</span><span class="sxs-lookup"><span data-stu-id="43a18-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="43a18-418">ASP.NET identity také umožňuje zvolit model trvalosti pro profily uživatelů ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="43a18-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="43a18-419">Data můžete uložit do databáze serveru SQL Server nebo do jiného úložiště dat, včetně úložišť dat NoSQL, jako jsou tabulky úložiště Azure.</span><span class="sxs-lookup"><span data-stu-id="43a18-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="43a18-420">Další informace naleznete [v tématu Jednotlivé uživatelské účty](creating-web-projects-in-visual-studio.md#indauth) v **tématu vytváření ASP.NET webových projektů v sadě Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="43a18-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="43a18-421">Ověřování na základě deklarací</span><span class="sxs-lookup"><span data-stu-id="43a18-421">Claims-based authentication</span></span>

<span data-ttu-id="43a18-422">ASP.NET nyní podporuje ověřování na základě deklarací identity, kde je identita uživatele reprezentována jako sada deklarací od důvěryhodného vystavittele.</span><span class="sxs-lookup"><span data-stu-id="43a18-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="43a18-423">Uživatele lze ověřovat pomocí uživatelského jména a hesla uchovávaných v databázi aplikací nebo pomocí poskytovatelů sociální identity (například Účty Microsoft, Facebook, Google, Twitter) nebo pomocí účtů organizace prostřednictvím služby Azure Active Directory nebo Služby ADF (ADFS).</span><span class="sxs-lookup"><span data-stu-id="43a18-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="43a18-424">Integrace se službou Azure Active Directory a službou Windows Server Active Directory</span><span class="sxs-lookup"><span data-stu-id="43a18-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="43a18-425">Nyní můžete vytvořit ASP.NET projekty, které používají Azure Active Directory nebo Windows Server Active Directory (AD) pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="43a18-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="43a18-426">Další informace naleznete v [tématu Organizační účty](creating-web-projects-in-visual-studio.md#orgauth) v **tématu Vytváření ASP.NET webových projektů v sadě Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="43a18-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="43a18-427">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-427">OWIN Integration</span></span>

<span data-ttu-id="43a18-428">ASP.NET ověřování je nyní založeno na middlewaru OWIN, který lze použít na libovolném hostiteli založeném na OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="43a18-429">Další informace o OWIN naleznete v následující části [Součásti Microsoft OWIN.](#TOC7)</span><span class="sxs-lookup"><span data-stu-id="43a18-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="43a18-430">Součásti Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="43a18-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="43a18-431">[Otevřené webové rozhraní pro rozhraní .NET](http://owin.org/) (OWIN) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="43a18-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="43a18-432">OWIN odděluje webové aplikace od serveru, takže webové aplikace host-agnostik.</span><span class="sxs-lookup"><span data-stu-id="43a18-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="43a18-433">Můžete například hostovat webovou aplikaci založenou na OWIN ve službě IIS nebo ji sami hostovat ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="43a18-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="43a18-434">Změny zavedené v součástech Microsoft OWIN (označované také jako projekt Katana) zahrnují nové serverové a hostitelské součásti, nové pomocné knihovny a middleware a nový ověřovací middleware.</span><span class="sxs-lookup"><span data-stu-id="43a18-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="43a18-435">Další informace o OWIN a Kataně najdete [v tématu Co je nového v OWIN a Kataně](../../../aspnet/overview/owin-and-katana/index.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="43a18-436">**Poznámka: [Aplikace OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) nelze spustit v klasickém režimu iis. musí být provozovány v integrovaném režimu.**</span><span class="sxs-lookup"><span data-stu-id="43a18-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="43a18-437">**Poznámka: [Aplikace OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) musí být spuštěny v plné důvěře.**</span><span class="sxs-lookup"><span data-stu-id="43a18-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="43a18-438">Nové servery a hostitelé</span><span class="sxs-lookup"><span data-stu-id="43a18-438">New Servers and Hosts</span></span>

<span data-ttu-id="43a18-439">V této verzi byly přidány nové součásti, které umožňují scénáře vlastního hostitele.</span><span class="sxs-lookup"><span data-stu-id="43a18-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="43a18-440">Mezi tyto součásti patří následující balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="43a18-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="43a18-441">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="43a18-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="43a18-442">Poskytuje server OWIN, který používá **HttpListener** naslouchat požadavkům HTTP a nasměrovat je do kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="43a18-443">**Microsoft.Owin.Hosting** Poskytuje knihovnu pro vývojáře, kteří chtějí vlastní hostování kanálu OWIN ve vlastním procesu, jako je například konzolová aplikace nebo služba systému Windows.</span><span class="sxs-lookup"><span data-stu-id="43a18-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="43a18-444">**OwinHost**.</span><span class="sxs-lookup"><span data-stu-id="43a18-444">**OwinHost**.</span></span> <span data-ttu-id="43a18-445">Poskytuje samostatný spustitelný soubor, `Microsoft.Owin.Hosting` který zabalí a umožňuje vlastní hostování kanálu OWIN bez nutnosti psát vlastní hostitelskou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="43a18-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="43a18-446">Kromě toho `Microsoft.Owin.Host.SystemWeb` balíček nyní umožňuje middleware poskytovat rady **serveru SystemWeb,** označující, že middleware by měla být volána během určité ASP.NET fáze kanálu.</span><span class="sxs-lookup"><span data-stu-id="43a18-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="43a18-447">Tato funkce je užitečná zejména pro ověřování middleware, který by měl být spuštěn v rané fázi ASP.NET kanálu.</span><span class="sxs-lookup"><span data-stu-id="43a18-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="43a18-448">Pomocné knihovny a middleware</span><span class="sxs-lookup"><span data-stu-id="43a18-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="43a18-449">I když můžete psát komponenty OWIN pouze pomocí definice funkce a `Microsoft.Owin` typu ze specifikace OWIN, nový balíček poskytuje uživatelsky přívětivější sadu abstrakcí.</span><span class="sxs-lookup"><span data-stu-id="43a18-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="43a18-450">Tento balíček kombinuje několik dřívějších balíčků `Owin.Extensions` `Owin.Types`(např. ,) do jednoho, dobře strukturovaného objektového modelu, který pak mohou snadno používat jiné komponenty OWIN.</span><span class="sxs-lookup"><span data-stu-id="43a18-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="43a18-451">Ve skutečnosti většina součástí Microsoft OWIN nyní používá tento balíček.</span><span class="sxs-lookup"><span data-stu-id="43a18-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="43a18-452">[Aplikace OWIN](http://www.owin.org) nelze spustit v klasickém režimu iis. musí být provozovány v integrovaném režimu.</span><span class="sxs-lookup"><span data-stu-id="43a18-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="43a18-453">[Aplikace OWIN](http://www.owin.org) musí být spuštěny v plné důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="43a18-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="43a18-454">Tato verze také obsahuje balíček Microsoft.Owin.Diagnostics, který obsahuje middleware k ověření spuštěné aplikace OWIN, plus middleware chybové stránky, které pomáhají vyšetřovat chyby.</span><span class="sxs-lookup"><span data-stu-id="43a18-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="43a18-455">Součásti ověřování</span><span class="sxs-lookup"><span data-stu-id="43a18-455">Authentication Components</span></span>

<span data-ttu-id="43a18-456">K dispozici jsou následující součásti ověřování.</span><span class="sxs-lookup"><span data-stu-id="43a18-456">The following authentication components are available.</span></span>

- <span data-ttu-id="43a18-457">**Adresář Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="43a18-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="43a18-458">Umožňuje ověřování pomocí místních nebo cloudových adresářových služeb.</span><span class="sxs-lookup"><span data-stu-id="43a18-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="43a18-459">**Microsoft.Owin.Security.Cookies** Umožňuje ověřování pomocí souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="43a18-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="43a18-460">Tento balíček `Microsoft.Owin.Security.Forms`byl dříve pojmenován .</span><span class="sxs-lookup"><span data-stu-id="43a18-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="43a18-461">**Microsoft.Owin.Security.Facebook** Umožňuje ověřování pomocí služby OAuth založené na Facebooku.</span><span class="sxs-lookup"><span data-stu-id="43a18-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="43a18-462">**Microsoft.Owin.Security.Google** Umožňuje ověřování pomocí služby Založené na OpenID společnosti Google.</span><span class="sxs-lookup"><span data-stu-id="43a18-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="43a18-463">**Microsoft.Owin.Security.Jwt** Umožňuje ověřování pomocí tokenů JWT.</span><span class="sxs-lookup"><span data-stu-id="43a18-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="43a18-464">**Microsoft.Owin.Security.MicrosoftAccount** Umožňuje ověřování pomocí účtů Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43a18-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="43a18-465">**Microsoft.Owin.Security.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="43a18-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="43a18-466">Poskytuje autorizační server OAuth a middleware pro ověřování tokenů nosiče.</span><span class="sxs-lookup"><span data-stu-id="43a18-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="43a18-467">**Microsoft.Owin.Security.Twitter** Umožňuje ověřování pomocí služby OAuth založené na Twitteru.</span><span class="sxs-lookup"><span data-stu-id="43a18-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="43a18-468">Tato verze obsahuje `Microsoft.Owin.Cors` také balíček, který obsahuje middleware pro zpracování požadavků HTTP napříč původem.</span><span class="sxs-lookup"><span data-stu-id="43a18-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="43a18-469">Podpora podepisování JWT byla odebrána v konečné verzi Sady Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43a18-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="43a18-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="43a18-470">Entity Framework 6</span></span>

<span data-ttu-id="43a18-471">Seznam nových funkcí a další chod v rámci entity 6 naleznete v [tématu Entity Framework Version History](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="43a18-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="43a18-472">ASP.NET Břitva 3</span><span class="sxs-lookup"><span data-stu-id="43a18-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="43a18-473">ASP.NET Razor 3 obsahuje následující nové funkce:</span><span class="sxs-lookup"><span data-stu-id="43a18-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="43a18-474">Podpora pro úpravy tabulátoru.</span><span class="sxs-lookup"><span data-stu-id="43a18-474">Support for Tab editing.</span></span> <span data-ttu-id="43a18-475">Dříve příkaz **Formát dokumentu,** automatické odsazení a automatické formátování v sadě Visual Studio nefungovaly správně při použití možnosti **Zachovat karty.**</span><span class="sxs-lookup"><span data-stu-id="43a18-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="43a18-476">Tato změna opravuje Visual Studio formátování pro razor kód pro formátování karty.</span><span class="sxs-lookup"><span data-stu-id="43a18-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="43a18-477">Podpora pravidel přepisování adres URL při generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="43a18-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="43a18-478">Odstranění transparentního atributu zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="43a18-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="43a18-479">Jedná se o narušující změnu a razor 3 je nekompatibilní s MVC4 a starší, zatímco Razor 2 je nekompatibilní s MVC5 nebo sestavení kompilované proti MVC5.</span><span class="sxs-lookup"><span data-stu-id="43a18-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="43a18-480">Problémy s razorem 3 opravené v sadě Visual Studio 2013 z předběžných verzí naleznete [zde](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="43a18-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="43a18-481">ASP.NET pozastavení aplikace</span><span class="sxs-lookup"><span data-stu-id="43a18-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="43a18-482">ASP.NET App Suspend je hra měnící funkce v rozhraní .NET Framework 4.5.1, která radikálně mění uživatelské prostředí a ekonomický model pro hostování velkého počtu ASP.NET lokalit na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="43a18-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="43a18-483">Další informace naleznete [v tématu ASP.NET App Suspend – responzivní sdílený web hosting .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span><span class="sxs-lookup"><span data-stu-id="43a18-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="43a18-484">Známé problémy a nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="43a18-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="43a18-485">Tato část popisuje známé problémy a narušující změny v ASP.NET a webových nástrojích pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43a18-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="43a18-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="43a18-486">NuGet</span></span>

- <span data-ttu-id="43a18-487">[Nový balíček obnovení nefunguje na Mono při použití souboru SLN](https://nuget.codeplex.com/workitem/3596) – bude opravena v nadcházející nuget.exe download a [NuGet.CommandLine balíček](http://www.nuget.org/packages/NuGet.CommandLine/) aktualizace.</span><span class="sxs-lookup"><span data-stu-id="43a18-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="43a18-488">[Obnovení nového balíčku nefunguje s projekty Wix](https://nuget.codeplex.com/workitem/3598) – bude opraveno v nadcházejícím stahování nuget.exe a aktualizaci [balíčku NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)</span><span class="sxs-lookup"><span data-stu-id="43a18-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="43a18-489">[Automatické obnovení balíčků nefunguje pro projekty ve složce řešení](https://nuget.codeplex.com/workitem/3625) – bude opravena v NuGet 2.8.</span><span class="sxs-lookup"><span data-stu-id="43a18-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="43a18-490">Webové rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43a18-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="43a18-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`se nevrátí `IQueryable<T>` vždy, jak jsme `$select` přidali podporu pro a `$expand`.</span><span class="sxs-lookup"><span data-stu-id="43a18-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="43a18-492">Naše dřívější `ODataQueryOptions<T>` ukázky pro vždy `ApplyTo` obsazení `IQueryable<T>`vrácená hodnota z .</span><span class="sxs-lookup"><span data-stu-id="43a18-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="43a18-493">To fungovalo dříve, protože možnosti`$filter` `$orderby`dotazu, které jsme podporovali dříve ( , , `$skip`, `$top`) nemění tvar dotazu.</span><span class="sxs-lookup"><span data-stu-id="43a18-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="43a18-494">Nyní, když `$select` `$expand` podporujeme a `ApplyTo` návratová `IQueryable<T>` hodnota z nebude vždy.</span><span class="sxs-lookup"><span data-stu-id="43a18-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="43a18-495">Pokud používáte ukázkový kód z předchozích, bude pokračovat `$select` v `$expand`práci, pokud klient neodesílá a .</span><span class="sxs-lookup"><span data-stu-id="43a18-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="43a18-496">Pokud však chcete `$select` podporovat `$expand` a budete muset změnit tento kód na toto.</span><span class="sxs-lookup"><span data-stu-id="43a18-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="43a18-497">**Request.Url nebo RequestContext.Url má hodnotu null během dávkového požadavku.**</span><span class="sxs-lookup"><span data-stu-id="43a18-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="43a18-498">Ve scénáři dávkování je **urlhelper** null při přístupu z **Request.Url** nebo **RequestContext.Url**.</span><span class="sxs-lookup"><span data-stu-id="43a18-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="43a18-499">Tento problém je nyní sledován zde: [BatchRequestContext.Url je null pro dávkování požadavku](http://aspnetwebstack.codeplex.com/workitem/1301).</span><span class="sxs-lookup"><span data-stu-id="43a18-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="43a18-500">Řešení tohoto problému je vytvořit novou instanci **UrlHelper**, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="43a18-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="43a18-501">**Vytvoření nové instance urlhelperu**</span><span class="sxs-lookup"><span data-stu-id="43a18-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="43a18-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="43a18-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="43a18-503">Při použití MVC5 a OrgAuth, pokud máte zobrazení, která antiforgerToken ověření, můžete narazit na následující chybu při zaúčtování dat do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="43a18-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="43a18-504">**Chyba**:</span><span class="sxs-lookup"><span data-stu-id="43a18-504">**Error**:</span></span>

    <span data-ttu-id="43a18-505">*Chyba serveru v aplikaci/.*</span><span class="sxs-lookup"><span data-stu-id="43a18-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="43a18-506"><em>Nárok typu "<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>"<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>nebo " nebyl v poskytnuté deklaraci identity claimidentity. Chcete-li povolit podporu tokenů proti padělání s ověřováním na základě deklarací identity, ověřte, zda nakonfigurovaný poskytovatel deklarací identit y poskytuje obě tyto deklarace identity v instancích ClaimsIdentity, které generuje. Pokud nakonfigurovaný zprostředkovatel deklarací používá jako jedinečný identifikátor jiný typ deklarace identity, lze jej nakonfigurovat nastavením statické vlastnosti AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span><span class="sxs-lookup"><span data-stu-id="43a18-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="43a18-507">**Řešení**:</span><span class="sxs-lookup"><span data-stu-id="43a18-507">**Workaround**:</span></span>

    <span data-ttu-id="43a18-508">Přidejte do global.asax následující řádek, abyste to opravili:</span><span class="sxs-lookup"><span data-stu-id="43a18-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="43a18-509">Tato oprava bude opravena pro další verzi.</span><span class="sxs-lookup"><span data-stu-id="43a18-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="43a18-510">Po upgradu aplikace MVC4 na MVC5 sestavte řešení a spusťte ho.</span><span class="sxs-lookup"><span data-stu-id="43a18-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="43a18-511">Měla by se zobrazit následující chyba:</span><span class="sxs-lookup"><span data-stu-id="43a18-511">You should see the following error:</span></span>

    <span data-ttu-id="43a18-512">[A] System.Web.WebPages.Razor.Configuration.HostSection nelze přetypovat na [B]System.Web.WebPages.Razor.Configuration.HostSection.</span><span class="sxs-lookup"><span data-stu-id="43a18-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="43a18-513">Typ A pochází z 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' v kontextu 'Default' v\_umístění 'C:\windows\Microsoft.Net\assembly\GAC MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="43a18-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="43a18-514">Typ B pochází z 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' v kontextu "Výchozí" v umístění C:\Windows\Microsoft.NET\Framework\v4.0.30319\Dočasné ASP.NET Soubory\root\6 d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="43a18-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="43a18-515">Chcete-li opravit výše uvedenou chybu, otevřete v projektu *všechny* soubory Web.config (včetně těch ve složce Zobrazení) a postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="43a18-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="43a18-516">Aktualizujte všechny výskyty verze "4.0.0.0" "System.Web.Mvc" na "5.0.0.0".</span><span class="sxs-lookup"><span data-stu-id="43a18-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="43a18-517">Aktualizujte všechny výskyty verze &quot;"2.0.0.0" "System.Web.Helpers", System.Web.WebPages&quot; a &quot;System.Web.WebPages.Razor&quot; na "3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="43a18-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="43a18-518">Například po provedené výše uvedené změny vazby sestavení by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="43a18-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="43a18-519">Informace o inovaci projektů MVC 4 na MVC 5 naleznete [v tématu Jak upgradovat ASP.NET mvc 4 a projekt webového rozhraní API pro ASP.NET MVC 5 a Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="43a18-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="43a18-520">Při použití ověření na straně klienta s jQuery Nenápadné ověření, ověřovací zpráva je někdy nesprávné pro vstupní prvek HTML s type ='number'.</span><span class="sxs-lookup"><span data-stu-id="43a18-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="43a18-521">Chyba ověření pro požadovanou hodnotu ("Pole stáří je povinné") se zobrazí, když je zadáno neplatné číslo namísto správné zprávy, že je vyžadováno platné číslo.</span><span class="sxs-lookup"><span data-stu-id="43a18-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="43a18-522">Tento problém se běžně vyskytuje s kódem scaffolded pro model s vlastností celé číslo v zobrazení vytvořit a upravit.</span><span class="sxs-lookup"><span data-stu-id="43a18-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="43a18-523">Chcete-li tento problém vyřešit, změňte pomocníka editoru z:</span><span class="sxs-lookup"><span data-stu-id="43a18-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="43a18-524">Do:</span><span class="sxs-lookup"><span data-stu-id="43a18-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="43a18-525">ASP.NET MVC 5 již nepodporuje částečnou důvěryhodnost.</span><span class="sxs-lookup"><span data-stu-id="43a18-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="43a18-526">Projekty, které odkazují na binární soubory MVC nebo WebAPI, by měly odebrat atribut [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) a atribut [AllowPartiallyTrustedCallers.](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)</span><span class="sxs-lookup"><span data-stu-id="43a18-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="43a18-527">Odebrání těchto atributů eliminuje chyby kompilátoru, jako je například následující.</span><span class="sxs-lookup"><span data-stu-id="43a18-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="43a18-528">Všimněte si, že jako vedlejší účinek tohoto nelze použít 4.0 a 5.0 sestavení ve stejné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="43a18-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="43a18-529">Je třeba aktualizovat všechny z nich 5.0.</span><span class="sxs-lookup"><span data-stu-id="43a18-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="43a18-530">Šablona SPA s autorizací facebooku může způsobit nestabilitu v aplikaci IE, zatímco web je hostován v intranetové zóně</span><span class="sxs-lookup"><span data-stu-id="43a18-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="43a18-531">Šablona SPA poskytuje externí přihlášení pomocí Facebooku.</span><span class="sxs-lookup"><span data-stu-id="43a18-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="43a18-532">Pokud je projekt vytvořený pomocí šablony spuštěn místně, přihlašování může způsobit selhání aplikace IE.</span><span class="sxs-lookup"><span data-stu-id="43a18-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="43a18-533">Řešení:</span><span class="sxs-lookup"><span data-stu-id="43a18-533">Solution:</span></span>

1. <span data-ttu-id="43a18-534">Host webové stránky v internetové zóně; Nebo</span><span class="sxs-lookup"><span data-stu-id="43a18-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="43a18-535">Otestujte scénář v jiném prohlížeči než IE.</span><span class="sxs-lookup"><span data-stu-id="43a18-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="43a18-536">Lešení webových formulářů</span><span class="sxs-lookup"><span data-stu-id="43a18-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="43a18-537">Webové formuláře lešení byla odebrána z VS2013 a bude k dispozici v budoucí aktualizaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43a18-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="43a18-538">Generování uživatelského přihrádky však můžete v rámci projektu webových formulářů stále používat přidáním závislostí MVC a generováním generování generování pro mvc.</span><span class="sxs-lookup"><span data-stu-id="43a18-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="43a18-539">Projekt bude obsahovat kombinaci webových formulářů a mvc.</span><span class="sxs-lookup"><span data-stu-id="43a18-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="43a18-540">Chcete-li přidat mvc do projektu webových formulářů, přidejte novou položku scaffolded a vyberte **položku Závislosti MVC 5**.</span><span class="sxs-lookup"><span data-stu-id="43a18-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="43a18-541">Vyberte možnost Minimální nebo Úplná v závislosti na tom, zda potřebujete všechny soubory obsahu, například skripty.</span><span class="sxs-lookup"><span data-stu-id="43a18-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="43a18-542">Potom přidejte šálací kód pro MVC, který vytvoří zobrazení a řadič v projektu.</span><span class="sxs-lookup"><span data-stu-id="43a18-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="43a18-543">MVC a webové api lešení - HTTP 404, nebyla nalezena chyba</span><span class="sxs-lookup"><span data-stu-id="43a18-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="43a18-544">Pokud dojde k chybě při přidávání šástavlna položky do projektu, je možné, že projekt bude ponechán v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="43a18-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="43a18-545">Některé provedené změny se šaše budou vráceny zpět, ale jiné změny, jako jsou například nainstalované balíčky NuGet, nebudou vráceny zpět.</span><span class="sxs-lookup"><span data-stu-id="43a18-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="43a18-546">Pokud jsou změny konfigurace směrování vráceny zpět, uživatelé obdrží chybu HTTP 404 při navigaci na položky sklopné kódy.</span><span class="sxs-lookup"><span data-stu-id="43a18-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="43a18-547">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="43a18-547">Workaround:</span></span>

- <span data-ttu-id="43a18-548">Chcete-li opravit tuto chybu pro MVC, přidejte novou položku scaffolded a vyberte mvc 5 závislosti (minimální nebo úplné).</span><span class="sxs-lookup"><span data-stu-id="43a18-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="43a18-549">Tento proces přidá všechny požadované změny do projektu.</span><span class="sxs-lookup"><span data-stu-id="43a18-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="43a18-550">Oprava této chyby pro webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="43a18-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="43a18-551">Přidejte třídu WebApiConfig do projektu.</span><span class="sxs-lookup"><span data-stu-id="43a18-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="43a18-552">Konfigurace webapiconfig.register v\_metodě Start aplikace v Global.asax takto:</span><span class="sxs-lookup"><span data-stu-id="43a18-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
