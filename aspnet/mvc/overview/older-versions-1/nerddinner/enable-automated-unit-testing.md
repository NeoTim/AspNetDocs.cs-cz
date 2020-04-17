---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Povolit automatizované testování částí | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 12 ukazuje, jak vyvinout sadu automatizovaných testů částí, které ověřují naši funkci NerdDinner a které nám dodají jistotu, že provedeme změny...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541465"
---
# <a name="enable-automated-unit-testing"></a>Povolení automatického testování jednotek

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 12 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 12 ukazuje, jak vyvinout sadu automatizovaných testů částí, které ověřují naše funkce NerdDinner a které nám dodají jistotu, že v budoucnu provedeme změny a vylepšení aplikace.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner Krok 12: Testování částí

Pojďme vyvinout sadu automatizovaných testů částí, které ověřují naše funkce NerdDinner a které nám dodají jistotu, že v budoucnu provedeme změny a vylepšení aplikace.

### <a name="why-unit-test"></a>Proč testování částí?

Na cestě do práce jednoho rána máte náhlý záblesk inspirace o aplikaci, na které pracujete. Uvědomujete si, že je změna, kterou můžete implementovat, která bude aplikace dramaticky lepší. Může to být refaktoring, který vyčistí kód, přidá novou funkci nebo opraví chybu.

Otázka, která vás konfrontuje, když dorazíte k počítači, je - "jak bezpečné je toto zlepšení?" Co když provedení změny má vedlejší účinky nebo něco rozbije? Změna může být jednoduchá a instalace trvá jen několik minut, ale co když ruční testování všech scénářů aplikace trvá několik hodin? Co když zapomenete pokrýt scénář a přerušená aplikace přejde do produkčního prostředí? Je dělat toto zlepšení opravdu stojí za veškeré úsilí?

Automatizované testy částí mohou poskytnout záchrannou síť, která vám umožní neustále vylepšovat aplikace a vyhnout se obavám z kódu, na kterém pracujete. Automatické testy, které rychle ověřují funkčnost, vám umožní s jistotou zakódovat kód – a umožní vám provádět vylepšení, která by vám jinak nemusela být příjemná. Pomáhají také vytvářet řešení, která jsou udržovatelnější a mají delší životnost , což vede k mnohem vyšší návratnosti investic.

Rozhraní ASP.NET MVC Framework usnadňuje a přirození umožňuje testování funkcí aplikace při testování částí. Umožňuje také pracovní postup TDD (Test Driven Development), který umožňuje vývoj založený na testu.

### <a name="nerddinnertests-project"></a>NerdDinner.Testy projektu

Když jsme vytvořili naši aplikaci NerdDinner na začátku tohoto kurzu, byli jsme vyzváni s dialogem s dotazem, zda chceme vytvořit projekt testování částí jít spolu s projektem aplikace:

![](enable-automated-unit-testing/_static/image1.png)

Ponechali jsme si vybrané tlačítko "Ano, vytvořit projekt testování částí" – což vedlo k přidání projektu "NerdDinner.Tests" do našeho řešení:

![](enable-automated-unit-testing/_static/image2.png)

Projekt NerdDinner.Tests odkazuje na sestavení projektu aplikace NerdDinner a umožňuje nám snadno přidat automatizované testy, které ověřují funkčnost aplikace.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Vytváření testů částí pro naši třídu modelu večeři

Přidáme některé testy do našeho projektu NerdDinner.Tests, které ověřují třídu Dinner, kterou jsme vytvořili při vytváření vrstvy modelu.

Začneme vytvořením nové složky v rámci našeho testovacího projektu s názvem "Modely", kde umístíme naše testy související s modelem. Poté klikneme pravým tlačítkem myši na složku a zvolíme příkaz **Přidat&gt;nový test.** Tím se zobrazí dialogové okno Přidat nový test.

Zvolíme vytvoření "Testování částí" a pojmenujeme jej "DinnerTest.cs":

![](enable-automated-unit-testing/_static/image3.png)

Když klikneme na tlačítko "ok" Visual Studio přidá (a otevře) DinnerTest.cs soubor do projektu:

![](enable-automated-unit-testing/_static/image4.png)

