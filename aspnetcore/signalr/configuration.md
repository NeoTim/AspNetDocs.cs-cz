---
title: Konfigurace jádra SignalR technologie ASP.NET
author: bradygaster
description: Zjistěte, jak nakonfigurovat aplikace SignalR technologie ASP.NET Core.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 02/07/2019
uid: signalr/configuration
ms.openlocfilehash: f5449a15743c1f38c550fe30945bdc19f069e3f5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070081"
---
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="e234f-103">Konfigurace jádra SignalR technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e234f-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="e234f-104">Serializace JSON/MessagePack možnosti</span><span class="sxs-lookup"><span data-stu-id="e234f-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="e234f-105">Funkce SignalR technologie ASP.NET Core podporuje dva protokoly pro kódování zprávy: [JSON](https://www.json.org/) a [MessagePack](https://msgpack.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="e234f-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="e234f-106">Všechny protokoly, které obsahuje možnosti konfigurace serializace.</span><span class="sxs-lookup"><span data-stu-id="e234f-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="e234f-107">Serializace JSON lze nastavit na serveru pomocí [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) metody rozšíření, které mohou být přidány po [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) v vaše `Startup.ConfigureServices` metody.</span><span class="sxs-lookup"><span data-stu-id="e234f-107">JSON serialization can be configured on the server using the [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="e234f-108">`AddJsonProtocol` Metoda přijímá delegát, který přijímá `options` objektu.</span><span class="sxs-lookup"><span data-stu-id="e234f-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="e234f-109">[PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) vlastnost k tomuto objektu je JSON.NET `JsonSerializerSettings` objekt, který můžete použít ke konfiguraci serializace argumenty a návratové hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e234f-109">The [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="e234f-110">Najdete v článku [JSON.NET dokumentaci](https://www.newtonsoft.com/json/help/html/Introduction.htm) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="e234f-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="e234f-111">Jako příklad konfigurace serializátoru, který chcete použít místo výchozí názvy "camelCase", "PascalCase" názvy vlastností, pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="e234f-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="e234f-112">V klientovi .NET, stejné `AddJsonProtocol` – metoda rozšíření existuje v [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span><span class="sxs-lookup"><span data-stu-id="e234f-112">In the .NET client, the same `AddJsonProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="e234f-113">`Microsoft.Extensions.DependencyInjection` Obor názvů musí být importován do resolve – metoda rozšíření:</span><span class="sxs-lookup"><span data-stu-id="e234f-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
            new DefaultContractResolver();
    })
    .Build();
