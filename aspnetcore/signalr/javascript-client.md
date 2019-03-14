---
title: ASP.NET Core SignalR JavaScript klienta
author: bradygaster
description: Přehled ASP.NET Core SignalR JavaScript klienta.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: db9a8bbc8f111728f0827e3639e40785149bf79e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075040"
---
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="26995-103">ASP.NET Core SignalR JavaScript klienta</span><span class="sxs-lookup"><span data-stu-id="26995-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="26995-104">Podle [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="26995-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="26995-105">Klientská knihovna ASP.NET Core SignalR JavaScript umožňuje vývojářům volat kód rozbočovače na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="26995-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="26995-106">[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([stažení](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="26995-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="26995-107">Instalace balíčku pro klienta SignalR</span><span class="sxs-lookup"><span data-stu-id="26995-107">Install the SignalR client package</span></span>

<span data-ttu-id="26995-108">Klientské knihovny SignalR JavaScript je dodávána jako [npm](https://www.npmjs.com/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="26995-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="26995-109">Pokud používáte Visual Studio, spusťte `npm install` z **Konzola správce balíčků** během činnosti v kořenové složce.</span><span class="sxs-lookup"><span data-stu-id="26995-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="26995-110">Visual Studio Code, spusťte příkaz z **integrovaný terminál**.</span><span class="sxs-lookup"><span data-stu-id="26995-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

<span data-ttu-id="26995-111">npm nainstaluje balíček obsahu *node_modules\\@aspnet\signalr\dist\browser* složky.</span><span class="sxs-lookup"><span data-stu-id="26995-111">npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="26995-112">Vytvořte novou složku s názvem *signalr* pod *wwwroot\\lib* složky.</span><span class="sxs-lookup"><span data-stu-id="26995-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="26995-113">Kopírovat *signalr.js* do souboru *wwwroot\lib\signalr* složky.</span><span class="sxs-lookup"><span data-stu-id="26995-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="26995-114">Použití klienta SignalR JavaScript</span><span class="sxs-lookup"><span data-stu-id="26995-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="26995-115">Odkazovat na klientovi SignalR JavaScript v `<script>` elementu.</span><span class="sxs-lookup"><span data-stu-id="26995-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="26995-116">Připojení k rozbočovači</span><span class="sxs-lookup"><span data-stu-id="26995-116">Connect to a hub</span></span>

<span data-ttu-id="26995-117">Následující kód vytvoří a spustí připojení.</span><span class="sxs-lookup"><span data-stu-id="26995-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="26995-118">Název centra se nerozlišují malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="26995-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-13,43-45)]

### <a name="cross-origin-connections"></a><span data-ttu-id="26995-119">Nepůvodního zdroje připojení</span><span class="sxs-lookup"><span data-stu-id="26995-119">Cross-origin connections</span></span>

<span data-ttu-id="26995-120">Obvykle prohlížeče načíst připojení ve stejné doméně jako požadovanou stránku.</span><span class="sxs-lookup"><span data-stu-id="26995-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="26995-121">Existují však situace, kdy je vyžadováno připojení k jiné doméně.</span><span class="sxs-lookup"><span data-stu-id="26995-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="26995-122">Aby se zabránilo škodlivým webům ve čtení citlivých dat z jiné lokality [nepůvodního zdroje připojení](xref:security/cors) jsou ve výchozím nastavení zakázané.</span><span class="sxs-lookup"><span data-stu-id="26995-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="26995-123">Žádosti nepůvodního zdroje, povolit jej `Startup` třídy.</span><span class="sxs-lookup"><span data-stu-id="26995-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="26995-124">Volání metod rozbočovače na z klienta</span><span class="sxs-lookup"><span data-stu-id="26995-124">Call hub methods from client</span></span>