Výchozí šablona testu jednotky Sady Visual Studio obsahuje spoustu kódu kotle, který mi připadá trochu chaotický. Pojďme vyčistit to jen obsahovat kód níže:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

Atribut [TestClass] ve výše uvedené třídě DinnerTest jej identifikuje jako třídu, která bude obsahovat testy, stejně jako volitelný kód inicializace testu a teardown. Můžeme definovat testy v něm přidáním veřejné metody, které mají atribut [TestMethod] na nich.

Níže jsou uvedeny první ze dvou testů přidáme, že cvičení naše večeře třídy. První test ověří, že naše Dinner je neplatná, pokud je vytvořena nová večeře bez správné nastavení všech vlastností. Druhý test ověří, že naše Večeře je platný, když Dinner má všechny vlastnosti nastavené s platnými hodnotami:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Všimněte si výše, že naše názvy testů jsou velmi explicitní (a poněkud podrobné). Děláme to proto, že bychom mohli nakonec vytvořit stovky nebo tisíce malých testů a chceme, aby bylo snadné rychle určit záměr a chování každého z nich (zvláště když se díváme přes seznam selhání v testovacím běžci). Názvy testů by měly být pojmenovány po funkcích, které testují. Výše používáme "Notovod by\_sloveso"\_pojmenování vzor.

Jsme strukturování testy pomocí "AAA" testovací vzor - což je zkratka pro "Uspořádat, zákon, assert":

- Uspořádat: Nastavení testované jednotky
- Zákon: Cvičení testovky a výsledky zachycení
- Assert: Ověření chování

Když píšeme testy, chceme se vyhnout tomu, aby jednotlivé testy dělaly příliš mnoho. Místo toho každý test by měl ověřit pouze jeden koncept (což bude mnohem jednodušší určit příčinu selhání). Dobrým vodítkem je vyzkoušet a mít pouze jeden příkaz assert pro každý test. Pokud máte více než jeden příkaz assert v testovací metodě, ujistěte se, že jsou všechny používány k testování stejného konceptu. Pokud jste na pochybách, proveďte další test.

### <a name="running-tests"></a>Spouštění testů

Visual Studio 2008 Professional (a vyšší edice) obsahuje předdefinovaný testovací běžec, který lze použít ke spuštění projektů Visual Studio Unit Test v rámci integrovaného testování. Můžeme vybrat **test-&gt;&gt;Run- Všechny testy v nabídce řešení** příkazu (nebo zadejte Ctrl R, A) pro spuštění všech našich testů částí. Nebo alternativně můžeme umístit kurzor v rámci konkrétní testovací třídy nebo testovací metody a použít **příkaz Test-Run-&gt;&gt;Tests in Current Context** menu (nebo zadejte Ctrl R, T) pro spuštění podmnožiny testů částí.

Umístěte kurzor v rámci DinnerTest třídy a zadejte "Ctrl R, T" spustit dva testy, které jsme právě definovali. Když to uděláme, zobrazí se v sadě Visual Studio okno "Výsledky testů" a zobrazí se v něm výsledky našeho testovacího běhu:

![](enable-automated-unit-testing/_static/image5.png)

*Poznámka: Okno výsledků testu VS ve výchozím nastavení nezobrazuje sloupec Název třídy. Můžete to přidat kliknutím pravým tlačítkem myši v okně Výsledky testu a pomocí příkazu Příkazpřidat nebo odebrat sloupce.*

Naše dva testy trvalo jen zlomek sekundy spustit - a jak můžete vidět, že oba prošel. Můžeme nyní pokračovat a rozšířit je vytvořením další testy, které ověřují konkrétní pravidlo ověření, stejně jako pokrytí dvou pomocných metod – IsUserHost() a IsUserRegistered() – které jsme přidali do Dinner třídy. Všechny tyto testy na místě pro Dinner třídy bude mnohem jednodušší a bezpečnější přidat nová obchodní pravidla a ověření do něj v budoucnu. Můžeme přidat naše nové pravidlo logiky večeři a pak během několika sekund ověřit, že nebyla přerušena žádné z našich předchozích funkcí logiky.