```

> [!NOTE]
> <span data-ttu-id="e234f-114">Není možné konfigurovat pomocí serializace JSON klienta jazyka JavaScript v tuto chvíli.</span><span class="sxs-lookup"><span data-stu-id="e234f-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="e234f-115">MessagePack možnosti serializace</span><span class="sxs-lookup"><span data-stu-id="e234f-115">MessagePack serialization options</span></span>

<span data-ttu-id="e234f-116">Poskytnutím delegáta, kterého lze nakonfigurovat MessagePack serializace [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) volání.</span><span class="sxs-lookup"><span data-stu-id="e234f-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="e234f-117">Zobrazit [MessagePack v knihovně SignalR](xref:signalr/messagepackhubprotocol) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="e234f-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="e234f-118">Není možné konfigurovat MessagePack serializace pomocí jazyka JavaScript klienta v tuto chvíli.</span><span class="sxs-lookup"><span data-stu-id="e234f-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="e234f-119">Konfigurovat možnosti serveru</span><span class="sxs-lookup"><span data-stu-id="e234f-119">Configure server options</span></span>

<span data-ttu-id="e234f-120">Následující tabulka popisuje možnosti pro konfiguraci rozbočovače SignalR:</span><span class="sxs-lookup"><span data-stu-id="e234f-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="e234f-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-121">Option</span></span> | <span data-ttu-id="e234f-122">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-122">Default Value</span></span> | <span data-ttu-id="e234f-123">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-123">Description</span></span> |
| ------ | ------------- | ----------- |
| `ClientTimeoutInterval` | <span data-ttu-id="e234f-124">30 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-124">30 seconds</span></span> | <span data-ttu-id="e234f-125">Server bude předpokládat, že klient odpojen Pokud neobdržel zprávu (včetně udržování) v tomto intervalu.</span><span class="sxs-lookup"><span data-stu-id="e234f-125">The server will consider the client disconnected if it hasn't received a message (including keep-alive) in this interval.</span></span> <span data-ttu-id="e234f-126">Může to trvat déle než tento interval časového limitu klienta ve skutečnosti označit odpojené kvůli jak tato možnost je implementovaná.</span><span class="sxs-lookup"><span data-stu-id="e234f-126">It could take longer than this timeout interval for the client to actually be marked disconnected, due to how this is implemented.</span></span> <span data-ttu-id="e234f-127">Doporučená hodnota je double `KeepAliveInterval` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e234f-127">The recommended value is double the `KeepAliveInterval` value.</span></span>|
| `HandshakeTimeout` | <span data-ttu-id="e234f-128">15 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-128">15 seconds</span></span> | <span data-ttu-id="e234f-129">Pokud klient nebude odeslat zprávu handshake počáteční v tomto časovém intervalu, je připojení ukončeno.</span><span class="sxs-lookup"><span data-stu-id="e234f-129">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> <span data-ttu-id="e234f-130">Toto je upřesňující nastavení, by měla být změněna pouze v případě chyby časového limitu handshake dochází z důvodu závažné sítích s latencí.</span><span class="sxs-lookup"><span data-stu-id="e234f-130">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="e234f-131">Další podrobnosti o procesu najdete v článku [specifikace protokolu rozbočovače SignalR](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="e234f-131">For more detail on the handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="e234f-132">15 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-132">15 seconds</span></span> | <span data-ttu-id="e234f-133">Pokud server není v rámci tohoto intervalu odeslal zprávu, je automaticky odeslána zpráva příkazu ping na udržení připojení otevřeného.</span><span class="sxs-lookup"><span data-stu-id="e234f-133">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> <span data-ttu-id="e234f-134">Při změně `KeepAliveInterval`, změnit `ServerTimeout` / `serverTimeoutInMilliseconds` nastavení na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="e234f-134">When changing `KeepAliveInterval`, change the `ServerTimeout`/`serverTimeoutInMilliseconds` setting on the client.</span></span> <span data-ttu-id="e234f-135">Doporučené `ServerTimeout` / `serverTimeoutInMilliseconds` hodnotu double `KeepAliveInterval` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e234f-135">The recommended `ServerTimeout`/`serverTimeoutInMilliseconds` value is double the `KeepAliveInterval` value.</span></span>  |
| `SupportedProtocols` | <span data-ttu-id="e234f-136">Všechny nainstalované protokoly</span><span class="sxs-lookup"><span data-stu-id="e234f-136">All installed protocols</span></span> | <span data-ttu-id="e234f-137">Protokolů podporovaných toto centrum.</span><span class="sxs-lookup"><span data-stu-id="e234f-137">Protocols supported by this hub.</span></span> <span data-ttu-id="e234f-138">Ve výchozím nastavení jsou povolené všechny protokoly, které jsou registrované na serveru, ale protokolů lze odebrat z tohoto seznamu zakázat konkrétní protokoly pro jednotlivé rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="e234f-138">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | `false` | <span data-ttu-id="e234f-139">Pokud `true`, podrobné zprávy o výjimkách se vrátí ke klientům, když dojde k výjimce v metodě rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="e234f-139">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="e234f-140">Výchozí hodnota je `false`, jak tyto zprávy o výjimkách mohou obsahovat citlivé údaje.</span><span class="sxs-lookup"><span data-stu-id="e234f-140">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="e234f-141">Možnosti je možné nakonfigurovat pro všechna centra poskytnutím delegáta možnosti k `AddSignalR` volání v `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="e234f-141">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    });
}
```

<span data-ttu-id="e234f-142">Možnosti pro jedno centrum přepsat globální možnosti uvedené v `AddSignalR` a dá se nakonfigurovat pomocí [AddHubOptions\<T >](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="e234f-142">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
});
```

