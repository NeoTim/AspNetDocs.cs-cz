---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Osvědčené postupy pro vývoj webových aplikací (vytváření cloudových aplikací v reálném světě s Azure) | Dokumenty společnosti Microsoft
author: MikeWasson
description: Cloudová kniha Building Real World S Azure vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje to 13 vzorů a postupů, které může...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675997"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Osvědčené postupy pro vývoj webových aplikací (vytváření reálných cloudových aplikací s Azure)

od [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Stáhnout Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stáhnout E-knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Cloudová kniha Building Real World S Azure** vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje 13 vzorů a postupů, které vám mohou pomoci úspěšně vyvíjet webové aplikace pro cloud. Informace o e-knize najdete [v první kapitole](introduction.md).

První tři vzory byly o nastavení agilního vývojového procesu; zbytek je o architektuře a kódu. Tohle je sbírka osvědčených postupů pro vývoj webových aplikací:

- [Bezstátní webové servery](#stateless) za inteligentní vyrovnávání zatížení.
- [Vyhněte se stavu relace](#sessionstate) (nebo pokud se mu nemůžete vyhnout, použijte distribuovanou mezipaměť spíše než databázi).
- [Pomocí sítě CDN](#cdn) můžete ukládat statické datové zdroje souborů do mezipaměti (obrázky, skripty).
- [Použijte asynchronní podporu rozhraní .NET 4.5,](#async) abyste zabránili blokování volání.

Tyto postupy platí pro veškerý vývoj webových aplikací, nejen pro cloudové aplikace, ale jsou obzvláště důležité pro cloudové aplikace. Spolupracují, aby vám pomohly optimálně využít vysoce flexibilní škálování nabízené cloudovým prostředím. Pokud tyto postupy nedodržujete, narazíte na omezení při pokusu o škálování aplikace.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Webová vrstva bez státní příslušnosti za inteligentním vyvažovačem zatížení

*Bezstavová webová vrstva* znamená, že do paměti webového serveru nebo systému souborů neukládáte žádná data aplikací. Udržování vaší webové úrovně bezstavové umožňuje jak poskytovat lepší zákaznickou zkušenost a ušetřit peníze:

- Pokud je webová vrstva bezstavová a je sedět za nástrojů pro vyrovnávání zatížení, můžete rychle reagovat na změny v provozu aplikací dynamickým přidáním nebo odebráním serverů. V cloudovém prostředí, kde platíte pouze za serverové prostředky tak dlouho, dokud je skutečně používáte, může se tato schopnost reagovat na změny v poptávce promítnout do obrovských úspor.
- Webová vrstva bez stavů je architektonicky mnohem jednodušší škálovat aplikace. To také umožňuje reagovat na škálování potřeb rychleji, a utrácet méně peněz na vývoj a testování v procesu.
- Cloudové servery, jako jsou místní servery, je třeba občas opravit a restartovat; a pokud je webová vrstva bezstavová, přesměrování provozu při dočasném snížení serveru nezpůsobí chyby nebo neočekávané chování.

Většina reálných aplikací je třeba uložit stav pro webovou relaci; hlavním bodem zde není ukládat na webovém serveru. Stav můžete uložit jinými způsoby, například na straně klienta v souborech cookie nebo mimo proces na straně serveru v ASP.NET stavu relace pomocí zprostředkovatele mezipaměti. Soubory můžete ukládat v [úložišti objektů blob Windows Azure](unstructured-blob-storage.md) namísto místního systému souborů.

Jako příklad toho, jak snadné je škálovat aplikaci na webech Windows Azure, pokud je vaše webová vrstva bezstavová, najdete na kartě **Škálování** pro web Windows Azure na portálu pro správu:

![Karta Změnit velikost](web-development-best-practices/_static/image1.png)

Chcete-li přidat webové servery, stačí přetáhnout jezdec počtu instancí doprava. Nastavte ji na 5 a klikněte na **Uložit**a během několika sekund máte 5 webových serverů v systému Windows Azure, které zpracovávají provoz vašeho webu.

![Pět instancí](web-development-best-practices/_static/image2.png)

Stejně snadno můžete nastavit odpočítávání instancí na 3 nebo zpět na 1. Když se zpotovíte zpět, začnete okamžitě šetřit peníze, protože Windows Azure se účtuje podle minuty, ne podle hodiny.

Můžete také říct Windows Azure, aby automaticky zvyšoval nebo snižoval počet webových serverů na základě využití procesoru. V následujícím příkladu, když využití procesoru klesne pod 60 %, počet webových serverů se sníží na minimálně 2, a pokud využití procesoru klesne nad 80 %, počet webových serverů se zvýší až na maximálně 4.

![Škálování podle využití procesoru](web-development-best-practices/_static/image3.png)

Nebo co když víte, že vaše stránky budou zaneprázdněny pouze během pracovní doby? Windows Azure můžete říct, aby během dne spouštěl více serverů a zmenšoval se na jeden server večery, noci a víkendy. Následující série snímků obrazovky ukazuje, jak nastavit webové stránky pro spuštění jednoho serveru mimo pracovní dobu a 4 servery během pracovní doby od 8:00 do 17:00.

![Škálování podle plánu](web-development-best-practices/_static/image4.png)

![Nastavení časů plánu](web-development-best-practices/_static/image5.png)

![Denní plán](web-development-best-practices/_static/image6.png)

![Týdenní rozvrh](web-development-best-practices/_static/image7.png)

![Víkendový plán](web-development-best-practices/_static/image8.png)

A samozřejmě to vše lze provést ve skriptech i na portálu.

Možnost vaší aplikace škálovat je téměř neomezená v systému Windows Azure, pokud se vyhnete překážkám pro dynamické přidávání nebo odebírání virtuálních počítačů serveru tím, že udržujete webovou vrstvu bezstavovou.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Vyhnout se stavu relace

Často není praktické v reálné cloudové aplikaci, aby se zabránilo ukládání nějaké formy stavu pro relaci uživatele, ale některé přístupy mají vliv na výkon a škálovatelnost více než ostatní. Pokud máte uložit stav, nejlepším řešením je, aby množství stavu malé a uložit jej do cookies. Pokud to není možné, dalším nejlepším řešením je použít ASP.NET stavu relace s poskytovatelem pro [distribuované mezipaměti v paměti](distributed-caching.md#sessionstate). Nejhorší řešení z hlediska výkonu a škálovatelnosti je použít zprostředkovatele stavu relace podporované databází.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Použití sítě CDN k uložení statických datových zdrojů souborů do mezipaměti

CDN je zkratka pro Content Delivery Network. Poskytujete statické datové zdroje, jako jsou obrázky a soubory skriptů zprostředkovateli CDN a zprostředkovatel ukládá tyto soubory do mezipaměti v datových centrech po celém světě tak, aby kdekoli lidé přístup k vaší aplikaci, dostanou relativně rychlou odezvu a nízkou latenci pro prostředky uložené v mezipaměti. To urychluje celkovou dobu načítání webu a snižuje zatížení webových serverů. Sítě CDN jsou obzvláště důležité, pokud oslovujete publikum, které je geograficky široce distribuováno.

Windows Azure má CDN a další sítě CDN můžete použít v aplikaci, která běží v Systému Windows Azure nebo v jakémkoli webhostingovém prostředí.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Pomocí asynchronní podpory rozhraní .NET 4.5 se vyhnete blokování hovorů.

.NET 4.5 rozšířené c# a VB programovací jazyky, aby bylo mnohem jednodušší zpracování úloh asynchronně. Výhodou asynchronního programování není pouze pro paralelní zpracování situacích, jako je například když chcete zahájit více volání webové služby současně. Umožňuje také, aby váš webový server fungoval efektivněji a spolehlivěji za podmínek vysokého zatížení. Webový server má k dispozici pouze omezený počet vláken a za podmínek vysokého zatížení, když jsou všechna vlákna používána, příchozí požadavky musí počkat, dokud nebudou vlákna uvolněna. Pokud kód aplikace nezpracovává úlohy, jako jsou databázové dotazy a volání webové služby asynchronně, mnoho podprocesů jsou zbytečně svázané, zatímco server čeká na vstupně-o odpověď. To omezuje objem provozu, který může server zpracovat za podmínek vysokého zatížení. S asynchronní programování, vlákna, která čekají na webovou službu nebo databázi vrátit data jsou uvolněny až do služby nové požadavky, dokud jsou přijata data. Na rušném webovém serveru pak mohou být okamžitě zpracovány stovky nebo tisíce požadavků, které by jinak čekaly na uvolnění vláken.

Jak jste viděli dříve, je to tak snadné snížit počet webových serverů manipulaci s vaší webové stránky, jak je zvýšit. Pokud tedy server může dosáhnout větší propustnosti, nepotřebujete tolik z nich a můžete snížit náklady, protože pro daný objem provozu potřebujete méně serverů, než byste jinak potřebovali.

Podpora asynchronního programovacího modelu .NET 4.5 je součástí ASP.NET 4.5 pro webové formuláře, MVC a webové rozhraní API. v rozhraní Entity Framework 6 a v [rozhraní API úložiště Windows Azure](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx).

### <a name="async-support-in-aspnet-45"></a>Asynchronní podpora v ASP.NET 4.5

V ASP.NET 4.5 byla přidána podpora asynchronního programování nejen do jazyka, ale také do rozhraní MVC, Web Forms a Web API. Například metoda akce řadiče mvc ASP.NET přijímá data z webového požadavku a předá je zobrazení, které pak vytvoří html, který má být odeslán do prohlížeče. Metoda akce často potřebuje získat data z databáze nebo webové služby, aby je mohla zobrazit na webové stránce nebo uložit data zadaná na webové stránce. V těchto scénářích je snadné, aby metoda akce asynchronní: namísto vrácení *Objekt U akce,* vrátíte *&lt;Task ActionResult&gt; * a označíte metodu *asynchronním* klíčovým slovem. Uvnitř metody, když řádek kódu spustí operaci, která zahrnuje čekací dobu, označíte ji klíčovým slovem await.

Zde je jednoduchá metoda akce, která volá metodu úložiště pro databázový dotaz:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

A tady je stejná metoda, která zpracovává volání databáze asynchronně:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

Pod kryty kompilátor generuje příslušný asynchronní kód. Když aplikace provede volání `FindTaskByIdAsync`, ASP.NET `FindTask` provede požadavek a potom odpojit pracovní vlákno a zpřístupní jej ke zpracování jiného požadavku. Po `FindTask` dokončení požadavku je vlákno restartováno, aby pokračovalo ve zpracování kódu, který přichází po tomto volání. Během mezimezi při `FindTask` zahájení požadavku a při vrácení dat máte k dispozici vlákno pro užitečnou práci, která by jinak byla svázána čekáním na odpověď.

Existuje určitá režie pro asynchronní kód, ale za podmínek nízkého zatížení, že režie je zanedbatelná, zatímco za podmínek vysoké zatížení jste schopni zpracovat požadavky, které by jinak být drženy čekání na dostupná vlákna.

Bylo možné provést tento druh asynchronního programování od ASP.NET 1.1, ale bylo obtížné psát, náchylné k chybám a obtížné ladit. Nyní, když jsme zjednodušili kódování pro to v ASP.NET 4.5, není důvod, aby to už.

### <a name="async-support-in-entity-framework-6"></a>Asynchronní podpora v rámci entity 6

Jako součást asynchronní podpory v 4.5 jsme dodali asynchronní podporu pro volání webových služeb, sokety a vstupně-in souborového systému, ale nejběžnějším vzorem pro webové aplikace je přístup k databázi a naše knihovny dat nepodporovaly asynchronní. Nyní Entity Framework 6 přidává asynchronní podporu pro přístup k databázi.

V entity Framework 6 všechny metody, které způsobují dotaz nebo příkaz, který má být odeslán do databáze mají asynchronní verze. Příklad zde ukazuje asynchronní verzi *Find* metody.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

A tato asynchronní podpora funguje nejen pro vložení, odstranění, aktualizace a jednoduché nálezy, ale také pracuje s dotazy LINQ:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

Existuje `Async` verze `ToList` metody, protože v tomto kódu, která je metoda, která způsobí, že dotaz má být odeslán do databáze. Metody `Where` `OrderByDescending` a pouze konfigurovat dotaz, `ToListAsync` zatímco metoda spustí dotaz a `result` uloží odpověď v proměnné.

## <a name="summary"></a>Souhrn

Můžete implementovat osvědčené postupy pro vývoj webových aplikací popsané zde v libovolném rámci webového programování a v jakémkoli cloudovém prostředí, ale máme nástroje v ASP.NET a Windows Azure, které vám to usnadní. Pokud budete postupovat podle těchto vzorů, můžete snadno horizontální navýšení kapacity webové vrstvy a budete minimalizovat své výdaje, protože každý server bude schopen zvládnout větší provoz.

[Další kapitola](single-sign-on.md) se zabývá tím, jak cloud umožňuje scénáře jednotného přihlášení.

## <a name="resources"></a>Zdroje a prostředky

Další informace naleznete v následujících zdrojích.

Bezstátní webové servery:

- [Vzory a postupy společnosti Microsoft – pokyny k automatickému škálování](https://msdn.microsoft.com/library/dn589774.aspx).
- [Zakázání spřažení instancí ARR ve webech Windows Azure](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/). Příspěvek na blogu od Ereze Benariho vysvětluje spřažení relací ve webech Windows Azure.

Cdn:

- [FailSafe: Vytváření škálovatelných, odolných cloudových služeb](https://channel9.msdn.com/Series/FailSafe). Devítidílný video seriál ulricha Homanna, Marca Mercuriho a Marka Simmse. Podívejte se na diskuzi CDN v epizodě 3 od 1:34:00.
- [Vzor y microsoft patterns and practices static content hosting pattern pattern](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN Recenze](http://www.cdnreviews.com/). Přehled mnoha CDN.

Asynchronní programování:

- [Použití asynchronních metod v ASP.NET MVC 4](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Režie: Rick Anderson.
- [Asynchronní programování s asynchronní a Čeká (C# a Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). Dokument White Paper msdn, který vysvětluje důvody pro asynchronní programování, jak funguje v ASP.NET 4.5 a jak psát kód k jeho implementaci.
- [Asynchronní dotaz a uložit rozhraní entity Framework](https://msdn.microsoft.com/data/jj819165)
- [Jak vytvářet ASP.NET webových aplikací pomocí asynchronní](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). Videoprezentace Rowana Millera. Obsahuje grafickou ukázku toho, jak může asynchronní programování usnadnit dramatické zvýšení propustnosti webového serveru za podmínek vysokého zatížení.
- [FailSafe: Vytváření škálovatelných, odolných cloudových služeb](https://channel9.msdn.com/Series/FailSafe). Devítidílný video seriál ulricha Homanna, Marca Mercuriho a Marka Simmse. Diskuse o dopadu asynchronního programování na škálovatelnost najdete v epizodě 4 a 8.
- [Kouzlo použití asynchronních metod v ASP.NET 4,5 plus důležité gotcha](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Blogový příspěvek od Scotta Hanselmana, především o použití asynchronní v aplikacích ASP.NET Web Forms.

Další osvědčené postupy pro vývoj webových aplikací naleznete v následujících zdrojích:

- [Oprava ukázkové aplikace - osvědčené postupy](the-fix-it-sample-application.md#bestpractices). V dodatku této e-knihy je uvedena řada osvědčených postupů, které byly implementovány v aplikaci Fix It.
- [Webový seznam vývojářů](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Předchozí](continuous-integration-and-continuous-delivery.md)
> [další](single-sign-on.md)
