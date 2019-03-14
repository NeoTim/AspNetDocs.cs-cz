---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET and Web Tools pro Visual Studio 2013 – poznámky k | Dokumentace Microsoftu
author: microsoft
description: Tento dokument popisuje verzi technologie ASP.NET and Web Tools pro Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 43878bc101ef97e8bbb6c150f4125707da7660c9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066844"
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="24e05-103">ASP.NET a webové nástroje pro Visual Studio 2013 – poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="24e05-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>
====================
<span data-ttu-id="24e05-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="24e05-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="24e05-105">Tento dokument popisuje verzi technologie ASP.NET and Web Tools pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="24e05-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>


## <a name="contents"></a><span data-ttu-id="24e05-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="24e05-106">Contents</span></span>

- [<span data-ttu-id="24e05-107">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="24e05-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="24e05-108">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="24e05-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="24e05-109">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="24e05-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="24e05-110">Novinky v ASP.NET and Web Tools pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="24e05-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="24e05-111">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="24e05-112">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="24e05-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="24e05-113">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="24e05-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="24e05-114">Browser Link</span><span class="sxs-lookup"><span data-stu-id="24e05-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="24e05-115">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="24e05-116">Podpora aplikací webové služby Azure App Service v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="24e05-117">Vylepšení publikování webu</span><span class="sxs-lookup"><span data-stu-id="24e05-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="24e05-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="24e05-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="24e05-119">Webové formuláře ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="24e05-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="24e05-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="24e05-121">Rozhraní ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="24e05-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="24e05-122">Funkce SignalR technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="24e05-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="24e05-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="24e05-124">Komponenty Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="24e05-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="24e05-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="24e05-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="24e05-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="24e05-127">Pozastavení aplikace technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="24e05-128">Známé problémy a změny způsobující chyby</span><span class="sxs-lookup"><span data-stu-id="24e05-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="24e05-129">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="24e05-129">Installation Notes</span></span>

<span data-ttu-id="24e05-130">ASP.NET and Web Tools pro Visual Studio 2013 jsou spojeny v instalačním programu pro hlavní a je možné stáhnout [tady](https://www.asp.net/downloads).</span><span class="sxs-lookup"><span data-stu-id="24e05-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="24e05-131">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="24e05-131">Documentation</span></span>

<span data-ttu-id="24e05-132">Kurzy a další informace o ASP.NET and Web Tools pro Visual Studio 2013 jsou k dispozici [Web ASP.NET s](https://www.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="24e05-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="24e05-133">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="24e05-133">Software Requirements</span></span>

<span data-ttu-id="24e05-134">ASP.NET and Web Tools vyžaduje Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="24e05-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="24e05-135">Novinky v ASP.NET and Web Tools pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="24e05-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="24e05-136">Následující části popisují funkce, které byly zavedeny ve vydané verzi.</span><span class="sxs-lookup"><span data-stu-id="24e05-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="24e05-137">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-137">One ASP.NET</span></span>

<span data-ttu-id="24e05-138">S vydáním sady Visual Studio 2013 jsme udělali krok k zabezpečení sjednocujícího prostředí pomocí technologie ASP.NET, takže můžete snadno kombinovat a párovat ty, které chcete.</span><span class="sxs-lookup"><span data-stu-id="24e05-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="24e05-139">Například můžete spustit projekt s použitím MVC a snadno přidat stránky webových formulářů do projektu později nebo generování uživatelského rozhraní webových rozhraní API v projektu webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="24e05-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="24e05-140">One ASP.NET se točí kolem usnadnit vám jako vývojáři k provádění akcí, které jste si oblíbili v technologii ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="24e05-141">Bez ohledu na to, jakou technologii zvolíte budete moci spolehnout, že vytváříte na důvěryhodné základní architektury One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="24e05-142">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="24e05-142">New Web Project Experience</span></span>

<span data-ttu-id="24e05-143">Vylepšili jsme možnosti vytváření nových webových projektů v sadě Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="24e05-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="24e05-144">V **nový webový projekt ASP.NET** dialogového okna můžete vybrat typ projektu chcete, nakonfigurovat libovolnou kombinaci technologie (webové formuláře, MVC, webové rozhraní API), nakonfigurujte možnosti ověřování a přidejte projekt testu jednotek.</span><span class="sxs-lookup"><span data-stu-id="24e05-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![Nový projekt ASP.NET](release-notes/_static/image1.png)

<span data-ttu-id="24e05-146">Nové dialogové okno umožňuje změnit výchozí nastavení ověřování pro celou řadu šablon.</span><span class="sxs-lookup"><span data-stu-id="24e05-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="24e05-147">Například při vytváření projektu aplikace webových formulářů ASP.NET můžete vybrat některý z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="24e05-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="24e05-148">Bez ověřování</span><span class="sxs-lookup"><span data-stu-id="24e05-148">No Authentication</span></span>
- <span data-ttu-id="24e05-149">Jednotlivých uživatelských účtů (členství technologie ASP.NET nebo sociální zprostředkovatele přihlášení)</span><span class="sxs-lookup"><span data-stu-id="24e05-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="24e05-150">Účty organizace (Active Directory v aplikaci internet)</span><span class="sxs-lookup"><span data-stu-id="24e05-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="24e05-151">Ověřování Windows (Active Directory v intranetu aplikace)</span><span class="sxs-lookup"><span data-stu-id="24e05-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![Možnosti ověřování](release-notes/_static/image2.png)

<span data-ttu-id="24e05-153">Další informace o nový proces pro vytváření webových projektů, naleznete v tématu [vytváření webových projektů ASP.NET v sadě Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="24e05-154">Další informace o nových možnostech ověřování najdete v tématu [ASP.NET Identity](#TOC8) dále v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="24e05-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="24e05-155">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="24e05-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="24e05-156">ASP.NET generování uživatelského rozhraní je architektura generování kódu pro webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="24e05-157">To umožňuje snadno přidat do projektu, který komunikuje s datovým modelem často používaný kód.</span><span class="sxs-lookup"><span data-stu-id="24e05-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="24e05-158">V předchozích verzích sady Visual Studio generování uživatelského rozhraní omezovala na projekty ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="24e05-159">Pomocí sady Visual Studio 2013 můžete nyní používat generování uživatelského rozhraní pro libovolný projekt ASP.NET, včetně webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="24e05-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="24e05-160">Visual Studio 2013 pro projekt webových formulářů aktuálně nepodporuje generování stránek, ale můžete pořád používat generování uživatelského rozhraní s webovými formuláři tak, že přidáte k projektu závislosti MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="24e05-161">Podpora pro generování stránky pro webové formuláře bude přidána v budoucí aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="24e05-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="24e05-162">Při používání generování uživatelského rozhraní, zajišťujeme, že všechny požadované závislosti jsou nainstalovány v projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="24e05-163">Například pokud začínat projekt webových formulářů ASP.NET a poté použijte generování uživatelského rozhraní pro přidání Kontroleru webového rozhraní API, požadované balíčky NuGet a odkazy jsou přidány do projektu automaticky.</span><span class="sxs-lookup"><span data-stu-id="24e05-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="24e05-164">Chcete-li přidat generování uživatelského rozhraní MVC do projektu webových formulářů, přidejte **novou vygenerovanou položku** a vyberte **závislosti MVC 5** v dialogovém okně.</span><span class="sxs-lookup"><span data-stu-id="24e05-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="24e05-165">Existují dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a úplné.</span><span class="sxs-lookup"><span data-stu-id="24e05-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="24e05-166">Pokud vyberete minimální, pouze balíčky NuGet a odkazy pro architekturu ASP.NET MVC se přidají do vašeho projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="24e05-167">Pokud vyberete možnost Úplná minimální závislosti jsou přidány, a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="24e05-168">Podpora pro generování kontrolerů asynchronní používá nové asynchronní funkce z Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="24e05-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="24e05-169">Další informace a podrobné pokyny najdete v tématu [generování uživatelského rozhraní ASP.NET: Přehled](aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="24e05-170">Browser Link – SignalR kanál mezi prohlížečem a sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="24e05-171">Nové [Browser Link](using-browser-link.md) funkce vám umožní připojení více prohlížečů k sadě Visual Studio a aktualizovat všechny kliknutím na tlačítko na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="24e05-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="24e05-172">Můžete připojit více prohlížečů na váš web development, včetně mobilních emulátorů a klikněte na aktualizovat na Aktualizovat všechny prohlížeče všechny ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="24e05-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="24e05-173">Browser Link také poskytuje rozhraní API umožňuje vývojářům umožňuje psát rozšíření odkazů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="24e05-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="24e05-174">Tím, že umožňuje vývojářům využívat rozhraní API odkazů prohlížeče, bude možné vytvořit velmi pokročilé scénáře, které překročí hranice mezi Visual Studio a v jakémkoli prohlížeči, který je připojený.</span><span class="sxs-lookup"><span data-stu-id="24e05-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="24e05-175">Web Essentials využívá rozhraní API k vytvoření integrovaného prostředí mezi Visual Studio a prohlížeči vývojářských nástrojů, vzdálené řízení mobilních emulátorů a mnoho dalších.</span><span class="sxs-lookup"><span data-stu-id="24e05-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="24e05-176">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="24e05-177">Visual Studio 2013 obsahuje nové editoru HTML Razor soubory a soubory HTML ve webových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="24e05-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="24e05-178">Nový editor HTML obsahuje jedno jednotné schéma založených na HTML5.</span><span class="sxs-lookup"><span data-stu-id="24e05-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="24e05-179">Má uživatelské rozhraní jQuery automatické uzavírání závorek a AngularJS atribut technologie IntelliSense, atribut seskupení technologie IntelliSense, ID a název třídy technologie Intellisense a dalších vylepšení včetně lepší výkon, formátování a inteligentní značky.</span><span class="sxs-lookup"><span data-stu-id="24e05-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="24e05-180">Následující snímek obrazovky ukazuje, jak pomocí Bootstrap atribut technologie IntelliSense v editoru jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="24e05-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![Technologie IntelliSense v editoru HTML](release-notes/_static/image4.png)

<span data-ttu-id="24e05-182">Visual Studio 2013 také dodává s oběma CoffeeScript a méně editory součástí.</span><span class="sxs-lookup"><span data-stu-id="24e05-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="24e05-183">LESS editor pochází z šablon stylů CSS editor se skvělými funkcemi a má napříč všemi méně dokumenty v technologii Intellisense pro konkrétní proměnné a objekty mixin @import řetězce.</span><span class="sxs-lookup"><span data-stu-id="24e05-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="24e05-184">Podpora aplikací webové služby Azure App Service v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="24e05-185">Ve Visual Studiu 2013 pomocí sady Azure SDK for .NET 2.2, můžete použít **Průzkumníka serveru** pracovat přímo s vzdálené webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="24e05-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="24e05-186">Můžete se přihlásit ke svému účtu Azure vytvářet nové webové aplikace, konfigurace aplikací, zobrazit protokoly v reálném čase a další.</span><span class="sxs-lookup"><span data-stu-id="24e05-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="24e05-187">Vydáno odesílaných krátce po SDK 2.2, budete moct spustit v režimu ladění vzdáleně v Azure.</span><span class="sxs-lookup"><span data-stu-id="24e05-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="24e05-188">Většina nových funkcí pro Azure App Service Web Apps pracovat i v sadě Visual Studio 2012 při instalaci v aktuální verzi sady Azure SDK pro .NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="24e05-189">Další informace naleznete v následujících materiálech:</span><span class="sxs-lookup"><span data-stu-id="24e05-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="24e05-190">Vytvoření webové aplikace ASP.NET ve službě Azure App Service</span><span class="sxs-lookup"><span data-stu-id="24e05-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="24e05-191">Řešení potíží s webovou aplikací ve službě Azure App Service pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24e05-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="24e05-192">Vylepšení publikování webu</span><span class="sxs-lookup"><span data-stu-id="24e05-192">Web Publish Enhancements</span></span>

<span data-ttu-id="24e05-193">Visual Studio 2013 obsahuje nové a vylepšené funkce publikování webu.</span><span class="sxs-lookup"><span data-stu-id="24e05-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="24e05-194">Tady je několik z nich:</span><span class="sxs-lookup"><span data-stu-id="24e05-194">Here are a few of them:</span></span>

- <span data-ttu-id="24e05-195">Snadno [automatizovat šifrování souborů Web.config](https://go.microsoft.com/fwlink/?LinkId=325529).</span><span class="sxs-lookup"><span data-stu-id="24e05-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="24e05-196">(Tento odkaz a následující dva přejděte na dokumentaci na webu MSDN, které nemusí být k dispozici, dokud v den v 10/17.)</span><span class="sxs-lookup"><span data-stu-id="24e05-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="24e05-197">Snadno [automatizovat pořizování aplikace v režimu offline během nasazování](https://go.microsoft.com/fwlink/?LinkId=325530).</span><span class="sxs-lookup"><span data-stu-id="24e05-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="24e05-198">Nakonfigurujete nástroj nasazení webu na [nahrazujícím datum poslední změny kontrolního součtu souboru](https://go.microsoft.com/fwlink/?LinkId=325531) pro zjištění souborů, které mají být zkopírovány do serveru.</span><span class="sxs-lookup"><span data-stu-id="24e05-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="24e05-199">Pokud používáte FTP nebo systému souborů publikovat metody i s nasazením webu rychle publikujte jednotlivé vybrané soubory (včetně souboru Web.config).</span><span class="sxs-lookup"><span data-stu-id="24e05-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="24e05-200">Další informace o nasazení webu ASP.NET najdete v tématu [webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).</span><span class="sxs-lookup"><span data-stu-id="24e05-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="24e05-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="24e05-201">NuGet 2.7</span></span>

<span data-ttu-id="24e05-202">NuGet 2.7 zahrnuje bohatou sadu nových funkcí, které jsou popsány podrobně v [zpráva k vydání verze NuGet 2.7](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="24e05-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="24e05-203">Tato verze NuGet také odstraňuje nutnost poskytovat explicitní souhlas pro funkce obnovení balíčků NuGet stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="24e05-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="24e05-204">Souhlas (a související zaškrtávací políčko v dialogovém okně NuGet Předvolby) je nyní povoleno nainstalováním NuGet.</span><span class="sxs-lookup"><span data-stu-id="24e05-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="24e05-205">Obnovení balíčku teď jednoduše funguje ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="24e05-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="24e05-206">ASP.NET – webové formuláře</span><span class="sxs-lookup"><span data-stu-id="24e05-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="24e05-207">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-207">One ASP.NET</span></span>

<span data-ttu-id="24e05-208">Šablony projektů webových formulářů bez problémů integrovat nové prostředí One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="24e05-209">Můžete přidat MVC a webového rozhraní API podporují do projektu webové formuláře a nakonfigurujete ověřování pomocí Průvodce vytvořením projektu One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="24e05-210">Další informace najdete v tématu [vytváření webových projektů ASP.NET v sadě Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="24e05-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="24e05-211">ASP.NET Identity</span></span>

<span data-ttu-id="24e05-212">Šablony projektů webových formulářů podporují novou architekturu identit technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="24e05-213">Kromě toho šablony teď podporují vytváření intranetový projekt webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="24e05-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="24e05-214">Další informace najdete v tématu [metody ověřování](creating-web-projects-in-visual-studio.md#auth) v **vytváření webových projektů ASP.NET v sadě Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="24e05-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="24e05-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="24e05-215">Bootstrap</span></span>

<span data-ttu-id="24e05-216">Použití šablony webových formulářů [Bootstrap](http://twitter.github.io/bootstrap/) k poskytování elegantní a rychle reagující vzhled a chování, které můžete snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="24e05-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="24e05-217">Další informace najdete v tématu [Bootstrap v šablony webových projektů Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="24e05-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="24e05-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="24e05-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="24e05-219">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-219">One ASP.NET</span></span>

<span data-ttu-id="24e05-220">Šablon projektu Web MVC bez problémů integrovat nové prostředí One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="24e05-221">Můžete přizpůsobit projekt MVC a konfigurace ověřování pomocí Průvodce vytvořením projektu One ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="24e05-222">Úvodní kurz k ASP.NET MVC 5 najdete za [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="24e05-223">Informace o upgradu projektů MVC 4 do MVC 5 najdete v tématu [pokyny k upgradu ASP.NET MVC 4 a projektem webového rozhraní API technologie ASP.NET MVC 5 a webovým rozhraním API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="24e05-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="24e05-224">ASP.NET Identity</span></span>

<span data-ttu-id="24e05-225">Použití ASP.NET Identity pro ověřování a správě identit se aktualizovaly šablon projektu MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="24e05-226">Kurz ověřování Facebooku nebo Googlu a členství v nové rozhraní API najdete tady [vytvoření aplikace ASP.NET MVC 5 pomocí Facebooku a Google OAuth2 nebo OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) a [vytvoření aplikace ASP.NET MVC pomocí ověření a Databáze SQL a nasazení do služby Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="24e05-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="24e05-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="24e05-227">Bootstrap</span></span>

<span data-ttu-id="24e05-228">Šablona projektu MVC byl aktualizován na použití [Bootstrap](http://getbootstrap.com/) k poskytování elegantní a rychle reagující vzhled a chování, které můžete snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="24e05-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="24e05-229">Další informace najdete v tématu [Bootstrap v šablony webových projektů Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="24e05-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="24e05-230">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="24e05-230">Authentication filters</span></span>

<span data-ttu-id="24e05-231">Ověřovací filtry se nový typ filtru v architektuře ASP.NET MVC, která spustí před filtry autorizace v kanálu ASP.NET MVC a umožňují zadat ověřovací logiky akcích, na řadič, nebo globálně pro všechny řadiče.</span><span class="sxs-lookup"><span data-stu-id="24e05-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="24e05-232">Filtry ověřování zpracovat přihlašovací údaje v požadavku a zadejte odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="24e05-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="24e05-233">Filtry ověřování můžete také přidat výzev ověřování v reakci na neoprávněné požadavky.</span><span class="sxs-lookup"><span data-stu-id="24e05-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="24e05-234">Přepisy filtru</span><span class="sxs-lookup"><span data-stu-id="24e05-234">Filter overrides</span></span>

<span data-ttu-id="24e05-235">Nyní můžete přepsat, jaké filtry se použijí metody dané akce nebo kontroleru zadáním filtru přepsání.</span><span class="sxs-lookup"><span data-stu-id="24e05-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="24e05-236">Přepsání filtry zadat sadu typy filtrů, které by se neměl spouštět pro daný obor (akce nebo kontroleru).</span><span class="sxs-lookup"><span data-stu-id="24e05-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="24e05-237">To umožňuje konfigurovat filtry, které platí globálně, ale potom vyloučit určité globální filtry z použití na konkrétní akce nebo řadiče.</span><span class="sxs-lookup"><span data-stu-id="24e05-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="24e05-238">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="24e05-238">Attribute routing</span></span>

<span data-ttu-id="24e05-239">ASP.NET MVC teď podporuje směrování atributů, díky příspěvek podle Tim McCall, autora [ http://attributerouting.net ](http://attributerouting.net).</span><span class="sxs-lookup"><span data-stu-id="24e05-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="24e05-240">Se směrováním atributů můžete zadat trasy anotací akce a kontrolery.</span><span class="sxs-lookup"><span data-stu-id="24e05-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="24e05-241">Rozhraní API pro ASP.NET Web 2</span><span class="sxs-lookup"><span data-stu-id="24e05-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="24e05-242">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="24e05-242">Attribute routing</span></span>

<span data-ttu-id="24e05-243">Rozhraní ASP.NET Web API nyní podporuje směrování atributů, díky příspěvek podle Tim McCall, autora [ http://attributerouting.net ](http://attributerouting.net).</span><span class="sxs-lookup"><span data-stu-id="24e05-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="24e05-244">Se směrováním atributů můžete zadat trasy rozhraní Web API anotací akce a kontrolery takto:</span><span class="sxs-lookup"><span data-stu-id="24e05-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="24e05-245">Směrování atributů vám dává větší kontrolu nad identifikátory URI webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="24e05-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="24e05-246">Můžete například snadno definovat prostředek hierarchii pomocí jediného kontroleru rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="24e05-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="24e05-247">Směrování atributů také poskytuje pohodlné syntaxe pro zadání volitelné parametry, výchozí hodnoty a omezení trasy:</span><span class="sxs-lookup"><span data-stu-id="24e05-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="24e05-248">Další informace o směrování atributů najdete v tématu [směrováním atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="24e05-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="24e05-249">OAuth 2.0</span></span>

<span data-ttu-id="24e05-250">Šablony projektu webového rozhraní API a jednostránkové aplikace teď podporují ověřování pomocí OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="24e05-251">OAuth 2.0 je architektura určená k autorizaci přístupu klientů k chráněným prostředkům.</span><span class="sxs-lookup"><span data-stu-id="24e05-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="24e05-252">Funguje pro celou řadu klientů včetně prohlížečů a mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="24e05-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="24e05-253">Podpoře OAuth 2.0 je založená na nové middleware zabezpečení poskytované komponenty Microsoft OWIN pro ověřování nosiče a implementaci autorizace role serveru.</span><span class="sxs-lookup"><span data-stu-id="24e05-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="24e05-254">Případně klienti se můžou autorizovat pomocí organizační autorizační server, jako je Azure Active Directory nebo služby AD FS ve Windows serveru 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="24e05-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="24e05-255">Vylepšení protokolu OData</span><span class="sxs-lookup"><span data-stu-id="24e05-255">OData Improvements</span></span>

<span data-ttu-id="24e05-256">**Podpora pro $select $rozbalte $batch, $value a**</span><span class="sxs-lookup"><span data-stu-id="24e05-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="24e05-257">ASP.NET Web API OData má teď plnou podporu pro $select, rozbalte položku $ a $value.</span><span class="sxs-lookup"><span data-stu-id="24e05-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="24e05-258">Můžete také použít $batch pro žádost o dávkové zpracování a zpracování sad změn.</span><span class="sxs-lookup"><span data-stu-id="24e05-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="24e05-259">Možnosti $select a $$expand umožňují změnit tvar data, která je vrácena z koncového bodu OData.</span><span class="sxs-lookup"><span data-stu-id="24e05-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="24e05-260">Další informace najdete v tématu [Introducing $select a $expand rozbalte podpory v Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="24e05-261">**Vylepšená rozšiřitelnost**</span><span class="sxs-lookup"><span data-stu-id="24e05-261">**Improved extensibility**</span></span>

<span data-ttu-id="24e05-262">Formátovací moduly OData se teď rozšiřitelné.</span><span class="sxs-lookup"><span data-stu-id="24e05-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="24e05-263">Můžete přidat položku metadat Atom, podporuje pojmenované datového proudu a media link položek, přidání anotací instance a přizpůsobit způsob generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="24e05-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="24e05-264">**Typ bez podpory**</span><span class="sxs-lookup"><span data-stu-id="24e05-264">**Type-less support**</span></span>

<span data-ttu-id="24e05-265">Teď můžete vytvářet služby OData, aniž byste museli definovat typy CLR pro vaše typy entit.</span><span class="sxs-lookup"><span data-stu-id="24e05-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="24e05-266">Místo toho můžete své řadiče OData trvat nebo vrátit instanci **IEdmObject**, což jsou formátovací moduly OData můžeme serializovat a deserializovat.</span><span class="sxs-lookup"><span data-stu-id="24e05-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="24e05-267">**Znovu použít existující model**</span><span class="sxs-lookup"><span data-stu-id="24e05-267">**Reuse an existing model**</span></span>

<span data-ttu-id="24e05-268">Pokud již máte existující entity data model (EDM), můžete teď znovu použít ho přímo, namísto nutnosti vytvářet nové.</span><span class="sxs-lookup"><span data-stu-id="24e05-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="24e05-269">Například pokud používáte Entity Framework, můžete použít EDM, který vytváří EF za vás.</span><span class="sxs-lookup"><span data-stu-id="24e05-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="24e05-270">Žádost o dávkové zpracování</span><span class="sxs-lookup"><span data-stu-id="24e05-270">Request Batching</span></span>

<span data-ttu-id="24e05-271">Žádost o dávkové zpracování kombinuje několik operací do jednoho požadavku HTTP POST, snížit síťový provoz a poskytovat plynulejší méně přetížení uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="24e05-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="24e05-272">Rozhraní ASP.NET Web API nyní podporuje několik strategií pro dávkové zpracování požadavku:</span><span class="sxs-lookup"><span data-stu-id="24e05-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="24e05-273">Použijte koncový bod $batch služby OData.</span><span class="sxs-lookup"><span data-stu-id="24e05-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="24e05-274">Balíček několika požadavků do jednoho požadavku vícedílné zprávy standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="24e05-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="24e05-275">Používejte vlastní formát dávkování.</span><span class="sxs-lookup"><span data-stu-id="24e05-275">Use a custom batching format.</span></span>

<span data-ttu-id="24e05-276">Pokud chcete povolit žádosti o dávkové zpracování, jednoduše přidejte trasu s obslužnou rutinu dávkování do konfigurace webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="24e05-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="24e05-277">Můžete taky řídit, zda požadavky nebo provést postupně a v libovolném pořadí.</span><span class="sxs-lookup"><span data-stu-id="24e05-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="24e05-278">Přenosné ASP.NET Web API klienta</span><span class="sxs-lookup"><span data-stu-id="24e05-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="24e05-279">Klienta ASP.NET Web API nyní slouží k vytvoření knihovny tříd portable, které pracují mezi aplikacemi pro Windows Store a Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="24e05-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="24e05-280">Můžete také vytvořit přenosné formátovací moduly, které můžete sdílet mezi klientem a serverem.</span><span class="sxs-lookup"><span data-stu-id="24e05-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="24e05-281">Zlepšení testovatelnosti</span><span class="sxs-lookup"><span data-stu-id="24e05-281">Improved Testability</span></span>

<span data-ttu-id="24e05-282">Webové rozhraní API 2 je to mnohem jednodušší k jednotce pro vaše rozhraní API řadičů testu.</span><span class="sxs-lookup"><span data-stu-id="24e05-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="24e05-283">Stačí vytvořit instanci váš kontroler API s zprávy s požadavkem a konfiguraci a poté zavolejte metodu akce, kterou chcete testovat.</span><span class="sxs-lookup"><span data-stu-id="24e05-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="24e05-284">Je také snadné napodobení **UrlHelper** třídy pro metody akce, které provádějí generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="24e05-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="24e05-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="24e05-285">IHttpActionResult</span></span>

<span data-ttu-id="24e05-286">Teď můžete implementovat IHttpActionResult k zapouzdření výsledku metody akce vašeho webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="24e05-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="24e05-287">IHttpActionResult vrátil z metody akce webového rozhraní API provádí modulem runtime ASP.NET Web API pro vytvoření zprávy výsledné odpovědi.</span><span class="sxs-lookup"><span data-stu-id="24e05-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="24e05-288">IHttpActionResult mohou být vráceny všechny akce webového rozhraní API pro zjednodušení jednotky testování vaší implementace rozhraní Web API.</span><span class="sxs-lookup"><span data-stu-id="24e05-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="24e05-289">Pro usnadnění práce, jsou k dispozici několik implementací IHttpActionResult úprav, včetně výsledků pro vrácení konkrétní stavové kódy formátovaný obsah nebo obsah vyjedná odpovědi.</span><span class="sxs-lookup"><span data-stu-id="24e05-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="24e05-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="24e05-290">HttpRequestContext</span></span>

<span data-ttu-id="24e05-291">Nové **HttpRequestContext** sleduje jakýkoli stav, který se váže na žádost, ale není ihned k dispozici z požadavku.</span><span class="sxs-lookup"><span data-stu-id="24e05-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="24e05-292">Například můžete použít **HttpRequestContext** zobrazíte data trasy, která objekt přidružený k požadavku, klientského certifikátu **UrlHelper** a kořenový adresář virtuální cesty.</span><span class="sxs-lookup"><span data-stu-id="24e05-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="24e05-293">Můžete snadno vytvářet **HttpRequestContext** účely testování jednotky.</span><span class="sxs-lookup"><span data-stu-id="24e05-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="24e05-294">Protože objekt zabezpečení pro požadavek je naplněn s požadavkem, aniž byste museli spoléhat na **vlastnost Thread.CurrentPrincipal**, objekt zabezpečení je teď dostupná v průběhu životního cyklu požadavku i když je v kanálu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="24e05-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="24e05-295">CORS</span><span class="sxs-lookup"><span data-stu-id="24e05-295">CORS</span></span>

<span data-ttu-id="24e05-296">Díky Další skvělý příspěvek od společnosti Brock Allen ASP.NET teď plně podporuje různé žádost o sdílení zdroji (CORS).</span><span class="sxs-lookup"><span data-stu-id="24e05-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="24e05-297">Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu.</span><span class="sxs-lookup"><span data-stu-id="24e05-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="24e05-298">[CORS](http://www.w3.org/TR/cors/) je standard W3C, která umožňuje server zmírnit zásadu stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="24e05-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="24e05-299">Pomocí CORS, server explicitně můžou některé požadavky cross-origin zatímco jiné odmítnout.</span><span class="sxs-lookup"><span data-stu-id="24e05-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="24e05-300">Webové rozhraní API 2 nyní podporuje CORS, včetně automatické zpracování předběžných požadavků.</span><span class="sxs-lookup"><span data-stu-id="24e05-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="24e05-301">Další informace najdete v tématu [povolení žádostí nepůvodního zdroje v rozhraní ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="24e05-302">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="24e05-302">Authentication Filters</span></span>

<span data-ttu-id="24e05-303">Ověřovací filtry se nový typ filtru v rozhraní ASP.NET Web API, která spustí před filtry autorizace v kanálu rozhraní ASP.NET Web API a umožňují zadat ověřovací logiky akcích, na řadič, nebo globálně pro všechny řadiče.</span><span class="sxs-lookup"><span data-stu-id="24e05-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="24e05-304">Filtry ověřování zpracovat přihlašovací údaje v požadavku a zadejte odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="24e05-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="24e05-305">Filtry ověřování můžete také přidat výzev ověřování v reakci na neoprávněné požadavky.</span><span class="sxs-lookup"><span data-stu-id="24e05-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="24e05-306">Přepsání filtru</span><span class="sxs-lookup"><span data-stu-id="24e05-306">Filter Overrides</span></span>

<span data-ttu-id="24e05-307">Nyní můžete přepsat, jaké filtry se použijí metody dané akce nebo kontroleru, tak, že určíte filtru přepsání.</span><span class="sxs-lookup"><span data-stu-id="24e05-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="24e05-308">Přepsání filtry zadat sadu filtr typy, které by neměl spouštět pro daný obor (akce nebo kontroleru).</span><span class="sxs-lookup"><span data-stu-id="24e05-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="24e05-309">To umožňuje přidat globální filtry, ale pak vyloučit některé z určité akce nebo řadiče.</span><span class="sxs-lookup"><span data-stu-id="24e05-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="24e05-310">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-310">OWIN Integration</span></span>

<span data-ttu-id="24e05-311">Rozhraní ASP.NET Web API nyní plně podporuje OWIN a lze je spustit na žádném hostiteli podporující OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="24e05-312">Jsou zde také zahrnuty **HostAuthenticationFilter** , který poskytuje integraci se systémem ověřování OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="24e05-313">Díky integraci OWIN mohou samoobslužné hostování webového rozhraní API ve vašem vlastním procesu společně s další middleware OWIN, jako je například SignalR.</span><span class="sxs-lookup"><span data-stu-id="24e05-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="24e05-314">Další informace najdete v tématu [OWIN použití na webové rozhraní API ASP.NET Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="24e05-315">Funkce SignalR technologie ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="24e05-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="24e05-316">Následující části popisují funkce SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="24e05-317">Základem OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="24e05-318">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="24e05-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="24e05-319">Podpora víc domén</span><span class="sxs-lookup"><span data-stu-id="24e05-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="24e05-320">zařízení s iOS a Android podporují prostřednictvím MonoTouch a Monodroidu</span><span class="sxs-lookup"><span data-stu-id="24e05-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="24e05-321">Klient Portable .NET</span><span class="sxs-lookup"><span data-stu-id="24e05-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="24e05-322">Nový balíček pro hostování na vlastním serveru</span><span class="sxs-lookup"><span data-stu-id="24e05-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="24e05-323">Podpora serveru zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="24e05-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="24e05-324">Odebrat server podpory pro rozhraní .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="24e05-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="24e05-325">Odeslání zprávy do seznamu klienti a skupiny</span><span class="sxs-lookup"><span data-stu-id="24e05-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="24e05-326">Odesílání zprávy pro konkrétního uživatele</span><span class="sxs-lookup"><span data-stu-id="24e05-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="24e05-327">Lepší podporu pro zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="24e05-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="24e05-328">Jednodušší jednotky testování rozbočovače</span><span class="sxs-lookup"><span data-stu-id="24e05-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="24e05-329">Zpracování chyb JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="24e05-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="24e05-330">Příklad toho, jak upgradovat existující projekt 1.x do SignalR 2.0, naleznete v tématu [inovace knihovnou SignalR 1.x projektu](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="24e05-331">Základem OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-331">Built on OWIN</span></span>

<span data-ttu-id="24e05-332">Funkce SignalR 2.0 je sestavena zcela na [OWIN (Open Web Interface pro .NET)](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="24e05-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="24e05-333">Tato změna umožňuje procesu instalace pro funkci SignalR mnohem více konzistentní mezi aplikací SignalR webové hostována a v místním prostředí, ale má také požadovaný počet změn rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="24e05-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="24e05-334">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="24e05-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="24e05-335">Z důvodu kompatibility se standardy OWIN, tyto metody jsou přejmenované na `MapSignalR`.</span><span class="sxs-lookup"><span data-stu-id="24e05-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="24e05-336">`MapSignalR` volá se, bez parametrů se namapuje všechny rozbočovače (jako `MapHubs` nemá ve verzi 1.x); Chcete-li namapovat jednotlivé **PersistentConnection** objektů, zadejte jako parametr typu a přípona adresy URL pro připojení jako typ připojení první argument.</span><span class="sxs-lookup"><span data-stu-id="24e05-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="24e05-337">`MapSignalR` Metoda je volána v třídy pro spuštění Owin.</span><span class="sxs-lookup"><span data-stu-id="24e05-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="24e05-338">Visual Studio 2013 obsahuje nové šablony pro třídy pro spuštění Owin; Pokud chcete použít tuto šablonu, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="24e05-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="24e05-339">Klikněte pravým tlačítkem na projekt</span><span class="sxs-lookup"><span data-stu-id="24e05-339">Right-click on the project</span></span>
2. <span data-ttu-id="24e05-340">Vyberte **přidat**, **novou položku...**</span><span class="sxs-lookup"><span data-stu-id="24e05-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="24e05-341">Vyberte **třída Owin Startup**.</span><span class="sxs-lookup"><span data-stu-id="24e05-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="24e05-342">Pojmenujte novou třídu **Startup.cs**.</span><span class="sxs-lookup"><span data-stu-id="24e05-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="24e05-343">V **webovou aplikaci,** obsahující třídy Owin při spuštění `MapSignalR` metody se pak přidá do vaší Owin spouštění pomocí položky v uzlu nastavení aplikace v souboru Web.Config, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="24e05-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="24e05-344">V **aplikace v místním prostředí**, třída při spuštění se předá jako parametr typu `WebApp.Start` metody.</span><span class="sxs-lookup"><span data-stu-id="24e05-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="24e05-345">**Mapování centra a připojení v SignalR 1.x (ze souboru global aplikace ve webové aplikaci):**</span><span class="sxs-lookup"><span data-stu-id="24e05-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="24e05-346">**Mapování centra a připojení v SignalR 2.0 (ze souboru třída Owin Startup):**</span><span class="sxs-lookup"><span data-stu-id="24e05-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="24e05-347">V **aplikace v místním prostředí**, třída při spuštění se předá jako parametr typu pro `WebApp.Start` způsob, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="24e05-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="24e05-348">Podpora víc domén</span><span class="sxs-lookup"><span data-stu-id="24e05-348">Cross-Domain Support</span></span>

<span data-ttu-id="24e05-349">V knihovně SignalR 1.x různé požadavky na doménu se řídí jediného příznaku EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="24e05-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="24e05-350">Tento příznak řídí požadavky na JSONP a CORS.</span><span class="sxs-lookup"><span data-stu-id="24e05-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="24e05-351">Pro větší flexibilitu a podporu všech CORS je odebraná ze součásti serveru pro funkci SignalR (lients JavaScriptu dál normálně ho používat CORS Pokud se zjistí, jestli prohlížeč podporuje), a nové middlewaru OWIN, který byl zpřístupněn pro podporu těchto scénářů.</span><span class="sxs-lookup"><span data-stu-id="24e05-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript lients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="24e05-352">V systému SignalR 2.0, pokud JSONP se vyžaduje na straně klienta (pro podporu požadavků mezi doménami ve starších prohlížečích), ji budou muset být explicitně povoluje nastavením `EnableJSONP` na `HubConfiguration` objektu `true`, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="24e05-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="24e05-353">JSONP je standardně zakázaná, protože je to méně bezpečné než CORS.</span><span class="sxs-lookup"><span data-stu-id="24e05-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="24e05-354">Chcete-li přidat nový middlewarem CORS v SignalR 2.0, přidejte `Microsoft.Owin.Cors` knihovny do projektu a volejte `UseCors` před SignalR middleware, jak je znázorněno v následující části.</span><span class="sxs-lookup"><span data-stu-id="24e05-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="24e05-355">**Přidání do projektu Microsoft.Owin.Cors**: Pokud chcete nainstalovat tuto knihovnu, spusťte následující příkaz v konzole Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="24e05-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="24e05-356">Tento příkaz přidá 2.0.0 verzi balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="24e05-357">**Volání UseCors**</span><span class="sxs-lookup"><span data-stu-id="24e05-357">**Calling UseCors**</span></span>

<span data-ttu-id="24e05-358">Následující fragmenty kódu ukazují, jak implementovat připojení mezi doménami v knihovně SignalR 1.x a 2.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="24e05-359">**Implementace žádosti napříč doménami v knihovně SignalR 1.x (ze souboru global aplikace)**</span><span class="sxs-lookup"><span data-stu-id="24e05-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="24e05-360">**Implementace žádosti napříč doménami v SignalR 2.0 (ze souboru kódu C#)**</span><span class="sxs-lookup"><span data-stu-id="24e05-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="24e05-361">Následující kód ukazuje, jak povolit CORS a JSONP v projektu SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="24e05-362">Tento vzorový kód používá `Map` a `RunSignalR` místo `MapSignalR`, takže middlewarem CORS běží pouze pro funkci SignalR žádosti, které vyžadují podporu CORS (a nikoli pro veškerý provoz na cestě zadané v `MapSignalR`.) `Map` lze také použít pro veškerý middleware, který je potřeba spustit pro konkrétní předponu adresy URL, a nikoli pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="24e05-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="24e05-363">zařízení s iOS a Android podporují prostřednictvím MonoTouch a Monodroidu</span><span class="sxs-lookup"><span data-stu-id="24e05-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="24e05-364">Byla přidána podpora pro iOS a Android klienty, kteří používají MonoTouch a Monodroidu součásti ze [knihovna pro Xamarin](https://xamarin.com/).</span><span class="sxs-lookup"><span data-stu-id="24e05-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="24e05-365">Další informace o tom, jak je používat, naleznete v tématu [pomocí komponenty Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span><span class="sxs-lookup"><span data-stu-id="24e05-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="24e05-366">Tyto součásti vám bude k dispozici [Xamarin Store](https://store.xamarin.com/) při vydání verze SignalR RTW je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="24e05-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a> <span data-ttu-id="24e05-367">### Přenosné klienta .NET</span><span class="sxs-lookup"><span data-stu-id="24e05-367">### Portable .NET client</span></span>

<span data-ttu-id="24e05-368">Pro lepší usnadňují vývoj pro různé platformy, Silverlight, WinRT a klienti Windows Phone byly nahrazeny jednoho přenosné .NET klienta, který podporuje tyto platformy:</span><span class="sxs-lookup"><span data-stu-id="24e05-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="24e05-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="24e05-369">NET 4.5</span></span>
- <span data-ttu-id="24e05-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="24e05-370">Silverlight 5</span></span>
- <span data-ttu-id="24e05-371">WinRT (.NET pro aplikace Windows Store)</span><span class="sxs-lookup"><span data-stu-id="24e05-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="24e05-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="24e05-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="24e05-373">Nový balíček pro hostování na vlastním serveru</span><span class="sxs-lookup"><span data-stu-id="24e05-373">New Self-Host Package</span></span>

<span data-ttu-id="24e05-374">Teď je k balíčku NuGet, aby bylo snazší, abyste mohli začít s hostování na vlastním serveru knihovnou SignalR (SignalR aplikace, které jsou hostované v procesu nebo jiné aplikace, nikoli hostované na webovém serveru).</span><span class="sxs-lookup"><span data-stu-id="24e05-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="24e05-375">Upgrade projektu hostování na vlastním serveru integrované s knihovnou SignalR 1.x, odebrat balíček Microsoft.AspNet.SignalR.Owin a přidání Microsoft.AspNet.SignalR.SelfHost balíčku.</span><span class="sxs-lookup"><span data-stu-id="24e05-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="24e05-376">Další informace o zahájení práce s balíček hostování na vlastním serveru najdete v tématu [kurzu: SignalR v místním](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="24e05-377">Podpora serveru zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="24e05-377">Backward-compatible server support</span></span>

<span data-ttu-id="24e05-378">V předchozích verzích nástroje SignalR, verze balíčku SignalR v klientovi a serveru museli být identické.</span><span class="sxs-lookup"><span data-stu-id="24e05-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="24e05-379">Aby bylo možné podporovat tlustá klientské aplikace, které by bylo obtížné aktualizovat, SignalR 2.0 teď podporuje pomocí staršího klienta na novější verzi serveru.</span><span class="sxs-lookup"><span data-stu-id="24e05-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="24e05-380">**Poznámka: Funkce SignalR 2.0 nepodporuje serverů se staršími verzemi vytvořené pomocí nových klientů.**</span><span class="sxs-lookup"><span data-stu-id="24e05-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="24e05-381">Odebrat server podpory pro rozhraní .NET 4.0</span><span class="sxs-lookup"><span data-stu-id="24e05-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="24e05-382">Funkce SignalR 2.0 klesla podporu pro server vzájemná funkční spolupráce s .NET 4.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="24e05-383">Rozhraní .NET 4.5 musí být použit s knihovnou SignalR 2.0 servery.</span><span class="sxs-lookup"><span data-stu-id="24e05-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="24e05-384">Se stále vyžaduje .NET 4.0 klienta SignalR 2.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="24e05-385">Odeslání zprávy do seznamu klienti a skupiny</span><span class="sxs-lookup"><span data-stu-id="24e05-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="24e05-386">V systému SignalR 2.0 je možné odeslat zprávu pomocí seznamu klienta a ID skupin.</span><span class="sxs-lookup"><span data-stu-id="24e05-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="24e05-387">Následující fragmenty kódu ukazují, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="24e05-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="24e05-388">**Odeslání zprávy do seznamu klienti a skupiny pomocí PersistentConnection**</span><span class="sxs-lookup"><span data-stu-id="24e05-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="24e05-389">**Odeslání zprávy do seznamu klienti a skupiny pomocí centra**</span><span class="sxs-lookup"><span data-stu-id="24e05-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="24e05-390">Odesílání zprávy pro konkrétního uživatele</span><span class="sxs-lookup"><span data-stu-id="24e05-390">Sending a message to a specific user</span></span>

<span data-ttu-id="24e05-391">Tato funkce umožňuje uživatelům určit, co je ID uživatele IRequest přes nové rozhraní IUserIdProvider podle:</span><span class="sxs-lookup"><span data-stu-id="24e05-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="24e05-392">**Rozhraní IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="24e05-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="24e05-393">Ve výchozím nastavení bude implementace, která se používá jako uživatelské jméno uživatele IPrincipal.Identity.Name.</span><span class="sxs-lookup"><span data-stu-id="24e05-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="24e05-394">Rozbočovače budete moct posílat zprávy k těmto uživatelům přes nové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="24e05-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="24e05-395">**Pomocí Clients.User rozhraní API**</span><span class="sxs-lookup"><span data-stu-id="24e05-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="24e05-396">Lepší podporu pro zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="24e05-396">Better Error Handling Support</span></span>

<span data-ttu-id="24e05-397">Uživatelé teď můžou vyvolat **HubException** z jakékoli volání rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="24e05-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="24e05-398">Konstruktor třídy **HubException** přijímá řetězcovou zprávu a objekt dodatečné údaje o chybě.</span><span class="sxs-lookup"><span data-stu-id="24e05-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="24e05-399">SignalR bude automaticky serializovat výjimky a jejich odesílání do klienta ve kterém se použije k odmítnutí/převzetí služeb při volání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="24e05-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="24e05-400">**Zobrazit výjimkách centra podrobné** nastavení nemá žádný vliv na **HubException** odesílaných zpět do klienta, nebo Ne, jsou vždy odeslána.</span><span class="sxs-lookup"><span data-stu-id="24e05-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="24e05-401">**Ukázka, odesílání HubException klientovi kód na straně serveru**</span><span class="sxs-lookup"><span data-stu-id="24e05-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="24e05-402">**Kód jazyka JavaScript klienta demonstrace reakce na HubException odeslaných ze serveru**</span><span class="sxs-lookup"><span data-stu-id="24e05-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="24e05-403">**Klientský kód .NET demonstrace reakce na HubException odeslaných ze serveru**</span><span class="sxs-lookup"><span data-stu-id="24e05-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="24e05-404">Jednodušší jednotky testování rozbočovače</span><span class="sxs-lookup"><span data-stu-id="24e05-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="24e05-405">Funkce SignalR 2.0 obsahuje rozhraní volá `IHubCallerConnectionContext` v centrech, která usnadňuje vytvoření mock klienta u volání rozbočovače na straně.</span><span class="sxs-lookup"><span data-stu-id="24e05-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="24e05-406">Následující fragmenty kódu ukazují, toto rozhraní pomocí oblíbených testovacích postroje [xUnit.net](https://github.com/xunit/xunit) a [moq](https://code.google.com/p/moq/).</span><span class="sxs-lookup"><span data-stu-id="24e05-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="24e05-407">**Testování částí SignalR pomocí xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="24e05-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="24e05-408">**Testování částí SignalR pomocí moq**</span><span class="sxs-lookup"><span data-stu-id="24e05-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="24e05-409">Zpracování chyb JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="24e05-409">JavaScript error handling</span></span>

<span data-ttu-id="24e05-410">Všechny zpětná volání JavaScript zpracování chyb v SignalR 2.0 vrátí objekty jazyka JavaScript chyby namísto nezpracovaných řetězců.</span><span class="sxs-lookup"><span data-stu-id="24e05-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="24e05-411">To umožňuje SignalR bohatší informace do vaší obslužné rutiny chyb.</span><span class="sxs-lookup"><span data-stu-id="24e05-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="24e05-412">Vnitřní výjimka z můžete získat `source` vlastnost chyby.</span><span class="sxs-lookup"><span data-stu-id="24e05-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="24e05-413">**Klientský kód jazyka JavaScript, který zpracovává výjimku Start.Fail**</span><span class="sxs-lookup"><span data-stu-id="24e05-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="24e05-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="24e05-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="24e05-415">Nový systém členství technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="24e05-416">ASP.NET Identity je nový systém členství pro aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="24e05-417">ASP.NET Identity snadno integrovat data profilu uživatelská data aplikací.</span><span class="sxs-lookup"><span data-stu-id="24e05-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="24e05-418">ASP.NET Identity můžete také zvolte model trvalosti pro profily uživatelů ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="24e05-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="24e05-419">Data můžete ukládat v databázi serveru SQL Server nebo jiného úložiště dat, včetně datových úložišť typu NoSQL, jako jsou úložiště tabulek Azure.</span><span class="sxs-lookup"><span data-stu-id="24e05-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="24e05-420">Další informace najdete v tématu [jednotlivé uživatelské účty](creating-web-projects-in-visual-studio.md#indauth) v **vytváření webových projektů ASP.NET v sadě Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="24e05-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="24e05-421">Ověřování na základě deklarací</span><span class="sxs-lookup"><span data-stu-id="24e05-421">Claims-based authentication</span></span>

<span data-ttu-id="24e05-422">Technologie ASP.NET nyní podporuje ověřování nezaloženého na deklaracích, kde je identitu uživatele reprezentována jako sada deklarací z důvěryhodného vystavitele.</span><span class="sxs-lookup"><span data-stu-id="24e05-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="24e05-423">Uživatelé mohou být ověřené pomocí uživatelského jména a hesla, které jsou zachovány v databázi aplikace, nebo pomocí zprostředkovatelů sociálních identit (například: Microsoft účty, Facebook, Google, Twitter), nebo pomocí účty organizace prostřednictvím Azure Active Directory nebo Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="24e05-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="24e05-424">Integrace s Azure Active Directory a Windows Server Active Directory</span><span class="sxs-lookup"><span data-stu-id="24e05-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="24e05-425">Nyní můžete vytvořit projekty ASP.NET, které používají Azure Active Directory nebo Windows Server Active Directory (AD) pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="24e05-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="24e05-426">Další informace najdete v tématu [účty organizace](creating-web-projects-in-visual-studio.md#orgauth) v **vytváření webových projektů ASP.NET v sadě Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="24e05-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="24e05-427">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-427">OWIN Integration</span></span>

<span data-ttu-id="24e05-428">Ověřování pomocí technologie ASP.NET je teď podle middleware OWIN, který jde použít na všechny hostitele na bázi OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="24e05-429">Další informace o OWIN, naleznete na následujícím [komponenty Microsoft OWIN](#TOC7) oddílu.</span><span class="sxs-lookup"><span data-stu-id="24e05-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="24e05-430">Komponenty Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="24e05-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="24e05-431">[Otevřete Web Interface pro .NET](http://owin.org/) (OWIN) definuje abstrakce mezi .NET webové servery a webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="24e05-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="24e05-432">OWIN odpojí webové aplikace ze serveru, provedení hostitele nezávislá na webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="24e05-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="24e05-433">Můžete například hostování OWIN webové aplikace ve službě IIS nebo samoobslužné hostování ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="24e05-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="24e05-434">Změny zavedené v komponenty Microsoft OWIN (označované také jako projektu Katana) zahrnují nové součásti serveru a hostitele, nové pomocné knihovny a middleware a nový ověřovací middleware.</span><span class="sxs-lookup"><span data-stu-id="24e05-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="24e05-435">Další informace o OWIN a Katana najdete v tématu [co je nového v OWIN a Katana](../../../aspnet/overview/owin-and-katana/index.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="24e05-436">**Poznámka: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) aplikace nelze spustit v režimu classic služby IIS; musí být spuštěn v integrovaném režimu.**</span><span class="sxs-lookup"><span data-stu-id="24e05-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="24e05-437">**Poznámka: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) aplikace musí být spuštěn v režimu plné důvěryhodnosti.**</span><span class="sxs-lookup"><span data-stu-id="24e05-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="24e05-438">Nové servery a hostitele</span><span class="sxs-lookup"><span data-stu-id="24e05-438">New Servers and Hosts</span></span>

<span data-ttu-id="24e05-439">V této vydané verzi byly přidány nové komponenty aby se povolily scénáře hostování na vlastním serveru.</span><span class="sxs-lookup"><span data-stu-id="24e05-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="24e05-440">Mezi tyto komponenty patří následující balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="24e05-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="24e05-441">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="24e05-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="24e05-442">Poskytuje serveru OWIN, který používá **HttpListener** pro naslouchání požadavků protokolu HTTP a směrují je do kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="24e05-443">**Microsoft.Owin.Hosting** poskytuje knihovnu pro vývojáře, kteří chtějí samoobslužné hostování ve vlastním procesu, jako je například konzolové aplikace nebo služba Windows kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="24e05-444">**OwinHost**.</span><span class="sxs-lookup"><span data-stu-id="24e05-444">**OwinHost**.</span></span> <span data-ttu-id="24e05-445">Poskytuje samostatný spustitelný soubor, který obtéká `Microsoft.Owin.Hosting` a umožňuje hostování na vlastním serveru kanál OWIN bez nutnosti psát vlastní hostitelskou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="24e05-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="24e05-446">Kromě toho `Microsoft.Owin.Host.SystemWeb` balíček nyní umožňuje middlewaru, který má poskytnout nápovědu pro **SystemWeb** server označující, že by měla být volána middleware fázi konkrétní kanálu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="24e05-447">Tato funkce je zvláště užitečná pro middleware ověřování, které by měly být spuštěny již v rané fázi kanálu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24e05-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="24e05-448">Pomocné rutiny knihovny a Middleware</span><span class="sxs-lookup"><span data-stu-id="24e05-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="24e05-449">I když můžete napsat komponenty OWIN používat pouze funkce a typ definice z specifikace OWIN nové `Microsoft.Owin` balíček poskytuje sadu abstrakce přívětivější.</span><span class="sxs-lookup"><span data-stu-id="24e05-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="24e05-450">Tento balíček kombinuje několik starších balíčků (například `Owin.Extensions`, `Owin.Types`) do jednoho, strukturované objektový model, který může potom snadno využívat jiné komponenty OWIN.</span><span class="sxs-lookup"><span data-stu-id="24e05-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="24e05-451">Ve skutečnosti většinou komponenty Microsoft OWIN nyní tento balíček použít.</span><span class="sxs-lookup"><span data-stu-id="24e05-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="24e05-452">[OWIN](http://www.owin.org) aplikace nelze spustit v režimu classic služby IIS; musí být spuštěn v integrovaném režimu.</span><span class="sxs-lookup"><span data-stu-id="24e05-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="24e05-453">[OWIN](http://www.owin.org) aplikace musí být spuštěn v režimu plné důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="24e05-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="24e05-454">Tato verze rovněž obsahuje Microsoft.Owin.Diagnostics balíček, který zahrnuje middleware pro ověření běžící aplikaci OWIN a middleware chybovou stránku umožňující vyšetřování chyb.</span><span class="sxs-lookup"><span data-stu-id="24e05-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="24e05-455">Ověření součásti</span><span class="sxs-lookup"><span data-stu-id="24e05-455">Authentication Components</span></span>

<span data-ttu-id="24e05-456">Následující komponenty ověřování jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="24e05-456">The following authentication components are available.</span></span>

- <span data-ttu-id="24e05-457">**Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="24e05-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="24e05-458">Umožňuje ověřování pomocí místní nebo cloudové adresářové služby.</span><span class="sxs-lookup"><span data-stu-id="24e05-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="24e05-459">**Microsoft.Owin.Security.Cookies** umožňuje ověřování pomocí souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="24e05-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="24e05-460">Tento balíček se dříve nazýval `Microsoft.Owin.Security.Forms`.</span><span class="sxs-lookup"><span data-stu-id="24e05-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="24e05-461">**Microsoft.Owin.Security.Facebook** umožňuje ověřování pomocí služeb na základě OAuth pro Facebook.</span><span class="sxs-lookup"><span data-stu-id="24e05-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="24e05-462">**Microsoft.Owin.Security.Google** umožňuje ověřování pomocí služby Google OpenID založené.</span><span class="sxs-lookup"><span data-stu-id="24e05-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="24e05-463">**Microsoft.Owin.Security.Jwt** umožňuje ověřování pomocí tokenů JWT.</span><span class="sxs-lookup"><span data-stu-id="24e05-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="24e05-464">**Microsoft.Owin.Security.MicrosoftAccount** umožňuje ověřování používá účty Microsoft.</span><span class="sxs-lookup"><span data-stu-id="24e05-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="24e05-465">**Microsoft.Owin.Security.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="24e05-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="24e05-466">Poskytuje serveru ověřování OAuth, jakož i middleware pro ověřování nosných tokenů.</span><span class="sxs-lookup"><span data-stu-id="24e05-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="24e05-467">**Microsoft.Owin.Security.Twitter** umožňuje ověřování pomocí služeb na základě OAuth pro Twitter.</span><span class="sxs-lookup"><span data-stu-id="24e05-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="24e05-468">Tato verze rovněž obsahuje `Microsoft.Owin.Cors` balíček, který obsahuje middleware pro zpracování požadavků HTTP mezi zdroji.</span><span class="sxs-lookup"><span data-stu-id="24e05-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="24e05-469">V konečné verzi sady Visual Studio 2013 byla odebrána podpora k podepisování tokenů JWT.</span><span class="sxs-lookup"><span data-stu-id="24e05-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="24e05-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="24e05-470">Entity Framework 6</span></span>

<span data-ttu-id="24e05-471">Seznam nových funkcí a další změny v Entity Framework 6 najdete v tématu [historie verzí Entity Framework](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="24e05-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="24e05-472">Syntaxe Razor rozhraní ASP.NET 3</span><span class="sxs-lookup"><span data-stu-id="24e05-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="24e05-473">Syntaxe Razor rozhraní ASP.NET 3 obsahuje následující nové funkce:</span><span class="sxs-lookup"><span data-stu-id="24e05-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="24e05-474">Podpora pro úpravy karty.</span><span class="sxs-lookup"><span data-stu-id="24e05-474">Support for Tab editing.</span></span> <span data-ttu-id="24e05-475">Dříve **formátovat dokument** příkazu, Automatické odsazení a automatické formátování v sadě Visual Studio nefungovala správně při použití **zachovat tabulátory** možnost.</span><span class="sxs-lookup"><span data-stu-id="24e05-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="24e05-476">Tato změna opravuje formátování kódu Razor pro kartu formátování pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24e05-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="24e05-477">Podporu pravidel přepisování adres URL při generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="24e05-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="24e05-478">Odebrání transparentní atribut zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="24e05-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="24e05-479">K zásadní změně a díky Razor 3 nekompatibilní pomocí MVC4 a starší, zatímco Razor 2 není kompatibilní s MVC5 nebo sestavení, proti MVC5.</span><span class="sxs-lookup"><span data-stu-id="24e05-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="24e05-480">Můžete najít Razor 3 opravených chybách v sadě Visual Studio 2013 z předběžných verzí [tady](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="24e05-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="24e05-481">Pozastavení aplikace technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e05-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="24e05-482">Pozastavení aplikace technologie ASP.NET je funkce mění pravidla hry v rozhraní .NET Framework 4.5.1, podstatně změní uživatelské prostředí a ekonomický model pro hostování velký počet webů ASP.NET na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="24e05-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="24e05-483">Další informace najdete v tématu [pozastavení aplikace technologie ASP.NET – responzivní sdílené hostování webů .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e05-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="24e05-484">Známé problémy a změny způsobující chyby</span><span class="sxs-lookup"><span data-stu-id="24e05-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="24e05-485">Tato část popisuje známé problémy a novinkách v ASP.NET and Web Tools pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="24e05-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="24e05-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="24e05-486">NuGet</span></span>

- <span data-ttu-id="24e05-487">[Nový balíček obnovení nebude fungovat v Mono, při použití souboru SLN](https://nuget.codeplex.com/workitem/3596) – bude opravený v nadcházející nuget.exe stahování a [NuGet.CommandLine balíčku](http://www.nuget.org/packages/NuGet.CommandLine/) aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="24e05-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="24e05-488">[Nové obnovení balíčků nefunguje s projekty Wix](https://nuget.codeplex.com/workitem/3598) – bude opravený v nadcházející nuget.exe stahování a [NuGet.CommandLine balíčku](http://www.nuget.org/packages/NuGet.CommandLine/) aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="24e05-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="24e05-489">[Automatické obnovení balíčku nebude fungovat pro projekty v rámci složky řešení](https://nuget.codeplex.com/workitem/3625) – bude opravený v NuGet 2.8.</span><span class="sxs-lookup"><span data-stu-id="24e05-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="24e05-490">Rozhraní API pro ASP.NET Web</span><span class="sxs-lookup"><span data-stu-id="24e05-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="24e05-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` nevrací `IQueryable<T>` vždy, protože jsme přidali podporu pro `$select` a `$expand`.</span><span class="sxs-lookup"><span data-stu-id="24e05-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="24e05-492">Naše starší ukázky pro `ODataQueryOptions<T>` vždy zasazena návratová hodnota z `ApplyTo` k `IQueryable<T>`.</span><span class="sxs-lookup"><span data-stu-id="24e05-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="24e05-493">To dříve pracoval, protože možnosti dotazu, pro které podporujeme dříve (`$filter`, `$orderby`, `$skip`, `$top`) nedojde ke změně tvaru dotazu.</span><span class="sxs-lookup"><span data-stu-id="24e05-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="24e05-494">Teď podporujeme `$select` a `$expand` návratovou hodnotu z `ApplyTo` nebudou `IQueryable<T>` vždy.</span><span class="sxs-lookup"><span data-stu-id="24e05-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="24e05-495">Pokud použijete ukázkový kód z dříve, pokud klient nezasílal bude dál pracovní `$select` a `$expand`.</span><span class="sxs-lookup"><span data-stu-id="24e05-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="24e05-496">Nicméně pokud chcete podporovat `$select` a `$expand` budete muset změnit na to, že kód.</span><span class="sxs-lookup"><span data-stu-id="24e05-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="24e05-497">**Request.Url nebo RequestContext.Url má hodnotu null během žádosti o služby batch**</span><span class="sxs-lookup"><span data-stu-id="24e05-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="24e05-498">Ve scénáři dávkování **UrlHelper** má hodnotu null při přístupu z **Request.Url** nebo **RequestContext.Url**.</span><span class="sxs-lookup"><span data-stu-id="24e05-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="24e05-499">Tento problém je aktuálně sledovat tady: [Má hodnotu null pro dávkové zpracování požadavku BatchRequestContext.Url](http://aspnetwebstack.codeplex.com/workitem/1301).</span><span class="sxs-lookup"><span data-stu-id="24e05-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="24e05-500">Alternativní řešení je vytvořit novou instanci třídy **UrlHelper**, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="24e05-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="24e05-501">**Vytvoření nové instance UrlHelper**</span><span class="sxs-lookup"><span data-stu-id="24e05-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="24e05-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="24e05-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="24e05-503">Při použití MVC5 a OrgAuth, pokud máte zobrazení, které provést ověření AntiForgerToken, můžete narazit na následující chybu při odesílání dat do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="24e05-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="24e05-504">**Chyba**:</span><span class="sxs-lookup"><span data-stu-id="24e05-504">**Error**:</span></span>

    <span data-ttu-id="24e05-505">*Chyba serveru v aplikaci '/'.*</span><span class="sxs-lookup"><span data-stu-id="24e05-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="24e05-506"><em>Deklarace typu "<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'nebo'<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>" není k dispozici na zadaný objekt ClaimsIdentity. Povolení podpory tokenů proti padělání pomocí ověřování nezaloženého na deklaracích, zkontrolujte, zda nakonfigurované zprostředkovatele je poskytování obě tyto deklarace identity ClaimsIdentity instancí, který generuje. Pokud zprostředkovatele deklarací identity nakonfigurovaný místo toho používá jiný typ deklarací jako jedinečný identifikátor, můžete nakonfigurovat tak, že nastavíte vlastnost statické AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span><span class="sxs-lookup"><span data-stu-id="24e05-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="24e05-507">**Alternativní řešení**:</span><span class="sxs-lookup"><span data-stu-id="24e05-507">**Workaround**:</span></span>

    <span data-ttu-id="24e05-508">Přidejte následující řádek v souboru Global.asax to opravit:</span><span class="sxs-lookup"><span data-stu-id="24e05-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="24e05-509">Tato chyba bude opravena pro další verzi.</span><span class="sxs-lookup"><span data-stu-id="24e05-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="24e05-510">Po provedení upgradu aplikace MVC4 pro MVC5, sestavte řešení a spusťte jej.</span><span class="sxs-lookup"><span data-stu-id="24e05-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="24e05-511">Zobrazí se následující chyba:</span><span class="sxs-lookup"><span data-stu-id="24e05-511">You should see the following error:</span></span>

    <span data-ttu-id="24e05-512">[A] System.Web.WebPages.Razor.Configuration.HostSection nelze přetypovat na [B]System.Web.WebPages.Razor.Configuration.HostSection.</span><span class="sxs-lookup"><span data-stu-id="24e05-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="24e05-513">Typu A mohou být "System.Web.WebPages.Razor, verze = 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35" v kontextu "Default" v umístění "C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\ V4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll ".</span><span class="sxs-lookup"><span data-stu-id="24e05-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="24e05-514">Typ B pochází z "System.Web.WebPages.Razor, verze = 3.0.0.0, jazyková verze = neutral, PublicKeyToken = 31bf3856ad364e35" v kontextu "Default" v umístění ' Files\root\6d05bbd0\ C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary technologie ASP.NET e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll ".</span><span class="sxs-lookup"><span data-stu-id="24e05-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="24e05-515">Chcete-li výše uvedené chybu opravit, otevřete *všechny* souborů Web.config (včetně těch v zobrazení složky) v projektu a proveďte následující:</span><span class="sxs-lookup"><span data-stu-id="24e05-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="24e05-516">Aktualizujte všechny výskyty "System.Web.Mvc" verze "4.0.0.0" "5.0.0.0".</span><span class="sxs-lookup"><span data-stu-id="24e05-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="24e05-517">Aktualizovat všechny výskyty verzi "System.Web.Helpers", "2.0.0.0" &quot;System.Web.WebPages&quot; a &quot;System.Web.WebPages.Razor&quot; na "3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="24e05-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="24e05-518">Například po provedení výše uvedené změny vazeb sestavení by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="24e05-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="24e05-519">Informace o upgradu projektů MVC 4 do MVC 5 najdete v tématu [pokyny k upgradu ASP.NET MVC 4 a projektem webového rozhraní API technologie ASP.NET MVC 5 a webovým rozhraním API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="24e05-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="24e05-520">Při použití ověřování na straně klienta s jQuery Nerušivý ověření, je někdy zprávu ověření pro element input HTML s typem = 'number'.</span><span class="sxs-lookup"><span data-stu-id="24e05-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="24e05-521">Chyba ověřování pro povinnou hodnotu ("The Age pole je povinné") se zobrazí kdy je zadáno neplatné číslo místo správnou zprávu, že je požadováno platné číslo.</span><span class="sxs-lookup"><span data-stu-id="24e05-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="24e05-522">Tento problém se běžně vyskytují se automaticky generovaný kód pro model s celočíselnou vlastnost pro zobrazení vytvořit a upravit.</span><span class="sxs-lookup"><span data-stu-id="24e05-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="24e05-523">Chcete-li tento problém obejít, změňte pomocný editor ze:</span><span class="sxs-lookup"><span data-stu-id="24e05-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="24e05-524">Do:</span><span class="sxs-lookup"><span data-stu-id="24e05-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="24e05-525">ASP.NET MVC 5 se už nepodporuje částečným vztahem důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="24e05-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="24e05-526">Projekty propojení na binární soubory MVC nebo WebAPI by měla být odstraněna [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) atribut a [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) atribut.</span><span class="sxs-lookup"><span data-stu-id="24e05-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="24e05-527">Odebírání těchto atributů dojde k odstranění chyby kompilátoru, jako je následující.</span><span class="sxs-lookup"><span data-stu-id="24e05-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="24e05-528">Všimněte si, jak vedlejším účinkem této je nelze použít 4.0 a 5.0 sestavení ve stejné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="24e05-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="24e05-529">Budete muset aktualizovat všechny z nich 5.0.</span><span class="sxs-lookup"><span data-stu-id="24e05-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="24e05-530">Jednostránková aplikace šablony s autorizací služby Facebook může způsobit nestabilitu v Internet Exploreru, zatímco je hostovaný na webu do zóny sítě intranet</span><span class="sxs-lookup"><span data-stu-id="24e05-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="24e05-531">Šablona SPA poskytuje externí Přihlaste se pomocí Facebooku.</span><span class="sxs-lookup"><span data-stu-id="24e05-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="24e05-532">Když projekt vytvořen pomocí šablony běží místně, může způsobit podepisování se v Internet Exploreru k chybě.</span><span class="sxs-lookup"><span data-stu-id="24e05-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="24e05-533">Řešení:</span><span class="sxs-lookup"><span data-stu-id="24e05-533">Solution:</span></span>

1. <span data-ttu-id="24e05-534">Hostování webu v Internetové zóně; nebo</span><span class="sxs-lookup"><span data-stu-id="24e05-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="24e05-535">Otestování tohoto scénáře v prohlížeči než Internet Exploreru.</span><span class="sxs-lookup"><span data-stu-id="24e05-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="24e05-536">Webové formuláře, generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="24e05-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="24e05-537">Webové formuláře generování uživatelského rozhraní se odebral z VS2013 a bude k dispozici v budoucí aktualizaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24e05-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="24e05-538">Generování uživatelského rozhraní v rámci projektu webových formulářů však můžete použít přidáním závislosti MVC a generování generování uživatelského rozhraní pro MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="24e05-539">Váš projekt bude obsahovat kombinaci webových formulářů a MVC.</span><span class="sxs-lookup"><span data-stu-id="24e05-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="24e05-540">Přidat do projektu webových formulářů MVC, přidejte nová vygenerovaná položka a vyberte **závislosti MVC 5**.</span><span class="sxs-lookup"><span data-stu-id="24e05-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="24e05-541">Vyberte minimální nebo úplné v závislosti na tom, jestli budete potřebovat všechny soubory obsahu, jako jsou skripty.</span><span class="sxs-lookup"><span data-stu-id="24e05-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="24e05-542">Potom přidání vygenerované položky pro MVC, který vytvoří zobrazení a kontroler ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="24e05-543">MVC a generování rozhraní Web API – HTTP 404, nebyla nalezena chyba</span><span class="sxs-lookup"><span data-stu-id="24e05-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="24e05-544">Pokud dojde k chybě při přidání vygenerované položky do projektu, je možné, že váš projekt bude ponechána v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="24e05-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="24e05-545">Některé změny se generování uživatelského rozhraní bude vrácena zpět, ale jiné změny, jako je například nainstalované balíčky NuGet, nebude vrácena zpět.</span><span class="sxs-lookup"><span data-stu-id="24e05-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="24e05-546">Pokud se vrátí zpět změny konfigurace směrování, uživatelům se zobrazí chyba HTTP 404 při přechodu na automaticky generovaný položky.</span><span class="sxs-lookup"><span data-stu-id="24e05-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="24e05-547">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="24e05-547">Workaround:</span></span>

- <span data-ttu-id="24e05-548">Chcete-li vyřešit tuto chybu pro MVC, přidejte nová vygenerovaná položka a vybrat závislosti MVC 5 (minimální nebo úplná).</span><span class="sxs-lookup"><span data-stu-id="24e05-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="24e05-549">Tento proces se všechny požadované změny, přidejte do projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="24e05-550">Chcete-li vyřešit tuto chybu pro webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="24e05-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="24e05-551">Přidání třídy WebApiConfig do projektu.</span><span class="sxs-lookup"><span data-stu-id="24e05-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="24e05-552">V aplikaci nakonfigurovat WebApiConfig.Register\_začátek metody v souboru Global.asax následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="24e05-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