Všimněte si, jak použití popisného názvu testu usnadňuje rychlé pochopení toho, co jednotlivé testy ověřují. Doporučuji používat příkaz nabídky **Tools-Options,&gt;** otevření&gt;obrazovky konfigurace testovacího nástroje - spuštění testu a kontrola políčka "Poklepání na neúspěšný nebo neprůkazný výsledek testu jednotky zobrazí bod selhání v testu". To vám umožní poklepat na selhání v okně výsledků testu a okamžitě přejít na selhání assert.

### <a name="creating-dinnerscontroller-unit-tests"></a>Vytváření testů částí DinnersController

Pojďme nyní vytvořit některé testy částí, které ověřují naše DinnersController funkce. Začneme kliknutím pravým tlačítkem myši na složku "Řadiče" v rámci našeho testovacího projektu a pak zvolte příkaz Nabídky **Přidat&gt;nový test.** Vytvoříme "Test částí" a pojmenujeme jej "DinnersControllerTest.cs".

Vytvoříme dvě testovací metody, které ověřují Metodu akce Details() na DinnersController. První ověří, že zobrazení je vrácena při požadavku existující večeři. Druhý ověří, že je vráceno zobrazení "NotFound", pokud je požadována neexistující večeře:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

Výše uvedený kód zkompiluje clean. Když spustíme testy, oba selžou:

![](enable-automated-unit-testing/_static/image6.png)

Pokud se podíváme na chybové zprávy, uvidíme, že důvod, proč testy se nezdařilo bylo proto, že naše DinnersRepository třídy nebylo možné připojit k databázi. Naše aplikace NerdDinner používá připojovací řetězec k místnímu souboru\_SQL Server Express, který se nachází pod adresářem \App Data projektu aplikace NerdDinner. Vzhledem k tomu, že náš projekt NerdDinner.Tests zkompiluje a spustí v jiném adresáři než v projektu aplikace, relativní umístění cesty našeho připojovacího řetězce je nesprávné.

*Mohli bychom* to opravit zkopírováním databázového souboru SQL Express do našeho testovacího projektu a potom k němu přidat příslušný testovací připojovací řetězec v souboru App.config našeho testovacího projektu. To by si výše uvedené testy odblokovány a běží.

Testování částí kód pomocí skutečné databáze, i když přináší s sebou řadu výzev. Konkrétně:

- Výrazně zpomaluje dobu provádění testů částí. Čím déle trvá spuštění testů, tím menší je pravděpodobnost jejich častého spuštění. V ideálním případě chcete, aby vaše testy částí bylo možné spustit během několika sekund – a mít to být něco, co děláte stejně přirozeně jako kompilace projektu.
- Komplikuje logiku nastavení a vyčištění v rámci testů. Chcete, aby každý test jednotky být izolované a nezávislé na ostatní (bez vedlejších účinků nebo závislostí). Při práci s reálnou databází musíte mít na paměti stav a obnovit jej mezi testy.

Podívejme se na návrhový vzor s názvem "vkládání závislostí", který nám může pomoci vyřešit tyto problémy a vyhnout se nutnosti používat skutečnou databázi s našimi testy.

### <a name="dependency-injection"></a>Injektáž závislostí

Právě teď DinnersController je pevně "spojený" s DinnerRepository třídy. "Spojka" označuje situaci, kdy třída výslovně spoléhá na jinou třídu, aby fungovala:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

Vzhledem k tomu, že třída DinnerRepository vyžaduje přístup k databázi, pevně spojená závislost, kterou má třída DinnersController na DinnerRepository, nakonec vyžaduje, abychom měli databázi, aby byly testovány metody akce DinnersController.

Můžeme obejít pomocí návrhového vzoru s názvem "vkládání závislostí" – což je přístup, kde závislosti (jako třídy úložiště, které poskytují přístup k datům) již nejsou implicitně vytvořeny v rámci tříd, které je používají. Místo toho závislosti mohou být explicitně předány třídě, která je používá pomocí argumentů konstruktoru. Pokud jsou závislosti definovány pomocí rozhraní, pak máme flexibilitu předat v "falešné" implementace závislostí pro scénáře testování částí. To nám umožňuje vytvářet implementace závislostí specifické pro testování, které ve skutečnosti nevyžadují přístup k databázi.

Chcete-li zobrazit v akci, implementujeme vkládání závislostí s naší DinnersController.

#### <a name="extracting-an-idinnerrepository-interface"></a>Extrahování rozhraní IDinnerRepository

