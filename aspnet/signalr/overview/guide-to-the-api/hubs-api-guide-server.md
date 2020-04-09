---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: Průvodce rozhraním API center signalr ASP.NET - server (C#) | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod do programování na straně serveru ASP.NET SignalR Hubs API pro SignalR verze 2, s ukázkami kódu demonstrujícími...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676186"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>Průvodce rozhraním API center ASP.NET SignalR – server (C#)

podle [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument poskytuje úvod do programování na straně serveru ASP.NET rozhraní API signalr hubů pro SignalR verze 2, s ukázkami kódu, které ukazují běžné možnosti.
> 
> Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server. V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta. V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru. SignalR se postará o všechny klient-to-server instalatérské pro vás.
> 
> SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení. Úvod do SignalR, rozbočovače a trvalá připojení naleznete [v tématu Úvod do SignalR 2](../getting-started/introduction-to-signalr.md).
> 
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR verze 2
>   
> 
> 
> ## <a name="topic-versions"></a>Verze tématu
> 
> Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).
> 
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
> 
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Jak zaregistrovat middleware SignalR](#route)

    - [Adresa URL /signalr](#signalrurl)
    - [Konfigurace možností SignalR](#options)
- [Jak vytvořit a používat třídy Hub](#hubclass)

    - [Životnost objektu centra](#transience)
    - [Camel-caseing z hubjména v javascriptových klientech](#hubnames)
    - [Více rozbočovačů](#multiplehubs)
    - [Rozbočovače silného typu](#stronglytypedhubs)
- [Jak definovat metody ve třídě Hub, které mohou klienti volat](#hubmethods)

    - [Camel-caseing názvů metod v javascriptových klientech](#methodnames)
    - [Kdy provést asynchronně](#asyncmethods)
    - [Definování přetížení](#overloads)
    - [Hlášení průběhu z vyvolání metody centra](#progress)
- [Jak volat klientské metody z třídy Hub](#callfromhub)

    - [Výběr klientů, kteří budou přijímat vzdálené volání procedur](#selectingclients)
    - [Žádné ověření v době kompilace pro názvy metod](#dynamicmethodnames)
    - [Porovnávání názvů metod bez malých a velkých písmen](#caseinsensitive)
    - [Asynchronní spuštění](#asyncclient)
- [Jak spravovat členství ve skupině z třídy Hub](#groupsfromhub)

    - [Asynchronní provádění metod Add and Remove](#asyncgroupmethods)
    - [Trvalost členství ve skupině](#grouppersistence)
    - [Skupiny pro jednoho uživatele](#singleusergroups)
- [Jak zpracovat události životnosti připojení ve třídě Hub](#connectionlifetime)

    - [Když OnConnected, OnDisconnected a OnReconnected se nazývají](#onreconnected)
    - [Stav volajícího není naplněn.](#nocallerstate)
- [Jak získat informace o klientovi z Context vlastnost](#contextproperty)
- [Jak předat stav mezi klienty a třídou Hub](#passstate)
- [Jak zpracovat chyby ve třídě Hub](#handleErrors)
- [Jak volat metody klienta a spravovat skupiny mimo třídu Hub](#callfromoutsidehub)

    - [Volání klientských metod](#callingclientsoutsidehub)
    - [Správa členství ve skupině](#managinggroupsoutsidehub)
- [Jak povolit trasování](#tracing)
- [Jak přizpůsobit kanál Rozbočovače](#hubpipeline)

Dokumentaci k programování klientů naleznete v následujících zdrojích:

- [SignalR Hubs API Guide - Klient JavaScript](hubs-api-guide-javascript-client.md)
- [Průvodce rozhraním API hubů SignalR – klient .NET](hubs-api-guide-net-client.md)

Součásti serveru pro SignalR 2 jsou k dispozici pouze v rozhraní .NET 4.5. Servery se systémem .NET 4.0 musí používat SignalR v1.x.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>Jak zaregistrovat middleware SignalR

Chcete-li definovat trasu, kterou budou klienti `MapSignalR` používat pro připojení k centru, zavolejte metodu při spuštění aplikace. `MapSignalR`je [metoda rozšíření](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` pro třídu. Následující příklad ukazuje, jak definovat směr Huby SignalR pomocí spouštěcí třídy OWIN.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

Pokud přidáváte funkce SignalR do aplikace ASP.NET MVC, ujistěte se, že je před ostatními trasami přidána trasa SignalR. Další informace naleznete v [tématu Výuka: Začínáme s SignalR 2 a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>Adresa URL /signalr

Ve výchozím nastavení je adresa URL trasy, kterou klienti používají pro připojení k centru, "/signalr". (Nepleťte si tuto adresu URL s adresou URL "/signalr/hubs", která je určen pro automaticky generovaný soubor JavaScript. Další informace o generovaném proxy serveru naleznete v [tématu SignalR Hubs API Guide - JavaScript Client - Vygenerovaný proxy server a co pro vás dělá](hubs-api-guide-javascript-client.md#genproxy).)

Mohou existovat mimořádné okolnosti, které činí tuto základní adresu URL nepoužitelnou pro SignalR; například máte složku v projektu s názvem *signalr* a nechcete změnit název. V takovém případě můžete změnit základní adresu URL, jak je znázorněno v následujících příkladech (nahradit "/signalr" v ukázkovém kódu požadovanou adresou URL).

**Kód serveru, který určuje adresu URL**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**Klientský kód JavaScriptu, který určuje adresu URL (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**Klientský kód JavaScriptu, který určuje adresu URL (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**Kód klienta .NET, který určuje adresu URL**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>Konfigurace možností signalr

Přetížení `MapSignalR` metody umožňují zadat vlastní adresu URL, vlastní překládání závislostí a následující možnosti:

- Povolte volání mezi doménami pomocí CORS nebo JSONP z klientů prohlížeče.

    Obvykle, pokud prohlížeč načte `http://contoso.com`stránku z , signalr připojení `http://contoso.com/signalr`je ve stejné doméně, at . Pokud stránka `http://contoso.com` z vytvoří `http://fabrikam.com/signalr`připojení k , to je připojení mezi doménami. Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázána. Další informace naleznete [v tématu ASP.NET SignalR Hubs API Guide – JavaScript Client - Jak navázat připojení mezi doménami](hubs-api-guide-javascript-client.md#crossdomain).
- Povolte podrobné chybové zprávy.

    Dojde-li k chybám, výchozí chování SignalR je odeslat klientům oznámení bez podrobností o tom, co se stalo. Odesílání podrobných informací o chybě klientům se v produkčním prostředí nedoporučuje, protože uživatelé se zlými úmysly mohou tyto informace použít při útocích proti vaší aplikaci. Při řešení potíží můžete pomocí této možnosti dočasně povolit informativní hlášení chyb.
- Zakázat automaticky generované soubory proxy JavaScript.

    Ve výchozím nastavení je v reakci na adresu URL "/signalr/huby" generován soubor JavaScriptu se serverem proxy pro vaše třídy Hub. Pokud nechcete používat proxy servery JavaScript nebo chcete tento soubor vygenerovat ručně a odkazovat na fyzický soubor ve svých klientech, můžete tuto možnost použít k zakázání generování proxy serveru. Další informace naleznete v [tématu SignalR Hubs API Guide – JavaScript Client - Jak vytvořit fyzický soubor pro proxy server generovaný signalr](hubs-api-guide-javascript-client.md#manualproxy).

Následující příklad ukazuje, jak zadat adresu URL připojení SignalR `MapSignalR` a tyto možnosti ve volání metody. Chcete-li zadat vlastní adresu URL, nahraďte v příkladu adresu URL, kterou chcete použít, v příkladu.To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Jak vytvořit a používat třídy Hub

Chcete-li vytvořit centrum, vytvořte třídu, která je odvozena od [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx). Následující příklad ukazuje jednoduchou třídu Hub pro chatovací aplikaci.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

V tomto příkladu může připojený `NewContosoChatMessage` klient volat metodu a když se tak stane, přijatá data jsou vysílána všem připojeným klientům.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Životnost objektu centra

Není konkretizovat Hub třídy nebo volání jeho metody z vlastního kódu na serveru; vše, co je pro vás provedeno potrubím SignalR Hubs. SignalR vytvoří novou instanci třídy Hub pokaždé, když potřebuje zpracovat operaci hubu, například když se klient připojí, odpojí nebo provede volání metody na server.

Vzhledem k tomu, že instance třídy Hub jsou přechodné, nelze je použít k udržování stavu z jednoho volání metody na další. Pokaždé, když server obdrží volání metody z klienta, nová instance třídy Hub zpracuje zprávu. Chcete-li udržovat stav prostřednictvím více připojení a volání metod, použijte jinou metodu, jako je například `Hub`databáze nebo statická proměnná ve třídě Hub nebo jinou třídu, která není odvozena z . Pokud zachováte data v paměti pomocí metody, jako je například statická proměnná ve třídě Hub, data budou ztracena při recyklaci domény aplikace.

Pokud chcete odesílat zprávy klientům z vlastního kódu, který běží mimo třídu Hub, nemůžete to udělat vytvořením instance třídy Hub, ale můžete to udělat získáním odkazu na kontextový objekt SignalR pro třídu Hub. Další informace naleznete v tématu [Jak volat klientské metody a spravovat skupiny mimo hub třídy](#callfromoutsidehub) dále v tomto tématu.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>Camel-caseing z hubjména v javascriptových klientech

Ve výchozím nastavení klienti JavaScriptu odkazují na centra pomocí verze názvu třídy s camel-cased. SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu. Předchozí příklad by byl `contosoChatHub` označován jako v kódu Jazyka JavaScript.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

Pokud chcete zadat jiný název pro klienty, `HubName` které chcete použít, přidejte atribut. Při použití `HubName` atributu se v klientech JavaScriptu nezmění žádný název na případ camelu.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Více rozbočovačů

V aplikaci můžete definovat více tříd Hub. Když to uděláte, připojení je sdílené, ale skupiny jsou oddělené:

- Všichni klienti budou používat stejnou adresu URL k navázání připojení SignalR s vaší službou ("/signalr" nebo vlastní adresou URL, pokud jste ji zadali) a toto připojení se používá pro všechna centra definovaná službou.

    Neexistuje žádný rozdíl výkonu pro více rozbočovačů ve srovnání s definováním všech funkcí rozbočovače v jedné třídě.
- Všechna centra získají stejné informace o požadavku HTTP.

    Vzhledem k tomu, že všechny rozbočovače sdílejí stejné připojení, pouze informace o požadavku HTTP, které server získá, je to, co je dodáváno v původním požadavku HTTP, který naváže připojení SignalR. Pokud použijete požadavek na připojení k předání informací z klienta na server zadáním řetězce dotazu, nemůžete poskytnout různé řetězce dotazu různým rozbočovačům. Všechna centra obdrží stejné informace.
- Vygenerovaný soubor proxy jazyka JavaScript bude obsahovat proxy servery pro všechna centra v jednom souboru.

    Informace o proxy serverech JavaScript naleznete v [tématu SignalR Hubs API Guide - JavaScript Client - Vygenerovaný proxy server a co dělá pro vás](hubs-api-guide-javascript-client.md#genproxy).
- Skupiny jsou definovány v rozbočovačích.

    V SignalR můžete definovat pojmenované skupiny pro vysílání do podskupin připojených klientů. Skupiny jsou udržovány samostatně pro každé centrum. Například skupina s názvem "Správci" by obsahovat `ContosoChatHub` jednu sadu klientů pro vaši třídu a `StockTickerHub` stejný název skupiny by odkazovat na jinou sadu klientů pro vaši třídu.

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Rozbočovače silného typu

Chcete-li definovat rozhraní pro metody rozbočovače, na které může klient odkazovat `Hub<T>` (a povolit intellisense `Hub`u metod rozbočovače), odvodit rozbočovač z (představeného v SignalR 2.1) spíše než :

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Jak definovat metody ve třídě Hub, které mohou klienti volat

Chcete-li vystavit metodu v centru, kterou chcete volat elita z klienta, deklarujte veřejnou metodu, jak je znázorněno v následujících příkladech.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Můžete zadat návratový typ a parametry, včetně komplexních typů a polí, stejně jako v libovolné metodě Jazyka C#. Všechna data, která obdržíte v parametrech nebo se vrátíte volajícímu, jsou sdělována mezi klientem a serverem pomocí JSON a SignalR automaticky zpracovává vazbu složitých objektů a polí objektů.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>Camel-caseing názvů metod v javascriptových klientech

Ve výchozím nastavení klienti JavaScriptu odkazují na metody Hub pomocí camel-cased verze názvu metody. SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

Pokud chcete zadat jiný název pro klienty, `HubMethodName` které chcete použít, přidejte atribut.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Kdy provést asynchronně

Pokud metoda bude dlouhotrvající nebo má dělat práci, která by zahrnovala čekání, jako je například vyhledávání databáze nebo volání webové služby, `void` proveďte Hub metoda asynchronní [vrácenítask](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (místo návratu) nebo [task&lt;&gt; t](https://msdn.microsoft.com/library/dd321424.aspx) objekt (místo návratového `T` typu). Když vrátíte `Task` objekt z metody SignalR čeká `Task` na dokončení a potom odešle nebalený výsledek zpět klientovi, takže není žádný rozdíl v tom, jak kód volání metody v klientovi.

Vytvoření metody Hub asynchronní zabraňuje blokování připojení při použití přenosu WebSocket. Při spuštění metody Hub synchronně a přenos je WebSocket, následné vyvolání metod na rozbočovači ze stejného klienta jsou blokovány, dokud hub metoda nedokončí.

Následující příklad ukazuje stejnou metodu kódovku pro synchronní nebo asynchronní spuštění, následovanou klientským kódem Jazyka JavaScript, který funguje pro volání obou verzí.

**Synchronní**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**Asynchronní**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

Další informace o použití asynchronních metod v ASP.NET 4.5 naleznete [v tématu Použití asynchronních metod v ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="overloads"></a>

### <a name="defining-overloads"></a>Definování přetížení

Pokud chcete definovat přetížení pro metodu, počet parametrů v každém přetížení se musí lišit. Pokud rozlišujete přetížení pouze zadáním různých typů parametrů, vaše třída Hub se zkompiluje, ale služba SignalR vyvolá výjimku v době běhu, když se klienti pokusí volat jedno z přetížení.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>Hlášení průběhu z vyvolání metody centra

SignalR 2.1 přidává podporu pro [průběh vykazování vzor](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) zavedený v .NET 4.5. Chcete-li implementovat `IProgress<T>` hlášení průběhu, definujte parametr pro metodu centra, ke které má klient přístup:

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

Při psaní dlouho běžící serverové metody je důležité použít asynchronní programovací vzor, jako je Async/ Await, nikoli blokování vlákna centra.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Jak volat klientské metody z třídy Hub

Chcete-li volat klientské metody `Clients` ze serveru, použijte vlastnost v metodě ve třídě Hub. Následující příklad ukazuje kód `addNewMessageToPage` serveru, který volá všechny připojené klienty, a klientský kód, který definuje metodu v klientovi JavaScript.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

Vyvolání metody klienta je asynchronní operace a `Task`vrátí . Použití `await`:

* Chcete-li zajistit, že zpráva je odeslána bez chyby. 
* Chcete-li povolit zachycení a zpracování chyb v bloku try-catch.

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

Nelze získat vrácenou hodnotu z metody klienta; syntaxe, `int x = Clients.All.add(1,1)` jako je nefunguje.

Pro parametry můžete určit složité typy a pole. Následující příklad předá klientovi komplexní typ v parametru metody.

**Kód serveru, který volá metodu klienta pomocí komplexního objektu**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**Kód serveru, který definuje složitý objekt**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Výběr klientů, kteří budou přijímat vzdálené volání procedur

Vlastnost Clients vrátí objekt [HubConnectionContext,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) který poskytuje několik možností pro určení, kteří klienti obdrží vzdálené volání procedur:

- Všichni připojení klienti.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- Pouze volající klient.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- Všichni klienti kromě volajícího klienta.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- Konkrétní klient identifikovaný ID připojení.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    Tento příklad `addContosoChatMessageToPage` volá volajícího klienta a `Clients.Caller`má stejný účinek jako pomocí .
- Všichni připojení klienti kromě určených klientů, identifikované ID připojení.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- Všichni připojení klienti v zadané skupině.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- Všichni připojení klienti v zadané skupině s výjimkou určených klientů identifikovaných ID připojení.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- Všichni připojení klienti v zadané skupině kromě volajícího klienta.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- Konkrétní uživatel, identifikovaný id uživatele.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    Ve výchozím nastavení `IPrincipal.Identity.Name`je to , ale to lze změnit [registrací implementace IUserIdProvider s globálním hostitelem](mapping-users-to-connections.md#IUserIdProvider).
- Všichni klienti a skupiny v seznamu ID připojení.

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- Seznam skupin.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- Uživatel podle jména.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- Seznam uživatelských jmen (uveden v SignalR 2.1).

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Žádné ověření v době kompilace pro názvy metod

Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj neexistuje žádné ověření technologie IntelliSense nebo kompilace. Výraz je vyhodnocen za běhu. Při spuštění volání metody SignalR odešle název metody a hodnoty parametrů klientovi a pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou jí předány. Pokud není v klientovi nalezena žádná odpovídající metoda, není vyvolána žádná chyba. Informace o formátu dat, která SignalR přenáší klientovi na pozadí při volání metody klienta, naleznete [v tématu Úvod do SignalR](../getting-started/introduction-to-signalr.md).

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Porovnávání názvů metod bez malých a velkých písmen

Porovnávání názvů metod nerozlišuje malá a velká písmena. Například `Clients.All.addContosoChatMessageToPage` na serveru bude `AddContosoChatMessageToPage` `addcontosochatmessagetopage`spuštěna `addContosoChatMessageToPage` , , nebo na straně klienta.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Asynchronní spuštění

Metoda, kterou voláte, se provádí asynchronně. Jakýkoli kód, který přichází po volání metody klientovi, se spustí okamžitě bez čekání na signalr dokončení přenosu dat klientům, pokud nezadáte, že následující řádky kódu by měly čekat na dokončení metody. Následující příklad kódu ukazuje, jak spustit dvě klientské metody postupně.

**Použití Await (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

Pokud použijete `await` čekat, až klient metoda dokončí před spuštěním další řádek kódu, to neznamená, že klienti skutečně obdrží zprávu před spuštěním dalšího řádku kódu. "Dokončení" volání metody klienta pouze znamená, že SignalR udělal vše potřebné k odeslání zprávy. Pokud potřebujete ověření, že klienti obdrželi zprávu, musíte tento mechanismus naprogramovat sami. Můžete například kód `MessageReceived` metodu na rozbočovača a v `addContosoChatMessageToPage` `MessageReceived` metodě na klienta můžete volat po práci, kterou potřebujete udělat na straně klienta. V `MessageReceived` centru můžete dělat cokoliv práce závisí na skutečném příjmu klienta a zpracování volání původní metody.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Použití proměnné řetězce jako názvu metody

Pokud chcete vyvolat metodu klienta pomocí proměnné řetězce jako `Clients.All` název `Clients.Others` `Clients.Caller`metody, přetypování (nebo , atd.) a `IClientProxy` pak volat [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Jak spravovat členství ve skupině z třídy Hub

Skupiny v SignalR poskytují metodu pro vysílání zpráv do určených podmnožiny připojených klientů. Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.

Chcete-li spravovat členství ve skupině, použijte `Groups` metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) poskytované vlastností třídy Hub. Následující příklad ukazuje `Groups.Add` `Groups.Remove` metody a používané v metodách Hub, které jsou volány klientským kódem, následované klientským kódem JavaScriptu, který je volá.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**Klient JavaScriptu pomocí generovaného proxy serveru**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

Není třeba explicitně vytvářet skupiny. Ve skutečnosti je skupina automaticky vytvořena při prvním zadání `Groups.Add`jejího názvu ve volání a je odstraněna při odebrání posledního připojení z členství v ní.

Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin. SignalR odesílá zprávy klientům a skupinám na základě [modelu pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)a server neudržuje seznamy skupin nebo členství ve skupinách. To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, musí být do nového uzlu rozšířen jakýkoli stav, který signalr udržuje.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Asynchronní provádění metod Add and Remove

Metody `Groups.Add` `Groups.Remove` a metody asynchronně. Pokud chcete přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, musíte se ujistit, že `Groups.Add` metoda dokončí jako první. Následující příklad kódu ukazuje, jak to udělat.

**Přidání klienta do skupiny a následné zasílání zpráv**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Trvalost členství ve skupině

SignalR sleduje připojení, nikoli uživatele, takže pokud chcete, aby byl uživatel ve stejné skupině pokaždé, když uživatel naváže připojení, musíte zavolat `Groups.Add` pokaždé, když uživatel naváže nové připojení.

Po dočasné ztrátě připojení, někdy SignalR můžete obnovit připojení automaticky. V takovém případě SignalR obnovuje stejné připojení, nikoli navazování nového připojení, a tak je automaticky obnoveno členství klienta ve skupině. To je možné i v případě, že dočasné přerušení je výsledkem restartování nebo selhání serveru, protože stav připojení pro každého klienta, včetně členství ve skupinách, je round-tripped ke klientovi. Pokud server přejde dolů a je nahrazen novým serverem před časovým limitem připojení, klient se může automaticky znovu připojit k novému serveru a znovu se zaregistrovat do skupin, kterých je členem.

Pokud nelze připojení obnovit automaticky po ztrátě připojení nebo po uplynutí doby připojení nebo po odpojení klienta (například když prohlížeč přejde na novou stránku), členství ve skupinách dojde ke ztrátě. Při příštím připojení uživatele bude nové připojení. Chcete-li zachovat členství ve skupinách, když stejný uživatel naváže nové připojení, musí aplikace sledovat přidružení mezi uživateli a skupinami a obnovit členství ve skupinách pokaždé, když uživatel naváže nové připojení.

Další informace o připojení a opětovné připojení naleznete v tématu [Jak zpracovat události životnosti připojení ve třídě Hub](#connectionlifetime) dále v tomto tématu.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Skupiny pro jednoho uživatele

Aplikace, které používají SignalR obvykle musí sledovat přidružení mezi uživateli a připojení, aby věděli, který uživatel odeslal zprávu a který uživatel by měl přijímat zprávy. Skupiny se používají v jednom ze dvou běžně používaných vzorů pro to.

- Skupiny pro jednoho uživatele.

    Jako název skupiny můžete zadat uživatelské jméno a přidat aktuální ID připojení do skupiny při každém připojení nebo opětovném připojení uživatele. Odesílání zpráv uživateli, který odesíláte do skupiny. Nevýhodou této metody je, že skupina neposkytuje způsob, jak zjistit, zda je uživatel online nebo offline.
- Sledování přidružení mezi uživatelskými jmény a ID připojení.

    Můžete uložit přidružení mezi jednotlivými uživatelskými jmény a jedním nebo více ID připojení do slovníku nebo databáze a aktualizovat uložená data při každém připojení nebo odpojení uživatele. Chcete-li uživateli odesílat zprávy, zadejte ID připojení. Nevýhodou této metody je, že trvá více paměti.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Jak zpracovat události životnosti připojení ve třídě Hub

Typickými důvody pro zpracování událostí životnosti připojení je sledovat, zda je uživatel připojen nebo ne, a sledovat přidružení mezi uživatelskými jmény a ID připojení. Chcete-li spustit vlastní kód při připojení `OnConnected`nebo `OnDisconnected`odpojení klientů, přepište , a `OnReconnected` virtuální metody třídy Hub, jak je znázorněno v následujícím příkladu.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>Když OnConnected, OnDisconnected a OnReconnected se nazývají

Pokaždé, když prohlížeč přejde na novou stránku, musí být navázáno `OnDisconnected` nové připojení, `OnConnected` což znamená, že SignalR provede metodu následovanou metodou. SignalR vždy vytvoří nové ID připojení při navázání nového připojení.

Metoda `OnReconnected` je volána, pokud došlo k dočasnému přerušení připojení, ze kterého může signalr automaticky obnovit, například když je kabel dočasně odpojen a znovu připojen před časovým limitem připojení. Metoda `OnDisconnected` je volána, když je klient odpojen a SignalR nelze automaticky znovu připojit, například když prohlížeč přejde na novou stránku. Proto je možné posloupnosti událostí `OnConnected`pro `OnReconnected` `OnDisconnected`daného klienta , , ; nebo `OnConnected` `OnDisconnected`, . Pro dané připojení se `OnConnected` `OnDisconnected`sekvence `OnReconnected` nezobrazí .

Metoda `OnDisconnected` není volat v některých scénářích, například když server přejde dolů nebo domény aplikace získá recyklovány. Když je jiný server zapnutý nebo doména aplikace dokončí recyklaci, někteří klienti `OnReconnected` se mohou znovu připojit a událost zapálit.

Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Stav volajícího není naplněn.

Metody obslužné rutiny životnosti připojení jsou volány ze `state` serveru, což znamená, že `Caller` žádný stav, který vložíte do objektu na straně klienta, nebude naplněn ve vlastnosti na serveru. Informace o `state` objektu `Caller` a vlastnosti naleznete v tématu [Jak předat stav mezi klienty a Hub třídy](#passstate) dále v tomto tématu.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Jak získat informace o klientovi z Context vlastnost

Chcete-li získat informace o `Context` klientovi, použijte vlastnost Hub třídy. Vlastnost `Context` vrátí [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) objekt, který poskytuje přístup k následujícím informacím:

- ID připojení volajícího klienta.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    ID připojení je identifikátor GUID, který je přiřazen SignalR (nelze zadat hodnotu ve vlastním kódu). Pro každé připojení existuje jedno ID připojení a stejné ID připojení používají všechna centra, pokud máte ve vaší aplikaci více center.
- Data hlavičky HTTP.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    Můžete také získat hlavičky `Context.Headers`HTTP z . Důvodem pro více odkazů na stejnou `Context.Headers` věc je, `Context.Request` že byl vytvořen `Context.Headers` jako první, vlastnost byla přidána později a byla zachována pro zpětnou kompatibilitu.
- Data řetězce dotazu.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    Můžete také získat data `Context.QueryString`řetězce dotazu z aplikace .

    Řetězec dotazu, který získáte v této vlastnosti je ten, který byl použit s požadavkem HTTP, který nastavoval připojení SignalR. Parametry řetězce dotazu můžete přidat v klientovi konfigurací připojení, což je pohodlný způsob, jak předat data o klientovi z klienta na server. Následující příklad ukazuje jeden způsob, jak přidat řetězec dotazu v klientovi JavaScriptpři použití generovaného proxy serveru.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    Další informace o nastavení parametrů řetězce dotazu naleznete v příručkách rozhraní API pro klienty [JavaScript](hubs-api-guide-javascript-client.md) a [.NET.](hubs-api-guide-net-client.md)

    Můžete najít metodu přenosu použitou pro připojení v datech řetězce dotazu, spolu s některými dalšími hodnotami používanými interně SignalR:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    Hodnota `transportMethod` bude "webSockets", "serverSentEvents", "foreverFrame" nebo "longPolling". Všimněte si, že pokud `OnConnected` zkontrolujete tuto hodnotu v metodě obslužné rutiny události, v některých scénářích můžete zpočátku získat hodnotu přenosu, která není konečnou vyjednanou metodou přenosu pro připojení. V takovém případě metoda vyvolá výjimku a bude volána znovu později při stanovení konečné metody přenosu.
- Soubory cookie.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    Soubory cookie můžete `Context.RequestCookies`získat také od společnosti .
- Informace o uživateli.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- Objekt HttpContext pro požadavek :

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    Použijte tuto metodu `HttpContext.Current` namísto `HttpContext` získání získat objekt pro připojení SignalR.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>Jak předat stav mezi klienty a třídou Hub

Proxy klient poskytuje `state` objekt, ve kterém můžete ukládat data, která chcete přenášet na server s každým voláním metody. Na serveru můžete přistupovat k `Clients.Caller` těmto datům ve vlastnosti v hubových metodách, které jsou volány klienty. Vlastnost `Clients.Caller` není naplněna pro metody obslužné rutiny události životnosti `OnConnected`připojení , `OnDisconnected`a `OnReconnected`.

Vytváření nebo aktualizace `state` dat v `Clients.Caller` objektu a vlastnosti funguje v obou směrech. Můžete aktualizovat hodnoty na serveru a jsou předány zpět klientovi.

Následující příklad ukazuje kód klienta JavaScript, který ukládá stav pro přenos na server s každým voláním metody.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

Následující příklad ukazuje ekvivalentní kód v klientovi .NET.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

Ve třídě Hub můžete přistupovat k `Clients.Caller` těmto datům ve vlastnosti. Následující příklad ukazuje kód, který načte stav uvedený v předchozím příkladu.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> Tento mechanismus pro uchování stavu není určen pro velké množství `state` `Clients.Caller` dat, protože vše, co vložíte do nebo vlastnost je round-tripped s každou metodou vyvolání. Je to užitečné pro menší položky, jako jsou uživatelská jména nebo čítače.

V VB.NET nebo v centru silného typu nelze získat přístup k `Clients.Caller`objektu stavu volajícího . místo toho `Clients.CallerState` použijte (zavedeno v SignalR 2.1):

**Použití CallerState v C #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**Použití stavu volajícího v jazyce Visual Basic**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Jak zpracovat chyby ve třídě Hub

Chcete-li zpracovat chyby, ke kterým dochází ve vašich metodách třídy Hub, nejprve se `await`ujistěte, že "dodržovat" všechny výjimky z asynchronních operací (například vyvolání klientských metod) pomocí . Poté použijte jednu nebo více z následujících metod:

- Zalomit kód metody v try-catch bloky a protokolovat objekt výjimky. Pro účely ladění můžete odeslat výjimku klientovi, ale z bezpečnostních důvodů se nedoporučuje odesílání podrobných informací klientům v produkčním prostředí.
- Vytvořte kanálový modul rozbočovačů, který zpracovává metodu [OnIncomingError.](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) Následující příklad ukazuje kanálový modul, který zaznamenává chyby, následovaný kódem v Startup.cs, který vstřikuje modul do kanálu hubů.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- Použijte `HubException` třídu (zavedenou v SignalR 2). Tato chyba může být vyvolána z libovolného vyvolání centra. Konstruktor `HubError` přebírá zprávu řetězce a objekt pro ukládání dalších chybových dat. SignalR bude automaticky serializovat výjimku a odeslat ji klientovi, kde bude použit k odmítnutí nebo selhání vyvolání metody rozbočovače.

    Následující ukázky kódu ukazují, `HubException` jak vyvolat vyvolání centra a jak zpracovat výjimku v klientech JavaScript a .NET.

    **Kód serveru demonstrující třídu HubException**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **Kód klienta JavaScriptu demonstrující odpověď na vyvolání hubexception v rozbočovači**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **Kód klienta .NET, který ukazuje odpověď na vyvolání hubvýjimky v rozbočovači**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

Další informace o modulech kanálu hubu najdete v [tématu Jak přizpůsobit kanál rozbočovačů](#hubpipeline) dále v tomto tématu.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>Jak povolit trasování

Chcete-li povolit trasování na straně serveru, přidejte do souboru Web.config prvek system.diagnostics, jak je znázorněno v tomto příkladu:

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Při spuštění aplikace v sadě Visual Studio, můžete zobrazit protokoly v okně **Výstup.**

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>Jak volat metody klienta a spravovat skupiny mimo třídu Hub

Chcete-li volat klientské metody z jiné třídy než vaše třída Hub, získejte odkaz na kontextový objekt SignalR pro centrum a použijte je k volání metod na straně klienta nebo ke správě skupin.

Následující ukázková `StockTicker` třída získá objekt context, uloží jej do instance třídy, uloží instanci třídy do statické vlastnosti `updateStockPrice` a použije kontext z instance `StockTickerHub`třídy singleton k volání metody u klientů, kteří jsou připojeni k centru s názvem .

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

Pokud potřebujete použít kontext vícekrát v objektu s dlouhou životností, získejte odkaz jednou a uložte jej, nikoli jej pokaždé znovu. Získání kontextu jednou zajišťuje, že SignalR odesílá zprávy klientům ve stejném pořadí, ve kterém vaše metody Hub provést vyvolání metody klienta. Kurz, který ukazuje, jak používat kontext SignalR pro rozbočovač, naleznete [v tématu Vysílání serveru s ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>Volání klientských metod

Můžete určit, kteří klienti obdrží vzdálené volání procedur, ale máte méně možností než při volání z třídy Hub. Důvodem je, že kontext není přidružen k určitému volání z klienta, takže žádné metody, `Clients.Others`které `Clients.Caller`vyžadují `Clients.OthersInGroup`znalost aktuálního ID připojení, například , nebo , nebo , nejsou k dispozici. K dispozici jsou následující možnosti:

- Všichni připojení klienti.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- Konkrétní klient identifikovaný ID připojení.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- Všichni připojení klienti kromě určených klientů, identifikované ID připojení.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- Všichni připojení klienti v zadané skupině.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- Všichni připojení klienti v zadané skupině s výjimkou určených klientů, identifikované ID připojení.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

Pokud voláte do třídy mimo centrum z metod ve třídě Hub, můžete předat Aktuální `Clients.Client` `Clients.AllExcept`ID `Clients.Group` připojení `Clients.Caller` `Clients.Others`a `Clients.OthersInGroup`použít jej s , , nebo simulovat , nebo . V následujícím příkladu `MoveShapeHub` třída předá ID `Broadcaster` připojení do `Broadcaster` třídy `Clients.Others`tak, aby třída může simulovat .

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Správa členství ve skupině

Pro správu skupin máte stejné možnosti jako ve třídě Hub.

- Přidání klienta do skupiny

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- Odebrání klienta ze skupiny

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Jak přizpůsobit kanál Rozbočovače

SignalR umožňuje vložit vlastní kód do kanálu hubu. Následující příklad ukazuje vlastní modul kanálu rozbočovače, který protokoluje každé příchozí volání metody přijaté z klienta a volání odchozí metody vyvolané na straně klienta:

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

Následující kód v *Startup.cs* souboru registruje modul spustit v kanálu Hub:

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

Existuje mnoho různých metod, které můžete přepsat. Úplný seznam naleznete v tématu [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).
