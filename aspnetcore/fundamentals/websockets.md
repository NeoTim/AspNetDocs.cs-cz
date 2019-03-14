---
title: Webové sockety v ASP.NET Core
author: rick-anderson
description: Zjistěte, jak začít pracovat s objekty Websocket v ASP.NET Core.
monikerRange: '>= aspnetcore-1.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/17/2019
uid: fundamentals/websockets
ms.openlocfilehash: 76acb9c96ed5e8bbbaf39eeb6cb23307bb44fb8d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068035"
---
# <a name="websockets-support-in-aspnet-core"></a>Webové sockety v ASP.NET Core

Podle [Petr Dykstra](https://github.com/tdykstra) a [Andrew Stanton sestry](https://github.com/anurse)

Tento článek vysvětluje, jak začít pracovat s objekty Websocket v ASP.NET Core. [Protokol WebSocket](https://wikipedia.org/wiki/WebSocket) ([RFC 6455](https://tools.ietf.org/html/rfc6455)) je protokol, který umožňuje obousměrný trvalé komunikačních kanálů přes připojení TCP. Používá se v aplikacích, které využívají samosprávné komunikace rychlé, v reálném čase, jako jsou konverzace, řídicí panel a herních aplikací.

[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples) ([stažení](xref:index#how-to-download-a-sample)). Zobrazit [další kroky](#next-steps) části Další informace.

## <a name="prerequisites"></a>Požadavky

* ASP.NET Core 1.1 nebo vyšší
* Libovolný operační systém, který podporuje ASP.NET Core:
  
  * Windows 7 / Windows Server 2008 nebo novější
  * Linux
  * macOS
  
* Pokud aplikace běží na Windows se službou IIS:

  * Windows 8 nebo Windows Server 2012 nebo novější
  * IIS 8 / IIS 8 Express
  * Musí být povolené protokoly Websocket (najdete v článku [podpora služby IIS/IIS Express](#iisiis-express-support) části.).
  
* Pokud aplikace běží na [HTTP.sys](xref:fundamentals/servers/httpsys):

  * Windows 8 nebo Windows Server 2012 nebo novější

* Podporované prohlížeče, naleznete v tématu https://caniuse.com/#feat=websockets.

## <a name="when-to-use-websockets"></a>Kdy použít objekty Websocket

Použijte pracovat přímo s připojení soketu Websocket. Například můžete použijte objekty Websocket pro zajištění nejlepšího možného výkonu s hry v reálném čase.

[Funkce SignalR technologie ASP.NET Core](xref:signalr/introduction) je knihovna, která zjednodušuje přidávání funkce webu v reálném čase do aplikací. Používá objekty Websocket, kdykoli je to možné.

## <a name="how-to-use-websockets"></a>Jak používat objekty Websocket

* Nainstalujte [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) balíčku.
* Nakonfigurujte middleware.
* Přijímal požadavky protokolu WebSocket.
* Odesílání a příjem zpráv.

### <a name="configure-the-middleware"></a>Nakonfigurujte middleware

Přidat objekty Websocket middlewaru v `Configure` metodu `Startup` třídy:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSockets)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=UseWebSockets)]

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Můžete nakonfigurovat následující nastavení:

* `KeepAliveInterval` – Jak často k odesílání rámců "příkaz ping" ke klientovi, aby proxy servery udržení připojení otevřeného. Výchozí hodnota je dvě minuty.
* `ReceiveBufferSize` – Velikost vyrovnávací paměti používané přijímat data. Pokročilí uživatelé může být nutné změnit to pro optimalizace na základě velikosti dat výkonu. Výchozí hodnota je 4 KB.

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

Můžete nakonfigurovat následující nastavení:

* `KeepAliveInterval` – Jak často k odesílání rámců "příkaz ping" ke klientovi, aby proxy servery udržení připojení otevřeného. Výchozí hodnota je dvě minuty.
* `ReceiveBufferSize` – Velikost vyrovnávací paměti používané přijímat data. Pokročilí uživatelé může být nutné změnit to pro optimalizace na základě velikosti dat výkonu. Výchozí hodnota je 4 KB.
* `AllowedOrigins` – Seznam povolených hodnot hlavičky Origin pro požadavky protokolu WebSocket. Ve výchozím nastavení jsou povoleny všechny původy. Podrobnosti najdete v části "Omezení objektu websocket na straně zdroje" níže.

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptions)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptions)]

