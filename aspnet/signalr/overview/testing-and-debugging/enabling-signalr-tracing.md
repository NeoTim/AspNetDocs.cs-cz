---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: Povolování trasování signálů | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak povolit a nakonfigurovat trasování pro servery a klienty signalizace. Trasování umožňuje zobrazit diagnostické informace o událostech...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578832"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="864e4-104">Povolení trasování knihovnou SignalR</span><span class="sxs-lookup"><span data-stu-id="864e4-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="864e4-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="864e4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="864e4-106">Tento dokument popisuje, jak povolit a nakonfigurovat trasování pro servery a klienty signalizace.</span><span class="sxs-lookup"><span data-stu-id="864e4-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="864e4-107">Trasování umožňuje zobrazit diagnostické informace o událostech v aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="864e4-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="864e4-108">Toto téma bylo původně napsáno nadFletcherm.</span><span class="sxs-lookup"><span data-stu-id="864e4-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="864e4-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="864e4-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="864e4-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="864e4-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="864e4-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="864e4-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="864e4-112">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="864e4-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="864e4-113">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="864e4-113">Questions and comments</span></span>
>
> <span data-ttu-id="864e4-114">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="864e4-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="864e4-115">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="864e4-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="864e4-116">Pokud je povoleno trasování, aplikace signalizace vytvoří položky protokolu pro události.</span><span class="sxs-lookup"><span data-stu-id="864e4-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="864e4-117">Události můžete protokolovat z klienta i serveru.</span><span class="sxs-lookup"><span data-stu-id="864e4-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="864e4-118">Trasování v protokolu serveru protokoluje připojení, poskytovatele škálování a události sběrnice zpráv.</span><span class="sxs-lookup"><span data-stu-id="864e4-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="864e4-119">Trasování v klientském počítači protokoluje události připojení.</span><span class="sxs-lookup"><span data-stu-id="864e4-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="864e4-120">V nástroji Signal 2,1 a později trasování klienta protokoluje úplný obsah zpráv o voláních centra.</span><span class="sxs-lookup"><span data-stu-id="864e4-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="864e4-121">Obsah</span><span class="sxs-lookup"><span data-stu-id="864e4-121">Contents</span></span>

