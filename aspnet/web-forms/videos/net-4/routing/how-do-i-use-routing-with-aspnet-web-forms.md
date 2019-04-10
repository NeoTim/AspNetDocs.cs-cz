---
uid: web-forms/videos/net-4/routing/how-do-i-use-routing-with-aspnet-web-forms
title: 'Postup: Použití směrování s webovými formuláři ASP.NET? | Dokumenty Microsoft'
author: rick-anderson
description: Chris pixelů na toto video ukazuje, jak implementovat směrování webových formulářů v technologii ASP.NET 4. Nejprve je mapování adresy URL p porovnání koncept směrování adresy URL...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: a3ab6cd9-8f71-4b73-9336-21c0de078269
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-use-routing-with-aspnet-web-forms
msc.type: video
ms.openlocfilehash: f5036d780ed4fd0dd8caabbf4badb39fd9ee2de3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59417062"
---
# <a name="how-do-i-use-routing-with-aspnet-web-forms"></a><span data-ttu-id="d41f8-105">Postup: Použití směrování s webovými formuláři ASP.NET?</span><span class="sxs-lookup"><span data-stu-id="d41f8-105">How Do I: Use Routing with ASP.NET Web Forms?</span></span>

<span data-ttu-id="d41f8-106">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d41f8-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d41f8-107">Chris pixelů na toto video ukazuje, jak implementovat směrování webových formulářů v technologii ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="d41f8-107">In this video Chris Pels shows how to implement routing for Web Forms in ASP.NET 4.</span></span> <span data-ttu-id="d41f8-108">Nejprve koncept směrování adresy URL se porovnává se mapování adresy URL na fyzickou v lokalitě.</span><span class="sxs-lookup"><span data-stu-id="d41f8-108">First, the concept of routing a URL is compared to mapping the URL to a physical file in the site.</span></span> <span data-ttu-id="d41f8-109">Potom směrování vzorku pro adresy URL je definován v souboru global.asax souboru aplikace\_spuštění obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="d41f8-109">Then, a sample route for a URL is defined in the global.asax file Application\_Start event handler.</span></span> <span data-ttu-id="d41f8-110">Trasa obsahuje parametrizované hodnotu, která může uživatel zadat v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="d41f8-110">The route contains a parameterized value that the user can enter in the URL.</span></span> <span data-ttu-id="d41f8-111">Se pak vytvoří ukázkovou stránku a hodnota parametru trasy, které je extrahován na stránce\_obslužná rutina události Load.</span><span class="sxs-lookup"><span data-stu-id="d41f8-111">A sample page is then created and the route parameter value is extracted in the Page\_Load event handler.</span></span> <span data-ttu-id="d41f8-112">V dalším kroku Druhá trasa je definován, který má více parametrů a trasy na stejnou stránku jako počáteční trasy.</span><span class="sxs-lookup"><span data-stu-id="d41f8-112">Next, a second route is defined that has multiple parameters and routes to the same page as the initial route.</span></span> <span data-ttu-id="d41f8-113">Na stránce\_obslužná rutina události zatížení rozbalen a extrahovat hodnotu parametru další trasy a zobrazit různé informace, podle toho, jaké hodnoty byly předány na stránku.</span><span class="sxs-lookup"><span data-stu-id="d41f8-113">The Page\_Load event handler is expanded to extract the additional route parameter value and display different information depending upon what values have been passed to the page.</span></span>

[<span data-ttu-id="d41f8-114">&#9654;Podívejte se na video (15 minut)</span><span class="sxs-lookup"><span data-stu-id="d41f8-114">&#9654; Watch video (15 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-routing-with-aspnet-web-forms)

> [!div class="step-by-step"]
> <span data-ttu-id="d41f8-115">[Předchozí](aspnet-4-quick-hit-outbound-webforms-routing.md)
> [další](how-do-i-work-with-urls-in-aspnet-routing.md)</span><span class="sxs-lookup"><span data-stu-id="d41f8-115">[Previous](aspnet-4-quick-hit-outbound-webforms-routing.md)
[Next](how-do-i-work-with-urls-in-aspnet-routing.md)</span></span>
