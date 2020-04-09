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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="bc341-103">ASP.NET zdrojový kód WebHooks a balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="bc341-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="bc341-104">Microsoft ASP.NET WebHooks je součástí řady modulů Microsoft ASP.NET a je hostován jako [open source projekt na GitHubu](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="bc341-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="bc341-105">To znamená, že přijímáme příspěvky, ale před odesláním žádosti o přijetí se prosím podívejte na [pokyny pro příspěvky.](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)</span><span class="sxs-lookup"><span data-stu-id="bc341-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="bc341-106">Tato online dokumentace, kterou nyní čtete, je také hostována jako [Open Source na GitHubu](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) a také přijímá příspěvky.</span><span class="sxs-lookup"><span data-stu-id="bc341-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="bc341-107">Balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="bc341-107">NuGet packages</span></span>

<span data-ttu-id="bc341-108">[Balíčky NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) jsou rozděleny do tří částí:</span><span class="sxs-lookup"><span data-stu-id="bc341-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="bc341-109">[Běžné](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Společný balíček, který je sdílen mezi odesílateli a příjemci.</span><span class="sxs-lookup"><span data-stu-id="bc341-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="bc341-110">[Odesílatel](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Sada balíčků podporujících odesílání vlastních WebHooků ostatním.</span><span class="sxs-lookup"><span data-stu-id="bc341-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="bc341-111">Funkce pro odesílání WebHooks je podrobněji popsána v [odesílání WebHooks](sending/senders.md).</span><span class="sxs-lookup"><span data-stu-id="bc341-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="bc341-112">[Přijímače](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Sada balíčků podporujících příjem WebHooks od ostatních.</span><span class="sxs-lookup"><span data-stu-id="bc341-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="bc341-113">Funkce pro příjem WebHooks je popsána podrobněji v [příjem WebHooks](receiving/index.md).</span><span class="sxs-lookup"><span data-stu-id="bc341-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
