---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 'Iterace #5 – vytvořit testy částí (VB) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: V páté iteraci usnadňujeme údržbu a úpravy naší aplikace přidáním testů částí. Zesměšňujeme naše třídy datových modelů a vytváříme testy částí pro o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: cc5425de86e7481894fbea242fa555b5598167f6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542336"
---
# <a name="iteration-5--create-unit-tests-vb"></a>Iterace č. 5 – vytvoření testů jednotek (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> V páté iteraci usnadňujeme údržbu a úpravy naší aplikace přidáním testů částí. Zesměšňujeme naše třídy datových modelů a vytváříme testy částí pro naše řadiče a logiku ověřování.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Vytvoření aplikace pro správu kontaktů ASP.NET MVC (VB)

V této sérii kurzů vytvoříme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Contact Manager umožňuje ukládat kontaktní informace - jména, telefonní čísla a e-mailové adresy - pro seznam osob.

Vytvoříme aplikaci přes více iterací. S každou iterací postupně vylepšujeme aplikaci. Cílem tohoto přístupu více iterace je umožnit pochopit důvod pro každou změnu.

- Iterace #1 - Vytvořte aplikaci. V první iteraci vytvoříme Správce kontaktů nejjednodušším možným způsobem. Přidáváme podporu pro základní databázové operace: Vytvořit, Číst, Aktualizovat a odstranit (CRUD).

- Iterace #2 - Make aplikace vypadat hezky. V této iteraci vylepšujeme vzhled aplikace úpravou výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů.

- #3 iterace – přidejte ověření formuláře. Ve třetí iteraci přidáme ověření základního formuláře. Bráníme uživatelům v odesílání formuláře bez vyplnění požadovaných polí formuláře. Ověřujeme také e-mailové adresy a telefonní čísla.

- Iterace #4 - Proveďte aplikaci volně spojená. V této čtvrté iteraci využíváme několik vzorů návrhu softwaru, abychom usnadnili údržbu a úpravu aplikace Správce kontaktů. Například refaktorujeme naši aplikaci tak, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 - vytvořit testy částí. V páté iteraci usnadňujeme údržbu a úpravy naší aplikace přidáním testů částí. Zesměšňujeme naše třídy datových modelů a vytváříme testy částí pro naše řadiče a logiku ověřování.

- Iterace #6 – použijte vývoj řízený testem. V této šesté iteraci přidáme nové funkce do naší aplikace zápisem testů částí první a psaní kódu proti testování částí. V této iteraci přidáme skupiny kontaktů.

- Iterace #7 - Přidat funkci Ajax. V sedmé iteraci zlepšujeme odezvu a výkon naší aplikace přidáním podpory pro Ajax.

## <a name="this-iteration"></a>Tato iterace

V předchozí iteraci aplikace Contact Manager jsme refaktored aplikace, které mají být více volně spřažené. Aplikaci jsme rozdělili do různých vrstev řadiče, služby a úložiště. Každá vrstva interaguje s vrstvou pod ní prostřednictvím rozhraní.

Refaktored aplikace, aby se aplikace snadněji udržovat a upravovat. Například pokud potřebujeme použít novou technologii přístupu k datům, můžeme jednoduše změnit vrstvu úložiště bez dotyku řadiče nebo vrstvy služby. Tím, že správce kontaktů volně propojte, jsme učinili aplikaci odolnější vůči změnám.

Ale co se stane, když potřebujeme přidat novou funkci do aplikace Správce kontaktů? Nebo co se stane, když opravíme chybu? Smutné, ale dobře prokázané, pravda o psaní kódu je, že kdykoli se dotknete kódu, vytvoříte riziko zavedení nových chyb.

Například jeden krásný den vás může manažer požádat o přidání nové funkce do Správce kontaktů. Chce, abyste přidali podporu pro skupiny kontaktů. Chce, abyste uživatelům umožnili uspořádat své kontakty do skupin, jako jsou Přátelé, Firma a tak dále.

