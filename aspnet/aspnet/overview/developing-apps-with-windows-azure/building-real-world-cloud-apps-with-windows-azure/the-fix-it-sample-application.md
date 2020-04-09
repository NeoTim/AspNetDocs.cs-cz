---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Dodatek: Ukázková aplikace Fix It (vytváření cloudových aplikací v reálném světě s Azure) | Dokumenty společnosti Microsoft'
author: MikeWasson
description: Cloudová kniha Building Real World S Azure vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje to 13 vzorů a postupů, které může...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675990"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Dodatek: Ukázková aplikace Fix It (vytváření cloudových aplikací v reálném světě s Azure)

od [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Stáhněte si projekt Fix It](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **Cloudová kniha Building Real World S Azure** vychází z prezentace vyvinuté Scottem Guthriem. Vysvětluje 13 vzorů a postupů, které vám mohou pomoci úspěšně vyvíjet webové aplikace pro cloud. Informace o e-knize najdete [v první kapitole](introduction.md).

Tento dodatek k elektronické knize Building Real World Cloud Apps s azure e-book obsahuje následující části, které poskytují další informace o ukázkové aplikaci Fix It, kterou si můžete stáhnout:

- [Známé problémy](#knownissues)
- [Osvědčené postupy](#bestpractices)
- [Jak spustit aplikaci z Visual Studia v místním počítači](#run-in-vs)
- [Jak nasadit základní aplikaci do webových aplikací Služby aplikací Azure App Service pomocí skriptů Windows PowerShell](#deploybase)
- [Poradce při potížích se skripty prostředí Windows PowerShell](#troubleshooting)
- [Jak nasadit aplikaci se zpracováním fronty do webových aplikací Služby App Service Azure a cloudové služby Azure](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Známé problémy

Aplikace Fix It byla původně vyvinuta s cílem co nejjednodušeji ilustrovat některé vzory prezentované v této e-knize. Nicméně, protože e-kniha je o budování reálných aplikací, podrobili jsme kód Fix It procesu kontroly a testování podobnému tomu, co bychom udělali pro uvolněný software. Našli jsme řadu problémů, a stejně jako u všech reálných aplikací, některé z nich jsme opravili a některé z nich jsme odložili na pozdější verzi.

Následující seznam obsahuje problémy, které by měly být řešeny v produkční aplikaci, ale z toho či onoho důvodu jsme se rozhodli neřešit v počáteční verzi ukázkové aplikace Fix It.

### <a name="security"></a>Zabezpečení

- Ujistěte se, že nemůžete přiřadit úkol neexistujícímu vlastníkovi.
- Ujistěte se, že můžete zobrazit a upravit pouze úkoly, které jste vytvořili nebo které jsou vám přiřazeny.
- Pro přihlašovací stránky a ověřovací soubory cookie použijte protokol HTTPS.
- Zadejte časový limit pro ověřovací soubory cookie.

### <a name="input-validation"></a>Ověření vstupu

Obecně platí, že produkční aplikace by provést více ověření vstupu než fix it aplikace. Například velikost obrázku / velikost souboru obrázku povolená pro nahrávání by měla být omezena.

### <a name="administrator-functionality"></a>Funkce správce

Správce by měl mít možnost změnit vlastnictví existujících úkolů. Tvůrce úkolu může například opustit společnost a ponechat nikomu oprávnění k údržbě úkolu, pokud není povolen přístup správce.

### <a name="queue-message-processing"></a>Zpracování zpráv fronty

Zpracování zpráv fronty v aplikaci Fix It bylo navrženo tak, aby bylo jednoduché, aby ilustrovalo pracovní vzor zaměřený na frontu s minimálním množstvím kódu. Tento jednoduchý kód by nebyl adekvátní pro skutečnou produkční aplikaci.

- Kód nezaručuje, že každá zpráva fronty bude zpracována maximálně jednou. Když se zobrazí zpráva z fronty, je časový čas, během kterého je zpráva neviditelná pro ostatní posluchače fronty. Pokud vyprší časový limit před odstraněním zprávy, zpráva se znovu zobrazí. Proto pokud instance role pracovního procesu stráví dlouhou dobu zpracování zprávy, je teoreticky možné, aby se stejná zpráva zpracovala dvakrát, což má za následek duplicitní úlohu v databázi. Další informace o tomto problému najdete [v tématu použití front úložiště Azure](https://msdn.microsoft.com/library/ff803365.aspx#sec7).
- Logika dotazování fronty může být nákladově efektivnější, a to dávkou načítání zpráv. Pokaždé, když zavoláte [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), je transakční náklady. Místo toho můžete volat [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (všimněte si množného čísla 's'), který získá více zpráv v jedné transakci. Transakční náklady na fronty úložiště Azure jsou velmi nízké, takže dopad na náklady není ve většině scénářů podstatný.
- Těsná smyčka ve frontě kódu zpracování zpráv způsobí spřažení procesoru, který nevyužívá vícejádrové virtuální počítače efektivně. Lepší návrh by použít paralelismus úlohy spustit několik asynchronních úloh paralelně.
- Zpracování zpráv fronty má pouze základní zpracování výjimek. Například kód nezpracovává [poškozená zprávy](https://msdn.microsoft.com/library/ms789028.aspx). (Pokud zpracování zprávy způsobí výjimku, budete muset protokolovat chybu a odstranit zprávu, nebo role pracovního procesu se pokusí zpracovat znovu a smyčka bude pokračovat po neomezenou dobu.)

### <a name="sql-queries-are-unbounded"></a>Dotazy SQL jsou neohraničené.

Aktuální fix It kód umístí žádné omezení na kolik řádků dotazy pro index stránky může vrátit. Pokud je do databáze zadán velký objem úkolů, může velikost přijatých výsledných seznamů způsobit problémy s výkonem. Řešením je implementovat stránkování. Příklad najdete v tématu [Řazení, filtrování a stránkování pomocí entity frameworku v ASP.NET aplikace MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).

### <a name="view-models-recommended"></a>Zobrazit doporučené modely

Aplikace Fix It používá třídu entity FixItTask k předání informací mezi řadičem a zobrazením. Osvědčeným postupem je použití modelů zobrazení. Model domény (např. třída entity FixItTask) je navržen podle toho, co je potřeba pro trvalost dat, zatímco model zobrazení může být navržen pro prezentaci dat. Další informace naleznete [v tématu 12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).

### <a name="secure-image-blob-recommended"></a>Doporučujeme zabezpečený objekt blob obrázku

Aplikace Fix It ukládá nahrané obrázky jako veřejné, což znamená, že každý, kdo najde adresu URL, má přístup k obrázkům. Obrázky by mohly být zabezpečeny místo veřejné.

### <a name="no-powershell-automation-scripts-for-queues"></a>Žádné skripty automatizace prostředí PowerShell pro fronty

Ukázkové skripty automatizace Prostředí PowerShell byly napsány jenom pro základní verzi fix it, která běží výhradně ve webových aplikacích Služby Azure App Service. Nezadali jsme skripty pro nastavení a nasazení do webové aplikace a prostředí cloudové služby, které jsou nutné pro zpracování fronty.

### <a name="special-handling-for-html-codes-in-user-input"></a>Speciální zpracování kódů HTML v uživatelském vstupu

ASP.NET automaticky zabraňuje mnoha způsobům, jakými se uživatelé se zlými úmysly mohou pokoušet o útoky skriptování mezi weby zadáním skriptu do textových polí pro vstup uživatele. A pomocník MVC `DisplayFor` slouží k zobrazení názvy úkolů a poznámky automaticky HTML-kóduje hodnoty, které odešle do prohlížeče. Ale v produkční aplikaci možná budete chtít přijmout další opatření. Další informace naleznete [v tématu Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).

<a id="bestpractices"></a>
## <a name="best-practices"></a>Osvědčené postupy

Následují některé problémy, které byly opraveny po zjištění v kontrole kódu a testování původní verze aplikace Fix It. Některé byly způsobeny tím, že původní kodér si nebyl vědom konkrétního osvědčeného postupu, některé jednoduše proto, že kód byl napsán rychle a nebyl určen pro uvolněný software. Uvádíme zde problémy v případě, že je něco, co jsme se naučili z této recenze a testování, které by mohly být užitečné pro ostatní, kteří také vyvíjejí webové aplikace.

### <a name="dispose-the-database-repository"></a>Likvidace úložiště databáze

Třída `FixItTaskRepository` musí dispose entity `DbContext` framework instance. Udělali jsme to `IDisposable` implementací ve `FixItTaskRepository` třídě:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

Všimněte si, že AutoFac automaticky vykáže `FixItTaskRepository` instanci, takže ji nemusíme explicitně vyřadit.

Další možností je `DbContext` odebrat `FixItTaskRepository`členovou proměnnou `DbContext` z a místo toho vytvořit `using` místní proměnnou v rámci každé metody úložiště uvnitř příkazu. Příklad:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Registrovat singletons jako takové s DI

Vzhledem k tomu, `PhotoService` `Logger` že je potřeba pouze jedna instance třídy a třídy, tyto třídy by měly být [registrovány jako jednotlivé instance pro vkládání závislostí](https://code.google.com/p/autofac/wiki/InstanceScope) v *DependenciesConfig.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Zabezpečení: Nezobrazovat uživatelům podrobnosti o chybě

Původní aplikace Fix It neměla obecnou chybovou stránku a nechala všechny výjimky vybřednout do ui, takže některé výjimky, jako jsou chyby připojení k databázi, by mohly vést k zobrazení úplného trasování zásobníku do prohlížeče. Podrobné informace o chybách mohou někdy usnadnit útoky uživatelů se zlými úmysly. Řešením je protokolovat podrobnosti o výjimce a zobrazit uživateli chybovou stránku, která neobsahuje podrobnosti o chybě. Aplikace Fix It se již přihlašovala a `<customErrors mode=On>` aby bylo možné zobrazit chybovou stránku, přidali jsme ji do souboru Web.config.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Ve výchozím nastavení je *zobrazení\Shared\Error.cshtml* zobrazena u chyb. Můžete přizpůsobit *Error.cshtml* nebo vytvořit vlastní zobrazení `defaultRedirect` chybové stránky a přidat atribut. Můžete také zadat různé chybové stránky pro konkrétní chyby.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Zabezpečení: povolit pouze úkol, který má být editován jeho tvůrce

Stránka Index řídicího panelu zobrazuje pouze úkoly vytvořené přihlášeným uživatelem, ale uživatel se zlými úmysly může vytvořit adresu URL s ID pro úlohu jiného uživatele. Přidali jsme kód v *DashboardController.cs* vrátit 404 v tomto případě:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>Nepolykejte výjimky

Původní fix It aplikace právě vrátil nulu po protokolování výjimku, která vyplývá z dotazu SQL:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

To by to vypadat na uživatele, jako by dotaz proběhl úspěšně, ale prostě nevrátil žádné řádky. Řešení je znovu vyvolat výjimku po zachycení a protokolování:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Zachytit všechny výjimky v rolích pracovního procesu

Všechny neošetřené výjimky v roli pracovního procesu způsobí, že virtuální ho disponizuje, takže chcete zabalit vše, co děláte v bloku try-catch a zpracovat všechny výjimky.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Určit délku pro vlastnosti řetězce ve třídách entit

Aby bylo možné zobrazit jednoduchý kód, původní verze fix it aplikace nespecifikoval délky pro pole FixItTask entity a v důsledku toho byly definovány jako varchar(max) v databázi. V důsledku toho by uI přijmout téměř jakékoli množství vstupů. Určení délek nastaví omezení, která platí pro vstup uživatele na webové stránce i velikost sloupce v databázi:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Označit soukromé členy jako jen pro čtení, pokud se neočekává jejich změna

Například ve `DashboardController` třídě `FixItTaskRepository` instance je vytvořena a neočekává se, že se změní, takže jsme ji [definovali](https://msdn.microsoft.com/library/acdd6hb7.aspx)jako jen pro čtení .

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Použijte seznam. Any() místo seznamu. Počet() &gt; 0

Pokud vás zajímá jen to, zda jedna nebo více položek v seznamu odpovídá zadaným kritériím, použijte metodu [Any,](https://msdn.microsoft.com/library/bb534972.aspx) protože se vrátí, jakmile je nalezena položka odpovídající kritériím, zatímco `Count` metoda musí vždy iterovat každou položku. Soubor *Dashboard Index.cshtml* měl původně tento kód:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Změnili jsme to na toto:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>Generování adres URL v zobrazeních MVC pomocí pomocníků MVC

U tlačítka **Vytvořit fix it** na domovské stránce aplikace Fix It pevně zakódovala kotevní prvek:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

Pro zobrazení / akce odkazy, jako je tento, je lepší použít [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML pomocník, například:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Použít Task.Delay místo Thread.Sleep v roli pracovního procesu

Šablona nového `Thread.Sleep` projektu vloží do ukázkového kódu pro roli pracovního procesu, ale příčinou spánku vlákna může způsobit, že fond vláken vytvoří další nepotřebná vlákna. Můžete se tomu vyhnout pomocí [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) místo.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Vyhněte se asynchronní neplatné

Pokud asynchronní metoda není nutné vrátit hodnotu, `Task` vrátí `void`typ spíše než .

Tento příklad je `FixItQueueManager` z třídy:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

Měli byste `async void` použít pouze pro obslužné rutiny událostí nejvyšší úrovně. Pokud definujete metodu jako `async void`, volající nemůže **čekat** na metodu nebo zachytit žádné výjimky metoda vyvolá. Další informace naleznete [v tématu Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>Použití tokenu zrušení k přerušení smyčky role pracovní ho diody

Metoda **Run** v roli pracovního procesu obvykle obsahuje nekonečnou smyčku. Když je role pracovního procesu zastavení, je volána metoda [RoleEntryPoint.OnStop.](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) Tuto metodu byste měli použít ke zrušení práce, která se provádí uvnitř **Run** metody a řádně ukončit. V opačném případě může být proces ukončen uprostřed operace.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Odhlásit se z automatického postupu čichání MIME

V některých případech aplikace Internet Explorer hlásí jiný typ MIME, než jaký je určen webovým serverem. Pokud například aplikace Internet Explorer najde obsah HTML v souboru dodaném s hlavičkou content-type: text/plain v záhlaví odpovědi HTTP, aplikace Internet Explorer rozhodne, že obsah by měl být vykreslen jako HTML. Bohužel, tento "MIME-sniffing" může také vést k bezpečnostním problémům pro servery hostující nedůvěryhodný obsah. V boji proti tomuto problému, Internet Explorer 8 provedla řadu změn mime-typ určení kódu a umožňuje vývojářům aplikací [odhlásit mime-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx). Do souboru *Web.config* byl přidán následující kód.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Povolit sdružování a minifikaci

Když Visual Studio vytvoří nový webový projekt, není ve výchozím nastavení povoleno sdružování a minifikace souborů JavaScriptu. Přidali jsme řádek kódu v BundleConfig.cs:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Nastavení časového času vypršení platnosti ověřovacích souborů cookie

Ve výchozím nastavení vyprší platnost ověřovacích souborů cookie za dva týdny. Kratší doba je bezpečnější. Toto nastavení můžete změnit v *StartupAuth.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>Jak spustit aplikaci z Visual Studia v místním počítači

Aplikaci Fix It lze spustit dvěma způsoby:

- Spusťte základní aplikaci, která zapisuje nové úlohy přímo do databáze SQL.
- Spusťte aplikaci pomocí fronty a back-endové služby k vytvoření úloh. Vzor fronty je popsán v kapitole [Vzor práce zaměřené na frontu](queue-centric-work-pattern.md).

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Spuštění základní aplikace

1. Nainstalujte [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. Nainstalujte [sadu Azure SDK pro rozhraní .NET pro Visual Studio](https://azure.microsoft.com/downloads/).
3. Stáhněte soubor ZIP z [Galerie kódů MSDN](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).
4. V Průzkumníkovi souborů klikněte pravým tlačítkem myši na soubor ZIP a potom klikněte na Vlastnosti a potom v okně Vlastnosti klikněte na Odblokovat.
5. Rozbalte soubor.
6. Poklepáním na soubor .sln spusťte visual studio.
7. V nabídce **Nástroje** klepněte na položku **NuGet Package Manager**a potom na **konzolu Správce balíčků**.
8. V konzole Správce balíčků (PMC) klikněte na Obnovit.
9. Ukončete visual studio.
10. Spusťte [emulátor úložiště Azure](/azure/storage/common/storage-use-emulator).
11. Restartujte visual studio a otevřete soubor řešení, který jste zavřeli v předchozím kroku.
12. Ujistěte se, že projekt FixIt je nastaven jako projekt po spuštění a potom stisknutím kombinace kláves CTRL+F5 projekt spusťte.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Spuštění aplikace se zpracováním fronty

1. Postupujte podle pokynů pro [Spuštění základní aplikace](#runbase)a zavřete prohlížeč a zavřete Visual Studio.
2. Spusťte Visual Studio s oprávněními správce. (Budete používat výpočetní emulátor Azure a to vyžaduje oprávnění správce.)
3. V souboru *Web.config* aplikace v projektu *MyFixIt* (webový `appSettings/UseQueues` projekt) změňte hodnotu na hodnotu "true":

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Pokud [emulátor úložiště Azure](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) není pořád spuštěný, spusťte ho znovu.
5. Spusťte webový projekt FixIt a projekt MyFixItCloudService současně.

    Použití sady Visual Studio:

   1. Stisknutím **klávesy F5** spusťte projekt FixIt.
   2. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt MyFixItCloudService a potom klepněte na příkaz **Ladění** > **spustit novou instanci**.

    Použití aplikace Visual Studio 2013 Express pro web:

   3. V Průzkumníku řešení klepněte pravým tlačítkem myši na řešení FixIt a vyberte **příkaz Vlastnosti**.
   4. Vyberte **více projektů po spuštění**.
   5. V rozevíracím seznamu **Akce** v části MyFixIt a MyFixItCloudService vyberte **Spustit**.
   6. Klikněte na tlačítko **OK**.
   7. Stiskněte klávesu **F5** a oba projekty se spustí.

      Když spustíte projekt MyFixItCloudService, Visual Studio spustí azure compute emulátor. V závislosti na konfiguraci brány firewall může být nutné povolit emulátor prostřednictvím brány firewall.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Jak nasadit základní aplikaci do webových aplikací Služby aplikací Azure App Service pomocí skriptů Windows PowerShell

Pro ilustraci [automatizovat vše](automate-everything.md) vzor, fix It aplikace je dodáván se skripty, které nastavují prostředí v Azure a nasadit projekt do nového prostředí. Následující pokyny vysvětlují, jak používat skripty.

Pokud chcete spustit v Azure bez použití front a provedené změny spustit místně s frontami, ujistěte se, že jste nastavili UseQueues appSetting hodnotu zpět na false před pokračováním s následujícími pokyny.

Tyto pokyny předpokládají, že jste už stáhli a spusťte řešení Fix It místně a že máte účet Azure nebo máte předplatné Azure, které máte oprávnění ke správě.

1. Nainstalujte konzolu **Azure PowerShell.** Pokyny najdete v tématu [Jak nainstalovat a nakonfigurovat Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).

    Tato přizpůsobená konzola je nakonfigurovaná pro práci s vaším předplatným Azure. Modul Azure se nainstaluje do adresáře *Program Files* a automaticky se importuje při každém použití konzoly Azure PowerShell.

    Pokud dáváte přednost práci v jiném hostitelském programu, jako je například Windows PowerShell ISE, nezapomeňte použít rutinu [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) k importu modulu Azure nebo pomocí příkazu v modulu Azure k aktivaci automatického importu modulu.
2. Spusťte Azure PowerShell s možností **Spustit jako správce.**
3. Spusťte rutinu [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) a nastavte zásadu `RemoteSigned`spuštění prostředí Azure PowerShell na . Chcete-li změnu zásad dokončit, zadejte **y** (pro ano).

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Toto nastavení umožňuje spouštět místní skripty, které nejsou digitálně podepsané. (Můžete také nastavit zásady `Unrestricted`spuštění na , což by eliminovalo potřebu odblokovat krok později, ale to se nedoporučuje z bezpečnostních důvodů.)
4. Spusťte rutinu `Add-AzureAccount` a nastavte PowerShell s přihlašovacími údaji pro váš účet.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Platnost těchto pověření vyprší po určité době a je `Add-AzureAccount` třeba rutinu znovu spustit. Jak se tato e-kniha píše, časový limit před vypršením platnosti přihlašovacích údajů je 12 hodin.
5. Pokud máte více předplatných, použijte rutinu Select-AzureSubscription k určení předplatného, ve kterém chcete vytvořit testovací prostředí.
6. Importujte certifikát správy pro stejné předplatné `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` Azure pomocí rutin a rutin. První z těchto rutin stáhne soubor certifikátu a ve druhém zadáte umístění tohoto souboru, aby se importoval. > [!IMPORTANT]
   > Uchovávejte stažený soubor na bezpečném místě nebo ho po dokončení ho odstraňte, protože obsahuje certifikát, který lze použít ke správě služeb Azure.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    Certifikát se používá pro volání rozhraní REST API, které detekuje ip adresu vývojového počítače za účelem nastavení pravidla brány firewall na serveru SQL Database.
7. Spusťte rutinu [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) (aliasy jsou `cd`, `chdir`a ) a `sl`přejděte do adresáře, který obsahuje skripty. (Jsou umístěny ve složce *Automatizace* ve složce řešení Fix It.) Pokud některý z názvů adresářů obsahuje mezery, vložte cestu do uvozovek. Chcete-li například `c:\Sample Apps\FixIt\Automation` přejít do adresáře, můžete zadat následující příkaz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Chcete-li povolit spuštění těchto skriptů prostředím Windows PowerShell, použijte rutinu [Odblokovat soubor.](https://go.microsoft.com/fwlink/p/?linkid=294021) (Skripty jsou blokovány, protože byly staženy z Internetu.)

    > [!WARNING]
    > Zabezpečení - `Unblock-File` Před spuštěním libovolného skriptu nebo spustitelného souboru otevřete soubor v programu Poznámkový blok, zkontrolujte příkazy a ověřte, zda neobsahují žádný škodlivý kód.

    Například následující příkaz spustí `Unblock-File` rutinu na všech skriptech v aktuálním adresáři.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Chcete-li vytvořit webovou aplikaci pro základní (bez zpracování front) Opravit aplikaci, spusťte skript pro vytváření prostředí.

    Požadovaný `Name` parametr určuje název databáze a používá se také pro účet úložiště, který skript vytvoří. Název musí být globálně jedinečný v rámci domény azurewebsites.net. Pokud zadáte název, který není jedinečný, jako fixit nebo test (nebo dokonce `New-AzureWebsite` jako v příkladu fixitdemo), rutina selže s vnitřní chybou, která hlásí konflikt. Skript převede název na všechna malá písmena, aby vyhověl požadavkům na název webových aplikací, účtů úložiště a databází.

    Požadovaný `SqlDatabasePassword` parametr určuje heslo pro účet správce, který bude vytvořen pro databázi SQL. Do hesla nezahrnejte speciální&amp; &lt; &gt; znaky XML (;). Toto je omezení způsobu, jakým byly skripty napsány, nikoli omezení Azure.

    Chcete-li například vytvořit webovou aplikaci s názvem "fixitdemo" a použít heslo správce serveru SQL Server "Passw0rd1", můžete zadat následující příkaz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Název musí být jedinečný v doméně azurewebsites.net a heslo musí splňovat požadavky databáze SQL pro složitost hesla. (Příklad Passw0rd1 splňuje požadavky.)

    Všimněte si, že příkaz začíná ". \". Chcete-li zabránit škodlivému spuštění skriptů, prostředí Windows PowerShell vyžaduje, abyste při spuštění skriptu poskytli plně kvalifikovanou cestu k souboru skriptu. Tečku můžete použít k označení aktuálního\"adresáře (". ) nebo poskytnout plně kvalifikovanou cestu, jako jsou:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Další informace o skriptu `Get-Help` získáte pomocí rutiny.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Pomocí rutiny `Detailed` `Full`, `Parameters`, `Examples` a parametry rutiny Get-Help můžete filtrovat vrácenou nápovědu.

    Pokud skript selže nebo generuje chyby, jako je například "New-AzureWebsite : Call Set-AzureSubscription a Select-AzureSubscription první", možná jste nedokončili konfiguraci Azure PowerShellu.

    Po dokončení skriptu můžete pomocí portálu pro správu Azure zobrazit prostředky, které byly vytvořeny, jak je znázorněno v kapitole [Automatizovat vše.](automate-everything.md)
10. Chcete-li nasadit projekt FixIt do nového prostředí Azure, použijte skript *AzureWebsite.ps1.* Příklad:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Po dokončení nasazení se otevře prohlížeč s fix It spuštěným v Azure.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Poradce při potížích se skripty prostředí Windows PowerShell

Nejčastější chyby při spuštění těchto skriptů souvisejí s oprávněními. Ujistěte `Add-AzureAccount` se, že a `Import-AzurePublishSettingsFile` byly úspěšné a že jste je použili pro stejné předplatné Azure. I `Add-AzureAccount` kdyby byl úspěšný, možná budete muset spustit znovu. Platnost oprávnění `Add-AzureAccount` přidaná za 12 hodin vyprší.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>Odkaz na objekt není nastaven na instanci objektu.

Pokud skript vrátí chyby, například "Odkaz na objekt není nastaven na instanci objektu", což znamená, že prostředí `Add-AzureAccount` Windows PowerShell nemůže najít objekt ke zpracování (jedná se o výjimku s nulovým odkazem), spusťte rutinu a zkuste skript znovu.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: Na serveru došlo k vnitřní chybě.

Rutina `New-AzureWebsite` vrátí vnitřní chybu, pokud název není jedinečný v azurewebsites.net doméně. Chcete-li chybu vyřešit, použijte pro název jinou hodnotu, která je v parametru Name *new-AzureWebsiteEnv.ps1*.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Restartování skriptu

Pokud potřebujete restartovat skript *New-AzureWebsiteEnv.ps1,* protože se nezdařilo před tiskem zprávy "Skript je dokončen", můžete odstranit prostředky, které skript vytvořený před jeho zastavením. Pokud například skript již vytvořil webovou aplikaci ContosoFixItDemo a skript znovu spustíte se stejným názvem, skript se nezdaří, protože název je používán.

Chcete-li zjistit, které prostředky skript vytvořený před jeho zastavením, použijte následující rutiny:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Chcete-li spustit tuto rutinu, `Get-AzureSqlDatabase`přepojit název databázového serveru na :`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

Chcete-li tyto prostředky odstranit, použijte následující příkazy. Všimněte si, že pokud odstraníte databázový server, automaticky odstraníte databáze přidružené k serveru.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Jak nasadit aplikaci se zpracováním fronty do webových aplikací Služby App Service Azure a cloudové služby Azure

Chcete-li povolit fronty, proveďte v souboru MyFixIt\Web.config následující změny. V `appSettings`části změňte `UseQueues` hodnotu na hodnotu "true":

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Pak nasadíte aplikaci MVC do webové aplikace ve službě Azure App Service, jak je popsáno [výše](#deploybase).

Dále vytvořte novou cloudovou službu Azure. Skripty, které jsou součástí aplikace Fix It, nevytvářejí ani nenasazují cloudovou službu, takže k tomu musíte použít portál Azure. Na portálu klikněte na **Nový** -- **výpočetní –** **cloudová služba** -- **Rychlé vytvoření**a zadejte adresu URL a umístění datového centra. Použijte stejné datové centrum, do kterého jste webovou aplikaci nasadili.

![](the-fix-it-sample-application/_static/image1.png)

Před nasazením cloudové služby je třeba aktualizovat některé konfigurační soubory.

V aplikaci MyFixIt.WorkerRole\app.config v `connectionStrings`části `appdb` nahraďte hodnotu připojovacího řetězce skutečným připojovacím řetězcem pro databázi SQL. Připojovací řetězec můžete získat z portálu. Na portálu klikněte na **položku SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP a JDBC**. Zkopírujte připojovací řetězec ADO.NET a vložte hodnotu do souboru app.config. Nahraďte\_heslo\_{vaše heslo zde}" heslem databáze. (Za předpokladu, že jste použili skripty k nasazení aplikace `SqlDatabasePassword` MVC, zadali jste heslo databáze v parametru skriptu.)

Výsledek by měl vypadat takto:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

Ve stejném souboru MyFixIt.WorkerRole\app.config v části `appSettings`nahraďte dvě zástupné hodnoty pro účet úložiště Azure.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Přístupový klíč můžete získat z portálu. Přečtěte [si, jak spravovat účty úložiště](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

V myfixitcloudservice\ServiceConfiguration.Cloud.cscfg nahraďte stejné dva zástupné hodnoty pro účet úložiště Azure.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Teď jste připraveni nasadit cloudovou službu. V řešení prozkoumat klikněte pravým tlačítkem myši na projekt MyFixItCloudService a vyberte **publikovat**. Další informace naleznete[v tématu](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)" Deploy the Application to Azure ", což je v části 2 [tohoto kurzu](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).

> [!div class="step-by-step"]
> [Předchozí](more-patterns-and-guidance.md)