::: moniker-end

### <a name="accept-websocket-requests"></a>Přijímal požadavky protokolu WebSocket

Někde dále v cyklu požadavku (dále v `Configure` metoda nebo akce MVC, například) zkontrolujte, jestli je požadavek protokolu WebSocket a přijmout požadavek protokolu WebSocket.

Následující příklad je z později v `Configure` metody:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=AcceptWebSocket&highlight=7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=AcceptWebSocket&highlight=7)]

::: moniker-end

Požadavek protokolu WebSocket může dojít na libovolnou adresu URL, ale tento vzorový kód přijímá jenom žádosti o `/ws`.

### <a name="send-and-receive-messages"></a>Odesílání a příjem zpráv

`AcceptWebSocketAsync` Metoda upgraduje na připojení soketu websocket bylo připojení TCP a poskytuje [protokolu WebSocket](/dotnet/core/api/system.net.websockets.websocket) objektu. Použití `WebSocket` objektu pro odesílání a příjem zpráv.

Předá kódu uvedeného výše, který přijme žádost protokolu WebSocket `WebSocket` objektu `Echo` metody. Kód přijme zprávu a okamžitě odešle zpět stejné zprávy. Zprávy jsou odeslané a přijaté ve smyčce, dokud klient ukončí připojení:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=Echo)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=Echo)]

::: moniker-end

Při přijímání připojení soketu websocket bylo před zahájením smyčky, middleware kanálu se ukončí. Po zavření soketu, unwinds kanálu. To znamená požadavek se zastaví v budoucnu v kanálu při přijetí objekt WebSocket. Když je smyčka dokončena, je uzavřený soket žádost pokračuje zálohování kanálu.

::: moniker range=">= aspnetcore-2.2"

### <a name="handle-client-disconnects"></a>Odpojení popisovač klienta

Server není informována automaticky, když se klient odpojí z důvodu ztráty připojení. Server přijme zprávu o odpojení, pouze pokud klient odešle, nejde provést, pokud dojde ke ztrátě připojení k Internetu. Pokud chcete provést určitou akci, pokud k tomu dojde, nastavte vypršení časového limitu po nic je přijatou od klienta v rámci určité časové okno.

Pokud klient není vždy zasílání zpráv a nechcete konec časového limitu připojení pouze z důvodu nepovede nečinné připojení, mají klienta pomocí časovače odešlete zprávu ping každých X sekund. Na serveru, pokud nebyla zpráva dorazila do 2\*X sekund po předchozí, ukončit připojení a hlásí, že klient byl odpojen. Počkejte, až dvakrát předpokládaného časového intervalu ponechte další čas zpoždění v síti, které mohou zdržet na zprávu ping.

### <a name="websocket-origin-restriction"></a>Omezení objektu websocket na straně zdroje

Poskytovanou CORS se nevztahují na objekty Websocket. Prohlížeče **není**:

* Provedení přípravné požadavků CORS.
* Respektujeme zadaná v omezení `Access-Control` záhlaví při provádění požadavků protokolu WebSocket.

Ale prohlížeče odesílají `Origin` záhlaví při vydávání žádostí protokolu WebSocket. Aplikace musí být nakonfigurovaný k ověření tyto hlavičky k zajištění, že jsou povoleny pouze objekty Websocket očekávané původ, odkud pocházejí.

Pokud váš server hostuješ na "https://server.com"a hostování vašeho klienta na"https://client.com", přidejte "https://client.com" k `AllowedOrigins` seznamu pro objekty Websocket ověření.

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptionsAO&highlight=6-7)]