Naším prvním krokem bude vytvoření nového rozhraní IDinnerRepository, které zapouzdřuje kontrakt úložiště, který naše řadiče vyžadují k načtení a aktualizaci Dinners.

Tuto smlouvu rozhraní můžeme definovat ručně tak, že klikneme pravým tlačítkem myši na složku \Models a potom vybereme příkaz Nabídky **Přidat&gt;novou položku** a vytvoříme nové rozhraní s názvem IDinnerRepository.cs.

Alternativně můžeme použít refaktoring nástroje integrované do Visual Studio Professional (a vyšší edice) automaticky extrahovat a vytvořit rozhraní pro nás z naší stávající DinnerRepository třídy. Chcete-li extrahovat toto rozhraní pomocí VS, jednoduše umístěte kurzor v textovém editoru na DinnerRepository třídy a potom pravým tlačítkem myši a zvolte příkaz příkazu **refaktor-&gt;extrahovat rozhraní:**

![](enable-automated-unit-testing/_static/image7.png)

Tím se spustí dialog "Extrahovat rozhraní" a vyzve nás k názvu rozhraní k vytvoření. Bude výchozí IDinnerRepository a automaticky vybrat všechny veřejné metody na existující DinnerRepository třídy přidat do rozhraní:

![](enable-automated-unit-testing/_static/image8.png)

Když klikneme na tlačítko "ok", Visual Studio přidá nové rozhraní IDinnerRepository do naší aplikace:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

A naše stávající DinnerRepository třídy budou aktualizovány tak, aby implementuje rozhraní:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>Aktualizace DinnersController pro podporu vkládání konstruktoru

Nyní budeme aktualizovat DinnersController třídy používat nové rozhraní.

V současné době DinnersController je pevně zakódován tak, že jeho pole "dinnerRepository" je vždy dinnerrepository třída:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Změníme tak, aby pole "dinnerRepository" je typu IDinnerRepository místo DinnerRepository. Pak přidáme dva veřejné DinnersController konstruktory. Jeden z konstruktorů umožňuje IDinnerRepository být předány jako argument. Druhý je výchozí konstruktor, který používá naše stávající DinnerRepository implementace:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

Vzhledem k tomu, že ASP.NET MVC ve výchozím nastavení vytvoří třídy řadiče pomocí výchozí konstruktory, naše DinnersController za běhu bude i nadále používat DinnerRepository třídy k provedení přístupu k datům.

Nyní můžeme aktualizovat naše testy částí, i když předat v "falešné" večeři implementace úložiště pomocí konstruktoru parametru. Toto "falešné" úložiště večeří nebude vyžadovat přístup k reálné databázi a místo toho použije ukázková data v paměti.

#### <a name="creating-the-fakedinnerrepository-class"></a>Vytvoření třídy FakeDinnerRepository

Pojďme vytvořit FakeDinnerRepository třídy.

Začneme vytvořením adresáře "Fakes" v rámci našeho projektu NerdDinner.Tests a pak do něj přidáme novou třídu FakeDinnerRepository (klikněte pravým tlačítkem myši na složku a zvolte **Add-&gt;New Class**):

![](enable-automated-unit-testing/_static/image9.png)

Budeme aktualizovat kód tak, aby Třída FakeDinnerRepository implementuje rozhraní IDinnerRepository. Můžeme pak pravým tlačítkem myši na něj a zvolit příkaz kontextové nabídky "Implement interface IDinnerRepository":

![](enable-automated-unit-testing/_static/image10.png)

To způsobí, že Visual Studio automaticky přidá všechny členy rozhraní IDinnerRepository do naší třídy FakeDinnerRepository s výchozími implementacemi "se zakázaným inzerováním":

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Potom můžeme aktualizovat FakeDinnerRepository implementace pracovat off v&lt;paměti&gt; List Dinner kolekce předána jako argument konstruktoru:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Nyní máme falešnou implementaci IDinnerRepository, která nevyžaduje databázi a místo toho může pracovat mimo seznam objektů Dinner v paměti.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Použití FakeDinnerRepository s testy částí

Vraťme se k testům částí DinnersController, které se dříve nezdařily, protože databáze nebyla k dispozici. Můžeme aktualizovat testovací metody použít FakeDinnerRepository naplněný ukázkovými daty v paměti dinnersController pomocí následujícího kódu:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