- [<span data-ttu-id="864e4-122">Povolení trasování na serveru</span><span class="sxs-lookup"><span data-stu-id="864e4-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="864e4-123">Protokolování událostí serveru do textových souborů</span><span class="sxs-lookup"><span data-stu-id="864e4-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="864e4-124">Protokolování událostí serveru do protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="864e4-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="864e4-125">Povolení trasování v klientu .NET (desktopové aplikace pro Windows)</span><span class="sxs-lookup"><span data-stu-id="864e4-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="864e4-126">Protokolování událostí klienta plochy do konzoly</span><span class="sxs-lookup"><span data-stu-id="864e4-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="864e4-127">Protokolování událostí klienta plochy do textového souboru</span><span class="sxs-lookup"><span data-stu-id="864e4-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="864e4-128">Povolení trasování v klientech Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="864e4-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="864e4-129">Protokolování událostí klienta Windows Phone do uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="864e4-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="864e4-130">Protokolování událostí klienta Windows Phone do konzoly ladění</span><span class="sxs-lookup"><span data-stu-id="864e4-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="864e4-131">Povolení trasování v klientovi JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="864e4-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="864e4-132">Povolení trasování na serveru</span><span class="sxs-lookup"><span data-stu-id="864e4-132">Enabling tracing on the server</span></span>

<span data-ttu-id="864e4-133">V závislosti na typu projektu povolíte trasování na serveru v konfiguračním souboru aplikace (soubor App. config nebo Web. config). Určíte, které kategorie událostí chcete protokolovat.</span><span class="sxs-lookup"><span data-stu-id="864e4-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="864e4-134">V konfiguračním souboru můžete také určit, zda chcete protokolovat události do textového souboru, do protokolu událostí systému Windows nebo do vlastního protokolu pomocí implementace [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="864e4-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="864e4-135">Kategorie událostí serveru obsahují následující řazení zpráv:</span><span class="sxs-lookup"><span data-stu-id="864e4-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="864e4-136">Zdroj</span><span class="sxs-lookup"><span data-stu-id="864e4-136">Source</span></span> | <span data-ttu-id="864e4-137">Zprávy</span><span class="sxs-lookup"><span data-stu-id="864e4-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="864e4-138">Signál. SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="864e4-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="864e4-139">Nastavení poskytovatele škálování sběrnice zpráv SQL, operace databáze, chyba a události časového limitu</span><span class="sxs-lookup"><span data-stu-id="864e4-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="864e4-140">Signál. ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="864e4-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="864e4-141">Vytváření a předplatné, chyby a události zasílání zpráv v tématu zprostředkovatel škálování služby Service Bus</span><span class="sxs-lookup"><span data-stu-id="864e4-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="864e4-142">Signál. RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="864e4-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="864e4-143">Připojení, odpojení a chybové události poskytovatele škálování Redis</span><span class="sxs-lookup"><span data-stu-id="864e4-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="864e4-144">Signál. ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="864e4-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="864e4-145">Události zasílání zpráv ve škálování</span><span class="sxs-lookup"><span data-stu-id="864e4-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="864e4-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="864e4-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="864e4-147">Přenosové připojení protokolu WebSocket, odpojení, zasílání zpráv a chybové události</span><span class="sxs-lookup"><span data-stu-id="864e4-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="864e4-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="864e4-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="864e4-149">ServerSentEvents přenosu, odpojení, zasílání zpráv a chybové události</span><span class="sxs-lookup"><span data-stu-id="864e4-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="864e4-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="864e4-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="864e4-151">ForeverFrame přenosu, odpojení, zasílání zpráv a chybové události</span><span class="sxs-lookup"><span data-stu-id="864e4-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="864e4-152">Signalizace. Transports. LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="864e4-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="864e4-153">LongPolling přenosu, odpojení, zasílání zpráv a chybové události</span><span class="sxs-lookup"><span data-stu-id="864e4-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="864e4-154">Signalizace. Transports. TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="864e4-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="864e4-155">Přenosové připojení, odpojení a události udržení naživu</span><span class="sxs-lookup"><span data-stu-id="864e4-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="864e4-156">Signál. ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="864e4-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="864e4-157">Události zjišťování centra</span><span class="sxs-lookup"><span data-stu-id="864e4-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="864e4-158">Protokolování událostí serveru do textových souborů</span><span class="sxs-lookup"><span data-stu-id="864e4-158">Logging server events to text files</span></span>

<span data-ttu-id="864e4-159">Následující kód ukazuje, jak povolit trasování pro každou kategorii události.</span><span class="sxs-lookup"><span data-stu-id="864e4-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="864e4-160">Tato ukázka nakonfiguruje aplikaci tak, aby protokoloval události do textových souborů.</span><span class="sxs-lookup"><span data-stu-id="864e4-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="864e4-161">**Kód serveru XML pro povolení trasování**</span><span class="sxs-lookup"><span data-stu-id="864e4-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="864e4-162">V kódu výše položka `SignalRSwitch` určuje parametr [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) , který se používá pro události odeslané do určeného protokolu.</span><span class="sxs-lookup"><span data-stu-id="864e4-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="864e4-163">V tomto případě je nastavená na `Verbose` to znamená, že se zaznamenávají všechny zprávy ladění a trasování.</span><span class="sxs-lookup"><span data-stu-id="864e4-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="864e4-164">Následující výstup zobrazuje položky ze souboru `transports.log.txt` pro aplikaci pomocí výše uvedeného konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="864e4-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="864e4-165">Zobrazuje nové připojení, odebrané připojení a události prezenčního signálu přenosu.</span><span class="sxs-lookup"><span data-stu-id="864e4-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="864e4-166">Protokolování událostí serveru do protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="864e4-166">Logging server events to the event log</span></span>

<span data-ttu-id="864e4-167">Chcete-li protokolovat události do protokolu událostí místo textového souboru, změňte hodnoty položek v uzlu `sharedListeners`.</span><span class="sxs-lookup"><span data-stu-id="864e4-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="864e4-168">Následující kód ukazuje, jak protokolovat události serveru do protokolu událostí:</span><span class="sxs-lookup"><span data-stu-id="864e4-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="864e4-169">**Kód serveru XML pro protokolování událostí do protokolu událostí**</span><span class="sxs-lookup"><span data-stu-id="864e4-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="864e4-170">Události jsou protokolovány v aplikačním protokolu a jsou k dispozici prostřednictvím Prohlížeč událostí, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="864e4-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![Prohlížeč událostí zobrazení protokolů signálu](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="864e4-172">Pokud používáte protokol událostí, nastavte hodnotu **TraceLevel** na **chybu** , aby se zachoval počet zpráv, které lze spravovat.</span><span class="sxs-lookup"><span data-stu-id="864e4-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="864e4-173">Povolení trasování v klientu .NET (desktopové aplikace pro Windows)</span><span class="sxs-lookup"><span data-stu-id="864e4-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="864e4-174">Klient rozhraní .NET může protokolovat události do konzoly, textového souboru nebo do vlastního protokolu pomocí implementace [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span><span class="sxs-lookup"><span data-stu-id="864e4-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="864e4-175">Chcete-li povolit protokolování v klientovi .NET, nastavte vlastnost `TraceLevel` připojení na hodnotu [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) a vlastnost `TraceWriter` na platnou instanci [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) .</span><span class="sxs-lookup"><span data-stu-id="864e4-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="864e4-176">Protokolování událostí klienta plochy do konzoly</span><span class="sxs-lookup"><span data-stu-id="864e4-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="864e4-177">Následující C# kód ukazuje, jak protokolovat události v klientovi .NET do konzoly nástroje:</span><span class="sxs-lookup"><span data-stu-id="864e4-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="864e4-178">Protokolování událostí klienta plochy do textového souboru</span><span class="sxs-lookup"><span data-stu-id="864e4-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="864e4-179">Následující C# kód ukazuje, jak protokolovat události v klientovi .NET do textového souboru:</span><span class="sxs-lookup"><span data-stu-id="864e4-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="864e4-180">Následující výstup zobrazuje položky ze souboru `ClientLog.txt` pro aplikaci pomocí výše uvedeného konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="864e4-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="864e4-181">Zobrazuje se klient, který se připojuje k serveru, a centrum vyvolá metodu klienta nazvanou `addMessage`:</span><span class="sxs-lookup"><span data-stu-id="864e4-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="864e4-182">Povolení trasování v klientech Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="864e4-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="864e4-183">Aplikace Signal pro aplikace Windows Phone používají stejný klient .NET jako desktopové aplikace, ale [Konzola. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) a zápis do souboru pomocí [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="864e4-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="864e4-184">Místo toho je nutné vytvořit vlastní implementaci objektu [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) pro trasování.</span><span class="sxs-lookup"><span data-stu-id="864e4-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="864e4-185">Protokolování událostí klienta Windows Phone do uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="864e4-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="864e4-186">[Základ signálu](https://github.com/SignalR/SignalR/archive/master.zip) obsahuje vzorový Windows Phone, který zapisuje výstup trasování do [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) pomocí vlastní implementace [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) s názvem `TextBlockWriter`.</span><span class="sxs-lookup"><span data-stu-id="864e4-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="864e4-187">Tuto třídu lze najít v projektu **Samples/Microsoft. ASPNET. signaler. Client. WP8. Samples** .</span><span class="sxs-lookup"><span data-stu-id="864e4-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="864e4-188">Při vytváření instance `TextBlockWriter`předejte aktuální [Třída SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , kde vytvoří [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) pro použití pro výstup trasování:</span><span class="sxs-lookup"><span data-stu-id="864e4-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="864e4-189">Výstup trasování se pak zapíše do nového [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) vytvořeného v [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , které jste předali:</span><span class="sxs-lookup"><span data-stu-id="864e4-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="864e4-190">Protokolování událostí klienta Windows Phone do konzoly ladění</span><span class="sxs-lookup"><span data-stu-id="864e4-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="864e4-191">Chcete-li odeslat výstup do konzoly ladění namísto uživatelského rozhraní, vytvořte implementaci objektu [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , který zapisuje do okna ladění a přiřaďte ho k vlastnosti [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) vašeho připojení:</span><span class="sxs-lookup"><span data-stu-id="864e4-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="864e4-192">Informace o trasování budou následně zapsány do okna ladění v aplikaci Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="864e4-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="864e4-193">Povolení trasování v klientovi JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="864e4-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="864e4-194">Chcete-li povolit protokolování na straně klienta pro připojení, nastavte vlastnost `logging` objektu Connection před voláním metody `start` k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="864e4-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="864e4-195">**JavaScriptový kód klienta pro povolení trasování do konzoly prohlížeče (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="864e4-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="864e4-196">**JavaScriptový kód klienta pro povolení trasování do konzoly prohlížeče (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="864e4-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="864e4-197">Když je trasování povoleno, klient jazyka JavaScript protokoluje události do konzoly prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="864e4-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="864e4-198">Přístup ke konzole prohlížeče najdete v tématu [monitorování přenosů](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span><span class="sxs-lookup"><span data-stu-id="864e4-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="864e4-199">Na následujícím snímku obrazovky vidíte klienta jazyka JavaScript s povoleným trasováním.</span><span class="sxs-lookup"><span data-stu-id="864e4-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="864e4-200">Zobrazuje události připojení a volání centra v konzole prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="864e4-200">It shows connection and hub invocation events in the browser console:</span></span>

![Události trasování signálu v konzole prohlížeče](enabling-signalr-tracing/_static/image4.png)
