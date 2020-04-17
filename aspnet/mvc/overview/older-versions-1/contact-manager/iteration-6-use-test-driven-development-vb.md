---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: 'Iterace #6 – použití vývoje řízeného testováním (VB) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: V této šesté iteraci přidáme nové funkce do naší aplikace zápisem testů částí první a psaní kódu proti testování částí. V této iteraci,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 8464f4cdee673ef75d561e4cf89613fdca2c16af
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542804"
---
# <a name="iteration-6--use-test-driven-development-vb"></a>Iterace č. 6 – použití vývoje řízeného testy (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> V této šesté iteraci přidáme nové funkce do naší aplikace zápisem testů částí první a psaní kódu proti testování částí. V této iteraci přidáme skupiny kontaktů.

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

V předchozí iteraci aplikace Contact Manager jsme vytvořili testy částí, abychom poskytli záchrannou síť pro náš kód. Motivací pro vytvoření testů částí bylo, aby byl náš kód odolnější vůči změnám. S testování částí na místě, můžeme šťastně provést jakoukoli změnu našeho kódu a okamžitě vědět, zda jsme porušili stávající funkce.

V této iteraci používáme testy částí pro zcela jiný účel. V této iteraci používáme testy částí jako součást filozofie návrhu aplikace s názvem *vývoj řízený testováním*. Při procvičování vývoj řízený testy, nejprve napíšete testy a pak napíšete kód proti testům.

Přesněji řečeno, při procvičování vývoje řízeného testováním existují tři kroky, které dokončíte při vytváření kódu (červená / zelená / refaktor):

1. Napsat test částí, který se nezdaří (červená)
2. Napište kód, který projde testováním částí (zelená)
3. Refaktorovat kód (Refaktor)

Nejprve napíšete test částí. Testování částí by měl vyjádřit svůj záměr pro jak očekáváte, že váš kód chovat. Při prvním vytvoření testování částí by měl test částí selhat. Test by měl selhat, protože jste ještě nenapsali žádný kód aplikace, který splňuje test.

Dále napíšete pouze dostatek kódu, aby test částí projít. Cílem je napsat kód nejlínějším, nejnedbalejším a nejrychlejším možným způsobem. Neměli byste ztrácet čas přemýšlením o architektuře vaší aplikace. Místo toho byste se měli zaměřit na psaní minimální množství kódu potřebné k uspokojení záměru vyjádřené testování částí.

Nakonec poté, co jste napsali dostatek kódu, můžete krok zpět a zvážit celkovou architekturu vaší aplikace. V tomto kroku přepsat (refaktorovat) kód s využitím vzorů návrhu softwaru – jako je například vzor úložiště – tak, aby váš kód je více udržovatelné. V tomto kroku můžete nebojácně přepsat kód, protože váš kód je pokryt testy částí.

Existuje mnoho výhod, které vyplývají z praxe test-řízený vývoj. Za prvé, vývoj řízený testem vás vynutí zaměřit se na kód, který je ve skutečnosti třeba napsat. Vzhledem k tomu, že jste neustále zaměřena na jen psaní dostatek kódu projít konkrétní test, jste zabráněno putování do plevele a psaní obrovské množství kódu, který nikdy nebudete používat.

Za druhé, metodika návrhu "test first" vás nutí psát kód z hlediska, jak bude váš kód použit. Jinými slovy, při procvičování vývoje řízeného testy neustále píšete testy z uživatelského hlediska. Proto vývoj řízený testováním může mít za následek čistší a srozumitelnější api.

Nakonec vývoj řízený testováním vás vynutí psát testy částí jako součást normálního procesu psaní aplikace. Jako termín projektu se blíží, testování je obvykle první věc, která jde ven z okna. Při procvičování vývojřízený testem, na druhé straně, je pravděpodobnější, že bude ctnostný o psaní testů částí, protože vývoj řízený testem činí testy částí ústředním bodem procesu vytváření aplikace.

> [!NOTE] 
> 
> Chcete-li se dozvědět více o test-řízený vývoj, doporučuji, abyste si přečetli Michael Feathers knihu **Efektivně pracovat s Legacy Code**.

V této iteraci přidáme novou funkci do naší aplikace Správce kontaktů. Přidáváme podporu pro skupiny kontaktů. Pomocí skupin kontaktů můžete kontakty uspořádat do kategorií, jako jsou skupiny Firmy a Přátelé.

Tuto novou funkci přidáme do naší aplikace pomocí procesu vývoje řízeného testováním. Nejprve napíšeme naše testy částí a napíšeme všechny naše kódy proti těmto testům.

## <a name="what-gets-tested"></a>Co dostane testovány

