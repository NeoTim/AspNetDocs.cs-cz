---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: Průvodce rozhraním API center signalr ASP.NET - server (C#) | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod do programování na straně serveru ASP.NET SignalR Hubs API pro SignalR verze 2, s ukázkami kódu demonstrujícími...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676186"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="d4f14-103">Průvodce rozhraním API center ASP.NET SignalR – server (C#)</span><span class="sxs-lookup"><span data-stu-id="d4f14-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="d4f14-104">podle [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d4f14-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d4f14-105">Tento dokument poskytuje úvod do programování na straně serveru ASP.NET rozhraní API signalr hubů pro SignalR verze 2, s ukázkami kódu, které ukazují běžné možnosti.</span><span class="sxs-lookup"><span data-stu-id="d4f14-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="d4f14-106">Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server.</span><span class="sxs-lookup"><span data-stu-id="d4f14-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d4f14-107">V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d4f14-108">V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="d4f14-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d4f14-109">SignalR se postará o všechny klient-to-server instalatérské pro vás.</span><span class="sxs-lookup"><span data-stu-id="d4f14-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="d4f14-110">SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d4f14-111">Úvod do SignalR, rozbočovače a trvalá připojení naleznete [v tématu Úvod do SignalR 2](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d4f14-112">Verze softwaru použité v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="d4f14-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="d4f14-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d4f14-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="d4f14-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d4f14-114">.NET 4.5</span></span>
> - <span data-ttu-id="d4f14-115">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="d4f14-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="d4f14-116">Verze tématu</span><span class="sxs-lookup"><span data-stu-id="d4f14-116">Topic versions</span></span>
> 
> <span data-ttu-id="d4f14-117">Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="d4f14-118">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="d4f14-118">Questions and comments</span></span>
> 
> <span data-ttu-id="d4f14-119">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="d4f14-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d4f14-120">Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="d4f14-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="d4f14-121">Přehled</span><span class="sxs-lookup"><span data-stu-id="d4f14-121">Overview</span></span>

<span data-ttu-id="d4f14-122">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="d4f14-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="d4f14-123">Jak zaregistrovat middleware SignalR</span><span class="sxs-lookup"><span data-stu-id="d4f14-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="d4f14-124">Adresa URL /signalr</span><span class="sxs-lookup"><span data-stu-id="d4f14-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="d4f14-125">Konfigurace možností SignalR</span><span class="sxs-lookup"><span data-stu-id="d4f14-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="d4f14-126">Jak vytvořit a používat třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="d4f14-127">Životnost objektu centra</span><span class="sxs-lookup"><span data-stu-id="d4f14-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="d4f14-128">Camel-caseing z hubjména v javascriptových klientech</span><span class="sxs-lookup"><span data-stu-id="d4f14-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="d4f14-129">Více rozbočovačů</span><span class="sxs-lookup"><span data-stu-id="d4f14-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="d4f14-130">Rozbočovače silného typu</span><span class="sxs-lookup"><span data-stu-id="d4f14-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="d4f14-131">Jak definovat metody ve třídě Hub, které mohou klienti volat</span><span class="sxs-lookup"><span data-stu-id="d4f14-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="d4f14-132">Camel-caseing názvů metod v javascriptových klientech</span><span class="sxs-lookup"><span data-stu-id="d4f14-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="d4f14-133">Kdy provést asynchronně</span><span class="sxs-lookup"><span data-stu-id="d4f14-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="d4f14-134">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="d4f14-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="d4f14-135">Hlášení průběhu z vyvolání metody centra</span><span class="sxs-lookup"><span data-stu-id="d4f14-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="d4f14-136">Jak volat klientské metody z třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="d4f14-137">Výběr klientů, kteří budou přijímat vzdálené volání procedur</span><span class="sxs-lookup"><span data-stu-id="d4f14-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="d4f14-138">Žádné ověření v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="d4f14-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="d4f14-139">Porovnávání názvů metod bez malých a velkých písmen</span><span class="sxs-lookup"><span data-stu-id="d4f14-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="d4f14-140">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="d4f14-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="d4f14-141">Jak spravovat členství ve skupině z třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="d4f14-142">Asynchronní provádění metod Add and Remove</span><span class="sxs-lookup"><span data-stu-id="d4f14-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="d4f14-143">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="d4f14-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="d4f14-144">Skupiny pro jednoho uživatele</span><span class="sxs-lookup"><span data-stu-id="d4f14-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="d4f14-145">Jak zpracovat události životnosti připojení ve třídě Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="d4f14-146">Když OnConnected, OnDisconnected a OnReconnected se nazývají</span><span class="sxs-lookup"><span data-stu-id="d4f14-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="d4f14-147">Stav volajícího není naplněn.</span><span class="sxs-lookup"><span data-stu-id="d4f14-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="d4f14-148">Jak získat informace o klientovi z Context vlastnost</span><span class="sxs-lookup"><span data-stu-id="d4f14-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="d4f14-149">Jak předat stav mezi klienty a třídou Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="d4f14-150">Jak zpracovat chyby ve třídě Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="d4f14-151">Jak volat metody klienta a spravovat skupiny mimo třídu Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="d4f14-152">Volání klientských metod</span><span class="sxs-lookup"><span data-stu-id="d4f14-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="d4f14-153">Správa členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="d4f14-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="d4f14-154">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="d4f14-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="d4f14-155">Jak přizpůsobit kanál Rozbočovače</span><span class="sxs-lookup"><span data-stu-id="d4f14-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="d4f14-156">Dokumentaci k programování klientů naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="d4f14-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="d4f14-157">SignalR Hubs API Guide - Klient JavaScript</span><span class="sxs-lookup"><span data-stu-id="d4f14-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="d4f14-158">Průvodce rozhraním API hubů SignalR – klient .NET</span><span class="sxs-lookup"><span data-stu-id="d4f14-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="d4f14-159">Součásti serveru pro SignalR 2 jsou k dispozici pouze v rozhraní .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d4f14-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="d4f14-160">Servery se systémem .NET 4.0 musí používat SignalR v1.x.</span><span class="sxs-lookup"><span data-stu-id="d4f14-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="d4f14-161">Jak zaregistrovat middleware SignalR</span><span class="sxs-lookup"><span data-stu-id="d4f14-161">How to register SignalR middleware</span></span>

<span data-ttu-id="d4f14-162">Chcete-li definovat trasu, kterou budou klienti `MapSignalR` používat pro připojení k centru, zavolejte metodu při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="d4f14-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="d4f14-163">`MapSignalR`je [metoda rozšíření](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` pro třídu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="d4f14-164">Následující příklad ukazuje, jak definovat směr Huby SignalR pomocí spouštěcí třídy OWIN.</span><span class="sxs-lookup"><span data-stu-id="d4f14-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="d4f14-165">Pokud přidáváte funkce SignalR do aplikace ASP.NET MVC, ujistěte se, že je před ostatními trasami přidána trasa SignalR.</span><span class="sxs-lookup"><span data-stu-id="d4f14-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="d4f14-166">Další informace naleznete v [tématu Výuka: Začínáme s SignalR 2 a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="d4f14-167">Adresa URL /signalr</span><span class="sxs-lookup"><span data-stu-id="d4f14-167">The /signalr URL</span></span>

<span data-ttu-id="d4f14-168">Ve výchozím nastavení je adresa URL trasy, kterou klienti používají pro připojení k centru, "/signalr".</span><span class="sxs-lookup"><span data-stu-id="d4f14-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="d4f14-169">(Nepleťte si tuto adresu URL s adresou URL "/signalr/hubs", která je určen pro automaticky generovaný soubor JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4f14-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="d4f14-170">Další informace o generovaném proxy serveru naleznete v [tématu SignalR Hubs API Guide - JavaScript Client - Vygenerovaný proxy server a co pro vás dělá](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="d4f14-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="d4f14-171">Mohou existovat mimořádné okolnosti, které činí tuto základní adresu URL nepoužitelnou pro SignalR; například máte složku v projektu s názvem *signalr* a nechcete změnit název.</span><span class="sxs-lookup"><span data-stu-id="d4f14-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="d4f14-172">V takovém případě můžete změnit základní adresu URL, jak je znázorněno v následujících příkladech (nahradit "/signalr" v ukázkovém kódu požadovanou adresou URL).</span><span class="sxs-lookup"><span data-stu-id="d4f14-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="d4f14-173">**Kód serveru, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="d4f14-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="d4f14-174">**Klientský kód JavaScriptu, který určuje adresu URL (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="d4f14-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="d4f14-175">**Klientský kód JavaScriptu, který určuje adresu URL (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="d4f14-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="d4f14-176">**Kód klienta .NET, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="d4f14-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="d4f14-177">Konfigurace možností signalr</span><span class="sxs-lookup"><span data-stu-id="d4f14-177">Configuring SignalR Options</span></span>

<span data-ttu-id="d4f14-178">Přetížení `MapSignalR` metody umožňují zadat vlastní adresu URL, vlastní překládání závislostí a následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="d4f14-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="d4f14-179">Povolte volání mezi doménami pomocí CORS nebo JSONP z klientů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="d4f14-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="d4f14-180">Obvykle, pokud prohlížeč načte `http://contoso.com`stránku z , signalr připojení `http://contoso.com/signalr`je ve stejné doméně, at .</span><span class="sxs-lookup"><span data-stu-id="d4f14-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="d4f14-181">Pokud stránka `http://contoso.com` z vytvoří `http://fabrikam.com/signalr`připojení k , to je připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="d4f14-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="d4f14-182">Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázána.</span><span class="sxs-lookup"><span data-stu-id="d4f14-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="d4f14-183">Další informace naleznete [v tématu ASP.NET SignalR Hubs API Guide – JavaScript Client - Jak navázat připojení mezi doménami](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="d4f14-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="d4f14-184">Povolte podrobné chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="d4f14-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="d4f14-185">Dojde-li k chybám, výchozí chování SignalR je odeslat klientům oznámení bez podrobností o tom, co se stalo.</span><span class="sxs-lookup"><span data-stu-id="d4f14-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="d4f14-186">Odesílání podrobných informací o chybě klientům se v produkčním prostředí nedoporučuje, protože uživatelé se zlými úmysly mohou tyto informace použít při útocích proti vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d4f14-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="d4f14-187">Při řešení potíží můžete pomocí této možnosti dočasně povolit informativní hlášení chyb.</span><span class="sxs-lookup"><span data-stu-id="d4f14-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="d4f14-188">Zakázat automaticky generované soubory proxy JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4f14-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="d4f14-189">Ve výchozím nastavení je v reakci na adresu URL "/signalr/huby" generován soubor JavaScriptu se serverem proxy pro vaše třídy Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="d4f14-190">Pokud nechcete používat proxy servery JavaScript nebo chcete tento soubor vygenerovat ručně a odkazovat na fyzický soubor ve svých klientech, můžete tuto možnost použít k zakázání generování proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="d4f14-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="d4f14-191">Další informace naleznete v [tématu SignalR Hubs API Guide – JavaScript Client - Jak vytvořit fyzický soubor pro proxy server generovaný signalr](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="d4f14-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="d4f14-192">Následující příklad ukazuje, jak zadat adresu URL připojení SignalR `MapSignalR` a tyto možnosti ve volání metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="d4f14-193">Chcete-li zadat vlastní adresu URL, nahraďte v příkladu adresu URL, kterou chcete použít, v příkladu.To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span><span class="sxs-lookup"><span data-stu-id="d4f14-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="d4f14-194">Jak vytvořit a používat třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-194">How to create and use Hub classes</span></span>

<span data-ttu-id="d4f14-195">Chcete-li vytvořit centrum, vytvořte třídu, která je odvozena od [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d4f14-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="d4f14-196">Následující příklad ukazuje jednoduchou třídu Hub pro chatovací aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d4f14-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="d4f14-197">V tomto příkladu může připojený `NewContosoChatMessage` klient volat metodu a když se tak stane, přijatá data jsou vysílána všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="d4f14-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="d4f14-198">Životnost objektu centra</span><span class="sxs-lookup"><span data-stu-id="d4f14-198">Hub object lifetime</span></span>

<span data-ttu-id="d4f14-199">Není konkretizovat Hub třídy nebo volání jeho metody z vlastního kódu na serveru; vše, co je pro vás provedeno potrubím SignalR Hubs.</span><span class="sxs-lookup"><span data-stu-id="d4f14-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="d4f14-200">SignalR vytvoří novou instanci třídy Hub pokaždé, když potřebuje zpracovat operaci hubu, například když se klient připojí, odpojí nebo provede volání metody na server.</span><span class="sxs-lookup"><span data-stu-id="d4f14-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="d4f14-201">Vzhledem k tomu, že instance třídy Hub jsou přechodné, nelze je použít k udržování stavu z jednoho volání metody na další.</span><span class="sxs-lookup"><span data-stu-id="d4f14-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="d4f14-202">Pokaždé, když server obdrží volání metody z klienta, nová instance třídy Hub zpracuje zprávu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="d4f14-203">Chcete-li udržovat stav prostřednictvím více připojení a volání metod, použijte jinou metodu, jako je například `Hub`databáze nebo statická proměnná ve třídě Hub nebo jinou třídu, která není odvozena z .</span><span class="sxs-lookup"><span data-stu-id="d4f14-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="d4f14-204">Pokud zachováte data v paměti pomocí metody, jako je například statická proměnná ve třídě Hub, data budou ztracena při recyklaci domény aplikace.</span><span class="sxs-lookup"><span data-stu-id="d4f14-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="d4f14-205">Pokud chcete odesílat zprávy klientům z vlastního kódu, který běží mimo třídu Hub, nemůžete to udělat vytvořením instance třídy Hub, ale můžete to udělat získáním odkazu na kontextový objekt SignalR pro třídu Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="d4f14-206">Další informace naleznete v tématu [Jak volat klientské metody a spravovat skupiny mimo hub třídy](#callfromoutsidehub) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="d4f14-207">Camel-caseing z hubjména v javascriptových klientech</span><span class="sxs-lookup"><span data-stu-id="d4f14-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="d4f14-208">Ve výchozím nastavení klienti JavaScriptu odkazují na centra pomocí verze názvu třídy s camel-cased.</span><span class="sxs-lookup"><span data-stu-id="d4f14-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="d4f14-209">SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="d4f14-210">Předchozí příklad by byl `contosoChatHub` označován jako v kódu Jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4f14-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="d4f14-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="d4f14-212">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="d4f14-213">Pokud chcete zadat jiný název pro klienty, `HubName` které chcete použít, přidejte atribut.</span><span class="sxs-lookup"><span data-stu-id="d4f14-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="d4f14-214">Při použití `HubName` atributu se v klientech JavaScriptu nezmění žádný název na případ camelu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="d4f14-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="d4f14-216">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="d4f14-217">Více rozbočovačů</span><span class="sxs-lookup"><span data-stu-id="d4f14-217">Multiple Hubs</span></span>

<span data-ttu-id="d4f14-218">V aplikaci můžete definovat více tříd Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="d4f14-219">Když to uděláte, připojení je sdílené, ale skupiny jsou oddělené:</span><span class="sxs-lookup"><span data-stu-id="d4f14-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="d4f14-220">Všichni klienti budou používat stejnou adresu URL k navázání připojení SignalR s vaší službou ("/signalr" nebo vlastní adresou URL, pokud jste ji zadali) a toto připojení se používá pro všechna centra definovaná službou.</span><span class="sxs-lookup"><span data-stu-id="d4f14-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="d4f14-221">Neexistuje žádný rozdíl výkonu pro více rozbočovačů ve srovnání s definováním všech funkcí rozbočovače v jedné třídě.</span><span class="sxs-lookup"><span data-stu-id="d4f14-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="d4f14-222">Všechna centra získají stejné informace o požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4f14-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="d4f14-223">Vzhledem k tomu, že všechny rozbočovače sdílejí stejné připojení, pouze informace o požadavku HTTP, které server získá, je to, co je dodáváno v původním požadavku HTTP, který naváže připojení SignalR.</span><span class="sxs-lookup"><span data-stu-id="d4f14-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="d4f14-224">Pokud použijete požadavek na připojení k předání informací z klienta na server zadáním řetězce dotazu, nemůžete poskytnout různé řetězce dotazu různým rozbočovačům.</span><span class="sxs-lookup"><span data-stu-id="d4f14-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="d4f14-225">Všechna centra obdrží stejné informace.</span><span class="sxs-lookup"><span data-stu-id="d4f14-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="d4f14-226">Vygenerovaný soubor proxy jazyka JavaScript bude obsahovat proxy servery pro všechna centra v jednom souboru.</span><span class="sxs-lookup"><span data-stu-id="d4f14-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="d4f14-227">Informace o proxy serverech JavaScript naleznete v [tématu SignalR Hubs API Guide - JavaScript Client - Vygenerovaný proxy server a co dělá pro vás](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="d4f14-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="d4f14-228">Skupiny jsou definovány v rozbočovačích.</span><span class="sxs-lookup"><span data-stu-id="d4f14-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="d4f14-229">V SignalR můžete definovat pojmenované skupiny pro vysílání do podskupin připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="d4f14-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="d4f14-230">Skupiny jsou udržovány samostatně pro každé centrum.</span><span class="sxs-lookup"><span data-stu-id="d4f14-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="d4f14-231">Například skupina s názvem "Správci" by obsahovat `ContosoChatHub` jednu sadu klientů pro vaši třídu a `StockTickerHub` stejný název skupiny by odkazovat na jinou sadu klientů pro vaši třídu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="d4f14-232">Rozbočovače silného typu</span><span class="sxs-lookup"><span data-stu-id="d4f14-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="d4f14-233">Chcete-li definovat rozhraní pro metody rozbočovače, na které může klient odkazovat `Hub<T>` (a povolit intellisense `Hub`u metod rozbočovače), odvodit rozbočovač z (představeného v SignalR 2.1) spíše než :</span><span class="sxs-lookup"><span data-stu-id="d4f14-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="d4f14-234">Jak definovat metody ve třídě Hub, které mohou klienti volat</span><span class="sxs-lookup"><span data-stu-id="d4f14-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="d4f14-235">Chcete-li vystavit metodu v centru, kterou chcete volat elita z klienta, deklarujte veřejnou metodu, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="d4f14-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="d4f14-236">Můžete zadat návratový typ a parametry, včetně komplexních typů a polí, stejně jako v libovolné metodě Jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="d4f14-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="d4f14-237">Všechna data, která obdržíte v parametrech nebo se vrátíte volajícímu, jsou sdělována mezi klientem a serverem pomocí JSON a SignalR automaticky zpracovává vazbu složitých objektů a polí objektů.</span><span class="sxs-lookup"><span data-stu-id="d4f14-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="d4f14-238">Camel-caseing názvů metod v javascriptových klientech</span><span class="sxs-lookup"><span data-stu-id="d4f14-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="d4f14-239">Ve výchozím nastavení klienti JavaScriptu odkazují na metody Hub pomocí camel-cased verze názvu metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="d4f14-240">SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="d4f14-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="d4f14-242">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="d4f14-243">Pokud chcete zadat jiný název pro klienty, `HubMethodName` které chcete použít, přidejte atribut.</span><span class="sxs-lookup"><span data-stu-id="d4f14-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="d4f14-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="d4f14-245">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="d4f14-246">Kdy provést asynchronně</span><span class="sxs-lookup"><span data-stu-id="d4f14-246">When to execute asynchronously</span></span>

<span data-ttu-id="d4f14-247">Pokud metoda bude dlouhotrvající nebo má dělat práci, která by zahrnovala čekání, jako je například vyhledávání databáze nebo volání webové služby, `void` proveďte Hub metoda asynchronní [vrácenítask](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (místo návratu) nebo [task&lt;&gt; t](https://msdn.microsoft.com/library/dd321424.aspx) objekt (místo návratového `T` typu).</span><span class="sxs-lookup"><span data-stu-id="d4f14-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="d4f14-248">Když vrátíte `Task` objekt z metody SignalR čeká `Task` na dokončení a potom odešle nebalený výsledek zpět klientovi, takže není žádný rozdíl v tom, jak kód volání metody v klientovi.</span><span class="sxs-lookup"><span data-stu-id="d4f14-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="d4f14-249">Vytvoření metody Hub asynchronní zabraňuje blokování připojení při použití přenosu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="d4f14-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="d4f14-250">Při spuštění metody Hub synchronně a přenos je WebSocket, následné vyvolání metod na rozbočovači ze stejného klienta jsou blokovány, dokud hub metoda nedokončí.</span><span class="sxs-lookup"><span data-stu-id="d4f14-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="d4f14-251">Následující příklad ukazuje stejnou metodu kódovku pro synchronní nebo asynchronní spuštění, následovanou klientským kódem Jazyka JavaScript, který funguje pro volání obou verzí.</span><span class="sxs-lookup"><span data-stu-id="d4f14-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="d4f14-252">**Synchronní**</span><span class="sxs-lookup"><span data-stu-id="d4f14-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="d4f14-253">**Asynchronní**</span><span class="sxs-lookup"><span data-stu-id="d4f14-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="d4f14-254">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="d4f14-255">Další informace o použití asynchronních metod v ASP.NET 4.5 naleznete [v tématu Použití asynchronních metod v ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="d4f14-256">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="d4f14-256">Defining Overloads</span></span>

<span data-ttu-id="d4f14-257">Pokud chcete definovat přetížení pro metodu, počet parametrů v každém přetížení se musí lišit.</span><span class="sxs-lookup"><span data-stu-id="d4f14-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="d4f14-258">Pokud rozlišujete přetížení pouze zadáním různých typů parametrů, vaše třída Hub se zkompiluje, ale služba SignalR vyvolá výjimku v době běhu, když se klienti pokusí volat jedno z přetížení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="d4f14-259">Hlášení průběhu z vyvolání metody centra</span><span class="sxs-lookup"><span data-stu-id="d4f14-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="d4f14-260">SignalR 2.1 přidává podporu pro [průběh vykazování vzor](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) zavedený v .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d4f14-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="d4f14-261">Chcete-li implementovat `IProgress<T>` hlášení průběhu, definujte parametr pro metodu centra, ke které má klient přístup:</span><span class="sxs-lookup"><span data-stu-id="d4f14-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="d4f14-262">Při psaní dlouho běžící serverové metody je důležité použít asynchronní programovací vzor, jako je Async/ Await, nikoli blokování vlákna centra.</span><span class="sxs-lookup"><span data-stu-id="d4f14-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="d4f14-263">Jak volat klientské metody z třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="d4f14-264">Chcete-li volat klientské metody `Clients` ze serveru, použijte vlastnost v metodě ve třídě Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="d4f14-265">Následující příklad ukazuje kód `addNewMessageToPage` serveru, který volá všechny připojené klienty, a klientský kód, který definuje metodu v klientovi JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d4f14-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="d4f14-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="d4f14-267">Vyvolání metody klienta je asynchronní operace a `Task`vrátí .</span><span class="sxs-lookup"><span data-stu-id="d4f14-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="d4f14-268">Použití `await`:</span><span class="sxs-lookup"><span data-stu-id="d4f14-268">Use `await`:</span></span>

* <span data-ttu-id="d4f14-269">Chcete-li zajistit, že zpráva je odeslána bez chyby.</span><span class="sxs-lookup"><span data-stu-id="d4f14-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="d4f14-270">Chcete-li povolit zachycení a zpracování chyb v bloku try-catch.</span><span class="sxs-lookup"><span data-stu-id="d4f14-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="d4f14-271">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="d4f14-272">Nelze získat vrácenou hodnotu z metody klienta; syntaxe, `int x = Clients.All.add(1,1)` jako je nefunguje.</span><span class="sxs-lookup"><span data-stu-id="d4f14-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="d4f14-273">Pro parametry můžete určit složité typy a pole.</span><span class="sxs-lookup"><span data-stu-id="d4f14-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="d4f14-274">Následující příklad předá klientovi komplexní typ v parametru metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="d4f14-275">**Kód serveru, který volá metodu klienta pomocí komplexního objektu**</span><span class="sxs-lookup"><span data-stu-id="d4f14-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="d4f14-276">**Kód serveru, který definuje složitý objekt**</span><span class="sxs-lookup"><span data-stu-id="d4f14-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="d4f14-277">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="d4f14-278">Výběr klientů, kteří budou přijímat vzdálené volání procedur</span><span class="sxs-lookup"><span data-stu-id="d4f14-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="d4f14-279">Vlastnost Clients vrátí objekt [HubConnectionContext,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) který poskytuje několik možností pro určení, kteří klienti obdrží vzdálené volání procedur:</span><span class="sxs-lookup"><span data-stu-id="d4f14-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="d4f14-280">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="d4f14-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="d4f14-281">Pouze volající klient.</span><span class="sxs-lookup"><span data-stu-id="d4f14-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="d4f14-282">Všichni klienti kromě volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="d4f14-283">Konkrétní klient identifikovaný ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="d4f14-284">Tento příklad `addContosoChatMessageToPage` volá volajícího klienta a `Clients.Caller`má stejný účinek jako pomocí .</span><span class="sxs-lookup"><span data-stu-id="d4f14-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="d4f14-285">Všichni připojení klienti kromě určených klientů, identifikované ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="d4f14-286">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="d4f14-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="d4f14-287">Všichni připojení klienti v zadané skupině s výjimkou určených klientů identifikovaných ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="d4f14-288">Všichni připojení klienti v zadané skupině kromě volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="d4f14-289">Konkrétní uživatel, identifikovaný id uživatele.</span><span class="sxs-lookup"><span data-stu-id="d4f14-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="d4f14-290">Ve výchozím nastavení `IPrincipal.Identity.Name`je to , ale to lze změnit [registrací implementace IUserIdProvider s globálním hostitelem](mapping-users-to-connections.md#IUserIdProvider).</span><span class="sxs-lookup"><span data-stu-id="d4f14-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="d4f14-291">Všichni klienti a skupiny v seznamu ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="d4f14-292">Seznam skupin.</span><span class="sxs-lookup"><span data-stu-id="d4f14-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="d4f14-293">Uživatel podle jména.</span><span class="sxs-lookup"><span data-stu-id="d4f14-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="d4f14-294">Seznam uživatelských jmen (uveden v SignalR 2.1).</span><span class="sxs-lookup"><span data-stu-id="d4f14-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="d4f14-295">Žádné ověření v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="d4f14-295">No compile-time validation for method names</span></span>

<span data-ttu-id="d4f14-296">Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj neexistuje žádné ověření technologie IntelliSense nebo kompilace.</span><span class="sxs-lookup"><span data-stu-id="d4f14-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="d4f14-297">Výraz je vyhodnocen za běhu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="d4f14-298">Při spuštění volání metody SignalR odešle název metody a hodnoty parametrů klientovi a pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou jí předány.</span><span class="sxs-lookup"><span data-stu-id="d4f14-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="d4f14-299">Pokud není v klientovi nalezena žádná odpovídající metoda, není vyvolána žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="d4f14-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="d4f14-300">Informace o formátu dat, která SignalR přenáší klientovi na pozadí při volání metody klienta, naleznete [v tématu Úvod do SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="d4f14-301">Porovnávání názvů metod bez malých a velkých písmen</span><span class="sxs-lookup"><span data-stu-id="d4f14-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="d4f14-302">Porovnávání názvů metod nerozlišuje malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="d4f14-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d4f14-303">Například `Clients.All.addContosoChatMessageToPage` na serveru bude `AddContosoChatMessageToPage` `addcontosochatmessagetopage`spuštěna `addContosoChatMessageToPage` , , nebo na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="d4f14-304">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="d4f14-304">Asynchronous execution</span></span>

<span data-ttu-id="d4f14-305">Metoda, kterou voláte, se provádí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="d4f14-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="d4f14-306">Jakýkoli kód, který přichází po volání metody klientovi, se spustí okamžitě bez čekání na signalr dokončení přenosu dat klientům, pokud nezadáte, že následující řádky kódu by měly čekat na dokončení metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="d4f14-307">Následující příklad kódu ukazuje, jak spustit dvě klientské metody postupně.</span><span class="sxs-lookup"><span data-stu-id="d4f14-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="d4f14-308">**Použití Await (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="d4f14-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="d4f14-309">Pokud použijete `await` čekat, až klient metoda dokončí před spuštěním další řádek kódu, to neznamená, že klienti skutečně obdrží zprávu před spuštěním dalšího řádku kódu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="d4f14-310">"Dokončení" volání metody klienta pouze znamená, že SignalR udělal vše potřebné k odeslání zprávy.</span><span class="sxs-lookup"><span data-stu-id="d4f14-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="d4f14-311">Pokud potřebujete ověření, že klienti obdrželi zprávu, musíte tento mechanismus naprogramovat sami.</span><span class="sxs-lookup"><span data-stu-id="d4f14-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="d4f14-312">Můžete například kód `MessageReceived` metodu na rozbočovača a v `addContosoChatMessageToPage` `MessageReceived` metodě na klienta můžete volat po práci, kterou potřebujete udělat na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="d4f14-313">V `MessageReceived` centru můžete dělat cokoliv práce závisí na skutečném příjmu klienta a zpracování volání původní metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="d4f14-314">Použití proměnné řetězce jako názvu metody</span><span class="sxs-lookup"><span data-stu-id="d4f14-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="d4f14-315">Pokud chcete vyvolat metodu klienta pomocí proměnné řetězce jako `Clients.All` název `Clients.Others` `Clients.Caller`metody, přetypování (nebo , atd.) a `IClientProxy` pak volat [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d4f14-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="d4f14-316">Jak spravovat členství ve skupině z třídy Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="d4f14-317">Skupiny v SignalR poskytují metodu pro vysílání zpráv do určených podmnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="d4f14-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="d4f14-318">Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.</span><span class="sxs-lookup"><span data-stu-id="d4f14-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="d4f14-319">Chcete-li spravovat členství ve skupině, použijte `Groups` metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) poskytované vlastností třídy Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="d4f14-320">Následující příklad ukazuje `Groups.Add` `Groups.Remove` metody a používané v metodách Hub, které jsou volány klientským kódem, následované klientským kódem JavaScriptu, který je volá.</span><span class="sxs-lookup"><span data-stu-id="d4f14-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="d4f14-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="d4f14-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="d4f14-322">**Klient JavaScriptu pomocí generovaného proxy serveru**</span><span class="sxs-lookup"><span data-stu-id="d4f14-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="d4f14-323">Není třeba explicitně vytvářet skupiny.</span><span class="sxs-lookup"><span data-stu-id="d4f14-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="d4f14-324">Ve skutečnosti je skupina automaticky vytvořena při prvním zadání `Groups.Add`jejího názvu ve volání a je odstraněna při odebrání posledního připojení z členství v ní.</span><span class="sxs-lookup"><span data-stu-id="d4f14-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="d4f14-325">Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin.</span><span class="sxs-lookup"><span data-stu-id="d4f14-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="d4f14-326">SignalR odesílá zprávy klientům a skupinám na základě [modelu pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)a server neudržuje seznamy skupin nebo členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="d4f14-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="d4f14-327">To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, musí být do nového uzlu rozšířen jakýkoli stav, který signalr udržuje.</span><span class="sxs-lookup"><span data-stu-id="d4f14-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="d4f14-328">Asynchronní provádění metod Add and Remove</span><span class="sxs-lookup"><span data-stu-id="d4f14-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="d4f14-329">Metody `Groups.Add` `Groups.Remove` a metody asynchronně.</span><span class="sxs-lookup"><span data-stu-id="d4f14-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="d4f14-330">Pokud chcete přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, musíte se ujistit, že `Groups.Add` metoda dokončí jako první.</span><span class="sxs-lookup"><span data-stu-id="d4f14-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="d4f14-331">Následující příklad kódu ukazuje, jak to udělat.</span><span class="sxs-lookup"><span data-stu-id="d4f14-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="d4f14-332">**Přidání klienta do skupiny a následné zasílání zpráv**</span><span class="sxs-lookup"><span data-stu-id="d4f14-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="d4f14-333">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="d4f14-333">Group membership persistence</span></span>

<span data-ttu-id="d4f14-334">SignalR sleduje připojení, nikoli uživatele, takže pokud chcete, aby byl uživatel ve stejné skupině pokaždé, když uživatel naváže připojení, musíte zavolat `Groups.Add` pokaždé, když uživatel naváže nové připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="d4f14-335">Po dočasné ztrátě připojení, někdy SignalR můžete obnovit připojení automaticky.</span><span class="sxs-lookup"><span data-stu-id="d4f14-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="d4f14-336">V takovém případě SignalR obnovuje stejné připojení, nikoli navazování nového připojení, a tak je automaticky obnoveno členství klienta ve skupině.</span><span class="sxs-lookup"><span data-stu-id="d4f14-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="d4f14-337">To je možné i v případě, že dočasné přerušení je výsledkem restartování nebo selhání serveru, protože stav připojení pro každého klienta, včetně členství ve skupinách, je round-tripped ke klientovi.</span><span class="sxs-lookup"><span data-stu-id="d4f14-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="d4f14-338">Pokud server přejde dolů a je nahrazen novým serverem před časovým limitem připojení, klient se může automaticky znovu připojit k novému serveru a znovu se zaregistrovat do skupin, kterých je členem.</span><span class="sxs-lookup"><span data-stu-id="d4f14-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="d4f14-339">Pokud nelze připojení obnovit automaticky po ztrátě připojení nebo po uplynutí doby připojení nebo po odpojení klienta (například když prohlížeč přejde na novou stránku), členství ve skupinách dojde ke ztrátě.</span><span class="sxs-lookup"><span data-stu-id="d4f14-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="d4f14-340">Při příštím připojení uživatele bude nové připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="d4f14-341">Chcete-li zachovat členství ve skupinách, když stejný uživatel naváže nové připojení, musí aplikace sledovat přidružení mezi uživateli a skupinami a obnovit členství ve skupinách pokaždé, když uživatel naváže nové připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="d4f14-342">Další informace o připojení a opětovné připojení naleznete v tématu [Jak zpracovat události životnosti připojení ve třídě Hub](#connectionlifetime) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="d4f14-343">Skupiny pro jednoho uživatele</span><span class="sxs-lookup"><span data-stu-id="d4f14-343">Single-user groups</span></span>

<span data-ttu-id="d4f14-344">Aplikace, které používají SignalR obvykle musí sledovat přidružení mezi uživateli a připojení, aby věděli, který uživatel odeslal zprávu a který uživatel by měl přijímat zprávy.</span><span class="sxs-lookup"><span data-stu-id="d4f14-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="d4f14-345">Skupiny se používají v jednom ze dvou běžně používaných vzorů pro to.</span><span class="sxs-lookup"><span data-stu-id="d4f14-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="d4f14-346">Skupiny pro jednoho uživatele.</span><span class="sxs-lookup"><span data-stu-id="d4f14-346">Single-user groups.</span></span>

    <span data-ttu-id="d4f14-347">Jako název skupiny můžete zadat uživatelské jméno a přidat aktuální ID připojení do skupiny při každém připojení nebo opětovném připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="d4f14-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="d4f14-348">Odesílání zpráv uživateli, který odesíláte do skupiny.</span><span class="sxs-lookup"><span data-stu-id="d4f14-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="d4f14-349">Nevýhodou této metody je, že skupina neposkytuje způsob, jak zjistit, zda je uživatel online nebo offline.</span><span class="sxs-lookup"><span data-stu-id="d4f14-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="d4f14-350">Sledování přidružení mezi uživatelskými jmény a ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="d4f14-351">Můžete uložit přidružení mezi jednotlivými uživatelskými jmény a jedním nebo více ID připojení do slovníku nebo databáze a aktualizovat uložená data při každém připojení nebo odpojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="d4f14-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="d4f14-352">Chcete-li uživateli odesílat zprávy, zadejte ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="d4f14-353">Nevýhodou této metody je, že trvá více paměti.</span><span class="sxs-lookup"><span data-stu-id="d4f14-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="d4f14-354">Jak zpracovat události životnosti připojení ve třídě Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="d4f14-355">Typickými důvody pro zpracování událostí životnosti připojení je sledovat, zda je uživatel připojen nebo ne, a sledovat přidružení mezi uživatelskými jmény a ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="d4f14-356">Chcete-li spustit vlastní kód při připojení `OnConnected`nebo `OnDisconnected`odpojení klientů, přepište , a `OnReconnected` virtuální metody třídy Hub, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="d4f14-357">Když OnConnected, OnDisconnected a OnReconnected se nazývají</span><span class="sxs-lookup"><span data-stu-id="d4f14-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="d4f14-358">Pokaždé, když prohlížeč přejde na novou stránku, musí být navázáno `OnDisconnected` nové připojení, `OnConnected` což znamená, že SignalR provede metodu následovanou metodou.</span><span class="sxs-lookup"><span data-stu-id="d4f14-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="d4f14-359">SignalR vždy vytvoří nové ID připojení při navázání nového připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="d4f14-360">Metoda `OnReconnected` je volána, pokud došlo k dočasnému přerušení připojení, ze kterého může signalr automaticky obnovit, například když je kabel dočasně odpojen a znovu připojen před časovým limitem připojení. Metoda `OnDisconnected` je volána, když je klient odpojen a SignalR nelze automaticky znovu připojit, například když prohlížeč přejde na novou stránku.</span><span class="sxs-lookup"><span data-stu-id="d4f14-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="d4f14-361">Proto je možné posloupnosti událostí `OnConnected`pro `OnReconnected` `OnDisconnected`daného klienta , , ; nebo `OnConnected` `OnDisconnected`, .</span><span class="sxs-lookup"><span data-stu-id="d4f14-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="d4f14-362">Pro dané připojení se `OnConnected` `OnDisconnected`sekvence `OnReconnected` nezobrazí .</span><span class="sxs-lookup"><span data-stu-id="d4f14-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="d4f14-363">Metoda `OnDisconnected` není volat v některých scénářích, například když server přejde dolů nebo domény aplikace získá recyklovány.</span><span class="sxs-lookup"><span data-stu-id="d4f14-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="d4f14-364">Když je jiný server zapnutý nebo doména aplikace dokončí recyklaci, někteří klienti `OnReconnected` se mohou znovu připojit a událost zapálit.</span><span class="sxs-lookup"><span data-stu-id="d4f14-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="d4f14-365">Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="d4f14-366">Stav volajícího není naplněn.</span><span class="sxs-lookup"><span data-stu-id="d4f14-366">Caller state not populated</span></span>

<span data-ttu-id="d4f14-367">Metody obslužné rutiny životnosti připojení jsou volány ze `state` serveru, což znamená, že `Caller` žádný stav, který vložíte do objektu na straně klienta, nebude naplněn ve vlastnosti na serveru.</span><span class="sxs-lookup"><span data-stu-id="d4f14-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="d4f14-368">Informace o `state` objektu `Caller` a vlastnosti naleznete v tématu [Jak předat stav mezi klienty a Hub třídy](#passstate) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="d4f14-369">Jak získat informace o klientovi z Context vlastnost</span><span class="sxs-lookup"><span data-stu-id="d4f14-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="d4f14-370">Chcete-li získat informace o `Context` klientovi, použijte vlastnost Hub třídy.</span><span class="sxs-lookup"><span data-stu-id="d4f14-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="d4f14-371">Vlastnost `Context` vrátí [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) objekt, který poskytuje přístup k následujícím informacím:</span><span class="sxs-lookup"><span data-stu-id="d4f14-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="d4f14-372">ID připojení volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="d4f14-373">ID připojení je identifikátor GUID, který je přiřazen SignalR (nelze zadat hodnotu ve vlastním kódu).</span><span class="sxs-lookup"><span data-stu-id="d4f14-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="d4f14-374">Pro každé připojení existuje jedno ID připojení a stejné ID připojení používají všechna centra, pokud máte ve vaší aplikaci více center.</span><span class="sxs-lookup"><span data-stu-id="d4f14-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="d4f14-375">Data hlavičky HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4f14-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="d4f14-376">Můžete také získat hlavičky `Context.Headers`HTTP z .</span><span class="sxs-lookup"><span data-stu-id="d4f14-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="d4f14-377">Důvodem pro více odkazů na stejnou `Context.Headers` věc je, `Context.Request` že byl vytvořen `Context.Headers` jako první, vlastnost byla přidána později a byla zachována pro zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="d4f14-378">Data řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="d4f14-379">Můžete také získat data `Context.QueryString`řetězce dotazu z aplikace .</span><span class="sxs-lookup"><span data-stu-id="d4f14-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="d4f14-380">Řetězec dotazu, který získáte v této vlastnosti je ten, který byl použit s požadavkem HTTP, který nastavoval připojení SignalR.</span><span class="sxs-lookup"><span data-stu-id="d4f14-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="d4f14-381">Parametry řetězce dotazu můžete přidat v klientovi konfigurací připojení, což je pohodlný způsob, jak předat data o klientovi z klienta na server.</span><span class="sxs-lookup"><span data-stu-id="d4f14-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="d4f14-382">Následující příklad ukazuje jeden způsob, jak přidat řetězec dotazu v klientovi JavaScriptpři použití generovaného proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="d4f14-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="d4f14-383">Další informace o nastavení parametrů řetězce dotazu naleznete v příručkách rozhraní API pro klienty [JavaScript](hubs-api-guide-javascript-client.md) a [.NET.](hubs-api-guide-net-client.md)</span><span class="sxs-lookup"><span data-stu-id="d4f14-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="d4f14-384">Můžete najít metodu přenosu použitou pro připojení v datech řetězce dotazu, spolu s některými dalšími hodnotami používanými interně SignalR:</span><span class="sxs-lookup"><span data-stu-id="d4f14-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="d4f14-385">Hodnota `transportMethod` bude "webSockets", "serverSentEvents", "foreverFrame" nebo "longPolling".</span><span class="sxs-lookup"><span data-stu-id="d4f14-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="d4f14-386">Všimněte si, že pokud `OnConnected` zkontrolujete tuto hodnotu v metodě obslužné rutiny události, v některých scénářích můžete zpočátku získat hodnotu přenosu, která není konečnou vyjednanou metodou přenosu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="d4f14-387">V takovém případě metoda vyvolá výjimku a bude volána znovu později při stanovení konečné metody přenosu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="d4f14-388">Soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="d4f14-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="d4f14-389">Soubory cookie můžete `Context.RequestCookies`získat také od společnosti .</span><span class="sxs-lookup"><span data-stu-id="d4f14-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="d4f14-390">Informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="d4f14-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="d4f14-391">Objekt HttpContext pro požadavek :</span><span class="sxs-lookup"><span data-stu-id="d4f14-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="d4f14-392">Použijte tuto metodu `HttpContext.Current` namísto `HttpContext` získání získat objekt pro připojení SignalR.</span><span class="sxs-lookup"><span data-stu-id="d4f14-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="d4f14-393">Jak předat stav mezi klienty a třídou Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="d4f14-394">Proxy klient poskytuje `state` objekt, ve kterém můžete ukládat data, která chcete přenášet na server s každým voláním metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="d4f14-395">Na serveru můžete přistupovat k `Clients.Caller` těmto datům ve vlastnosti v hubových metodách, které jsou volány klienty.</span><span class="sxs-lookup"><span data-stu-id="d4f14-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="d4f14-396">Vlastnost `Clients.Caller` není naplněna pro metody obslužné rutiny události životnosti `OnConnected`připojení , `OnDisconnected`a `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="d4f14-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="d4f14-397">Vytváření nebo aktualizace `state` dat v `Clients.Caller` objektu a vlastnosti funguje v obou směrech.</span><span class="sxs-lookup"><span data-stu-id="d4f14-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="d4f14-398">Můžete aktualizovat hodnoty na serveru a jsou předány zpět klientovi.</span><span class="sxs-lookup"><span data-stu-id="d4f14-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="d4f14-399">Následující příklad ukazuje kód klienta JavaScript, který ukládá stav pro přenos na server s každým voláním metody.</span><span class="sxs-lookup"><span data-stu-id="d4f14-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="d4f14-400">Následující příklad ukazuje ekvivalentní kód v klientovi .NET.</span><span class="sxs-lookup"><span data-stu-id="d4f14-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="d4f14-401">Ve třídě Hub můžete přistupovat k `Clients.Caller` těmto datům ve vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d4f14-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="d4f14-402">Následující příklad ukazuje kód, který načte stav uvedený v předchozím příkladu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="d4f14-403">Tento mechanismus pro uchování stavu není určen pro velké množství `state` `Clients.Caller` dat, protože vše, co vložíte do nebo vlastnost je round-tripped s každou metodou vyvolání.</span><span class="sxs-lookup"><span data-stu-id="d4f14-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="d4f14-404">Je to užitečné pro menší položky, jako jsou uživatelská jména nebo čítače.</span><span class="sxs-lookup"><span data-stu-id="d4f14-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="d4f14-405">V VB.NET nebo v centru silného typu nelze získat přístup k `Clients.Caller`objektu stavu volajícího . místo toho `Clients.CallerState` použijte (zavedeno v SignalR 2.1):</span><span class="sxs-lookup"><span data-stu-id="d4f14-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="d4f14-406">**Použití CallerState v C #**</span><span class="sxs-lookup"><span data-stu-id="d4f14-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="d4f14-407">**Použití stavu volajícího v jazyce Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="d4f14-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="d4f14-408">Jak zpracovat chyby ve třídě Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="d4f14-409">Chcete-li zpracovat chyby, ke kterým dochází ve vašich metodách třídy Hub, nejprve se `await`ujistěte, že "dodržovat" všechny výjimky z asynchronních operací (například vyvolání klientských metod) pomocí .</span><span class="sxs-lookup"><span data-stu-id="d4f14-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="d4f14-410">Poté použijte jednu nebo více z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="d4f14-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="d4f14-411">Zalomit kód metody v try-catch bloky a protokolovat objekt výjimky.</span><span class="sxs-lookup"><span data-stu-id="d4f14-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="d4f14-412">Pro účely ladění můžete odeslat výjimku klientovi, ale z bezpečnostních důvodů se nedoporučuje odesílání podrobných informací klientům v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d4f14-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="d4f14-413">Vytvořte kanálový modul rozbočovačů, který zpracovává metodu [OnIncomingError.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d4f14-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="d4f14-414">Následující příklad ukazuje kanálový modul, který zaznamenává chyby, následovaný kódem v Startup.cs, který vstřikuje modul do kanálu hubů.</span><span class="sxs-lookup"><span data-stu-id="d4f14-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="d4f14-415">Použijte `HubException` třídu (zavedenou v SignalR 2).</span><span class="sxs-lookup"><span data-stu-id="d4f14-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="d4f14-416">Tato chyba může být vyvolána z libovolného vyvolání centra.</span><span class="sxs-lookup"><span data-stu-id="d4f14-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="d4f14-417">Konstruktor `HubError` přebírá zprávu řetězce a objekt pro ukládání dalších chybových dat.</span><span class="sxs-lookup"><span data-stu-id="d4f14-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="d4f14-418">SignalR bude automaticky serializovat výjimku a odeslat ji klientovi, kde bude použit k odmítnutí nebo selhání vyvolání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="d4f14-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="d4f14-419">Následující ukázky kódu ukazují, `HubException` jak vyvolat vyvolání centra a jak zpracovat výjimku v klientech JavaScript a .NET.</span><span class="sxs-lookup"><span data-stu-id="d4f14-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="d4f14-420">**Kód serveru demonstrující třídu HubException**</span><span class="sxs-lookup"><span data-stu-id="d4f14-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="d4f14-421">**Kód klienta JavaScriptu demonstrující odpověď na vyvolání hubexception v rozbočovači**</span><span class="sxs-lookup"><span data-stu-id="d4f14-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="d4f14-422">**Kód klienta .NET, který ukazuje odpověď na vyvolání hubvýjimky v rozbočovači**</span><span class="sxs-lookup"><span data-stu-id="d4f14-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="d4f14-423">Další informace o modulech kanálu hubu najdete v [tématu Jak přizpůsobit kanál rozbočovačů](#hubpipeline) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="d4f14-424">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="d4f14-424">How to enable tracing</span></span>

<span data-ttu-id="d4f14-425">Chcete-li povolit trasování na straně serveru, přidejte do souboru Web.config prvek system.diagnostics, jak je znázorněno v tomto příkladu:</span><span class="sxs-lookup"><span data-stu-id="d4f14-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="d4f14-426">Při spuštění aplikace v sadě Visual Studio, můžete zobrazit protokoly v okně **Výstup.**</span><span class="sxs-lookup"><span data-stu-id="d4f14-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="d4f14-427">Jak volat metody klienta a spravovat skupiny mimo třídu Hub</span><span class="sxs-lookup"><span data-stu-id="d4f14-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="d4f14-428">Chcete-li volat klientské metody z jiné třídy než vaše třída Hub, získejte odkaz na kontextový objekt SignalR pro centrum a použijte je k volání metod na straně klienta nebo ke správě skupin.</span><span class="sxs-lookup"><span data-stu-id="d4f14-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="d4f14-429">Následující ukázková `StockTicker` třída získá objekt context, uloží jej do instance třídy, uloží instanci třídy do statické vlastnosti `updateStockPrice` a použije kontext z instance `StockTickerHub`třídy singleton k volání metody u klientů, kteří jsou připojeni k centru s názvem .</span><span class="sxs-lookup"><span data-stu-id="d4f14-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="d4f14-430">Pokud potřebujete použít kontext vícekrát v objektu s dlouhou životností, získejte odkaz jednou a uložte jej, nikoli jej pokaždé znovu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="d4f14-431">Získání kontextu jednou zajišťuje, že SignalR odesílá zprávy klientům ve stejném pořadí, ve kterém vaše metody Hub provést vyvolání metody klienta.</span><span class="sxs-lookup"><span data-stu-id="d4f14-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="d4f14-432">Kurz, který ukazuje, jak používat kontext SignalR pro rozbočovač, naleznete [v tématu Vysílání serveru s ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="d4f14-433">Volání klientských metod</span><span class="sxs-lookup"><span data-stu-id="d4f14-433">Calling client methods</span></span>

<span data-ttu-id="d4f14-434">Můžete určit, kteří klienti obdrží vzdálené volání procedur, ale máte méně možností než při volání z třídy Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="d4f14-435">Důvodem je, že kontext není přidružen k určitému volání z klienta, takže žádné metody, `Clients.Others`které `Clients.Caller`vyžadují `Clients.OthersInGroup`znalost aktuálního ID připojení, například , nebo , nebo , nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d4f14-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="d4f14-436">K dispozici jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="d4f14-436">The following options are available:</span></span>

- <span data-ttu-id="d4f14-437">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="d4f14-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="d4f14-438">Konkrétní klient identifikovaný ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="d4f14-439">Všichni připojení klienti kromě určených klientů, identifikované ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="d4f14-440">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="d4f14-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="d4f14-441">Všichni připojení klienti v zadané skupině s výjimkou určených klientů, identifikované ID připojení.</span><span class="sxs-lookup"><span data-stu-id="d4f14-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="d4f14-442">Pokud voláte do třídy mimo centrum z metod ve třídě Hub, můžete předat Aktuální `Clients.Client` `Clients.AllExcept`ID `Clients.Group` připojení `Clients.Caller` `Clients.Others`a `Clients.OthersInGroup`použít jej s , , nebo simulovat , nebo .</span><span class="sxs-lookup"><span data-stu-id="d4f14-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="d4f14-443">V následujícím příkladu `MoveShapeHub` třída předá ID `Broadcaster` připojení do `Broadcaster` třídy `Clients.Others`tak, aby třída může simulovat .</span><span class="sxs-lookup"><span data-stu-id="d4f14-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="d4f14-444">Správa členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="d4f14-444">Managing group membership</span></span>

<span data-ttu-id="d4f14-445">Pro správu skupin máte stejné možnosti jako ve třídě Hub.</span><span class="sxs-lookup"><span data-stu-id="d4f14-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="d4f14-446">Přidání klienta do skupiny</span><span class="sxs-lookup"><span data-stu-id="d4f14-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="d4f14-447">Odebrání klienta ze skupiny</span><span class="sxs-lookup"><span data-stu-id="d4f14-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="d4f14-448">Jak přizpůsobit kanál Rozbočovače</span><span class="sxs-lookup"><span data-stu-id="d4f14-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="d4f14-449">SignalR umožňuje vložit vlastní kód do kanálu hubu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="d4f14-450">Následující příklad ukazuje vlastní modul kanálu rozbočovače, který protokoluje každé příchozí volání metody přijaté z klienta a volání odchozí metody vyvolané na straně klienta:</span><span class="sxs-lookup"><span data-stu-id="d4f14-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="d4f14-451">Následující kód v *Startup.cs* souboru registruje modul spustit v kanálu Hub:</span><span class="sxs-lookup"><span data-stu-id="d4f14-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="d4f14-452">Existuje mnoho různých metod, které můžete přepsat.</span><span class="sxs-lookup"><span data-stu-id="d4f14-452">There are many different methods that you can override.</span></span> <span data-ttu-id="d4f14-453">Úplný seznam naleznete v tématu [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d4f14-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
