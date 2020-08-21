---
uid: ajax/cdn/overview
title: Content Delivery Network Microsoft AJAX | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 9eebe0e52af2a0fca967a51afb58c7db174d9fdb
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702917"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="cf61e-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="cf61e-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="cf61e-103">Provozní aplikace by neměly mít u prostředků CDN nevratnou závislost.</span><span class="sxs-lookup"><span data-stu-id="cf61e-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="cf61e-104">Aplikace by měly být testovány na prostředek CDN, na který se odkazuje, a použít záložní prostředek, pokud CDN není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="cf61e-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="cf61e-105">Rozhraní Microsoft Ajax CDN nemá žádnou smlouvu SLA nad rámec použití Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="cf61e-106">[Tento problém GitHubu](https://github.com/dotnet/AspNetDocs/issues/116) použijte k nahlášení problémů se službou Microsoft Ajax CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="cf61e-107">Obsah</span><span class="sxs-lookup"><span data-stu-id="cf61e-107">Table of Contents</span></span>

<span data-ttu-id="cf61e-108">**[ajax.microsoft.com přejmenováno na ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="cf61e-109">**[Podpora sady Visual Studio. vsdoc](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="cf61e-110">**[Použití ASP.NET AJAX z CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="cf61e-111">**[Použití jQuery z CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="cf61e-112">**[Použití uživatelského rozhraní jQuery z CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="cf61e-113">**[Soubory třetích stran na CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="cf61e-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="cf61e-114">Verze jQuery na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="cf61e-115">jQuery migrace verzí na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="cf61e-116">Vydání uživatelského rozhraní jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="cf61e-117">Vydání ověření jQuery na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="cf61e-118">jQuery Mobile releases na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="cf61e-119">Vydání šablon jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="cf61e-120">Vydávání cyklů jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="cf61e-121">vydávané datatabulka jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="cf61e-122">Modernizr vydaných verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="cf61e-123">JSHint vydaných verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="cf61e-124">Vyseknutí verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="cf61e-125">Globalizace verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="cf61e-126">Odpověď verze v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="cf61e-127">Bootstrap vydaných verzí na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="cf61e-128">Zavedení TouchCarousel vydání na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="cf61e-129"> VerzeHammer.js v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="cf61e-130">ASP.NET webové formuláře a verze AJAX v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="cf61e-131">Verze ASP.NET MVC na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="cf61e-132">ASP.NET signalizace v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="cf61e-133">Technologie Microsoft Ajax Content Delivery Network (CDN) hostuje oblíbené knihovny JavaScript třetích stran, jako je jQuery, a umožňuje je snadno přidat do svých webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="cf61e-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="cf61e-134">Například můžete začít používat jQuery, který je hostován v tomto CDN jednoduše přidáním &lt; &gt; značky skriptu na stránku, která odkazuje na AJAX.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="cf61e-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="cf61e-135">Díky využití sítě CDN můžete významně zlepšit výkon aplikací AJAX.</span><span class="sxs-lookup"><span data-stu-id="cf61e-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="cf61e-136">Obsah sítě CDN je uložený v mezipaměti na serverech umístěných po celém světě.</span><span class="sxs-lookup"><span data-stu-id="cf61e-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="cf61e-137">CDN kromě toho umožňuje prohlížečům znovu použít soubory JavaScriptu třetích stran v mezipaměti pro weby, které se nacházejí v různých doménách.</span><span class="sxs-lookup"><span data-stu-id="cf61e-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="cf61e-138">CDN podporuje protokol SSL (HTTPS) pro případ, že potřebujete poskytovat webovou stránku pomocí SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="cf61e-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="cf61e-139">CDN hostuje následující knihovny skriptů třetích stran, které jste nahráli, a uděluje jim oprávnění vlastníci těchto knihoven:</span><span class="sxs-lookup"><span data-stu-id="cf61e-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="cf61e-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="cf61e-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="cf61e-141">uživatelské rozhraní jQuery (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="cf61e-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="cf61e-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="cf61e-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="cf61e-143">Ověření jQuery (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="cf61e-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="cf61e-144">Cyklus jQuery (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="cf61e-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="cf61e-145">DataTables jQuery (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="cf61e-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="cf61e-146">Microsoft Ajax CDN také obsahuje následující knihovny, které byly nahrány Microsoftem:</span><span class="sxs-lookup"><span data-stu-id="cf61e-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="cf61e-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="cf61e-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="cf61e-148">Soubory JavaScriptu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="cf61e-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="cf61e-149">Soubory JavaScriptu pro signál ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="cf61e-150">Microsoft nenárokuje vlastnictví žádné knihovny třetích stran hostované v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="cf61e-151">Vlastníci těchto knihoven mají licenci na tyto knihovny.</span><span class="sxs-lookup"><span data-stu-id="cf61e-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="cf61e-152">Všechna práva, která může být nutné stáhnout a používat tyto knihovny, jsou udělována výhradně příslušnými vlastníky autorských práv.</span><span class="sxs-lookup"><span data-stu-id="cf61e-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="cf61e-153">Vzhledem k tomu, že se nejedná o knihovny Microsoftu, společnost Microsoft neposkytuje žádné záruky ani licence k duševnímu vlastnictví (včetně žádného mlčky odvozeného patentového práva) pro knihovny třetích stran hostované v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="cf61e-154">Pokud chcete odeslat knihovnu JavaScriptu a vaše knihovna je jedním z hlavních knihoven JavaScriptu (jak je uvedeno v části http://trends.builtwith.com) nebo rozšíření/moduly plug-in do těchto knihoven, které jsou (a) oblíbené; nebo (b) užitečné pro použití v ASP.NET, pak prosím kontaktujte AjaxCDNSubmission@Microsoft.com .</span><span class="sxs-lookup"><span data-stu-id="cf61e-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="cf61e-155">ajax.microsoft.com přejmenováno na ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="cf61e-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="cf61e-156">CDN, který používal název domény microsoft.com, byl změněn tak, aby používal název domény aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="cf61e-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="cf61e-157">Tato změna byla provedena kvůli zvýšení výkonu, protože když se prohlížeč odkazuje na doménu microsoft.com, poslal by všechny soubory cookie z této domény v rámci jednotlivých požadavků.</span><span class="sxs-lookup"><span data-stu-id="cf61e-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="cf61e-158">Přejmenováním na jiný název domény, než je microsoft.com výkon, se dá zvýšit o až 25%.</span><span class="sxs-lookup"><span data-stu-id="cf61e-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="cf61e-159">Poznámka ajax.microsoft.com bude i nadále fungovat, ale doporučuje se ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="cf61e-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="cf61e-160">Starý formát: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="cf61e-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="cf61e-161">Nový formát: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="cf61e-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="cf61e-162">Podpora sady Visual Studio. vsdoc</span><span class="sxs-lookup"><span data-stu-id="cf61e-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="cf61e-163">Chcete-li v sadě Visual Studio 2008 správně používat soubory. vsdoc, musíte se ujistit, že je nainstalována sada VS 2008 SP1 a zda je nainstalována oprava hotfix pro soubory vsdoc.</span><span class="sxs-lookup"><span data-stu-id="cf61e-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="cf61e-164">Můžete je získat tady:</span><span class="sxs-lookup"><span data-stu-id="cf61e-164">You can get these from here:</span></span>

- [<span data-ttu-id="cf61e-165">Stažení sady Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="cf61e-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Stažení sady Visual Studio 2008 SP1")
- [<span data-ttu-id="cf61e-166">Stažení. vsdoc hotfix pro Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="cf61e-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Stažení. vsdoc hotfix pro Visual Studio 2008 SP1")

<span data-ttu-id="cf61e-167">Visual Studio 2010 podporuje soubory. vsdoc bez dalších oprav.</span><span class="sxs-lookup"><span data-stu-id="cf61e-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="cf61e-168">Použití ASP.NET AJAX z CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="cf61e-169">Při použití ASP.NET 4 můžete přesměrovat všechny požadavky na skripty ASP.NET Framework do sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="cf61e-170">Načtení skriptů z CDN místo místního webového serveru může podstatně zlepšit výkon veřejných websites ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cf61e-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="cf61e-171">Pomocí vlastnosti EnableCDN ScriptManager přesměrujte všechny požadavky skriptu ASP.NET Framework na Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="cf61e-172">Použití jQuery z CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="cf61e-173">Můžete použít skripty jQuery hostované v CDN ve vaší webové aplikaci přidáním následujícího elementu skriptu na stránku:</span><span class="sxs-lookup"><span data-stu-id="cf61e-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="cf61e-174">CDN obsahuje také verzi minifikovaného skriptu jQuery, kterou můžete použít v následujícím elementu:</span><span class="sxs-lookup"><span data-stu-id="cf61e-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="cf61e-175">Chcete-li, aby vaše stránka mohla být načítána z místní cesty na vašem vlastním webu v případě, že CDN není k dispozici, přidejte následující element hned za element odkazující na síť CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="cf61e-176">Následující vzorová stránka používá verzi CDN knihovny jQuery (s Fallback pro místní kopírování) k zobrazení obsahu prvku div při kliknutí na tlačítko.</span><span class="sxs-lookup"><span data-stu-id="cf61e-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="cf61e-177">Další informace o jQuery a stažení místní kopie jQuery získáte návštěvou webu [jQuery](http://jquery.com/) .</span><span class="sxs-lookup"><span data-stu-id="cf61e-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="cf61e-178">Použití uživatelského rozhraní jQuery z CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="cf61e-179">CDN je také hostitelem knihovny uživatelského rozhraní jQuery.</span><span class="sxs-lookup"><span data-stu-id="cf61e-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="cf61e-180">Knihovna uživatelského rozhraní jQuery obsahuje bohatou sadu widgetů a efektů, které můžete použít ve svých aplikacích ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cf61e-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="cf61e-181">Například následující stránka ukazuje, jak lze použít uživatelské rozhraní jQuery DatePicker v kontextu aplikace webových formulářů ASP.NET pro zobrazení místního kalendáře:</span><span class="sxs-lookup"><span data-stu-id="cf61e-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="cf61e-182">Když přesunete fokus na textové pole pomocí klávesnice, zobrazí se kalendář:</span><span class="sxs-lookup"><span data-stu-id="cf61e-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Automaticky otevíraná okna vytvořená pomocí DatePicker](overview/_static/image1.png)

<span data-ttu-id="cf61e-184">Všimněte si, že do výše uvedeného kódu musíte zahrnout tři soubory ze sítě CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="cf61e-185">Knihovna jQuery knihovna &mdash; uživatelského rozhraní jQuery závisí na knihovně jQuery.</span><span class="sxs-lookup"><span data-stu-id="cf61e-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="cf61e-186">Knihovnu jQuery je nutné přidat na stránku před přidáním knihovny uživatelského rozhraní jQuery.</span><span class="sxs-lookup"><span data-stu-id="cf61e-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="cf61e-187">Knihovna uživatelského rozhraní jQuery &mdash; Knihovna rozhraní jQuery obsahuje všechny efekty a pomůcky uživatelského rozhraní jQuery, jako je widget DatePicker použitý na stránce výše.</span><span class="sxs-lookup"><span data-stu-id="cf61e-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="cf61e-188">Motiv uživatelského rozhraní jQuery &mdash; : uživatelské rozhraní jQuery podporuje různé motivy.</span><span class="sxs-lookup"><span data-stu-id="cf61e-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="cf61e-189">Výše uvedená stránka obsahuje odkaz na soubor CSS pro import motivu Redmond.</span><span class="sxs-lookup"><span data-stu-id="cf61e-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="cf61e-190">Všechny standardní motivy uživatelského rozhraní jQuery jsou hostovány v CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="cf61e-191">Na [této stránce](jquery-ui/cdnjqueryui1910.md "Uživatelské rozhraní jQuery 1.8.10 ve službě Microsoft Ajax CDN") můžete zobrazit miniatury pro každý motiv.</span><span class="sxs-lookup"><span data-stu-id="cf61e-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="cf61e-192">Další informace o knihovně uživatelského rozhraní jQuery najdete na oficiálním [webu s uživatelským rozhraním jQuery](http://jQueryUI.com "Web uživatelského rozhraní jQuery").</span><span class="sxs-lookup"><span data-stu-id="cf61e-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="cf61e-193">Soubory třetích stran na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="cf61e-194">CDN hostuje některé z nejoblíbenějších knihoven JavaScript třetích stran.</span><span class="sxs-lookup"><span data-stu-id="cf61e-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="cf61e-195">Microsoft nenárokuje vlastnictví žádné knihovny třetích stran hostované v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="cf61e-196">Vlastníci těchto knihoven mají licenci na tyto knihovny.</span><span class="sxs-lookup"><span data-stu-id="cf61e-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="cf61e-197">Všechna práva, která může být nutné stáhnout a používat tyto knihovny, jsou udělována výhradně příslušnými vlastníky autorských práv.</span><span class="sxs-lookup"><span data-stu-id="cf61e-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="cf61e-198">Vzhledem k tomu, že se nejedná o knihovny Microsoftu, společnost Microsoft neposkytuje žádné záruky ani licence k duševnímu vlastnictví (včetně žádného mlčky odvozeného patentového práva) pro knihovny třetích stran hostované v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="cf61e-199">Verze jQuery na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="cf61e-200">Následující verze jQuery jsou hostovány v CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-351"></a><span data-ttu-id="cf61e-201">jQuery verze 3.5.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-201">jQuery version 3.5.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.1.slim.min.map

#### <a name="jquery-version-350"></a><span data-ttu-id="cf61e-202">jQuery verze 3.5.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-202">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="cf61e-203">jQuery verze 3.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-203">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="cf61e-204">jQuery verze 3.4.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-204">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="cf61e-205">jQuery verze 3.3.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-205">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="cf61e-206">jQuery verze 3.2.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-206">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="cf61e-207">jQuery verze 3.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-207">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="cf61e-208">jQuery verze 3.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-208">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="cf61e-209">jQuery verze 3.1.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-209">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="cf61e-210">jQuery verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-210">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="cf61e-211">jQuery – verze 2.2.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-211">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="cf61e-212">jQuery – verze 2.2.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-212">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="cf61e-213">jQuery verze 2.2.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-213">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="cf61e-214">jQuery verze 2.2.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-214">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="cf61e-215">jQuery verze 2.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-215">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="cf61e-216">jQuery verze 2.1.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-216">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="cf61e-217">jQuery verze 2.1.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-217">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="cf61e-218">jQuery verze 2.1.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-218">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="cf61e-219">jQuery verze 2.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-219">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="cf61e-220">jQuery verze 2.1.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-220">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="cf61e-221">jQuery verze 2.0.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-221">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="cf61e-222">jQuery verze 2.0.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-222">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="cf61e-223">jQuery verze 2.0.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-223">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="cf61e-224">jQuery verze 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-224">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="cf61e-225">jQuery verze 1.12.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-225">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="cf61e-226">jQuery verze 1.12.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-226">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="cf61e-227">jQuery verze 1.12.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-227">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="cf61e-228">jQuery verze 1.12.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-228">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="cf61e-229">jQuery verze 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-229">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="cf61e-230">jQuery verze 1.11.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-230">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="cf61e-231">jQuery verze 1.11.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-231">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="cf61e-232">jQuery verze 1.11.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-232">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="cf61e-233">jQuery verze 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-233">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="cf61e-234">jQuery verze 1.10.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-234">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="cf61e-235">jQuery verze 1.10.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-235">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="cf61e-236">jQuery verze 1.10.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-236">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="cf61e-237">jQuery verze 1.9.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-237">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="cf61e-238">jQuery verze 1.9.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-238">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="cf61e-239">jQuery verze 1.8.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-239">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="cf61e-240">jQuery verze 1.8.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-240">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="cf61e-241">jQuery verze 1.8.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-241">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="cf61e-242">jQuery verze 1.8.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-242">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="cf61e-243">jQuery verze 1.7.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-243">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="cf61e-244">jQuery verze 1.7.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-244">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="cf61e-245">jQuery verze 1,7</span><span class="sxs-lookup"><span data-stu-id="cf61e-245">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="cf61e-246">jQuery verze 1.6.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-246">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="cf61e-247">jQuery verze 1.6.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-247">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="cf61e-248">jQuery verze 1.6.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-248">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="cf61e-249">jQuery verze 1.6.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-249">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="cf61e-250">jQuery verze 1,6</span><span class="sxs-lookup"><span data-stu-id="cf61e-250">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="cf61e-251">jQuery verze 2.5.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-251">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="cf61e-252">jQuery verze 1.5.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-252">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="cf61e-253">jQuery verze 1,5</span><span class="sxs-lookup"><span data-stu-id="cf61e-253">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="cf61e-254">jQuery verze 1.4.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-254">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="cf61e-255">jQuery verze 1.4.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-255">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="cf61e-256">jQuery verze 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-256">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="cf61e-257">jQuery verze 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-257">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="cf61e-258">jQuery verze 1,4</span><span class="sxs-lookup"><span data-stu-id="cf61e-258">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="cf61e-259">jQuery verze 1.3.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-259">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="cf61e-260">jQuery migrace verzí na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-260">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="cf61e-261">Následující vydání nástroje jQuery migrace jsou hostována v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-261">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="cf61e-262">jQuery migrace verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-262">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="cf61e-263">jQuery migrace verze 1.2.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-263">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="cf61e-264">jQuery migrace verze 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-264">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="cf61e-265">jQuery migrace verze 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-265">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="cf61e-266">jQuery migrace verze 1.1.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-266">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="cf61e-267">jQuery migrace verze 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-267">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="cf61e-268">Vydání uživatelského rozhraní jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-268">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="cf61e-269">Následující verze knihovny uživatelského rozhraní jQuery jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-269">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-270">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-270">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-271">1.12.1 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-271">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Uživatelské rozhraní jQuery 1.12.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-272">1.12.0 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-272">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Uživatelské rozhraní jQuery 1.12.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-273">1.11.4 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-273">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Uživatelské rozhraní jQuery 1.11.4 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-274">1.11.3 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-274">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Uživatelské rozhraní jQuery 1.11.3 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-275">1.11.2 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-275">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Uživatelské rozhraní jQuery 1.11.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-276">1.11.1 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-276">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Uživatelské rozhraní jQuery 1.11.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-277">1.11.0 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-277">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Uživatelské rozhraní jQuery 1.11.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-278">1.10.4 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-278">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Uživatelské rozhraní jQuery 1.10.4 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-279">1.10.3 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-279">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Uživatelské rozhraní jQuery 1.10.3 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-280">1.10.2 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-280">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Uživatelské rozhraní jQuery 1.10.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-281">1.10.1 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-281">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Uživatelské rozhraní jQuery 1.10.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-282">1.10.0 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-282">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Uživatelské rozhraní jQuery 1.10.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-283">1.9.2 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-283">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Uživatelské rozhraní jQuery 1.9.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-284">1.9.1 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-284">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Uživatelské rozhraní jQuery 1.9.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-285">1.9.0 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-285">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Uživatelské rozhraní jQuery 1.9.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-286">1.8.24 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-286">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Uživatelské rozhraní jQuery 1.8.24 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-287">1.8.23 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-287">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Uživatelské rozhraní jQuery 1.8.23 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-288">1.8.22 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-288">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Uživatelské rozhraní jQuery 1.8.22 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-289">1.8.21 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-289">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Uživatelské rozhraní jQuery 1.8.21 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-290">1.8.20 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-290">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Uživatelské rozhraní jQuery 1.8.20 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-291">1.8.19 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-291">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Uživatelské rozhraní jQuery 1.8.19 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-292">1.8.18 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-292">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Uživatelské rozhraní jQuery 1.8.18 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-293">1.8.17 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-293">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Uživatelské rozhraní jQuery 1.8.17 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-294">1.8.16 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-294">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Uživatelské rozhraní jQuery 1.8.16 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-295">1.8.15 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-295">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Uživatelské rozhraní jQuery 1.8.15 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-296">1.8.14 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-296">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Uživatelské rozhraní jQuery 1.8.14 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-297">1.8.13 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-297">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Uživatelské rozhraní jQuery 1.8.13 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-298">1.8.12 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-298">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Uživatelské rozhraní jQuery 1.8.12 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-299">1.8.11 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-299">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Uživatelské rozhraní jQuery 1.8.11 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-300">1.8.10 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-300">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Uživatelské rozhraní jQuery 1.8.10 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-301">1.8.9 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-301">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Uživatelské rozhraní jQuery 1.8.9 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-302">1.8.8 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-302">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Uživatelské rozhraní jQuery 1.8.8 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-303">1.8.7 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-303">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Uživatelské rozhraní jQuery 1.8.7 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-304">1.8.6 uživatelského rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="cf61e-304">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Uživatelské rozhraní jQuery 1.8.6 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-305">Uživatelské rozhraní jQuery 1.8.5</span><span class="sxs-lookup"><span data-stu-id="cf61e-305">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "Uživatelské rozhraní jQuery 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="cf61e-306">Vydání ověření jQuery na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-306">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="cf61e-307">Následující verze modulu plug-in pro [ověření jQuery](https://jqueryvalidation.org/ "Modul plug-in jQuery ověřování") jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-307">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-308">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-308">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-309">jQuery ověřit 1.19.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-309">jQuery Validate 1.19.2</span></span>](jquery-validate/cdnjqueryvalidate1192.md "1.19.2 ověření jQuery")
- [<span data-ttu-id="cf61e-310">jQuery ověřit 1.19.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-310">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "1.19.1 ověření jQuery")
- [<span data-ttu-id="cf61e-311">jQuery ověřit 1.19.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-311">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "1.19.0 ověření jQuery")
- [<span data-ttu-id="cf61e-312">jQuery ověřit 1.17.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-312">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "1.17.0 ověření jQuery")
- [<span data-ttu-id="cf61e-313">jQuery ověřit 1.16.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-313">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="cf61e-314">jQuery ověřit 1.15.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-314">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="cf61e-315">jQuery ověřit 1.15.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-315">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="cf61e-316">jQuery ověřit 1.14.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-316">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="cf61e-317">jQuery ověřit 1.13.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-317">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="cf61e-318">jQuery ověřit 1.13.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-318">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="cf61e-319">jQuery ověřit 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-319">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="cf61e-320">jQuery ověřit 1.11.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-320">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="cf61e-321">jQuery ověřit 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-321">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="cf61e-322">jQuery ověřit 1.10.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-322">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="cf61e-323">jQuery Validate 1,9</span><span class="sxs-lookup"><span data-stu-id="cf61e-323">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate verze 1.9")
- [<span data-ttu-id="cf61e-324">jQuery ověřit 1.8.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-324">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate verze 1.8.1")
- [<span data-ttu-id="cf61e-325">jQuery Validate 1,8</span><span class="sxs-lookup"><span data-stu-id="cf61e-325">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate verze 1.8")
- [<span data-ttu-id="cf61e-326">jQuery Validate 1,7</span><span class="sxs-lookup"><span data-stu-id="cf61e-326">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate verze 1.7")
- [<span data-ttu-id="cf61e-327">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="cf61e-327">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="cf61e-328">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="cf61e-328">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="cf61e-329">jQuery Mobile releases na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-329">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="cf61e-330">Následující verze knihovny jQuery Mobile Library jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-330">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-331">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-331">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-332">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="cf61e-332">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-333">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-333">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-334">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-334">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-335">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-335">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-336">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-336">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-337">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-337">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-338">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-338">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-339">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-339">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-340">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-340">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-341">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-341">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-342">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-342">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-343">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="cf61e-343">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-344">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-344">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-345">jQuery Mobile 1,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-345">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-346">jQuery Mobile 1,0 RC 2</span><span class="sxs-lookup"><span data-stu-id="cf61e-346">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-347">jQuery Mobile 1,0 RC 1</span><span class="sxs-lookup"><span data-stu-id="cf61e-347">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="cf61e-348">jQuery Mobile 1,0 Beta 3</span><span class="sxs-lookup"><span data-stu-id="cf61e-348">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 ve službě Microsoft Ajax CDN")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="cf61e-349">Vydání šablon jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-349">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="cf61e-350">Následující verze modulu plug-in šablony jQuery jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-350">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-351">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-351">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-352">jQuery Templates Beta 1</span><span class="sxs-lookup"><span data-stu-id="cf61e-352">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="cf61e-353">Vydávání cyklů jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-353">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="cf61e-354">Následující verze modulu plug-in cyklus jQuery jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-354">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-355">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-355">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-356">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="cf61e-356">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="cf61e-357">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="cf61e-357">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="cf61e-358">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="cf61e-358">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="cf61e-359">vydávané datatabulka jQuery v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-359">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="cf61e-360">Následující verze modulu plug-in pro DataTables jQuery jsou hostovány v této síti CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-360">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="cf61e-361">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-361">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-362">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="cf61e-362">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="cf61e-363">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-363">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="cf61e-364">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-364">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="cf61e-365">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-365">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="cf61e-366">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-366">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="cf61e-367">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-367">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="cf61e-368">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-368">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="cf61e-369">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-369">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="cf61e-370">Modernizr vydaných verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-370">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="cf61e-371">Následující verze [modernizr](http://www.modernizr.com "Modernizr") jsou hostované na CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-371">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="cf61e-372">JSHint vydaných verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-372">JSHint Releases on the CDN</span></span>

<span data-ttu-id="cf61e-373">Následující verze [JSHint](http://www.jshint.com "JSHint") jsou hostované na CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-373">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="cf61e-374">Vyseknutí verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-374">Knockout Releases on the CDN</span></span>

<span data-ttu-id="cf61e-375">Následující vydané verze [vyseknutí](http://www.knockoutjs.com "Tomuto") jsou hostovány v CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-375">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="cf61e-376">Globalizace verzí v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-376">Globalize Releases on the CDN</span></span>

<span data-ttu-id="cf61e-377">Následující vydání [globalizace](https://github.com/jquery/globalize "Globalizace") jsou hostovány v CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-377">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="cf61e-378">Globalizace verze 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-378">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="cf61e-379">Globalizace verze 0.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-379">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="cf61e-380">všechny jazykové verze</span><span class="sxs-lookup"><span data-stu-id="cf61e-380">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="cf61e-381">Nahraďte "{Code-Code}" požadovaným kódem jazykové verze, například globalize.culture.en-GB.js= = soubory Microsoftu na CDN = = tyto knihovny byly nahrány společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cf61e-381">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="cf61e-382">Odpověď verze v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-382">Respond Releases on the CDN</span></span>

<span data-ttu-id="cf61e-383">V CDN jsou hostované následující verze [odpovědi](https://github.com/scottjehl/Respond "Reakce") :</span><span class="sxs-lookup"><span data-stu-id="cf61e-383">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="cf61e-384">Odpověď verze 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-384">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="cf61e-385">Odpověď verze 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-385">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="cf61e-386">Odpověď verze 1.4.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-386">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="cf61e-387">Odpověď verze 1.3.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-387">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="cf61e-388">Odpověď verze 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-388">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="cf61e-389">Bootstrap vydaných verzí na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-389">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="cf61e-390">Následující verze [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") Bootstrap se hostují v CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-390">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-452"></a><span data-ttu-id="cf61e-391">Bootstrap verze 4.5.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-391">Bootstrap version 4.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.2/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-450"></a><span data-ttu-id="cf61e-392">Bootstrap verze 4.5.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-392">Bootstrap version 4.5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-441"></a><span data-ttu-id="cf61e-393">Bootstrap verze 4.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-393">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="cf61e-394">Bootstrap verze 4.3.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-394">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="cf61e-395">Bootstrap verze 4.2.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-395">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="cf61e-396">Bootstrap verze 4.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-396">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="cf61e-397">Bootstrap verze 4.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-397">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="cf61e-398">Bootstrap verze 3.4.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-398">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="cf61e-399">Bootstrap verze 3.4.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-399">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="cf61e-400">Bootstrap verze 3.3.7</span><span class="sxs-lookup"><span data-stu-id="cf61e-400">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="cf61e-401">Bootstrap verze 3.3.6</span><span class="sxs-lookup"><span data-stu-id="cf61e-401">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="cf61e-402">Bootstrap verze 3.3.5</span><span class="sxs-lookup"><span data-stu-id="cf61e-402">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="cf61e-403">Bootstrap verze 3.3.4</span><span class="sxs-lookup"><span data-stu-id="cf61e-403">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="cf61e-404">Bootstrap verze 3.3.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-404">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="cf61e-405">Bootstrap verze 3.3.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-405">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="cf61e-406">Bootstrap verze 3.3.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-406">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="cf61e-407">Bootstrap verze 3.2.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-407">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="cf61e-408">Bootstrap verze 3.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-408">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="cf61e-409">Bootstrap verze 3.1.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-409">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="cf61e-410">Bootstrap verze 3.0.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-410">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="cf61e-411">Bootstrap verze 3.0.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-411">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="cf61e-412">Bootstrap verze 3.0.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-412">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="cf61e-413">Bootstrap verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-413">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="cf61e-414">Bootstrap verze 2.3.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-414">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="cf61e-415">Bootstrap verze 2.3.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-415">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="cf61e-416">Zavedení TouchCarousel vydání na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-416">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="cf61e-417">Následující verze [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") spouštěcích TouchCarousel vydání se hostují v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-417">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="cf61e-418">Bootstrap TouchCarousel verze 0.8.0</span><span class="sxs-lookup"><span data-stu-id="cf61e-418">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="cf61e-419">Verze Hammer.js v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-419">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="cf61e-420">Následující verze [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js vydání jsou hostovány v CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-420">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="cf61e-421">2.0.4 verze Hammer.js</span><span class="sxs-lookup"><span data-stu-id="cf61e-421">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="cf61e-422">ASP.NET webové formuláře a verze AJAX v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-422">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="cf61e-423">Následující verze knihovny ASP.NET AJAX jsou hostovány v CDN.</span><span class="sxs-lookup"><span data-stu-id="cf61e-423">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="cf61e-424">Kliknutím na každý odkaz zobrazíte aktuální seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="cf61e-424">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cf61e-425">ASP.NET webové formuláře a AJAX verze 4.5.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-425">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "Webové formuláře ASP.NET a Ajax 4.5.2")
- [<span data-ttu-id="cf61e-426">ASP.NET webové formuláře a AJAX verze 4</span><span class="sxs-lookup"><span data-stu-id="cf61e-426">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "Webové formuláře ASP.NET a Ajax 4")
- [<span data-ttu-id="cf61e-427">ASP.NET AJAX verze 3,5</span><span class="sxs-lookup"><span data-stu-id="cf61e-427">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="cf61e-428">Verze ASP.NET MVC na CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-428">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="cf61e-429">Následující soubory JavaScriptu ASP.NET MVC jsou hostovány v této síti CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-429">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="cf61e-430">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-430">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="cf61e-431">ASP.NET MVC 5,1</span><span class="sxs-lookup"><span data-stu-id="cf61e-431">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="cf61e-432">ASP.NET MVC 5,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-432">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="cf61e-433">ASP.NET MVC 4,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-433">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="cf61e-434">ASP.NET MVC 3,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-434">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="cf61e-435">ASP.NET MVC 2,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-435">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="cf61e-436">ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="cf61e-436">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="cf61e-437">ASP.NET signalizace v CDN</span><span class="sxs-lookup"><span data-stu-id="cf61e-437">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="cf61e-438">Následující soubory JavaScriptu pro ASP.NET signalizaci jsou hostovány v této síti CDN:</span><span class="sxs-lookup"><span data-stu-id="cf61e-438">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="cf61e-439">Signál ASP.NET 2.2.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-439">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="cf61e-440">Signál ASP.NET 2.2.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-440">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="cf61e-441">2.2.0 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-441">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="cf61e-442">2.1.0 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-442">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="cf61e-443">2.0.3 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-443">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="cf61e-444">2.0.2 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-444">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="cf61e-445">Signál ASP.NET 2.0.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-445">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="cf61e-446">2.0.0 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-446">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="cf61e-447">Signál ASP.NET 1.1.3</span><span class="sxs-lookup"><span data-stu-id="cf61e-447">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="cf61e-448">ASP.NETový signál 1.1.2</span><span class="sxs-lookup"><span data-stu-id="cf61e-448">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="cf61e-449">Signál ASP.NET 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cf61e-449">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="cf61e-450">1.1.0 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-450">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="cf61e-451">1.0.1 signálu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cf61e-451">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="cf61e-452">Informace o podmínek použití pro CDN najdete v tématu věnovaném [podmínkám použití Microsoft Ajax CDN](https://www.asp.net/terms-of-use "Používání podmínek použití Microsoft Ajax CDN").</span><span class="sxs-lookup"><span data-stu-id="cf61e-452">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
