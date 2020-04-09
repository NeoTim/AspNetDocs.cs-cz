---
uid: signalr/overview/performance/signalr-performance
title: Výkon signalismu | Dokumenty společnosti Microsoft
author: bradygaster
description: Výkon aplikace SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676088"
---
# <a name="signalr-performance"></a><span data-ttu-id="8039d-103">Výkon aplikace SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-103">SignalR Performance</span></span>

<span data-ttu-id="8039d-104">podle [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8039d-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="8039d-105">Toto téma popisuje, jak navrhnout, měřit a zlepšit výkon v aplikaci SignalR.</span><span class="sxs-lookup"><span data-stu-id="8039d-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="8039d-106">Verze softwaru použité v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="8039d-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="8039d-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8039d-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="8039d-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="8039d-108">.NET 4.5</span></span>
> - <span data-ttu-id="8039d-109">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="8039d-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="8039d-110">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="8039d-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="8039d-111">Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="8039d-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="8039d-112">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="8039d-112">Questions and comments</span></span>
>
> <span data-ttu-id="8039d-113">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="8039d-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="8039d-114">Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="8039d-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="8039d-115">Poslední prezentace o výkonu signalr a škálování naleznete [v tématu škálování v reálném čase web s ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="8039d-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="8039d-116">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="8039d-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="8039d-117">Na co dát pozor při navrhování</span><span class="sxs-lookup"><span data-stu-id="8039d-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="8039d-118">Optimalizace výkonu serveru SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="8039d-119">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="8039d-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="8039d-120">Použití čítačů výkonu SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="8039d-121">Použití jiných čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="8039d-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="8039d-122">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="8039d-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="8039d-123">Na co dát pozor při navrhování</span><span class="sxs-lookup"><span data-stu-id="8039d-123">Design considerations</span></span>

<span data-ttu-id="8039d-124">Tato část popisuje vzory, které mohou být implementovány během návrhu aplikace SignalR, aby bylo zajištěno, že výkon není bráněno generováním zbytečného síťového provozu.</span><span class="sxs-lookup"><span data-stu-id="8039d-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="8039d-125">Četnost omezení zpráv</span><span class="sxs-lookup"><span data-stu-id="8039d-125">Throttling message frequency</span></span>

<span data-ttu-id="8039d-126">Dokonce i v aplikaci, která odesílá zprávy na vysoké frekvenci (například herní aplikace v reálném čase), většina aplikací nemusí odesílat více než několik zpráv za sekundu.</span><span class="sxs-lookup"><span data-stu-id="8039d-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="8039d-127">Chcete-li snížit množství provozu, který generuje každý klient, může být implementována smyčka zpráv, která fronty a odesílá zprávy ne častěji než pevná sazba (to znamená, že až určitý počet zpráv bude odeslána každou sekundu, pokud jsou zprávy v tomto časovém intervalu, které mají být odeslány).</span><span class="sxs-lookup"><span data-stu-id="8039d-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="8039d-128">Ukázková aplikace, která omezuje zprávy na určitou rychlost (z klienta i serveru), naleznete [v tématu Vysokofrekvenční realtime s SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="8039d-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="8039d-129">Zmenšení velikosti zprávy</span><span class="sxs-lookup"><span data-stu-id="8039d-129">Reducing message size</span></span>

<span data-ttu-id="8039d-130">Velikost zprávy SignalR můžete zmenšit zmenšením velikosti serializovaných objektů.</span><span class="sxs-lookup"><span data-stu-id="8039d-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="8039d-131">Pokud v kódu serveru odesíláte objekt, který obsahuje vlastnosti, které není nutné přenášet, `JsonIgnore` zabraňte serializace těchto vlastností pomocí atributu.</span><span class="sxs-lookup"><span data-stu-id="8039d-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="8039d-132">Názvy vlastností jsou také uloženy ve zprávě; názvy vlastností lze zkrátit `JsonProperty` pomocí atributu.</span><span class="sxs-lookup"><span data-stu-id="8039d-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="8039d-133">Následující ukázka kódu ukazuje, jak vyloučit vlastnost z odesílané klientovi a jak zkrátit názvy vlastností:</span><span class="sxs-lookup"><span data-stu-id="8039d-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="8039d-134">**Kód serveru .NET, který demonstruje atribut JsonIgnore k vyloučení dat odesílaných klientovi, a atribut JsonProperty pro zmenšení velikosti zprávy**</span><span class="sxs-lookup"><span data-stu-id="8039d-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="8039d-135">Chcete-li zachovat čitelnost/ udržovatelnost v kódu klienta, zkrácené názvy vlastností mohou být po přijetí zprávy přemapovány na názvy vhodné pro člověka.</span><span class="sxs-lookup"><span data-stu-id="8039d-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="8039d-136">Následující ukázka kódu ukazuje jeden možný způsob přemapování zkrácené názvy na delší, definováním `reMap` zprávy smlouvy (mapování) a pomocí funkce použít smlouvu na optimalizované třídy zpráv:</span><span class="sxs-lookup"><span data-stu-id="8039d-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="8039d-137">**Kód JavaScriptu na straně klienta, který přemapuje zkrácené názvy vlastností na názvy čitelné pro člověka**</span><span class="sxs-lookup"><span data-stu-id="8039d-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="8039d-138">Názvy lze zkrátit ve zprávách z klienta na server také pomocí stejné metody.</span><span class="sxs-lookup"><span data-stu-id="8039d-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="8039d-139">Snížení nároku na paměť (to znamená množství paměti použité pro zprávu) objektu zprávy může také zlepšit výkon.</span><span class="sxs-lookup"><span data-stu-id="8039d-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="8039d-140">Například pokud není potřeba `int` celý rozsah, `short` nebo `byte` lze použít místo.</span><span class="sxs-lookup"><span data-stu-id="8039d-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="8039d-141">Vzhledem k tomu, že zprávy jsou uloženy v sběrnici zpráv v paměti serveru, snížení velikosti zpráv může také řešit problémy s pamětí serveru.</span><span class="sxs-lookup"><span data-stu-id="8039d-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="8039d-142">Optimalizace výkonu serveru SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="8039d-143">Následující nastavení konfigurace lze vyladit server pro lepší výkon v aplikaci SignalR.</span><span class="sxs-lookup"><span data-stu-id="8039d-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="8039d-144">Obecné informace o tom, jak zlepšit výkon v aplikaci ASP.NET, naleznete [v tématu Zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="8039d-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="8039d-145">**Nastavení konfigurace SignalR**</span><span class="sxs-lookup"><span data-stu-id="8039d-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="8039d-146">**DefaultMessageBufferSize**: Ve výchozím nastavení SignalR uchovává 1000 zpráv v paměti na rozbočovač na připojení.</span><span class="sxs-lookup"><span data-stu-id="8039d-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="8039d-147">Pokud jsou používány velké zprávy, to může způsobit problémy s pamětí, které lze zmírnit snížením této hodnoty.</span><span class="sxs-lookup"><span data-stu-id="8039d-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="8039d-148">Toto nastavení lze `Application_Start` nastavit v obslužné `Configuration` rutině události v ASP.NET aplikaci nebo v metodě spouštěcí třídy OWIN v samoobslužné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8039d-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="8039d-149">Následující ukázka ukazuje, jak snížit tuto hodnotu, aby se snížila nároky na paměť vaší aplikace, aby se snížilo množství použité paměti serveru:</span><span class="sxs-lookup"><span data-stu-id="8039d-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="8039d-150">**Kód serveru .NET v Startup.cs pro snížení výchozí velikosti vyrovnávací paměti zprávy**</span><span class="sxs-lookup"><span data-stu-id="8039d-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="8039d-151">**Nastavení konfigurace služby IIS**</span><span class="sxs-lookup"><span data-stu-id="8039d-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="8039d-152">**Maximální počet souběžných požadavků na aplikaci**: Zvýšení počtu souběžných požadavků služby IIS zvýší prostředky serveru, které jsou k dispozici pro obsluhování požadavků.</span><span class="sxs-lookup"><span data-stu-id="8039d-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="8039d-153">Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, proveďte v příkazovém řádku se zvýšenými oprávněními následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="8039d-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="8039d-154">**ApplicationPool QueueLength**: Toto je maximální počet požadavků, které http.sys fronty pro fond aplikací.</span><span class="sxs-lookup"><span data-stu-id="8039d-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="8039d-155">Když je fronta plná, nové požadavky obdrží odpověď 503 "Služba není k dispozici".</span><span class="sxs-lookup"><span data-stu-id="8039d-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="8039d-156">Výchozí hodnota je 1000.</span><span class="sxs-lookup"><span data-stu-id="8039d-156">The default value is 1000.</span></span>

    <span data-ttu-id="8039d-157">Zkrácení délky fronty pro pracovní proces ve fondu aplikací, který je hostitelem vaší aplikace, šetří paměťové prostředky.</span><span class="sxs-lookup"><span data-stu-id="8039d-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="8039d-158">Další informace naleznete v [tématu Správa, optimalizace a konfigurace fondů aplikací](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="8039d-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="8039d-159">**ASP.NET nastavení konfigurace**</span><span class="sxs-lookup"><span data-stu-id="8039d-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="8039d-160">Tato část obsahuje nastavení konfigurace, `aspnet.config` která lze nastavit v souboru.</span><span class="sxs-lookup"><span data-stu-id="8039d-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="8039d-161">Tento soubor se nachází v jednom ze dvou umístění, v závislosti na platformě:</span><span class="sxs-lookup"><span data-stu-id="8039d-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="8039d-162">ASP.NET nastavení, která mohou zlepšit výkon SignalR patří následující:</span><span class="sxs-lookup"><span data-stu-id="8039d-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="8039d-163">**Maximální počet souběžných požadavků na procesor**: Zvýšení tohoto nastavení může zmírnit problémová místa výkonu.</span><span class="sxs-lookup"><span data-stu-id="8039d-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="8039d-164">Chcete-li toto nastavení zvýšit, `aspnet.config` přidejte do souboru následující nastavení konfigurace:</span><span class="sxs-lookup"><span data-stu-id="8039d-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="8039d-165">**Limit fronty požadavků**: Pokud celkový počet `maxConcurrentRequestsPerCPU` připojení překročí nastavení, ASP.NET zahájí omezení požadavků pomocí fronty.</span><span class="sxs-lookup"><span data-stu-id="8039d-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="8039d-166">Chcete-li zvětšit velikost fronty, `requestQueueLimit` můžete zvýšit nastavení.</span><span class="sxs-lookup"><span data-stu-id="8039d-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="8039d-167">Chcete-li to provést, přidejte `processModel` následující `config/machine.config` nastavení konfigurace `aspnet.config`do uzlu v (spíše než ):</span><span class="sxs-lookup"><span data-stu-id="8039d-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="8039d-168">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="8039d-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="8039d-169">Tato část popisuje způsoby, jak najít problémová místa výkonu ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8039d-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="8039d-170">Ověření, zda je používán websocket</span><span class="sxs-lookup"><span data-stu-id="8039d-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="8039d-171">Zatímco SignalR můžete použít různé přenosy pro komunikaci mezi klientem a serverem, WebSocket nabízí významnou výhodu výkonu a by měl být použit, pokud klient a server podporují.</span><span class="sxs-lookup"><span data-stu-id="8039d-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="8039d-172">Chcete-li zjistit, zda váš klient a server splňují požadavky pro WebSocket, naleznete v [tématu Přenosy a záložní](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="8039d-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="8039d-173">Chcete-li zjistit, jaký přenos se používá ve vaší aplikaci, můžete použít nástroje pro vývojáře prohlížeče a zkontrolujte protokoly, abyste zjistili, jaký přenos se používá pro připojení.</span><span class="sxs-lookup"><span data-stu-id="8039d-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="8039d-174">Informace o používání nástrojů pro vývoj prohlížeče v aplikacích Internet Explorer a Chrome naleznete v [tématu Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="8039d-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="8039d-175">Použití čítačů výkonu SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-175">Using SignalR performance counters</span></span>

<span data-ttu-id="8039d-176">Tato část popisuje, jak povolit a používat čítače výkonu SignalR, které se nacházejí v `Microsoft.AspNet.SignalR.Utils` balíčku.</span><span class="sxs-lookup"><span data-stu-id="8039d-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="8039d-177">Instalace programu signalr.exe</span><span class="sxs-lookup"><span data-stu-id="8039d-177">Installing signalr.exe</span></span>

<span data-ttu-id="8039d-178">Čítače výkonu lze přidat na server pomocí nástroje s názvem SignalR.exe.</span><span class="sxs-lookup"><span data-stu-id="8039d-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="8039d-179">Chcete-li nainstalovat tento nástroj, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="8039d-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="8039d-180">V sadě Visual Studio vyberte **nástroje, které** > spravuje správce > **balíčků NuGet,\*\*\*\*spravovat balíčky NuGet pro řešení.**</span><span class="sxs-lookup"><span data-stu-id="8039d-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="8039d-181">Vyhledejte **soubor signalr.utils**a vyberte Instalovat.</span><span class="sxs-lookup"><span data-stu-id="8039d-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="8039d-182">Přijměte licenční smlouvu pro instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8039d-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="8039d-183">SignalR.exe bude nainstalován `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`do aplikace .</span><span class="sxs-lookup"><span data-stu-id="8039d-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="8039d-184">Instalace čítačů výkonu pomocí programu SignalR.exe</span><span class="sxs-lookup"><span data-stu-id="8039d-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="8039d-185">Chcete-li nainstalovat čítače výkonu SignalR, spusťte program SignalR.exe na příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="8039d-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="8039d-186">Chcete-li odebrat čítače výkonu SignalR, spusťte nástroj SignalR.exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="8039d-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="8039d-187">Čítače výkonu SignalR</span><span class="sxs-lookup"><span data-stu-id="8039d-187">SignalR Performance counters</span></span>

<span data-ttu-id="8039d-188">Balíček nástroje nainstaluje následující čítače výkonu.</span><span class="sxs-lookup"><span data-stu-id="8039d-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="8039d-189">Čítače "Celkem" měří počet událostí od posledního fondu aplikací nebo restartování serveru.</span><span class="sxs-lookup"><span data-stu-id="8039d-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="8039d-190">**Metriky připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-190">**Connection metrics**</span></span>

<span data-ttu-id="8039d-191">Následující metriky měří události životnosti připojení, ke kterým dochází.</span><span class="sxs-lookup"><span data-stu-id="8039d-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="8039d-192">Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="8039d-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="8039d-193">**Připojená připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-193">**Connections Connected**</span></span>
- <span data-ttu-id="8039d-194">**Znovu připojeno připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="8039d-195">**Odpojená připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="8039d-196">**Aktuální připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-196">**Connections Current**</span></span>

<span data-ttu-id="8039d-197">**Metriky zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-197">**Message metrics**</span></span>

<span data-ttu-id="8039d-198">Následující metriky měří přenos zpráv generovaný SignalR.</span><span class="sxs-lookup"><span data-stu-id="8039d-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="8039d-199">**Celkový počet přijatých zpráv připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="8039d-200">**Celkový počet odeslaných zpráv připojení**</span><span class="sxs-lookup"><span data-stu-id="8039d-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="8039d-201">**Přijaté zprávy o připojení/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="8039d-202">**Odeslané zprávy o připojení/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="8039d-203">**Metriky sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-203">**Message bus metrics**</span></span>

<span data-ttu-id="8039d-204">Následující metriky měří provoz prostřednictvím interní sběrnice zpráv SignalR, fronty, ve které jsou umístěny všechny příchozí a odchozí zprávy SignalR.</span><span class="sxs-lookup"><span data-stu-id="8039d-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="8039d-205">Zpráva je **publikována při** odeslání nebo vysílání.</span><span class="sxs-lookup"><span data-stu-id="8039d-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="8039d-206">Odběratel **Subscriber** v tomto kontextu je odběr na sběrnici zpráv; to by se mělo rovnat počtu klientů plus samotný server.</span><span class="sxs-lookup"><span data-stu-id="8039d-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="8039d-207">**Přidělený pracovník** je součást, která odesílá data aktivním připojením. **zaneprázdněný pracovník** je ten, který aktivně odesílá zprávu.</span><span class="sxs-lookup"><span data-stu-id="8039d-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="8039d-208">**Celkový počet přijatých zpráv sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="8039d-209">**Přijaté zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="8039d-210">**Zprávy sběrnice zpráv publikováno celkem**</span><span class="sxs-lookup"><span data-stu-id="8039d-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="8039d-211">**Publikované zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="8039d-212">**Signální sběrnice odběratelé aktuální**</span><span class="sxs-lookup"><span data-stu-id="8039d-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="8039d-213">**Předplatitelé sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="8039d-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="8039d-214">**Odběratelé sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="8039d-215">**Pracovníci přidělených sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="8039d-216">**Zaneprázdnění pracovníci sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="8039d-217">**Aktuální témata sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="8039d-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="8039d-218">**Metriky chyb**</span><span class="sxs-lookup"><span data-stu-id="8039d-218">**Error metrics**</span></span>

<span data-ttu-id="8039d-219">Následující metriky měří chyby generované přenosy zpráv SignalR.</span><span class="sxs-lookup"><span data-stu-id="8039d-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="8039d-220">K chybám **řešení rozbočovače** dochází, když nelze přeložit metodu rozbočovače nebo rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="8039d-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="8039d-221">**Chyby vyvolání centra** jsou výjimky vyvolání při vyvolání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="8039d-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="8039d-222">**Chyby přenosu** jsou chyby připojení vyvolány během požadavku HTTP nebo odpovědi.</span><span class="sxs-lookup"><span data-stu-id="8039d-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="8039d-223">**Chyby: Všech součet**</span><span class="sxs-lookup"><span data-stu-id="8039d-223">**Errors: All Total**</span></span>
- <span data-ttu-id="8039d-224">**Chyby: Vše/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="8039d-225">**Chyby: Rozlišení centra celkem**</span><span class="sxs-lookup"><span data-stu-id="8039d-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="8039d-226">**Chyby: Rozlišení rozbočovače/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="8039d-227">**Chyby: Vyvolání centra celkem**</span><span class="sxs-lookup"><span data-stu-id="8039d-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="8039d-228">**Chyby: Vyvolání centra/S**</span><span class="sxs-lookup"><span data-stu-id="8039d-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="8039d-229">**Chyby: Přenos celkem**</span><span class="sxs-lookup"><span data-stu-id="8039d-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="8039d-230">**Chyby: Přenos/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="8039d-231">**Metriky horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-231">**Scaleout metrics**</span></span>

<span data-ttu-id="8039d-232">Následující metriky měří provoz a chyby generované poskytovatelem horizontálního navýšení kapacity.</span><span class="sxs-lookup"><span data-stu-id="8039d-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="8039d-233">A **Stream** v tomto kontextu je jednotka škálování používaná zprostředkovatelem horizontálního navýšení kapacity; Toto je tabulka, pokud sql server se používá, téma, pokud service bus se používá a předplatné, pokud redis se používá.</span><span class="sxs-lookup"><span data-stu-id="8039d-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="8039d-234">Každý datový proud zajišťuje operace seřazeného čtení a zápisu. jeden datový proud je potenciální omezení škálování, takže počet datových proudů lze zvýšit, aby se toto kritické místo snížilo.</span><span class="sxs-lookup"><span data-stu-id="8039d-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="8039d-235">Pokud se používá více datových proudů, SignalR bude automaticky distribuovat (střep) zprávy přes tyto datové proudy způsobem, který zajišťuje zprávy odeslané z daného připojení jsou v pořádku.</span><span class="sxs-lookup"><span data-stu-id="8039d-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="8039d-236">Nastavení [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) řídí délku fronty odesílání horizontálního navýšení kapacity udržované signalr.</span><span class="sxs-lookup"><span data-stu-id="8039d-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="8039d-237">Nastavení na hodnotu větší než 0 umístí všechny zprávy do fronty odesílání, které mají být odeslány jeden po druhém na konfigurované zasílání zpráv backplane.</span><span class="sxs-lookup"><span data-stu-id="8039d-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="8039d-238">Pokud velikost fronty přejde nad nakonfigurovanou délku, následná volání k odeslání se nezdaří okamžitě s [InvalidOperationException,](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) dokud počet zpráv ve frontě je menší než nastavení znovu.</span><span class="sxs-lookup"><span data-stu-id="8039d-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="8039d-239">Zařazení do fronty je ve výchozím nastavení zakázáno, protože implementované backplanes mají obvykle vlastní fronty nebo řízení toku na místě.</span><span class="sxs-lookup"><span data-stu-id="8039d-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="8039d-240">V případě SQL Server sdružování připojení účinně omezuje počet odesílá děje v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="8039d-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="8039d-241">Ve výchozím nastavení se pro SQL Server a Redis používá pouze jeden datový proud, pro službu Service Bus se používá pět datových proudů a zařazení do fronty je zakázáno, ale tato nastavení lze změnit prostřednictvím konfigurace na serveru SQL Server a Service Bus:</span><span class="sxs-lookup"><span data-stu-id="8039d-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="8039d-242">**Kód serveru .NET pro konfiguraci počtu tabulek a délky fronty pro rozhraní backplane serveru SQL Server**</span><span class="sxs-lookup"><span data-stu-id="8039d-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="8039d-243">**Kód serveru .NET pro konfiguraci počtu témat a délky fronty pro prostojovací rozhraní Service Bus**</span><span class="sxs-lookup"><span data-stu-id="8039d-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="8039d-244">A **Ukládání do vyrovnávací paměti** datový proud je ten, který vstoupil do chybného stavu; pokud je datový proud v chybovaném stavu, všechny zprávy odeslané do backplane se nezdaří okamžitě, dokud datový proud již není chybovat.</span><span class="sxs-lookup"><span data-stu-id="8039d-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="8039d-245">**Délka fronty odeslat** je počet zpráv, které byly odeslány, ale ještě nebyly odeslány.</span><span class="sxs-lookup"><span data-stu-id="8039d-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="8039d-246">**Přijaté zprávy sběrnice zpráv horizontálního navýšení kapacity/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="8039d-247">**Celkový počet streamů horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="8039d-248">**Otevřít streamy horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="8039d-249">**Ukládání datových proudů horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="8039d-250">**Úplné chyby horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="8039d-251">**Chyby horizontálního navýšení kapacity/s**</span><span class="sxs-lookup"><span data-stu-id="8039d-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="8039d-252">**Délka fronty odeslání horizontálního navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="8039d-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="8039d-253">Další informace o tom, co tyto čítače měří, najdete v [tématu Škálování signalr s Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="8039d-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="8039d-254">Použití jiných čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="8039d-254">Using other performance counters</span></span>

<span data-ttu-id="8039d-255">Následující čítače výkonu může být také užitečné při sledování výkonu vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="8039d-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="8039d-256">**Paměti**</span><span class="sxs-lookup"><span data-stu-id="8039d-256">**Memory**</span></span>

- <span data-ttu-id="8039d-257">.NET CLR\\Paměti # bajty ve všech hromadách (pro w3wp)</span><span class="sxs-lookup"><span data-stu-id="8039d-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="8039d-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="8039d-258">**ASP.NET**</span></span>

- <span data-ttu-id="8039d-259">Technologie ASP.NET\Požadavky aktuální</span><span class="sxs-lookup"><span data-stu-id="8039d-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="8039d-260">Technologie ASP.NET\Zařazena do fronty</span><span class="sxs-lookup"><span data-stu-id="8039d-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="8039d-261">Technologie ASP.NET\Odmítnuto</span><span class="sxs-lookup"><span data-stu-id="8039d-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="8039d-262">**Cpu**</span><span class="sxs-lookup"><span data-stu-id="8039d-262">**CPU**</span></span>

- <span data-ttu-id="8039d-263">Informace o procesoru\Čas procesoru</span><span class="sxs-lookup"><span data-stu-id="8039d-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="8039d-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="8039d-264">**TCP/IP**</span></span>

- <span data-ttu-id="8039d-265">Založena připojení TCPv6/Připojení</span><span class="sxs-lookup"><span data-stu-id="8039d-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="8039d-266">TCPv4/Navázáno připojení</span><span class="sxs-lookup"><span data-stu-id="8039d-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="8039d-267">**Webová služba**</span><span class="sxs-lookup"><span data-stu-id="8039d-267">**Web Service**</span></span>

- <span data-ttu-id="8039d-268">Webová služba\Aktuální připojení</span><span class="sxs-lookup"><span data-stu-id="8039d-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="8039d-269">Webová služba\Maximální počet připojení</span><span class="sxs-lookup"><span data-stu-id="8039d-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="8039d-270">**Dělení na vlákna**</span><span class="sxs-lookup"><span data-stu-id="8039d-270">**Threading**</span></span>

- <span data-ttu-id="8039d-271">Zámky a vlákna\\.NET CLR # aktuálních logických vláken</span><span class="sxs-lookup"><span data-stu-id="8039d-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="8039d-272">Zámky a vlákna\\.NET CLR # aktuálních fyzických vláken</span><span class="sxs-lookup"><span data-stu-id="8039d-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="8039d-273">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="8039d-273">Other Resources</span></span>

<span data-ttu-id="8039d-274">Další informace o ASP.NET sledování výkonu a ladění naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="8039d-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="8039d-275">[ASP.NET přehled výkonu](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="8039d-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="8039d-276">ASP.NET využití vláken ve službě IIS 7.5, IIS 7.0 a IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="8039d-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="8039d-277">&lt;applicationPool&gt; Element (Nastavení webu)</span><span class="sxs-lookup"><span data-stu-id="8039d-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
