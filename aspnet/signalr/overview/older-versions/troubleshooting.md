---
uid: signalr/overview/older-versions/troubleshooting
title: Řešení potíží se signálním rzií (SignalR 1.x) | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento článek popisuje běžné problémy s vývojem aplikací SignalR.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543090"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="cd180-103">Řešení potíží s knihovnou SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="cd180-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="cd180-104">podle [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="cd180-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="cd180-105">Tento dokument popisuje běžné problémy s řešením potíží se signálem SignalR.</span><span class="sxs-lookup"><span data-stu-id="cd180-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="cd180-106">Tento dokument obsahuje následující části.</span><span class="sxs-lookup"><span data-stu-id="cd180-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="cd180-107">Volající metody mezi klientem a serverem tiše se nezdaří</span><span class="sxs-lookup"><span data-stu-id="cd180-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="cd180-108">Další problémy s připojením</span><span class="sxs-lookup"><span data-stu-id="cd180-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="cd180-109">Chyby kompilace a na straně serveru</span><span class="sxs-lookup"><span data-stu-id="cd180-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="cd180-110">Problémy s visual studio</span><span class="sxs-lookup"><span data-stu-id="cd180-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="cd180-111">Problémy s Internetovou informační službou</span><span class="sxs-lookup"><span data-stu-id="cd180-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="cd180-112">Problémy s Azure</span><span class="sxs-lookup"><span data-stu-id="cd180-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="cd180-113">Volající metody mezi klientem a serverem tiše se nezdaří</span><span class="sxs-lookup"><span data-stu-id="cd180-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="cd180-114">Tato část popisuje možné příčiny volání metody mezi klientem a serverem nezdaří bez smysluplné chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="cd180-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="cd180-115">V aplikaci SignalR server nemá žádné informace o metodách, které klient implementuje; Když server vyvolá metodu klienta, jsou klientovi odeslána data názvu metody a parametru a metoda je spuštěna pouze v případě, že existuje ve formátu, který server zadal.</span><span class="sxs-lookup"><span data-stu-id="cd180-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="cd180-116">Pokud není v klientovi nalezena žádná odpovídající metoda, nic se nestane a na serveru není vyvolána žádná chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="cd180-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="cd180-117">Chcete-li dále zkoumat klientské metody, které nejsou volány, můžete zapnout protokolování před voláním metody start v centru a zjistit, jaká volání přicházejí ze serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="cd180-118">Informace o povolení protokolování v aplikaci JavaScript naleznete v tématu [Jak povolit protokolování na straně klienta (verze klienta JavaScriptu).](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="cd180-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="cd180-119">Informace o povolení protokolování klientské aplikace .NET naleznete v tématu [Jak povolit protokolování na straně klienta (verze klienta.NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="cd180-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="cd180-120">Chybně napsaná metoda, nesprávný podpis metody nebo nesprávný název rozbočovače</span><span class="sxs-lookup"><span data-stu-id="cd180-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="cd180-121">Pokud název nebo podpis volané metody přesně neodpovídá vhodné metodě na straně klienta, volání se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="cd180-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="cd180-122">Ověřte, zda název metody volaný serverem odpovídá názvu metody v klientovi.</span><span class="sxs-lookup"><span data-stu-id="cd180-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="cd180-123">SignalR také vytvoří proxy centra pomocí camel-cased metody, jak je vhodné `SendMessage` v Jazyce `sendMessage` JavaScript, takže metoda volaná na serveru by být volána v proxy klienta.</span><span class="sxs-lookup"><span data-stu-id="cd180-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="cd180-124">Pokud použijete `HubName` atribut v kódu na straně serveru, ověřte, zda použitý název odpovídá názvu použitému k vytvoření centra v klientovi.</span><span class="sxs-lookup"><span data-stu-id="cd180-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="cd180-125">Pokud `HubName` atribut nepoužíváte, ověřte, zda je název centra v klientovi JavaScriptu camel-cased, například chatHub místo ChatHub.</span><span class="sxs-lookup"><span data-stu-id="cd180-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="cd180-126">Duplicitní název metody v klientovi</span><span class="sxs-lookup"><span data-stu-id="cd180-126">Duplicate method name on client</span></span>

<span data-ttu-id="cd180-127">Ověřte, zda nemáte duplicitní metodu v klientovi, která se liší pouze případ.</span><span class="sxs-lookup"><span data-stu-id="cd180-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="cd180-128">Pokud má klientská aplikace `sendMessage`metodu nazývanou , `SendMessage` ověřte, zda není také volána metoda.</span><span class="sxs-lookup"><span data-stu-id="cd180-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="cd180-129">Chybějící analyzátor JSON na straně klienta</span><span class="sxs-lookup"><span data-stu-id="cd180-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="cd180-130">SignalR vyžaduje Analyzátor JSON být přítomen serializovat volání mezi serverem a klientem.</span><span class="sxs-lookup"><span data-stu-id="cd180-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="cd180-131">Pokud váš klient nemá předdefinovaný analyzátor JSON (například Internet Explorer 7), budete ho muset do aplikace zahrnout.</span><span class="sxs-lookup"><span data-stu-id="cd180-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="cd180-132">Můžete si stáhnout Analyzátor JSON [zde](http://nuget.org/packages/json2).</span><span class="sxs-lookup"><span data-stu-id="cd180-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="cd180-133">Míchání centra a syntaxe trvalého připojení</span><span class="sxs-lookup"><span data-stu-id="cd180-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="cd180-134">SignalR používá dva modely komunikace: Rozbočovače a PersistentConnections.</span><span class="sxs-lookup"><span data-stu-id="cd180-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="cd180-135">Syntaxe pro volání těchto dvou komunikačních modelů se liší v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="cd180-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="cd180-136">Pokud jste do kódu serveru přidali rozbočovač, ověřte, že veškerý klientský kód používá správnou syntaxi rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="cd180-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="cd180-137">**Klientský kód JavaScriptu, který vytváří trvalé připojení v klientovi JavaScriptu**</span><span class="sxs-lookup"><span data-stu-id="cd180-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="cd180-138">**Klientský kód JavaScriptu, který vytvoří hubproxy v klientovi Javascriptu**</span><span class="sxs-lookup"><span data-stu-id="cd180-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="cd180-139">**Kód serveru Jazyka C#, který mapuje trasu na trvalé připojení**</span><span class="sxs-lookup"><span data-stu-id="cd180-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="cd180-140">**Kód serveru C#, který mapuje trasu do centra nebo na více rozbočovačů, pokud máte více aplikací**</span><span class="sxs-lookup"><span data-stu-id="cd180-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="cd180-141">Připojení bylo spuštěno před přidáním předplatných.</span><span class="sxs-lookup"><span data-stu-id="cd180-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="cd180-142">Pokud je připojení centra spuštěno před tím, než jsou do proxy serveru přidány metody, které lze volat ze serveru, nebudou zprávy přijaty.</span><span class="sxs-lookup"><span data-stu-id="cd180-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="cd180-143">Následující kód Jazyka JavaScript nespustí rozbočovač správně:</span><span class="sxs-lookup"><span data-stu-id="cd180-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="cd180-144">**Nesprávný kód klienta javascriptu, který neumožňuje přijímat zprávy hubů**</span><span class="sxs-lookup"><span data-stu-id="cd180-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="cd180-145">Místo toho přidejte před voláním předvolání metody Start:</span><span class="sxs-lookup"><span data-stu-id="cd180-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="cd180-146">**Klientský kód JavaScriptu, který správně přidává odběry do rozbočovače**</span><span class="sxs-lookup"><span data-stu-id="cd180-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="cd180-147">Chybějící název metody v serveru proxy centra</span><span class="sxs-lookup"><span data-stu-id="cd180-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="cd180-148">Ověřte, zda je metoda definovaná na serveru přihlášena k odběru v klientovi.</span><span class="sxs-lookup"><span data-stu-id="cd180-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="cd180-149">I když server definuje metodu, musí být stále přidána do proxy serveru klienta.</span><span class="sxs-lookup"><span data-stu-id="cd180-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="cd180-150">Metody lze přidat do proxy klienta následujícími způsoby (Všimněte si, že metoda je přidána do `client` člena rozbočovače, nikoli přímo do rozbočovače):</span><span class="sxs-lookup"><span data-stu-id="cd180-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="cd180-151">**Klientský kód JavaScriptu, který přidává metody do proxy centra**</span><span class="sxs-lookup"><span data-stu-id="cd180-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="cd180-152">Metody rozbočovače nebo rozbočovače, které nejsou deklarovány jako veřejné</span><span class="sxs-lookup"><span data-stu-id="cd180-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="cd180-153">Chcete-li být viditelné na straně klienta, `public`musí být deklarována implementace centra a metody jako .</span><span class="sxs-lookup"><span data-stu-id="cd180-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="cd180-154">Přístup k rozbočovači z jiné aplikace</span><span class="sxs-lookup"><span data-stu-id="cd180-154">Accessing hub from a different application</span></span>

<span data-ttu-id="cd180-155">SignalR Rozbočovače lze přistupovat pouze prostřednictvím aplikací, které implementují klienty SignalR.</span><span class="sxs-lookup"><span data-stu-id="cd180-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="cd180-156">SignalR nelze spolupracovat s jinými komunikačními knihovnami (například SOAP nebo WCF webové služby.) Pokud není pro cílovou platformu k dispozici žádný klient SignalR, nelze získat přímý přístup ke koncovému bodu serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="cd180-157">Ruční serializace dat</span><span class="sxs-lookup"><span data-stu-id="cd180-157">Manually serializing data</span></span>

<span data-ttu-id="cd180-158">SignalR bude automaticky používat JSON serializovat parametry metody- není třeba to udělat sami.</span><span class="sxs-lookup"><span data-stu-id="cd180-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="cd180-159">Metoda vzdáleného rozbočovače nebyla spuštěna na straně klienta ve funkci OnDisconnected</span><span class="sxs-lookup"><span data-stu-id="cd180-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="cd180-160">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-160">This behavior is by design.</span></span> <span data-ttu-id="cd180-161">Při `OnDisconnected` volání rozbočovač již `Disconnected` vstoupil do stavu, který neumožňuje další metody rozbočovače, které mají být volány.</span><span class="sxs-lookup"><span data-stu-id="cd180-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="cd180-162">**Kód serveru Jazyka C#, který správně spustí kód v události OnDisconnected**</span><span class="sxs-lookup"><span data-stu-id="cd180-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="cd180-163">Bylo dosaženo limitu připojení.</span><span class="sxs-lookup"><span data-stu-id="cd180-163">Connection limit reached</span></span>

<span data-ttu-id="cd180-164">Při použití plné verze služby IIS v klientském operačním systému, jako je windows 7, je uložen limit připojení 10.</span><span class="sxs-lookup"><span data-stu-id="cd180-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="cd180-165">Při použití klientského operačního operačního příkazu se tomuto limitu vyhněte pomocí služby IIS Express.</span><span class="sxs-lookup"><span data-stu-id="cd180-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="cd180-166">Připojení mezi doménami není správně nastaveno</span><span class="sxs-lookup"><span data-stu-id="cd180-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="cd180-167">Pokud připojení mezi doménami (připojení, pro které adresa URL signalru není ve stejné doméně jako hostitelská stránka) není správně nastaveno, může dojít k selhání připojení bez chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="cd180-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="cd180-168">Informace o povolení komunikace mezi doménami naleznete v [tématu Jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="cd180-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="cd180-169">Připojení pomocí ntlm (Active Directory) nefunguje v klientovi .NET</span><span class="sxs-lookup"><span data-stu-id="cd180-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="cd180-170">Připojení v klientské aplikaci .NET, která používá zabezpečení domény, může selhat, pokud připojení není správně nakonfigurováno.</span><span class="sxs-lookup"><span data-stu-id="cd180-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="cd180-171">Chcete-li použít SignalR v prostředí domény, nastavte vlastnost potřebného připojení takto:</span><span class="sxs-lookup"><span data-stu-id="cd180-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="cd180-172">**Kód klienta jazyka C#, který implementuje pověření připojení**</span><span class="sxs-lookup"><span data-stu-id="cd180-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="cd180-173">Další problémy s připojením</span><span class="sxs-lookup"><span data-stu-id="cd180-173">Other connection issues</span></span>

<span data-ttu-id="cd180-174">Tato část popisuje příčiny a řešení pro konkrétní příznaky nebo chybové zprávy, ke kterým dochází během připojení.</span><span class="sxs-lookup"><span data-stu-id="cd180-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="cd180-175">Před odesláním dat je nutné volat začátek.</span><span class="sxs-lookup"><span data-stu-id="cd180-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="cd180-176">Tato chyba se běžně zobrazuje, pokud kód odkazuje na objekty SignalR před spuštěním připojení.</span><span class="sxs-lookup"><span data-stu-id="cd180-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="cd180-177">Po dokončení připojení musí být přidány metody definované na serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="cd180-178">Všimněte si, `Start` že volání je asynchronní, takže kód po volání může být proveden před jeho dokončením.</span><span class="sxs-lookup"><span data-stu-id="cd180-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="cd180-179">Nejlepší způsob, jak přidat obslužné rutiny po úplném spuštění připojení je umístit do funkce zpětného volání, která je předána jako parametr metody start:</span><span class="sxs-lookup"><span data-stu-id="cd180-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="cd180-180">**Kód klienta JavaScriptu, který správně přidává obslužné rutiny událostí, které odkazují na objekty SignalR**</span><span class="sxs-lookup"><span data-stu-id="cd180-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="cd180-181">Tato chyba se také zobrazí, pokud se připojení zastaví, zatímco signalr objekty jsou stále odkazuje.</span><span class="sxs-lookup"><span data-stu-id="cd180-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="cd180-182">Chyba "301 Trvale přesunuta" nebo "302 přesunuta dočasně"</span><span class="sxs-lookup"><span data-stu-id="cd180-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="cd180-183">Tato chyba může být vidět, pokud projekt obsahuje složku s názvem SignalR, který bude zasahovat do automaticky vytvořené proxy.</span><span class="sxs-lookup"><span data-stu-id="cd180-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="cd180-184">Chcete-li se této chybě vyhnout, nepoužívejte složku volanou `SignalR` v aplikaci ani nezapněte automatické generování proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="cd180-185">Další podrobnosti najdete [v tématu Vygenerovaný proxy server a to, co pro vás dělá.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)</span><span class="sxs-lookup"><span data-stu-id="cd180-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="cd180-186">Chyba "403 Zakázáno" v klientovi .NET nebo Silverlight</span><span class="sxs-lookup"><span data-stu-id="cd180-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="cd180-187">K této chybě může dojít v prostředích mezi doménami, kde není správně povolena komunikace mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="cd180-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="cd180-188">Informace o povolení komunikace mezi doménami naleznete v [tématu Jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="cd180-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="cd180-189">Chcete-li vytvořit připojení mezi doménami v klientovi Silverlight, přečtěte [si informace o připojení mezi doménami z klientů Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span><span class="sxs-lookup"><span data-stu-id="cd180-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="cd180-190">Chyba "404 nebyla nalezena"</span><span class="sxs-lookup"><span data-stu-id="cd180-190">"404 Not Found" error</span></span>

<span data-ttu-id="cd180-191">Existuje několik příčin tohoto problému.</span><span class="sxs-lookup"><span data-stu-id="cd180-191">There are several causes for this issue.</span></span> <span data-ttu-id="cd180-192">Ověřte všechny následující skutečnosti:</span><span class="sxs-lookup"><span data-stu-id="cd180-192">Verify all of the following:</span></span>

- <span data-ttu-id="cd180-193">**Odkaz na adresu proxy centra není správně formátován:** Tato chyba je běžně vidět, pokud odkaz na vygenerovanou adresu proxy centra není správně formátován.</span><span class="sxs-lookup"><span data-stu-id="cd180-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="cd180-194">Ověřte, zda je správně nastaven odkaz na adresu centra.</span><span class="sxs-lookup"><span data-stu-id="cd180-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="cd180-195">Podrobnosti naleznete [v tématu Jak odkazovat na dynamicky generovaný proxy server.](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)</span><span class="sxs-lookup"><span data-stu-id="cd180-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="cd180-196">**Přidání tras do aplikace před přidáním trasy rozbočovače:** Pokud aplikace používá jiné trasy, ověřte, zda `MapHubs`je první přidanou trasou volání aplikace .</span><span class="sxs-lookup"><span data-stu-id="cd180-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="cd180-197">"Chyba interního serveru 500"</span><span class="sxs-lookup"><span data-stu-id="cd180-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="cd180-198">Jedná se o velmi obecnou chybu, která může mít širokou škálu příčin.</span><span class="sxs-lookup"><span data-stu-id="cd180-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="cd180-199">Podrobnosti o chybě by se měly objevit v protokolu událostí serveru nebo lze nalézt laděním serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="cd180-200">Podrobnější informace o chybách lze získat zapnutím podrobných chyb na serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="cd180-201">Další informace naleznete v tématu [Jak zpracovat chyby ve třídě Hub](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span><span class="sxs-lookup"><span data-stu-id="cd180-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="cd180-202">Chyba &lt;"TypeError:&gt; hubType is undefined"</span><span class="sxs-lookup"><span data-stu-id="cd180-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="cd180-203">Tato chyba bude mít `MapHubs` za následek, pokud volání není provedena správně.</span><span class="sxs-lookup"><span data-stu-id="cd180-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="cd180-204">Další informace naleznete [v tématu Jak zaregistrovat trasu SignalR a nakonfigurovat možnosti SignalR.](../guide-to-the-api/hubs-api-guide-server.md#route)</span><span class="sxs-lookup"><span data-stu-id="cd180-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="cd180-205">JsonSerializationException nebyl zpracován uživatelským kódem.</span><span class="sxs-lookup"><span data-stu-id="cd180-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="cd180-206">Ověřte, zda parametry odesílané do metod neobsahují neserializovatelné typy (například popisovače souborů nebo připojení k databázi).</span><span class="sxs-lookup"><span data-stu-id="cd180-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="cd180-207">Pokud potřebujete použít členy na straně serveru objektu, který nechcete být odeslány klientovi (buď z důvodu `JSONIgnore` zabezpečení nebo z důvodu serializace), použijte atribut.</span><span class="sxs-lookup"><span data-stu-id="cd180-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="cd180-208">Chyba protokolu: Neznámý přenos</span><span class="sxs-lookup"><span data-stu-id="cd180-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="cd180-209">K této chybě může dojít, pokud klient nepodporuje přenosy, které používá SignalR.</span><span class="sxs-lookup"><span data-stu-id="cd180-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="cd180-210">Informace o tom, na kterých lze prohlížeče používat s SignalR, naleznete v části [Transporty a záložní](../getting-started/introduction-to-signalr.md#transports) soubory.</span><span class="sxs-lookup"><span data-stu-id="cd180-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="cd180-211">"Generování proxy centra JavaScript hub bylo zakázáno."</span><span class="sxs-lookup"><span data-stu-id="cd180-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="cd180-212">K této chybě `DisableJavaScriptProxies` dojde, pokud je nastavena a zároveň `signalr/hubs`obsahuje odkaz na dynamicky generovaný proxy server na .</span><span class="sxs-lookup"><span data-stu-id="cd180-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="cd180-213">Další informace o ručním vytváření proxy serveru naleznete v [tématu Vygenerovaný proxy server a o tom, co pro vás dělá](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="cd180-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="cd180-214">"ID připojení je v nesprávném formátu" nebo "Identita uživatele se nemůže během aktivního připojení SignalR změnit"</span><span class="sxs-lookup"><span data-stu-id="cd180-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="cd180-215">Tato chyba může být vidět, pokud je používáno ověřování a klient je odhlášen před zastavením připojení.</span><span class="sxs-lookup"><span data-stu-id="cd180-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="cd180-216">Řešením je zastavit připojení SignalR před odhlášením klienta.</span><span class="sxs-lookup"><span data-stu-id="cd180-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="cd180-217">"Nezachycená chyba: SignalR: jQuery nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="cd180-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="cd180-218">Ujistěte se, že jQuery je odkazováno před chybou souboru SignalR.js</span><span class="sxs-lookup"><span data-stu-id="cd180-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="cd180-219">Klient JavaScript SignalR vyžaduje ke spuštění jQuery.</span><span class="sxs-lookup"><span data-stu-id="cd180-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="cd180-220">Ověřte, zda je odkaz na jQuery správný, zda je použitá cesta platná a zda je odkaz na jQuery před odkazem na SignalR.</span><span class="sxs-lookup"><span data-stu-id="cd180-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="cd180-221">Chyba "Uncaught TypeError:&lt;Nelze&gt;číst vlastnost " vlastnosti ' nedefinované"</span><span class="sxs-lookup"><span data-stu-id="cd180-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="cd180-222">Tato chyba je výsledkem toho, že jQuery nebo proxy centra správně odkazuje.</span><span class="sxs-lookup"><span data-stu-id="cd180-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="cd180-223">Ověřte, zda je váš odkaz na jQuery a proxy centra správný, zda je použitá cesta platná a zda je odkaz na jQuery před odkazem na proxy centra.</span><span class="sxs-lookup"><span data-stu-id="cd180-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="cd180-224">Výchozí odkaz na proxy centra hubů by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="cd180-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="cd180-225">**Kód html na straně klienta, který správně odkazuje na proxy centra**</span><span class="sxs-lookup"><span data-stu-id="cd180-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="cd180-226">Chyba RuntimeBinderException nebyla zpracována kódem uživatele.</span><span class="sxs-lookup"><span data-stu-id="cd180-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="cd180-227">K této chybě může dojít `Hub.On` při použití nesprávné přetížení.</span><span class="sxs-lookup"><span data-stu-id="cd180-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="cd180-228">Pokud má metoda vrácenou hodnotu, musí být jako parametr obecného typu zadán návratový typ:</span><span class="sxs-lookup"><span data-stu-id="cd180-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="cd180-229">**Metoda definovaná na straně klienta (bez generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="cd180-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="cd180-230">ID připojení je nekonzistentní nebo konce připojení mezi načtením stránky</span><span class="sxs-lookup"><span data-stu-id="cd180-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="cd180-231">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-231">This behavior is by design.</span></span> <span data-ttu-id="cd180-232">Vzhledem k tomu, že objekt rozbočovače je hostován v objektu stránky, rozbočovač je zničen při aktualizaci stránky.</span><span class="sxs-lookup"><span data-stu-id="cd180-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="cd180-233">Vícestránková aplikace musí udržovat přidružení mezi uživateli a ID připojení tak, aby byly konzistentní mezi načítánístránky.</span><span class="sxs-lookup"><span data-stu-id="cd180-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="cd180-234">ID připojení mohou být uložena na `ConcurrentDictionary` serveru v objektu nebo databázi.</span><span class="sxs-lookup"><span data-stu-id="cd180-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="cd180-235">Chyba "Hodnota nemůže být null"</span><span class="sxs-lookup"><span data-stu-id="cd180-235">"Value cannot be null" error</span></span>

<span data-ttu-id="cd180-236">Metody na straně serveru s volitelnými parametry nejsou aktuálně podporovány. Pokud je volitelný parametr vynechán, metoda se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="cd180-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="cd180-237">Další informace naleznete v [tématu Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span><span class="sxs-lookup"><span data-stu-id="cd180-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="cd180-238">"Firefox nemůže navázat připojení k serveru &lt;&gt;na adrese " chyba v Firebug</span><span class="sxs-lookup"><span data-stu-id="cd180-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="cd180-239">Tato chybová zpráva může být viděn v Firebug, pokud vyjednávání přenosu WebSocket selže a jiný přenos se používá místo.</span><span class="sxs-lookup"><span data-stu-id="cd180-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="cd180-240">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="cd180-241">Chyba "Vzdálený certifikát je neplatný podle postupu ověření" v klientské aplikaci .NET</span><span class="sxs-lookup"><span data-stu-id="cd180-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="cd180-242">Pokud váš server vyžaduje vlastní klientské certifikáty, můžete přidat certifikát x509 k připojení před posunutím požadavku.</span><span class="sxs-lookup"><span data-stu-id="cd180-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="cd180-243">Přidejte certifikát k `Connection.AddClientCertificate`připojení pomocí aplikace .</span><span class="sxs-lookup"><span data-stu-id="cd180-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="cd180-244">Připojení klesne po uplynutí doby vypršel časový limit ověřování</span><span class="sxs-lookup"><span data-stu-id="cd180-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="cd180-245">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-245">This behavior is by design.</span></span> <span data-ttu-id="cd180-246">Ověřovací pověření nelze změnit, pokud je připojení aktivní. chcete-li aktualizovat pověření, musí být připojení zastaveno a restartováno.</span><span class="sxs-lookup"><span data-stu-id="cd180-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="cd180-247">OnConnected dostane volána dvakrát při použití jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="cd180-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="cd180-248">`initializePage` Funkce jQuery Mobile vynutí opětovné spuštění skriptů na každé stránce, čímž se vytvoří druhé připojení.</span><span class="sxs-lookup"><span data-stu-id="cd180-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="cd180-249">Řešení tohoto problému zahrnují:</span><span class="sxs-lookup"><span data-stu-id="cd180-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="cd180-250">Před soubor javascriptu uveďte odkaz na soubor jQuery Mobile.</span><span class="sxs-lookup"><span data-stu-id="cd180-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="cd180-251">Zakažte `initializePage` `$.mobile.autoInitializePage = false`funkci nastavením .</span><span class="sxs-lookup"><span data-stu-id="cd180-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="cd180-252">Před zahájením připojení počkejte na dokončení inicializace stránky.</span><span class="sxs-lookup"><span data-stu-id="cd180-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="cd180-253">Zprávy jsou zpožděny v aplikacích Silverlight pomocí událostí odeslaných serverem</span><span class="sxs-lookup"><span data-stu-id="cd180-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="cd180-254">Zprávy jsou zpožděny při použití událostí odeslaných serverem v systému Silverlight.</span><span class="sxs-lookup"><span data-stu-id="cd180-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="cd180-255">Chcete-li místo toho vynutit použití dlouhého dotazování, použijte při spuštění připojení následující:</span><span class="sxs-lookup"><span data-stu-id="cd180-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="cd180-256">"Oprávnění odepřeno" pomocí protokolu Forever Frame</span><span class="sxs-lookup"><span data-stu-id="cd180-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="cd180-257">Jedná se o známý problém popsaný [zde](https://github.com/SignalR/SignalR/issues/1963).</span><span class="sxs-lookup"><span data-stu-id="cd180-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="cd180-258">Tento příznak může být viděn pomocí nejnovější knihovny JQuery; Řešení je downgrade aplikace na JQuery 1.8.2.</span><span class="sxs-lookup"><span data-stu-id="cd180-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="cd180-259">Chyby kompilace a na straně serveru</span><span class="sxs-lookup"><span data-stu-id="cd180-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="cd180-260">Následující část obsahuje možná řešení chyby klienta a runtime na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="cd180-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="cd180-261">Odkaz na instanci Hub je null.</span><span class="sxs-lookup"><span data-stu-id="cd180-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="cd180-262">Vzhledem k tomu, že instance centra je vytvořenpro každé připojení, nelze vytvořit instanci rozbočovače ve vašem kódu sami.</span><span class="sxs-lookup"><span data-stu-id="cd180-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="cd180-263">Chcete-li volat metody na rozbočovači z mimo rozbočovačsám, najdete v [tématu Jak volat metody klienta a spravovat skupiny mimo hub třídy](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) jak získat odkaz na kontext rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="cd180-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="cd180-264">HTTPContext.Current.Session má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="cd180-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="cd180-265">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-265">This behavior is by design.</span></span> <span data-ttu-id="cd180-266">SignalR nepodporuje stav relace ASP.NET, protože povolení stavu relace by přerušilo oboustranné zasílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="cd180-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="cd180-267">Žádná vhodná metoda k přepsání</span><span class="sxs-lookup"><span data-stu-id="cd180-267">No suitable method to override</span></span>

<span data-ttu-id="cd180-268">Tato chyba se může zobrazit, pokud používáte kód ze starší dokumentace nebo blogů.</span><span class="sxs-lookup"><span data-stu-id="cd180-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="cd180-269">Ověřte, zda neodkazujete na názvy metod, které `OnConnectedAsync`byly změněny nebo zastaralé (například ).</span><span class="sxs-lookup"><span data-stu-id="cd180-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="cd180-270">Adresa HostContextExtensions.WebSocketServerUrl má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="cd180-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="cd180-271">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-271">This behavior is by design.</span></span> <span data-ttu-id="cd180-272">Tento člen je zastaralé a by neměl být používán.</span><span class="sxs-lookup"><span data-stu-id="cd180-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="cd180-273">Chyba "Trasa s názvem signalr.hubs" je již v kolekci tras.</span><span class="sxs-lookup"><span data-stu-id="cd180-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="cd180-274">Tato chyba se `MapHubs` zobrazí, pokud je volána dvakrát vaší aplikací.</span><span class="sxs-lookup"><span data-stu-id="cd180-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="cd180-275">Některé ukázkové `MapHubs` aplikace volají přímo v souboru globální aplikace; jiní volat v obálkové třídě.</span><span class="sxs-lookup"><span data-stu-id="cd180-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="cd180-276">Ujistěte se, že vaše aplikace neprovádí obojí.</span><span class="sxs-lookup"><span data-stu-id="cd180-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="cd180-277">Problémy s visual studio</span><span class="sxs-lookup"><span data-stu-id="cd180-277">Visual Studio issues</span></span>

<span data-ttu-id="cd180-278">Tato část popisuje problémy, ke kterým došlo v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd180-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="cd180-279">Uzel Dokumenty skriptu se v Průzkumníku řešení nezobrazuje</span><span class="sxs-lookup"><span data-stu-id="cd180-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="cd180-280">Některé z našich výukových programů vás nasměrují na uzel "Dokumenty skriptů" v Průzkumníku řešení při ladění.</span><span class="sxs-lookup"><span data-stu-id="cd180-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="cd180-281">Tento uzel je vytvořen ladicím programem JavaScript a zobrazí se pouze při ladění klientů prohlížeče v aplikaci Internet Explorer; pokud se používá Chrome nebo Firefox, uzel se nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="cd180-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="cd180-282">Ladicí program JavaScript také nebude spuštěn, pokud je spuštěn jiný ladicí program klienta, například ladicí program Silverlight.</span><span class="sxs-lookup"><span data-stu-id="cd180-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="cd180-283">SignalR nefunguje v sadě Visual Studio 2008 nebo starší</span><span class="sxs-lookup"><span data-stu-id="cd180-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="cd180-284">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="cd180-284">This behavior is by design.</span></span> <span data-ttu-id="cd180-285">SignalR vyžaduje rozhraní .NET Framework 4 nebo novější; to vyžaduje, aby aplikace SignalR byly vyvinuty v sadě Visual Studio 2010 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="cd180-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="cd180-286">Problémy se svis</span><span class="sxs-lookup"><span data-stu-id="cd180-286">IIS issues</span></span>

<span data-ttu-id="cd180-287">Tato část obsahuje problémy s Internetovou informační službou.</span><span class="sxs-lookup"><span data-stu-id="cd180-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="cd180-288">Web ováže po volání MapHubs</span><span class="sxs-lookup"><span data-stu-id="cd180-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="cd180-289">Tento problém byl opraven v nejnovější verzi SignalR.</span><span class="sxs-lookup"><span data-stu-id="cd180-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="cd180-290">Ověřte, zda používáte nejnovější vydanou verzi SignalR aktualizací instalace pomocí NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd180-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="cd180-291">Problémy s Azure</span><span class="sxs-lookup"><span data-stu-id="cd180-291">Azure issues</span></span>

<span data-ttu-id="cd180-292">Tato část obsahuje problémy s Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cd180-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="cd180-293">Zprávy nejsou přijímány prostřednictvím backplane Azure po změně názvů témat</span><span class="sxs-lookup"><span data-stu-id="cd180-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="cd180-294">Témata používaná propojovacím rozhraním Azure nejsou určena k konfiguraci uživatele.</span><span class="sxs-lookup"><span data-stu-id="cd180-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
