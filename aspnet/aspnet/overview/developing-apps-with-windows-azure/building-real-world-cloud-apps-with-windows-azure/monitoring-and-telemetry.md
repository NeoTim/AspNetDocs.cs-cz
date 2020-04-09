---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: Monitorování a telemetrie (vytváření reálných cloudových aplikací s Azure) | Dokumenty společnosti Microsoft
author: MikeWasson
description: Cloudová kniha Building Real World S Azure vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje to 13 vzorů a postupů, které může...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676032"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>Monitorování a telemetrie (vytváření reálných cloudových aplikací s Azure)

od [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Stáhnout Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stáhnout E-knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Cloudová kniha Building Real World S Azure** vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje 13 vzorů a postupů, které vám mohou pomoci úspěšně vyvíjet webové aplikace pro cloud. Informace o e-knize najdete [v první kapitole](introduction.md).

Mnoho lidí spoléhá na zákazníky, aby jim vědět, kdy jejich aplikace je dole. To není opravdu nejlepší praxe kdekoli, a to zejména ne v cloudu. Neexistuje žádná záruka rychlého oznámení, a když dostanete oznámení, často získáte minimální nebo zavádějící údaje o tom, co se stalo. Díky dobrým telemetrickým a protokolovacím systémům si můžete být vědomi toho, co se s vaší aplikací děje, a když se něco pokazí, zjistíte to hned a máte užitečné informace o řešení potíží, se kterými můžete pracovat.

## <a name="buy-or-rent-a-telemetry-solution"></a>Kupte nebo půjčte telemetrické řešení

> [!NOTE]
> Tento článek byl napsán před [Application Insights](/azure/application-insights/app-insights-overview) byl propuštěn. Application Insights je upřednostňovaný přístup pro telemetrická řešení v Azure. Další informace najdete [v tématu Nastavení přehledů aplikací pro ASP.NET web.](/azure/application-insights/app-insights-asp-net)

Jednou z věcí, která je skvělá o cloudovém prostředí, je, že je opravdu snadné koupit nebo pronajmout si cestu k vítězství. Telemetrie je příkladem. Bez velkého úsilí můžete získat opravdu dobrý telemetrický systém v provozu, velmi nákladově efektivní. Existuje spousta skvělých partnerů, kteří se integrují s Azure, a někteří z nich mají volné úrovně – takže můžete získat základní telemetrii pro nic za nic. Tady jsou jen některé z těch, které jsou v současné době dostupné v Azure:

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) také obsahuje funkce monitorování.

Rychle projdeme nastavením Nové relikvie, abychom ukázali, jak snadné může být použití telemetrického systému.

Na portálu pro správu Azure se zaregistrujte ke službě. Klepněte na tlačítko **Nový**a potom na **tlačítko Store**. Zobrazí se dialogové okno **Zvolit doplněk.** Posuňte se dolů a klepněte na **tlačítko Nová relikvie**.

![Výběr doplňku](monitoring-and-telemetry/_static/image1.png)

Klikněte na šipku vpravo a vyberte požadovanou úroveň služby. Pro tuto ukázku použijeme bezplatnou úroveň.

![Přizpůsobení doplňku](monitoring-and-telemetry/_static/image2.png)

Klikněte na šipku vpravo, potvrďte "nákup" a nová relikvie se nyní zobrazuje jako doplněk na portálu.

![Zkontrolovat nákup](monitoring-and-telemetry/_static/image3.png)

![Nový doplněk Relic na portálu pro správu](monitoring-and-telemetry/_static/image4.png)

Klikněte na **Informace o připojení**a zkopírujte licenční klíč.

![Informace o připojení](monitoring-and-telemetry/_static/image5.png)

Přejděte na kartu **Konfigurovat** pro webovou aplikaci na portálu, nastavte **sledování výkonu** na **doplněk**a nastavte rozevírací seznam **Zvolit doplněk** na **novou relikvii**. Potom klepněte na tlačítko **Uložit**.

![Nová relikvie na kartě Konfigurace](monitoring-and-telemetry/_static/image6.png)

V sadě Visual Studio nainstalujte balíček New Relic NuGet do aplikace.

![Analýza vývojářů na kartě Konfigurace](monitoring-and-telemetry/_static/image7.png)

Nasaďte aplikaci do Azure a začněte ji používat. Vytvořte několik úkolů Fix It poskytnout některé aktivity pro new relic sledovat.

