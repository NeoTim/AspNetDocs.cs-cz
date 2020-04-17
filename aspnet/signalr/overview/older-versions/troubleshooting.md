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
# <a name="signalr-troubleshooting-signalr-1x"></a>Řešení potíží s knihovnou SignalR (SignalR 1.x)

podle [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument popisuje běžné problémy s řešením potíží se signálem SignalR.

Tento dokument obsahuje následující části.

- [Volající metody mezi klientem a serverem tiše se nezdaří](#connection)
- [Další problémy s připojením](#other)
- [Chyby kompilace a na straně serveru](#server)
- [Problémy s visual studio](#vs)
- [Problémy s Internetovou informační službou](#iis)
- [Problémy s Azure](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>Volající metody mezi klientem a serverem tiše se nezdaří

Tato část popisuje možné příčiny volání metody mezi klientem a serverem nezdaří bez smysluplné chybové zprávy. V aplikaci SignalR server nemá žádné informace o metodách, které klient implementuje; Když server vyvolá metodu klienta, jsou klientovi odeslána data názvu metody a parametru a metoda je spuštěna pouze v případě, že existuje ve formátu, který server zadal. Pokud není v klientovi nalezena žádná odpovídající metoda, nic se nestane a na serveru není vyvolána žádná chybová zpráva.

Chcete-li dále zkoumat klientské metody, které nejsou volány, můžete zapnout protokolování před voláním metody start v centru a zjistit, jaká volání přicházejí ze serveru. Informace o povolení protokolování v aplikaci JavaScript naleznete v tématu [Jak povolit protokolování na straně klienta (verze klienta JavaScriptu).](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging) Informace o povolení protokolování klientské aplikace .NET naleznete v tématu [Jak povolit protokolování na straně klienta (verze klienta.NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Chybně napsaná metoda, nesprávný podpis metody nebo nesprávný název rozbočovače

Pokud název nebo podpis volané metody přesně neodpovídá vhodné metodě na straně klienta, volání se nezdaří. Ověřte, zda název metody volaný serverem odpovídá názvu metody v klientovi. SignalR také vytvoří proxy centra pomocí camel-cased metody, jak je vhodné `SendMessage` v Jazyce `sendMessage` JavaScript, takže metoda volaná na serveru by být volána v proxy klienta. Pokud použijete `HubName` atribut v kódu na straně serveru, ověřte, zda použitý název odpovídá názvu použitému k vytvoření centra v klientovi. Pokud `HubName` atribut nepoužíváte, ověřte, zda je název centra v klientovi JavaScriptu camel-cased, například chatHub místo ChatHub.

### <a name="duplicate-method-name-on-client"></a>Duplicitní název metody v klientovi

Ověřte, zda nemáte duplicitní metodu v klientovi, která se liší pouze případ. Pokud má klientská aplikace `sendMessage`metodu nazývanou , `SendMessage` ověřte, zda není také volána metoda.

### <a name="missing-json-parser-on-the-client"></a>Chybějící analyzátor JSON na straně klienta

SignalR vyžaduje Analyzátor JSON být přítomen serializovat volání mezi serverem a klientem. Pokud váš klient nemá předdefinovaný analyzátor JSON (například Internet Explorer 7), budete ho muset do aplikace zahrnout. Můžete si stáhnout Analyzátor JSON [zde](http://nuget.org/packages/json2).

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Míchání centra a syntaxe trvalého připojení

SignalR používá dva modely komunikace: Rozbočovače a PersistentConnections. Syntaxe pro volání těchto dvou komunikačních modelů se liší v kódu klienta. Pokud jste do kódu serveru přidali rozbočovač, ověřte, že veškerý klientský kód používá správnou syntaxi rozbočovače.

**Klientský kód JavaScriptu, který vytváří trvalé připojení v klientovi JavaScriptu**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Klientský kód JavaScriptu, který vytvoří hubproxy v klientovi Javascriptu**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**Kód serveru Jazyka C#, který mapuje trasu na trvalé připojení**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**Kód serveru C#, který mapuje trasu do centra nebo na více rozbočovačů, pokud máte více aplikací**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>Připojení bylo spuštěno před přidáním předplatných.

Pokud je připojení centra spuštěno před tím, než jsou do proxy serveru přidány metody, které lze volat ze serveru, nebudou zprávy přijaty. Následující kód Jazyka JavaScript nespustí rozbočovač správně:

**Nesprávný kód klienta javascriptu, který neumožňuje přijímat zprávy hubů**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Místo toho přidejte před voláním předvolání metody Start:

**Klientský kód JavaScriptu, který správně přidává odběry do rozbočovače**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Chybějící název metody v serveru proxy centra

Ověřte, zda je metoda definovaná na serveru přihlášena k odběru v klientovi. I když server definuje metodu, musí být stále přidána do proxy serveru klienta. Metody lze přidat do proxy klienta následujícími způsoby (Všimněte si, že metoda je přidána do `client` člena rozbočovače, nikoli přímo do rozbočovače):

**Klientský kód JavaScriptu, který přidává metody do proxy centra**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Metody rozbočovače nebo rozbočovače, které nejsou deklarovány jako veřejné

Chcete-li být viditelné na straně klienta, `public`musí být deklarována implementace centra a metody jako .

### <a name="accessing-hub-from-a-different-application"></a>Přístup k rozbočovači z jiné aplikace

SignalR Rozbočovače lze přistupovat pouze prostřednictvím aplikací, které implementují klienty SignalR. SignalR nelze spolupracovat s jinými komunikačními knihovnami (například SOAP nebo WCF webové služby.) Pokud není pro cílovou platformu k dispozici žádný klient SignalR, nelze získat přímý přístup ke koncovému bodu serveru.

### <a name="manually-serializing-data"></a>Ruční serializace dat

SignalR bude automaticky používat JSON serializovat parametry metody- není třeba to udělat sami.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Metoda vzdáleného rozbočovače nebyla spuštěna na straně klienta ve funkci OnDisconnected

Toto chování je záměrné. Při `OnDisconnected` volání rozbočovač již `Disconnected` vstoupil do stavu, který neumožňuje další metody rozbočovače, které mají být volány.

**Kód serveru Jazyka C#, který správně spustí kód v události OnDisconnected**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>Bylo dosaženo limitu připojení.

Při použití plné verze služby IIS v klientském operačním systému, jako je windows 7, je uložen limit připojení 10. Při použití klientského operačního operačního příkazu se tomuto limitu vyhněte pomocí služby IIS Express.

### <a name="cross-domain-connection-not-set-up-properly"></a>Připojení mezi doménami není správně nastaveno

Pokud připojení mezi doménami (připojení, pro které adresa URL signalru není ve stejné doméně jako hostitelská stránka) není správně nastaveno, může dojít k selhání připojení bez chybové zprávy. Informace o povolení komunikace mezi doménami naleznete v [tématu Jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>Připojení pomocí ntlm (Active Directory) nefunguje v klientovi .NET

Připojení v klientské aplikaci .NET, která používá zabezpečení domény, může selhat, pokud připojení není správně nakonfigurováno. Chcete-li použít SignalR v prostředí domény, nastavte vlastnost potřebného připojení takto:

**Kód klienta jazyka C#, který implementuje pověření připojení**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>Další problémy s připojením

Tato část popisuje příčiny a řešení pro konkrétní příznaky nebo chybové zprávy, ke kterým dochází během připojení.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>Před odesláním dat je nutné volat začátek.

Tato chyba se běžně zobrazuje, pokud kód odkazuje na objekty SignalR před spuštěním připojení. Po dokončení připojení musí být přidány metody definované na serveru. Všimněte si, `Start` že volání je asynchronní, takže kód po volání může být proveden před jeho dokončením. Nejlepší způsob, jak přidat obslužné rutiny po úplném spuštění připojení je umístit do funkce zpětného volání, která je předána jako parametr metody start:

**Kód klienta JavaScriptu, který správně přidává obslužné rutiny událostí, které odkazují na objekty SignalR**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Tato chyba se také zobrazí, pokud se připojení zastaví, zatímco signalr objekty jsou stále odkazuje.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>Chyba "301 Trvale přesunuta" nebo "302 přesunuta dočasně"

Tato chyba může být vidět, pokud projekt obsahuje složku s názvem SignalR, který bude zasahovat do automaticky vytvořené proxy. Chcete-li se této chybě vyhnout, nepoužívejte složku volanou `SignalR` v aplikaci ani nezapněte automatické generování proxy serveru. Další podrobnosti najdete [v tématu Vygenerovaný proxy server a to, co pro vás dělá.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>Chyba "403 Zakázáno" v klientovi .NET nebo Silverlight

K této chybě může dojít v prostředích mezi doménami, kde není správně povolena komunikace mezi doménami. Informace o povolení komunikace mezi doménami naleznete v [tématu Jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Chcete-li vytvořit připojení mezi doménami v klientovi Silverlight, přečtěte [si informace o připojení mezi doménami z klientů Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>Chyba "404 nebyla nalezena"

Existuje několik příčin tohoto problému. Ověřte všechny následující skutečnosti:

- **Odkaz na adresu proxy centra není správně formátován:** Tato chyba je běžně vidět, pokud odkaz na vygenerovanou adresu proxy centra není správně formátován. Ověřte, zda je správně nastaven odkaz na adresu centra. Podrobnosti naleznete [v tématu Jak odkazovat na dynamicky generovaný proxy server.](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)
- **Přidání tras do aplikace před přidáním trasy rozbočovače:** Pokud aplikace používá jiné trasy, ověřte, zda `MapHubs`je první přidanou trasou volání aplikace .

### <a name="500-internal-server-error"></a>"Chyba interního serveru 500"

Jedná se o velmi obecnou chybu, která může mít širokou škálu příčin. Podrobnosti o chybě by se měly objevit v protokolu událostí serveru nebo lze nalézt laděním serveru. Podrobnější informace o chybách lze získat zapnutím podrobných chyb na serveru. Další informace naleznete v tématu [Jak zpracovat chyby ve třídě Hub](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>Chyba &lt;"TypeError:&gt; hubType is undefined"

Tato chyba bude mít `MapHubs` za následek, pokud volání není provedena správně. Další informace naleznete [v tématu Jak zaregistrovat trasu SignalR a nakonfigurovat možnosti SignalR.](../guide-to-the-api/hubs-api-guide-server.md#route)

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException nebyl zpracován uživatelským kódem.

Ověřte, zda parametry odesílané do metod neobsahují neserializovatelné typy (například popisovače souborů nebo připojení k databázi). Pokud potřebujete použít členy na straně serveru objektu, který nechcete být odeslány klientovi (buď z důvodu `JSONIgnore` zabezpečení nebo z důvodu serializace), použijte atribut.

### <a name="protocol-error-unknown-transport-error"></a>Chyba protokolu: Neznámý přenos

K této chybě může dojít, pokud klient nepodporuje přenosy, které používá SignalR. Informace o tom, na kterých lze prohlížeče používat s SignalR, naleznete v části [Transporty a záložní](../getting-started/introduction-to-signalr.md#transports) soubory.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"Generování proxy centra JavaScript hub bylo zakázáno."

K této chybě `DisableJavaScriptProxies` dojde, pokud je nastavena a zároveň `signalr/hubs`obsahuje odkaz na dynamicky generovaný proxy server na . Další informace o ručním vytváření proxy serveru naleznete v [tématu Vygenerovaný proxy server a o tom, co pro vás dělá](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"ID připojení je v nesprávném formátu" nebo "Identita uživatele se nemůže během aktivního připojení SignalR změnit"

Tato chyba může být vidět, pokud je používáno ověřování a klient je odhlášen před zastavením připojení. Řešením je zastavit připojení SignalR před odhlášením klienta.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Nezachycená chyba: SignalR: jQuery nebyl nalezen. Ujistěte se, že jQuery je odkazováno před chybou souboru SignalR.js

Klient JavaScript SignalR vyžaduje ke spuštění jQuery. Ověřte, zda je odkaz na jQuery správný, zda je použitá cesta platná a zda je odkaz na jQuery před odkazem na SignalR.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>Chyba "Uncaught TypeError:&lt;Nelze&gt;číst vlastnost " vlastnosti ' nedefinované"

Tato chyba je výsledkem toho, že jQuery nebo proxy centra správně odkazuje. Ověřte, zda je váš odkaz na jQuery a proxy centra správný, zda je použitá cesta platná a zda je odkaz na jQuery před odkazem na proxy centra. Výchozí odkaz na proxy centra hubů by měl vypadat takto:

**Kód html na straně klienta, který správně odkazuje na proxy centra**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>Chyba RuntimeBinderException nebyla zpracována kódem uživatele.

K této chybě může dojít `Hub.On` při použití nesprávné přetížení. Pokud má metoda vrácenou hodnotu, musí být jako parametr obecného typu zadán návratový typ:

**Metoda definovaná na straně klienta (bez generovaného proxy serveru)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>ID připojení je nekonzistentní nebo konce připojení mezi načtením stránky

Toto chování je záměrné. Vzhledem k tomu, že objekt rozbočovače je hostován v objektu stránky, rozbočovač je zničen při aktualizaci stránky. Vícestránková aplikace musí udržovat přidružení mezi uživateli a ID připojení tak, aby byly konzistentní mezi načítánístránky. ID připojení mohou být uložena na `ConcurrentDictionary` serveru v objektu nebo databázi.

### <a name="value-cannot-be-null-error"></a>Chyba "Hodnota nemůže být null"

Metody na straně serveru s volitelnými parametry nejsou aktuálně podporovány. Pokud je volitelný parametr vynechán, metoda se nezdaří. Další informace naleznete v [tématu Optional Parameters](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox nemůže navázat připojení k serveru &lt;&gt;na adrese " chyba v Firebug

Tato chybová zpráva může být viděn v Firebug, pokud vyjednávání přenosu WebSocket selže a jiný přenos se používá místo. Toto chování je záměrné.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>Chyba "Vzdálený certifikát je neplatný podle postupu ověření" v klientské aplikaci .NET

Pokud váš server vyžaduje vlastní klientské certifikáty, můžete přidat certifikát x509 k připojení před posunutím požadavku. Přidejte certifikát k `Connection.AddClientCertificate`připojení pomocí aplikace .

### <a name="connection-drops-after-authentication-times-out"></a>Připojení klesne po uplynutí doby vypršel časový limit ověřování

Toto chování je záměrné. Ověřovací pověření nelze změnit, pokud je připojení aktivní. chcete-li aktualizovat pověření, musí být připojení zastaveno a restartováno.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected dostane volána dvakrát při použití jQuery Mobile

`initializePage` Funkce jQuery Mobile vynutí opětovné spuštění skriptů na každé stránce, čímž se vytvoří druhé připojení. Řešení tohoto problému zahrnují:

- Před soubor javascriptu uveďte odkaz na soubor jQuery Mobile.
- Zakažte `initializePage` `$.mobile.autoInitializePage = false`funkci nastavením .
- Před zahájením připojení počkejte na dokončení inicializace stránky.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Zprávy jsou zpožděny v aplikacích Silverlight pomocí událostí odeslaných serverem

Zprávy jsou zpožděny při použití událostí odeslaných serverem v systému Silverlight. Chcete-li místo toho vynutit použití dlouhého dotazování, použijte při spuštění připojení následující:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>"Oprávnění odepřeno" pomocí protokolu Forever Frame

Jedná se o známý problém popsaný [zde](https://github.com/SignalR/SignalR/issues/1963). Tento příznak může být viděn pomocí nejnovější knihovny JQuery; Řešení je downgrade aplikace na JQuery 1.8.2.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Chyby kompilace a na straně serveru

 Následující část obsahuje možná řešení chyby klienta a runtime na straně serveru. 

### <a name="reference-to-hub-instance-is-null"></a>Odkaz na instanci Hub je null.

Vzhledem k tomu, že instance centra je vytvořenpro každé připojení, nelze vytvořit instanci rozbočovače ve vašem kódu sami. Chcete-li volat metody na rozbočovači z mimo rozbočovačsám, najdete v [tématu Jak volat metody klienta a spravovat skupiny mimo hub třídy](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) jak získat odkaz na kontext rozbočovače.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session má hodnotu null.

Toto chování je záměrné. SignalR nepodporuje stav relace ASP.NET, protože povolení stavu relace by přerušilo oboustranné zasílání zpráv.

### <a name="no-suitable-method-to-override"></a>Žádná vhodná metoda k přepsání

Tato chyba se může zobrazit, pokud používáte kód ze starší dokumentace nebo blogů. Ověřte, zda neodkazujete na názvy metod, které `OnConnectedAsync`byly změněny nebo zastaralé (například ).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>Adresa HostContextExtensions.WebSocketServerUrl má hodnotu null.

Toto chování je záměrné. Tento člen je zastaralé a by neměl být používán.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>Chyba "Trasa s názvem signalr.hubs" je již v kolekci tras.

Tato chyba se `MapHubs` zobrazí, pokud je volána dvakrát vaší aplikací. Některé ukázkové `MapHubs` aplikace volají přímo v souboru globální aplikace; jiní volat v obálkové třídě. Ujistěte se, že vaše aplikace neprovádí obojí.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Problémy s visual studio

Tato část popisuje problémy, ke kterým došlo v sadě Visual Studio.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Uzel Dokumenty skriptu se v Průzkumníku řešení nezobrazuje

Některé z našich výukových programů vás nasměrují na uzel "Dokumenty skriptů" v Průzkumníku řešení při ladění. Tento uzel je vytvořen ladicím programem JavaScript a zobrazí se pouze při ladění klientů prohlížeče v aplikaci Internet Explorer; pokud se používá Chrome nebo Firefox, uzel se nezobrazí. Ladicí program JavaScript také nebude spuštěn, pokud je spuštěn jiný ladicí program klienta, například ladicí program Silverlight.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR nefunguje v sadě Visual Studio 2008 nebo starší

Toto chování je záměrné. SignalR vyžaduje rozhraní .NET Framework 4 nebo novější; to vyžaduje, aby aplikace SignalR byly vyvinuty v sadě Visual Studio 2010 nebo novější.

<a id="iis"></a>

## <a name="iis-issues"></a>Problémy se svis

Tato část obsahuje problémy s Internetovou informační službou.

### <a name="web-site-crashes-after-maphubs-call"></a>Web ováže po volání MapHubs

Tento problém byl opraven v nejnovější verzi SignalR. Ověřte, zda používáte nejnovější vydanou verzi SignalR aktualizací instalace pomocí NuGet.

<a id="azure"></a>

## <a name="azure-issues"></a>Problémy s Azure

Tato část obsahuje problémy s Microsoft Azure.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Zprávy nejsou přijímány prostřednictvím backplane Azure po změně názvů témat

Témata používaná propojovacím rozhraním Azure nejsou určena k konfiguraci uživatele.