Chcete-li implementovat tuto novou funkci, budete muset upravit všechny tři vrstvy aplikace Správce kontaktů. Budete muset přidat nové funkce do řadičů, vrstvy služby a úložiště. Jakmile začnete upravovat kód, riskujete porušení funkce, která fungovala dříve.

Refaktoring naší aplikace do samostatných vrstev, jako jsme to udělali v předchozí iteraci, byla dobrá věc. Bylo to dobré, protože nám umožňuje provádět změny v celých vrstvách, aniž bychom se dotkli zbytku aplikace. Pokud však chcete usnadnit údržbu a úpravu kódu v rámci vrstvy, je třeba vytvořit testy částí pro kód.

Testování částí slouží k testování jednotlivých jednotek kódu. Tyto jednotky kódu jsou menší než celé vrstvy aplikace. Obvykle použijete testování částí k ověření, zda konkrétní metoda v kódu se chová očekávaným způsobem. Například byste vytvořit test jednotky pro CreateContact() metoda vystavena ContactManagerService třídy.

Testování částí pro aplikaci funguje stejně jako záchranná síť. Kdykoli upravíte kód v aplikaci, můžete spustit sadu testů částí a zkontrolovat, zda změna porušuje stávající funkce. Testy částí, aby váš kód bezpečné upravit. Testy částí provést všechny kód ve vaší aplikaci odolnější ke změně.

V této iteraci přidáme testy částí do naší aplikace Správce kontaktů. Tímto způsobem v další iteraci můžeme přidat skupiny kontaktů do naší aplikace bez obav o porušení stávajících funkcí.

> [!NOTE] 
> 
> Existuje celá řada architektury testování částí, včetně NUnit, xUnit.net a MbUnit. V tomto kurzu používáme rozhraní testování částí součástí sady Visual Studio. Můžete však stejně snadno použít jeden z těchto alternativních rámců.

## <a name="what-gets-tested"></a>Co dostane testovány

V dokonalém světě by byl celý váš kód pokryt testy částí. V dokonalém světě bys měl dokonalou záchrannou síť. Budete moci upravit libovolný řádek kódu ve vaší aplikaci a okamžitě vědět, provedením testů částí, zda změna porušila existující funkce.

Nicméně, my nežijeme v dokonalém světě. V praxi se při psaní testů částí soustředíte na psaní testů pro obchodní logiku (například logiku ověření). Zejména nezapisujete testy částí logiky přístupu k datům nebo logiky zobrazení. *do not*

Aby byly užitečné, testy částí musí být provedeny velmi rychle. Snadno můžete hromadit stovky (nebo dokonce tisíce) testů částí pro aplikaci. Pokud testování částí trvat dlouhou dobu ke spuštění pak se vyhnete jejich spuštění. Jinými slovy, dlouho běžící testy částí jsou k ničemu pro každodenní účely kódování.

Z tohoto důvodu obvykle nezapisujete testy částí pro kód, který spolupracuje s databází. Spuštění stovky testů částí proti živé databázi by bylo příliš pomalé. Místo toho zesměšňujete databázi a napíšete kód, který interaguje s falešnou databází (diskutujeme o zesměšňování databáze níže).

Z podobného důvodu obvykle nezapisujete testy částí pro zobrazení. Chcete-li otestovat zobrazení, je nutné sčítat webový server. Vzhledem k tomu, že střídání webového serveru je poměrně pomalý proces, není doporučeno vytvářet testy částí pro vaše zobrazení.

Pokud vaše zobrazení obsahuje složitou logiku, měli byste zvážit přesunutí logiky do metod Helper. Můžete psát testy částí pro pomocné metody, které se spouštějí bez střídání webového serveru.

> [!NOTE] 
> 
> Při psaní testů pro logiku přístupu k datům nebo logiku zobrazení není dobrý nápad při psaní testů částí, tyto testy mohou být velmi cenné při vytváření funkčních nebo integračních testů.

