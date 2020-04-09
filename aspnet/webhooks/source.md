---
uid: webhooks/source
title: ASP.NET zdrojový kód WebHooks a balíčky NuGet | Dokumenty společnosti Microsoft
author: rick-anderson
description: Odkazy na ASP.NET zdrojový kód WebHooks a balíčky NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675325"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET zdrojový kód WebHooks a balíčky NuGet

Microsoft ASP.NET WebHooks je součástí řady modulů Microsoft ASP.NET a je hostován jako [open source projekt na GitHubu](https://github.com/aspnet/WebHooks). To znamená, že přijímáme příspěvky, ale před odesláním žádosti o přijetí se prosím podívejte na [pokyny pro příspěvky.](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)

Tato online dokumentace, kterou nyní čtete, je také hostována jako [Open Source na GitHubu](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) a také přijímá příspěvky.

## <a name="nuget-packages"></a>Balíčky NuGet

[Balíčky NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) jsou rozděleny do tří částí:

* [Běžné](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Společný balíček, který je sdílen mezi odesílateli a příjemci.

* [Odesílatel](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Sada balíčků podporujících odesílání vlastních WebHooků ostatním. Funkce pro odesílání WebHooks je podrobněji popsána v [odesílání WebHooks](sending/senders.md).

* [Přijímače](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Sada balíčků podporujících příjem WebHooks od ostatních. Funkce pro příjem WebHooks je popsána podrobněji v [příjem WebHooks](receiving/index.md).
