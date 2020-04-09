---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: Principy a zpracování událostí životnosti připojení v signalr | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento článek popisuje, jak používat události vystavené rozhraní API hubs.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676214"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>Principy a zpracování událostí doby platnosti v knihovně SignalR

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek obsahuje přehled signalr připojení, opětovné připojení a odpojení události, které můžete zpracovat a nastavení časového limitu a udržování naživu, které můžete nakonfigurovat.
>
> Článek předpokládá, že již máte nějaké znalosti SignalR a události životnosti připojení. Úvod do SignalR naleznete [v tématu Úvod do SignalR](../getting-started/introduction-to-signalr.md). Seznamy událostí životnosti připojení naleznete v následujících zdrojích:
>
> - [Jak zpracovat události životnosti připojení ve třídě Hub](hubs-api-guide-server.md#connectionlifetime)
> - [Jak zpracovat události životnosti připojení v klientech JavaScriptu](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [Jak zpracovat události životnosti připojení v klientech .NET](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
>
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento článek obsahuje následující části:

- [Terminologie a scénáře životnosti připojení](#terminology)

    - [SignalR připojení, přenosová spojení a fyzická spojení](#signalrvstransport)
    - [Scénáře odpojení přenosu](#transportdisconnect)
    - [Scénáře odpojení klienta](#clientdisconnect)
    - [Scénáře odpojení serveru](#serverdisconnect)
- [Nastavení časového limitu a udržování](#timeoutkeepalive)

    - [Connectiontimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [Keepalive](#keepalive)
    - [Jak změnit nastavení časového limitu a udržování](#changetimeout)
- [Jak upozornit uživatele na odpojení](#notifydisconnect)
- [Jak se neustále znovu připojit](#continuousreconnect)
- [Jak odpojit klienta v kódu serveru](#disconnectclientfromserver)
- [Zjištění důvodu odpojení](#detectingreasonfordisconnection)

Odkazy na referenční témata rozhraní API jsou na verzi rozhraní .NET 4.5 rozhraní API. Pokud používáte rozhraní .NET 4, přečtěte si [verzi rozhraní API .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Terminologie a scénáře životnosti připojení

Obslužná rutina `OnReconnected` události v `OnConnected` rozbočovači SignalR lze spustit přímo po, ale ne po `OnDisconnected` pro daného klienta. Důvod, proč můžete mít opětovné připojení bez odpojení je, že existuje několik způsobů, ve kterém slovo "připojení" se používá v SignalR.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR připojení, přenosová spojení a fyzická spojení

Tento článek bude rozlišovat mezi *signalr připojení*, *dopravní spojení*, a *fyzické spojení*:

- **SignalR připojení** odkazuje na logický vztah mezi klientem a adresu URL serveru, udržuje rozhraní API SignalR a jednoznačně identifikován id připojení. Data o tomto vztahu je udržována SignalR a slouží k navázání připojení přenosu. Vztah končí a SignalR disponuje data `Stop` při volání klienta metodu nebo časový limit je dosaženo při SignalR se pokouší obnovit ztracené připojení přenosu.
- **Přenos připojení** odkazuje na logický vztah mezi klientem a serverem, udržuje jeden ze čtyř rozhraní API přenosu: WebSockets, události odeslané serverem, forever frame nebo dlouhé dotazování. SignalR používá rozhraní API přenosu k vytvoření přenosového připojení a rozhraní API přenosu závisí na existenci fyzického síťového připojení k vytvoření přenosového připojení. Přenosové připojení končí, když signalr ukončí nebo když rozhraní API přenosu zjistí, že fyzické připojení je přerušeno.
- **Fyzické připojení** označuje fyzické síťové spojení – dráty, bezdrátové signály, směrovače atd., které usnadňují komunikaci mezi klientským počítačem a serverovým počítačem. Fyzické připojení musí být k dispozici pro navázání přenosového spojení a musí být navázáno přenosové spojení, aby bylo možné navázat spojení SignalR. Přerušení fyzické připojení však není vždy okamžitě ukončit připojení přenosu nebo signalr připojení, jak bude vysvětleno dále v tomto tématu.

V následujícím diagramu je připojení SignalR reprezentováno vrstvou Rozhraní API hubů a signalizačního centra persistentconnection api, přenosové připojení je reprezentováno vrstvou Transports a fyzické připojení je reprezentováno čarami mezi serverem a klienty.

![Diagram architektury SignalR](handling-connection-lifetime-events/_static/image1.png)

Při volání `Start` metody v klientovi SignalR poskytujete klientský kód SignalR se všemi informacemi, které potřebuje k navázání fyzického připojení k serveru. SignalR klientský kód používá tyto informace k vytvoření požadavku HTTP a navázání fyzického připojení, které používá jednu ze čtyř metod přenosu. Pokud se nezdaří přenosové připojení nebo selže server, připojení SignalR nezmizí okamžitě, protože klient má stále informace, které potřebuje k automatickému obnovení nového přenosového připojení ke stejné adrese URL SignalR. V tomto scénáři se nejedná o žádný zásah z uživatelské aplikace a když klientský kód SignalR vytvoří nové přenosové připojení, nespustí nové připojení SignalR. Kontinuita připojení SignalR se odráží v tom, že ID připojení, které je `Start` vytvořeno při volání metody, se nezmění.

Obslužná rutina `OnReconnected` události v centru se spustí, když je po ztrátě automaticky obnoveno přenosové připojení. Obslužná rutina `OnDisconnected` události se spustí na konci připojení SignalR. Připojení SignalR může skončit libovolným z následujících způsobů:

- Pokud klient volá `Stop` metodu, je na server odeslána zpráva stop a klient i server okamžitě ukončí připojení SignalR.
- Po ztrátě připojení mezi klientem a serverem se klient pokusí znovu připojit a server čeká na opětovné připojení klienta. Pokud jsou pokusy o opětovné připojení neúspěšné a časový limit odpojení končí, klient i server ukončí připojení SignalR. Klient se přestane pokoušet o opětovné připojení a server disponuje svou reprezentací připojení SignalR.
- Pokud klient zastaví spuštění bez nutnosti `Stop` volat metodu, server čeká na opětovné připojení klienta a poté ukončí připojení SignalR po uplynutí časového limitu odpojení.
- Pokud server přestane běžet, klient se pokusí znovu připojit (znovu vytvořit připojení přenosu) a potom ukončí připojení SignalR po uplynutí časového limitu odpojení.

Pokud nejsou žádné problémy s připojením a uživatelská `Stop` aplikace ukončí připojení SignalR voláním metody, signalr připojení a přenosové připojení začíná a končí přibližně ve stejnou dobu. Následující části popisují podrobněji další scénáře.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Scénáře odpojení přenosu

Fyzická připojení mohou být pomalá nebo může dojít k přerušení připojení. V závislosti na faktorech, jako je délka přerušení, může dojít k přerušení přenosového spojení. SignalR se pak pokusí obnovit přenosové spojení. Někdy rozhraní API připojení přenosu zjistí přerušení a klesne přenosové připojení a SignalR okamžitě zjistí, že připojení je ztraceno. V jiných scénářích ani rozhraní API připojení přenosu ani SignalR se dozví okamžitě, že došlo ke ztrátě připojení. Pro všechny přenosy s výjimkou dlouhé dotazování klient SignalR používá funkci s názvem *keepalive* ke kontrole ztráty připojení, které rozhraní API přenosu není schopen zjistit. Informace o připojení dlouhé dotazování, naleznete [v tématu timeout a keepalive nastavení](#timeoutkeepalive) dále v tomto tématu.

Pokud je připojení neaktivní, server pravidelně odesílá klientovi paket keepalive. K datu, kdy je tento článek zapsán, je výchozí frekvence každých 10 sekund. Nasloucháním pro tyto pakety, klienti mohou zjistit, pokud došlo k potížím s připojením. Pokud keepalive paket není přijat, pokud je očekáván, po krátké době klient předpokládá, že existují problémy s připojením, jako je pomalost nebo přerušení. Pokud keepalive stále není přijat po delší době, klient předpokládá, že připojení bylo vynecháno a začne se pokouší znovu připojit.

Následující diagram znázorňuje události klienta a serveru, které jsou vyvolány v typickém scénáři, když existují problémy s fyzickým připojením, které nejsou okamžitě rozpoznány rozhraním API přenosu. Diagram se vztahuje na následující okolnosti:

- Přenos je WebSockets, forever frame nebo události odeslané serverem.
- Existují různá období přerušení fyzického síťového připojení.
- Rozhraní API přenosu nezjistí přerušení, takže SignalR spoléhá na keepalive funkce k jejich zjištění.

![Dopravní odpojení](handling-connection-lifetime-events/_static/image2.png)

Pokud klient přejde do režimu opětovného připojení, ale nemůže navázat přenosové připojení v rámci limitu časového limitu odpojení, server ukončí připojení SignalR. V takovém případě server spustí `OnDisconnected` metodu centra a zařadí zprávu o odpojení, která se odešle klientovi v případě, že se klientu podaří připojit později. Pokud se klient pak znovu připojí, přijme příkaz `Stop` odpojení a zavolá metodu. V tomto `OnReconnected` scénáři není spuštěna při opětovném `OnDisconnected` připojení klienta a `Stop`není spuštěnpři volání klienta . Následující diagram znázorňuje tento scénář.

![Přerušení přenosu – časový čas serveru](handling-connection-lifetime-events/_static/image3.png)

Události životnosti připojení SignalR, které mohou být vyvolány na straně klienta jsou následující:

- `ConnectionSlow`událost klienta.

    Je aktivována, když přednastavená část časového limitu keepalive uplynula od poslední zprávy nebo příkazping keepalive byl přijat. Výchozí doba upozornění časového limitu keepalive je 2/3 časového limitu keepalive. Časový limit keepalive je 20 sekund, takže k upozornění dojde přibližně 13 sekund.

    Ve výchozím nastavení server odesílá příkazy ping keepalive každých 10 sekund a klient kontroluje příkazy ping keepalive přibližně každé 2 sekundy (jedna třetina rozdílu mezi hodnotou časového limitu keepalive a hodnotou upozornění časového limitu keepalive).

    Pokud rozhraní API přenosu zjistí odpojení, SignalR může být informován o odpojení před keepalive časový limit období upozornění přejde. V takovém případě `ConnectionSlow` by událost nebyla vyvolána a SignalR by přejít přímo na `Reconnecting` událost.
- `Reconnecting`událost klienta.

    Vyvolána, když (a) rozhraní API přenosu zjistí, že dojde ke ztrátě připojení nebo (b) keepalive časový limit uplynul od poslední zprávy nebo keepalive ping byla přijata. SignalR klientský kód začne se pokouší znovu připojit. Tuto událost můžete zpracovat, pokud chcete, aby aplikace provést určitou akci při ztrátě připojení přenosu. Výchozí časový limit keepalive je aktuálně 20 sekund.

    Pokud se váš klientský kód pokusí volat metodu Hub, zatímco SignalR je v režimu opětovného připojení, SignalR se pokusí odeslat příkaz. Většinou se takové pokusy nezdaří, ale za určitých okolností by mohly uspět. Pro události odeslané serverem, forever frame a dlouhé přenosy dotazování SignalR používá dva komunikační kanály, jeden, který klient používá k odesílání zpráv a jeden, který používá pro příjem zpráv. Kanál používaný pro příjem je trvale otevřený, a to je ten, který je uzavřen při přerušení fyzického připojení. Kanál používaný pro odesílání zůstane k dispozici, takže pokud je obnoveno fyzické připojení, volání metody z klienta na server může být úspěšné před obnovením kanálu příjmu. Vrácená hodnota nebude přijata, dokud SignalR znovu neotevře kanál používaný pro příjem.
- `Reconnected`událost klienta.

    Je aktivována při obnovení připojení přenosu. Obslužná rutina `OnReconnected` události v centru se spustí.
- `Closed`klientská`disconnected` událost (událost v JavaScriptu).

    Vyvolána při vypršení časového limitu odpojení, zatímco signalr klientský kód se pokouší znovu připojit po ztrátě připojení přenosu. Výchozí časový limit odpojení je 30 sekund. (Tato událost je také vyvolána `Stop` při ukončení připojení, protože je volána metoda.)

Přerušení přenosu připojení, které nejsou zjištěny rozhraní API přenosu a nezpozdit příjem udržování ping ze serveru po dobu delší, než keepalive časový limit období upozornění období nemusí způsobit žádné události životnosti připojení, které mají být vyvolány.

Některá síťová prostředí záměrně uzavírají nečinné připojení a další funkcí paketů keepalive je zabránit tomu tím, že tyto sítě budou vědět, že je používáno připojení SignalR. V extrémních případech nemusí výchozí frekvence udržování ping nestačí k zabránění uzavřeným připojením. V takovém případě můžete nakonfigurovat keepalive ping, který má být odesílán častěji. Další informace naleznete v [tématu Timeout and keepalive nastavení](#timeoutkeepalive) dále v tomto tématu.

> [!NOTE]
>
> **Důležité:** Sled událostí popsaných zde není zaručena. SignalR provádí každý pokus o zvýšení události životnosti připojení předvídatelným způsobem podle tohoto schématu, ale existuje mnoho variant síťových událostí a mnoho způsobů, ve kterém základní komunikační architektury, jako je například rozhraní API přenosu jejich zpracování. Například `Reconnected` událost nemusí být vyvolána při opětovném připojení `OnConnected` klienta nebo obslužná rutina na serveru může být spuštěna, když je pokus o navázání připojení neúspěšný. Toto téma popisuje pouze účinky, které by za normálních okolností vznikly určitými typickými okolnostmi.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>Scénáře odpojení klienta

V klientovi prohlížeče je klientský kód SignalR, který udržuje připojení SignalR, spuštěn v kontextu JavaScriptu webové stránky. To je důvod, proč signalr připojení musí skončit, když přejdete z jedné stránky na druhou, a to je důvod, proč máte více připojení s více ID připojení, pokud se připojíte z více oken prohlížeče nebo karty. Když uživatel zavře okno prohlížeče nebo kartu nebo přejde na novou stránku nebo aktualizuje stránku, signalr připojení okamžitě ukončí, protože `Stop` SignalR klientský kód zpracovává, že prohlížeč událost pro vás a volá metodu. V těchto scénářích nebo v libovolné platformě klienta, když vaše aplikace `Stop` volá metodu, obslužná rutina `OnDisconnected` události se spustí okamžitě na serveru a klient vyvolá `Closed` událost (událost je pojmenována `disconnected` v Jazyce JavaScript).

Pokud klientská aplikace nebo počítač, který je spuštěn na selhání nebo přejde do režimu spánku (například když uživatel zavře přenosný počítač), server není informován o tom, co se stalo. Pokud server ví, ztráta klienta může být způsobena přerušením připojení a klient se může pokoušet znovu připojit. Proto v těchto scénářích server čeká dát klientovi možnost `OnDisconnected` znovu připojit a neprovede, dokud vyprší časový limit odpojení (přibližně 30 sekund ve výchozím nastavení). Následující diagram znázorňuje tento scénář.

![Selhání klientského počítače](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Scénáře odpojení serveru

Když server přejde do režimu offline – restartuje se, selže, doména aplikace recykluje atd. `ConnectionSlow` Pokud klient přejde do režimu opětovného připojení a server se obnoví nebo restartuje nebo nový server přejde do režimu online před vypršením časového limitu odpojení, klient se znovu připojí k obnovenému nebo novému serveru. V takovém případě signalr připojení pokračuje na `Reconnected` straně klienta a je vyvolána událost. Na prvním serveru, `OnDisconnected` je nikdy spuštěn a na `OnReconnected` novém serveru, je spuštěn, i když `OnConnected` nebyl nikdy proveden pro tohoto klienta na tomto serveru dříve. (Efekt je stejný, pokud se klient po restartování nebo recyklaci domény aplikace znovu připojí ke stejnému serveru, protože při restartování serveru nemá paměť na předchozí aktivitu připojení.) Následující diagram předpokládá, že rozhraní API přenosu se okamžitě `ConnectionSlow` dozví o ztracené připojení, takže událost není vyvolána.

![Selhání serveru a opětovné připojení](handling-connection-lifetime-events/_static/image5.png)

Pokud server není k dispozici v období časového limitu odpojení, připojení SignalR končí. V tomto scénáři `Closed` `disconnected` událost (v klientech JavaScript) `OnDisconnected` je vyvolána na straně klienta, ale nikdy volá na serveru. Následující diagram předpokládá, že rozhraní API přenosu nezjistí ztracené připojení, takže je zjištěna funkce `ConnectionSlow` keepalive SignalR a je vyvolána událost.

![Selhání serveru a časový čas](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Nastavení časového limitu a udržování

Výchozí `ConnectionTimeout`, `DisconnectTimeout`a `KeepAlive` hodnoty jsou vhodné pro většinu scénářů, ale lze změnit, pokud vaše prostředí má zvláštní potřeby. Například pokud vaše síťové prostředí zavře připojení, které jsou nečinné po dobu 5 sekund, bude pravděpodobně muset snížit keepalive hodnotu.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>Connectiontimeout

Toto nastavení představuje dobu, po kterou má být přenosové připojení otevřené a čeká se na odpověď před jeho zavřením a otevřením nového připojení. Výchozí hodnota je 110 sekund.

Toto nastavení platí pouze v případě, že je zakázána funkce keepalive, která se obvykle vztahuje pouze na přenos dlouhé dotazování. Následující diagram znázorňuje vliv tohoto nastavení na dlouhé připojení přenosu dotazování.

![Přenosové připojení s dlouhým dotazem](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

Toto nastavení představuje dobu čekání po ztrátě připojení `Disconnected` přenosu před vyvoláním události. Výchozí hodnota je 30 sekund. Když nastavíte `DisconnectTimeout`, `KeepAlive` je automaticky nastavena na `DisconnectTimeout` 1/3 hodnoty.

<a id="keepalive"></a>

### <a name="keepalive"></a>Keepalive

Toto nastavení představuje dobu čekání před odesláním paketu keepalive přes nečinné připojení. Výchozí hodnota je 10 sekund. Tato hodnota nesmí být větší než `DisconnectTimeout` 1/3 hodnoty.

Chcete-li nastavit `DisconnectTimeout` obě `KeepAlive`a `KeepAlive` `DisconnectTimeout`, nastavte po . V `KeepAlive` opačném případě bude `DisconnectTimeout` vaše `KeepAlive` nastavení přepsáno, když se automaticky nastaví na 1/3 hodnoty časového času.

Pokud chcete zakázat keepalive funkce, nastavte `KeepAlive` na hodnotu null. Funkce keepalive je automaticky zakázána pro přenos dlouhé dotazování.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Jak změnit nastavení časového limitu a udržování

Chcete-li změnit výchozí hodnoty pro `Application_Start` tato nastavení, nastavte je v souboru *Global.asax,* jak je znázorněno v následujícím příkladu. Hodnoty zobrazené v ukázkovém kódu jsou stejné jako výchozí hodnoty.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Jak upozornit uživatele na odpojení

V některých aplikacích můžete chtít zobrazit zprávu uživateli, pokud jsou problémy s připojením. Máte několik možností, jak a kdy to udělat. Následující ukázky kódu jsou určeny pro klienta JavaScriptpomocí generovaného proxy serveru.

- Zpracování `connectionSlow` události zobrazíte zprávu, jakmile SignalR je vědomi problémů s připojením, před přejde do režimu opětovného připojení.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- Zpracování `reconnecting` události zobrazíte zprávu, když SignalR si je vědoma odpojení a přejde do režimu opětovného připojení.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Zpracování `disconnected` události zobrazíte zprávu, když časový čas pokusu o opětovné připojení. V tomto scénáři jediný způsob, jak obnovit připojení se serverem znovu je `Start` restartování připojení SignalR voláním metody, která vytvoří nové ID připojení. Následující ukázka kódu používá příznak k ujistěte se, že vydáte oznámení pouze po obnovení časového limitu, `Stop` nikoli po normální konec připojení SignalR způsobené voláním metody.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Jak se neustále znovu připojit

V některých aplikacích můžete chtít automaticky obnovit připojení po jeho ztrátě a vypršel časový limit pokusu o opětovné připojení. Chcete-li to provést, `Start` můžete `Closed` volat metodu z obslužné rutiny události (obslužná`disconnected` rutina události v klientech JavaScriptu). Můžete chtít počkat určitou dobu `Start` před voláním, aby se zabránilo tomu příliš často, když server nebo fyzické připojení nejsou k dispozici. Následující ukázka kódu je pro klienta JavaScript pomocí generovaného proxy serveru.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Potenciální problém, který je třeba si uvědomit v mobilních klientech, je, že pokusy o nepřetržité opětovné připojení, pokud není k dispozici server nebo fyzické připojení, mohou způsobit zbytečné vybití baterie.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Jak odpojit klienta v kódu serveru

SignalR verze 2 nemá integrované rozhraní API serveru pro odpojení klientů. Existují [plány pro přidání této funkce v budoucnu](https://github.com/SignalR/SignalR/issues/2101). V aktuální verzi SignalR nejjednodušší způsob, jak odpojit klienta od serveru je implementovat metodu odpojení na straně klienta a volat tuto metodu ze serveru. Následující ukázka kódu ukazuje metodu odpojení pro klienta JavaScriptu pomocí generovaného proxy serveru.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Zabezpečení – ani tato metoda pro odpojení klientů, ani navrhované integrované rozhraní API se bude zabývat scénářem napadených klientů, kteří `stopClient` používají škodlivý kód, protože klienti se mohou znovu připojit nebo hacknutý kód může metodu odebrat nebo změnit jeho pravost. Vhodné místo pro implementaci stavové ochrany typu denial-of-service (DOS) není v rámci nebo ve vrstvě serveru, ale spíše v infrastruktuře front-endu.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>Zjištění důvodu odpojení

SignalR 2.1 přidá přetížení `OnDisconnect` události serveru, který označuje, pokud klient záměrně odpojenspíše než vypršení časového limitu. Parametr `StopCalled` je true, pokud klient explicitně ukončil připojení. Pokud v jazyce JavaScript chyba serveru vedla klienta k odpojení, `$.connection.hub.lastError`budou informace o chybě předány klientovi jako .

**Kód serveru C# : `stopCalled` parametr**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript klientský kód: přístup `lastError` v `disconnect` události.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