> [!NOTE]
> `Origin` Záhlaví je řízena klientem a stejně jako `Referer` záhlaví, můžete zfalšovaná. Proveďte **není** používají tyto hlavičky jako mechanismus ověřování.

::: moniker-end

## <a name="iisiis-express-support"></a>Podpora služby IIS/IIS Express

Windows Server 2012 nebo novější a Windows 8 nebo novější s služby IIS/IIS Express 8 nebo novější obsahuje podporu protokolu WebSocket.

> [!NOTE]
> Při použití IIS Expressu, jsou vždy povoleny protokoly Websocket.

### <a name="enabling-websockets-on-iis"></a>Povolení ve službě IIS WebSockets

Pokud chcete povolit podporu protokolu WebSocket ve Windows serveru 2012 nebo novější:

> [!NOTE]
> Tyto kroky se nevyžadují, při použití IIS Expressu

1. Použití **přidat role a funkce** z průvodce **spravovat** nabídky nebo na odkaz v **správce serveru**.
1. Vyberte **instalace na základě rolí nebo na základě funkcí**. Vyberte **Další**.
1. Vyberte příslušný server (ve výchozím nastavení je vybraný místní server). Vyberte **Další**.
1. Rozbalte **webového serveru (IIS)** v **role** stromu, rozbalte **Webový Server**a potom rozbalte **vývoj aplikací**.
1. Vyberte **protokol WebSocket**. Vyberte **Další**.
1. Pokud nejsou potřebné další funkce, vyberte **Další**.
1. Vyberte **Install** (Nainstalovat).
1. Po dokončení instalace, vybrat **Zavřít** ukončíte průvodce.

Pokud chcete povolit podporu protokolu WebSocket v systému Windows 8 nebo novější:

> [!NOTE]
> Tyto kroky se nevyžadují, při použití IIS Expressu

1. Přejděte do **ovládací panely** > **programy** > **programy a funkce** > **zapnout Windows funkce na nebo vypnout** (levé straně obrazovky).
1. Otevřete následující uzly: **Internetová informační služba** > **webové služby** > **funkce pro vývoj aplikací**.
1. Vyberte **protokol WebSocket** funkce. Vyberte **OK**.

### <a name="disable-websocket-when-using-socketio-on-nodejs"></a>Zakázat protokol WebSocket, když v Node.js pomocí socket.io

Pokud používáte podpora protokolu WebSocket v [socket.io](https://socket.io/) na [Node.js](https://nodejs.org/), zakázat pomocí modul WebSocket služby IIS výchozí `webSocket` element v *web.config* nebo *applicationHost.config*. Pokud není tento krok provést, modul WebSocket služby IIS se pokusí se zpracovat komunikaci pomocí protokolu WebSocket spíše než Node.js a aplikace.

```xml
<system.webServer>
  <webSocket enabled="false" />
</system.webServer>
```

## <a name="next-steps"></a>Další kroky

[Ukázkovou aplikaci](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples) , který doprovází tento článek je odezvu aplikace. Obsahuje webovou stránku, která umožňuje připojení pomocí protokolu WebSocket, a server odešle všechny zprávy, které obdrží zpět do klienta. Spustit z příkazového řádku (ne zřídila pro spuštění ze sady Visual Studio službou IIS Express) a přejděte do http://localhost:5000. Webové stránky zobrazí v levém horním rohu stav připojení:

![Počáteční stav webové stránky](websockets/_static/start.png)

Vyberte **připojit** na adresu URL odeslat požadavek protokolu WebSocket. Zadejte testovací zprávu a vybrat **odeslat**. Až budete hotovi, vyberte **zavřít soketu**. **Komunikace protokolu** části sestavy každý otevřený, odesílání a akce při zavření jako to se stane.

![Počáteční stav webové stránky](websockets/_static/end.png)