Jak jsme diskutovali v předchozí iteraci, obvykle nezapisujete testy částí logiky přístupu k datům nebo logiku zobrazení. Nezapisujete testy částí logiky přístupu k datům, protože přístup k databázi je relativně pomalá operace. Nezapisujete testy částí pro logiku zobrazení, protože přístup k zobrazení vyžaduje střídání webového serveru, což je relativně pomalá operace. Neměli byste psát test částí, pokud test může být proveden znovu a znovu velmi rychle

Vzhledem k tomu, že vývoj řízený testováním je řízen testy částí, zaměřujeme se zpočátku na zápis řadiče a obchodní logiky. Vyhýbáme se dotyku databáze nebo zobrazení. Nebudeme upravovat databázi nebo vytvářet naše zobrazení až do samého konce tohoto kurzu. Začneme s tím, co lze testovat.

## <a name="creating-user-stories"></a>Vytváření uživatelských scénářů

Při procvičování vývoje řízeného testováním vždy začínáte napsáním testu. To okamžitě vyvolává otázku: Jak se rozhodnete, jaký test napsat jako první? Chcete-li odpovědět na tuto otázku, měli byste napsat sadu [*uživatelských scénářů*](http://en.wikipedia.org/wiki/User_stories).

Příběh uživatele je velmi stručný (obvykle jedna věta) popis požadavku na software. Měl by se jedná o netechnický popis požadavku napsaného z uživatelského hlediska.

Zde je sada uživatelských scénářů, které popisují funkce vyžadované novou funkcí skupiny kontaktů:

1. Uživatel může zobrazit seznam skupin kontaktů.
2. Uživatel může vytvořit novou skupinu kontaktů.
3. Uživatel může odstranit existující skupinu kontaktů.
4. Uživatel může při vytváření nového kontaktu vybrat skupinu kontaktů.
5. Uživatel může při úpravách existujícího kontaktu vybrat skupinu kontaktů.
6. V zobrazení Rejstřík se zobrazí seznam skupin kontaktů.
7. Když uživatel klepne na skupinu kontaktů, zobrazí se seznam odpovídajících kontaktů.

Všimněte si, že tento seznam uživatelských scénářů je zcela srozumitelný pro zákazníka. Neexistuje žádná zmínka o podrobnostech technické implementace.

Zatímco v procesu vytváření aplikace, sada uživatelských scénářů může být přesnější. Příběh uživatele můžete rozdělit do více článků (požadavků). Můžete se například rozhodnout, že vytvoření nové skupiny kontaktů by mělo zahrnovat ověření. Odeslání skupiny kontaktů bez názvu by mělo vrátit chybu ověření.

Po vytvoření seznamu uživatelských scénářů, jste připraveni napsat první test částí. Začneme vytvořením testování částí pro zobrazení seznamu skupin kontaktů.

## <a name="listing-contact-groups"></a>Výpis skupin kontaktů

Náš první uživatelský příběh je, že uživatel by měl mít možnost zobrazit seznam skupin kontaktů. Musíme ten příběh vyjádřit testem.

Vytvořte nový test částí kliknutím pravým tlačítkem myši na složku Řadiče v projektu ContactManager.Testy, výběrem **možnosti Přidat, Nový test**a výběrem šablony **Testování částí** (viz obrázek 1). Pojmenujte nový test jednotky GroupControllerTest.vb a klepněte na tlačítko **OK.**

[![Přidání testu jednotky GroupControllerTest](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**Obrázek 01**: Přidání testu jednotky GroupControllerTest(Klepnutím[zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image2.png)

Náš první test částí je obsažen v seznamu 1. Tento test ověří, že metoda Index() řadiče skupiny vrátí sadu skupin. Test ověří, zda je v datech zobrazení vrácena kolekce skupin.

**Výpis 1 - Řadiče\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

Při prvním zadání kódu do seznamu 1 v sadě Visual Studio získáte spoustu červených klikatých řádků. Nevytvořili jsme třídy GroupController nebo Group.

V tomto okamžiku můžeme ani sestavit naši aplikaci, takže můžeme t provést náš první test částí. To je dobře. To se počítá jako neúspěšný test. Proto máme nyní oprávnění začít psát kód aplikace. Musíme napsat dostatek kódu k provedení našeho testu.

Třída řadiče skupiny v výpisu 2 obsahuje minimální kód potřebný k předání testu jednotky. Akce Index() vrátí staticky kódovaný seznam skupin (třída Skupiny je definována v seznamu 3).

**Výpis 2 - Řadiče\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**Výpis 3 - Modely\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

Po přidání GroupController a Group třídy do našeho projektu, náš první testování částí úspěšně dokončí (viz obrázek 2). Udělali jsme minimální práci potřebnou k tomu, abychom prošli testem. Je čas oslavovat.

[![Úspěch!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**Obrázek 02**: Úspěch! [(Klikněte pro zobrazení full-size image)](iteration-6-use-test-driven-development-vb/_static/image4.png)

## <a name="creating-contact-groups"></a>Vytváření skupin kontaktů

Nyní můžeme přejít na druhý příběh uživatele. Musíme být schopni vytvořit nové skupiny kontaktů. Musíme tento záměr vyjádřit zkouškou.

Test v výpisu 4 ověří, že volání Create() metoda s novou skupinou přidá skupinu do seznamu skupinvrácených metodou Index(). Jinými slovy, pokud vytvořím novou skupinu, měl bych být schopen získat novou skupinu zpět ze seznamu skupin vrácených metodou Index().

**Výpis 4 - Řadiče\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

Test v výpisu 4 volá metodu Create() řadiče skupiny s novou skupinou kontaktů. Dále test ověří, že volání metody Group controller Index() vrátí novou skupinu v zobrazení dat.

Upravený řadič skupiny v seznamu 5 obsahuje minimální změny potřebné k průchodu nového testu.

**Výpis 5 - Řadiče\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>Řadič skupiny v seznamu 5 má novou akci Vytvořit(). Tato akce přidá skupinu do kolekce skupin. Všimněte si, že akce Index() byla změněna tak, aby vrátila obsah kolekce skupin.

Opět jsme provedli minimální množství práce potřebné k provedení jednotkového testu. Po provázku těchto změn v řadiči skupiny všechny naše testy částí projít.

## <a name="adding-validation"></a>Přidání ověření

Tento požadavek nebyl výslovně uveden v příběhu uživatele. Je však rozumné požadovat, aby skupina měla název. V opačném případě by uspořádání kontaktů do skupin nebylo příliš užitečné.

Výpis 6 obsahuje nový test, který vyjadřuje tento záměr. Tento test ověří, že pokus o vytvoření skupiny bez zadání názvu má za následek chybovou zprávu ověření ve stavu modelu.

**Výpis 6 - Řadiče\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

Aby bylo možné splnit tento test, musíme přidat Name vlastnost naší třídy Skupiny (viz Výpis 7). Kromě toho musíme přidat malý kousek logiky ověření do naší akce group controller s Create() (viz výpis 8).

**Výpis 7 - Modely\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**Výpis 8 - Řadiče\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

Všimněte si, že akce Create() řadiče skupiny nyní obsahuje logiku ověření i databáze. V současné době databáze používá řadič skupiny se skládá z nic víc než kolekce v paměti.

## <a name="time-to-refactor"></a>Čas do refaktoru

Třetím krokem v red/green/refactor je část Refactor. V tomto okamžiku musíme ustoupit od našeho kódu a zvážit, jak můžeme refaktorovat naši aplikaci, abychom zlepšili její návrh. Fáze Refactor je fáze, ve které pečlivě přemýšlíme o nejlepším způsobu implementace principů a vzorů návrhu softwaru.

Máme možnost upravit náš kód jakýmkoli způsobem, který se rozhodneme zlepšit návrh kódu. Máme záchrannou síť testů částí, které nám brání v přerušení stávajících funkcí.

Právě teď, naše skupina řadič je nepořádek z hlediska dobrého softwarového designu. Řadič skupiny obsahuje zamotaný nepořádek ověření a přístupový kód dat. Abychom se vyhnuli porušování zásady jednotné odpovědnosti, musíme tyto obavy rozdělit do různých tříd.

Naše refaktorovaná třída řadiče skupiny je obsažena v seznamu 9. Řadič byl upraven tak, aby používal vrstvu služby ContactManager. Jedná se o stejnou vrstvu služby, kterou používáme s řadičem kontaktu.

Výpis 10 obsahuje nové metody přidané do vrstvy služby ContactManager pro podporu ověřování, výpisu a vytváření skupin. Rozhraní IContactManagerService bylo aktualizováno tak, aby zahrnovalo nové metody.

Výpis 11 obsahuje novou třídu FakeContactManagerRepository, která implementuje rozhraní IContactManagerRepository. Na rozdíl od entityContactManagerRepository třídy, která také implementuje rozhraní IContactManagerRepository, naše nové FakeContactManagerRepository třída nekomunikuje s databází. Třída FakeContactManagerRepository používá kolekci v paměti jako proxy pro databázi. Tuto třídu použijeme v našich jednotkových testech jako falešnou vrstvu úložiště.

**Výpis 9 - Řadiče\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**Výpis 10 - Řadiče\ContactManagerService.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**Výpis 11 - Controllers\FakeContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

Úprava rozhraní IContactManagerRepository vyžaduje použití k implementaci metod CreateGroup() a ListGroups() ve třídě EntityContactManagerRepository. Nejlínější a nejrychlejší způsob, jak to udělat, je přidat metody se zakázaným inzerováním, které vypadají takto:

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

A konečně, tyto změny v návrhu naší aplikace vyžadují, abychom provést některé změny v našich testů částí. Nyní je třeba použít FakeContactManagerRepository při provádění testů částí. Aktualizovaná třída GroupControllerTest je obsažena v výpisu 12.

**Výpis 12 – řadiče\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

Poté, co provedeme všechny tyto změny, znovu všechny naše testy částí projít. Dokončili jsme celý cyklus Red / Green / Refactor. Implementovali jsme první dva příběhy uživatelů. Nyní máme podpůrné testy částí pro požadavky vyjádřené v uživatelských scénářích. Implementace zbývající části scénáře uživatelů zahrnuje opakování stejného cyklu red/green/refactor.

## <a name="modifying-our-database"></a>Úprava naší databáze

Bohužel, i když jsme splnili všechny požadavky vyjádřené v našich jednotkových testech, naše práce není hotová. Stále potřebujeme upravit naši databázi.

Musíme vytvořit novou databázovou tabulku skupiny. Postupujte následovně:

1. V okně Průzkumník serveru klepněte pravým tlačítkem myši na složku Tabulky a vyberte možnost nabídky **Přidat novou tabulku**.
2. Zadejte dva sloupce popsané níže v Návrháři tabulek.
3. Označte sloupec Id jako primární klíč a sloupec Identita.
4. Uložte novou tabulku s názvem Skupiny kliknutím na ikonu diskety.

<a id="0.12_table01"></a>

| **Název sloupce** | **Typ dat** | **Povolit hodnoty Null** |
| --- | --- | --- |
| ID | int | False |
| Název | nvarchar(50) | False |

Dále musíme odstranit všechna data z tabulky Kontakty (jinak nebudeme moci vytvořit relaci mezi tabulkami Kontakty a Skupiny). Postupujte následovně:

1. Klepněte pravým tlačítkem myši na tabulku Kontakty a vyberte možnost nabídky **Zobrazit data tabulky**.
2. Odstraňte všechny řádky.

Dále musíme definovat relaci mezi databázovou tabulkou Skupiny a existující databázovou tabulkou Kontaktů. Postupujte následovně:

1. Poklepáním na tabulku Kontakty v okně Průzkumník serveru otevřete Návrhář e-bulky.
2. Přidejte nový celý sloupec do tabulky Kontakty s názvem GroupId.
3. Klepnutím na tlačítko Vztah otevřete dialogové okno Vztahy cizího klíče (viz obrázek 3).
4. Klikněte na tlačítko Přidat.
5. Klepněte na tlačítko se třemi tečkami, které se zobrazí vedle tlačítka Specifikace tabulky a sloupců.
6. V dialogovém okně Tabulky a sloupce vyberte Skupiny jako tabulku primárního klíče a ID jako sloupec primárního klíče. Vyberte kontakty jako tabulku cizího klíče a GroupId jako sloupec cizího klíče (viz obrázek 4). Klikněte na tlačítko OK.
7. V části **SPECIFIKACE VLOŽENÍ a AKTUALIZACE**vyberte hodnotu **Kaskáda** pro **pravidlo odstranění**.
8. Klepnutím na tlačítko Zavřít zavřete dialogové okno Relace cizího klíče.
9. Klepnutím na tlačítko Uložit uložte změny do tabulky Kontakty.

[![Vytvoření relace tabulky databáze](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**Obrázek 03**: Vytvoření relace tabulky databáze[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image6.png)

[![Určení relací tabulek](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**Obrázek 04**: Určení relací[tabulek(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image8.png)

### <a name="updating-our-data-model"></a>Aktualizace našeho datového modelu

Dále musíme aktualizovat náš datový model, aby reprezentoval novou databázovou tabulku. Postupujte následovně:

1. Poklepáním na soubor ContactManagerModel.edmx ve složce Modely otevřete Návrhář entit.
2. Klepněte pravým tlačítkem myši na povrch návrháře a vyberte možnost nabídky **Aktualizovat model z databáze**.
3. V Průvodci aktualizací vyberte tabulku Skupiny a klepněte na tlačítko Dokončit (viz obrázek 5).
4. Klepněte pravým tlačítkem myši na entitu Skupiny a vyberte možnost nabídky **Přejmenovat**. Změňte název entity *Skupiny* na *Skupiny* (singulární číslo).
5. Klikněte pravým tlačítkem myši na vlastnost Navigace skupin, která se zobrazí v dolní části entity Kontakt. Změňte název vlastnosti Navigace *skupiny* na *Skupinu* (singulární číslo).

[![Aktualizace modelu entity frameworku z databáze](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**Obrázek 05**: Aktualizace modelu entity framework u databáze([Klepnutím zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image10.png)

Po dokončení těchto kroků bude datový model představovat tabulky Kontakty i Skupiny. Návrhář entit by měl zobrazit obě entity (viz obrázek 6).

[![Návrhář entit zobrazuje skupinu a kontakt](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**Obrázek 06**: Návrhář entit zobrazuje skupinu a[kontakt(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image12.png)

### <a name="creating-our-repository-classes"></a>Vytváření našich tříd úložiště

Dále musíme implementovat naši třídu úložiště. V průběhu této iterace jsme přidali několik nových metod do rozhraní IContactManagerRepository při psaní kódu pro splnění našich testů částí. Konečná verze rozhraní IContactManagerRepository je obsažena v výpisu 14.

**Výpis 14 - Modely\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

Ve skutečnosti jsme neimplementovali žádnou z metod souvisejících s prací se skupinami kontaktů v naší skutečné třídě EntityContactManagerRepository. V současné době entityContactManagerRepository třída má metody se zakázaným inzerováním pro každou metodu skupiny kontaktů uvedené v rozhraní IContactManagerRepository. Například listGroups() metoda aktuálně vypadá takto:

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

Metody se zakázaným inzerováním nám umožnily zkompilovat naši aplikaci a předat testy částí. Nyní je však čas skutečně implementovat tyto metody. Konečná verze entityContactManagerRepository třídy je obsažena v výpisu 13.

**Výpis 13 - Modely\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>Vytvoření zobrazení

ASP.NET mvc aplikace při použití výchozího ASP.NET zobrazení motoru. Takže nevytvářejte zobrazení v reakci na konkrétní test částí. Však vzhledem k tomu, že aplikace by k ničemu bez zobrazení, můžeme dokončit tuto iteraci bez vytvoření a úpravy zobrazení obsažených v aplikaci Správce kontaktů.

Pro správu skupin kontaktů musíme vytvořit následující nová zobrazení (viz obrázek 7):

- Zobrazení\Skupina\Index.aspx - Zobrazí seznam skupin kontaktů.
- Zobrazení\Skupina\Delete.aspx - Zobrazí formulář potvrzení pro odstranění skupiny kontaktů.

[![Zobrazení Index skupiny](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**Obrázek 07**: Zobrazení indexu skupiny(Kliknutím[zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image14.png)

Musíme upravit následující existující zobrazení tak, aby zahrnovala skupiny kontaktů:

- Zobrazení\Domů\Vytvořit.aspx
- Zobrazení\Domů\Upravit.aspx
- Zobrazení\Domů\Index.aspx

Upravená zobrazení můžete zobrazit v aplikaci Visual Studio, která doprovází tento kurz. Obrázek 8 například znázorňuje zobrazení Rejstřík kontaktů.

[![Zobrazení Rejstřík kontaktu](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**Obrázek 08**: Zobrazení indexu[kontaktu(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-6-use-test-driven-development-vb/_static/image16.png)

## <a name="summary"></a>Souhrn

V této iteraci jsme přidali nové funkce do naší aplikace Contact Manager podle metodiky návrhu vývojové aplikace řízené testováním. Začali jsme vytvořením sady uživatelských scénářů. Vytvořili jsme sadu testů částí, která odpovídá požadavkům vyjádřeným v uživatelských scénářích. Nakonec jsme napsali jen tolik kódu, aby splňovaly požadavky vyjádřené testy částí.

Poté, co jsme dokončili psaní dostatek kódu ke splnění požadavků vyjádřených testy částí, jsme aktualizovali naši databázi a zobrazení. Do databáze jsme přidali novou tabulku Skupiny a aktualizovali jsme náš datový model entity frameworku. Také jsme vytvořili a upravili sadu zobrazení.

V další iteraci -- poslední iteraci -- přepíšeme naši aplikaci, abychom využili Ajax. Využitím ajaxu zlepšíme odezvu a výkon aplikace Contact Manager.

> [!div class="step-by-step"]
> [Předchozí](iteration-5-create-unit-tests-vb.md)
> [další](iteration-7-add-ajax-functionality-vb.md)
