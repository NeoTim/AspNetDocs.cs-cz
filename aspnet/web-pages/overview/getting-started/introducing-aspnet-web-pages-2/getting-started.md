---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: Začínáme | Microsoft Docs
author: Rick-Anderson
description: WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET. Použijte Visual Studio nebo Visual Studio Code. Tento návod...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240756"
---
# <a name="getting-started"></a><span data-ttu-id="6e8de-105">začínáme</span><span class="sxs-lookup"><span data-stu-id="6e8de-105">Getting Started</span></span>

<span data-ttu-id="6e8de-106">, autor: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6e8de-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="6e8de-107">WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e8de-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="6e8de-108">Použijte [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) nebo [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6e8de-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="6e8de-109">Tyto doprovodné materiály a aplikace poskytují přehled webových stránek ASP.NET (verze 2 nebo novější) a syntaxe Razor, což je odlehčené rozhraní pro vytváření dynamických webů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="6e8de-110">Také zavádí WebMatrix, nástroj pro vytváření stránek a lokalit.</span><span class="sxs-lookup"><span data-stu-id="6e8de-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="6e8de-111">**Level**: New to ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="6e8de-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="6e8de-112">**Předpokládá se dovednost**: HTML, základní šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="6e8de-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="6e8de-113">Co se naučíte v prvním kurzu sady:</span><span class="sxs-lookup"><span data-stu-id="6e8de-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="6e8de-114">Jaké jsou technologie webových stránek ASP.NET a k čemu slouží.</span><span class="sxs-lookup"><span data-stu-id="6e8de-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="6e8de-115">Jaká je WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6e8de-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="6e8de-116">Jak nainstalovat vše.</span><span class="sxs-lookup"><span data-stu-id="6e8de-116">How to install everything.</span></span>
> - <span data-ttu-id="6e8de-117">Vytvoření webu pomocí WebMatrixu</span><span class="sxs-lookup"><span data-stu-id="6e8de-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="6e8de-118">Popsané funkce a technologie:</span><span class="sxs-lookup"><span data-stu-id="6e8de-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="6e8de-119">Instalace webové platformy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6e8de-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="6e8de-120">WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-120">WebMatrix.</span></span>
> - <span data-ttu-id="6e8de-121">stránky *. cshtml*</span><span class="sxs-lookup"><span data-stu-id="6e8de-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="6e8de-122">Jan Pope původně napsal tento kurz.</span><span class="sxs-lookup"><span data-stu-id="6e8de-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="6e8de-123">FitzMacken ho aktualizoval pro Microsoft WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="6e8de-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6e8de-124">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="6e8de-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6e8de-125">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="6e8de-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="6e8de-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="6e8de-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="6e8de-127">Co byste měli znát?</span><span class="sxs-lookup"><span data-stu-id="6e8de-127">What Should You Know?</span></span>

<span data-ttu-id="6e8de-128">Předpokládáme, že jste obeznámeni s:</span><span class="sxs-lookup"><span data-stu-id="6e8de-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="6e8de-129">**HTML**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-129">**HTML**.</span></span> <span data-ttu-id="6e8de-130">Nejsou vyžadovány žádné podrobné znalosti.</span><span class="sxs-lookup"><span data-stu-id="6e8de-130">No in-depth expertise is required.</span></span> <span data-ttu-id="6e8de-131">Nebudeme vysvětlovat kód HTML, ale nepoužíváme to nic složitě.</span><span class="sxs-lookup"><span data-stu-id="6e8de-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="6e8de-132">Poskytneme odkazy na kurzy HTML, kde se domníváme, že jsou užitečné.</span><span class="sxs-lookup"><span data-stu-id="6e8de-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="6e8de-133">Šablony stylů **CSS**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="6e8de-134">Stejné jako u formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="6e8de-134">Same as with HTML.</span></span>
- <span data-ttu-id="6e8de-135">**Základní nápady databáze**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-135">**Basic database ideas**.</span></span> <span data-ttu-id="6e8de-136">Pokud jste tabulku použili pro data a seřadili a vyfiltrují data, je to úroveň odbornosti, která je obecně předpokladem pro tuto sadu kurzů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="6e8de-137">Také předpokládáme, že vás zajímá základní programování.</span><span class="sxs-lookup"><span data-stu-id="6e8de-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="6e8de-138">Webové stránky ASP.NET používají programovací jazyk nazvaný C#.</span><span class="sxs-lookup"><span data-stu-id="6e8de-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="6e8de-139">V programování nemusíte mít žádné pozadí, stačí to jenom na vás.</span><span class="sxs-lookup"><span data-stu-id="6e8de-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="6e8de-140">Pokud jste už dříve napsali JavaScript na webové stránce, měli byste mít spoustu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="6e8de-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="6e8de-141">Všimněte si, že pokud jste obeznámeni s programováním, může se stát, že tento kurz se zpočátku posouvá pomalu, zatímco nově přinášíme nové programátory do rychlosti.</span><span class="sxs-lookup"><span data-stu-id="6e8de-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="6e8de-142">Stejně jako v předchozích několika kurzech se ale bude vysvětlovat méně základních programů, které vám pomohou při seznámení s rychlejším klipem.</span><span class="sxs-lookup"><span data-stu-id="6e8de-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="6e8de-143">Co potřebujete?</span><span class="sxs-lookup"><span data-stu-id="6e8de-143">What Do You Need?</span></span>

<span data-ttu-id="6e8de-144">Zde je seznam toho, co budete potřebovat:</span><span class="sxs-lookup"><span data-stu-id="6e8de-144">Here's what you'll need:</span></span>

- <span data-ttu-id="6e8de-145">Počítač se systémem Windows 8, Windows 7, Windows Server 2008 nebo Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="6e8de-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="6e8de-146">Živé připojení k Internetu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-146">A live internet connection.</span></span>
- <span data-ttu-id="6e8de-147">Oprávnění správce (požadováno pro proces instalace).</span><span class="sxs-lookup"><span data-stu-id="6e8de-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="6e8de-148">Co jsou webové stránky ASP.NET?</span><span class="sxs-lookup"><span data-stu-id="6e8de-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="6e8de-149">Webové stránky ASP.NET jsou rozhraní, které můžete použít k vytvoření dynamických webových stránek.</span><span class="sxs-lookup"><span data-stu-id="6e8de-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="6e8de-150">Jednoduchá webová stránka HTML je statická; jeho obsah je určen pevným kódem HTML, který je na stránce.</span><span class="sxs-lookup"><span data-stu-id="6e8de-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="6e8de-151">Dynamické stránky, jako jsou ty, které vytvoříte pomocí webových stránek ASP.NET, vám umožní vytvořit obsah stránky za běhu pomocí kódu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="6e8de-152">Dynamické stránky umožňují provádět nejrůznější akce.</span><span class="sxs-lookup"><span data-stu-id="6e8de-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="6e8de-153">Uživatele můžete požádat o zadání pomocí formuláře a pak změnit, co stránka zobrazuje nebo jak vypadá.</span><span class="sxs-lookup"><span data-stu-id="6e8de-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="6e8de-154">Můžete získat informace od uživatele, uložit ho do databáze a pak ho zobrazit později.</span><span class="sxs-lookup"><span data-stu-id="6e8de-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="6e8de-155">Můžete odesílat e-maily z webu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-155">You can send email from your site.</span></span> <span data-ttu-id="6e8de-156">Můžete komunikovat s jinými službami na webu (například službou mapování) a vytvořit stránky, které integrují informace z těchto zdrojů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="6e8de-157">Co je WebMatrix?</span><span class="sxs-lookup"><span data-stu-id="6e8de-157">What is WebMatrix?</span></span>

<span data-ttu-id="6e8de-158">WebMatrix je nástroj, který integruje editor webových stránek, databázový nástroj, webový server pro testování stránek a funkce pro publikování vašeho webu na internetu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="6e8de-159">WebMatrix je zdarma a je snadné ji nainstalovat a snadno používat.</span><span class="sxs-lookup"><span data-stu-id="6e8de-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="6e8de-160">(Funguje také pro jednoduché stránky HTML a také pro jiné technologie, jako je PHP.)</span><span class="sxs-lookup"><span data-stu-id="6e8de-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="6e8de-161">Pro práci s ASP.NET webovými stránkami *nemusíte* ve skutečnosti používat WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6e8de-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="6e8de-162">Můžete vytvářet stránky pomocí textového editoru, například a testovat stránky pomocí webového serveru, ke kterému máte přístup.</span><span class="sxs-lookup"><span data-stu-id="6e8de-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="6e8de-163">WebMatrix je ale velmi snadné, takže tyto kurzy budou používat WebMatrix v celém rozsahu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="6e8de-164">O těchto kurzech</span><span class="sxs-lookup"><span data-stu-id="6e8de-164">About These Tutorials</span></span>

<span data-ttu-id="6e8de-165">V tomto kurzu se naučíte, jak používat webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e8de-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="6e8de-166">V tomto úvodním kurzu je celkem 9 kurzů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="6e8de-167">Je součástí série kurzů, které vás přesměrují z ASP.NET začátečníků na webové stránky a vytváření reálných webů s profesionálním přehledem.</span><span class="sxs-lookup"><span data-stu-id="6e8de-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="6e8de-168">V tomto prvním kurzu se soustředíme na to, jak se naučíte pracovat s ASP.NET webovými stránkami.</span><span class="sxs-lookup"><span data-stu-id="6e8de-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="6e8de-169">Až budete hotovi, můžete pracovat s dalšími kurzy, které se nacházejí v tomto umístění a které podrobněji ilustrují webové stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="6e8de-170">Podrobnější vysvětlení jsme záměrně snadno našli.</span><span class="sxs-lookup"><span data-stu-id="6e8de-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="6e8de-171">A kdykoli zobrazíme něco, v tomto kurzu si vždycky vyberu způsob, jakým je nejjednodušší pochopit.</span><span class="sxs-lookup"><span data-stu-id="6e8de-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="6e8de-172">Pozdější kurzy nastaví další hloubku a ukáže vám efektivnější nebo pružnější přístup (ještě více zajímavější).</span><span class="sxs-lookup"><span data-stu-id="6e8de-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="6e8de-173">Tyto kurzy ale vyžadují, abyste nejdřív pochopili základy.</span><span class="sxs-lookup"><span data-stu-id="6e8de-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="6e8de-174">Sada kurzů, kterou jste právě zahájili, pokrývá tyto funkce webových stránek ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="6e8de-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="6e8de-175">Seznámení s nainstalovanou a načítají se všechno.</span><span class="sxs-lookup"><span data-stu-id="6e8de-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="6e8de-176">(To je v kurzu, který čtete.)</span><span class="sxs-lookup"><span data-stu-id="6e8de-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="6e8de-177">Základy programování webových stránek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e8de-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="6e8de-178">Vytváří se databáze.</span><span class="sxs-lookup"><span data-stu-id="6e8de-178">Creating a database.</span></span>
- <span data-ttu-id="6e8de-179">Vytvoření a zpracování formuláře vstupu uživatele.</span><span class="sxs-lookup"><span data-stu-id="6e8de-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="6e8de-180">Přidávání, aktualizace a odstraňování dat v databázi.</span><span class="sxs-lookup"><span data-stu-id="6e8de-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="6e8de-181">Co budete vytvářet?</span><span class="sxs-lookup"><span data-stu-id="6e8de-181">What Will You Create?</span></span>

<span data-ttu-id="6e8de-182">V tomto kurzu se nastavuje a následně vyvíjejí kolem webu, kde můžete vypsat videa, která chcete.</span><span class="sxs-lookup"><span data-stu-id="6e8de-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="6e8de-183">Budete moct zadat filmy, upravit je a zobrazit jejich seznam.</span><span class="sxs-lookup"><span data-stu-id="6e8de-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="6e8de-184">Tady je pár stránek, které vytvoříte v této sadě kurzů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="6e8de-185">První z nich zobrazuje stránku se seznamem filmů, kterou vytvoříte:</span><span class="sxs-lookup"><span data-stu-id="6e8de-185">The first one shows the movie listing page that you'll create:</span></span>

![Aplikace dokončil Movie ukazující seznam filmů](getting-started/_static/image1.png)

<span data-ttu-id="6e8de-187">A tady je stránka, která vám umožní přidat nové informace o videu na web:</span><span class="sxs-lookup"><span data-stu-id="6e8de-187">And here's the page that lets you add new movie information to your site:</span></span>

![Dokončená aplikace filmů ukazující stránku přidat film](getting-started/_static/image2.png)

<span data-ttu-id="6e8de-189">V dalším kurzu se nastavují buildy na této sadě a přidají se další funkce, jako je nahrávání obrázků, odesílání a posílání e-mailů a integrace se sociálními médii.</span><span class="sxs-lookup"><span data-stu-id="6e8de-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="6e8de-190">Podívejte se na tuto aplikaci spuštěnou v Azure</span><span class="sxs-lookup"><span data-stu-id="6e8de-190">See this App Running on Azure</span></span>

<span data-ttu-id="6e8de-191">Chcete zobrazit dokončený web běžící jako živá webová aplikace?</span><span class="sxs-lookup"><span data-stu-id="6e8de-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="6e8de-192">Úplnou verzi aplikace můžete nasadit do svého účtu Azure pouhým kliknutím na následující tlačítko.</span><span class="sxs-lookup"><span data-stu-id="6e8de-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="6e8de-193">K nasazení tohoto řešení do Azure potřebujete účet Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="6e8de-194">Pokud ještě nemáte účet, máte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="6e8de-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="6e8de-195">[Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="6e8de-196">[Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="6e8de-197">Instalace všeho</span><span class="sxs-lookup"><span data-stu-id="6e8de-197">Installing Everything</span></span>

<span data-ttu-id="6e8de-198">Vše můžete nainstalovat pomocí instalačního programu webové platformy od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="6e8de-199">V důsledku toho nainstalujete instalační program a pak ho použijete k instalaci všech ostatních.</span><span class="sxs-lookup"><span data-stu-id="6e8de-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="6e8de-200">Chcete-li použít webové stránky, je nutné mít nainstalován alespoň systém Windows XP s aktualizací SP3 nebo Windows Server 2008 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="6e8de-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="6e8de-201">Na [stránce webové stránky](../../../index.md) na webu ASP.NET klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![Web ASP.NET s &quot; tlačítkem nainstalovat WebMatrix &quot;](getting-started/_static/image3.png)

<span data-ttu-id="6e8de-203">Před instalací WebMatrixu se zobrazí výzva, abyste přijali Licenční podmínky a prohlášení o zásadách ochrany osobních údajů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![přijmout termín pro zahájení instalace](getting-started/_static/image4.png)

<span data-ttu-id="6e8de-205">Kliknutím na **Spustit** spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="6e8de-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="6e8de-206">(Pokud chcete instalační program uložit, klikněte na **Uložit** a spusťte instalační program ze složky, kam jste ho uložili.)</span><span class="sxs-lookup"><span data-stu-id="6e8de-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="6e8de-207">Zobrazí se instalace webové platformy, která je připravena k instalaci WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="6e8de-208">Klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="6e8de-209">Instalační proces zobrazí informace o tom, co je potřeba nainstalovat do vašeho počítače, a spustí proces.</span><span class="sxs-lookup"><span data-stu-id="6e8de-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="6e8de-210">V závislosti na tom, co je potřeba nainstalovat, může proces trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="6e8de-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="6e8de-211">Kliknutím **na Souhlasím** přijměte licenční podmínky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="6e8de-212">Hello, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="6e8de-212">Hello, WebMatrix</span></span>

<span data-ttu-id="6e8de-213">Až to bude hotové, proces instalace může automaticky spustit WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6e8de-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="6e8de-214">Pokud tomu tak není, v systému Windows v nabídce **Start** spusťte **Microsoft WebMatrix**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="6e8de-215">Při prvním spuštění WebMatrixu budete mít možnost se přihlásit k Microsoft Azure pomocí účet Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6e8de-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="6e8de-216">Když se přihlásíte, obdržíte 10 bezplatných webových aplikací prostřednictvím Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="6e8de-217">Tyto bezplatné webové aplikace poskytují pohodlný způsob, jak testovat vaše aplikace.</span><span class="sxs-lookup"><span data-stu-id="6e8de-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="6e8de-218">Pokud ještě nemáte účet Azure, ale máte předplatné MSDN, můžete [si aktivovat výhody předplatného MSDN](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="6e8de-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="6e8de-219">V opačném případě můžete během několika minut vytvořit bezplatný zkušební účet.</span><span class="sxs-lookup"><span data-stu-id="6e8de-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6e8de-220">Podrobnosti najdete v článku [Bezplatná zkušební verze Azure](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="6e8de-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="6e8de-221">K pokračování v tomto kurzu se nemusíte přihlašovat hned.</span><span class="sxs-lookup"><span data-stu-id="6e8de-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="6e8de-222">Pokud se teď přihlásíte, budete mít i nadále možnost přihlásit se později.</span><span class="sxs-lookup"><span data-stu-id="6e8de-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="6e8de-223">Poslední [téma](publishing.md) v této sérii kurzů se zabývá tím, jak nasadit váš web do Azure. Proto byste se museli přihlašovat k dokončení tohoto tématu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="6e8de-224">V tomto okamžiku se buď přihlaste pomocí účet Microsoft nebo v pravém dolním rohu vyberte **ne** .</span><span class="sxs-lookup"><span data-stu-id="6e8de-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![Přihlášení](getting-started/_static/image7.png)

<span data-ttu-id="6e8de-226">Začněte tím, že vytvoříte prázdný web a přidáte stránku.</span><span class="sxs-lookup"><span data-stu-id="6e8de-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="6e8de-227">V pozdějším kurzu v této sadě budete hrát s jednou z vestavěných šablon webů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="6e8de-228">V okně Start klikněte na **Nový**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-228">In the start window, click **New**.</span></span>

![Úvodní obrazovka WebMatrixu](getting-started/_static/image8.png)

<span data-ttu-id="6e8de-230">Šablony jsou předem připravené soubory a stránky pro různé typy webů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="6e8de-231">Chcete-li zobrazit všechny šablony, které jsou ve výchozím nastavení k dispozici, vyberte možnost galerie šablon.</span><span class="sxs-lookup"><span data-stu-id="6e8de-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![Vybrat galerii šablon](getting-started/_static/image9.png)

<span data-ttu-id="6e8de-233">V okně **rychlé zprovoznění** vyberte ze skupiny **ASP.NET** možnost **prázdná lokalita** a pojmenujte novou lokalitu "WebPagesMovies".</span><span class="sxs-lookup"><span data-stu-id="6e8de-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![Okno WebMatrix rychlé zprovoznění s vybranou šablonou prázdného webu](getting-started/_static/image10.png)

<span data-ttu-id="6e8de-235">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-235">Click **Next**.</span></span>

<span data-ttu-id="6e8de-236">Pokud jste se přihlásili k vašemu účet Microsoft, budete mít možnost vytvořit si web na Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="6e8de-237">Na základě názvu vašeho webu je doporučený výchozí název **WebPagesMovies.azurewebsites.NET** ; vykřičník však indikuje, že tento název není k dispozici v systému Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="6e8de-238">Pro jednoduchost vyberte **Přeskočit** pro obejít vytváření webu v Azure hned teď.</span><span class="sxs-lookup"><span data-stu-id="6e8de-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="6e8de-239">Později v této sérii publikujte web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8de-239">Later in this series, we will publish the site to Azure.</span></span>

![Vytvoření webu Azure](getting-started/_static/image11.png)

<span data-ttu-id="6e8de-241">WebMatrix vytvoří a otevře web:</span><span class="sxs-lookup"><span data-stu-id="6e8de-241">WebMatrix creates and opens the site:</span></span>

![Nový web WebPagesMovies otevřený ve WebMatrixu](getting-started/_static/image12.png)

<span data-ttu-id="6e8de-243">V horní části je k dispozici panel nástrojů Rychlý přístup a pás karet.</span><span class="sxs-lookup"><span data-stu-id="6e8de-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="6e8de-244">V levém dolním rohu se zobrazí selektor pracovního prostoru, ve kterém můžete přepínat mezi úlohami (**weby**, **soubory**, **databázemi**a **sestavami**).</span><span class="sxs-lookup"><span data-stu-id="6e8de-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="6e8de-245">Napravo je podokno obsahu pro Editor a pro sestavy.</span><span class="sxs-lookup"><span data-stu-id="6e8de-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="6e8de-246">V dolní části se vám občas zobrazuje oznamovací pruh pro zprávy.</span><span class="sxs-lookup"><span data-stu-id="6e8de-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="6e8de-247">Další informace o WebMatrixu a jejích funkcích najdete v těchto kurzech.</span><span class="sxs-lookup"><span data-stu-id="6e8de-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="6e8de-248">Vytvoření webové stránky</span><span class="sxs-lookup"><span data-stu-id="6e8de-248">Creating a Web Page</span></span>

<span data-ttu-id="6e8de-249">Pokud se chcete seznámit s webovými stránkami WebMatrix a ASP.NET, vytvoříte jednoduchou stránku.</span><span class="sxs-lookup"><span data-stu-id="6e8de-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="6e8de-250">V selektoru pracovního prostoru vyberte pracovní prostor **soubory** .</span><span class="sxs-lookup"><span data-stu-id="6e8de-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="6e8de-251">Tento pracovní prostor vám umožní pracovat se soubory a složkami.</span><span class="sxs-lookup"><span data-stu-id="6e8de-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="6e8de-252">V levém podokně se zobrazuje struktura souborů webu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="6e8de-253">Pás karet se změní na Zobrazit úlohy týkající se souborů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-253">The ribbon changes to show file-related tasks.</span></span>

![Pracovní prostor souborů v WebMatrixu](getting-started/_static/image13.png)

<span data-ttu-id="6e8de-255">Na pásu karet klikněte na šipku pod položkou **Nový** a pak klikněte na **nový soubor**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![&quot; &quot; Vytvoření nového souboru pomocí nového příkazu na pásu karet](getting-started/_static/image14.png)

<span data-ttu-id="6e8de-257">WebMatrix zobrazí seznam typů souborů.</span><span class="sxs-lookup"><span data-stu-id="6e8de-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="6e8de-258">Vyberte **cshtml**a do pole **název** zadejte "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="6e8de-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="6e8de-259">Stránka CSHTML je stránka ASP.NET webové stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![Vytváří se nová stránka s CSHTML s názvem HelloWorld. cshtml.](getting-started/_static/image15.png)

<span data-ttu-id="6e8de-261">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-261">Click **OK**.</span></span>

<span data-ttu-id="6e8de-262">WebMatrix vytvoří stránku a otevře ji v editoru.</span><span class="sxs-lookup"><span data-stu-id="6e8de-262">WebMatrix creates the page and opens it in the editor.</span></span>

![Nová stránka HelloWorld v editoru WebMatrixu](getting-started/_static/image16.png)

<span data-ttu-id="6e8de-264">Jak vidíte, stránka obsahuje hlavně běžný kód HTML, s výjimkou bloku v horní části, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="6e8de-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="6e8de-265">To je pro přidání kódu, jak uvidíte za chvíli.</span><span class="sxs-lookup"><span data-stu-id="6e8de-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="6e8de-266">Všimněte si, že různé části stránky &mdash; názvy elementů, atributy a text spolu s blokem nahoře – jsou všechny v různých barvách.</span><span class="sxs-lookup"><span data-stu-id="6e8de-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="6e8de-267">To se nazývá *zvýrazňování syntaxe*a usnadňuje tak zachování všeho, co je jasné.</span><span class="sxs-lookup"><span data-stu-id="6e8de-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="6e8de-268">Je to jedna z funkcí, která usnadňuje práci s webovými stránkami ve WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="6e8de-269">Přidejte obsah pro `<head>` prvky a `<body>` jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="6e8de-270">(Pokud chcete, můžete pouze zkopírovat následující blok a nahradit celou existující stránku tímto kódem.)</span><span class="sxs-lookup"><span data-stu-id="6e8de-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="6e8de-271">Na panelu nástrojů Rychlý přístup nebo v nabídce **soubor** klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![Tlačítko Uložit na panelu nástrojů Rychlý přístup k WebMatrixu](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="6e8de-273">Testování stránky</span><span class="sxs-lookup"><span data-stu-id="6e8de-273">Testing the Page</span></span>

<span data-ttu-id="6e8de-274">V pracovním prostoru **soubory** klikněte pravým tlačítkem na stránku *HelloWorld. cshtml* a pak klikněte na **Spustit v prohlížeči**.</span><span class="sxs-lookup"><span data-stu-id="6e8de-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![Spuštění stránky pomocí tlačítka spustit na pásu karet WebMatrix](getting-started/_static/image18.png)

<span data-ttu-id="6e8de-276">WebMatrix spustí integrovaný webový server (IIS Express), který můžete použít k testování stránek v počítači.</span><span class="sxs-lookup"><span data-stu-id="6e8de-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="6e8de-277">(Bez IIS Express ve WebMatrixu byste museli stránku publikovat na webovém serveru ještě předtím, než ji budete moct otestovat.) Stránka se zobrazí ve výchozím prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="6e8de-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;&quot;Stránka Hello World spuštěná v prohlížeči](getting-started/_static/image19.png)

<span data-ttu-id="6e8de-279">Všimněte si, že když testujete stránku ve WebMatrixu, adresa URL v prohlížeči je podobná `http://localhost:33651/HelloWorld.cshtml.` názvu *localhost* odkazuje na místní server, což znamená, že stránka je obsluhována webovým serverem, který je ve vašem počítači.</span><span class="sxs-lookup"><span data-stu-id="6e8de-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="6e8de-280">Jak je uvedeno, WebMatrix obsahuje program webového serveru s názvem IIS Express, který se spouští při spuštění stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="6e8de-281">Číslo za *localhost* (například *localhost: 33651*) odkazuje na *číslo portu* v počítači.</span><span class="sxs-lookup"><span data-stu-id="6e8de-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="6e8de-282">Toto je číslo "kanálu", který IIS Express používá pro tento konkrétní web.</span><span class="sxs-lookup"><span data-stu-id="6e8de-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="6e8de-283">Číslo portu je vybráno náhodně z rozsahu 1024 až 65536 při vytváření lokality a je odlišné pro každý web, který vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="6e8de-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="6e8de-284">(Při testování vlastního webového serveru bude číslo portu skoro určitě jiné číslo než 33561.) Když pro každý web použijete jiný port, IIS Express může mít přímý odkaz na vaše weby, se kterými se mluví.</span><span class="sxs-lookup"><span data-stu-id="6e8de-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="6e8de-285">Později, když publikujete web na veřejný webový server, na adrese URL se už nezobrazuje *localhost* .</span><span class="sxs-lookup"><span data-stu-id="6e8de-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="6e8de-286">V tomto okamžiku se zobrazí více typickou adresa URL, například `http://myhostingsite/mywebsite/HelloWorld.cshtml` nebo cokoli, co stránka je.</span><span class="sxs-lookup"><span data-stu-id="6e8de-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="6e8de-287">V této sérii kurzů se dozvíte více o publikování webu později.</span><span class="sxs-lookup"><span data-stu-id="6e8de-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="6e8de-288">Přidání kódu na straně serveru</span><span class="sxs-lookup"><span data-stu-id="6e8de-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="6e8de-289">Zavřete prohlížeč a vraťte se zpátky na stránku ve WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="6e8de-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="6e8de-290">Přidejte řádek do bloku kódu tak, aby vypadal jako následující kód:</span><span class="sxs-lookup"><span data-stu-id="6e8de-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="6e8de-291">Toto je trochu kódu Razor.</span><span class="sxs-lookup"><span data-stu-id="6e8de-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="6e8de-292">Je pravděpodobně jasné, že získá aktuální datum a čas a vloží tuto hodnotu do *proměnné* s názvem `currentDateTime` .</span><span class="sxs-lookup"><span data-stu-id="6e8de-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="6e8de-293">V dalším kurzu si přečtete Další informace o syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="6e8de-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="6e8de-294">V těle stránky za `<p>Hello World!</p>` element přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="6e8de-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="6e8de-295">Tento kód získá hodnotu, kterou vložíte do `currentDateTime` proměnné v horní části, a vloží ji do značky stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="6e8de-296">`@`Znak označí kód webových stránek ASP.NET na stránce.</span><span class="sxs-lookup"><span data-stu-id="6e8de-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="6e8de-297">Spusťte znovu stránku (WebMatrix uloží změny, než se stránka spustí).</span><span class="sxs-lookup"><span data-stu-id="6e8de-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="6e8de-298">Tentokrát se na stránce zobrazí datum a čas.</span><span class="sxs-lookup"><span data-stu-id="6e8de-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World &quot; Stránka běžící v prohlížeči s dynamicky generovaným zobrazením času](getting-started/_static/image20.png)

