---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Zobrazení videa v ASP.NET Web Pages lokality (Razor) | Dokumentace Microsoftu
author: Rick-Anderson
description: Tato kapitola popisuje zobrazení videa ASP.NET Web Pages se stránkou pro syntaxi Razor.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 8f4b7186ae5c7b7b384ebcb23f7c9ad65caeb0bd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068863"
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a5238-103">Zobrazení videa na webu rozhraní ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="a5238-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="a5238-104">podle [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a5238-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a5238-105">Tento článek vysvětluje, jak použít přehrávač videa (média) na webu rozhraní ASP.NET Web Pages (Razor) umožňuje uživatelům zobrazit videa, které jsou uloženy na serveru.</span><span class="sxs-lookup"><span data-stu-id="a5238-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="a5238-106">ASP.NET Web Pages se syntaxí Razor umožňuje přehrát Flash (*SWF*), Media Player (*WMV*) a Silverlight (*.xap*) videa.</span><span class="sxs-lookup"><span data-stu-id="a5238-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="a5238-107">Co se dozvíte:</span><span class="sxs-lookup"><span data-stu-id="a5238-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a5238-108">Jak zvolit přehrávač videa.</span><span class="sxs-lookup"><span data-stu-id="a5238-108">How to choose a video player.</span></span>
> - <span data-ttu-id="a5238-109">Jak přidat video do webové stránky.</span><span class="sxs-lookup"><span data-stu-id="a5238-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="a5238-110">Jak nastavit atributy přehrávač videa.</span><span class="sxs-lookup"><span data-stu-id="a5238-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="a5238-111">Jedná se o syntaxi ASP.NET Razor stránky funkcí představených v následujícím článku:</span><span class="sxs-lookup"><span data-stu-id="a5238-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a5238-112">`Video` Pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="a5238-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a5238-113">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="a5238-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a5238-114">Rozhraní ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="a5238-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a5238-115">Služba WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="a5238-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="a5238-116">V tomto kurzu funguje taky pomocí služby WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="a5238-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="a5238-117">Úvod</span><span class="sxs-lookup"><span data-stu-id="a5238-117">Introduction</span></span>

<span data-ttu-id="a5238-118">Můžete chtít zobrazit videa ve vaší lokalitě.</span><span class="sxs-lookup"><span data-stu-id="a5238-118">You might want to display a video on your site.</span></span> <span data-ttu-id="a5238-119">Jedním ze způsobů, který je propojení na lokalitu, která už má video, jako je YouTube.</span><span class="sxs-lookup"><span data-stu-id="a5238-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="a5238-120">Pokud chcete vložit video z těchto webů přímo do vašich vlastních stránek, můžete obvykle se zobrazí kód HTML z lokality a potom ho zkopírujete do stránky.</span><span class="sxs-lookup"><span data-stu-id="a5238-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="a5238-121">Například následující příklad ukazuje postup vložení YouTube videa:</span><span class="sxs-lookup"><span data-stu-id="a5238-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="a5238-122">Pokud chcete přehrát video, které je na svůj vlastní web (ne na veřejný web sdílení videí), nelze propojit přímo pomocí vloženého kódu tímto způsobem.</span><span class="sxs-lookup"><span data-stu-id="a5238-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="a5238-123">Však můžete přehrát videa z webu pomocí `Video` pomocné rutiny, která vykresluje media player přímo na stránce.</span><span class="sxs-lookup"><span data-stu-id="a5238-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="a5238-124">Výběr přehrávače videa</span><span class="sxs-lookup"><span data-stu-id="a5238-124">Choosing a Video Player</span></span>

<span data-ttu-id="a5238-125">Existuje mnoho formátů videosouborů a každý formát obvykle vyžaduje jiný přehrávač a způsobu, jak nakonfigurovat přehrávač.</span><span class="sxs-lookup"><span data-stu-id="a5238-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="a5238-126">Na stránkách ASP.NET Razor můžete přehrát video webovou stránku pomocí `Video` pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="a5238-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="a5238-127">`Video` Pomocné rutiny zjednodušuje proces vkládání videí na webové stránce, protože automaticky generuje `object` a `embed` elementy HTML, které se běžně používají ke přidat video do stránky.</span><span class="sxs-lookup"><span data-stu-id="a5238-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="a5238-128">`Video` Pomocné rutiny podporuje následující přehrávače médií:</span><span class="sxs-lookup"><span data-stu-id="a5238-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="a5238-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="a5238-129">Adobe Flash</span></span>
- <span data-ttu-id="a5238-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="a5238-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="a5238-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="a5238-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="a5238-132">Přehrávače pro Flash</span><span class="sxs-lookup"><span data-stu-id="a5238-132">The Flash Player</span></span>

<span data-ttu-id="a5238-133">`Flash` Aktér `Video` pomocné rutiny umožňují přehrávat animace Flash videa (*SWF* soubory) na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="a5238-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="a5238-134">Přinejmenším budete muset zadat cestu k souboru videa.</span><span class="sxs-lookup"><span data-stu-id="a5238-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="a5238-135">Pokud chcete zadat pouze cestu, hráč používá výchozí hodnoty, které jsou nastavené v aktuální verzi pracovat bez velkých příprav.</span><span class="sxs-lookup"><span data-stu-id="a5238-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="a5238-136">Výchozí nastavení jsou:</span><span class="sxs-lookup"><span data-stu-id="a5238-136">Typical default settings are:</span></span>

- <span data-ttu-id="a5238-137">Video se zobrazí pomocí jeho výchozí šířky a výšky a bez barvu pozadí.</span><span class="sxs-lookup"><span data-stu-id="a5238-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="a5238-138">Video se přehraje automaticky při načtení stránky.</span><span class="sxs-lookup"><span data-stu-id="a5238-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="a5238-139">Video smyčky nepřetržitě, dokud explicitně je zastavená.</span><span class="sxs-lookup"><span data-stu-id="a5238-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="a5238-140">Video se škálovat zobrazíte všechna videa, místo oříznutí videa podle určité velikosti.</span><span class="sxs-lookup"><span data-stu-id="a5238-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="a5238-141">Video se přehraje v okně.</span><span class="sxs-lookup"><span data-stu-id="a5238-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="a5238-142">MediaPlayer Player</span><span class="sxs-lookup"><span data-stu-id="a5238-142">The MediaPlayer Player</span></span>

<span data-ttu-id="a5238-143">`MediaPlayer` Aktér `Video` pomocné rutiny umožňuje přehrát Windows Media Video (*WMV* soubory), Windows Media audio (*.wma* soubory) a MP3 (*.mp3* soubory) na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="a5238-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="a5238-144">Musí obsahovat cestu k souboru médií k přehrání; všechny ostatní parametry jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="a5238-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="a5238-145">Pokud chcete zadat pouze cestu, přehrávač používá výchozí nastavení nastavte pomocí aktuální verze MediaPlayer, jako je třeba:</span><span class="sxs-lookup"><span data-stu-id="a5238-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="a5238-146">Video se zobrazí pomocí jeho výchozí šířka a výška.</span><span class="sxs-lookup"><span data-stu-id="a5238-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="a5238-147">Video se přehraje automaticky při načtení stránky.</span><span class="sxs-lookup"><span data-stu-id="a5238-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="a5238-148">Video se přehraje jednou (ho nebude opakovat).</span><span class="sxs-lookup"><span data-stu-id="a5238-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="a5238-149">Přehrávač zobrazuje úplnou sadu ovládacích prvků v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a5238-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="a5238-150">Video se přehraje v okně.</span><span class="sxs-lookup"><span data-stu-id="a5238-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="a5238-151">Přehrávač Silverlight</span><span class="sxs-lookup"><span data-stu-id="a5238-151">The Silverlight Player</span></span>

<span data-ttu-id="a5238-152">`Silverlight` Aktér `Video` pomocné rutiny umožňuje přehrát Windows Media Video (*WMV* soubory), Windows Media zvuku (*.wma* soubory) a MP3 (*.mp3* soubory).</span><span class="sxs-lookup"><span data-stu-id="a5238-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="a5238-153">Je nutné nastavit parametr cesty tak, aby odkazoval na balíček aplikace založené na technologii Silverlight (*.xap* souboru).</span><span class="sxs-lookup"><span data-stu-id="a5238-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="a5238-154">Je třeba také nastavit parametry šířku a výšku.</span><span class="sxs-lookup"><span data-stu-id="a5238-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="a5238-155">Všechny ostatní parametry jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="a5238-155">All other parameters are optional.</span></span> <span data-ttu-id="a5238-156">Při použití technologie Silverlight přehrávače videa, pokud nastavíte jenom požadované parametry, zobrazí Silverlight přehrávač videa bez barvu pozadí.</span><span class="sxs-lookup"><span data-stu-id="a5238-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="a5238-157">V případě, že ještě neznáte Silverlight: *.xap* soubor je komprimovaný soubor, který obsahuje rozložení podle pokynů v *.xaml* souboru spravovaného kódu v sestavení a volitelné materiály.</span><span class="sxs-lookup"><span data-stu-id="a5238-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="a5238-158">Můžete vytvořit *.xap* souboru v sadě Visual Studio jako projekt aplikace Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a5238-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="a5238-159">`Silverlight` Přehrávač videa používá jak nastavení, které zadáte pro přehrávač a nastavení, které jsou součástí *.xap* souboru.</span><span class="sxs-lookup"><span data-stu-id="a5238-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="a5238-160">Typy MIME</span><span class="sxs-lookup"><span data-stu-id="a5238-160">MIME Types</span></span>
> 
> <span data-ttu-id="a5238-161">Když prohlížeč stáhne soubor, prohlížeče, zajišťuje, typ souboru odpovídá typ MIME zadaný pro dokument, který se vykresluje.</span><span class="sxs-lookup"><span data-stu-id="a5238-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="a5238-162">Typ MIME je typ nebo médium typ obsahu souboru.</span><span class="sxs-lookup"><span data-stu-id="a5238-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="a5238-163">`Video` Pomocné rutiny používá následující typy MIME:</span><span class="sxs-lookup"><span data-stu-id="a5238-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="a5238-164">Playing Flash (.swf) Videos</span><span class="sxs-lookup"><span data-stu-id="a5238-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="a5238-165">Tento postup ukazuje, jak přehrávat animace Flash video s názvem *sample.swf*.</span><span class="sxs-lookup"><span data-stu-id="a5238-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="a5238-166">V postupu se předpokládá, že máte složku s názvem *média* na váš web a že *SWF* soubor je v této složce.</span><span class="sxs-lookup"><span data-stu-id="a5238-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="a5238-167">Přidejte knihovnu ASP.NET Web Helpers na váš web, jak je popsáno v [instalace pomocné rutiny na webu technologie ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě nepřidali.</span><span class="sxs-lookup"><span data-stu-id="a5238-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="a5238-168">Na webu, přidejte na stránku a pojmenujte ho *FlashVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a5238-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="a5238-169">Přidejte následující kód na stránku:</span><span class="sxs-lookup"><span data-stu-id="a5238-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="a5238-170">Spuštění stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a5238-170">Run the page in a browser.</span></span> <span data-ttu-id="a5238-171">(Ujistěte se, že je vybrána na stránce v **soubory** pracovního prostoru před jeho spuštěním.) Na stránce se zobrazí a video se přehraje automaticky.</span><span class="sxs-lookup"><span data-stu-id="a5238-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="a5238-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span><span class="sxs-lookup"><span data-stu-id="a5238-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="a5238-173">Můžete nastavit `quality` parametr pro Flash video a `low`, `autolow`, `autohigh`, `medium`, `high`, a `best`:</span><span class="sxs-lookup"><span data-stu-id="a5238-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="a5238-174">Můžete změnit na Flash video přehrát na konkrétní velikosti pomocí `scale` parametr, který můžete nastavit takto:</span><span class="sxs-lookup"><span data-stu-id="a5238-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="a5238-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="a5238-175">`showall`.</span></span> <span data-ttu-id="a5238-176">Díky tomu celé video viditelné při zachování původního poměru stran obrázku.</span><span class="sxs-lookup"><span data-stu-id="a5238-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="a5238-177">Však může skončit s ohraničení na každé straně.</span><span class="sxs-lookup"><span data-stu-id="a5238-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="a5238-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="a5238-178">`noorder`.</span></span> <span data-ttu-id="a5238-179">To při zachování poměru stran původní škáluje videa, ale může být oříznuté.</span><span class="sxs-lookup"><span data-stu-id="a5238-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="a5238-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="a5238-180">`exactfit`.</span></span> <span data-ttu-id="a5238-181">Díky tomu celé video viditelné bez zachování původní poměr stran, ale může dojít k narušení.</span><span class="sxs-lookup"><span data-stu-id="a5238-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="a5238-182">Pokud nezadáte `scale` parametr celé video se nebude zobrazovat a původní poměr stran obrázku se nebude udržovat bez jakékoli oříznutí.</span><span class="sxs-lookup"><span data-stu-id="a5238-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="a5238-183">Následující příklad ukazuje způsob použití `scale` parametr:</span><span class="sxs-lookup"><span data-stu-id="a5238-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="a5238-184">Flash player podporuje video režim nastavení s názvem `windowMode`.</span><span class="sxs-lookup"><span data-stu-id="a5238-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="a5238-185">Tento parametr můžete nastavit `window`, `opaque`, a `transparent`.</span><span class="sxs-lookup"><span data-stu-id="a5238-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="a5238-186">Ve výchozím nastavení `windowMode` je nastavena na `window`, která zobrazí video v samostatném okně na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="a5238-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="a5238-187">`opaque` Nastavení skryje všechno, co se za video na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="a5238-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="a5238-188">`transparent` Umožní její nastavení zajistit na pozadí webovou stránku zobrazit prostřednictvím videa, za předpokladu, že libovolné části videa je transparentní.</span><span class="sxs-lookup"><span data-stu-id="a5238-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="a5238-189">Přehrávání MediaPlayer (*WMV*) videa</span><span class="sxs-lookup"><span data-stu-id="a5238-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="a5238-190">Následující postup ukazuje, jak k přehrání videa Media okno s názvem *sample.wmv* , který je *média* složky.</span><span class="sxs-lookup"><span data-stu-id="a5238-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="a5238-191">Přidejte knihovnu ASP.NET Web Helpers na váš web, jak je popsáno v [instalace pomocné rutiny na webu technologie ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste tak již neučinili.</span><span class="sxs-lookup"><span data-stu-id="a5238-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="a5238-192">Vytvoří novou stránku s názvem *MediaPlayerVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a5238-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="a5238-193">Přidejte následující kód na stránku:</span><span class="sxs-lookup"><span data-stu-id="a5238-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="a5238-194">Spuštění stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a5238-194">Run the page in a browser.</span></span> <span data-ttu-id="a5238-195">Video načte a přehraje automaticky.</span><span class="sxs-lookup"><span data-stu-id="a5238-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="a5238-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span><span class="sxs-lookup"><span data-stu-id="a5238-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="a5238-197">Můžete nastavit `playCount` na celé číslo, která určuje, kolikrát Pokud chcete přehrát video automaticky:</span><span class="sxs-lookup"><span data-stu-id="a5238-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="a5238-198">`uiMode` Parametr umožňuje určit, jaké ovládací prvky zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a5238-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="a5238-199">Můžete nastavit `uiMode` k `invisible`, `none`, `mini`, nebo `full`.</span><span class="sxs-lookup"><span data-stu-id="a5238-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="a5238-200">Pokud nezadáte `uiMode` parametr, bude se na video zobrazí se stavové okno hledání panelu, ovládací prvek tlačítka a ovládání hlasitosti kromě grafického okna.</span><span class="sxs-lookup"><span data-stu-id="a5238-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="a5238-201">Tyto ovládací prvky se zobrazí také v případě použití přehrávače pro přehrání zvukového souboru.</span><span class="sxs-lookup"><span data-stu-id="a5238-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="a5238-202">Tady je příklad, jak používat `uiMode` parametr:</span><span class="sxs-lookup"><span data-stu-id="a5238-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="a5238-203">Ve výchozím nastavení je zvuk na při přehrávání videa.</span><span class="sxs-lookup"><span data-stu-id="a5238-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="a5238-204">Nastavením může ztlumit zvuk `mute` parametr na hodnotu true:</span><span class="sxs-lookup"><span data-stu-id="a5238-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="a5238-205">Hlasitost videa MediaPlayer můžete řídit tak, že nastavíte `volume` parametr na hodnotu mezi 0 a 100.</span><span class="sxs-lookup"><span data-stu-id="a5238-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="a5238-206">Výchozí hodnota je 50.</span><span class="sxs-lookup"><span data-stu-id="a5238-206">The default value is 50.</span></span> <span data-ttu-id="a5238-207">Tady je příklad:</span><span class="sxs-lookup"><span data-stu-id="a5238-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="a5238-208">Přehrávání videa technologie Silverlight</span><span class="sxs-lookup"><span data-stu-id="a5238-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="a5238-209">Tento postup ukazuje, jak k přehrání videa, které jsou obsaženy v technologii Silverlight *.xap* stránka, která je ve složce s názvem *média*.</span><span class="sxs-lookup"><span data-stu-id="a5238-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="a5238-210">Přidejte knihovnu ASP.NET Web Helpers na váš web, jak je popsáno v [instalace pomocné rutiny na webu technologie ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste tak již neučinili.</span><span class="sxs-lookup"><span data-stu-id="a5238-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="a5238-211">Vytvoří novou stránku s názvem *SilverlightVideo.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a5238-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="a5238-212">Přidejte následující kód na stránku:</span><span class="sxs-lookup"><span data-stu-id="a5238-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="a5238-213">Spuštění stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a5238-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="a5238-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span><span class="sxs-lookup"><span data-stu-id="a5238-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a5238-215">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="a5238-215">Additional Resources</span></span>


<span data-ttu-id="a5238-216">[Přehled technologie Silverlight](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="a5238-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="a5238-217">Atributy značky Flash OBJEKT a vložení</span><span class="sxs-lookup"><span data-stu-id="a5238-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="a5238-218">[Windows Media Player 11 SDK PARAM značky](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="a5238-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