### <a name="advanced-http-configuration-options"></a><span data-ttu-id="e234f-143">Rozšířené možnosti konfigurace protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="e234f-143">Advanced HTTP configuration options</span></span>

<span data-ttu-id="e234f-144">Použití `HttpConnectionDispatcherOptions` konfigurace upřesňujících nastavení související s přenosy a správa vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="e234f-144">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="e234f-145">Tyto možnosti jsou nakonfigurované pomocí předání delegáta, kterého [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) v `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="e234f-145">These options are configured by passing a delegate to [MapHub\<T>](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) in `Startup.Configure`.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseSignalR((configure) => 
    {
        var desiredTransports = 
            HttpTransportType.WebSockets |
            HttpTransportType.LongPolling;

        configure.MapHub<MyHub>("/myhub", (options) => 
        {
            options.Transports = desiredTransports;
        });
    });
}
```

<span data-ttu-id="e234f-146">Následující tabulka popisuje možnosti pro konfiguraci rozšířené možnosti HTTP SignalR technologie ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="e234f-146">The following table describes options for configuring ASP.NET Core SignalR's advanced HTTP options:</span></span>

| <span data-ttu-id="e234f-147">Možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-147">Option</span></span> | <span data-ttu-id="e234f-148">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-148">Default Value</span></span> | <span data-ttu-id="e234f-149">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-149">Description</span></span> |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="e234f-150">32 KB.</span><span class="sxs-lookup"><span data-stu-id="e234f-150">32 KB</span></span> | <span data-ttu-id="e234f-151">Maximální počet bajtů přijatých z klienta, který vyrovnávací paměti serveru.</span><span class="sxs-lookup"><span data-stu-id="e234f-151">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="e234f-152">Zvýšení hodnoty tuto umožňuje serveru pro příjem větší zprávy, ale může mít negativní vliv na využití paměti.</span><span class="sxs-lookup"><span data-stu-id="e234f-152">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> |
| `AuthorizationData` | <span data-ttu-id="e234f-153">Data jsou automaticky shromážděna z `Authorize` atributy použité u třídy rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="e234f-153">Data automatically gathered from the `Authorize` attributes applied to the Hub class.</span></span> | <span data-ttu-id="e234f-154">Seznam [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objekty sloužící k určení, pokud je klient autorizaci k připojení k rozbočovači.</span><span class="sxs-lookup"><span data-stu-id="e234f-154">A list of [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="e234f-155">32 KB.</span><span class="sxs-lookup"><span data-stu-id="e234f-155">32 KB</span></span> | <span data-ttu-id="e234f-156">Maximální počet bajtů odeslaných aplikace, která vyrovnávací paměti serveru.</span><span class="sxs-lookup"><span data-stu-id="e234f-156">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="e234f-157">Zvýšení hodnoty tuto umožňuje serveru odesílat větší zprávy, ale může mít negativní vliv na využití paměti.</span><span class="sxs-lookup"><span data-stu-id="e234f-157">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> |
| `Transports` | <span data-ttu-id="e234f-158">Všechny přenosy jsou povolené.</span><span class="sxs-lookup"><span data-stu-id="e234f-158">All Transports are enabled.</span></span> | <span data-ttu-id="e234f-159">Bitová maska z `HttpTransportType` hodnoty, které můžete omezit přenosy klienta můžete použít pro připojení.</span><span class="sxs-lookup"><span data-stu-id="e234f-159">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> |
| `LongPolling` | <span data-ttu-id="e234f-160">Níže jsou uvedeny.</span><span class="sxs-lookup"><span data-stu-id="e234f-160">See below.</span></span> | <span data-ttu-id="e234f-161">Další možnosti specifické pro dlouhé dotazování přenosu.</span><span class="sxs-lookup"><span data-stu-id="e234f-161">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="e234f-162">Níže jsou uvedeny.</span><span class="sxs-lookup"><span data-stu-id="e234f-162">See below.</span></span> | <span data-ttu-id="e234f-163">Další možnosti specifické pro přenos objekty Websocket.</span><span class="sxs-lookup"><span data-stu-id="e234f-163">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="e234f-164">Dlouhý interval dotazování přenosu má další možnosti, které lze konfigurovat pomocí `LongPolling` vlastnost:</span><span class="sxs-lookup"><span data-stu-id="e234f-164">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="e234f-165">Možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-165">Option</span></span> | <span data-ttu-id="e234f-166">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-166">Default Value</span></span> | <span data-ttu-id="e234f-167">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-167">Description</span></span> |
| ------ | ------------- | ----------- |
| `PollTimeout` | <span data-ttu-id="e234f-168">90 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-168">90 seconds</span></span> | <span data-ttu-id="e234f-169">Maximální množství času na server čeká na zprávu k odeslání do klienta před ukončením žádosti o jednotné hlasování.</span><span class="sxs-lookup"><span data-stu-id="e234f-169">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="e234f-170">Snížení hodnoty způsobí, že klient k vydávání nových žádostí o dotazování častěji.</span><span class="sxs-lookup"><span data-stu-id="e234f-170">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> |

<span data-ttu-id="e234f-171">Přenos pomocí protokolu WebSocket má další možnosti, které lze konfigurovat pomocí `WebSockets` vlastnost:</span><span class="sxs-lookup"><span data-stu-id="e234f-171">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="e234f-172">Možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-172">Option</span></span> | <span data-ttu-id="e234f-173">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-173">Default Value</span></span> | <span data-ttu-id="e234f-174">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-174">Description</span></span> |
| ------ | ------------- | ----------- |
| `CloseTimeout` | <span data-ttu-id="e234f-175">5 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-175">5 seconds</span></span> | <span data-ttu-id="e234f-176">Po zavření serveru, pokud se klientovi nepodaří zavřete v tomto časovém intervalu, připojení se ukončí.</span><span class="sxs-lookup"><span data-stu-id="e234f-176">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | `null` | <span data-ttu-id="e234f-177">Delegát, který je možné nastavit `Sec-WebSocket-Protocol` vlastní hodnoty záhlaví.</span><span class="sxs-lookup"><span data-stu-id="e234f-177">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="e234f-178">Delegát přijme hodnoty vyžádané klientem jako vstup a měl by vrátit na požadovanou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e234f-178">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="e234f-179">Konfigurovat možnosti klienta</span><span class="sxs-lookup"><span data-stu-id="e234f-179">Configure client options</span></span>

<span data-ttu-id="e234f-180">Možnosti klienta lze nakonfigurovat podle `HubConnectionBuilder` typ (k dispozici v rozhraní .NET a JavaScript klientech), stejně jako na `HubConnection` samotný.</span><span class="sxs-lookup"><span data-stu-id="e234f-180">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="e234f-181">Konfigurace protokolování</span><span class="sxs-lookup"><span data-stu-id="e234f-181">Configure logging</span></span>

<span data-ttu-id="e234f-182">Protokolování je nakonfigurován v klientu .NET pomocí `ConfigureLogging` metody.</span><span class="sxs-lookup"><span data-stu-id="e234f-182">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="e234f-183">Protokolování poskytovatelů a filtry můžete zaregistrovat stejně, jako jsou na serveru.</span><span class="sxs-lookup"><span data-stu-id="e234f-183">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="e234f-184">Zobrazit [protokolování v ASP.NET Core](xref:fundamentals/logging/index) Další informace naleznete v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="e234f-184">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="e234f-185">Aby bylo možné zaregistrovat poskytovatele protokolování, je nutné nainstalovat potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="e234f-185">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="e234f-186">Najdete v článku [vestavěné protokolování poskytovatelé](xref:fundamentals/logging/index#built-in-logging-providers) část dokumentace pro úplný seznam.</span><span class="sxs-lookup"><span data-stu-id="e234f-186">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="e234f-187">Například pokud chcete povolit protokolování konzoly, nainstalujte `Microsoft.Extensions.Logging.Console` balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="e234f-187">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="e234f-188">Volání `AddConsole` – metoda rozšíření:</span><span class="sxs-lookup"><span data-stu-id="e234f-188">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="e234f-189">V klientovi JavaScript podobný `configureLogging` metody existuje.</span><span class="sxs-lookup"><span data-stu-id="e234f-189">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="e234f-190">Zadejte `LogLevel` hodnotu, která minimální úroveň zprávy protokolu k vytvoření.</span><span class="sxs-lookup"><span data-stu-id="e234f-190">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="e234f-191">Protokoly se zapisují do okna konzoly prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="e234f-191">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="e234f-192">Chcete-li zakázat protokolování úplně, zadejte `signalR.LogLevel.None` v `configureLogging` metody.</span><span class="sxs-lookup"><span data-stu-id="e234f-192">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="e234f-193">K dispozici ke klientovi JavaScript úrovně protokolu jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="e234f-193">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="e234f-194">Protokolování zpráv při nastavení na úrovni protokolu na jednu z těchto hodnot umožňuje **nebo vyšší** dané úrovni.</span><span class="sxs-lookup"><span data-stu-id="e234f-194">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="e234f-195">úroveň</span><span class="sxs-lookup"><span data-stu-id="e234f-195">Level</span></span> | <span data-ttu-id="e234f-196">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-196">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="e234f-197">Jsou zaznamenány žádné zprávy.</span><span class="sxs-lookup"><span data-stu-id="e234f-197">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="e234f-198">Zprávy, které indikují chybu celé aplikace.</span><span class="sxs-lookup"><span data-stu-id="e234f-198">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="e234f-199">Zprávy, které indikují chybu aktuální operaci.</span><span class="sxs-lookup"><span data-stu-id="e234f-199">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="e234f-200">Zprávy, které označují méně závažné potíže.</span><span class="sxs-lookup"><span data-stu-id="e234f-200">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="e234f-201">Informační zprávy.</span><span class="sxs-lookup"><span data-stu-id="e234f-201">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="e234f-202">Diagnostické zprávy je užitečné pro ladění.</span><span class="sxs-lookup"><span data-stu-id="e234f-202">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="e234f-203">Velmi podrobné diagnostické zprávy, které jsou navržené pro diagnostiku specifické problémy.</span><span class="sxs-lookup"><span data-stu-id="e234f-203">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="e234f-204">Nakonfigurovat povolené přenosy</span><span class="sxs-lookup"><span data-stu-id="e234f-204">Configure allowed transports</span></span>

<span data-ttu-id="e234f-205">Přenosy systém signalr se dá nakonfigurovat v `WithUrl` volání (`withUrl` v JavaScriptu).</span><span class="sxs-lookup"><span data-stu-id="e234f-205">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="e234f-206">Bitový OR hodnoty `HttpTransportType` slouží k omezení klienta používat pouze zadaný přenosy.</span><span class="sxs-lookup"><span data-stu-id="e234f-206">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="e234f-207">Ve výchozím nastavení jsou povolené všechny přenosy.</span><span class="sxs-lookup"><span data-stu-id="e234f-207">All transports are enabled by default.</span></span>

<span data-ttu-id="e234f-208">Například zakázat přenos Server-Sent události, ale povolte připojení objekty Websocket a dlouhý interval dotazování:</span><span class="sxs-lookup"><span data-stu-id="e234f-208">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="e234f-209">V klientovi JavaScript přenosy jsou nakonfigurovány tak, že nastavíte `transport` na objekt možnosti poskytnuté `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="e234f-209">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="e234f-210">Konfigurace ověřování nosiče</span><span class="sxs-lookup"><span data-stu-id="e234f-210">Configure bearer authentication</span></span>

<span data-ttu-id="e234f-211">Pokud chcete poskytnout ověřovací data spolu s knihovnou SignalR požadavky, použijte `AccessTokenProvider` možnost (`accessTokenFactory` v JavaScriptu) k určení funkce, která vrací požadovaný přístupový token.</span><span class="sxs-lookup"><span data-stu-id="e234f-211">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="e234f-212">V klientovi .NET Tento přístupový token předaný jako HTTP "Ověřování nosiče" token (použití `Authorization` záhlaví s typem `Bearer`).</span><span class="sxs-lookup"><span data-stu-id="e234f-212">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="e234f-213">V klientovi JavaScript přístupový token se používá jako nosný token **s výjimkou** v několika případech, kdy prohlížeč rozhraní API omezit schopnosti uplatňovat hlavičky (konkrétně v Server-Sent události a protokoly Websocket požadavky).</span><span class="sxs-lookup"><span data-stu-id="e234f-213">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="e234f-214">V těchto případech je přístupový token k dispozici jako hodnotu řetězce dotazu `access_token`.</span><span class="sxs-lookup"><span data-stu-id="e234f-214">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="e234f-215">V klientovi .NET `AccessTokenProvider` možnost lze zadat pomocí možnosti delegáta v `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="e234f-215">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        };
    })
    .Build();
