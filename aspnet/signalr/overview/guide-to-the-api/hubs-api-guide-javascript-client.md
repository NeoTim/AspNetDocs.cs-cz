---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API Guide - JavaScript Client | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod do používání rozhraní HUBS API pro SignalR verze 2 v klientech JavaScriptu, jako jsou prohlížeče a aplikátor Windows Store (WinJS) ...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676081"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="20149-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span><span class="sxs-lookup"><span data-stu-id="20149-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="20149-104">Tento dokument poskytuje úvod do používání rozhraní HUBS API pro SignalR verze 2 v klientech JavaScriptu, jako jsou prohlížeče a aplikace Windows Store (WinJS).</span><span class="sxs-lookup"><span data-stu-id="20149-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="20149-105">Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server.</span><span class="sxs-lookup"><span data-stu-id="20149-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="20149-106">V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="20149-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="20149-107">V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="20149-108">SignalR se postará o všechny klient-to-server instalatérské pro vás.</span><span class="sxs-lookup"><span data-stu-id="20149-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="20149-109">SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="20149-110">Úvod k SignalR, rozbočovače a trvalá připojení naleznete [v tématu Úvod do SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="20149-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="20149-111">Verze softwaru použité v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="20149-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="20149-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="20149-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="20149-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="20149-113">.NET 4.5</span></span>
> - <span data-ttu-id="20149-114">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="20149-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="20149-115">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="20149-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="20149-116">Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="20149-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="20149-117">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="20149-117">Questions and comments</span></span>
>
> <span data-ttu-id="20149-118">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="20149-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="20149-119">Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="20149-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="20149-120">Přehled</span><span class="sxs-lookup"><span data-stu-id="20149-120">Overview</span></span>

<span data-ttu-id="20149-121">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="20149-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="20149-122">Vygenerovaný proxy server a co to dělá pro vás</span><span class="sxs-lookup"><span data-stu-id="20149-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="20149-123">Kdy použít vygenerovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="20149-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="20149-124">Nastavení klienta</span><span class="sxs-lookup"><span data-stu-id="20149-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="20149-125">Jak odkazovat na dynamicky generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="20149-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="20149-126">Jak vytvořit fyzický soubor pro proxy server vygenerovaný signalr</span><span class="sxs-lookup"><span data-stu-id="20149-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="20149-127">Jak navázat spojení</span><span class="sxs-lookup"><span data-stu-id="20149-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="20149-128">$.connection.hub je stejný objekt, který vytvoří $.hubConnection()</span><span class="sxs-lookup"><span data-stu-id="20149-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="20149-129">Asynchronní spuštění metody start</span><span class="sxs-lookup"><span data-stu-id="20149-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="20149-130">Jak navázat připojení mezi doménami</span><span class="sxs-lookup"><span data-stu-id="20149-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="20149-131">Jak nakonfigurovat připojení</span><span class="sxs-lookup"><span data-stu-id="20149-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="20149-132">Jak zadat parametry řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="20149-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="20149-133">Jak určit způsob přenosu</span><span class="sxs-lookup"><span data-stu-id="20149-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="20149-134">Jak získat proxy pro třídu Hub</span><span class="sxs-lookup"><span data-stu-id="20149-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="20149-135">Jak definovat metody na straně klienta, který může server volat</span><span class="sxs-lookup"><span data-stu-id="20149-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="20149-136">Jak volat metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="20149-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="20149-137">Jak zpracovat události životnosti připojení</span><span class="sxs-lookup"><span data-stu-id="20149-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="20149-138">Jak zpracovat chyby</span><span class="sxs-lookup"><span data-stu-id="20149-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="20149-139">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="20149-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="20149-140">Dokumentaci k programování serveru nebo klientů .NET naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="20149-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="20149-141">Průvodce rozhraním API hubů SignalR – server</span><span class="sxs-lookup"><span data-stu-id="20149-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="20149-142">Průvodce rozhraním API hubů SignalR – klient .NET</span><span class="sxs-lookup"><span data-stu-id="20149-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="20149-143">Součást serveru SignalR 2 je k dispozici pouze v rozhraní .NET 4.5 (i když je klient .NET pro SignalR 2 na rozhraní .NET 4.0).</span><span class="sxs-lookup"><span data-stu-id="20149-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="20149-144">Vygenerovaný proxy server a co to dělá pro vás</span><span class="sxs-lookup"><span data-stu-id="20149-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="20149-145">Můžete naprogramovat klienta JavaScript u společnosti SignalR se službou SignalR nebo bez něj, který pro vás signalr generuje.</span><span class="sxs-lookup"><span data-stu-id="20149-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="20149-146">Co proxy dělá pro vás je zjednodušit syntaxi kódu, který používáte pro připojení, psát metody, které server volá, a metody volání na serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="20149-147">Při psaní kódu pro volání serverových metod umožňuje vygenerovaný proxy server použít syntaxi, `serverMethod(arg1, arg2)` která `invoke('serverMethod', arg1, arg2)`vypadá, jako byste prováděli místní funkci: můžete místo .</span><span class="sxs-lookup"><span data-stu-id="20149-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="20149-148">Vygenerovaná syntaxe proxy také umožňuje okamžitou a srozumitelnou chybu na straně klienta, pokud nesprávně zadáte název metody serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="20149-149">A pokud ručně vytvoříte soubor, který definuje proxy servery, můžete také získat podporu IntelliSense pro psaní kódu, který volá metody serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="20149-150">Předpokládejme například, že máte na serveru následující třídu Hub:</span><span class="sxs-lookup"><span data-stu-id="20149-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="20149-151">Následující příklady kódu ukazují, jak vypadá kód JavaScript `NewContosoChatMessage` u vyvolání metody na serveru `addContosoChatMessageToPage` a přijímání vyvolání metody ze serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="20149-152">**S vygenerovaným proxy**</span><span class="sxs-lookup"><span data-stu-id="20149-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="20149-153">**Bez generovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="20149-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="20149-154">Kdy použít vygenerovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="20149-154">When to use the generated proxy</span></span>

