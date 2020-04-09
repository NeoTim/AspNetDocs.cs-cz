---
uid: webhooks/diagnostics/logging
title: ASP.NET Protokolování WebHooks | Dokumenty společnosti Microsoft
author: rick-anderson
description: Jak se přihlásit ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675348"
---
# <a name="aspnet-webhooks-logging"></a>protokolování ASP.NET WebHooks

Microsoft ASP.NET WebHooks používá protokolování jako způsob hlášení problémů a problémů. Ve výchozím nastavení protokoly jsou zapsány pomocí [System.Diagnostics.Trace,](https://msdn.microsoft.com/library/system.diagnostics.trace) kde mohou být manged pomocí [naslouchací procesy trasování](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) jako jakýkoli jiný datový proud protokolu.

Při nasazování webové aplikace jako Azure Web App, protokoly jsou automaticky zvedl a lze spravovat společně s jakýmkoli jiným [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) protokolování. Podrobnosti najdete v tématu [Povolení protokolování diagnostiky pro webové aplikace ve službě Azure App Service.](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Kromě toho protokoly lze získat přímo z vnitřní Visual Studio, jak je popsáno v [Řešení potíží s webovou aplikací ve službě Azure App Service pomocí Sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Přesměrování protokolů

Namísto zápisu protokolů do [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), je možné poskytnout alternativní implementaci protokolování, která se může přihlásit přímo do správce protokolu, jako je [Log4Net](http://logging.apache.org/log4net/) a [NLog](http://nlog-project.org/). Jednoduše poskytněte implementaci [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) a zaregistrujte jej pomocí vstřikovaného stroje závislostí podle vašeho výběru a bude vyzvednut společností Microsoft ASP.NET WebHooks. Podrobnosti naleznete [v tématu Vkládání závislostí v ASP.NET webové rozhraní API 2.](https://www.asp.net/web-api/overview/advanced/dependency-injection)
