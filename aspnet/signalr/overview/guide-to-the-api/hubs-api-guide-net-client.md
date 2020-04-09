---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET Průvodce rozhraním API center signalr - klient .NET (C#) | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod k použití rozhraní API hubs pro SignalR verze 2 v klientech .NET, jako je Windows Store (WinRT), WPF, Silverlight a nevýhody...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676333"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="c73ff-103">ASP.NET SignalR Hubs API Guide - klient .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="c73ff-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c73ff-104">Tento dokument poskytuje úvod k použití rozhraní API hubs pro SignalR verze 2 v klientech .NET, jako jsou Windows Store (WinRT), WPF, Silverlight a konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="c73ff-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="c73ff-105">Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server.</span><span class="sxs-lookup"><span data-stu-id="c73ff-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="c73ff-106">V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="c73ff-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="c73ff-107">V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="c73ff-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="c73ff-108">SignalR se postará o všechny klient-to-server instalatérské pro vás.</span><span class="sxs-lookup"><span data-stu-id="c73ff-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="c73ff-109">SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="c73ff-110">Úvod do SignalR, Rozbočovače a trvalá připojení nebo pro kurz, který ukazuje, jak vytvořit kompletní aplikaci SignalR, naleznete v [tématu SignalR - Začínáme](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="c73ff-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c73ff-111">Verze softwaru použité v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="c73ff-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c73ff-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c73ff-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="c73ff-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c73ff-113">.NET 4.5</span></span>
> - <span data-ttu-id="c73ff-114">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="c73ff-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c73ff-115">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="c73ff-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c73ff-116">Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="c73ff-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c73ff-117">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="c73ff-117">Questions and comments</span></span>
>
> <span data-ttu-id="c73ff-118">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="c73ff-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c73ff-119">Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="c73ff-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c73ff-120">Přehled</span><span class="sxs-lookup"><span data-stu-id="c73ff-120">Overview</span></span>

<span data-ttu-id="c73ff-121">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="c73ff-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="c73ff-122">Nastavení klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="c73ff-123">Jak navázat spojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="c73ff-124">Připojení mezi doménami od klientů Silverlight</span><span class="sxs-lookup"><span data-stu-id="c73ff-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="c73ff-125">Jak nakonfigurovat připojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="c73ff-126">Jak nastavit maximální počet souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="c73ff-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="c73ff-127">Jak zadat parametry řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="c73ff-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="c73ff-128">Jak určit způsob přenosu</span><span class="sxs-lookup"><span data-stu-id="c73ff-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="c73ff-129">Jak zadat hlavičky HTTP</span><span class="sxs-lookup"><span data-stu-id="c73ff-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="c73ff-130">Jak zadat klientské certifikáty</span><span class="sxs-lookup"><span data-stu-id="c73ff-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="c73ff-131">Jak vytvořit server proxy hubu</span><span class="sxs-lookup"><span data-stu-id="c73ff-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="c73ff-132">Jak definovat metody na straně klienta, který může server volat</span><span class="sxs-lookup"><span data-stu-id="c73ff-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="c73ff-133">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="c73ff-134">Metody s parametry, určení typů parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="c73ff-135">Metody s parametry, určení dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="c73ff-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="c73ff-136">Odebrání obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="c73ff-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="c73ff-137">Jak volat metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="c73ff-138">Jak zpracovat události životnosti připojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="c73ff-139">Jak zpracovat chyby</span><span class="sxs-lookup"><span data-stu-id="c73ff-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="c73ff-140">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="c73ff-141">Ukázky kódu aplikace WPF, Silverlight a konzoly pro klientské metody, které může server volat</span><span class="sxs-lookup"><span data-stu-id="c73ff-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="c73ff-142">Ukázkové klientské projekty .NET naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="c73ff-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="c73ff-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, příklady konzolových aplikací).</span><span class="sxs-lookup"><span data-stu-id="c73ff-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="c73ff-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) na GitHub.com (příklad WPF).</span><span class="sxs-lookup"><span data-stu-id="c73ff-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="c73ff-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) na GitHub.com (příklad konzolové aplikace).</span><span class="sxs-lookup"><span data-stu-id="c73ff-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="c73ff-146">Dokumentaci k programování klientů jazyka JavaScript naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="c73ff-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="c73ff-147">Průvodce rozhraním API hubů SignalR – server</span><span class="sxs-lookup"><span data-stu-id="c73ff-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="c73ff-148">SignalR Hubs API Guide - Klient JavaScript</span><span class="sxs-lookup"><span data-stu-id="c73ff-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="c73ff-149">Odkazy na referenční témata rozhraní API jsou na verzi rozhraní .NET 4.5 rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="c73ff-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="c73ff-150">Pokud používáte rozhraní .NET 4, přečtěte si [verzi rozhraní API .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="c73ff-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="c73ff-151">Nastavení klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-151">Client setup</span></span>

<span data-ttu-id="c73ff-152">Nainstalujte balíček [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (nikoli balíček [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr)</span><span class="sxs-lookup"><span data-stu-id="c73ff-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="c73ff-153">Tento balíček podporuje klienty WinRT, Silverlight, WPF, konzolové aplikace a Windows Phone pro rozhraní .NET 4 i .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="c73ff-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="c73ff-154">Pokud verze SignalR, které máte na straně klienta se liší od verze, kterou máte na serveru, SignalR je často schopen přizpůsobit se rozdílu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="c73ff-155">Například server se systémem SignalR verze 2 bude podporovat klienty s nainstalovanou verzí 1.1.x a také klienty, kteří mají nainstalovanou verzi 2.</span><span class="sxs-lookup"><span data-stu-id="c73ff-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="c73ff-156">Pokud je rozdíl mezi verzí na serveru a verzí na straně klienta příliš velký nebo pokud je `InvalidOperationException` klient novější než server, signalr vyvolá výjimku, když se klient pokusí navázat připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="c73ff-157">Chybová zpráva`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`je " ".</span><span class="sxs-lookup"><span data-stu-id="c73ff-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="c73ff-158">Jak navázat spojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-158">How to establish a connection</span></span>

<span data-ttu-id="c73ff-159">Před navázáním připojení je třeba `HubConnection` vytvořit objekt a vytvořit proxy server.</span><span class="sxs-lookup"><span data-stu-id="c73ff-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="c73ff-160">Chcete-li navázat připojení, `Start` volání `HubConnection` metody na objektu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="c73ff-161">Pro klienty JavaScriptu musíte před voláním `Start` metody k navázání připojení zaregistrovat alespoň jednu obslužnou rutinu události.</span><span class="sxs-lookup"><span data-stu-id="c73ff-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="c73ff-162">To není nutné pro klienty .NET.</span><span class="sxs-lookup"><span data-stu-id="c73ff-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="c73ff-163">Pro klienty JavaScriptu generovaný proxy kód automaticky vytvoří proxy servery pro všechna centra, která existují na serveru, a registrace obslužné rutiny je způsob, jakým označíte, které centra má váš klient v úmyslu použít.</span><span class="sxs-lookup"><span data-stu-id="c73ff-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="c73ff-164">Ale pro klienta .NET vytvoříte servery proxy hub ručně, takže SignalR předpokládá, že budete používat libovolné centrum, pro které vytvoříte proxy server.</span><span class="sxs-lookup"><span data-stu-id="c73ff-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="c73ff-165">Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR.</span><span class="sxs-lookup"><span data-stu-id="c73ff-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c73ff-166">Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="c73ff-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="c73ff-167">Metoda `Start` se provádí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="c73ff-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="c73ff-168">Chcete-li se ujistit, že následující řádky kódu se `await` nespustí až po navázání připojení, `.Wait()` použijte v ASP.NET 4.5 asynchronní metody nebo v synchronní metodě.</span><span class="sxs-lookup"><span data-stu-id="c73ff-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="c73ff-169">Nepoužívejte `.Wait()` v klientovi WinRT.</span><span class="sxs-lookup"><span data-stu-id="c73ff-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="c73ff-170">Připojení mezi doménami od klientů Silverlight</span><span class="sxs-lookup"><span data-stu-id="c73ff-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="c73ff-171">Informace o povolení připojení mezi doménami z klientů Silverlight naleznete [v tématu Zpřístupnění služby přes hranice domény](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="c73ff-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="c73ff-172">Jak nakonfigurovat připojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-172">How to configure the connection</span></span>

<span data-ttu-id="c73ff-173">Před navázáním připojení můžete určit některou z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="c73ff-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="c73ff-174">Limit souběžných připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="c73ff-175">Parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-175">Query string parameters.</span></span>
- <span data-ttu-id="c73ff-176">Způsob přenosu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-176">The transport method.</span></span>
- <span data-ttu-id="c73ff-177">Hlavičky HTTP.</span><span class="sxs-lookup"><span data-stu-id="c73ff-177">HTTP headers.</span></span>
- <span data-ttu-id="c73ff-178">Klientské certifikáty.</span><span class="sxs-lookup"><span data-stu-id="c73ff-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="c73ff-179">Jak nastavit maximální počet souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="c73ff-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="c73ff-180">V klientech WPF bude pravděpodobně muset zvýšit maximální počet souběžných připojení z výchozí hodnoty 2.</span><span class="sxs-lookup"><span data-stu-id="c73ff-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="c73ff-181">Doporučená hodnota je 10.</span><span class="sxs-lookup"><span data-stu-id="c73ff-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="c73ff-182">Další informace naleznete v tématu [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="c73ff-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="c73ff-183">Jak zadat parametry řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="c73ff-183">How to specify query string parameters</span></span>

<span data-ttu-id="c73ff-184">Pokud chcete odeslat data na server, když se klient připojí, můžete k objektu připojení přidat parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="c73ff-185">Následující příklad ukazuje, jak nastavit parametr řetězce dotazu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="c73ff-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="c73ff-186">Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="c73ff-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="c73ff-187">Jak určit způsob přenosu</span><span class="sxs-lookup"><span data-stu-id="c73ff-187">How to specify the transport method</span></span>

<span data-ttu-id="c73ff-188">V rámci procesu připojení klient SignalR obvykle vyjedná se serverem určit nejlepší přenos, který je podporován serverem i klientem.</span><span class="sxs-lookup"><span data-stu-id="c73ff-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="c73ff-189">Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít.</span><span class="sxs-lookup"><span data-stu-id="c73ff-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="c73ff-190">Chcete-li určit metodu přenosu, přejděte v objektu přenosu do metody Start.</span><span class="sxs-lookup"><span data-stu-id="c73ff-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="c73ff-191">Následující příklad ukazuje, jak určit metodu přenosu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="c73ff-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="c73ff-192">Obor názvů [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) obsahuje následující třídy, které můžete použít k určení přenosu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="c73ff-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="c73ff-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="c73ff-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="c73ff-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="c73ff-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (K dispozici pouze v případě, že server i klient používají rozhraní .NET 4.5.)</span><span class="sxs-lookup"><span data-stu-id="c73ff-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="c73ff-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automaticky vybere nejlepší přenos, který je podporován klientem i serverem.</span><span class="sxs-lookup"><span data-stu-id="c73ff-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="c73ff-197">Toto je výchozí přenos.</span><span class="sxs-lookup"><span data-stu-id="c73ff-197">This is the default transport.</span></span> <span data-ttu-id="c73ff-198">Předání této `Start` metody má stejný účinek jako nepředávání v ničem.)</span><span class="sxs-lookup"><span data-stu-id="c73ff-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="c73ff-199">Přenos ForeverFrame není zahrnuta v tomto seznamu, protože je používán pouze prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="c73ff-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="c73ff-200">Informace o tom, jak zkontrolovat metodu přenosu v kódu serveru, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Jak získat informace o klientovi z Context vlastnost](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="c73ff-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="c73ff-201">Další informace o přenosu a záložních souborech naleznete [v tématu Úvod do SignalR - Transports a Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="c73ff-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="c73ff-202">Jak zadat hlavičky HTTP</span><span class="sxs-lookup"><span data-stu-id="c73ff-202">How to specify HTTP headers</span></span>

<span data-ttu-id="c73ff-203">Chcete-li nastavit záhlaví `Headers` protokolu HTTP, použijte vlastnost objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="c73ff-204">Následující příklad ukazuje, jak přidat hlavičku HTTP.</span><span class="sxs-lookup"><span data-stu-id="c73ff-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="c73ff-205">Jak zadat klientské certifikáty</span><span class="sxs-lookup"><span data-stu-id="c73ff-205">How to specify client certificates</span></span>

<span data-ttu-id="c73ff-206">Chcete-li přidat klientské `AddClientCertificate` certifikáty, použijte metodu na objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="c73ff-207">Jak vytvořit server proxy hubu</span><span class="sxs-lookup"><span data-stu-id="c73ff-207">How to create the Hub proxy</span></span>

<span data-ttu-id="c73ff-208">Chcete-li definovat metody na straně klienta, který může centrum volat ze serveru, a vyvolat metody v `CreateHubProxy` centru na serveru, vytvořte proxy server pro centrum voláním objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="c73ff-209">Řetězec, do `CreateHubProxy` kterého se předáváte, je název třídy `HubName` Hub nebo název určený atributem, pokud byl použit na serveru.</span><span class="sxs-lookup"><span data-stu-id="c73ff-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="c73ff-210">Porovnávání názvů nerozlišuje malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="c73ff-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="c73ff-211">**Třída Hub na serveru**</span><span class="sxs-lookup"><span data-stu-id="c73ff-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="c73ff-212">**Vytvoření klientského proxy serveru pro třídu Hub**</span><span class="sxs-lookup"><span data-stu-id="c73ff-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="c73ff-213">Pokud vyzdobíte třídu Hub atributem, `HubName` použijte tento název.</span><span class="sxs-lookup"><span data-stu-id="c73ff-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="c73ff-214">**Třída Hub na serveru**</span><span class="sxs-lookup"><span data-stu-id="c73ff-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="c73ff-215">**Vytvoření klientského proxy serveru pro třídu Hub**</span><span class="sxs-lookup"><span data-stu-id="c73ff-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="c73ff-216">Pokud zavoláte `HubConnection.CreateHubProxy` vícekrát `hubName`se stejným , získáte `IHubProxy` stejný objekt uložený v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="c73ff-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c73ff-217">Jak definovat metody na straně klienta, který může server volat</span><span class="sxs-lookup"><span data-stu-id="c73ff-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="c73ff-218">Chcete-li definovat metodu, kterou může server `On` volat, použijte metodu proxy k registraci obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="c73ff-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="c73ff-219">Porovnávání názvů metod nerozlišuje malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="c73ff-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="c73ff-220">Například `Clients.All.UpdateStockPrice` na serveru bude `updateStockPrice` `updatestockprice`spuštěna `UpdateStockPrice` , , nebo na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="c73ff-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="c73ff-221">Různé klientské platformy mají různé požadavky na způsob psaní kódu metody pro aktualizaci ui.</span><span class="sxs-lookup"><span data-stu-id="c73ff-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="c73ff-222">Uvedené příklady jsou pro klienty WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="c73ff-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="c73ff-223">Příklady aplikací WPF, Silverlight a konzoly jsou uvedeny v [samostatné části dále v tomto tématu](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="c73ff-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="c73ff-224">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-224">Methods without parameters</span></span>

<span data-ttu-id="c73ff-225">Pokud metoda, kterou zpracováváte, nemá parametry, použijte neobecné `On` přetížení metody:</span><span class="sxs-lookup"><span data-stu-id="c73ff-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="c73ff-226">**Klientská metoda volání kódu serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="c73ff-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="c73ff-227">**Kód klienta WinRT pro metodu volanou ze serveru bez parametrů[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="c73ff-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c73ff-228">Metody s parametry, určení typů parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="c73ff-229">Pokud metoda, kterou zpracováváte, má parametry, zadejte typy parametrů `On` jako obecné typy metody.</span><span class="sxs-lookup"><span data-stu-id="c73ff-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="c73ff-230">Existují obecné přetížení `On` metody, která vám umožní zadat až 8 parametrů (4 na Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="c73ff-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="c73ff-231">V následujícím příkladu je do `UpdateStockPrice` metody odeslán jeden parametr.</span><span class="sxs-lookup"><span data-stu-id="c73ff-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="c73ff-232">**Serverkód volá metodu klienta s parametrem**</span><span class="sxs-lookup"><span data-stu-id="c73ff-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="c73ff-233">**Třída Stock použitá pro parametr**</span><span class="sxs-lookup"><span data-stu-id="c73ff-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="c73ff-234">**Kód klienta WinRT pro metodu volanou ze serveru s parametrem[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="c73ff-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c73ff-235">Metody s parametry, určení dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="c73ff-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="c73ff-236">Jako alternativu k určení parametrů jako `On` obecných typů metody můžete zadat parametry jako dynamické objekty:</span><span class="sxs-lookup"><span data-stu-id="c73ff-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="c73ff-237">**Serverkód volá metodu klienta s parametrem**</span><span class="sxs-lookup"><span data-stu-id="c73ff-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="c73ff-238">**Třída Stock použitá pro parametr**</span><span class="sxs-lookup"><span data-stu-id="c73ff-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="c73ff-239">**Kód klienta WinRT pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="c73ff-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="c73ff-240">Odebrání obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="c73ff-240">How to remove a handler</span></span>

<span data-ttu-id="c73ff-241">Chcete-li odebrat `Dispose` obslužnou rutinu, zavolejte její metodu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="c73ff-242">**Kód klienta pro metodu volanou ze serveru**</span><span class="sxs-lookup"><span data-stu-id="c73ff-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="c73ff-243">**Kód klienta pro odebrání obslužné rutiny**</span><span class="sxs-lookup"><span data-stu-id="c73ff-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="c73ff-244">Jak volat metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-244">How to call server methods from the client</span></span>

<span data-ttu-id="c73ff-245">Chcete-li volat metodu na `Invoke` serveru, použijte metodu na proxy hubu.</span><span class="sxs-lookup"><span data-stu-id="c73ff-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="c73ff-246">Pokud metoda serveru nemá žádnou vrácenou hodnotu, `Invoke` použijte neobecné přetížení metody.</span><span class="sxs-lookup"><span data-stu-id="c73ff-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="c73ff-247">**Kód serveru pro metodu, která nemá žádnou vrácenou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="c73ff-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="c73ff-248">**Kód klienta volající metodu, která nemá žádnou vrácenou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="c73ff-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="c73ff-249">Pokud má metoda serveru vrácenou hodnotu, zadejte jako `Invoke` obecný typ metody návratový typ.</span><span class="sxs-lookup"><span data-stu-id="c73ff-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="c73ff-250">**Kód serveru pro metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu**</span><span class="sxs-lookup"><span data-stu-id="c73ff-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="c73ff-251">**Třída Stock použitá pro parametr a vrácenou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="c73ff-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="c73ff-252">**Klientský kód volající metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu v ASP.NET asynchronní metodě 4.5**</span><span class="sxs-lookup"><span data-stu-id="c73ff-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="c73ff-253">**Klientský kód volající metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu v synchronní metodě**</span><span class="sxs-lookup"><span data-stu-id="c73ff-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="c73ff-254">Metoda `Invoke` se spustí asynchronně a `Task` vrátí objekt.</span><span class="sxs-lookup"><span data-stu-id="c73ff-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="c73ff-255">Pokud nezadáte `await` nebo `.Wait()`, další řádek kódu se spustí před metoda, kterou vyvolat dokončil provádění.</span><span class="sxs-lookup"><span data-stu-id="c73ff-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="c73ff-256">Jak zpracovat události životnosti připojení</span><span class="sxs-lookup"><span data-stu-id="c73ff-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="c73ff-257">SignalR poskytuje následující události životnosti připojení, které můžete zpracovat:</span><span class="sxs-lookup"><span data-stu-id="c73ff-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="c73ff-258">`Received`: Vyvolána při přijetí všech dat na připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="c73ff-259">Poskytuje přijatá data.</span><span class="sxs-lookup"><span data-stu-id="c73ff-259">Provides the received data.</span></span>
- <span data-ttu-id="c73ff-260">`ConnectionSlow`: Aktivováno, když klient zjistí pomalé nebo často upadající připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="c73ff-261">`Reconnecting`: Vyvolána při základní přenos začne znovu připojit.</span><span class="sxs-lookup"><span data-stu-id="c73ff-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="c73ff-262">`Reconnected`: Aktivováno, když je základní přenos znovu připojen.</span><span class="sxs-lookup"><span data-stu-id="c73ff-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="c73ff-263">`StateChanged`: Aktivováno při změně stavu připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="c73ff-264">Poskytuje starý a nový stav.</span><span class="sxs-lookup"><span data-stu-id="c73ff-264">Provides the old state and the new state.</span></span> <span data-ttu-id="c73ff-265">Informace o hodnotách stavu připojení naleznete v [tématu ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="c73ff-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="c73ff-266">`Closed`: Aktivováno po odpojení připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="c73ff-267">Chcete-li například zobrazit varovné zprávy pro chyby, které nejsou závažné, ale způsobit občasné `ConnectionSlow` problémy s připojením, jako je například pomalost nebo časté přetažení připojení, zpracovat událost.</span><span class="sxs-lookup"><span data-stu-id="c73ff-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="c73ff-268">Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="c73ff-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="c73ff-269">Jak zpracovat chyby</span><span class="sxs-lookup"><span data-stu-id="c73ff-269">How to handle errors</span></span>

<span data-ttu-id="c73ff-270">Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který signalr vrátí po chybě, obsahuje minimální informace o chybě.</span><span class="sxs-lookup"><span data-stu-id="c73ff-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="c73ff-271">Pokud se `newContosoChatMessage` například volání nezdaří, chybová zpráva`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`v objektu chyby obsahuje " Odesílání podrobných chybových zpráv klientům v produkčním prostředí se nedoporučuje z bezpečnostních důvodů, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.</span><span class="sxs-lookup"><span data-stu-id="c73ff-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="c73ff-272">Chcete-li zpracovat chyby, které signalr `Error` vyvolává, můžete přidat obslužnou rutinu pro událost na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="c73ff-273">Chcete-li zpracovat chyby z vyvolání metody, zabalte kód do bloku try-catch.</span><span class="sxs-lookup"><span data-stu-id="c73ff-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="c73ff-274">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="c73ff-274">How to enable client-side logging</span></span>

<span data-ttu-id="c73ff-275">Chcete-li povolit protokolování `TraceLevel` `TraceWriter` na straně klienta, nastavte vlastnosti a na objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="c73ff-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="c73ff-276">Ukázky kódu aplikace WPF, Silverlight a konzoly pro klientské metody, které může server volat</span><span class="sxs-lookup"><span data-stu-id="c73ff-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="c73ff-277">Vzorky kódu zobrazené dříve pro definování klientských metod, které může server volat, platí pro klienty WinRT.</span><span class="sxs-lookup"><span data-stu-id="c73ff-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="c73ff-278">Následující ukázky ukazují ekvivalentní kód pro wpf, Silverlight a konzolové aplikační klienty.</span><span class="sxs-lookup"><span data-stu-id="c73ff-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="c73ff-279">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-279">Methods without parameters</span></span>

<span data-ttu-id="c73ff-280">**Kód klienta WPF pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="c73ff-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="c73ff-281">**Kód klienta Silverlight pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="c73ff-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="c73ff-282">**Klientský kód konzoly pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="c73ff-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c73ff-283">Metody s parametry, určení typů parametrů</span><span class="sxs-lookup"><span data-stu-id="c73ff-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="c73ff-284">**Kód klienta WPF pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="c73ff-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="c73ff-285">**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="c73ff-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="c73ff-286">**Kód klienta konzoly pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="c73ff-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c73ff-287">Metody s parametry, určení dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="c73ff-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="c73ff-288">**Kód klienta WPF pro metodu volanou ze serveru s parametrem, pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="c73ff-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="c73ff-289">**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="c73ff-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="c73ff-290">**Klientský kód konzoly pro metodu volanou ze serveru s parametrem, pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="c73ff-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
