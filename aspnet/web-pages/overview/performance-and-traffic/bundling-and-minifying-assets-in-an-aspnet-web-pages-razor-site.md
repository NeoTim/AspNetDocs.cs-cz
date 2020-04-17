---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Svazování a minifying aktiva v ASP.NET webových stránek (Břitva) stránek | Dokumenty společnosti Microsoft
author: rick-anderson
description: Svazování a minifikace jsou způsoby, jak vaše stránky rychleji. Sdružování umožňuje kombinovat více souborů JavaScript ( .js ) nebo více kaskádových stylů (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539910"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="67973-104">Sdružování a minifikace prostředků na webu s webovými stránkami ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="67973-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="67973-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="67973-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="67973-106">Svazování a minifikace jsou způsoby, jak vaše stránky rychleji.</span><span class="sxs-lookup"><span data-stu-id="67973-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="67973-107">Sdružování umožňuje kombinovat více souborů JavaScriptu (*js*) nebo více kaskádových souborů stylů *(CSS),* aby je bylo možné stáhnout jako jednotku, nikoli jako jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="67973-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="67973-108">Minifikace vytlačuje prázdné znaky a provádí jiné typy komprese, aby se stažené soubory jako malé možné.</span><span class="sxs-lookup"><span data-stu-id="67973-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="67973-109">RC verze ASP.NET webových stránek 2 nepodporuje sdružování a minification, protože balíček, který obsahuje požadované prvky ještě není k dispozici v Microsoft WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="67973-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="67973-110">Omlouváme se za tyto nepříjemnosti.</span><span class="sxs-lookup"><span data-stu-id="67973-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="67973-111">Očekává se, že balíček bude k dispozici v konečné verzi ASP.NET Webových stránek 2 a WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="67973-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