A teď, když jsme se spustit tyto testy, které oba projít:

![](enable-automated-unit-testing/_static/image11.png)

Nejlepší ze všeho je, že trvat jen zlomek sekundy ke spuštění a nevyžadují žádné složité nastavení / vyčištění logiky. Nyní můžeme otestovat všechny naše DinnersController kód metody akce (včetně výpisu, stránkování, podrobnosti, vytvořit, aktualizovat a odstranit), aniž by museli připojit k reálné databázi.

| **Vedlejší téma: Rozhraní vkládání závislostí** |
| --- |
| Provádění ruční vkládání závislostí (jako jsme výše) funguje dobře, ale stále těžší udržovat jako počet závislostí a součástí v aplikaci zvyšuje. Pro rozhraní .NET existuje několik rozhraní pro vkládání závislostí, které mohou pomoci poskytnout ještě větší flexibilitu správy závislostí. Tyto architektury, také někdy nazývá "Inverze control" (IoC) kontejnery, poskytují mechanismy, které umožňují další úroveň podpory konfigurace pro určení a předávání závislostí na objekty za běhu (nejčastěji pomocí vkládání konstruktoru). Některé z více populární OSS závislost í injection / IOC rámce v .NET patří: AutoFac, Ninject, Spring.NET, StructureMap a Windsor. ASP.NET MVC zveřejňuje rozhraní API rozšiřitelnosti, která umožňují vývojářům účastnit se řešení a vytváření instancí řadičů a která umožňuje, aby byly v tomto procesu čistě integrovány rozhraní Injection / IoC injection závislostí. Použití di/ioc rozhraní by také nám umožní odebrat výchozí konstruktor z našedinnersController – což by zcela odebrat spojení mezi ním a DinnerRepository. Nebudeme používat vkládání závislostí / ioc rámec s naší aplikací NerdDinner. Ale je to něco, co bychom mohli zvážit do budoucna, pokud NerdDinner kód-base a schopnosti rostly. |

### <a name="creating-edit-action-unit-tests"></a>Vytváření testů jednotek akcí úprav

Nyní vytvoříme některé testy částí, které ověřují funkci úprav y DinnersController. Začneme testováním http-get verze naší akce Úpravy:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Vytvoříme test, který ověří, že view podporované DinnerFormViewModel objektu je vykreslen zpět, když je požadována platná večeře:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Při spuštění testu však zjistíme, že se nezdaří, protože je vyvolána výjimka nulového odkazu, když metoda Edit přistupuje k vlastnosti User.Identity.Name k provedení kontroly Dinner.IsHostedBy().

Objekt User v základní třídě řadiče zapouzdřuje podrobnosti o přihlášeném uživateli a je naplněn ASP.NET MVC při vytváření řadiče za běhu. Protože testujeme DinnersController mimo prostředí webového serveru, objekt User není nastaven (tedy výjimka nulového odkazu).

### <a name="mocking-the-useridentityname-property"></a>Zesměšňování vlastnosti User.Identity.Name

Zosměšňující architektury usnadňují testování tím, že nám umožňují dynamicky vytvářet falešné verze závislých objektů, které podporují naše testy. Například můžeme použít mocking framework v našem testu akce Upravit dynamicky vytvořit objekt User, který naše DinnersController můžete použít k vyhledávání simulované uživatelské jméno. Tím se zabrání nulové odkaz vyvolána při spuštění našeho testu.

Existuje mnoho .NET výsměch architektury, které lze použít s ASP.NET MVC (můžete vidět seznam z nich zde: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)). Pro testování naší aplikace NerdDinner budeme používat open source mocking framework s názvem "Moq", který lze stáhnout zdarma z [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).

Po stažení přidáme odkaz v našem projektu NerdDinner.Tests do sestavení Moq.dll:

![](enable-automated-unit-testing/_static/image12.png)