> [!NOTE] 
> 
> ASP.NET MVC je modul pro zobrazení webových formulářů. Zatímco modul zobrazení webových formulářů je závislý na webovém serveru, jiné moduly zobrazení nemusí být.

## <a name="using-a-mock-object-framework"></a>Použití architektury mock objektu

Při vytváření testů částí, téměř vždy je třeba využít architektury mock objektu. Mock Object framework umožňuje vytvářet mocks a zástupné procedury pro třídy ve vaší aplikaci.

Například můžete použít mock objektu framework ke generování falešné verze třídy úložiště. Tímto způsobem můžete použít třídu mock úložiště namísto skutečné třídy úložiště v testování částí. Pomocí mock úložiště umožňuje vyhnout se provádění kódu databáze při provádění testování částí.

Visual Studio neobsahuje mock objektu rozhraní. Existuje však několik komerčních a open source mock object frameworků, které jsou k dispozici pro rozhraní .NET Framework:

1. Moq - Tento framework je k dispozici pod open source BSD licencí. Moq si můžete [https://code.google.com/p/moq/](https://code.google.com/p/moq/)stáhnout z .
2. Rhino Mocks - Tento rámec je k dispozici pod open source BSD licencí. Rhino Mocks si [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)můžete stáhnout z .
3. Izolátor Typemock - Jedná se o komerční rámec. Zkušební verzi si můžete [http://www.typemock.com/](http://www.typemock.com/)stáhnout z aplikace .

V tomto tutoriálu jsem se rozhodl použít Moq. Můžete však stejně snadno použít Rhino Mocks nebo Typemock Isolator k vytvoření mock objektů pro aplikaci Contact Manager.

Před použitím moq, musíte provést následující kroky:

1. .
2. Než rozbalíte stahování, ujistěte se, že na soubor kliknete pravým tlačítkem myši a kliknete na tlačítko označené **Odblokovat** (viz obrázek 1).
3. Rozbalte stahování.
4. Přidejte odkaz na sestavení Moq do testovacího projektu výběrem volby nabídky **Projekt, Přidat odkaz** otevřete dialogové okno **Přidat odkaz.** Na kartě Procházet vyhledejte složku, ve které jste rozbalili Moq, a vyberte sestavení Moq.dll. Klikněte na tlačítko **OK** (viz obrázek 2).

[![Odblokování Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**Obrázek 01**: Odblokování Moq[(Klikněte pro zobrazení full-size image)](iteration-5-create-unit-tests-vb/_static/image2.png)

[![Odkazy po přidání Moq](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**Obrázek 02**: Reference po přidání Moq(Klikněte[pro zobrazení full-size image)](iteration-5-create-unit-tests-vb/_static/image4.png)

## <a name="creating-unit-tests-for-the-service-layer"></a>Vytváření testů částí pro vrstvu služby

Začněme vytvořením sady testů částí pro naši vrstvu služeb aplikace Správce kontaktů. Tyto testy použijeme k ověření naší logiky ověřování.

Vytvořte novou složku s názvem Modely v projektu ContactManager.Tests. Dále klepněte pravým tlačítkem myši na složku Modely a vyberte **přidat, nový test**. Zobrazí se dialogové okno **Přidat nový test** zobrazené na obrázku 3. Vyberte šablonu **Testování částí** a pojmenujte nový test ContactManagerServiceTest.vb. Kliknutím na tlačítko **OK** přidáte nový test do testovacího projektu.

> [!NOTE] 
> 
> Obecně chcete, aby struktura složek testovacího projektu odpovídala struktuře složek ASP.NET projektu MVC. Například umístíte testy kontroleru do složky Řadiče, modelu testujete ve složce Modely a tak dále.

[![Modely\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**Obrázek 03**: Modely\ContactManagerServiceTest.cs([Klepnutím zobrazíte obrázek v plné velikosti](iteration-5-create-unit-tests-vb/_static/image6.png))

Zpočátku chceme otestovat metodu CreateContact() vystavenou třídou ContactManagerService. Vytvoříme následujících pět testů:

- CreateContact() - Testy, které CreateContact() vrátí hodnotu true při předání platného kontaktu metodě.
- CreateContactRequiredFirstName() - Testuje, že do stavu modelu je přidána chybová zpráva, když je kontakt s chybějícím křestním jménem předán metodě CreateContact().
- CreateContactRequiredLastName() - Testuje, že do stavu modelu je přidána chybová zpráva, když je kontakt s chybějícím příjmením předán metodě CreateContact().
- CreateContactInvalidPhone() - Testuje, že do stavu modelu je přidána chybová zpráva, když je kontakt s neplatným telefonním číslem předán metodě CreateContact().
- CreateContactInvalidEmail() - Testuje, že do stavu modelu je přidána chybová zpráva, když je kontakt s neplatnou e-mailovou adresou předán metodě CreateContact().

První test ověří, zda platný kontakt negeneruje chybu ověření. Zbývající testy kontrolují každé ověřovací pravidla.

Kód pro tyto testy je obsažen v výpisu 1.

**Výpis 1 - Modely\ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

Vzhledem k tomu, že používáme Contact třídy v výpisu 1, musíme přidat odkaz na Microsoft Entity Framework do našeho testovacího projektu. Přidejte odkaz na sestavení System.Data.Entity.

Výpis 1 obsahuje metodu s názvem Initialize(), která je zdobena atributem [TestInitialize]. Tato metoda je volána automaticky před spuštěním každého z testů částí (je volána 5 krát těsně před každým z testů částí). Metoda Initialize() vytvoří falešné úložiště s následujícím řádkem kódu:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

Tento řádek kódu používá rámec Moq ke generování mock úložiště z rozhraní IContactManagerRepository. Mock úložiště se používá místo skutečné EntityContactManagerRepository, aby se zabránilo přístupu k databázi při spuštění každého testu jednotky. Mock úložiště implementuje metody rozhraní IContactManagerRepository, ale metody nejsou ve skutečnosti nic dělat.

> [!NOTE] 
> 
> Při použití moq framework, je \_rozdíl mezi \_mockRepository a mockRepository.Object. První odkazuje na Mock(Of IContactManagerRepository) třídy, která obsahuje metody pro určení, jak mock úložiště bude chovat. Ten odkazuje na skutečné mock úložiště, které implementuje rozhraní IContactManagerRepository.

Mock úložiště se používá v Initialize() metoda při vytváření instance ContactManagerService třídy. Všechny jednotlivé testy částí používají tuto instanci třídy ContactManagerService.

Výpis 1 obsahuje pět metod, které odpovídají každé z testů částí. Každá z těchto metod je zdobena atributem [TestMethod]. Při spuštění testů částí je volána jakákoli metoda, která má tento atribut. Jinými slovy všechny metody, která je zdobena atributem [TestMethod] je test částí.

První test částí s názvem CreateContact(), ověří, že volání CreateContact() vrátí hodnotu true při předání platné instance třídy Contact metodě. Test vytvoří instanci Contact třídy, volá CreateContact() metoda a ověří, že CreateContact() vrátí hodnotu true.

Zbývající testy ověřte, že při createcontact() metoda je volána s neplatným Kontakt pak metoda vrátí false a očekávané chybové hlášení ověření je přidán do stavu modelu. Například test CreateContactRequiredFirstName() vytvoří instanci třídy Contact s prázdným řetězcem pro svou vlastnost FirstName. Dále createcontact() metoda je volána s neplatný kontakt. Nakonec test ověří, že CreateContact() vrátí false a že stav modelu obsahuje očekávanou chybovou zprávu ověření "Je vyžadováno první jméno."

Testy jednotek můžete spustit v výpisu 1 výběrem možnosti nabídky **Test, Spustit, Všechny testy v řešení (CTRL+R, A)**. Výsledky testů jsou zobrazeny v okně Výsledky testů (viz obrázek 4).

[![Výsledky testů](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**Obrázek 04**: Výsledky testů[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-5-create-unit-tests-vb/_static/image8.png)

## <a name="creating-unit-tests-for-controllers"></a>Vytváření testů jednotek pro řadiče

ASP.NET aplikace MVC řídí tok interakce s uživatelem. Při testování řadiče, chcete otestovat, zda řadič vrátí správný výsledek akce a zobrazit data. Můžete také chtít otestovat, zda řadič spolupracuje s třídami modelu očekávaným způsobem.

Výpis 2 například obsahuje dva testy částí pro metodu Create() řadiče kontaktu. První test částí ověří, že když je platný kontakt předán metodě Create(), metoda Create() přesměruje na akci Index. Jinými slovy, když předán platný kontakt, Create() metoda by měla vrátit RedirectToRouteResult, která představuje akci Index.

Nechceme testovat vrstvu služby ContactManager, když testujeme vrstvu kontroleru. Proto zesměšňujeme vrstvu služby s následujícím kódem v metodě Initialize:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

V testu jednotky CreateValidContact() zesměšňujeme chování volání metody CreateContact() vrstvy služby s následujícím řádkem kódu:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

Tento řádek kódu způsobí, že služba ContactManager mock vrátí hodnotu true, když je volána její metoda CreateContact(). Zesměšňováním vrstvy služby můžeme otestovat chování našeho řadiče bez nutnosti spustit libovolný kód ve vrstvě služby.

Druhý test jednotky ověří, že create() akce vrátí vytvořit zobrazení při předán neplatný kontakt na metodu. Způsobíme, že metoda vrstvy služby CreateContact() vrátí hodnotu false s následujícím řádkem kódu:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

Pokud Create() Metoda se chová tak, jak očekáváme, pak by měla vrátit vytvořit zobrazení, když vrstva služby vrátí hodnotu false. Tímto způsobem může řadič zobrazit chybové zprávy ověření v zobrazení Vytvořit a uživatel má možnost opravit tyto neplatné vlastnosti kontaktu.

Pokud máte v plánu vytvořit testy částí pro řadiče, pak je třeba vrátit explicitní zobrazení názvy z akce řadiče. Například nevracejte zobrazení, jako je toto:

Zpětné zobrazení()

Místo toho vraťte zobrazení takto:

Návratové zobrazení("Vytvořit")

Pokud nejste explicitní při vracení zobrazení, vrátí vlastnost ViewResult.ViewName prázdný řetězec.

**Výpis 2 - Řadiče\ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>Souhrn

V této iteraci jsme vytvořili testy částí pro naši aplikaci Správce kontaktů. Tyto testy částí můžeme kdykoli spustit, abychom ověřili, že naše aplikace se stále chová způsobem, který očekáváme. Jednotkové testy fungují jako záchranná síť pro naši aplikaci, která nám umožňuje bezpečně upravovat naši aplikaci v budoucnu.

Vytvořili jsme dvě sady testů částí. Nejprve jsme testovali naši ověřovací logiku vytvořením testů částí pro naši vrstvu služby. Dále jsme testovali naši logiku řízení toku vytvořením testů částí pro naši vrstvu řadiče. Při testování naší vrstvy služby jsme izolovali naše testy pro naši vrstvu služby z vrstvy úložiště tím, že jsme se vysmívali vrstvě úložiště. Při testování vrstvy řadiče jsme izolovali naše testy pro vrstvu řadiče tím, že jsme se vysmívali vrstvě služby.

V další iteraci upravíme aplikaci Správce kontaktů tak, aby podporovala skupiny kontaktů. Tuto novou funkci přidáme do naší aplikace pomocí procesu návrhu softwaru nazývaného vývoj řízený testováním.

> [!div class="step-by-step"]
> [Předchozí](iteration-4-make-the-application-loosely-coupled-vb.md)
> [další](iteration-6-use-test-driven-development-vb.md)