<span data-ttu-id="20149-155">Pokud chcete zaregistrovat více obslužných rutin událostí pro klientskou metodu, kterou server volá, nemůžete použít vygenerovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="20149-156">V opačném případě můžete použít vygenerovaný proxy server nebo ne na základě předvoleb kódování.</span><span class="sxs-lookup"><span data-stu-id="20149-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="20149-157">Pokud se rozhodnete ji nepoužívat, nemusíte odkazovat na adresu URL "signalr/hubs" v `script` prvku ve vašem klientském kódu.</span><span class="sxs-lookup"><span data-stu-id="20149-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="20149-158">Nastavení klienta</span><span class="sxs-lookup"><span data-stu-id="20149-158">Client setup</span></span>

<span data-ttu-id="20149-159">Klient JavaScriptu vyžaduje odkazy na jQuery a základní javascriptový soubor SignalR.</span><span class="sxs-lookup"><span data-stu-id="20149-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="20149-160">Verze jQuery musí být 1.6.4 nebo hlavní novější verze, například 1.7.2, 1.8.2 nebo 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="20149-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="20149-161">Pokud se rozhodnete použít vygenerovaný proxy server, budete také potřebovat odkaz na signalr generovaný proxy JavaScript soubor.</span><span class="sxs-lookup"><span data-stu-id="20149-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="20149-162">Následující příklad ukazuje, jak mohou odkazy vypadat na stránce HTML, která používá generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="20149-163">Tyto odkazy musí být zahrnuty v tomto pořadí: jQuery first, SignalR core po tom a SignalR proxy naposledy.</span><span class="sxs-lookup"><span data-stu-id="20149-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="20149-164">Jak odkazovat na dynamicky generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="20149-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="20149-165">V předchozím příkladu je odkaz na proxy server generovaný SignalR dynamicky generovaný kód Jazyka JavaScript, nikoli na fyzický soubor.</span><span class="sxs-lookup"><span data-stu-id="20149-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="20149-166">SignalR vytvoří javascriptový kód pro proxy za běhu a slouží klientovi v reakci na adresu URL "/signalr/hubs".</span><span class="sxs-lookup"><span data-stu-id="20149-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="20149-167">Pokud jste ve své `MapSignalR` metodě zadali jinou základní adresu URL pro připojení SignalR na serveru, je adresa URL dynamicky generovaného souboru proxy vaší vlastní adresou URL s připojenou "/hubs".</span><span class="sxs-lookup"><span data-stu-id="20149-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="20149-168">Pro klienty JavaScriptu pro Windows 8 (Windows Store) použijte fyzický soubor proxy namísto dynamicky generovaného.</span><span class="sxs-lookup"><span data-stu-id="20149-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="20149-169">Další informace naleznete v [tématu Jak vytvořit fyzický soubor pro server proxy generovaný signalr](#manualproxy) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="20149-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="20149-170">V zobrazení ASP.NET MVC 4 nebo 5 Razor použijte vlnovku k odkazování na kořen aplikace v odkazu na soubor proxy:</span><span class="sxs-lookup"><span data-stu-id="20149-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="20149-171">Další informace o používání signalru v MVC 5 naleznete v [tématech Začínáme s signalrem a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="20149-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="20149-172">V zobrazení ASP.NET MVC 3 `Url.Content` Razor použijte pro odkaz na proxy soubor:</span><span class="sxs-lookup"><span data-stu-id="20149-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="20149-173">V aplikaci ASP.NET webových formulářů použijte `ResolveClientUrl` pro odkaz na soubor proxy servery nebo jej zaregistrujte pomocí správce skriptů pomocí relativní cesty kořenového adresáře aplikace (počínaje vlnovkou):</span><span class="sxs-lookup"><span data-stu-id="20149-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="20149-174">Obecně platí, že použijte stejnou metodu pro určení adresy URL "/signalr/hubs", kterou používáte pro soubory CSS nebo JavaScript.</span><span class="sxs-lookup"><span data-stu-id="20149-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="20149-175">Pokud zadáte adresu URL bez použití vlnovky, v některých scénářích bude aplikace fungovat správně při testování v sadě Visual Studio pomocí služby IIS Express, ale při nasazení do úplné služby IIS se nezdaří, ale při nasazení do úplné služby IIS se nezdaří chyba 404.</span><span class="sxs-lookup"><span data-stu-id="20149-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="20149-176">Další informace naleznete **v tématu Řešení odkazů na prostředky kořenové úrovně** na [webových serverech v sadě Visual Studio pro ASP.NET webových projektech](https://msdn.microsoft.com/library/58wxa9w5.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="20149-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="20149-177">Když spustíte webový projekt v Sadě Visual Studio 2017 v režimu ladění a pokud používáte Internet Explorer jako prohlížeč, můžete zobrazit soubor proxy v **Průzkumníku řešení** v části **Skripty**.</span><span class="sxs-lookup"><span data-stu-id="20149-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="20149-178">Chcete-li zobrazit obsah souboru, poklepejte na **rozbočovače**.</span><span class="sxs-lookup"><span data-stu-id="20149-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="20149-179">Pokud nepoužíváte Visual Studio 2012 nebo 2013 a Internet Explorer, nebo pokud nejste v režimu ladění, můžete také získat obsah souboru procházením adresy URL "/signalR/hubs".</span><span class="sxs-lookup"><span data-stu-id="20149-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="20149-180">Pokud je například web `http://localhost:56699`spuštěn v `http://localhost:56699/SignalR/hubs` aplikaci , přejděte do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="20149-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="20149-181">Jak vytvořit fyzický soubor pro proxy server vygenerovaný signalr</span><span class="sxs-lookup"><span data-stu-id="20149-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="20149-182">Jako alternativu k dynamicky generovanému proxy serveru můžete vytvořit fyzický soubor, který má proxy kód a odkaz na tento soubor.</span><span class="sxs-lookup"><span data-stu-id="20149-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="20149-183">Můžete to udělat pro kontrolu nad ukládáním do mezipaměti nebo sdružováním chování, nebo získat IntelliSense při kódování volání serverové metody.</span><span class="sxs-lookup"><span data-stu-id="20149-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="20149-184">Chcete-li vytvořit soubor proxy, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="20149-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="20149-185">Nainstalujte balíček [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet.</span><span class="sxs-lookup"><span data-stu-id="20149-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="20149-186">Otevřete příkazový řádek a vyhledejte složku *nástrojů,* která obsahuje soubor SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="20149-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="20149-187">Složka nástroje je v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="20149-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="20149-188">Zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="20149-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="20149-189">Cesta k *dll je* obvykle složka *bin* ve složce projektu.</span><span class="sxs-lookup"><span data-stu-id="20149-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="20149-190">Tento příkaz vytvoří soubor s názvem *server.js* ve stejné složce jako *signalr.exe*.</span><span class="sxs-lookup"><span data-stu-id="20149-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="20149-191">Vložte soubor *server.js* do příslušné složky v projektu, přejmenujte jej podle potřeby pro vaši aplikaci a přidejte na něj odkaz namísto odkazu signala/hubs.</span><span class="sxs-lookup"><span data-stu-id="20149-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="20149-192">Jak navázat spojení</span><span class="sxs-lookup"><span data-stu-id="20149-192">How to establish a connection</span></span>

<span data-ttu-id="20149-193">Před navázáním připojení je třeba vytvořit objekt připojení, vytvořit proxy server a zaregistrovat obslužné rutiny událostí pro metody, které lze volat ze serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="20149-194">Když jsou nastaveny proxy servery a obslužné rutiny událostí, navázat připojení voláním `start` metody.</span><span class="sxs-lookup"><span data-stu-id="20149-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="20149-195">Pokud používáte vygenerovaný proxy server, nemusíte vytvářet objekt připojení ve vlastním kódu, protože generovaný proxy kód to udělá za vás.</span><span class="sxs-lookup"><span data-stu-id="20149-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="20149-196">**Navázat spojení (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="20149-197">**Navázat spojení (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="20149-198">Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR.</span><span class="sxs-lookup"><span data-stu-id="20149-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="20149-199">Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="20149-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="20149-200">Ve výchozím nastavení je umístění rozbočovače aktuální mstou. Pokud se připojujete k jinému serveru, zadejte adresu URL před voláním `start` metody, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="20149-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="20149-201">Obvykle zaregistrujete obslužné rutiny událostí před voláním `start` metody k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="20149-202">Pokud chcete zaregistrovat některé obslužné rutiny událostí po navázání připojení, můžete to udělat, ale `start` musíte zaregistrovat alespoň jednu z obslužné rutiny událostí před voláním metody.</span><span class="sxs-lookup"><span data-stu-id="20149-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="20149-203">Jedním z důvodů je, že v aplikaci může být mnoho center, `OnConnected` ale nebudete chtít spustit událost v každém centru, pokud budete používat pouze pro jednu z nich.</span><span class="sxs-lookup"><span data-stu-id="20149-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="20149-204">Při navázání připojení, přítomnost metody klienta na proxy hubu je to, `OnConnected` co říká SignalR ke spuštění události.</span><span class="sxs-lookup"><span data-stu-id="20149-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="20149-205">Pokud nezaregistrujete žádné obslužné rutiny událostí před voláním `start` metody, budete moci `OnConnected` vyvolat metody v centru, ale metoda Centra nebude volána a ze serveru nebudou vyvolány žádné klientské metody.</span><span class="sxs-lookup"><span data-stu-id="20149-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="20149-206">$.connection.hub je stejný objekt, který vytvoří $.hubConnection()</span><span class="sxs-lookup"><span data-stu-id="20149-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="20149-207">Jak můžete vidět z příkladů, při použití generovanéproxy, `$.connection.hub` odkazuje na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="20149-208">Jedná se o stejný objekt, `$.hubConnection()` který získáte voláním, když nepoužíváte vygenerovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="20149-209">Generovaný proxy kód vytvoří připojení pro vás provedením následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="20149-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Vytvoření připojení v generovaném souboru proxy](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="20149-211">Pokud používáte vygenerovaný proxy server, `$.connection.hub` můžete dělat cokoliv s tím, co můžete dělat s objektem připojení, když nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="20149-212">Asynchronní spuštění metody start</span><span class="sxs-lookup"><span data-stu-id="20149-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="20149-213">Metoda `start` se provádí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="20149-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="20149-214">Vrátí [jQuery Odložené objektu](http://api.jquery.com/category/deferred-object/), což znamená, že můžete přidat `pipe` `done`funkce `fail`zpětného volání voláním metody, jako je například , a .</span><span class="sxs-lookup"><span data-stu-id="20149-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="20149-215">Pokud máte kód, který chcete spustit po navázání připojení, jako je například volání metody serveru, vložte tento kód do funkce zpětného volání nebo jej volejte z funkce zpětného volání.</span><span class="sxs-lookup"><span data-stu-id="20149-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="20149-216">Metoda `.done` zpětného volání je spuštěna po navázání připojení a po `OnConnected` spuštění kódu, který máte v metodě obslužné rutiny události na serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="20149-217">Pokud vložíte příkaz "Nyní připojeno" z předchozího příkladu `start` jako další řádek `.done` kódu za `console.log` volání metody (není v zpětném volání), řádek se spustí před navázáním připojení, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="20149-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Nesprávný způsob psaní kódu, který se spustí po navázání připojení](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="20149-219">Jak navázat připojení mezi doménami</span><span class="sxs-lookup"><span data-stu-id="20149-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="20149-220">Obvykle, pokud prohlížeč načte `http://contoso.com`stránku z , signalr připojení `http://contoso.com/signalr`je ve stejné doméně, at .</span><span class="sxs-lookup"><span data-stu-id="20149-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="20149-221">Pokud stránka `http://contoso.com` z vytvoří `http://fabrikam.com/signalr`připojení k , to je připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="20149-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="20149-222">Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázána.</span><span class="sxs-lookup"><span data-stu-id="20149-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="20149-223">V SignalR 1.x byly požadavky mezi doménami řízeny jedním příznakem EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="20149-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="20149-224">Tento příznak řídil požadavky JSONP i CORS.</span><span class="sxs-lookup"><span data-stu-id="20149-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="20149-225">Pro větší flexibilitu byla veškerá podpora CORS odebrána ze serverové součásti SignalR (javascriptoví klienti stále používají CORS normálně, pokud je zjištěno, že prohlížeč podporuje) a pro podporu těchto scénářů byl zpřístupněn nový middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="20149-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="20149-226">Pokud je jsonp požadován o klientovi (pro podporu požadavků napříč doménami ve `EnableJSONP` starších `HubConfiguration` prohlížečích), bude nutné jej explicitně povolit nastavením objektu na `true`, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="20149-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="20149-227">JSONP je ve výchozím nastavení zakázán, protože je méně bezpečný než CORS.</span><span class="sxs-lookup"><span data-stu-id="20149-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="20149-228">**Přidání microsoft.owin.cors do projektu:** Chcete-li nainstalovat tuto knihovnu, spusťte v konzole Správce balíčků následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="20149-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="20149-229">Tento příkaz přidá verzi balíčku 2.1.0 do projektu.</span><span class="sxs-lookup"><span data-stu-id="20149-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="20149-230">Volání UseCors</span><span class="sxs-lookup"><span data-stu-id="20149-230">Calling UseCors</span></span>

 <span data-ttu-id="20149-231">Následující fragment kódu ukazuje, jak implementovat připojení mezi doménami v SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="20149-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="20149-232">**Implementace požadavků mezi doménami v SignalR 2**</span><span class="sxs-lookup"><span data-stu-id="20149-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="20149-233">Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="20149-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="20149-234">Tato ukázka `Map` `RunSignalR` kódu `MapSignalR`používá a místo , tak, aby middleware CORS běží pouze pro požadavky SignalR, které `MapSignalR`vyžadují podporu CORS (spíše než pro všechny provozy na cestě určené v .) Mapa může být také použita pro jakýkoli jiný middleware, který potřebuje ke spuštění pro konkrétní předponu URL, spíše než pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="20149-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="20149-235">Nenastavujte `jQuery.support.cors` hodnotu true v kódu.</span><span class="sxs-lookup"><span data-stu-id="20149-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![Nenastavovat jQuery.support.cors na true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="20149-237">SignalR zpracovává použití CORS.</span><span class="sxs-lookup"><span data-stu-id="20149-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="20149-238">Nastavení `jQuery.support.cors` true zakáže JSONP, protože způsobí, že SignalR předpokládat, že prohlížeč podporuje CORS.</span><span class="sxs-lookup"><span data-stu-id="20149-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="20149-239">Pokud se připojujete k adrese URL localhost, aplikace Internet Explorer 10 to nebude považovat za připojení mezi doménami, takže aplikace bude pracovat místně s aplikací IE 10, i když jste na serveru nepovolili připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="20149-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="20149-240">Informace o používání připojení mezi doménami v aplikaci Internet Explorer 9 naleznete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="20149-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="20149-241">Informace o používání připojení mezi doménami v Chromu naleznete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="20149-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="20149-242">Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR.</span><span class="sxs-lookup"><span data-stu-id="20149-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="20149-243">Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="20149-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="20149-244">Jak nakonfigurovat připojení</span><span class="sxs-lookup"><span data-stu-id="20149-244">How to configure the connection</span></span>

<span data-ttu-id="20149-245">Před navázáním připojení můžete zadat parametry řetězce dotazu nebo zadat metodu přenosu.</span><span class="sxs-lookup"><span data-stu-id="20149-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="20149-246">Jak zadat parametry řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="20149-246">How to specify query string parameters</span></span>

<span data-ttu-id="20149-247">Pokud chcete odeslat data na server, když se klient připojí, můžete k objektu připojení přidat parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="20149-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="20149-248">Následující příklady ukazují, jak nastavit parametr řetězce dotazu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="20149-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="20149-249">**Nastavení hodnoty řetězce dotazu před voláním metody start (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="20149-250">**Nastavení hodnoty řetězce dotazu před voláním metody start (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="20149-251">Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="20149-252">Jak určit způsob přenosu</span><span class="sxs-lookup"><span data-stu-id="20149-252">How to specify the transport method</span></span>

<span data-ttu-id="20149-253">V rámci procesu připojení klient SignalR obvykle vyjedná se serverem určit nejlepší přenos, který je podporován serverem i klientem.</span><span class="sxs-lookup"><span data-stu-id="20149-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="20149-254">Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít `start` zadáním metody přenosu při volání metody.</span><span class="sxs-lookup"><span data-stu-id="20149-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="20149-255">**Kód klienta, který určuje způsob přenosu (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="20149-256">**Kód klienta, který určuje způsob přenosu (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="20149-257">Jako alternativu můžete zadat více metod přenosu v pořadí, ve kterém chcete SignalR vyzkoušet:</span><span class="sxs-lookup"><span data-stu-id="20149-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="20149-258">**Kód klienta, který určuje záložní schéma vlastního přenosu (s generovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="20149-259">**Kód klienta, který určuje záložní schéma vlastního přenosu (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="20149-260">Pro určení způsobu přenosu můžete použít následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="20149-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="20149-261">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="20149-261">"webSockets"</span></span>
- <span data-ttu-id="20149-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="20149-262">"foreverFrame"</span></span>
- <span data-ttu-id="20149-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="20149-263">"serverSentEvents"</span></span>
- <span data-ttu-id="20149-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="20149-264">"longPolling"</span></span>

<span data-ttu-id="20149-265">Následující příklady ukazují, jak zjistit, která způsob přenosu je používán připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="20149-266">**Kód klienta, který zobrazuje způsob přenosu používaný připojením (s generovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="20149-267">**Kód klienta, který zobrazuje způsob přenosu používaný připojením (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="20149-268">Informace o tom, jak zkontrolovat metodu přenosu v kódu serveru, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Jak získat informace o klientovi z Context vlastnost](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="20149-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="20149-269">Další informace o přenosu a záložních souborech naleznete [v tématu Úvod do SignalR - Transports a Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="20149-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="20149-270">Jak získat proxy pro třídu Hub</span><span class="sxs-lookup"><span data-stu-id="20149-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="20149-271">Každý objekt připojení, který vytvoříte zapouzdřit informace o připojení ke službě SignalR, která obsahuje jednu nebo více hub tříd.</span><span class="sxs-lookup"><span data-stu-id="20149-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="20149-272">Chcete-li komunikovat s Hub třídy, použijte proxy objekt, který vytvoříte sami (pokud nepoužíváte generované proxy) nebo který je generován pro vás.</span><span class="sxs-lookup"><span data-stu-id="20149-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="20149-273">Na straně klienta je název proxy je camel-cased verze názvu třídy Hub.</span><span class="sxs-lookup"><span data-stu-id="20149-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="20149-274">SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="20149-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="20149-275">**Třída Hub na serveru**</span><span class="sxs-lookup"><span data-stu-id="20149-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="20149-276">**Získání odkazu na vygenerovaný proxy klienta pro centrum**</span><span class="sxs-lookup"><span data-stu-id="20149-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="20149-277">**Vytvoření klientského proxy serveru pro třídu Hub (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="20149-278">Pokud vyzdobíte třídu Hub atributem, `HubName` použijte přesný název bez evidence.</span><span class="sxs-lookup"><span data-stu-id="20149-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="20149-279">**Třída Hub na serveru s atributem HubName**</span><span class="sxs-lookup"><span data-stu-id="20149-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="20149-280">**Získání odkazu na vygenerovaný proxy klienta pro centrum**</span><span class="sxs-lookup"><span data-stu-id="20149-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="20149-281">**Vytvoření klientského proxy serveru pro třídu Hub (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="20149-282">Jak definovat metody na straně klienta, který může server volat</span><span class="sxs-lookup"><span data-stu-id="20149-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="20149-283">Chcete-li definovat metodu, kterou může server volat z centra, přidejte obslužnou rutinu události do proxy centra pomocí `client` vlastnosti generovaného proxy serveru nebo tuto metodu `on` zavolejte, pokud nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="20149-284">Parametry mohou být složité objekty.</span><span class="sxs-lookup"><span data-stu-id="20149-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="20149-285">Před voláním metody k `start` navázání připojení přidejte obslužnou rutinu události.</span><span class="sxs-lookup"><span data-stu-id="20149-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="20149-286">(Pokud chcete přidat obslužné `start` rutiny událostí po volání metody, naleznete v poznámce [Jak navázat připojení](#establishconnection) dříve v tomto dokumentu a použijte syntaxi zobrazenou pro definování metody bez použití generovaného proxy serveru.)</span><span class="sxs-lookup"><span data-stu-id="20149-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="20149-287">Porovnávání názvů metod nerozlišuje malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="20149-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="20149-288">Například `Clients.All.addContosoChatMessageToPage` na serveru bude `AddContosoChatMessageToPage` `addContosoChatMessageToPage`spuštěna `addcontosochatmessagetopage` , , nebo na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="20149-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="20149-289">**Definovat metodu na straně klienta (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="20149-290">**Alternativní způsob definování metody na straně klienta (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="20149-291">**Definovat metodu na straně klienta (bez generovaného proxy serveru nebo při přidání po volání metody start)**</span><span class="sxs-lookup"><span data-stu-id="20149-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="20149-292">**Kód serveru, který volá metodu klienta**</span><span class="sxs-lookup"><span data-stu-id="20149-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="20149-293">Následující příklady zahrnují komplexní objekt jako parametr metody.</span><span class="sxs-lookup"><span data-stu-id="20149-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="20149-294">**Definovat metodu na klienta, který má složitý objekt (s generované proxy)**</span><span class="sxs-lookup"><span data-stu-id="20149-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="20149-295">**Definovat metodu na klienta, který má složitý objekt (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="20149-296">**Kód serveru, který definuje složitý objekt**</span><span class="sxs-lookup"><span data-stu-id="20149-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="20149-297">**Kód serveru, který volá metodu klienta pomocí komplexního objektu**</span><span class="sxs-lookup"><span data-stu-id="20149-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="20149-298">Jak volat metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="20149-298">How to call server methods from the client</span></span>

<span data-ttu-id="20149-299">Chcete-li volat metodu serveru `server` z klienta, použijte `invoke` vlastnost generovaného proxy serveru nebo metodu na proxy centru, pokud nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="20149-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="20149-300">Vrácená hodnota nebo parametry mohou být složité objekty.</span><span class="sxs-lookup"><span data-stu-id="20149-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="20149-301">Předajte v camel-case verzi názvu metody v centru.</span><span class="sxs-lookup"><span data-stu-id="20149-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="20149-302">SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="20149-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="20149-303">Následující příklady ukazují, jak volat metodu serveru, která nemá vrácenou hodnotu, a jak volat metodu serveru, která má vrácenou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="20149-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="20149-304">**Metoda serveru bez atributu HubMethodName**</span><span class="sxs-lookup"><span data-stu-id="20149-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="20149-305">**Kód serveru, který definuje komplexní objekt předaný v parametru**</span><span class="sxs-lookup"><span data-stu-id="20149-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="20149-306">**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="20149-307">**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="20149-308">Pokud jste dekorované Hub `HubMethodName` metoda s atributem, použijte tento název beze změny případu.</span><span class="sxs-lookup"><span data-stu-id="20149-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="20149-309">**Metoda serveru** s atributem HubMethodName</span><span class="sxs-lookup"><span data-stu-id="20149-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="20149-310">**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="20149-311">**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="20149-312">Předchozí příklady ukazují, jak volat metodu serveru, která nemá žádnou vrácenou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="20149-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="20149-313">Následující příklady ukazují, jak volat metodu serveru, která má vrácenou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="20149-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="20149-314">**Kód serveru pro metodu, která má vrácenou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="20149-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="20149-315">**Třída Stock použitá pro vrácenou** hodnotu</span><span class="sxs-lookup"><span data-stu-id="20149-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="20149-316">**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="20149-317">**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="20149-318">Jak zpracovat události životnosti připojení</span><span class="sxs-lookup"><span data-stu-id="20149-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="20149-319">SignalR poskytuje následující události životnosti připojení, které můžete zpracovat:</span><span class="sxs-lookup"><span data-stu-id="20149-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="20149-320">`starting`: Vyvolána před odesláním dat přes připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="20149-321">`received`: Vyvolána při přijetí všech dat na připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="20149-322">Poskytuje přijatá data.</span><span class="sxs-lookup"><span data-stu-id="20149-322">Provides the received data.</span></span>
- <span data-ttu-id="20149-323">`connectionSlow`: Aktivováno, když klient zjistí pomalé nebo často upadající připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="20149-324">`reconnecting`: Vyvolána při základní přenos začne znovu připojit.</span><span class="sxs-lookup"><span data-stu-id="20149-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="20149-325">`reconnected`: Aktivováno, když je základní přenos znovu připojen.</span><span class="sxs-lookup"><span data-stu-id="20149-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="20149-326">`stateChanged`: Aktivováno při změně stavu připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="20149-327">Poskytuje starý a nový stav (Připojení, Připojení, Opětovné připojení nebo Odpojeno).</span><span class="sxs-lookup"><span data-stu-id="20149-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="20149-328">`disconnected`: Aktivováno po odpojení připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="20149-329">Chcete-li například zobrazit varovné zprávy v případě problémů s připojením, které mohou způsobit znatelné zpoždění, zvládejte `connectionSlow` událost.</span><span class="sxs-lookup"><span data-stu-id="20149-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="20149-330">**Zpracování události connectionSlow (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="20149-331">**Zpracování události connectionSlow (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="20149-332">Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="20149-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="20149-333">Jak zpracovat chyby</span><span class="sxs-lookup"><span data-stu-id="20149-333">How to handle errors</span></span>

<span data-ttu-id="20149-334">Klient JavaScript SignalR `error` poskytuje událost, pro kterou můžete přidat obslužnou rutinu.</span><span class="sxs-lookup"><span data-stu-id="20149-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="20149-335">Metodu fail můžete také použít k přidání obslužné rutiny pro chyby, které vyplývají z vyvolání metody serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="20149-336">Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který signalr vrátí po chybě, obsahuje minimální informace o chybě.</span><span class="sxs-lookup"><span data-stu-id="20149-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="20149-337">Pokud se `newContosoChatMessage` například volání nezdaří, chybová zpráva`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`v objektu chyby obsahuje " Odesílání podrobných chybových zpráv klientům v produkčním prostředí se nedoporučuje z bezpečnostních důvodů, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.</span><span class="sxs-lookup"><span data-stu-id="20149-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="20149-338">Následující příklad ukazuje, jak přidat obslužnou rutinu pro událost chyby.</span><span class="sxs-lookup"><span data-stu-id="20149-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="20149-339">**Přidání obslužné rutiny chyby (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="20149-340">**Přidání obslužné rutiny chyby (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="20149-341">Následující příklad ukazuje, jak zpracovat chybu z vyvolání metody.</span><span class="sxs-lookup"><span data-stu-id="20149-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="20149-342">**Zpracování chyby z vyvolání metody (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="20149-343">**Zpracování chyby z vyvolání metody (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="20149-344">Pokud volání metody selže, `error` je vyvolána také událost, `error` takže váš `.fail` kód v obslužné rutině metody a v zpětném volání metody by se spustil.</span><span class="sxs-lookup"><span data-stu-id="20149-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="20149-345">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="20149-345">How to enable client-side logging</span></span>

<span data-ttu-id="20149-346">Chcete-li povolit protokolování na `logging` straně klienta na připojení, `start` nastavte vlastnost objektu připojení před voláním metody k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="20149-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="20149-347">**Povolit protokolování (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="20149-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="20149-348">**Povolit protokolování (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="20149-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="20149-349">Chcete-li zobrazit protokoly, otevřete vývojářské nástroje prohlížeče a přejděte na kartu Konzola. Pro výukový program, který zobrazuje podrobné pokyny a snímky obrazovek, které ukazují, jak to udělat, naleznete [v tématu Vysílání serveru s ASP.NET Signalr - Povolit protokolování](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span><span class="sxs-lookup"><span data-stu-id="20149-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
