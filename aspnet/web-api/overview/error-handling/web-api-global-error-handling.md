---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: Globální zpracování chyb v rozhraní ASP.NET Web API 2 - ASP.NET 4.x
author: davidmatson
description: Přehled globálního zpracování chyb v rozhraní ASP.NET Web API 2 pro ASP.NET 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675418"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>Globální zpracování chyb v ASP.NET webovérozhraní API 2

podle [David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

Toto téma obsahuje přehled globálního zpracování chyb v ASP.NET web API 2 pro ASP.NET 4.x. Dnes neexistuje žádný snadný způsob, jak ve webovém rozhraní API protokolovat nebo zpracovávat chyby globálně. Některé neošetřené výjimky mohou být zpracovány pomocí [filtrů výjimek](exception-handling.md), ale existuje řada případů, které filtry výjimek nelze zpracovat. Příklad:

1. Výjimky vyzývané z konstruktorů řadiče.
2. Výjimky vyzývané z obslužných rutin zpráv.
3. Výjimky vyvolány během směrování.
4. Výjimky vyzvaté během serializace obsahu odpovědi.

Chceme poskytnout jednoduchý a konzistentní způsob, jak protokolovat a zpracovávat (pokud je to možné) tyto výjimky. 

Existují dva hlavní případy pro zpracování výjimek, případ, kdy jsme schopni odeslat odpověď na chybu a případ, kdy vše, co můžeme udělat, je protokolovat výjimku. Příkladem pro druhý případ je, když je vyvolána výjimka uprostřed obsahu odpovědi streamování; v takovém případě je příliš pozdě na odeslání nové zprávy odpovědi, protože stavový kód, záhlaví a částečný obsah již přešli přes drát, takže jednoduše přerušíme připojení. I když výjimku nelze zpracovat k vytvoření nové zprávy odpovědi, stále podporujeme protokolování výjimky. V případech, kdy můžeme zjistit chybu, můžeme vrátit odpovídající odpověď na chybu, jak je znázorněno v následujícím textu:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Existující možnosti

Kromě [filtrů výjimek](exception-handling.md)lze dnes použít [obslužné rutiny zpráv](../advanced/http-message-handlers.md) ke sledování všech odpovědí na úrovni 500, ale zpracování těchto odpovědí je obtížné, protože jim chybí kontext o původní chybě. Obslužné rutiny zpráv mají také některá stejná omezení jako filtry výjimek týkající se případů, které mohou zpracovat. Zatímco webové rozhraní API má trasovací infrastrukturu, která zachycuje chybové stavy, trasovací infrastruktura je pro diagnostické účely a není navržena ani vhodná pro spuštění v produkčním prostředí. Globální zpracování výjimek a protokolování by měly být služby, které mohou být spuštěny během výroby a zapojeny do stávajících monitorovacích řešení (například [ELMAH).](https://code.google.com/p/elmah/)

### <a name="solution-overview"></a>Přehled řešení

 Poskytujeme dvě nové uživatelem vyměnitelné [služby, IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) a IExceptionHandler, pro protokolování a zpracování neošetřených výjimek. Služby jsou velmi podobné, se dvěma hlavními rozdíly:

1. Podporujeme registraci více protokolů výjimek, ale pouze jednu obslužnou rutinu výjimky.
2. Protokolování výjimek se vždy nazývají, i když se chystáme přerušit připojení. Obslužné rutiny výjimek se volí pouze v případě, že si stále můžeme vybrat, kterou zprávu odpovědi máme odeslat.

Obě služby poskytují přístup k kontextu výjimky obsahující relevantní informace z bodu, kde byla zjištěna [výjimka, zejména HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), vyvolána výjimka a zdroj výjimky (podrobnosti níže).

### <a name="design-principles"></a>Principy návrhu

1. **Žádné změny** Vzhledem k tomu, že tato funkce je přidávána v dílčí verzi, jedním z důležitých omezení ovlivňujících řešení je, že nedojde k žádným zásadním změnám, a to buď pro zadání smluv, nebo chování. Toto omezení vyloučilo některé vyčištění, které bychom chtěli provést, pokud jde o existující bloky catch, které mění výjimky na 500 odpovědí. Tento další vyčištění je něco, co bychom mohli zvážit pro následné hlavní verze. Pokud je to pro vás důležité, hlasujte o tom na [ASP.NET hlas uživatele webového rozhraní API](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception).
2. **Zachování konzistence s konstrukcemi webového rozhraní API** Kanál filtrů webového rozhraní API je skvělý způsob, jak zpracovat průřezové obavy s flexibilitou použití logiky v konkrétním rozsahu akce, specifickém pro řadič nebo globálním rozsahu. Filtry, včetně filtrů výjimek, mají vždy kontexty akcí a kontroleru, i když jsou registrovány v globálním oboru. Tato smlouva má smysl pro filtry, ale znamená to, že filtry výjimek, i globálně vymezené filtry, nejsou vhodné pro některé případy zpracování výjimek, jako jsou výjimky z obslužných rutin zpráv, kde neexistuje žádná akce nebo kontext kontroleru. Pokud chceme použít flexibilní obor, který poskytují filtry pro zpracování výjimek, stále potřebujeme filtry výjimek. Ale pokud potřebujeme zpracovat výjimku mimo kontext řadiče, potřebujeme také samostatnou konstrukci pro úplné globální zpracování chyb (něco bez kontextu řadiče a omezení kontextu akce).

### <a name="when-to-use"></a>Kdy použít

- Protokolovače výjimek jsou řešením pro zobrazení všech neošetřených výjimek zachycených webovým rozhraním API.
- Obslužné rutiny výjimek jsou řešením pro přizpůsobení všech možných odpovědí na neošetřené výjimky zachycené webovým rozhraním API.
- Filtry výjimek jsou nejjednodušším řešením pro zpracování podmnožiny neošetřených výjimek souvisejících s určitou akcí nebo řadičem.

### <a name="service-details"></a>Podrobnosti o službě

 Rozhraní služby protokolování výjimek a obslužné rutiny jsou jednoduché asynchronní metody s ohledem na příslušné kontexty: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Poskytujeme také základní třídy pro obě tato rozhraní. Přepsání metody jádra (synchronizace nebo asynchronizace) je vše, co je nutné protokolovat nebo zpracovávat v doporučených časech. Pro protokolování `ExceptionLogger` základní třídy zajistí, že základní metoda protokolování je volána pouze jednou pro každou výjimku (i v případě, že později rozšíří dále zásobníku volání a je zachycen znovu). Základní `ExceptionHandler` třída bude volat metodu zpracování jádra pouze pro výjimky v horní části zásobníku volání, ignoruje starší vnořené bloky catch. (Zjednodušené verze těchto základních tříd jsou uvedeny v dodatku níže.) A `IExceptionLogger` `IExceptionHandler` přijímat informace o výjimce `ExceptionContext`prostřednictvím .

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Když framework volá protokolovací protokol výjimek nebo obslužnou rutinu výjimky, bude vždy poskytovat `Exception` a . `Request` S výjimkou testování částí bude také `RequestContext`vždy poskytovat . Bude zřídka poskytovat `ControllerContext` a `ActionContext` a (pouze při volání z bloku catch pro filtry výjimek). To bude velmi zřídka `Response`poskytnout (pouze v určitých případech služby IIS, když uprostřed pokusu o zápis odpovědi). Všimněte si, že vzhledem k tomu, že některé z těchto vlastností může být, `null` že je na spotřebiteli zkontrolovat `null` před přístupem členy třídy výjimek.`CatchBlock` je řetězec označující, který blok catch viděl výjimku. Řetězce bloku catch jsou následující:

- HttpServer (metoda SendAsync)
- HttpControllerDispatcher (metoda SendAsync)
- HttpBatchHandler (metoda SendAsync)
- IExceptionFilter (ApiController zpracovává kanál filtru výjimek v ExecuteAsync)
- Hostitel OWIN:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (pro ukládání výstupu do vyrovnávací paměti)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (pro výstup datového proudu)
- Webový hostitel:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (pro ukládání výstupu do vyrovnávací paměti)
    - HttpControllerHandler.WriteStreamedResponseContentAsync (pro výstup streamování)
    - HttpControllerHandler.WriteErrorResponseContentAsync (pro chyby při obnovení chyb y ve výstupním režimu ve vyrovnávací paměti)

Seznam řetězců catch block je také k dispozici prostřednictvím statických vlastností jen pro čtení. (Řetězec bloku catch jádra je na statických exceptioncatchbloech; zbytek se zobrazí na jedné statické třídě pro OWIN a webhostingu).`IsTopLevelCatchBlock` Je užitečné pro následující doporučený vzor zpracování výjimek pouze v horní části zásobníku volání. Spíše než soustružení výjimky do 500 odpovědí kdekoli dojde k vnořený blok catch, obslužná rutina výjimky můžete nechat výjimky šířit, dokud se chystá být viděn hostitelem.

Kromě `ExceptionContext`, logger dostane ještě jednu informaci prostřednictvím plné `ExceptionLoggerContext`:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

Druhá vlastnost `CanBeHandled`, umožňuje protokolovací nástroj k identifikaci výjimky, které nelze zpracovat. Když se připojení má být přerušeno a nelze odeslat žádnou novou zprávu odpovědi, úhozy kláves budou volány, ale obslužná rutina ***nebude*** volána a úhozy kláves mohou identifikovat tento scénář z této vlastnosti.

Kromě `ExceptionContext`, obslužná rutina získá další `ExceptionHandlerContext` jednu vlastnost, kterou může nastavit na úplné zpracování výjimky:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Obslužná rutina výjimky označuje, že zpracovala výjimku nastavením `Result` vlastnosti na výsledek akce (například [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)nebo vlastní výsledek). Pokud `Result` je vlastnost null, výjimka je neošetřené a původní výjimka bude znovu vyvolána.

Pro výjimky v horní části zásobníku volání jsme udělali další krok, abychom zajistili, že odpověď je vhodná pro volající rozhraní API. Pokud se výjimka rozšíří až na hostitele, volající mu zobrazí žlutou obrazovku smrti nebo nějakou jinou hostitelskou odpověď, která je obvykle HTML a obvykle není vhodnou chybovou odpovědí rozhraní API. V těchto případech Result spustí non-null a pouze v případě, že `null` vlastní obslužná rutina výjimky explicitně nastaví zpět na (neošetřené) bude výjimka šířit do hostitele. Nastavení `Result` `null` v takových případech může být užitečné pro dva scénáře:

1. OWIN hostované webové rozhraní API s vlastní výjimku zpracování middleware registrované před / mimo web API.
2. Místní ladění prostřednictvím prohlížeče, kde žlutá obrazovka smrti je ve skutečnosti užitečnou odpovědí na neošetřenou výjimku.

Pro protokolování výjimek a obslužné rutiny výjimek neděláme nic k obnovení, pokud samotný protokolovací nástroj nebo obslužná rutina vyvolá výjimku. (Kromě toho, že necháte výjimku šířit, zanechte zpětnou vazbu v dolní části této stránky, pokud máte lepší přístup.) Smlouva pro protokolování výjimek a obslužné rutiny je, že by neměly nechat výjimky šířit až do jejich volajících; v opačném případě se výjimka pouze rozšíří, často až k hostiteli, což má za následek chybu HTML (například ASP. NET je žlutá obrazovka) odesílána zpět klientovi (což obvykle není upřednostňovaná možnost pro volající rozhraní API, kteří očekávají JSON nebo XML).

## <a name="examples"></a>Příklady

### <a name="tracing-exception-logger"></a>Protokolování výjimek trasování

Protokolování výjimek níže odesílá data výjimek do nakonfigurovaných zdrojů trasování (včetně výstupního okna ladění v sadě Visual Studio).

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Obslužná rutina výjimky vlastní chybové zprávy

Obslužná rutina výjimky níže vytváří vlastní odpověď na chybu klientům, včetně e-mailové adresy pro kontaktování podpory.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Registrace filtrů výjimek

Pokud k vytvoření projektu použijete šablonu projektu "ASP.NET MVC 4 Web Application", vložte konfigurační kód webového `WebApiConfig` rozhraní API do třídy do složky *App_Start:*

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Dodatek: Podrobnosti základní třídy

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