<span data-ttu-id="26995-125">Klientům JavaScript volat veřejné metody rozbočovače prostřednictvím [vyvolat](/javascript/api/%40aspnet/signalr/hubconnection#invoke) metodu [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection).</span><span class="sxs-lookup"><span data-stu-id="26995-125">JavaScript clients call public methods on hubs via the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) method of the [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection).</span></span> <span data-ttu-id="26995-126">`invoke` Metoda přijímá dva argumenty:</span><span class="sxs-lookup"><span data-stu-id="26995-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="26995-127">Název metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="26995-127">The name of the hub method.</span></span> <span data-ttu-id="26995-128">V následujícím příkladu je název metody rozbočovače `SendMessage`.</span><span class="sxs-lookup"><span data-stu-id="26995-128">In the following example, the method name on the hub is `SendMessage`.</span></span>
* <span data-ttu-id="26995-129">Všechny argumenty podle metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="26995-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="26995-130">V následujícím příkladu je název argumentu `message`.</span><span class="sxs-lookup"><span data-stu-id="26995-130">In the following example, the argument name is `message`.</span></span> <span data-ttu-id="26995-131">Příklad kódu používá syntaxe funkce šipku, která je podporována v aktuálních verzích všechny hlavní prohlížeče s výjimkou aplikace Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="26995-131">The example code uses arrow function syntax that is supported in current versions of all major browsers except Internet Explorer.</span></span>

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="26995-132">Volání metody klienta od rozbočovače</span><span class="sxs-lookup"><span data-stu-id="26995-132">Call client methods from hub</span></span>

<span data-ttu-id="26995-133">Chcete-li přijímat zprávy z centra, definovat metodu pomocí [na](/javascript/api/%40aspnet/signalr/hubconnection#on) metodu `HubConnection`.</span><span class="sxs-lookup"><span data-stu-id="26995-133">To receive messages from the hub, define a method using the [on](/javascript/api/%40aspnet/signalr/hubconnection#on) method of the `HubConnection`.</span></span>

* <span data-ttu-id="26995-134">Název metody jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="26995-134">The name of the JavaScript client method.</span></span> <span data-ttu-id="26995-135">V následujícím příkladu je název metody `ReceiveMessage`.</span><span class="sxs-lookup"><span data-stu-id="26995-135">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="26995-136">Argumenty, které se předá metodě rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="26995-136">Arguments the hub passes to the method.</span></span> <span data-ttu-id="26995-137">V následujícím příkladu je hodnota argumentu `message`.</span><span class="sxs-lookup"><span data-stu-id="26995-137">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="26995-138">Předchozí kód v `connection.on` spustí, když kód na straně serveru pomocí volání [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) metoda.</span><span class="sxs-lookup"><span data-stu-id="26995-138">The preceding code in `connection.on` runs when server-side code calls it using the [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="26995-139">SignalR Určuje, jakou metodu klienta volat to provede spárováním odpovídajících názvu metody a argumenty definovaných v `SendAsync` a `connection.on`.</span><span class="sxs-lookup"><span data-stu-id="26995-139">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="26995-140">Jako osvědčený postup volání [start](/javascript/api/%40aspnet/signalr/hubconnection#start) metodu `HubConnection` po `on`.</span><span class="sxs-lookup"><span data-stu-id="26995-140">As a best practice, call the [start](/javascript/api/%40aspnet/signalr/hubconnection#start) method on the `HubConnection` after `on`.</span></span> <span data-ttu-id="26995-141">Tím se zajistí, že vaše obslužné rutiny jsou registrovány předtím, než jsou přijaty žádné zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-141">Doing so ensures your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="26995-142">Protokolování a zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="26995-142">Error handling and logging</span></span>

<span data-ttu-id="26995-143">Řetězce `catch` metoda na konec objektu `start` metodu ke zpracování chyby na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="26995-143">Chain a `catch` method to the end of the `start` method to handle client-side errors.</span></span> <span data-ttu-id="26995-144">Použití `console.error` chyby výstup do konzoly prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="26995-144">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=49-51)]

<span data-ttu-id="26995-145">Nastavení na straně klienta protokolu trasování předáním protokolovací nástroj a typ události do protokolu, když se připojení.</span><span class="sxs-lookup"><span data-stu-id="26995-145">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="26995-146">Zprávy jsou zaznamenány na úrovni zadaný protokol a vyšší.</span><span class="sxs-lookup"><span data-stu-id="26995-146">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="26995-147">Dostupné úrovně jsou následující:</span><span class="sxs-lookup"><span data-stu-id="26995-147">Available log levels are as follows:</span></span>

* <span data-ttu-id="26995-148">`signalR.LogLevel.Error` &ndash; Chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-148">`signalR.LogLevel.Error` &ndash; Error messages.</span></span> <span data-ttu-id="26995-149">Protokoly `Error` pouze zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-149">Logs `Error` messages only.</span></span>
* <span data-ttu-id="26995-150">`signalR.LogLevel.Warning` &ndash; Zprávy s upozorněním potenciální chyby.</span><span class="sxs-lookup"><span data-stu-id="26995-150">`signalR.LogLevel.Warning` &ndash; Warning messages about potential errors.</span></span> <span data-ttu-id="26995-151">Protokoly `Warning`, a `Error` zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-151">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="26995-152">`signalR.LogLevel.Information` &ndash; Stavové zprávy bez chyb.</span><span class="sxs-lookup"><span data-stu-id="26995-152">`signalR.LogLevel.Information` &ndash; Status messages without errors.</span></span> <span data-ttu-id="26995-153">Protokoly `Information`, `Warning`, a `Error` zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-153">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="26995-154">`signalR.LogLevel.Trace` &ndash; Trasovací zprávy.</span><span class="sxs-lookup"><span data-stu-id="26995-154">`signalR.LogLevel.Trace` &ndash; Trace messages.</span></span> <span data-ttu-id="26995-155">Protokoly vše, včetně dat přenášených mezi centrem a klienta.</span><span class="sxs-lookup"><span data-stu-id="26995-155">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="26995-156">Použití [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) metoda [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) nakonfigurovat úroveň protokolu.</span><span class="sxs-lookup"><span data-stu-id="26995-156">Use the [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) method on [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) to configure the log level.</span></span> <span data-ttu-id="26995-157">Zprávy jsou protokolovány do konzoly prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="26995-157">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="reconnect-clients"></a><span data-ttu-id="26995-158">Opětovné připojení klientů</span><span class="sxs-lookup"><span data-stu-id="26995-158">Reconnect clients</span></span>

<span data-ttu-id="26995-159">JavaScript klienta pro funkci SignalR nebude automaticky znovu připojit.</span><span class="sxs-lookup"><span data-stu-id="26995-159">The JavaScript client for SignalR doesn't automatically reconnect.</span></span> <span data-ttu-id="26995-160">Musíte napsat kód, který se znovu připojit klientu ručně.</span><span class="sxs-lookup"><span data-stu-id="26995-160">You must write code that will reconnect your client manually.</span></span> <span data-ttu-id="26995-161">Následující kód ukazuje typické nastavitelnou přístup:</span><span class="sxs-lookup"><span data-stu-id="26995-161">The following code demonstrates a typical reconnection approach:</span></span>

1. <span data-ttu-id="26995-162">Funkce (v tomto případě `start` funkce) se vytvoří připojení spustíte.</span><span class="sxs-lookup"><span data-stu-id="26995-162">A function (in this case, the `start` function) is created to start the connection.</span></span>
1. <span data-ttu-id="26995-163">Volání `start` funkce v rámci připojení `onclose` obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="26995-163">Call the `start` function in the connection's `onclose` event handler.</span></span>

[!code-javascript[Reconnect the JavaScript client](javascript-client/sample/wwwroot/js/chat.js?range=28-40)]

<span data-ttu-id="26995-164">Skutečná implementace by použít exponenciální regrese nebo opakování zadaného počtu opakování, než se ukončí.</span><span class="sxs-lookup"><span data-stu-id="26995-164">A real-world implementation would use an exponential back-off or retry a specified number of times before giving up.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26995-165">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="26995-165">Additional resources</span></span>

* [<span data-ttu-id="26995-166">Referenční dokumentace k rozhraní API v JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="26995-166">JavaScript API reference</span></span>](/javascript/api/?view=signalr-js-latest)
* [<span data-ttu-id="26995-167">Kurz jazyka JavaScript</span><span class="sxs-lookup"><span data-stu-id="26995-167">JavaScript tutorial</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="26995-168">Kurz Webpacku a TypeScript</span><span class="sxs-lookup"><span data-stu-id="26995-168">WebPack and TypeScript tutorial</span></span>](xref:tutorials/signalr-typescript-webpack)
* [<span data-ttu-id="26995-169">Centra</span><span class="sxs-lookup"><span data-stu-id="26995-169">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="26995-170">Klient .NET</span><span class="sxs-lookup"><span data-stu-id="26995-170">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="26995-171">Publikování do Azure</span><span class="sxs-lookup"><span data-stu-id="26995-171">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="26995-172">Požadavky mezi zdroji (CORS)</span><span class="sxs-lookup"><span data-stu-id="26995-172">Cross-Origin Requests (CORS)</span></span>](xref:security/cors)