Poté přidáme pomocnou metodu "CreateDinnersControllerAs(username)" do naší testovací třídy, která přebírá uživatelské jméno jako parametr a která pak "nadává" vlastnosti User.Identity.Name v instanci DinnersController:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Výše používáme Moq k vytvoření Mock objekt, který zfalšuje ControllerContext objekt (což je to, co ASP.NET MVC předává Controller třídy vystavit runtime objekty jako uživatel, požadavek, odpověď a relace). Voláme metodu "SetupGet" na Mock označuje, že vlastnost HttpContext.User.Identity.Name na ControllerContext by měla vrátit řetězec uživatelského jména jsme předali pomocné metody.

Můžeme zesměšňovat libovolný počet ControllerContext vlastnosti a metody. Pro ilustraci jsem také přidal SetupGet() volání pro Request.IsAuthenticated vlastnost (což není ve skutečnosti potřebné pro testy níže - ale který pomáhá ilustrovat, jak můžete zesměšňovat Request vlastnosti). Když jsme hotovi přiřadíinu ControllerContext mock na DinnersController naše pomocná metoda vrátí.

Nyní můžeme psát testy částí, které používají tuto pomocnou metodu k testování scénářů úprav zahrnujících různé uživatele:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

A teď, když děláme testy, které projdou:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>Testování scénářů UpdateModel()

Vytvořili jsme testy, které pokrývají http-get verzi akce Upravit. Nyní vytvoříme některé testy, které ověří verzi http-post akce Úpravy:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

Zajímavý nový scénář testování pro nás pro podporu s touto metodou akce je jeho použití UpdateModel() pomocné metody na controller základní třídy. Používáme tuto pomocnou metodu k vazbě hodnoty post formuláře na naše Dinner objekt instance.

Níže jsou uvedeny dva testy, které ukazuje, jak můžeme zadat formulář zaúčtované hodnoty pro UpdateModel() pomocné metody použít. Uděláme to vytvořením a naplněním Objektu FormCollection a pak jej přiřadíme vlastnosti "ValueProvider" na řadiči.

První test ověří, zda je při úspěšném uložení prohlížeč přesměrován na akci podrobností. Druhý test ověří, zda je při zaúčtování neplatného vstupu akce znovu zobrazeno zobrazení úprav s chybovou zprávou.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Testování zábal-Up

Probrali jsme základní koncepty, které se podílejí na třídách řídicích jednotek testování částí. Tyto techniky můžeme použít ke snadnému vytvoření stovek jednoduchých testů, které ověřují chování naší aplikace.

Vzhledem k tomu, že naše testy řadičů a modelů nevyžadují skutečnou databázi, jsou extrémně rychlé a snadno spustit. Během několika sekund budeme schopni provést stovky automatizovaných testů a okamžitě získat zpětnou vazbu o tom, zda změna, která jsme provedli, něco zlomila. To nám pomůže poskytnout důvěru neustále zlepšovat, refaktorovat a zdokonalovat naši aplikaci.

Testování jsme pokryli jako poslední téma v této kapitole - ale ne proto, že testování je něco, co byste měli udělat na konci vývojového procesu! Naopak, měli byste psát automatizované testy co nejdříve ve vašem vývojovém procesu. To vám umožní získat okamžitou zpětnou vazbu při vývoji, pomůže vám zamyslet se nad scénáři případu použití vaší aplikace a provede vás návrh aplikace s ohledem na čisté vrstvení a párování.

Další kapitola v knize bude diskutovat Test Driven Development (TDD), a jak ji používat s ASP.NET MVC. TDD je iterativní kódování praxe, kde nejprve napsat testy, které bude splňovat výsledný kód. S TDD začnete každou funkci vytvořením testu, který ověří funkce, které se chystáte implementovat. Psaní testování částí nejprve pomáhá zajistit, že jasně pochopit funkci a jak má fungovat. Teprve po zapsání testu (a jste ověřili, že se nezdaří) pak implementovat skutečné funkce test ověří. Vzhledem k tomu, že jste již strávili čas přemýšlením o případu použití, jak má funkce fungovat, budete lépe porozumět požadavkům a jak je nejlépe implementovat. Po dokončení implementace můžete znovu spustit test – a získat okamžitou zpětnou vazbu o tom, zda funkce funguje správně. TDD budeme více pokrývat v kapitole 10.

### <a name="next-step"></a>Další krok

Některé konečné zabalit komentáře.

> [!div class="step-by-step"]
> [Předchozí](use-ajax-to-implement-mapping-scenarios.md)
> [další](nerddinner-wrap-up.md)
