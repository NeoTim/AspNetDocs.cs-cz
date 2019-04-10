---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[Postup:]  Stránky technologie ASP.NET na základě informací v hlavičce protokolu HTTP mezipaměti | Dokumentace Microsoftu'
author: rick-anderson
description: V toto video pixelů na Chris ukazuje, jak zachovat stránku do výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP, na stránce. První, potenciální nadpisů HTTP...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404140"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="f0f75-104">[Postup:]  Mezipaměť stránky ASP.NET na základě informací v hlavičce protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="f0f75-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="f0f75-105">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f0f75-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f0f75-106">V toto video pixelů na Chris ukazuje, jak zachovat stránku do výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP, na stránce.</span><span class="sxs-lookup"><span data-stu-id="f0f75-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="f0f75-107">Nejprve jsou kontrolovány možných hodnot hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="f0f75-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="f0f75-108">Potom vytvoří ukázkovou stránku a pak direktivy OutputCache se používá s atributem VaryByHeader, který obsahuje hodnotu "přijmout jazyka", hlavičky protokolu HTTP, k řízení ukládání do mezipaměti podle jazyka prohlížeče uživatele.</span><span class="sxs-lookup"><span data-stu-id="f0f75-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="f0f75-109">Stránka s ukázkou je zobrazit v Internet Exploreru, která je nastavena na angličtina a pak ve Firefoxu, který je nastavený na použití francouzština.</span><span class="sxs-lookup"><span data-stu-id="f0f75-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="f0f75-110">Nakonec jsou popsány možnost přesunout definici mezipaměti CacheProfile v souboru web.config.</span><span class="sxs-lookup"><span data-stu-id="f0f75-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="f0f75-111">&#9654;Podívejte se na video (12 minut)</span><span class="sxs-lookup"><span data-stu-id="f0f75-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
