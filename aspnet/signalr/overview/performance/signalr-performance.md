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
# <a name="signalr-performance"></a>Výkon aplikace SignalR

podle [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak navrhnout, měřit a zlepšit výkon v aplikaci SignalR.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

Poslední prezentace o výkonu signalr a škálování naleznete [v tématu škálování v reálném čase web s ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).

Toto téma obsahuje následující oddíly:

- [Na co dát pozor při navrhování](#design)
- [Optimalizace výkonu serveru SignalR](#tuning)
- [Řešení potíží s výkonem](#troubleshooting)
- [Použití čítačů výkonu SignalR](#perfcounters)
- [Použití jiných čítačů výkonu](#othercounters)
- [Další zdroje](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Na co dát pozor při navrhování

Tato část popisuje vzory, které mohou být implementovány během návrhu aplikace SignalR, aby bylo zajištěno, že výkon není bráněno generováním zbytečného síťového provozu.

### <a name="throttling-message-frequency"></a>Četnost omezení zpráv

Dokonce i v aplikaci, která odesílá zprávy na vysoké frekvenci (například herní aplikace v reálném čase), většina aplikací nemusí odesílat více než několik zpráv za sekundu. Chcete-li snížit množství provozu, který generuje každý klient, může být implementována smyčka zpráv, která fronty a odesílá zprávy ne častěji než pevná sazba (to znamená, že až určitý počet zpráv bude odeslána každou sekundu, pokud jsou zprávy v tomto časovém intervalu, které mají být odeslány). Ukázková aplikace, která omezuje zprávy na určitou rychlost (z klienta i serveru), naleznete [v tématu Vysokofrekvenční realtime s SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>Zmenšení velikosti zprávy

Velikost zprávy SignalR můžete zmenšit zmenšením velikosti serializovaných objektů. Pokud v kódu serveru odesíláte objekt, který obsahuje vlastnosti, které není nutné přenášet, `JsonIgnore` zabraňte serializace těchto vlastností pomocí atributu. Názvy vlastností jsou také uloženy ve zprávě; názvy vlastností lze zkrátit `JsonProperty` pomocí atributu. Následující ukázka kódu ukazuje, jak vyloučit vlastnost z odesílané klientovi a jak zkrátit názvy vlastností:

**Kód serveru .NET, který demonstruje atribut JsonIgnore k vyloučení dat odesílaných klientovi, a atribut JsonProperty pro zmenšení velikosti zprávy**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

Chcete-li zachovat čitelnost/ udržovatelnost v kódu klienta, zkrácené názvy vlastností mohou být po přijetí zprávy přemapovány na názvy vhodné pro člověka. Následující ukázka kódu ukazuje jeden možný způsob přemapování zkrácené názvy na delší, definováním `reMap` zprávy smlouvy (mapování) a pomocí funkce použít smlouvu na optimalizované třídy zpráv:

**Kód JavaScriptu na straně klienta, který přemapuje zkrácené názvy vlastností na názvy čitelné pro člověka**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Názvy lze zkrátit ve zprávách z klienta na server také pomocí stejné metody.

Snížení nároku na paměť (to znamená množství paměti použité pro zprávu) objektu zprávy může také zlepšit výkon. Například pokud není potřeba `int` celý rozsah, `short` nebo `byte` lze použít místo.

Vzhledem k tomu, že zprávy jsou uloženy v sběrnici zpráv v paměti serveru, snížení velikosti zpráv může také řešit problémy s pamětí serveru.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Optimalizace výkonu serveru SignalR

Následující nastavení konfigurace lze vyladit server pro lepší výkon v aplikaci SignalR. Obecné informace o tom, jak zlepšit výkon v aplikaci ASP.NET, naleznete [v tématu Zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).

**Nastavení konfigurace SignalR**

- **DefaultMessageBufferSize**: Ve výchozím nastavení SignalR uchovává 1000 zpráv v paměti na rozbočovač na připojení. Pokud jsou používány velké zprávy, to může způsobit problémy s pamětí, které lze zmírnit snížením této hodnoty. Toto nastavení lze `Application_Start` nastavit v obslužné `Configuration` rutině události v ASP.NET aplikaci nebo v metodě spouštěcí třídy OWIN v samoobslužné aplikaci. Následující ukázka ukazuje, jak snížit tuto hodnotu, aby se snížila nároky na paměť vaší aplikace, aby se snížilo množství použité paměti serveru:

    **Kód serveru .NET v Startup.cs pro snížení výchozí velikosti vyrovnávací paměti zprávy**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**Nastavení konfigurace služby IIS**

- **Maximální počet souběžných požadavků na aplikaci**: Zvýšení počtu souběžných požadavků služby IIS zvýší prostředky serveru, které jsou k dispozici pro obsluhování požadavků. Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, proveďte v příkazovém řádku se zvýšenými oprávněními následující příkazy:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: Toto je maximální počet požadavků, které http.sys fronty pro fond aplikací. Když je fronta plná, nové požadavky obdrží odpověď 503 "Služba není k dispozici". Výchozí hodnota je 1000.

    Zkrácení délky fronty pro pracovní proces ve fondu aplikací, který je hostitelem vaší aplikace, šetří paměťové prostředky. Další informace naleznete v [tématu Správa, optimalizace a konfigurace fondů aplikací](https://technet.microsoft.com/library/cc745955.aspx).

**ASP.NET nastavení konfigurace**

Tato část obsahuje nastavení konfigurace, `aspnet.config` která lze nastavit v souboru. Tento soubor se nachází v jednom ze dvou umístění, v závislosti na platformě:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

ASP.NET nastavení, která mohou zlepšit výkon SignalR patří následující:

- **Maximální počet souběžných požadavků na procesor**: Zvýšení tohoto nastavení může zmírnit problémová místa výkonu. Chcete-li toto nastavení zvýšit, `aspnet.config` přidejte do souboru následující nastavení konfigurace:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Limit fronty požadavků**: Pokud celkový počet `maxConcurrentRequestsPerCPU` připojení překročí nastavení, ASP.NET zahájí omezení požadavků pomocí fronty. Chcete-li zvětšit velikost fronty, `requestQueueLimit` můžete zvýšit nastavení. Chcete-li to provést, přidejte `processModel` následující `config/machine.config` nastavení konfigurace `aspnet.config`do uzlu v (spíše než ):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Řešení potíží s výkonem

Tato část popisuje způsoby, jak najít problémová místa výkonu ve vaší aplikaci.

### <a name="verifying-that-websocket-is-being-used"></a>Ověření, zda je používán websocket

Zatímco SignalR můžete použít různé přenosy pro komunikaci mezi klientem a serverem, WebSocket nabízí významnou výhodu výkonu a by měl být použit, pokud klient a server podporují. Chcete-li zjistit, zda váš klient a server splňují požadavky pro WebSocket, naleznete v [tématu Přenosy a záložní](../getting-started/introduction-to-signalr.md#transports). Chcete-li zjistit, jaký přenos se používá ve vaší aplikaci, můžete použít nástroje pro vývojáře prohlížeče a zkontrolujte protokoly, abyste zjistili, jaký přenos se používá pro připojení. Informace o používání nástrojů pro vývoj prohlížeče v aplikacích Internet Explorer a Chrome naleznete v [tématu Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>Použití čítačů výkonu SignalR

Tato část popisuje, jak povolit a používat čítače výkonu SignalR, které se nacházejí v `Microsoft.AspNet.SignalR.Utils` balíčku.

### <a name="installing-signalrexe"></a>Instalace programu signalr.exe

Čítače výkonu lze přidat na server pomocí nástroje s názvem SignalR.exe. Chcete-li nainstalovat tento nástroj, postupujte takto:

1. V sadě Visual Studio vyberte **nástroje, které** > spravuje správce > **balíčků NuGet,****spravovat balíčky NuGet pro řešení.**
2. Vyhledejte **soubor signalr.utils**a vyberte Instalovat.

    ![](signalr-performance/_static/image1.png)
3. Přijměte licenční smlouvu pro instalaci balíčku.
4. SignalR.exe bude nainstalován `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`do aplikace .

### <a name="installing-performance-counters-with-signalrexe"></a>Instalace čítačů výkonu pomocí programu SignalR.exe

Chcete-li nainstalovat čítače výkonu SignalR, spusťte program SignalR.exe na příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

Chcete-li odebrat čítače výkonu SignalR, spusťte nástroj SignalR.exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>Čítače výkonu SignalR

Balíček nástroje nainstaluje následující čítače výkonu. Čítače "Celkem" měří počet událostí od posledního fondu aplikací nebo restartování serveru.

**Metriky připojení**

Následující metriky měří události životnosti připojení, ke kterým dochází. Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Připojená připojení**
- **Znovu připojeno připojení**
- **Odpojená připojení**
- **Aktuální připojení**

**Metriky zpráv**

Následující metriky měří přenos zpráv generovaný SignalR.

- **Celkový počet přijatých zpráv připojení**
- **Celkový počet odeslaných zpráv připojení**
- **Přijaté zprávy o připojení/s**
- **Odeslané zprávy o připojení/s**

**Metriky sběrnice zpráv**

Následující metriky měří provoz prostřednictvím interní sběrnice zpráv SignalR, fronty, ve které jsou umístěny všechny příchozí a odchozí zprávy SignalR. Zpráva je **publikována při** odeslání nebo vysílání. Odběratel **Subscriber** v tomto kontextu je odběr na sběrnici zpráv; to by se mělo rovnat počtu klientů plus samotný server. **Přidělený pracovník** je součást, která odesílá data aktivním připojením. **zaneprázdněný pracovník** je ten, který aktivně odesílá zprávu.

- **Celkový počet přijatých zpráv sběrnice zpráv**
- **Přijaté zprávy sběrnice zpráv/s**
- **Zprávy sběrnice zpráv publikováno celkem**
- **Publikované zprávy sběrnice zpráv/s**
- **Signální sběrnice odběratelé aktuální**
- **Předplatitelé sběrnice zpráv celkem**
- **Odběratelé sběrnice zpráv/s**
- **Pracovníci přidělených sběrnice zpráv**
- **Zaneprázdnění pracovníci sběrnice zpráv**
- **Aktuální témata sběrnice zpráv**

**Metriky chyb**

Následující metriky měří chyby generované přenosy zpráv SignalR. K chybám **řešení rozbočovače** dochází, když nelze přeložit metodu rozbočovače nebo rozbočovače. **Chyby vyvolání centra** jsou výjimky vyvolání při vyvolání metody rozbočovače. **Chyby přenosu** jsou chyby připojení vyvolány během požadavku HTTP nebo odpovědi.

- **Chyby: Všech součet**
- **Chyby: Vše/s**
- **Chyby: Rozlišení centra celkem**
- **Chyby: Rozlišení rozbočovače/s**
- **Chyby: Vyvolání centra celkem**
- **Chyby: Vyvolání centra/S**
- **Chyby: Přenos celkem**
- **Chyby: Přenos/s**

<a id="scaleout_metrics"></a>

**Metriky horizontálního navýšení kapacity**

Následující metriky měří provoz a chyby generované poskytovatelem horizontálního navýšení kapacity. A **Stream** v tomto kontextu je jednotka škálování používaná zprostředkovatelem horizontálního navýšení kapacity; Toto je tabulka, pokud sql server se používá, téma, pokud service bus se používá a předplatné, pokud redis se používá. Každý datový proud zajišťuje operace seřazeného čtení a zápisu. jeden datový proud je potenciální omezení škálování, takže počet datových proudů lze zvýšit, aby se toto kritické místo snížilo. Pokud se používá více datových proudů, SignalR bude automaticky distribuovat (střep) zprávy přes tyto datové proudy způsobem, který zajišťuje zprávy odeslané z daného připojení jsou v pořádku.

Nastavení [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) řídí délku fronty odesílání horizontálního navýšení kapacity udržované signalr. Nastavení na hodnotu větší než 0 umístí všechny zprávy do fronty odesílání, které mají být odeslány jeden po druhém na konfigurované zasílání zpráv backplane. Pokud velikost fronty přejde nad nakonfigurovanou délku, následná volání k odeslání se nezdaří okamžitě s [InvalidOperationException,](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) dokud počet zpráv ve frontě je menší než nastavení znovu. Zařazení do fronty je ve výchozím nastavení zakázáno, protože implementované backplanes mají obvykle vlastní fronty nebo řízení toku na místě. V případě SQL Server sdružování připojení účinně omezuje počet odesílá děje v jednom okamžiku.

Ve výchozím nastavení se pro SQL Server a Redis používá pouze jeden datový proud, pro službu Service Bus se používá pět datových proudů a zařazení do fronty je zakázáno, ale tato nastavení lze změnit prostřednictvím konfigurace na serveru SQL Server a Service Bus:

**Kód serveru .NET pro konfiguraci počtu tabulek a délky fronty pro rozhraní backplane serveru SQL Server**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Kód serveru .NET pro konfiguraci počtu témat a délky fronty pro prostojovací rozhraní Service Bus**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

A **Ukládání do vyrovnávací paměti** datový proud je ten, který vstoupil do chybného stavu; pokud je datový proud v chybovaném stavu, všechny zprávy odeslané do backplane se nezdaří okamžitě, dokud datový proud již není chybovat. **Délka fronty odeslat** je počet zpráv, které byly odeslány, ale ještě nebyly odeslány.

- **Přijaté zprávy sběrnice zpráv horizontálního navýšení kapacity/s**
- **Celkový počet streamů horizontálního navýšení kapacity**
- **Otevřít streamy horizontálního navýšení kapacity**
- **Ukládání datových proudů horizontálního navýšení kapacity**
- **Úplné chyby horizontálního navýšení kapacity**
- **Chyby horizontálního navýšení kapacity/s**
- **Délka fronty odeslání horizontálního navýšení kapacity**

Další informace o tom, co tyto čítače měří, najdete v [tématu Škálování signalr s Azure Service Bus](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Použití jiných čítačů výkonu

Následující čítače výkonu může být také užitečné při sledování výkonu vaší aplikace.

**Paměti**

- .NET CLR\\Paměti # bajty ve všech hromadách (pro w3wp)

**ASP.NET**

- Technologie ASP.NET\Požadavky aktuální
- Technologie ASP.NET\Zařazena do fronty
- Technologie ASP.NET\Odmítnuto

**Cpu**

- Informace o procesoru\Čas procesoru

**TCP/IP**

- Založena připojení TCPv6/Připojení
- TCPv4/Navázáno připojení

**Webová služba**

- Webová služba\Aktuální připojení
- Webová služba\Maximální počet připojení

**Dělení na vlákna**

- Zámky a vlákna\\.NET CLR # aktuálních logických vláken
- Zámky a vlákna\\.NET CLR # aktuálních fyzických vláken

<a id="otherresources"></a>

## <a name="other-resources"></a>Další prostředky

Další informace o ASP.NET sledování výkonu a ladění naleznete v následujících tématech:

- [ASP.NET přehled výkonu](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [ASP.NET využití vláken ve službě IIS 7.5, IIS 7.0 a IIS 6.0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; Element (Nastavení webu)](https://msdn.microsoft.com/library/dd560842.aspx)
