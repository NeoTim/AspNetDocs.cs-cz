---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: Použití asynchronních metod v ASP.NET 4,5 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření asynchronní aplikace webového formuláře ASP.NET pomocí Visual Studio Express 2012 pro web, což je zdarma...
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: a0aed792c5a2e790eed10c1aecf84fe5e535cea4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045153"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>Použití asynchronních metod v ASP.NET 4.5

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření asynchronní aplikace webového formuláře ASP.NET pomocí [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11), což je bezplatná verze Microsoft Visual Studio. Můžete také použít [Visual Studio 2012](https://www.microsoft.com/visualstudio/11). V tomto kurzu jsou uvedené následující oddíly.
> 
> - [Způsob zpracování požadavků fondem vláken](#HowRequestsProcessedByTP)
> - [Výběr synchronních nebo asynchronních metod](#ChoosingSyncVasync)
> - [Ukázková aplikace](#SampleApp)
> - [Synchronní stránka Gizma](#GizmosSynch)
> - [Vytvoření asynchronní stránky Gizma](#CreatingAsynchGizmos)
> - [Paralelní provádění více operací](#Parallel)
> - [Použití tokenu zrušení](#CancelToken)
> - [Konfigurace serveru pro volání webové služby vysoké souběžnosti nebo vysoké latence](#ServerConfig)
> 
> K dispozici je kompletní ukázka v tomto kurzu.  
> [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) na webu [GitHub](https://github.com/) .

Webové stránky ASP.NET 4,5 v kombinaci s [rozhraním .net 4,5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) umožňují registrovat asynchronní metody, které vracejí objekt typu [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). .NET Framework 4 představila asynchronní programovací koncept, který je označován jako [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) a ASP.NET 4,5, který podporuje [úlohu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). Úkoly jsou reprezentovány typem **úkolu** a souvisejícími typy v oboru názvů [System. Threading. Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) . .NET Framework 4,5 sestaví k této asynchronní podpoře s klíčovým slovem [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , která umožňují pracovat s objekty [úlohy](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) mnohem méně složitější než předchozí asynchronní přístupy. Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) je syntaktická zkratka pro značící, že část kódu by měla asynchronně čekat na nějakou jinou část kódu. Klíčové slovo [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) představuje pomocný parametr, který můžete použít k označení metod jako asynchronních metod založených na úlohách. Kombinace **operátoru await**, **Async**a objektu **Task** usnadňuje psaní asynchronního kódu v rozhraní .NET 4,5. Nový model pro asynchronní metody se nazývá *asynchronní vzor založený na úlohách* (**klepněte**). V tomto kurzu se předpokládá, že máte zkušenosti s asynchronním programováním pomocí klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) .

Další informace o klíčovém slově [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v následujících odkazech.

- [Dokument White Paper: asynchronii v .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Nejčastější dotazy k Async/await](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Asynchronní programování v aplikaci Visual Studio](https://msdn.microsoft.com/vstudio/gg316360)

## <a name="how-requests-are-processed-by-the-thread-pool"></a><a id="HowRequestsProcessedByTP"></a>  Způsob zpracování požadavků fondem vláken

Na webovém serveru .NET Framework udržuje fond vláken, která se používají k obsluhování požadavků ASP.NET. Když požadavek dorazí, vlákno z fondu se odešle do zpracování tohoto požadavku. Pokud je požadavek zpracováván synchronně, vlákno, který zpracovává požadavek, je při zpracování žádosti zaneprázdněno a vlákno nemůže obsluhovat jiný požadavek.   
  
Nemusí se jednat o problém, protože fond vláken je možné dostatečně velký, aby se vešel do mnoha zaneprázdněných vláken. Počet vláken ve fondu vláken je ale omezený (výchozí maximum pro .NET 4,5 je 5 000). Ve velkých aplikacích s vysokou souběžnou délkou dlouhotrvajících požadavků můžou být všechna dostupná vlákna zaneprázdněná. Tato podmínka se označuje jako vyčerpání vlákna. Po dosažení tohoto stavu vyřadí webové servery požadavky. Pokud se fronta požadavků zaplní, webový server odmítne žádosti se stavem HTTP 503 (Server je příliš zaneprázdněný). Fond vláken CLR má omezení pro vkládání nových vláken. Pokud je souběžnost souběžnosti (to znamená, že váš web může náhle obdržet velký počet požadavků) a že všechna dostupná vlákna požadavků jsou zaneprázdněna z důvodu back-endu s vysokou latencí, může vaše aplikace velmi špatně reagovat. Každé nové vlákno přidané do fondu vláken má navíc režii (například 1 MB paměti zásobníku). Webová aplikace, která používá synchronní metody pro obsluhu vysoké latence, kde se fond vláken rozrůste na standard .NET 4,5, ve výchozím nastavení maximum je 5 000 vláken, spotřebuje přibližně 5 GB více paměti, než je aplikace schopná, aby služba zpracovala stejné požadavky pomocí asynchronních metod a pouze 50 vláken. Při asynchronní práci nepoužíváte vždy vlákno. Například při provádění asynchronní žádosti webové služby nebude ASP.NET používat žádná vlákna mezi voláním **asynchronní** metody a **await**. Použití fondu vláken ke zpracování žádostí s vysokou latencí může způsobit velké nároky na paměť a špatné využití hardwaru serveru.

## <a name="processing-asynchronous-requests"></a>Zpracování asynchronních požadavků

Ve webových aplikacích, které zobrazují velký počet souběžných požadavků při spuštění nebo mají zátěžové zatížení (kde se souběžně roste souběžně), probíhá asynchronní volání webové služby, čímž se zvýší rychlost odezvy vaší aplikace. Asynchronní požadavek trvá zpracování jako synchronní požadavek stejným časem. Například pokud požadavek provede volání webové služby, které vyžaduje dokončení dvou sekund, požadavek trvá dvě sekundy, ať už se provádí synchronně nebo asynchronně. Během asynchronního volání však vlákno neblokuje odpověď na jiné požadavky, zatímco čeká na dokončení první žádosti. Asynchronní požadavky proto zabraňují zařazování požadavků a nárůstu fondu vláken, pokud existuje celá řada souběžných požadavků, které spouštějí dlouhotrvající operace.

## <a name="choosing-synchronous-or-asynchronous-methods"></a><a id="ChoosingSyncVasync"></a>  Výběr synchronních nebo asynchronních metod

V této části jsou uvedeny pokyny pro použití synchronních nebo asynchronních metod. Jsou to jenom pokyny. Prověřte každou aplikaci jednotlivě a určete, zda asynchronní metody pomůžou s výkonem.

Obecně platí, že použijte synchronní metody pro následující podmínky:

- Operace jsou jednoduché nebo krátkodobé.
- Jednoduchost je důležitější než efektivita.
- Operace jsou primárně operace CPU místo operací, které zahrnují velký výkon disku nebo síťové režie. Použití asynchronních metod na operacích vázaných na procesor poskytuje žádné výhody a má za následek větší režii.

Obecně použijte asynchronní metody pro následující podmínky:

- Voláte služby, které mohou být spotřebovány prostřednictvím asynchronních metod, a používáte rozhraní .NET 4,5 nebo vyšší.
- Operace jsou vázané na síť nebo vstupně-výstupní operace, nikoli vázané na procesor.
- Paralelismus je důležitější než jednoduchost kódu.
- Chcete poskytnout mechanismus, který umožňuje uživatelům zrušit dlouho běžící požadavek.
- Pokud výhoda přepínání vláken převáží náklady na přepínač kontextu. Obecně byste měli provést asynchronní metodu, pokud synchronní metoda blokuje vlákno žádosti ASP.NET při nečinnosti. Voláním asynchronního volání není vlákno požadavku ASP.NET zablokováno, protože při čekání na dokončení požadavku webové služby nebude fungovat.
- Testování ukazuje, že blokující operace jsou kritické pro výkon lokality a že služba IIS může obsluhovat více požadavků pomocí asynchronních metod pro tato blokující volání.

  Ukázka ke stažení ukazuje, jak efektivně používat asynchronní metody. Uvedená ukázka byla navržena tak, aby poskytovala jednoduchou ukázku asynchronního programování v ASP.NET 4,5. Vzorek není určen jako referenční architektura pro asynchronní programování v ASP.NET. Vzorový program volá metody [ASP.NET webového rozhraní API](../../../web-api/index.md) , které zavolají [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) pro simulaci dlouhotrvajících volání webové služby. Většina produkčních aplikací nebude zobrazovat takové zjevné výhody použití asynchronních metod.   
  
Několik aplikací vyžaduje, aby všechny metody byly asynchronní. Často převod několika synchronních metod na asynchronní metody poskytuje nejlepší zvýšení efektivity požadované práce.

## <a name="the-sample-application"></a><a id="SampleApp"></a>  Ukázková aplikace

Ukázkovou aplikaci si můžete stáhnout z [https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) webu [GitHubu](https://github.com/) . Úložiště se skládá ze tří projektů:

- *WebAppAsync*: projekt webových formulářů ASP.NET, který využívá službu webového rozhraní API **WebAPIpwg** . Většina kódu pro tento kurz je z tohoto projektu.
- *WebAPIpgw*: projekt webového rozhraní API ASP.NET MVC 4, který implementuje `Products, Gizmos and Widgets` řadiče. Poskytuje data pro projekt *WebAppAsync* a projekt *Mvc4Async* .
- *Mvc4Async*: projekt ASP.NET MVC 4, který obsahuje kód používaný v jiném kurzu. Provádí volání rozhraní Web API ke službě **WebAPIpwg** .

## <a name="the-gizmos-synchronous-page"></a><a id="GizmosSynch"></a>  Synchronní stránka Gizma

 Následující kód ukazuje `Page_Load` synchronní metodu, která se používá k zobrazení seznamu gizma. (Pro tento článek je Gizmo fiktivní mechanické zařízení.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

Následující kód ukazuje `GetGizmos` metodu služby Gizmo.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos`Metoda předává identifikátor URI službě HTTP webového rozhraní API ASP.NET, která vrací seznam dat gizma. Projekt *WebAPIpgw* obsahuje implementaci webového rozhraní API `gizmos, widget` a `product` řadičů.  
Následující obrázek ukazuje stránku gizma z ukázkového projektu.

![Gizma](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a name="creating-an-asynchronous-gizmos-page"></a><a id="CreatingAsynchGizmos"></a>  Vytvoření asynchronní stránky Gizma

Ukázka používá nová klíčová slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) (k dispozici v rozhraních .NET 4,5 a Visual Studio 2012), aby kompilátor mohl být zodpovědný za údržbu složitých transformací potřebných pro asynchronní programování. Kompilátor umožňuje psát kód pomocí konstrukcí toku asynchronního řízení v jazyce C# a kompilátor automaticky použije transformace potřebné k použití zpětných volání, aby nedocházelo k blokování vláken.

Asynchronní stránky ASP.NET musí zahrnovat direktivu [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) s `Async` atributem nastaveným na hodnotu "true". Následující kód ukazuje direktivu [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) s `Async` atributem nastaveným na hodnotu "true" pro stránku *GizmosAsync. aspx* .

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

Následující kód ukazuje `Gizmos` synchronní `Page_Load` metodu a `GizmosAsync` asynchronní stránku. Pokud Váš prohlížeč podporuje [ &lt; &gt; element značky HTML 5](http://www.w3.org/wiki/HTML/Elements/mark), změny se zobrazí `GizmosAsync` žlutým zvýrazněním.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

Asynchronní verze:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 Pro povolení asynchronní stránky byly provedeny následující změny `GizmosAsync` .

- Direktiva [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) musí mít `Async` atribut nastaven na hodnotu "true".
- `RegisterAsyncTask`Metoda se používá k registraci asynchronní úlohy obsahující kód, který běží asynchronně.
- Nová `GetGizmosSvcAsync` Metoda je označena pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , které kompilátor instruuje, aby vygeneroval zpětná volání pro části těla a automaticky vytvořila `Task` vrácenou hodnotu.
- &quot;&quot;K názvu asynchronní metody byla připojena asynchronní operace. Připojení "Async" není vyžadováno, ale je to konvence při psaní asynchronních metod.
- Návratový typ nové `GetGizmosSvcAsync` metody je `Task` . Návratový typ `Task` představuje probíhající práci a poskytuje volajícím metody s popisovačem, přes který má počkat na dokončení asynchronní operace.
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro volání webové služby.
- Bylo voláno rozhraní API asynchronní webové služby ( `GetGizmosAsync` ).

Uvnitř `GetGizmosSvcAsync` těla metody je volána jiná asynchronní metoda `GetGizmosAsync` . `GetGizmosAsync` okamžitě vrátí `Task<List<Gizmo>>` , který se nakonec dokončí, když jsou data k dispozici. Vzhledem k tomu, že nechcete nic dalšího dělat, dokud nebudete mít Gizmo data, kód očekává úlohu (pomocí klíčového slova **await** ). Klíčové slovo **await** lze použít pouze v metodách popsaných pomocí klíčového slova **Async** .

Klíčové slovo **await** neblokuje vlákno, dokud není úloha dokončena. Zaregistruje zbytek metody jako zpětné volání na úkolu a okamžitě se vrátí. Když se nakonec očekávaný úkol dokončí, vyvolá toto zpětné volání, takže bude pokračovat v provádění metody přímo tam, kde byla vypnuta. Další informace o použití klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v tématu [asynchronní odkazy](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

Následující kód ukazuje metody `GetGizmos` a `GetGizmosAsync`.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 Asynchronní změny jsou podobné těm, které jste udělali výše v **GizmosAsync** . 

- Podpis metody byl opatřen poznámkami pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , návratový typ byl změněn na `Task<List<Gizmo>>` a k názvu metody byl přidán *asynchronní* .
- Namísto synchronní třídy [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) se používá asynchronní třída [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) .
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro asynchronní metodu [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx) .

Na následujícím obrázku vidíte zobrazení asynchronního Gizmo.

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Prezentace prohlížečů gizma dat je shodná se zobrazením vytvořeným synchronním voláním. Jediným rozdílem je, že asynchronní verze může být větší výkon při velkém zatížení.

## <a name="registerasynctask-notes"></a>RegisterAsyncTask poznámky

Metody zapojování se spustí `RegisterAsyncTask` hned po provedení [operace PreRender](https://msdn.microsoft.com/library/ms178472.aspx).

Použijete-li události asynchronního void stránky přímo, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

už nebudete mít plnou kontrolu nad tím, kdy se události spouštějí. Například pokud. aspx a. Hlavní definují `Page_Load` události a jeden nebo oba jsou asynchronní, pořadí spouštění nelze zaručit. Pro obslužné rutiny událostí (například) platí stejné neurčité pořadí `async void Button_Click` .

## <a name="performing-multiple-operations-in-parallel"></a><a id="Parallel"></a>  Paralelní provádění více operací

Asynchronní metody mají významnou výhodu oproti synchronním metodám, pokud akce musí provádět několik nezávislých operací. V zadané ukázce zobrazuje synchronní stránka *pwg. aspx*(pro produkty, widgety a gizma) výsledky tří volání webové služby a získá seznam produktů, widgetů a gizma. Projekt [webového rozhraní API ASP.NET](../../../web-api/index.md) , který poskytuje tyto služby, používá [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) k simulaci latence nebo pomalých síťových volání. Když je zpoždění nastavené na 500 milisekund, bude stránka asynchronní *PWGasync. aspx* trvat trochu více než 500 milisekund, zatímco synchronní `PWG` verze trvá více než 1 500 milisekund. Synchronní stránka *pwg. aspx* je zobrazena v následujícím kódu.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

Asynchronní `PWGasync` kód za je uveden níže.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

Na následujícím obrázku vidíte zobrazení vrácené ze stránky asynchronní *PWGasync. aspx* .

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a name="using-a-cancellation-token"></a><a id="CancelToken"></a>  Použití tokenu zrušení

Návrat asynchronní metody `Task` jsou zrušitelné, to znamená, že přebírají parametr [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) , pokud je k dispozici `AsyncTimeout` atribut direktivy [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) . Následující kód ukazuje stránku *GizmosCancelAsync. aspx* s časovým limitem sekund.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

Následující kód ukazuje soubor *GizmosCancelAsync.aspx.cs* .

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

V poskytnuté ukázkové aplikaci výběr odkazu *GizmosCancelAsync* volá stránku *GizmosCancelAsync. aspx* a demonstruje zrušení (časování) asynchronního volání. Vzhledem k tomu, že doba zpoždění spadá do náhodného rozsahu, může být nutné stránku několikrát aktualizovat, aby se zobrazila chybová zpráva.

## <a name="server-configuration-for-high-concurrencyhigh-latency-web-service-calls"></a><a id="ServerConfig"></a>  Konfigurace serveru pro volání webové služby vysoké souběžnosti nebo vysoké latence

Aby bylo možné využít výhody asynchronní webové aplikace, může být nutné provést některé změny výchozí konfigurace serveru. Při konfiguraci a zátěži testování asynchronní webové aplikace mějte na paměti následující skutečnosti.

- Windows 7, Windows Vista, Window 8 a všechny klientské operační systémy Windows mají maximálně 10 souběžných požadavků. Budete potřebovat serverový operační systém Windows, abyste viděli výhody asynchronních metod při vysokém zatížení.
- Pomocí následujícího příkazu zaregistrujte .NET 4,5 se službou IIS z příkazového řádku se zvýšenými oprávněními:  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet \_ regiis – i  
  Viz    [registrační nástroj služby IIS ASP.NET (Aspnet \_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- Možná budete muset zvýšit limit [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) fronty z výchozí hodnoty 1 000 na 5 000. Pokud je nastavení příliš nízké, mohou se zobrazit [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) zamítnutí žádostí se stavem HTTP 503. Změna limitu HTTP.sys fronty:

    - Otevřete Správce služby IIS a přejděte do podokna fondy aplikací.
    - Klikněte pravým tlačítkem na cílový fond aplikací a vyberte **Upřesnit nastavení**.  
        ![Upřesnit](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - V dialogovém okně **Upřesnit nastavení** změňte *délku fronty* z 1 000 na 5 000.  
        ![Délka fronty](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  Všimněte si, že na obrázcích výše je rozhraní .NET Framework uvedeno jako v 4.0, i když fond aplikací používá rozhraní .NET 4,5. Pro pochopení této nesrovnalosti si přečtěte následující informace:

- [Verze rozhraní .NET a cílení na více verzí – .NET 4,5 je místní upgrade na rozhraní .NET 4,0](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [Jak nastavit aplikaci IIS nebo službu AppPool na použití ASP.NET 3,5 místo 2,0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [Verze a závislosti rozhraní .NET Framework](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- Pokud vaše aplikace používá webové služby nebo System.NET ke komunikaci s back-endu přes protokol HTTP, může být nutné zvýšit [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) element. U aplikací ASP.NET to je omezené funkcí Automatická konfigurace na 12 časů počtu procesorů. To znamená, že u čtyřjádrových procesů můžete mít \* až 12 4 = 48 souběžných připojení k koncovému bodu IP adres. Vzhledem k tomu, že se jedná o přizpůsobitelné [automatické konfigurace](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx), nejjednodušší způsob, jak zvýšit `maxconnection` ASP.NET aplikaci, je nastavit [System .NET. Třída ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) programově v `Application_Start` metodě z v souboru *Global. asax* . Příklad najdete v ukázkovém souboru ke stažení.
- V rozhraní .NET 4,5 by měla být výchozí hodnota 5000 pro [maxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) .

## <a name="contributors"></a>Přispěvatelé

- [Broderick dávky](http://stackoverflow.com/users/59641/levi)
- [Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei GE](https://blogs.msdn.com/b/hongmeig/)