<span data-ttu-id="6e8de-300">Chvíli počkejte a pak aktualizujte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="6e8de-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="6e8de-301">Zobrazuje se aktualizace data a času.</span><span class="sxs-lookup"><span data-stu-id="6e8de-301">The date and time display is updated.</span></span>

<span data-ttu-id="6e8de-302">V prohlížeči se podívejte na zdroj stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-302">In the browser, look at the page source.</span></span> <span data-ttu-id="6e8de-303">Vypadá to, že se jedná o následující značky:</span><span class="sxs-lookup"><span data-stu-id="6e8de-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="6e8de-304">Všimněte si, že `@{ }` blok v horní části není tam.</span><span class="sxs-lookup"><span data-stu-id="6e8de-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="6e8de-305">Všimněte si také, že zobrazení data a času zobrazuje skutečný řetězec znaků ( `1/18/2012 2:49:50 PM` nebo libovolné), a ne `@currentDateTime` jako na stránce *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="6e8de-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="6e8de-306">Co se stalo, když jste spustili stránku, ASP.NET zpracoval veškerý kód (v tomto případě je velmi malý), který byl označen pomocí `@` .</span><span class="sxs-lookup"><span data-stu-id="6e8de-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="6e8de-307">Kód vytvoří výstup a tento výstup byl vložen do stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="6e8de-308">To je to, co ASP.NET webové stránky.</span><span class="sxs-lookup"><span data-stu-id="6e8de-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="6e8de-309">Když si přečtete, že webové stránky ASP.NET vytvářejí dynamický webový obsah, co se vám zobrazuje, je to nápad.</span><span class="sxs-lookup"><span data-stu-id="6e8de-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="6e8de-310">Stránka, kterou jste právě vytvořili, obsahuje stejný kód HTML, který jste viděli předtím.</span><span class="sxs-lookup"><span data-stu-id="6e8de-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="6e8de-311">Může také obsahovat kód, který může provádět nejrůznější úlohy.</span><span class="sxs-lookup"><span data-stu-id="6e8de-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="6e8de-312">V tomto příkladu existovala triviální úloha získání aktuálního data a času.</span><span class="sxs-lookup"><span data-stu-id="6e8de-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="6e8de-313">Jak jste viděli, můžete kód ve formátu HTML a na stránce tak vydávat výstup.</span><span class="sxs-lookup"><span data-stu-id="6e8de-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="6e8de-314">Když někdo požádá o stránku *. cshtml* v prohlížeči, ASP.NET zpracuje stránku, i když je stále v rukou webového serveru.</span><span class="sxs-lookup"><span data-stu-id="6e8de-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="6e8de-315">ASP.NET vloží výstup kódu (pokud existuje) na stránku jako HTML.</span><span class="sxs-lookup"><span data-stu-id="6e8de-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="6e8de-316">Po dokončení zpracování kódu odešle ASP.NET výslednou stránku do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="6e8de-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="6e8de-317">Všechny prohlížeče v tuto minulosti jsou HTML.</span><span class="sxs-lookup"><span data-stu-id="6e8de-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="6e8de-318">Zde je diagram:</span><span class="sxs-lookup"><span data-stu-id="6e8de-318">Here's a diagram:</span></span>

