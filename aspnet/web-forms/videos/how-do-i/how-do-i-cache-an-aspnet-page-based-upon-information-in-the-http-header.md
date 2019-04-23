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
ms.lasthandoff: 04/17/2019
ms.locfileid: "59404140"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a>[Postup:]  Mezipaměť stránky ASP.NET na základě informací v hlavičce protokolu HTTP

podle [Chris pixelů na](https://twitter.com/chrispels)

V toto video pixelů na Chris ukazuje, jak zachovat stránku do výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP, na stránce. Nejprve jsou kontrolovány možných hodnot hlavičky protokolu HTTP. Potom vytvoří ukázkovou stránku a pak direktivy OutputCache se používá s atributem VaryByHeader, který obsahuje hodnotu "přijmout jazyka", hlavičky protokolu HTTP, k řízení ukládání do mezipaměti podle jazyka prohlížeče uživatele. Stránka s ukázkou je zobrazit v Internet Exploreru, která je nastavena na angličtina a pak ve Firefoxu, který je nastavený na použití francouzština. Nakonec jsou popsány možnost přesunout definici mezipaměti CacheProfile v souboru web.config.

[&#9654;Podívejte se na video (12 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
