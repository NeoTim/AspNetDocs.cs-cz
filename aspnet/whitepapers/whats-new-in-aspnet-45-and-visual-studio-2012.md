---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: Co je nového v ASP.NET 4.5 a Visual Studio 2012 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento dokument popisuje nové funkce a vylepšení, které jsou zaváděny v ASP.NET 4.5. Popisuje také vylepšení pro vývoj webových aplikací ...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676284"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>Novinky v ASP.NET 4.5 a v sadě Visual Studio 2012

> Tento dokument popisuje nové funkce a vylepšení, které jsou zaváděny v ASP.NET 4.5. Popisuje také vylepšení pro vývoj webových aplikací v sadě Visual Studio 2012. Tento dokument byl původně publikován 29.

- [ASP.NET core runtime a framework](#_Toc318097372)

    - [Asynchronní čtení a zápis http požadavků a odpovědí](#_Toc318097373)
    - [Vylepšení zpracování httprequest](#_Toc318097374)
    - [Asynchronní vyprázdnění odpovědi](#_Toc318097375)
    - [Podpora *await* a *task-based*asynchronní moduly a obslužné rutiny](#_Toc318097376)
    - [Asynchronní moduly HTTP](#_Toc318097377)
    - [Asynchronní obslužné rutiny PROTOKOLU HTTP](#_Toc318097378)
    - [Nové funkce ověření žádosti o ASP.NET](#_Toc318097379)
    - [Odložené ("opožděné") ověření požadavku](#_Toc318097380)
    - [Podpora neověřených požadavků](#_Toc318097381)
    - [Knihovna AntiXSS](#_Toc318097382)
    - [Podpora protokolu WebSockets](#_Toc318097383)
    - [Vytváření sady a minifikace](#_Toc318097384)
    - [Vylepšení výkonu pro webhosting](#_Toc_perf)

        - [Klíčové faktory výkonu](#_Toc_perf_1)
        - [Požadavky na nové funkce výkonu](#_Toc_perf_2)
        - [Sdílení běžných sestavení](#_Toc_perf_3)
        - [Použití vícejádrové kompilace JIT pro rychlejší spuštění](#_Toc_perf_4)
        - [Optimalizace uvolňování paměti pro optimalizaci paměti](#_Toc_perf_5)
        - [Předběžné načítání webových aplikací](#_Toc_perf_6)
- [ASP.NET – webové formuláře](#_Toc318097385)

    - [Ovládací prvky dat silného typu](#_Toc318097386)
    - [Vazba modelu](#_Toc318097387)

        - [Výběr dat](#_Toc318097388)
        - [Poskytovatelé hodnot](#_Toc318097389)
        - [Filtrování podle hodnot z ovládacího prvku](#_Toc318097390)
    - [Výrazy datové vazby kódované html](#_Toc318097391)
    - [Nenápadné ověřování](#_Toc318097392)
    - [Aktualizace HTML5](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET – webové stránky 2](#_Toc318097395)
- [Kandidát na vydání visual studia 2012](#_Toc318097396)

    - [Sdílení projektů mezi Visual Studio 2010 a Visual Studio 2012 Release Candidate (kompatibilita s projektem)](#project-compatibility)
    - [Změny konfigurace v ASP.NET šablonách webových stránek 4.5](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [Nativní podpora ve službách IIS 7 pro směrování ASP.NET](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [Editor HTML](#_Toc318097397)

        - [Inteligentní úkoly](#_Toc318097398)
        - [Podpora pro WAI-ARIA](#_Toc318097399)
        - [Nové úryvky HTML5](#_Toc318097400)
        - [Extrahovat do uživatelského ovládacího prvku](#_Toc318097401)
        - [Technologie IntelliSense pro kódové nugety v atributech](#_Toc318097402)
        - [Automatické přejmenování odpovídající značky při přejmenování počáteční nebo uzavírací značky](#_Toc318097403)
        - [Generování obslužné rutiny události](#_Toc318097404)
        - [Inteligentní odsazení](#_Toc318097405)
        - [Automatické snížení dokončení příkazu](#_Toc318097406)
    - [JavaScript – editor](#_Toc318097407)

        - [Osnova kódu](#_Toc318097408)
        - [Shoda složených závorek](#_Toc318097409)
        - [Přejít k definici](#_Toc318097410)
        - [Podpora pro ECMAScript5](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [Přetížení podpisu VSDOC](#_Toc318097413)
        - [Implicitní odkazy](#_Toc318097414)
    - [CSS Editor](#_Toc318097415)

        - [Automatické snížení dokončení příkazu](#_Toc318097416)
        - [Hierarchické odsazení.](#_Toc318097417)
        - [Podpora pro CSS hacks](#_Toc318097418)
        - [Schémata specifická pro dodavatele (-moz-,-webkit)](#_Toc318097419)
        - [Podpora pro komentování a odkomentování](#_Toc318097420)
        - [Výběr barvy](#_Toc318097421)
        - [Fragmenty](#_Toc318097422)
        - [Vlastní oblasti](#_Toc318097423)
    - [Inspektor stránek](#_Toc318097424)
    - [Publikování](#_Toc318097425)

        - [Profily publikování](#_Toc318097426)
        - [ASP.NET předkompilace a sloučení](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Disclaimer](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET core runtime a framework

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>Asynchronní čtení a zápis http požadavků a odpovědí

ASP.NET 4 zavedla možnost číst entitu požadavku HTTP jako datový proud pomocí metody *HttpRequest.GetBufferlessInputStream.* Tato metoda poskytla přístup k datovému proudu entity požadavku. Však provádí synchronně, který svázal vlákno po dobu trvání požadavku.

ASP.NET 4.5 podporuje schopnost číst datové proudy asynchronně na entitu požadavku HTTP a schopnost vyprázdnění asynchronně. ASP.NET 4.5 také umožňuje zdvojnásobit vyrovnávací paměť entity požadavku HTTP, což usnadňuje integraci s podřízenými rutinami HTTP, jako jsou obslužné rutiny stránky ASPX a řadiče ASP.NET MVC.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>Vylepšení zpracování httprequest

Odkaz datového proudu vrácené ASP.NET 4.5 z *HttpRequest.GetBufferlessInputStream* podporuje synchronní i asynchronní metody čtení. Stream *Stream* objektvrácený z *GetBufferlessInputStream* nyní implementuje metody BeginRead a EndRead. Asynchronní *Stream* metody umožňují asynchronně číst entitu požadavku v blocích, zatímco ASP.NET uvolní aktuální vlákno mezi každou iteraci asynchronní smyčky pro čtení.

ASP.NET 4.5 také přidal doprovodnou metodu pro čtení entity požadavku ve vyrovnávací paměti: *HttpRequest.GetBufferedInputStream*. Toto nové přetížení funguje jako *GetBufferlessInputStream*, podporující synchronní i asynchronní čtení. Však při čtení *GetBufferedInputStream* také zkopíruje bajty entity do ASP.NET vnitřní vyrovnávací paměti tak, aby moduly pro příjem dat a obslužné rutiny stále přístup k entitě požadavku. Například pokud některé upstream kód v kanálu již číst entitu požadavku pomocí *GetBufferedInputStream*, můžete stále používat *HttpRequest.Form* nebo *HttpRequest.Files*. To umožňuje provádět asynchronní zpracování na požadavek (například streamování velkého souboru nahrát do databáze), ale stále spustit stránky ASPX a Řadiče MVC ASP.NET později.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Asynchronní vyprázdnění odpovědi

Odesílání odpovědí klientovi HTTP může trvat značnou dobu, když je klient daleko nebo má připojení s malou šířkou pásma. Za normálních okolností ASP.NET vyrovnávací paměti bajtů odpovědi, jak jsou vytvořeny aplikací. ASP.NET pak provede jednu operaci odesílání časově rozlišených vyrovnávacích pamětí na samém konci zpracování požadavku.

Pokud je odpověď ve vyrovnávací paměti velká (například streamování velkého souboru klientovi), musíte pravidelně volat *HttpResponse.Flush,* abyste odeslali výstup ve vyrovnávací paměti klientovi a udrželi využití paměti pod kontrolou. Však protože *Flush* je synchronní volání, iterativně volání *Flush* stále spotřebovává vlákno po dobu trvání potenciálně dlouhotrvající požadavky.

ASP.NET 4.5 přidává podporu pro provádění vyprázdnění asynchronně pomocí *BeginFlush* a *EndFlush* metody *HttpResponse* třídy. Pomocí těchto metod můžete vytvořit asynchronní moduly a asynchronní obslužné rutiny, které postupně odesílají data klientovi bez vázání vláken operačního systému. Mezi *beginflush* a *EndFlush* volání, ASP.NET uvolní aktuální vlákno. To podstatně snižuje celkový počet aktivních vláken, které jsou potřebné pro podporu dlouhotrvající stahování HTTP.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>Podpora pro *čekání* a *úlohy* - založené asynchronní moduly a obslužné rutiny

Rozhraní .NET Framework 4 zavedlo koncept asynchronního programování označovaný jako *úloha*. Úkoly jsou reprezentovány typem *úlohy* a souvisejícími typy v oboru názvů *System.Threading.Tasks.* Rozhraní .NET Framework 4.5 na tom vychází s vylepšeními kompilátoru, které usnadňují práci s objekty *Úlohy.* V rozhraní .NET Framework 4.5 kompilátory podporují dvě nová klíčová slova: *await* a *async*. Klíčové slovo *await* je syntaktické zkratka pro označení, že část kódu by měla asynchronně čekat na jinou část kódu. Klíčové slovo *async* představuje nápovědu, kterou můžete použít k označení metod jako asynchronních metod založených na úlohách.

Kombinace *await*, *async*a *Task* objektu usnadňuje psaní asynchronního kódu v rozhraní .NET 4.5. ASP.NET 4.5 podporuje tato zjednodušení s novými rozhraními API, která umožňují psát asynchronní moduly HTTP a asynchronní obslužné rutiny HTTP pomocí nových vylepšení kompilátoru.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Asynchronní moduly HTTP

Předpokládejme, že chcete provést asynchronní práci v rámci metody, která vrací *Task* objekt. Následující příklad kódu definuje asynchronní metodu, která umožňuje asynchronní volání ke stažení domovské stránky společnosti Microsoft. Všimněte si použití klíčového slova *async* v podpisu metody a *await* volání *DownloadStringTaskAsync*.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

To je vše, co musíte napsat – rozhraní .NET Framework bude automaticky zpracovávat unwinding zásobníku volání při čekání na dokončení stahování, stejně jako automatické obnovení zásobníku volání po dokončení stahování.

Nyní předpokládejme, že chcete použít tuto asynchronní metodu v asynchronním ASP.NET modulu HTTP. ASP.NET 4.5 obsahuje pomocnou metodu (*EventHandlerTaskAsyncHelper*) a nový typ delegáta *(TaskEventHandler),* který můžete použít k integraci asynchronních metod založených na úlohách se starším asynchronním programovacím modelem vystaveným kanálem HTTP ASP.NET. Tento příklad ukazuje, jak:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Asynchronní obslužné rutiny PROTOKOLU HTTP

Tradiční přístup k psaní asynchronní obslužné rutiny v ASP.NET je implementovat rozhraní *IHttpAsyncHandler.* ASP.NET 4.5 zavádí *httptaskasynchandler* asynchronní základní typ, který můžete odvodit z, což usnadňuje psaní asynchronní obslužné rutiny.

Typ *HttpTaskAsyncHandler* je abstraktní a vyžaduje, abyste přepsali metodu *ProcessRequestAsync.* Interně ASP.NET se stará o integraci *návratového* podpisu (task objekt) *ProcessRequestAsync* se starším asynchronním programovacím modelem používaným kanálem ASP.NET.

Následující příklad ukazuje, jak můžete použít *Task* a *await* jako součást implementace asynchronní obslužné rutiny HTTP:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Nové funkce ověření žádosti o ASP.NET

Ve výchozím nastavení provádí ASP.NET ověření požadavku – zkoumá požadavky na vyhledávání značek nebo skriptů v polích, záhlavích, souborech cookie a tak dále. Pokud je zjištěna, ASP.NET vyvolá výjimku. To funguje jako první linie obrany proti potenciálním útokům skriptování mezi weby.

ASP.NET 4.5 usnadňuje selektivně čtení neověřených dat požadavků. ASP.NET 4.5 také integruje populární antixss knihovnu, která byla dříve externí knihovnou.

Vývojáři často žádali o možnost selektivně vypnout ověření žádosti pro své aplikace. Pokud je například vaše aplikace softwarefóra, můžete uživatelům povolit odesílání příspěvků a komentářů ve formátu HTML, ale přesto se ujistěte, že ověření žádosti kontroluje vše ostatní.

ASP.NET 4.5 zavádí dvě funkce, které usnadňují selektivně pracovat s neověřeným vstupem: odložené ("opožděné") ověření požadavku a přístup k neověřeným datům požadavku.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Odložené ("opožděné") ověření požadavku

V ASP.NET 4.5 jsou ve výchozím nastavení všechna data požadavku podmíněna ověřením požadavku. Aplikaci však můžete nakonfigurovat tak, aby odložila ověření žádosti, dokud k nim skutečně nepřistupujete k datům požadavku. (To se někdy označuje jako opožděné ověření požadavku, na základě termínů, jako je opožděné načítání pro určité scénáře dat.) Aplikaci můžete nakonfigurovat tak, aby používala odložené ověření v souboru Web.config, nastavením atributu *requestValidationMode* na 4,5 v elementu *httpRUntime,* jako v následujícím příkladu:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

Pokud je režim ověření požadavku nastaven na hodnotu 4.5, ověření požadavku se aktivuje pouze pro určitou hodnotu požadavku a pouze v případě, že váš kód přistupuje k této hodnotě. Například pokud váš kód získá hodnotu Request.Form["forum\_post"], ověření požadavku je vyvolána pouze pro tento prvek v kolekci formulářů. Žádný z ostatních prvků v kolekci *Form* jsou ověřeny. V předchozích verzích ASP.NET bylo ověření požadavku spuštěno pro celou kolekci požadavků, když byl přístupný libovolný prvek v kolekci. Nové chování usnadňuje různým součástem aplikace pohled na různá data požadavků bez aktivace ověření požadavku na jiných částech.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Podpora neověřených požadavků

Samotné ověření odloženého požadavku nevyřeší problém selektivně vynechání mj. Volání Request.Form["forum\_post"] stále aktivuje ověření žádosti pro tuto konkrétní hodnotu požadavku. Můžete však chtít získat přístup k tomuto poli bez spuštění ověření, protože chcete povolit značky v tomto poli.

Chcete-li povolit, ASP.NET 4.5 nyní podporuje neověřený přístup k datům požadavku. ASP.NET 4.5 obsahuje novou vlastnost *neověřené* kolekce ve třídě *HttpRequest.* Tato kolekce poskytuje přístup ke všem běžným hodnotám dat požadavku, jako *je Form*, *QueryString*, *Cookies*a *Url*.

Pomocí příkladu fóra, abyste mohli číst neověřená data požadavku, musíte nejprve nakonfigurovat aplikaci tak, aby používala nový režim ověření požadavku:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Potom můžete použít vlastnost *HttpRequest.Unvalidated* ke čtení neověřené hodnoty formuláře:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Bezpečnost - *Používejte neověřená data požadavků opatrně!* ASP.NET 4.5 přidal neověřené vlastnosti a kolekce požadavků, aby vám usnadnil přístup k velmi specifickým neověřeným datům požadavku. Je však nutné stále provádět vlastní ověření na nezpracovaná data požadavku zajistit, že nebezpečný text není vykreslen uživatelům.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>Knihovna AntiXSS

Vzhledem k popularitě Knihovny Microsoft AntiXSS, ASP.NET 4.5 nyní obsahuje základní kódování rutiny z verze 4.0 této knihovny.

Kódovací rutiny jsou implementovány typem *AntiXssEncoder* v novém oboru názvů *System.Web.Security.AntiXss.* Typ *AntiXssEncoder* můžete použít přímo voláním libovolné metody statického kódování, které jsou implementovány v typu. Nejjednodušší mandatorní přístup pro použití nových rutin anti-XSS je však konfigurace ASP.NET aplikace pro použití *antixssencoder* třídy ve výchozím nastavení. Chcete-li to provést, přidejte do souboru Web.config následující atribut:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

Pokud je atribut *encoderType* nastaven na použití typu *AntiXssEncoder,* veškeré kódování výstupu v ASP.NET automaticky použije nové rutiny kódování.

Jedná se o části externí knihovny AntiXSS, které byly začleněny do ASP.NET 4.5:

- *HtmlEncode*, *HtmlFormUrlEncode*a *HtmlAttributeEncode*
- *XmlAttributeEncode* a *XmlEncode*
- *UrlEncode* a *UrlPathEncode* (nové)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Podpora protokolu WebSockets

Protokol WebSockets je síťový protokol založený na standardech, který definuje způsob vytvoření zabezpečené obousměrné komunikace v reálném čase mezi klientem a serverem přes protokol HTTP. Společnost Microsoft spolupracovala s normalizačními orgány IETF a W3C, aby pomohla definovat protokol. Protokol WebSockets je podporován libovolným klientem (nejen prohlížeči), přičemž společnost Microsoft investuje značné prostředky podporující protokol WebSockets v klientských i mobilních operačních systémech.

Protokol WebSockets usnadňuje vytváření dlouhotrvajících přenosů dat mezi klientem a serverem. Například psaní chatovací aplikace je mnohem jednodušší, protože můžete vytvořit skutečné dlouhotrvající připojení mezi klientem a serverem. Není třeba se uchýlit k řešení, jako je periodické dotazování nebo http dlouhé dotazování simulovat chování soketu.

ASP.NET 4.5 a IIS 8 zahrnují podporu webových soketů nižší úrovně, což umožňuje vývojářům ASP.NET používat spravovaná rozhraní API pro asynchronní čtení a zápis řetězcových i binárních dat na objekt WebSockets. Pro ASP.NET 4.5 je nový obor názvů *System.Web.WebSockets,* který obsahuje typy pro práci s protokolem WebSockets.

Klient prohlížeče vytvoří připojení WebSockets vytvořením objektu *DOM WebSocket,* který odkazuje na adresu URL v ASP.NET aplikaci, jako v následujícím příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Koncové body WebSockets můžete vytvořit v ASP.NET pomocí libovolného druhu modulu nebo obslužné rutiny. V předchozím příkladu byl použit soubor ASHX, protože soubory ASHX jsou rychlým způsobem vytvoření obslužné rutiny.

Podle protokolu WebSockets ASP.NET aplikace přijímá požadavek WebSockets klienta tím, že označuje, že požadavek by měl být upgradován z požadavku HTTP GET na požadavek WebSockets. Tady je příklad:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

Metoda *AcceptWebSocketRequest* přijímá delegáta funkce, protože ASP.NET odpojit aktuální požadavek HTTP a poté přenese řízení na delegáta funkce. Koncepčně tento přístup je podobný jako při použití *System.Threading.Thread*, kde definujete delegáta spuštění vlákna, ve kterém se provádí práce na pozadí.

Po ASP.NET a klient úspěšně dokončili websockets handshake, ASP.NET volání delegáta a aplikace WebSockets spustí. Následující příklad kódu ukazuje jednoduchou aplikaci echo, která používá integrovanou podporu WebSockets v ASP.NET:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

Podpora v .NET 4.5 pro *await* klíčové slovo a operace založené na asynchronních úlohách je přirozené vhodné pro psaní aplikací WebSockets. Příklad kódu ukazuje, že požadavek WebSockets běží zcela asynchronně uvnitř ASP.NET. Aplikace čeká asynchronně pro zprávu, která má být odeslána z klienta voláním *await socket. ReceiveAsync*. Podobně můžete odeslat asynchronní zprávu klientovi voláním *await socket. SendAsync*.

V prohlížeči aplikace přijímá zprávy WebSockets prostřednictvím funkce *onmessage.* Chcete-li odeslat zprávu z prohlížeče, zavolejte metodu *send* typu *WebSocket* DOM, jak je znázorněno v tomto příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

V budoucnu můžeme vydat aktualizace této funkce, které abstrahují některé nízkoúrovňové kódování, které je požadováno v této verzi pro aplikace WebSockets.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Vytváření sady a minifikace

Sdružování umožňuje kombinovat jednotlivé soubory JavaScriptu a CSS do svazku, se kterým lze zacházet jako s jedním souborem. Minifikace kondenzuje soubory JavaScriptu a CSS odebráním mezer a dalších znaků, které nejsou vyžadovány. Tyto funkce fungují s webovými formuláři, ASP.NET MVC a webovými stránkami.

Balíčky jsou vytvářeny pomocí třídy Bundle nebo jedné z jejích podřízených tříd, ScriptBundle a StyleBundle. Po konfiguraci instance balíčku je sada zpřístupněna příchozím požadavkům pouhým přidáním do globální instance Kolekce balíčků. Ve výchozích šablonách se konfigurace svazku provádí v souboru BundleConfig. Tato výchozí konfigurace vytváří svazky pro všechny základní skripty a css soubory používané šablonami.

Balíčky jsou odkazovány z v rámci zobrazení pomocí jedné z několika možných pomocných metod. Za účelem podpory vykreslování různých značek pro balíček v režimu ladění vs. vydání mají třídy ScriptBundle a StyleBundle pomocnou metodu Render. V režimu ladění vykreslování vygeneruje značky pro každý prostředek v sadě. V režimu vydání vykreslí vykreslování vygeneruje jeden prvek značky pro celou sadu. Přepínání mezi laděním a režimem vydání lze provést úpravou atributu ladění elementu kompilace v souboru web.config, jak je znázorněno níže:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Kromě toho povolení nebo zakázání optimalizace lze nastavit přímo prostřednictvím BundleTable.EnableOptimizations vlastnost.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Když jsou soubory dodávány, jsou nejprve seřazeny abecedně (způsob jejich zobrazení v **Průzkumníku řešení).** Jsou pak uspořádány tak, aby známé knihovny a jejich vlastní rozšíření (například jQuery, MooTools a Dojo) jsou načteny jako první. Například konečné pořadí pro sdružování složky Skripty, jak je uvedeno výše, bude:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS soubory jsou také seřazeny abecedně a pak reorganizovány tak, aby reset.css a normalize.css před jakýmkoli jiným souborem. Konečné řazení sdružování výše uvedené složky Styly bude toto:

1. obnovit.css
2. obsah.css
3. forms.css
4. globals.css
5. menu.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Vylepšení výkonu pro webhosting

Rozhraní .NET Framework 4.5 a Windows 8 představují funkce, které vám pomohou dosáhnout významného zvýšení výkonu pro úlohy webového serveru. To zahrnuje snížení (až o 35 %) v době spuštění a v paměti stopy webhostingu stránek, které používají ASP.NET.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Klíčové faktory výkonu

V ideálním případě by všechny webové stránky měly být aktivní a v paměti, aby byla zajištěna rychlá odpověď na další požadavek, kdykoli to přijde. Mezi faktory, které mohou ovlivnit odezvu webu, patří:

- Čas potřebný k restartování webu po recyklaci fondu aplikací. Toto je doba potřebné ke spuštění procesu webového serveru pro web, když sestavení webu již nejsou v paměti. (Sestavení platformy jsou stále v paměti, protože jsou používány jinými weby.) Tato situace se označuje jako "studené místo, teplé rozhraní spuštění" nebo jen "studené spuštění webu."
- Kolik paměti místo zabírá. Podmínky pro toto jsou "spotřeba paměti na webu" nebo "nesdílená pracovní sada".

Nová zlepšení výkonu se zaměřují na oba tyto faktory.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Požadavky na nové funkce výkonu

Požadavky na nové funkce lze rozdělit do těchto kategorií:

- Vylepšení, která jsou spuštěna v rozhraní .NET Framework 4.
- Vylepšení, která vyžadují rozhraní .NET Framework 4.5, ale lze je spustit v libovolné verzi systému Windows.
- Vylepšení, která jsou k dispozici pouze s rozhraním .NET Framework 4.5 spuštěným v systému Windows 8.

Výkon se zvyšuje s každou úroveň zlepšení, které jste schopni povolit.

Některá vylepšení rozhraní .NET Framework 4.5 využívají výhod širších funkcí výkonu, které platí i pro jiné scénáře.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Sdílení běžných sestavení

**Požadavek:** Rozhraní .NET Framework 4 a Visual Studio 11 Developer Preview SDK

Různé weby na serveru často používají stejná pomocná sestavení (například sestavení ze startovací sady nebo ukázkové aplikace). Každý web má svou vlastní kopii těchto sestavení ve svém adresáři Bin. I když je kód objektu pro sestavení identický, jsou fyzicky oddělená sestavení, takže každé sestavení musí být čteno samostatně při spuštění studeného webu a uchováváno samostatně v paměti.

Nová funkce interning řeší tuto neefektivitu a snižuje požadavky na paměť RAM i dobu načítání. Interning umožňuje systému Windows zachovat jednu kopii každého sestavení v systému souborů a jednotlivá sestavení ve složkách přihrádky webu jsou nahrazena symbolickými odkazy na jednu kopii. Pokud jednotlivé lokality potřebuje odlišnou verzi sestavení, symbolický odkaz je nahrazen novou verzí sestavení a pouze tento web je ovlivněna.

Sdílení sestavení pomocí symbolických odkazů vyžaduje nový\_nástroj s názvem aspnet intern.exe, který umožňuje vytvářet a spravovat úložiště internovaných sestavení. Je k dispozici jako součást sady Visual Studio 11 Developer Preview SDK. (Bude však fungovat v systému, který má nainstalovánpouze rozhraní .NET Framework 4, za předpokladu, že jste nainstalovali nejnovější [aktualizaci](https://support.microsoft.com/kb/2468871).)

Chcete-li zajistit, aby všechna způsobilá sestavení byla\_internována, spouštějte pravidelně program aspnet intern.exe (například jednou týdně jako naplánovanou úlohu). Typické použití je následující:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Chcete-li zobrazit všechny možnosti, spusťte nástroj bez argumentů.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Použití vícejádrové kompilace JIT pro rychlejší spuštění

**Požadavek**: .NET Framework 4.5

Pro spuštění studeného webu musí být nejen sestavení čtena z disku, ale web musí být kompilován jit. U složitého webu to může způsobit významné zpoždění. Nová technika pro obecné účely v rozhraní .NET Framework 4.5 snižuje tato zpoždění rozložením kompilace JIT mezi dostupná procesorová jádra. Dělá to co nejvíce a co nejdříve pomocí informací shromážděných během předchozích startů webu. Tato funkce implementována [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) metoda.

Jit kompilace pomocí více jader je povolena ve výchozím nastavení v ASP.NET, takže není nutné provádět nic využít této funkce. Chcete-li tuto funkci zakázat, proveďte v souboru Web.config následující nastavení:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Optimalizace uvolňování paměti pro optimalizaci paměti

**Požadavek**: .NET Framework 4.5

Jakmile je web spuštěn, jeho použití haldy systému uvolňování paměti (GC) může být významným faktorem v jeho využití paměti. Stejně jako všechny uvolňování systému .NET Framework GC provádí kompromisy mezi časem procesoru (frekvence a význam kolekce) a spotřebou paměti (další místo, které se používá pro nové, uvolněné nebo volně použitelné objekty). V předchozích verzích jsme poskytli pokyny, jak nakonfigurovat gc pro dosažení správné rovnováhy (například [viz ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

Pro rozhraní .NET Framework 4.5 je namísto více samostatných nastavení k dispozici nastavení konfigurace definované úlohou, které umožňuje všechna dříve doporučená nastavení gc a nové ladění, které poskytuje další výkon pro pracovní sadu pro jednotlivé lokality.

Chcete-li povolit ladění paměti GC, přidejte do souboru Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config následující nastavení:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Pokud jste obeznámeni s předchozími pokyny pro změny aspnet.config, všimněte si, že toto nastavení nahrazuje staré nastavení – například není nutné nastavit gcServer, gcConcurrent atd. Staré nastavení není třeba odebírat.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Předběžné načítání webových aplikací

**Požadavek**: Rozhraní .NET Framework 4.5 spuštěné ve Windows 8

Pro několik verzí systém Windows obsahuje technologii známou jako [prefetcher,](http://en.wikipedia.org/wiki/Prefetcher) která snižuje náklady na čtení disku při spuštění aplikace. Vzhledem k tomu, že studené spuštění je problém převážně pro klientské aplikace, tato technologie nebyla zahrnuta do systému Windows Server, který zahrnuje pouze součásti, které jsou nezbytné pro server. Předběžné načítání je nyní k dispozici v nejnovější verzi systému Windows Server, kde může optimalizovat spouštění jednotlivých webů.

Pro systém Windows Server není prefetcher ve výchozím nastavení povolen. Chcete-li povolit a nakonfigurovat prefetcher pro web hosting s vysokou hustotou, spusťte na příkazovém řádku následující sadu příkazů:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Chcete-li integrovat prefetcher s ASP.NET aplikacemi, přidejte do souboru Web.config následující:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Ovládací prvky dat silného typu

V ASP.NET 4.5 obsahuje webforms některá vylepšení pro práci s daty. První zlepšení je silně zadali ovládací prvky dat. Pro ovládací prvky webových formulářů v předchozích verzích ASP.NET zobrazíte hodnotu vázanou na data pomocí *výrazu Eval* a výrazu datové vazby:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

Pro obousměrnou datovou vazbu použijete *bind*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

Za běhu tato volání použít reflexe číst hodnotu zadaného člena a potom zobrazit výsledek ve značkách. Tento přístup usnadňuje vázání dat proti libovolným, netvarovaným datům.

Výrazy datové vazby, jako je tato, však nepodporují funkce, jako je IntelliSense pro názvy členů, navigace (například Přejít na definici) nebo kontrola těchto názvů v době kompilace.

K vyřešení tohoto problému ASP.NET 4.5 přidá možnost deklarovat datový typ dat, ke kterým je ovládací prvek vázán. Provést pomocí nové *ItemType* vlastnost. Při nastavení této vlastnosti jsou v oboru výrazů datové vazby k dispozici dvě nové proměnné typu: *Item* a *BindItem*. Vzhledem k tomu, že proměnné jsou silně zadali, získáte všechny výhody prostředí pro vývoj sady Visual Studio.

Pro obousměrné výrazy datové vazby použijte proměnnou *BindItem:*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

Většina ovládacích prvků v rámci ASP.NET webových formulářů, které podporují datové vazby byly aktualizovány na podporu *ItemType* vlastnost.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Vazba modelu

Vazba modelu rozšiřuje datovou vazbu v ovládacích prvcích ASP.NET webových formulářů pro práci s přístupem k datům zaměřeným na kód. Zahrnuje koncepty z ovládacího prvku *ObjectDataSource* a z vazby modelu v ASP.NET MVC.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Výběr dat

Chcete-li nakonfigurovat ovládací prvek dat pro použití vazby modelu k výběru dat, nastavte vlastnost *SelectMethod* ovládacího prvku na název metody v kódu stránky. Ovládací prvek dat volá metodu ve vhodnou dobu v životním cyklu stránky a automaticky váže vrácená data. Není nutné explicitně volat metodu *DataBind.*

V následujícím příkladu je ovládací prvek *GridView* nakonfigurován tak, aby používal metodu s názvem *GetCategories*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

V kódu stránky vytvoříte metodu *GetCategories.* Pro jednoduchou operaci výběru metoda nepotřebuje žádné parametry a měla by vrátit objekt *IEnumerable* nebo *IQueryable.* Pokud je nastavena nová vlastnost *ItemType* (která umožňuje výrazy silného typu datové vazby, jak je vysvětleno v části [Ovládací prvky](#_Toc318097386) silného typu dat dříve), měly by být vráceny obecné verze těchto rozhraní – *&lt;IEnumerable T&gt; * nebo *IQueryable&lt;T&gt;*, s parametrem *T* odpovídajícího typu *itemtype* vlastnosti (například *IQueryable&lt;Category&gt;*).

Následující příklad ukazuje kód metody *GetCategories.* Tento příklad používá model Entity Framework Code First s ukázkovou databází Northwind. Kód zajišťuje, že dotaz vrátí podrobnosti o souvisejících produktech pro každou kategorii prostřednictvím metody *Include.* (Tím je zajištěno, že *templatefield* prvek ve značce zobrazí počet produktů v každé kategorii bez nutnosti [n + 1 vybrat](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Při spuštění stránky, *GridView* ovládací prvek volá *GetCategories* metoda automaticky a vykreslí vrácená data pomocí nakonfigurovaných polí:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Vzhledem k tomu, že metoda select vrátí objekt *IQueryable,* ovládací prvek *GridView* může dále manipulovat s dotazem před jeho spuštěním. Ovládací prvek *GridView* může například přidat výrazy dotazu pro řazení a stránkování do vráceného objektu *IQueryable* před jeho provedením, takže tyto operace jsou prováděny podkladovým zprostředkovatelem LINQ. V takovém případě entity Framework zajistí, že tyto operace jsou prováděny v databázi.

Následující příklad ukazuje ovládací prvek *GridView* upravený tak, aby umožňoval řazení a stránkování:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Nyní, když se stránka spustí, ovládací prvek může zajistit, že je zobrazena pouze aktuální stránka dat a že je seřazena podle vybraného sloupce:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Chcete-li filtrovat vrácená data, musí být parametry přidány do metody select. Tyto parametry budou naplněny vazby modelu v době běhu a můžete je použít ke změně dotazu před vrácením dat.

Předpokládejme například, že chcete uživatelům povolit filtrování produktů zadáním klíčového slova do řetězce dotazu. K metodě můžete přidat parametr a aktualizovat kód tak, aby používal hodnotu parametru:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Tento kód obsahuje *výraz Where,* pokud je k dispozici hodnota pro *klíčové slovo* a potom vrátí výsledky dotazu.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Poskytovatelé hodnot

Předchozí příklad nebyl konkrétní o tom, kde hodnota parametru *klíčového slova* pochází. Chcete-li označit tyto informace, můžete použít atribut parametru. V tomto příkladu můžete použít třídu *QueryStringAttribute,* která je v oboru názvů *System.Web.ModelBinding:*

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

To instruuje vazby modelu, aby se pokusili svázat hodnotu z řetězce dotazu na parametr *klíčového slova* za běhu. (To může zahrnovat provedení převodu typu, i když tomu tak není v tomto případě.) Pokud nelze zadat hodnotu a typ nelze utříci, je vyvolána výjimka.

Zdroje hodnot pro tyto metody jsou označovány jako poskytovatelé hodnot a atributy parametrů, které označují, který poskytovatel hodnoty použít, jsou označovány jako atributy poskytovatele hodnoty. Webové formuláře budou obsahovat poskytovatele hodnot a odpovídající atributy pro všechny typické zdroje vstupu uživatele v aplikaci webových formulářů, jako je řetězec dotazu, soubory cookie, hodnoty formulářů, ovládací prvky, stav zobrazení, stav relace a vlastnosti profilu. Můžete také napsat vlastní hodnotu zprostředkovatelů.

Ve výchozím nastavení se název parametru používá jako klíč k nalezení hodnoty v kolekci zprostředkovatele hodnoty. V příkladu bude kód hledat hodnotu řetězce dotazu s názvem klíčové slovo (například ~/default.aspx?keyword=chef). Vlastní klíč můžete zadat předáním jako argument atributu parametru. Chcete-li například použít hodnotu proměnné řetězce dotazu s názvem q, můžete to provést:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Pokud je tato metoda v kódu stránky, mohou uživatelé filtrovat výsledky předáním klíčového slova pomocí řetězce dotazu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

Vazba modelu provádí mnoho úkolů, které by jinak musely kódovat ručně: čtení hodnoty, kontrola nulové hodnoty, pokus o převod na příslušný typ, kontrola, zda byl převod úspěšný, a nakonec pomocí hodnoty v dotazu. Výsledkem vazby modelu je mnohem méně kódu a možnost opětovného použití funkcí v celé aplikaci.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Filtrování podle hodnot z ovládacího prvku

Předpokládejme, že chcete rozšířit příklad, aby uživatel mohl vybrat hodnotu filtru z rozevíracího seznamu. Přidejte následující rozevírací seznam do značky a nakonfigurujte jej tak, aby získal data z jiné metody pomocí vlastnosti *SelectMethod:*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

Obvykle byste také přidat *EmptyDataTemplate* prvek *GridView* ovládacíprvek tak, aby ovládací prvek zobrazí zprávu, pokud jsou nalezeny žádné odpovídající produkty:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

V kódu stránky přidejte novou metodu výběru pro rozevírací seznam:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Nakonec aktualizujte metodu *GetProducts* select tak, aby převzala nový parametr, který obsahuje ID vybrané kategorie z rozevíracího seznamu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Nyní, když se stránka spustí, mohou uživatelé vybrat kategorii z rozevíracího seznamu a ovládací prvek *GridView* je automaticky znovu vázán tak, aby zobrazoval filtrovaná data. To je možné, protože vazba modelu sleduje hodnoty parametrů pro vybrané metody a zjistí, zda se po postbacku změnila jakákoli hodnota parametru. Pokud ano, vazba modelu vynutí přidružené řízení dat znovu vázat na data.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>Výrazy datové vazby kódované html

Nyní můžete html kódovat výsledek výrazů datové vazby. Přidání dvojtečky (:) na konec předpony &lt;%#, která označuje výraz datové vazby:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Nenápadné ověřování

Nyní můžete nakonfigurovat integrované ovládací prvky validátoru tak, aby používaly nenápadný JavaScript pro logiku ověřování na straně klienta. Tím se výrazně sníží množství javascriptu vykresleného vakvátého v značkách stránky a zmenší se celková velikost stránky. Můžete nakonfigurovat nenápadný JavaScript pro ovládací prvky validátoru libovolným z těchto způsobů:

- Globálně přidáním následujícího nastavení do elementu * &lt;appSettings&gt; * v souboru Web.config: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Globálně nastavením statické *vlastnosti System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* na *UnobtrusiveValidationMode.WebForms* (obvykle v *metodě Start aplikace\_* v souboru Global.asax).
- Jednotlivě pro stránku nastavením nové *vlastnosti UnobtrusiveValidationMode* třídy *Page* na *UnobtrusiveValidationMode.WebForms*.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>Aktualizace HTML5

Některé vylepšení byly provedeny na serverové ovládací prvky webových formulářů využít nové funkce HTML5:

- Vlastnost *TextMode* ovládacího prvku *TextBox* byla aktualizována tak, aby podporovala nové typy vstupů HTML5, jako je *e-mail*, *datetime*a tak dále.
- Ovládací prvek *FileUpload* nyní podporuje nahrávání více souborů z prohlížečů, které podporují tuto funkci HTML5.
- Ovládací prvky Validator nyní podporují ověřování vstupních prvků HTML5.
- Nové elementy HTML5, které mají atributy, které představují adresu URL, nyní podporují runat="server". V důsledku toho můžete použít ASP.NET konvencí v adresách URL cesty, jako &lt;~ operátor reprezentovat kořen aplikace (například video runat ="server" src ="~/myVideo.wmv" /&gt;).
- Ovládací prvek *UpdatePanel* byl opraven tak, aby podporoval účtování vstupních polí HTML5.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta je nyní součástí sady Visual Studio 11 Beta. ASP.NET MVC je rámec pro vývoj vysoce testovatelných a udržovatelných webových aplikací využitím vzoru Model-View-Controller (MVC). ASP.NET MVC 4 usnadňuje vytváření aplikací pro mobilní web a zahrnuje ASP.NET webové rozhraní API, které vám pomůže vytvořit služby HTTP, které mohou dosáhnout libovolného zařízení. Další informace naleznete v [ASP.NET Poznámky k verzi MVC 4](mvc4-release-notes.md).

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET – webové stránky 2

Mezi nové funkce patří následující:

- Nové a aktualizované šablony webu.
- Přidání ověření na straně serveru a klienta pomocí *pomocníka ověřování.*
- Možnost registrace skriptů pomocí správce datových zdrojů.
- Povolení přihlášení z Facebooku a dalších webů pomocí OAuth a OpenID.
- Přidávání map pomocí pomocníka *Mapy.*
- Spouštění aplikací webových stránek vedle sebe.
- Vykreslovací stránky pro mobilní zařízení.

Další informace o těchto funkcích a příkladech celostránkového kódu naleznete [v tématu Hlavní funkce na webových stránkách 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

Tato část obsahuje informace o vylepšeních pro vývoj webových aplikací v aplikacích Visual Web Developer 11 Beta a Visual Studio 2012 Release Candidate.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Sdílení projektů mezi Visual Studio 2010 a Visual Studio 2012 Release Candidate (kompatibilita s projektem)

Až do Visual Studio 2012 Release Candidate, otevření existujícího projektu v novější verzi sady Visual Studio spustilprůvodce převodem. To vynutilo upgrade obsahu (prostředků) projektu a řešení na nové formáty, které nebyly zpětně kompatibilní. Proto po převodu nelze otevřít projekt ve starší verzi sady Visual Studio.

Mnoho zákazníků nám řeklo, že to nebyl správný přístup. V sadě Visual Studio 11 Beta nyní podporujeme sdílení projektů a řešení pomocí aktualizace Visual Studio 2010 SP1. To znamená, že pokud otevřete projekt 2010 v aplikaci Visual Studio 2012 Release Candidate, budete stále moci otevřít projekt v sadě Visual Studio 2010 SP1.

> [!NOTE]
> Několik typů projektů nelze sdílet mezi Visual Studio 2010 SP1 a Visual Studio 2012 Release Candidate. Patří mezi ně některé starší projekty (například ASP.NET projekty MVC 2) nebo projekty pro zvláštní účely (například instalační projekty).

Při prvním otevření webového projektu aktualizace Visual Studio 2010 SP1 v sadě Visual Studio 11 Beta jsou do souboru projektu přidány následující vlastnosti:

- Příznaky upgradu souboru
- Umístění záloha upgradu
- Verze OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation a OldToolsVersion jsou používány procesem, který upgraduje soubor projektu. Nemají žádný vliv na práci s projektem v sadě Visual Studio 2010.

VisualStudioVersion je nová vlastnost používaná MSBuild 4.5, která označuje verzi sady Visual Studio pro aktuální projekt. Vzhledem k tomu, že tato vlastnost neexistovala v MSBuild 4.0 (verze MSBuild, které Visual Studio 2010 SP1 používá), vložíme výchozí hodnotu do souboru projektu.

Vlastnost VSToolsPath se používá k určení správného souboru .targets, který má být importován z cesty reprezentované nastavením MSBuildExtensionsPath32.

Existují také některé změny týkající se importu prvků. Tyto změny jsou nutné pro podporu kompatibility mezi oběma verzemi sady Visual Studio.

> [!NOTE]
> Pokud je projekt sdílen mezi visual studio 2010 SP1 a Visual Studio 11 Beta ve dvou\_různých počítačích a pokud projekt obsahuje místní databázi ve složce Data aplikace, musíte se ujistit, že verze SQL Serveru používaná databází je nainstalována v obou počítačích.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>Změny konfigurace v ASP.NET šablonách webových stránek 4.5

Ve výchozím souboru *Web.config* pro web vytvořený pomocí šablon webu v aplikaci Visual Studio 2012 Release Candidate byly provedeny následující změny:

- V `<httpRuntime>` elementu `encoderType` je nyní atribut ve výchozím nastavení nastaven pro použití typů AntiXSS, které byly přidány do ASP.NET. Podrobnosti naleznete [v knihovně AntiXSS](#_Toc318097382).
- Také v `<httpRuntime>` elementu `requestValidationMode` je atribut nastaven na "4.5". To znamená, že ve výchozím nastavení je ověření požadavku nakonfigurováno tak, aby používalo odložené (opožděné" ověření. Podrobnosti naleznete v tématu [New ASP.NET Request Validation Features](#_Toc318097379).
- Prvek `<modules>` oddílu `<system.webServer>` neobsahuje `runAllManagedModulesForAllRequests` atribut. (Jeho výchozí hodnota je false.) To znamená, že pokud používáte verzi služby IIS 7, která nebyla aktualizována na aktualizaci SP1, můžete mít problémy s směrováním v nové síti. Další informace naleznete [v tématu Nativní podpora ve službách IIS 7 pro ASP.NET směrování](#Native_Support_In_IIS7_For_ASPNET_Routine).

Tyto změny nemají vliv na existující aplikace. Mohou však představovat rozdíl v chování mezi existujícími weby a novými weby, které vytvoříte pro ASP.NET 4.5 pomocí nových šablon.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>Nativní podpora ve službách IIS 7 pro směrování ASP.NET

Nejedná se o změnu ASP.NET jako takovou, ale o změnu šablon pro nové projekty webu, které vás mohou ovlivnit, pokud pracujete s verzí služby IIS 7, která nebyla použita pro aktualizaci SP1.

V ASP.NET můžete do aplikací přidat následující nastavení konfigurace, aby bylo možné podporovat směrování:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

Při **runAllManagedModulesForAllRequests** je true, `http://mysite/myapp/home` url jako přejde na ASP.NET, i když není *.aspx*, *.mvc*nebo podobné rozšíření na adresu URL.

Aktualizace, která byla provedena do služby IIS 7, způsobí, že nastavení **runAllManagedModulesForAllRequests** nebude nutné a nativně podporuje směrování ASP.NET. (Informace o této aktualizaci naleznete v článku podpory společnosti [Microsoft: Je k dispozici aktualizace, která umožňuje určitým obslužným rutinám služby IIS 7.0 nebo IIS 7.5 zpracovávat požadavky, jejichž adresy URL nekončí tečkou](https://support.microsoft.com/kb/980368).)

Pokud je váš web spuštěn ve službě IIS 7 a služby IIS byla aktualizována, není nutné nastavit **runAllManagedModulesForAllRequests** na true. Ve skutečnosti nastavení na hodnotu true se nedoporučuje, protože přidává zbytečné režie zpracování požadavku. Pokud je toto nastavení pravdivé, všechny požadavky, včetně požadavků pro *.htm*, *.jpg*a další statické soubory, také procházejí kanálem ASP.NET požadavku.

Pokud vytvoříte nový web ASP.NET 4.5 pomocí šablon, které jsou k dispozici v sadě Visual Studio 2012 RC, konfigurace webu nezahrnuje **runAllManagedModulesForAllRequests** nastavení. To znamená, že ve výchozím nastavení je nastavení false.

Pokud potom spustíte web v systému Windows 7 bez nainstalovaného aktualizace SP1, služba IIS 7 nebude obsahovat požadovanou aktualizaci. V důsledku toho nebude směrování fungovat a zobrazí se chyby. Pokud máte problém, kdy směrování nefunguje, můžete provést následující kroky:

- Aktualizujte systém Windows 7 na aktualizaci SP1, která přidá aktualizaci do služby IIS 7.
- Nainstalujte aktualizaci popsanou v článku podpory společnosti Microsoft uvedeném výše.
- Nastavte **runAllManagedModulesForAllRequests** na true v souboru Web.config tohoto webu. Všimněte si, že to přidá některé režii požadavků.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>Editor HTML

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Inteligentní úkoly

V návrhovém zobrazení mají komplexní vlastnosti serverových ovládacích prvků často přidružená dialogová okna a průvodce, kteří je usnadňují jejich nastavení. Pomocí speciálního dialogového okna můžete například přidat zdroj dat do ovládacího prvku *Repeater* nebo přidat sloupce do ovládacího prvku *GridView.*

Tento typ nápovědy k rozhraní pro komplexní vlastnosti však nebyl k dispozici v zobrazení zdroje. Proto Visual Studio 11 zavádí inteligentní úlohy pro zobrazení zdroje. Inteligentní úkoly jsou kontextové zkratky pro běžně používané funkce v editorech C# a Visual Basic.

U ovládacích prvků ASP.NET webových formulářů se inteligentní úlohy zobrazují na značkách serveru jako malý glyf, když je kurzor uvnitř prvku:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

Inteligentní úloha se po klepnutí na glyf zvětšuje nebo stisknete kombinaci kláves CTRL+. (tečka), stejně jako v editorech kódu. Potom zobrazí zkratky, které jsou podobné inteligentní úkoly v návrhovém zobrazení.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Například inteligentní úloha na předchozím obrázku znázorňuje možnosti GridView Tasks. Pokud zvolíte Upravit sloupce, zobrazí se následující dialogové okno:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

Vyplnění dialogového okna nastaví stejné vlastnosti, které můžete nastavit v návrhovém zobrazení. Když kliknete na OK, značky ovládacího prvku se aktualizují s novým nastavením:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>Podpora pro WAI-ARIA

Psaní přístupných webových stránek je stále důležitější. [Wai-ARIA přístupnost standard](http://www.w3.org/WAI/intro/aria) definuje, jak vývojáři by měli psát přístupné webové stránky. Tento standard je nyní plně podporován v sadě Visual Studio.

Například atribut *role* má nyní úplnou funkci IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

Standard WAI-ARIA také zavádí atributy, které jsou předponou *s árií-* které vám umožní přidat sémantiku do dokumentu HTML5. Visual Studio také plně podporuje tyto *aria-* atributy:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Nové úryvky HTML5

Chcete-li, aby bylo rychlejší a jednodušší psát běžně používané značky HTML5, Visual Studio obsahuje řadu výstřižků. Příkladem je úryvek videa:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Chcete-li fragment vyvolat, stiskněte klávesu Tab dvakrát, když je prvek vybraný v intelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Tím se vytvoří úryvek, který můžete přizpůsobit.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Extrahovat do uživatelského ovládacího prvku

Na velkých webových stránkách může být vhodné přesunout jednotlivé části do uživatelských ovládacích prvků. Tato forma refaktoringu může pomoci zvýšit čitelnost stránky a může zjednodušit strukturu stránky.

Chcete-li to usnadnit, můžete při úpravách stránek webových formulářů ve zdrojovém zobrazení vybrat text na stránce, kliknout na něj pravým tlačítkem myši a pak vybrat Možnost Extrahovat na uživatelské řízení:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>Technologie IntelliSense pro kódové nugety v atributech

Visual Studio vždy poskytuje IntelliSense pro kód na straně serveru nugety v libovolné stránce nebo ovládacíprvek. Visual Studio nyní obsahuje intelliSense pro kód ové kostky v atributech HTML.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

To usnadňuje vytváření výrazů datové vazby:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Automatické přejmenování odpovídající značky při přejmenování počáteční nebo uzavírací značky

Pokud přejmenujete element HTML (například změníte značku *div* na značku *záhlaví),* odpovídající otevírací nebo uzavírací značka se také změní v reálném čase.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

To pomáhá vyhnout se chybě, kdy zapomenete změnit uzavírací značku nebo změnit nesprávnou.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Generování obslužné rutiny události

Visual Studio nyní obsahuje funkce ve zdrojovém zobrazení, které vám pomohou psát obslužné rutiny událostí a svázat je ručně. Pokud upravujete název události ve zdrojovém zobrazení, &lt;technologie&gt;IntelliSense zobrazí možnost Vytvořit novou událost , která vytvoří obslužnou rutinu události v kódu stránky, která má správný podpis:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Ve výchozím nastavení bude obslužná rutina události používat ID ovládacího prvku pro název metody zpracování událostí:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

Výsledná obslužná rutina události bude vypadat takto (v tomto případě v c#):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Inteligentní odsazení

Když stisknete Enter uvnitř prázdného prvku HTML, editor umístí kurzor na správné místo:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Pokud v tomto umístění stisknete Enter, uzavírací značka se posune dolů a odsaze, aby odpovídala počáteční značce. Odsazený je také textový kurzor:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>Automatické snížení dokončení příkazu

Seznam Technologie IntelliSense v sadě Visual Studio nyní filtruje na základě toho, co zadáte, takže zobrazuje pouze relevantní možnosti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

Technologie IntelliSense také filtruje na základě titulního případu jednotlivých slov v seznamu Technologie IntelliSense. Pokud například zadáte "dl", zobrazí se jak dl, tak asp:DataList:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Tato funkce umožňuje rychlejší získání dokončení příkazu pro známé prvky.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript – editor

Editor JavaScriptu ve Visual Studiu 2012 Release Candidate je zcela nový a výrazně zlepšuje práci s JavaScriptem v sadě Visual Studio.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Osnova kódu

Osnova oblasti jsou nyní automaticky vytvořeny pro všechny funkce, což umožňuje sbalit části souboru, které nejsou relevantní pro aktuální fokus.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Shoda složených závorek

Když vložíte kurzor na otevírací nebo uzavírací složenou složenku, editor zvýrazní odpovídající kurzor.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Přejít k definici

Příkaz Přejít na definici umožňuje přejít na zdroj funkce nebo proměnné.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>Podpora pro ECMAScript5

Editor podporuje novou syntaxi a rozhraní API v ECMAScript5, nejnovější verzi standardu, který popisuje jazyk JavaScript.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

Technologie IntelliSense for DOM API byla vylepšena s podporou mnoha nových api HTML5, včetně *querySelector*, DOM Storage, cross-document messaging a *canvas*. Dom IntelliSense je nyní poháněn jedním jednoduchým souborem JavaScript, spíše než nativní definice knihovny typů. To usnadňuje prodloužení nebo výměnu.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>Přetížení podpisu VSDOC

Podrobné komentáře Technologie IntelliSense lze nyní deklarovat pro * &lt;samostatné&gt; * přetížení funkcí jazyka JavaScript pomocí nového elementu podpisu, jak je znázorněno v tomto příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Implicitní odkazy

Nyní můžete přidat soubory JavaScript do centrálního seznamu, který bude implicitně zahrnut do seznamu souborů, které daný soubor JavaScript nebo odkazy na bloky, což znamená, že dostanete IntelliSense pro jeho obsah. Můžete například přidat soubory jQuery do centrálního seznamu souborů a získáte funkce IntelliSense pro funkce jQuery v libovolném bloku souboru JavaScriptu, ať už jste na ně výslovně odkazovali (pomocí /// &lt;reference /&gt;) nebo ne.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS Editor

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>Automatické snížení dokončení příkazu

Seznam IntelliSense pro CSS nyní filtruje na základě vlastností css a hodnot podporovaných vybraným schématem.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

Technologie IntelliSense také podporuje vyhledávání v případě nadpisů:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Hierarchické odsazení

Editor CSS používá odsazení k zobrazení hierarchických pravidel, což poskytuje přehled o tom, jak jsou pravidla kaskádové architektury logicky uspořádána. V následujícím příkladu #list selektor je kaskádové podřízené seznamu a je tedy odsazen.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

Následující příklad ukazuje složitější dědičnost:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

Odsazení pravidla je určeno jeho nadřazená pravidla. Hierarchické odsazení je ve výchozím nastavení povoleno, ale můžete ho zakázat v dialogovém okně Možnosti (Nástroje, Možnosti z řádku nabídek):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>Podpora pro CSS hacks

Analýza stovek reálných souborů CSS ukazuje, že hacky CSS jsou velmi časté a nyní Visual Studio podporuje ty nejpoužívanější. Tato podpora zahrnuje IntelliSense a\*ověření hvězdy\_( ) a podtržítko ( ) vlastnost hacky:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

Typické volič hacky jsou také podporovány tak, aby hierarchické odsazení je zachována, i když jsou použity. Typický volič hack používá k cílení Internet Explorer 7 je předřadit volič s * \*: first-child + html*. Použití tohoto pravidla zachová hierarchické odsazení:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Schémata specifická pro dodavatele (-moz-, -webkit)

CSS3 zavádí mnoho vlastností, které byly implementovány různými prohlížeči v různých časech. To dříve vynutilo vývojářům kód pro konkrétní prohlížeče pomocí syntaxe specifické pro dodavatele. Tyto vlastnosti specifické pro prohlížeč jsou nyní součástí technologie IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Podpora pro komentování a odkomentování

Nyní můžete komentovat a odkomentovat pravidla CSS pomocí stejných zkratek, které používáte v editoru kódu (Ctrl +K,C pro komentář a Ctrl+K,můžete odkomentovat).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Výběr barvy

V předchozích verzích sady Visual Studio se technologie IntelliSense pro atributy související s barvami skládala z rozevíracího seznamu pojmenovaných hodnot barev. Tento seznam byl nahrazen plně vybaveným výběrem barev.

Když zadáte hodnotu barvy, výběr barvy se zobrazí automaticky a zobrazí se seznam dříve použitých barev následovaný výchozí paletou barev. Barvu můžete vybrat pomocí myši nebo klávesnice.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

Seznam lze rozbalit do úplného výběru barev. Výběr umožňuje ovládat alfa kanál automatickým převodem libovolné barvy na RGBA, když přesunete jezdec krytí:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Fragmenty kódu

Úryvky v editoru CSS usnadňují a urychlejí vytváření stylů mezi prohlížeči. Mnoho vlastností CSS3, které vyžadují nastavení specifická pro prohlížeč, bylo nyní vráceno do výstřižků.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

Fragmenty CSS podporují pokročilé scénáře (například dotazy na média CSS3) zadáním symbolu at (@), který zobrazuje seznam IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

Když vyberete @media hodnotu a stisknete klávesu Tab, editor CSS vloží následující úryvek:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Stejně jako u výstřižků pro kód můžete vytvořit vlastní fragmenty CSS.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Vlastní oblasti

Oblasti pojmenovaného kódu, které jsou již k dispozici v editoru kódu, jsou nyní k dispozici pro úpravy CSS. To vám umožní snadno seskupit související bloky stylů.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Při sbalení oblasti se zobrazí název oblasti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Inspektor stránek

Page Inspector je nástroj, který vykresluje webovou stránku (HTML, webové formuláře, ASP.NET MVC nebo webové stránky) v prostředí IDE sady Visual Studio a umožňuje prozkoumat zdrojový kód i výsledný výstup. U ASP.NET stránek umožňuje Panel stránky určit, který kód na straně serveru vytvořil značky HTML, které jsou vykresleny v prohlížeči.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Další informace o inspektoru stránky naleznete v následujících kurzech:

- Použití inspektoru stránky v [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- Použití inspektoru stránky v [ASP.NET webových formulářích](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Publikování

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Profily publikování

V sadě Visual Studio 2010 publikování informací pro projekty webových aplikací není uložen ve slučovací verzi a není určen pro sdílení s ostatními. V aplikaci Visual Studio 2012 Release Candidate byl změněn formát profilu publikování. Byl vyroben artefakt týmu a nyní je snadné využít z sestavení založených na MSBuild. Informace o konfiguraci sestavení jsou v dialogovém okně Publikovat, takže můžete snadno přepínat konfigurace sestavení před publikováním.

Profily publikování jsou uloženy ve složce PublishProfiles. Umístění složky závisí na tom, jaký programovací jazyk používáte:

- C#: Vlastnosti\PublishProfiles
- Visual Basic: Projekt\Publikovat profily

Každý profil je soubor MSBuild. Během publikování je tento soubor importován do souboru MSBuild projektu. V sadě Visual Studio 2010, pokud chcete provést změny v procesu publikování nebo balíčku, je nutné umístit vlastní nastavení do souboru s názvem **ProjectName**.wpp.targets. To je stále podporováno, ale nyní můžete umístit vlastní nastavení do samotného profilu publikování. Tímto způsobem budou vlastní nastavení použita pouze pro tento profil.

Nyní můžete také využít publikovat profily z MSBuild. Chcete-li tak učinit, použijte při vytváření projektu následující příkaz:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Hodnota project.csproj je cesta projektu a ProfileName je název profilu publikovat. Případně místo předání názvu profilu *pro Vlastnost PublishProfile* můžete předat úplnou cestu k profilu publikování.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET předkompilace a sloučení

U projektů webových aplikací visual studio 2012 Release Candidate přidá na stránce Vlastnosti balíčku nebo publikování webu možnost, která umožňuje předkompilovat a sloučit obsah webu při publikování nebo balení projektu. Chcete-li tyto možnosti zobrazit, klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení, zvolte Vlastnosti a pak zvolte stránku vlastností Package/Publish Web. Následující obrázek znázorňuje možnost Předkompilovat tuto aplikaci před publikováním.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Je-li vybrána tato možnost, visual studio předkompiluje aplikaci při každém publikování nebo balení webové aplikace. Chcete-li určit, jak je web předkompilován nebo jak jsou sestavení sloučena, nakonfigurujte tyto možnosti klepnutím na tlačítko Upřesnit.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Výchozí webový server pro testování webových projektů v sadě Visual Studio je nyní služba IIS Express. Visual Studio Development Server je stále možnost pro místní webový server během vývoje, ale IIS Express je nyní doporučený server. Prostředí používání služby IIS Express v sadě Visual Studio 11 Beta je velmi podobné použití v sadě Visual Studio 2010 SP1.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Disclaimer

Toto je předběžný dokument, který může být podstatně změněn před konečným komerčním vydáním zde popsaného softwaru.

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Vzhledem k tomu, že společnost Microsoft musí reagovat na měnící se podmínky na trhu, neměla by být vykládána jako závazek ze strany společnosti Microsoft a společnost Microsoft nemůže zaručit přesnost jakýchkoli informací předložených po datu zveřejnění.

Tato bílá kniha je pouze pro informační účely. SPOLEČNOST MICROSOFT NEPOSKYTUJE ŽÁDNÉ ZÁRUKY, VÝSLOVNÉ, PŘEDPOKLÁDANÉ ANI ZÁKONNÉ, POKUD JDE O INFORMACE V TOMTO DOKUMENTU.

Dodržování všech platných autorských zákonů je odpovědností uživatele. Bez omezení autorských práv nesmí být žádná část tohoto dokumentu reprodukována, ukládána nebo zaváděna do vyhledávacího systému ani přenášena v jakékoli formě nebo jakýmikoli prostředky (elektronicky, mechanicky, fotokopírováním, záznamem nebo jinak) ani za žádným účelem bez výslovného písemného souhlasu společnosti Microsoft Corporation.

Společnost Microsoft může mít patenty, patentové přihlášky, ochranné známky, autorská práva nebo jiná práva duševního vlastnictví týkající se předmětu tohoto dokumentu. S výjimkou případů výslovně uvedených v jakékoli písemné licenční smlouvě od společnosti Microsoft vám poskytnutí tohoto dokumentu neposkytuje žádnou licenci k těmto patentům, ochranným známkám, autorským právům nebo jinému duševnímu vlastnictví.

Není-li uvedeno jinak, jsou zde uvedené příklady společností, organizací, produktů, názvů domén, e-mailových adres, log, osob, míst a událostí, které jsou zde zobrazeny, smyšlené a žádné spojení se skutečnou společností, organizací, produktem, názvem domény, e-mailovou adresou, logem, osobou, místem nebo událostí, která by měla být nebo by měla být odvozena.

© 2012 Microsoft Corporation. Všechna práva vyhrazena.

Microsoft a Windows jsou registrované ochranné známky nebo ochranné známky společnosti Microsoft Corporation ve Spojených státech amerických a dalších zemích.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.