```

<span data-ttu-id="e234f-216">V klientovi JavaScript přístupový token je nakonfigurovaný tak, že nastavíte `accessTokenFactory` na objekt možnosti v `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="e234f-216">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="e234f-217">Konfigurace časového limitu a udržování možnosti</span><span class="sxs-lookup"><span data-stu-id="e234f-217">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="e234f-218">Další možnosti pro konfiguraci časového limitu a zachování chování, které jsou k dispozici na `HubConnection` samotného objektu:</span><span class="sxs-lookup"><span data-stu-id="e234f-218">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="e234f-219">.NET – možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-219">.NET Option</span></span> | <span data-ttu-id="e234f-220">Možnost jazyka JavaScript</span><span class="sxs-lookup"><span data-stu-id="e234f-220">JavaScript Option</span></span> | <span data-ttu-id="e234f-221">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-221">Default Value</span></span> | <span data-ttu-id="e234f-222">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-222">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="e234f-223">30 sekund (30 000 milisekund)</span><span class="sxs-lookup"><span data-stu-id="e234f-223">30 seconds (30,000 milliseconds)</span></span> | <span data-ttu-id="e234f-224">Časový limit pro aktivity serveru.</span><span class="sxs-lookup"><span data-stu-id="e234f-224">Timeout for server activity.</span></span> <span data-ttu-id="e234f-225">Pokud server není v tomto intervalu odeslal zprávu, klient bude považovat za server odpojen a aktivační události `Closed` událostí (`onclose` v JavaScriptu).</span><span class="sxs-lookup"><span data-stu-id="e234f-225">If the server hasn't sent a message in this interval, the client considers the server disconnected and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="e234f-226">Tato hodnota musí být dostatečně velký pro zprávu ping na odeslaných ze serveru **a** klient obdrží během intervalu časového limitu.</span><span class="sxs-lookup"><span data-stu-id="e234f-226">This value must be large enough for a ping message to be sent from the server **and** received by the client within the timeout interval.</span></span> <span data-ttu-id="e234f-227">Doporučená hodnota je čísla alespoň double server `KeepAliveInterval` hodnotu, abyste měli čas pro příkazy ping pro zjištění dorazí.</span><span class="sxs-lookup"><span data-stu-id="e234f-227">The recommended value is a number at least double the server's `KeepAliveInterval` value, to allow time for pings to arrive.</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="e234f-228">Nejde konfigurovat</span><span class="sxs-lookup"><span data-stu-id="e234f-228">Not configurable</span></span> | <span data-ttu-id="e234f-229">15 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-229">15 seconds</span></span> | <span data-ttu-id="e234f-230">Časový limit pro počáteční server handshake.</span><span class="sxs-lookup"><span data-stu-id="e234f-230">Timeout for initial server handshake.</span></span> <span data-ttu-id="e234f-231">Pokud server není v tomto intervalu odeslání odpovědi handshake, klient zruší handshake a aktivační události `Closed` událostí (`onclose` v JavaScriptu).</span><span class="sxs-lookup"><span data-stu-id="e234f-231">If the server doesn't send a handshake response in this interval, the client cancels the handshake and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="e234f-232">Toto je upřesňující nastavení, by měla být změněna pouze v případě chyby časového limitu handshake dochází z důvodu závažné sítích s latencí.</span><span class="sxs-lookup"><span data-stu-id="e234f-232">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="e234f-233">Další podrobnosti o procesu najdete v článku [specifikace protokolu rozbočovače SignalR](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="e234f-233">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |

<span data-ttu-id="e234f-234">V klientovi .NET jsou zadané hodnoty časového limitu jako `TimeSpan` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e234f-234">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="e234f-235">V klientovi JavaScript jsou zadané hodnoty časového limitu jako číslo určující dobu trvání v milisekundách.</span><span class="sxs-lookup"><span data-stu-id="e234f-235">In the JavaScript client, timeout values are specified as a number indicating the duration in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="e234f-236">Konfigurace dalších možností</span><span class="sxs-lookup"><span data-stu-id="e234f-236">Configure additional options</span></span>

<span data-ttu-id="e234f-237">Další možnosti se dá nakonfigurovat v `WithUrl` (`withUrl` v JavaScriptu) metoda `HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="e234f-237">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="e234f-238">.NET – možnost</span><span class="sxs-lookup"><span data-stu-id="e234f-238">.NET Option</span></span> | <span data-ttu-id="e234f-239">Možnost jazyka JavaScript</span><span class="sxs-lookup"><span data-stu-id="e234f-239">JavaScript Option</span></span> | <span data-ttu-id="e234f-240">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e234f-240">Default Value</span></span> | <span data-ttu-id="e234f-241">Popis</span><span class="sxs-lookup"><span data-stu-id="e234f-241">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | <span data-ttu-id="e234f-242">Funkce vrátí řetězec, který je k dispozici jako token nosiče ověřování v požadavcích HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-242">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | `false` | <span data-ttu-id="e234f-243">Nastavte na `true` přeskočit krok vyjednávání.</span><span class="sxs-lookup"><span data-stu-id="e234f-243">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="e234f-244">**Podporuje jenom při přenosu objekty Websocket je jediný povolený přenos**.</span><span class="sxs-lookup"><span data-stu-id="e234f-244">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="e234f-245">Toto nastavení není možné při použití služby Azure SignalR.</span><span class="sxs-lookup"><span data-stu-id="e234f-245">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="e234f-246">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-246">Not configurable \*</span></span> | <span data-ttu-id="e234f-247">prázdný</span><span class="sxs-lookup"><span data-stu-id="e234f-247">Empty</span></span> | <span data-ttu-id="e234f-248">Kolekce certifikáty TLS odeslat k ověření požadavků.</span><span class="sxs-lookup"><span data-stu-id="e234f-248">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="e234f-249">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-249">Not configurable \*</span></span> | <span data-ttu-id="e234f-250">prázdný</span><span class="sxs-lookup"><span data-stu-id="e234f-250">Empty</span></span> | <span data-ttu-id="e234f-251">Kolekce souborů cookie protokolu HTTP k odeslání při každé žádosti protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-251">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="e234f-252">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-252">Not configurable \*</span></span> | <span data-ttu-id="e234f-253">prázdný</span><span class="sxs-lookup"><span data-stu-id="e234f-253">Empty</span></span> | <span data-ttu-id="e234f-254">Přihlašovací údaje pro odesílání při každé žádosti protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-254">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="e234f-255">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-255">Not configurable \*</span></span> | <span data-ttu-id="e234f-256">5 sekund</span><span class="sxs-lookup"><span data-stu-id="e234f-256">5 seconds</span></span> | <span data-ttu-id="e234f-257">Pouze objekty Websocket.</span><span class="sxs-lookup"><span data-stu-id="e234f-257">WebSockets only.</span></span> <span data-ttu-id="e234f-258">Maximální množství času, klient počká po uzavření pro server a potvrďte žádosti o uzavření.</span><span class="sxs-lookup"><span data-stu-id="e234f-258">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="e234f-259">Pokud server není v tuto chvíli Potvrdit uzavření, klient neodpojí.</span><span class="sxs-lookup"><span data-stu-id="e234f-259">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="e234f-260">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-260">Not configurable \*</span></span> | <span data-ttu-id="e234f-261">prázdný</span><span class="sxs-lookup"><span data-stu-id="e234f-261">Empty</span></span> | <span data-ttu-id="e234f-262">Slovník další hlavičky protokolu HTTP k odeslání při každé žádosti protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-262">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="e234f-263">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-263">Not configurable \*</span></span> | `null` | <span data-ttu-id="e234f-264">Delegát, který lze použít ke konfiguraci nebo nahradit `HttpMessageHandler` používaný k odesílání požadavků HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-264">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="e234f-265">Není možné použít u připojení pomocí protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e234f-265">Not used for WebSocket connections.</span></span> <span data-ttu-id="e234f-266">Tento delegát musí vrátit nenulovou hodnotu, a přijímá jako parametr výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e234f-266">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="e234f-267">Upravte nastavení podle této výchozí hodnoty a vrácení nebo vrátí novou `HttpMessageHandler` instance.</span><span class="sxs-lookup"><span data-stu-id="e234f-267">Either modify settings on that default value and return it, or return a new `HttpMessageHandler` instance.</span></span> <span data-ttu-id="e234f-268">**Při nahrazování obslužnou rutinu nezapomeňte si zkopírovat na nastavení, která chcete zachovat od zadané obslužné rutiny, v opačném případě nakonfigurovaných možností (například soubory cookie a hlavičky) se nevztahuje na novou obslužnou rutinu.**</span><span class="sxs-lookup"><span data-stu-id="e234f-268">**When replacing the handler make sure to copy the settings you want to keep from the provided handler, otherwise, the configured options (such as Cookies and Headers) won't apply to the new handler.**</span></span> |
| `Proxy` | <span data-ttu-id="e234f-269">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-269">Not configurable \*</span></span> | `null` | <span data-ttu-id="e234f-270">Proxy server HTTP při odesílání požadavků HTTP.</span><span class="sxs-lookup"><span data-stu-id="e234f-270">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="e234f-271">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-271">Not configurable \*</span></span> | `false` | <span data-ttu-id="e234f-272">Nastavte tuto logickou hodnotu k odeslání výchozí přihlašovací údaje pro požadavky HTTP a Websocket.</span><span class="sxs-lookup"><span data-stu-id="e234f-272">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="e234f-273">To umožňuje použití ověřování Windows.</span><span class="sxs-lookup"><span data-stu-id="e234f-273">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="e234f-274">Nejde konfigurovat \*</span><span class="sxs-lookup"><span data-stu-id="e234f-274">Not configurable \*</span></span> | `null` | <span data-ttu-id="e234f-275">Delegát, který slouží k nakonfigurování dalších možností protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e234f-275">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="e234f-276">Obdrží instanci [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) , který lze použít ke konfiguraci možností.</span><span class="sxs-lookup"><span data-stu-id="e234f-276">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="e234f-277">Možnosti s hvězdičkou (\*) nejsou konfigurovatelné v klientovi JavaScript z důvodu omezení v prohlížeči rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="e234f-277">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="e234f-278">V klientovi .NET tyto možnosti je možné upravovat prostřednictvím delegáta možnosti poskytnuté `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="e234f-278">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="e234f-279">V klientovi JavaScript tyto možnosti lze zadat v objektu jazyka JavaScript poskytuje k `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="e234f-279">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    })
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="e234f-280">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="e234f-280">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
