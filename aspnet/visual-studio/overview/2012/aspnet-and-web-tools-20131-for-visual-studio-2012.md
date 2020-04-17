---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543571"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="d9bf7-103">Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d9bf7-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="d9bf7-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d9bf7-105">Tento dokument popisuje vydání ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="d9bf7-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="d9bf7-106">Contents</span></span>

- [<span data-ttu-id="d9bf7-107">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="d9bf7-108">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="d9bf7-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="d9bf7-109">Nové funkce v ASP.NET a webových nástrojích 2013.1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d9bf7-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="d9bf7-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d9bf7-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="d9bf7-111">Šablony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="d9bf7-112">ASP.NET šablonu MVC 5</span><span class="sxs-lookup"><span data-stu-id="d9bf7-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="d9bf7-113">šablona ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="d9bf7-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="d9bf7-114">Šablony položek</span><span class="sxs-lookup"><span data-stu-id="d9bf7-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="d9bf7-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d9bf7-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="d9bf7-116">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="d9bf7-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="d9bf7-117">Editor břitvy</span><span class="sxs-lookup"><span data-stu-id="d9bf7-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="d9bf7-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d9bf7-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="d9bf7-119">Známé problémy a nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="d9bf7-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="d9bf7-120">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="d9bf7-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="d9bf7-121">MVC a webové api lešení - HTTP 404, nebyla nalezena chyba</span><span class="sxs-lookup"><span data-stu-id="d9bf7-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="d9bf7-122">Visual Studio Express 2012 pro web přestane fungovat po přidání položky sádlo</span><span class="sxs-lookup"><span data-stu-id="d9bf7-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="d9bf7-123">ASP.NET Břitva 3</span><span class="sxs-lookup"><span data-stu-id="d9bf7-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="d9bf7-124">Zobrazení souboru cshtml pomocí funkce Procházet pomocí nebo F5 způsobí chybu serveru</span><span class="sxs-lookup"><span data-stu-id="d9bf7-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="d9bf7-125">Url Přepsat a tilde (~)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="d9bf7-126">Šablony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="d9bf7-127">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-127">Installation Notes</span></span>

<span data-ttu-id="d9bf7-128">[Instalace](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="d9bf7-129">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="d9bf7-129">Software Requirements</span></span>

<span data-ttu-id="d9bf7-130">Musíte mít visual studio 2012 nebo Visual Studio Express 2012 pro web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="d9bf7-131">Nové funkce v ASP.NET a webových nástrojích 2013.1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d9bf7-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="d9bf7-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d9bf7-132">Bootstrap</span></span>

<span data-ttu-id="d9bf7-133">Při přichycení mvc 5 řadiče a zobrazení, značky pro zobrazení používá [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="d9bf7-134">Šablony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="d9bf7-135">ASP.NET šablonu MVC 5</span><span class="sxs-lookup"><span data-stu-id="d9bf7-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="d9bf7-136">Přidali jsme novou šablonu MVC 5.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="d9bf7-137">Odkazuje na nejnovější balíčky MVC 5 NuGet a můžete použít přisycování uživatelského přilnavého zařízení k přidání řadičů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="d9bf7-138">šablona ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="d9bf7-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="d9bf7-139">Přidali jsme novou šablonu Webové ho rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="d9bf7-140">Odkazuje na nejnovější webové api 2 NuGet balíčky a můžete použít veslací lišty přidat řadiče a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="d9bf7-141">Šablony položek</span><span class="sxs-lookup"><span data-stu-id="d9bf7-141">Item Templates</span></span>

<span data-ttu-id="d9bf7-142">Přidali jsme nové šablony položek pro zobrazení MVC 5, webové stránky (Razor 3) a řadiče Web API 2.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="d9bf7-143">Instalují související balíčky NuGet do projektu při přidávání nových položek.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="d9bf7-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d9bf7-144">Entity Framework 6</span></span>

<span data-ttu-id="d9bf7-145">Když přistarém ovladači MVC nebo webového rozhraní API pomocí entity Framework, používáme Framework 6.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="d9bf7-146">Další informace o rozhraní Entity Framework naleznete v [historii verzí entity frameworku](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="d9bf7-147">Můžete také stáhnout a nainstalovat entity Framework 6 Nástroje pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="d9bf7-148">Viz [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="d9bf7-149">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="d9bf7-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="d9bf7-150">ASP.NET generování uživatelského rozhraní je rozhraní pro generování kódu pro ASP.NET webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="d9bf7-151">Usnadňuje přidání často používaný kód do projektu, který spolupracuje s datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="d9bf7-152">V předchozích verzích sady Visual Studio bylo lešení omezeno na ASP.NET projekty MVC.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="d9bf7-153">Pomocí této aktualizace můžete nyní používat zasanácí číslo pro všechny ASP.NET projektu, včetně webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="d9bf7-154">Tato aktualizace nepodporuje generování stránek pro projekt webových formulářů, ale můžete stále používat generování uživatelského formuláře s webovými formuláři přidáním závislostí MVC do projektu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="d9bf7-155">Podpora generování stránek pro webové formuláře bude přidána v budoucí aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="d9bf7-156">Při použití uživatelského přilechrápění zajišťujeme, že jsou v projektu nainstalovány všechny požadované závislosti.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="d9bf7-157">Pokud například začnete s projektem ASP.NET webových formulářů a potom pomocí uživatelského rozhraní přidáte řadič webového rozhraní API, budou do projektu automaticky přidány požadované balíčky nuget a odkazy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="d9bf7-158">Chcete-li přidat uživatelské rozhraní MVC do projektu webových formulářů, přidejte **novou položku scaffolded a** v dialogovém okně vyberte **závislosti MVC 5.**</span><span class="sxs-lookup"><span data-stu-id="d9bf7-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="d9bf7-159">Existují dvě možnosti pro lešení MVC; Minimální a plná.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="d9bf7-160">Pokud vyberete Minimální, do projektu se přidají pouze balíčky NuGet a odkazy pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="d9bf7-161">Pokud vyberete možnost Úplné, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="d9bf7-162">Podpora asynchronních řadičů lešení používá nové asynchronní funkce z entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="d9bf7-163">Další informace a kurzy naleznete [v tématu ASP.NET Přehled lešení](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="d9bf7-164">Tyto kurzy ukazují veselení s Visual Studio 2013, ale jsou také použitelné pro ASP.NET a webových nástrojů 2013.1 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="d9bf7-165">Editor břitvy</span><span class="sxs-lookup"><span data-stu-id="d9bf7-165">Razor Editor</span></span>

<span data-ttu-id="d9bf7-166">S touto aktualizací visual studio 2012 nyní podporuje nástroje a úpravy Razor 3.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="d9bf7-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d9bf7-167">NuGet 2.7</span></span>

<span data-ttu-id="d9bf7-168">NuGet 2.7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány na [NuGet 2.7 Poznámky k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="d9bf7-169">Tato verze NuGet odstraňuje potřebu pro uživatele explicitně povolit NuGet obnovit chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="d9bf7-170">Při instalaci NuGet 2.7 uživatelé implicitně souhlas k automatickému obnovení chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="d9bf7-171">Uživatelé mohou explicitně odhlásit obnovení balíčku prostřednictvím nastavení NuGet v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="d9bf7-172">Tato změna zjednodušuje fungování obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="d9bf7-173">Známé problémy a nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="d9bf7-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="d9bf7-174">ASP.NET lešení</span><span class="sxs-lookup"><span data-stu-id="d9bf7-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="d9bf7-175">MVC a webové api lešení - HTTP 404, nebyla nalezena chyba</span><span class="sxs-lookup"><span data-stu-id="d9bf7-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="d9bf7-176">Pokud při přidávání šástavla dojde k chybě, je možné, že projekt zůstane v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="d9bf7-177">Některé provedené změny se šaše budou vráceny zpět, ale jiné změny, jako jsou například nainstalované balíčky NuGet, nebudou vráceny zpět.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="d9bf7-178">Pokud jsou změny konfigurace směrování vráceny zpět, uživatelé obdrží chybu HTTP 404 při navigaci na položky sklopné kódy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="d9bf7-179">Chcete-li opravit tuto chybu pro MVC, přidejte novou položku scaffolded a vyberte mvc 5 závislosti (minimální nebo úplné).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="d9bf7-180">Tento proces přidá všechny požadované změny do projektu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="d9bf7-181">Oprava této chyby pro webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="d9bf7-182">Přidejte do projektu následující třídu WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="d9bf7-183">Konfigurace webapiconfig.register v\_metodě Start aplikace v Global.asax takto:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="d9bf7-184">Visual Studio Express 2012 pro web přestane fungovat po přidání položky sádlo</span><span class="sxs-lookup"><span data-stu-id="d9bf7-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="d9bf7-185">Pokud Visual Studio Express 2012 pro web přestane fungovat po přidání scaffolded položky s entity Framework (například web API 2 Controller s akcemi, pomocí entity Framework), je možné, že Visual Studio Express nepodařilo načíst nativní bitové kopie sestavení závislé na System.Web.Extensions.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="d9bf7-186">Chcete-li tento problém vyřešit, nakonfigurujte aplikaci Visual Studio Express tak, aby fungovala s bitovou kopií msil souboru System.Web.Extensions:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="d9bf7-187">Otevřete příkazový řádek v režimu správce.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="d9bf7-188">Přejděte na %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE nebo %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (pro 64bitový systém Windows).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="d9bf7-189">Otevřete v textovém editoru soubor VWDExpress.exe.config.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="d9bf7-190">Pod &lt;prvek konfiguračního&gt; &gt;/&lt;runtime přidejte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="d9bf7-191">Restartujte visual studio express 2012 pro web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="d9bf7-192">ASP.NET Břitva 3</span><span class="sxs-lookup"><span data-stu-id="d9bf7-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="d9bf7-193">Zobrazení souboru cshtml pomocí funkce Procházet pomocí nebo F5 způsobí chybu serveru</span><span class="sxs-lookup"><span data-stu-id="d9bf7-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="d9bf7-194">Když vytvoříte projekt MVC 5 v sadě Visual Studio 2012 (nebo otevřete v sadě Visual Studio 2012 projekt MVC 5, který byl vytvořen v sadě Visual Studio 2013) a pokusíte se zobrazit soubor cshtml pomocí funkce Procházet pomocí nebo F5, zobrazí se chyba, která uvádí – **Chyba serveru v aplikaci ./.**</span><span class="sxs-lookup"><span data-stu-id="d9bf7-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="d9bf7-195">Server se pokusí přejít na`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="d9bf7-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="d9bf7-196">Chcete-li tento problém vyřešit, změňte nastavení **Akce zahájení** v projektu na **Konkrétní stránku**.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="d9bf7-197">Není nutné zadat hodnotu pro stránku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="d9bf7-198">Po provedení této změny se výběrem f5 přejde`http://localhost:XXXX`do kořenového adresáře aplikace ( ).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="d9bf7-199">Toto chování není stejné jako chování pro projekty MVC 5 v sadě Visual Studio 2013, kde nastavení **Aktuální stránka** spustí otevřenou stránku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="d9bf7-200">Url Přepsat a tilde (~)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="d9bf7-201">Po upgradu na ASP.NET Razor 3 nebo ASP.NET MVC 5, tilda (~) zápis již nemusí fungovat správně, pokud používáte přepíše URL.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="d9bf7-202">Přepsání adresy URL ovlivňuje zápis tildy(~) &lt;v&gt; &lt;elementech&gt; &lt;HTML,&gt;jako je A/ , SCRIPT/ , LINK/ , a v důsledku toho se vlnovka již nemapuje do kořenového adresáře.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="d9bf7-203">Pokud například přepíšete požadavky na **asp.net/content** na **asp.net**, atribut href &lt;v a&gt; href="~/content/"/ **/** se překládá na **/content/content/** místo .</span><span class="sxs-lookup"><span data-stu-id="d9bf7-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="d9bf7-204">Chcete-li potlačit tuto změnu, můžete nastavit kontext **WasUrlRewritten služby IIS\_** na false v každé webové stránce nebo v **aplikaci\_BeginRequest** v Global.asax.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="d9bf7-205">Šablony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-205">Templates</span></span>

<span data-ttu-id="d9bf7-206">Při vytváření ASP.NET projektů MVC pomocí sady Visual Studio 2012 ve Windows 8.1 nebo Windows Server 2012 R2 zobrazí Visual Studio chybovou zprávu s textem Konfigurace webové [url] pro ASP.NET 4.5 se nezdařilo."</span><span class="sxs-lookup"><span data-stu-id="d9bf7-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![chyba konfigurace](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="d9bf7-208">Tato chyba se zobrazí, protože Visual Studio 2012 nepovoluje funkci ASP.NET 4.5, když je nainstalována v těchto verzích systému Windows.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="d9bf7-209">Chcete-li povolit ASP.NET 4.5, proveďte kroky popsané v [části Zapnutí nebo vypnutí funkcí systému Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![zapnutí nebo vypnutí funkcí systému Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="d9bf7-211">Případně můžete povolit ASP.NET 4.5 prostřednictvím příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="d9bf7-212">Otevřete příkazový řádek v režimu správce.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="d9bf7-213">Spusťte následující příkaz, abyste povolili ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