Potom se vraťte na stránku **Nová relikvie** na kartě **Doplňky na** portálu a klikněte na **Spravovat**. Portál vás odešle na portál pro správu nové relikvie pomocí jednotného přihlášení pro ověřování, takže nemusíte znovu zadávat přihlašovací údaje. Stránka Přehled představuje různé statistiky výkonu. (Kliknutím na obrázek zobrazíte plnou velikost stránky s přehledem.)

[![Nová karta Sledování relikvií](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Zde jsou jen některé statistiky, které můžete vidět:

- Průměrná doba odezvy v různých denních dobách.

    ![Doba odezvy](monitoring-and-telemetry/_static/image10.png)
- Propustnost (v požadavcích za minutu) v různých denních dobách.

    ![Propustnost](monitoring-and-telemetry/_static/image11.png)
- Čas procesoru serveru strávený zpracováním různých požadavků HTTP.

    ![Časy webových transakcí](monitoring-and-telemetry/_static/image12.png)
- Čas procesoru strávený v různých částech kódu aplikace:

    ![Podrobnosti trasování](monitoring-and-telemetry/_static/image13.png)
- Statistiky historické výkonnosti.

    ![Historické představení](monitoring-and-telemetry/_static/image14.png)
- Volání externích služeb, jako je například služba Blob a statistiky o tom, jak spolehlivé a responzivní služba byla.

    ![Externí služby](monitoring-and-telemetry/_static/image15.png)

    ![Externí služby](monitoring-and-telemetry/_static/image16.png)

    ![Externí služba](monitoring-and-telemetry/_static/image17.png)
- Informace o tom, kde na světě nebo kde v USA web app provoz přišel.

    ![Geography](monitoring-and-telemetry/_static/image18.png)

Můžete také nastavit sestavy a události. Můžete například kdykoli vyslovit chyby, poslat e-mail, který upozorní pracovníky podpory na problém.

![Sestavy](monitoring-and-telemetry/_static/image19.png)

New Relic je jen jedním z příkladů telemetrického systému; můžete získat to vše z jiných služeb stejně. Krása cloudu spočte, aniž byste museli psát jakýkoli kód a za minimální nebo žádné náklady, najednou můžete získat mnohem více informací o tom, jak je vaše aplikace používána a co vaši zákazníci skutečně zažívají.

<a id="log"></a>
## <a name="log-for-insight"></a>Protokolovat pro přehled

Telemetrie balíček je dobrý první krok, ale stále máte nástroj vlastní kód. Telemetrická služba vám řekne, když je problém a řekne vám, co zákazníci zažívají, ale nemusí vám velký přehled o tom, co se děje ve vašem kódu.

Nechcete, aby se vzdáleně na produkční server, abyste viděli, co vaše aplikace dělá. To by mohlo být praktické, když máte jeden server, ale co když jste škálování na stovky serverů a nevíte, které z nich je třeba dálkové do? Protokolování by mělo poskytnout dostatek informací, které nikdy nebudete muset vzdálené do produkčních serverů analyzovat a ladit problémy. Měli byste protokolovat dostatek informací, abyste mohli izolovat problémy výhradně prostřednictvím protokolů.

### <a name="log-in-production"></a>Přihlásit se k výrobě

Mnoho lidí zapne trasování ve výrobě pouze v případě, že je problém a chtějí ladit. To může způsobit značné zpoždění mezi časem, kdy jste si vědomi problému, a časem, kdy získáte užitečné informace o řešení potíží. A informace, které získáte, nemusí být užitečné pro občasné chyby.

Co doporučujeme v cloudovém prostředí, kde je levné úložiště je, že vždy ponechat přihlášení v produkčním prostředí. Tímto způsobem, když dojde k chybám, již je máte zaznamenány a máte historická data, která vám mohou pomoci analyzovat problémy, které se vyvíjejí v průběhu času nebo se pravidelně dějí v různých časech. Můžete automatizovat proces vymazání odstranit staré protokoly, ale můžete zjistit, že je dražší nastavit takový proces, než je zachovat protokoly.

Přidané náklady na protokolování jsou triviální ve srovnání s množstvím času řešení problémů a peněz, které můžete ušetřit tím, že budete mít všechny informace, které potřebujete, již k dispozici, když se něco pokazí. Pak, když někdo řekne, že měl náhodnou chybu někdy kolem 8:00 včera v noci, ale oni si nepamatují chybu, můžete snadno zjistit, v čem byl problém.

Za méně než $ 4 za měsíc můžete mít po ruce 50 gigabajtů protokolů a dopad protokolování na výkon je triviální, pokud budete mít na paměti jednu věc - abyste se vyhnuli kritickým bodům výkonu, ujistěte se, že knihovna protokolování je asynchronní.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>Odlišit protokoly, které informují od protokolů, které vyžadují akci

Protokoly jsou určeny k INFORM (Chci, abyste něco věděli) nebo ACT (chci, abyste něco udělat). Dávejte pozor, abyste pouze psát protokoly ACT pro problémy, které skutečně vyžadují osobu nebo automatizovaný proces k akci. Příliš mnoho protokolů ACT vytvoří hluk, což vyžaduje příliš mnoho práce, aby se přes to všechno prosévalo, aby se zjistilo skutečné problémy. A pokud vaše act protokoly automaticky spustí některé akce, jako je odesílání e-mailů pro pracovníky podpory, vyhněte se nechat tisíce takových akcí být spuštěna jediným problémem.

V trasování .NET System.Diagnostics lze protokolům přiřadit úroveň Error, Warning, Info a Debug/Verbose. Můžete odlišit ACT od inform protokoly vyhrazením úroveň chyby pro act protokoly a pomocí nižší úrovně pro inform protokoly.

![Úrovně protokolování](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Konfigurace úrovní protokolování za běhu

I když stojí za to mít přihlášení vždy v produkčním prostředí, dalším osvědčeným postupem je implementovat architekturu protokolování, která umožňuje upravit za běhu úroveň podrobností, které zaznamenáváte, bez opětovného nasazení nebo restartování aplikace. Například při použití trasovací `System.Diagnostics` zařízení v můžete vytvořit error, warning, info a ladění/verbose protokoly. Doporučujeme vždy protokolovat protokoly chyb, upozornění a informací v produkčním prostředí a budete chtít být schopni dynamicky přidávat protokolování ladění/podrobnosti pro řešení potíží případ od případu.

Webové aplikace ve službě Azure App Service `System.Diagnostics` mají integrovanou podporu pro zápis protokolů do systému souborů, úložiště tabulek nebo úložiště objektů blob. Můžete vybrat různé úrovně protokolování pro každý cíl úložiště a můžete změnit úroveň protokolování za běhu bez restartování aplikace. Podpora úložiště objektů blob usnadňuje spouštění úloh [analýzy HDInsight](https://docs.microsoft.com/azure/hdinsight/) v protokolech aplikací, protože HDInsight ví, jak pracovat s úložištěm objektů Blob přímo.

### <a name="log-exceptions"></a>Protokolování výjimek

Neuvázejte jen *výjimku. ToString()* v kódu protokolování. To vynechává kontextové informace. V případě chyb SQL vynechá číslo chyby SQL. Pro všechny výjimky, zahrnout informace o kontextu, výjimku sám a vnitřní výjimky a ujistěte se, že poskytujete vše, co bude potřeba pro řešení potíží. Informace o kontextu mohou například zahrnovat název serveru, identifikátor transakce a uživatelské jméno (nikoli však heslo nebo žádné tajné klíče!).

Pokud se spoléháte na to, že každý vývojář udělá správnou věc s protokolováním výjimek, některé z nich nebudou. Chcete-li zajistit, že se dostane provedeno správným způsobem pokaždé, sestavení zpracování výjimek přímo do vašeho logger rozhraní: předat samotný objekt výjimky do logger třídy a protokolovat data výjimky správně v logger třídy.

### <a name="log-calls-to-services"></a>Protokolovat volání služeb

Důrazně doporučujeme, abyste zápis protokolu pokaždé, když vaše aplikace volá do služby, ať už je to do databáze nebo rozhraní REST API nebo externí služby. Zahrnout do protokolů nejen údaj o úspěchu nebo neúspěchu, ale jak dlouho každý požadavek trval. V cloudovém prostředí se často zobrazují problémy související se zpomalením, nikoli úplné výpadky. Něco, co normálně trvá 10 milisekund, může náhle začít trvat vteřinu. Když vám někdo řekne, že vaše aplikace je pomalá, chcete mít možnost podívat se na New Relic nebo jakoukoli telemetrická službu, kterou máte, a ověřit jejich zkušenosti, a pak chcete mít možnost hledat jsou vaše vlastní protokoly, které se ponořují do podrobností o tom, proč je to pomalé.

### <a name="use-an-ilogger-interface"></a>Použití rozhraní ILogger

Co doporučujeme dělat při vytváření produkční aplikace je vytvořit jednoduchý *ILogger* rozhraní a držet některé metody v něm. To usnadňuje změnu implementace protokolování později a není nutné projít všechny kód k tomu. Mohli bychom `System.Diagnostics.Trace` používat třídu v celé aplikaci Fix It, ale místo toho ji používáme pod kryty ve třídě protokolování, která implementuje *ILogger*, a provádíme volání metod *ILogger* v celé aplikaci.

Tímto způsobem, pokud budete někdy chtít, aby [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) vaše protokolování bohatší, můžete nahradit bez ohledu na protokolování mechanismus, který chcete. Například, jak vaše aplikace roste, můžete se rozhodnout, že chcete použít komplexnější protokolování balíček, jako je [NLog](http://nlog-project.org/) nebo [Enterprise Library Protokolování application Block](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx). [(Log4Net](http://logging.apache.org/log4net/) je další populární protokolování rámce, ale to nedělá asynchronní protokolování.)

Jedním z možných důvodů pro použití rozhraní, jako je NLog je usnadnit rozdělení výstupu protokolování do samostatných úložišť dat s vysokou objema a vysokou hodnotou. To vám pomůže efektivně ukládat velké objemy dat INFORM, které nepotřebujete provádět rychlé dotazy, při zachování rychlého přístupu k datům ACT.

### <a name="semantic-logging"></a>Sémantické protokolování

Relativně nový způsob protokolování, které mohou vytvářet užitečnější diagnostické informace, naleznete v [tématu Enterprise Library Sémantic Logging Application Block (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). SLAB používá [trasování událostí pro Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) a [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) podporu v .NET 4.5, které vám umožní vytvořit strukturovanější a dotazovatelné protokoly. Pro každý typ události, kterou protokolujete, definujete jinou metodu, která umožňuje přizpůsobit informace, které píšete. Chcete-li například protokolovat chybu databáze `LogSQLDatabaseError` SQL, můžete volat metodu. Pro tento druh výjimky víte, že klíčovou informací je číslo chyby, takže můžete zahrnout parametr čísla chyby do podpisu metody a zaznamenat číslo chyby jako samostatné pole do záznamu protokolu, který píšete. Vzhledem k tomu, že číslo je v samostatném poli můžete snadněji a spolehlivěji získat sestavy na základě čísel chyb SQL, než byste mohli, pokud jste právě zřetězili číslo chyby do řetězce zprávy.

## <a name="logging-in-the-fix-it-app"></a>Protokolování aplikace Fix It

### <a name="the-ilogger-interface"></a>Rozhraní ILogger

Zde je rozhraní *ILogger* v aplikaci Fix It.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Tyto metody umožňují zápis protokolů na stejné čtyři úrovně podporované *System.Diagnostics*. Metody TraceApi jsou určeny pro protokolování volání externí služby s informacemi o latenci. Můžete také přidat sadu metod pro úroveň ladění/verbose.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>Implementace loggeru rozhraní ILogger

Implementace rozhraní je opravdu jednoduchá. Je to v podstatě jen volá do *standardnísystem.Diagnostics* metody. Následující úryvek zobrazuje všechny tři metody Informace a jednu druhou.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>Volání metod ILogger

Pokaždé, když kód v aplikaci Fix It zachytí výjimku, volá metodu *ILogger* pro protokolování podrobností o výjimce. A pokaždé, když provede volání do databáze, služby Blob nebo rozhraní REST API, spustí stopky před voláním, zastaví stopky při vrácení služby a zaznamená uplynulý čas spolu s informacemi o úspěchu nebo neúspěchu.

Všimněte si, že zpráva protokolu obsahuje název třídy a název metody. Je vhodné zajistit, aby zprávy protokolu určit, která část kódu aplikace je napsal.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Takže teď pokaždé, když fix It aplikace provedla volání do databáze SQL, můžete vidět volání, metodu, která ji volala, a přesně kolik času trvalo.

![Dotaz databáze SQL v protokolech](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Pokud procházíte protokoly, uvidíte, že volání databáze času je variabilní. Tyto informace by mohly být užitečné: protože aplikace zaznamenává to vše můžete analyzovat historické trendy v tom, jak databázová služba funguje v průběhu času. Služba může být například po většinu času rychlá, ale požadavky mohou selhat nebo odpovědi mohou zpomalit v určitých denních dobách.

Totéž můžete udělat pro službu Blob – pokaždé, když aplikace nahraje nový soubor, je tu protokol a můžete přesně vidět, jak dlouho trvalo nahrát každý soubor.

![Protokol nahrávání objektů blob](monitoring-and-telemetry/_static/image23.png)

Je to jen pár řádků kódu navíc k napsání pokaždé, když zavoláte službu, a teď, když někdo říká, že narazil na problém, víte přesně, co to bylo, zda to byla chyba, nebo i když to bylo jen běží pomalu. Můžete určit zdroj problému, aniž byste museli vzdáleni do serveru nebo zapnout protokolování po chybě a doufat, že ji znovu vytvoříte.

## <a name="dependency-injection-in-the-fix-it-app"></a>Vkládání závislostí v aplikaci Fix It

Možná se divíte, jak konstruktor úložiště v příkladu uvedeném výše získá implementaci rozhraní protokolovacího nástroje:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Chcete-li připojit rozhraní k implementaci aplikace používá [vkládání závislostí](http://en.wikipedia.org/wiki/Dependency_injection)(DI) s [AutoFac](http://autofac.org/). DI umožňuje používat objekt založený na rozhraní na mnoha místech v celém kódu a pouze zadat na jednom místě implementaci, která se používá při vytvoření instance rozhraní. To usnadňuje změnu implementace: například můžete chtít nahradit System.Diagnostics logger s Protokolovacího protokolu NLog. Nebo pro automatizované testování můžete chtít nahradit falešnou verzi protokolovacího nástroje.

Aplikace Fix It používá DI ve všech úložištích a ve všech řadičích. Konstruktory tříd řadiče získají rozhraní *ITaskRepository* stejným způsobem jako úložiště získá rozhraní protokolovacího nástroje:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

Aplikace používá knihovnu AutoFac DI k automatickému poskytování instancí *TaskRepository* a *Logger* pro tyto konstruktory.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Tento kód v podstatě říká, že kdekoli konstruktor potřebuje rozhraní *ILogger,* předat v instanci *Logger* třídy a kdykoli potřebuje *rozhraní IFixItTaskRepository,* předat v instanci *Třídy FixItTaskRepository.*

[AutoFac](http://autofac.org/) je jedním z mnoha rozhraní vkládání závislostí, které můžete použít. Dalším populárním je [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), který je doporučen a podporován Microsoft Patterns and Practices.

## <a name="built-in-logging-support-in-azure"></a>Integrovaná podpora protokolování v Azure

Azure podporuje následující druhy [protokolování pro webové aplikace ve službě Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- System.Diagnostics trasování (můžete zapnout a vypnout a nastavit úrovně za běhu bez restartování webu).
- Události systému Windows.
- Protokoly IIS (HTTP/FREB).

Azure podporuje následující druhy [protokolování v cloudových službách:](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)

- Sledování systému.
- Čítače výkonu.
- Události systému Windows.
- Protokoly IIS (HTTP/FREB).
- Vlastní monitorování adresářů.

Aplikace Fix It používá trasování System.Diagnostics. Vše, co musíte udělat, abyste povolili protokolování System.Diagnostics ve webové aplikaci, je překlopit přepínač na portálu nebo zavolat ROZHRANÍ REST API. Na portálu klikněte na kartu **Konfigurace** webu a posuňte se dolů a podívejte se na část **Diagnostika aplikací.** Přihlášení můžete zapnout nebo vypnout a vybrat požadovanou úroveň protokolování. Azure může protokoly zapsat do systému souborů nebo do účtu úložiště.

![Diagnostika aplikací a diagnostika webu na kartě Konfigurace](monitoring-and-telemetry/_static/image24.png)

Po povolení protokolování v Azure, uvidíte protokoly v okně Visual Studio Výstup, jak jsou vytvořeny.

![Nabídka Streamovací protokoly](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Nabídka Streamovací protokoly](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Můžete také mít protokoly zapsány do vašeho účtu úložiště a zobrazit je pomocí libovolného nástroje, který má přístup ke službě Azure Storage Table, jako je **Průzkumník serveru** v Visual Studiu nebo Průzkumník [úložiště Azure](https://azure.microsoft.com/features/storage-explorer/).

![Protokoly v Průzkumníkovi serveru](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Souhrn

Je to opravdu jednoduché implementovat out-of-the-box telemetrický systém, nástroj protokolování ve vlastním kódu a konfigurace protokolování v Azure. A když máte problémy s výrobou, kombinace telemetrického systému a vlastních protokolů vám pomůže rychle vyřešit problémy dříve, než se stanou hlavními problémy pro vaše zákazníky.

V [další kapitole](transient-fault-handling.md) se podíváme na to, jak zpracovat přechodné chyby, aby se nestaly problémy s výrobou, které musíte prozkoumat.

## <a name="resources"></a>Zdroje a prostředky

Další informace najdete v následujících materiálech.

Dokumentace především o telemetrii:

- [Vzory a postupy microsoftu – pokyny k Azure](https://msdn.microsoft.com/library/dn568099.aspx). Viz Pokyny k instrumentaci a telemetrii, pokyny pro měření služeb, vzor sledování koncových bodů stavu a vzor změny konfigurace za běhu.
- [Penny Sevření v cloudu: Povolení nového monitorování výkonu relikvií na webech Azure](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx).
- [Doporučené postupy pro návrh rozsáhlých služeb ve cloudových službách Azure](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Bílá kniha Marka Simmse a Michaela Thomassyho. Viz část Telemetrie a diagnostika.
- [Vývoj nové generace s přehledy aplikací](https://msdn.microsoft.com/magazine/dn683794.aspx). MSDN Časopis článek.

Dokumentace především o protokolování:

- [Sémantické protokolování aplikační blok (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neil Mackenzie představuje případ pro sémantické protokolování s SLAB.
- [Vytváření strukturovaných a smysluplných protokolů se sémantickým protokolováním](https://channel9.msdn.com/Events/Build/2013/3-336). (Video) Julian Dominguez představuje případ pro sémantické protokolování s SLAB.
- [EF6 SQL Protokolování – Část 1: Jednoduché protokolování](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). Arthur Vickers ukazuje, jak protokolovat dotazy spouštěné entity frameworku v EF 6.
- [Odolnost proti chybám připojení a příkazové zachycení s rozhraním entity v ASP.NET aplikaci MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Čtvrtý v devítidílné série kurz, ukazuje, jak používat EF 6 příkaz zachycení funkce protokolu SQL příkazy odeslané do databáze entity framework.
- [Zlepšit protokolování pomocí C# 5.0 atributy informací o volajícím](http://www.dotnetcurry.com/showarticle.aspx?ID=972). Jak snadno protokolovat název volající metody bez pevného kódování do literálu nebo pomocí reflexe, abyste jej získali ručně.

Dokumentace především o řešení problémů:

- [Azure Poradce &amp; při potížích ladění blog](https://blogs.msdn.com/b/kwill/).
- [AzureTools – diagnostický nástroj používaný týmem podpory pro vývojáře Azure](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true). Zavádí a poskytuje odkaz ke stažení pro nástroj, který lze použít na virtuálním počítači Azure ke stažení a spuštění široké škály diagnostických a monitorovacích nástrojů. Užitečné, když potřebujete diagnostikovat problém na konkrétním virtuálním počítači.
- [Poradce při potížích s webovou aplikací ve službě Azure App Service pomocí Visual Studia](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). Podrobný kurz pro začínáme s trasování System.Diagnostics a vzdálené ladění.

Videa:

- [FailSafe: Vytváření škálovatelných, odolných cloudových služeb](https://channel9.msdn.com/Series/FailSafe). Devítidílný seriál Ulricha Homanna, Marca Mercuriho a Marka Simmse. Představuje koncepty na vysoké úrovni a architektonické principy velmi přístupným a zajímavým způsobem, s příběhy z prostředí Microsoft Customer Advisory Team (CAT) se skutečnými zákazníky. Epizody 4 a 9 jsou o monitorování a telemetrii. Epizoda 9 obsahuje přehled monitorovacích služeb MetricsHub, AppDynamics, New Relic a PagerDuty.
- [Building Big: Poučení od zákazníků Azure – část II](https://channel9.msdn.com/Events/Build/2012/3-030). Mark Simms hovoří o navrhování pro selhání a instrumentace všechno. Podobně jako série Failsafe, ale jde do více jak-na detaily.

Ukázka kódu:

- [Základy cloudových služeb v Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace vytvořená týmem zákaznického poradenství Microsoft Azure. Ukazuje telemetrie a protokolování postupy, jak je vysvětleno v následujících článcích. Ukázka implementuje protokolování aplikací pomocí [NLog](http://nlog-project.org/). Související dokumentaci najdete v [sérii čtyř článků wiki technetu o telemetrii a protokolování](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon).

> [!div class="step-by-step"]
> [Předchozí](design-to-survive-failures.md)
> [další](transient-fault-handling.md)