![Koncepční postup, jak ASP.NET vygeneruje kód HTML dynamicky](getting-started/_static/image21.png)

<span data-ttu-id="6e8de-320">Nápad je jednoduchý, ale existuje mnoho zajímavých úkolů, které může kód provádět, a existuje mnoho zajímavých způsobů, jak můžete na stránku dynamicky přidávat obsah HTML.</span><span class="sxs-lookup"><span data-stu-id="6e8de-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="6e8de-321">A ASP.NET *. cshtml* stránky, podobně jako jakékoli stránky HTML, mohou také obsahovat kód, který běží v samotném prohlížeči (kód JavaScript a jQuery).</span><span class="sxs-lookup"><span data-stu-id="6e8de-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="6e8de-322">Všechny tyto věci prozkoumáte v této sadě kurzů a v dalších.</span><span class="sxs-lookup"><span data-stu-id="6e8de-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="6e8de-323">Připravujeme další</span><span class="sxs-lookup"><span data-stu-id="6e8de-323">Coming Up Next</span></span>

<span data-ttu-id="6e8de-324">V dalším kurzu v této sérii prozkoumáte ASP.NET webové stránky s více dalšími.</span><span class="sxs-lookup"><span data-stu-id="6e8de-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e8de-325">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="6e8de-325">Additional Resources</span></span>

<span data-ttu-id="6e8de-326">[Vytvořte si zcela nového webu ASP.NET](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span><span class="sxs-lookup"><span data-stu-id="6e8de-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="6e8de-327">Toto je kurz, který se konkrétně týká použití WebMatrixu (nikoli ASP.NET webových stránek).</span><span class="sxs-lookup"><span data-stu-id="6e8de-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="6e8de-328">Obsahuje ještě trochu více podrobností o některých dalších funkcích WebMatrixu, které se v této sadě kurzů nezabývá.</span><span class="sxs-lookup"><span data-stu-id="6e8de-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6e8de-329">Další</span><span class="sxs-lookup"><span data-stu-id="6e8de-329">Next</span></span>](intro-to-web-pages-programming.md)
