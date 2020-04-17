---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: 'Iterace #1 – vytvoření aplikace (C#) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: 'V první iteraci vytvoříme Správce kontaktů nejjednodušším možným způsobem. Přidáváme podporu pro základní databázové operace: Vytvořit, Číst, Aktualizovat a D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: ecc3c1201c784e20c6b2601735bee3d4ce721f22
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542544"
---
# <a name="iteration-1--create-the-application-c"></a>Iterace č. 1 – vytvoření aplikace (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> V první iteraci vytvoříme Správce kontaktů nejjednodušším možným způsobem. Přidáváme podporu pro základní databázové operace: Vytvořit, Číst, Aktualizovat a odstranit (CRUD).

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

V této první iteraci vytvoříme základní aplikaci. Cílem je vytvořit Správce kontaktů nejrychlejším a nejjednodušším možným způsobem. V pozdějších iterací, zlepšujeme návrh aplikace.

Aplikace Contact Manager je základní databázově řízená aplikace. Aplikaci můžete použít k vytvoření nových kontaktů, úpravám existujících kontaktů a odstranění kontaktů.

V této iteraci provedeme následující kroky:

1. ASP.NET aplikace MVC
2. Vytvoření databáze pro uložení našich kontaktů
3. Generovat třídu modelu pro naši databázi pomocí rozhraní Microsoft Entity Framework
4. Vytvoření akce a zobrazení kontroleru, které nám umožní vypsat všechny kontakty v databázi
5. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje vytvořit nový kontakt v databázi
6. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje upravit existující kontakt v databázi
7. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje odstranit existující kontakt v databázi

## <a name="software-prerequisites"></a>Softwarové požadavky

V ASP.NET aplikací mvc musíte mít v počítači nainstalovanou aplikaci Visual Studio 2008 nebo Visual Web Developer 2008 (Visual Web Developer je bezplatná verze sady Visual Studio, která neobsahuje všechny pokročilé funkce sady Visual Studio). Zkušební verzi sady Visual Studio 2008 nebo Visual Web Developer si můžete stáhnout z následující adresy:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Pro ASP.NET aplikací MVC s aplikací Visual Web Developer musíte mít nainstalovanou aktualizaci Visual Web Developer Service Pack 1. Bez aktualizace Service Pack 1 nelze vytvářet projekty webových aplikací.

ASP.NET rámci MVC. Rozhraní ASP.NET MVC framework si můžete stáhnout z následující adresy:

[https://www.asp.net/mvc](../../../index.md)

V tomto kurzu používáme Microsoft Entity Framework pro přístup k databázi. Entity Framework je součástí rozhraní .NET Framework 3.5 Service Pack 1. Tuto aktualizaci Service Pack si můžete stáhnout z následujícího umístění:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Jako alternativu k provádění každého z těchto stažení jeden po druhém můžete využít Instalační službu webové platformy (Web PI). Web PI si můžete stáhnout z následující adresy:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET projekt MVC

ASP.NET projekt webové aplikace MVC. Spusťte Visual Studio a vyberte možnost nabídky **Soubor, Nový projekt**. Zobrazí se dialogové okno **Nový projekt** (viz obrázek 1). Vyberte typ **webového** projektu a ASP.NET šablonu **webové aplikace MVC.** Pojmenujte svůj nový projekt *ContactManager* a klepněte na tlačítko OK.

Ujistěte se, že máte v rozevíracím seznamu v pravém horním rohu dialogového okna **Nový projekt** vybranou možnost Rozhraní .NET Framework 3.5. V opačném případě se ASP.NET šablona webové aplikace MVC nezobrazí.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**Obrázek 01**: Dialogové okno Nový projekt([Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image2.png)

ASP.NET aplikace MVC se zobrazí dialogové okno **Vytvořit projekt testování částí.** Toto dialogové okno můžete použít k označení, že chcete vytvořit a přidat projekt testování částí do vašeho řešení při vytváření aplikace ASP.NET MVC. I když nebudeme stavební testy částí v této iteraci, měli byste vybrat možnost **Ano, vytvořit projekt testování částí,** protože plánujeme přidat testy částí v pozdější iteraci. Přidání testovacího projektu při prvním vytvoření nového ASP.NET projektu MVC je mnohem jednodušší než přidání testovacího projektu po vytvoření projektu ASP.NET MVC.

> [!NOTE] 
> 
> Vzhledem k tomu, že aplikace Visual Web Developer nepodporuje testovací projekty, nezískáte při použití aplikace Visual Web Developer dialogové okno Vytvořit projekt testování částí.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**Obrázek 02**: Dialogové okno Vytvořit projekt testování částí[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image4.png)

ASP.NET aplikace MVC se zobrazí v okně Průzkumníka řešení sady Visual Studio (viz obrázek 3). Pokud se okno Průzkumník řešení nezobrazí, můžete toto okno otevřít výběrem možnosti **Nabídky Zobrazení, Průzkumník řešení**. Všimněte si, že řešení obsahuje dva projekty: ASP.NET projektu MVC a testovací projekt. Projekt ASP.NET MVC se jmenuje ContactManager a projekt Test se nazývá ContactManager.Tests.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**Obrázek 03**: Okno Průzkumník řešení[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image6.png)

## <a name="deleting-the-project-sample-files"></a>Odstranění ukázkových souborů projektu

Šablona projektu ASP.NET MVC obsahuje ukázkové soubory pro řadiče a zobrazení. Před vytvořením nové aplikace ASP.NET MVC byste měli tyto soubory odstranit. Soubory a složky v okně Průzkumník řešení můžete odstranit tak, že klepnete pravým tlačítkem myši na soubor nebo složku a vyberete možnost **Nabídky Odstranit**.

Je třeba odstranit následující soubory z projektu ASP.NET MVC:

- \Controllers\HomeController.cs

- \Zobrazení\Domů\About.aspx

- \Zobrazení\Domů\Index.aspx

A je třeba odstranit následující soubor z projektu Test:

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>Vytvoření databáze

Aplikace Contact Manager je webová aplikace řízená databází. K ukládání kontaktních informací používáme databázi.

Rozhraní ASP.NET MVC s libovolnou moderní databází včetně databází Microsoft SQL Server, Oracle, MySQL a IBM DB2. V tomto kurzu používáme databázi serveru Microsoft SQL Server. Při instalaci sady Visual Studio máte možnost instalace aplikace Microsoft SQL Server Express, která je bezplatnou verzí databáze serveru Microsoft SQL Server.

Vytvořte novou databázi tak,\_že kliknete pravým tlačítkem myši na složku Data aplikace v okně Průzkumník řešení a vyberete možnost nabídky **Přidat, novou položku**. V dialogovém okně **Přidat novou položku** vyberte kategorii **Data** a šablonu databáze serveru **SQL Server** (viz obrázek 4). Pojmenujte novou databázi ContactManagerDB.mdf a klepněte na tlačítko OK.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**Obrázek 04**: Vytvoření nové databáze Microsoft SQL Server Express ([Klepnutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-cs/_static/image8.png))

Po vytvoření nové databáze se databáze zobrazí\_ve složce Data aplikace v okně Průzkumník řešení. Poklepáním na soubor ContactManager.mdf otevřete okno Průzkumníka serveru a připojte se k databázi.

> [!NOTE] 
> 
> Okno Průzkumník serveru se nazývá okno Průzkumník databáze v případě aplikace Microsoft Visual Web Developer.

Okno Průzkumník serveru můžete použít k vytvoření nových databázových objektů, jako jsou databázové tabulky, zobrazení, aktivační události a uložené procedury. Klepněte pravým tlačítkem myši na složku Tabulky a vyberte možnost nabídky **Přidat novou tabulku**. Zobrazí se Návrhář tabulky databáze (viz obrázek 5).

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**Obrázek 05**: Návrhář tabulky databáze[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image10.png)

Potřebujeme vytvořit tabulku, která obsahuje následující sloupce:

<a id="0.1_table01"></a>

| **Název sloupce** | **Typ dat** | **Povolit hodnoty Null** |
| --- | --- | --- |
| ID | int | false (nepravda) |
| FirstName | nvarchar(50) | false (nepravda) |
| LastName | nvarchar(50) | false (nepravda) |
| Telefon | nvarchar(50) | false (nepravda) |
| E-mail | nvarchar(255) | false (nepravda) |

První sloupec, sloupec ID, je zvláštní. Sloupec ID je třeba označit jako sloupec Identita a sloupec Primární klíč. Můžete označit, že sloupec je sloupec identity rozbalením vlastnosti sloupce (podívejte se na obrázek 6) a posouvání dolů na identity specifikace vlastnost. Nastavte vlastnost **(Je identita)** na hodnotu **Ano**.

Sloupec označíte jako sloupec primárního klíče tak, že jej vyberete a kliknete na tlačítko s ikonou klávesy. Jakmile je sloupec označen jako sloupec Primární klíč, zobrazí se vedle sloupce ikona klíče (viz obrázek 6).

Po dokončení vytváření tabulky uložte novou tabulku klepnutím na tlačítko Uložit (tlačítko s ikonou diskety). Pojmenujte novou tabulku názvem *Kontakty*.

Po dokončení vytváření tabulky databáze kontaktů byste měli do tabulky přidat některé záznamy. Klepněte pravým tlačítkem myši na tabulku Kontakty v okně Průzkumník serveru a vyberte možnost nabídky **Zobrazit data tabulky**. Do mřížky, která se zobrazí, zadejte jeden nebo více kontaktů.

## <a name="creating-the-data-model"></a>Vytvoření datového modelu

Aplikace ASP.NET MVC se skládá z modelů, zobrazení a řadičů. Začneme vytvořením třídy Model, která představuje tabulku Kontakty, kterou jsme vytvořili v předchozí části.

V tomto kurzu používáme Microsoft Entity Framework pro generování třídy modelu z databáze automaticky.

> [!NOTE] 
> 
> Rozhraní ASP.NET MVC není žádným způsobem vázáno na rozhraní Microsoft Entity Framework. Můžete použít ASP.NET MVC s alternativními technologiemi přístupu k databázi, včetně NHibernate, LINQ na SQL nebo ADO.NET.

Chcete-li vytvořit třídy datového modelu, postupujte takto:

1. Klepněte pravým tlačítkem myši na složku Modely v okně Průzkumník řešení a vyberte **přidat novou položku**. Zobrazí se dialogové okno **Přidat novou položku** (viz obrázek 6).
2. Vyberte kategorii **Data** a šablonu **ADO.NET datového modelu entity.** Pojmenujte svůj datový model *ContactManagerModel.edmx* a klepněte na tlačítko **Přidat.** Zobrazí se Průvodce datovým modelem entity (viz obrázek 7).
3. V kroku **Zvolit obsah modelu** vyberte Generovat z **databáze** (viz obrázek 7).
4. V kroku **Zvolit datové připojení** vyberte databázi ContactManagerDB.mdf a zadejte název *ContactManagerDBEntities* pro nastavení připojení entity (viz obrázek 8).
5. V kroku **Zvolit databázové objekty** zaškrtněte políčko tabulky s popiskem (viz obrázek 9). Datový model bude obsahovat všechny tabulky obsažené v databázi (existuje pouze jedna tabulka Kontakty). Zadejte *modely*oboru názvů . Průvodce dokončete klepnutím na tlačítko Dokončit.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**Obrázek 06**: Dialogové okno Přidat novou položku[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image12.png)

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**Obrázek 07**: Zvolte obsah modelu[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image14.png)

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**Obrázek 08**: Vyberte datové připojení[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image16.png)

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**Obrázek 09**: Vyberte databázové objekty[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image18.png)

Po dokončení Průvodce datovým modelem entity se zobrazí Návrhář datového modelu entity. Návrhář zobrazí třídu, která odpovídá každé modelované tabulce. Měli byste vidět jednu třídu s názvem Kontakty.

Průvodce datovým modelem entity generuje názvy tříd na základě názvů tabulek databáze. Téměř vždy je třeba změnit název třídy generované průvodcem. Klepněte pravým tlačítkem myši na třídu Kontakty v návrháři a vyberte volbu nabídky **Přejmenovat**. Změňte název třídy z Kontakty (množné číslo) na Kontakt (jednotné číslo). Po změně názvu třídy by měla třída vypadat jako obrázek 10.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**Obrázek 10**: Třída Kontakt[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image20.png)

V tomto okamžiku jsme vytvořili náš databázový model. Můžeme použít Kontakt třídy představují konkrétní záznam kontaktu v naší databázi.

## <a name="creating-the-home-controller"></a>Vytvoření domácího řadiče

Dalším krokem je vytvoření našeho domácího ovladače. Domácí kontroler je výchozí řadič vyvolaný v ASP.NET aplikace MVC.

Vytvořte třídu Domácí kontroler kliknutím pravým tlačítkem myši na složku Řadiče v okně Průzkumník řešení a výběrem možnosti nabídky **Přidat, řadič** (viz obrázek 11). Všimněte si zaškrtávacího políčka s názvem **Přidat metody akce pro scénáře Vytvořit, Aktualizovat a Podrobnosti**. Před kliknutím na tlačítko **Přidat** zaškrtněte políčko, zda je zaškrtnuté políčko.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**Obrázek 11**: Přidání ovladače Domů[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image22.png)

Když vytvoříte domácí ovladač, získáte třídu v výpisu 1.

**Výpis 1 - Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>Výpis kontaktů

Aby bylo možné zobrazit záznamy v tabulce databáze kontaktů, musíme vytvořit akci Index() a zobrazení indexu.

Domácí kontroler již obsahuje akci Index(). Musíme upravit tuto metodu tak, aby to vypadalo jako Výpis 2.

**Výpis 2 - Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

Všimněte si, že třída Domácí kontrolor \_ve výpisu 2 obsahuje soukromé pole s názvem entity. Pole \_entity představuje entity z datového modelu. Pole \_entity používáme ke komunikaci s databází.

Metoda Index() vrátí zobrazení, které představuje všechny kontakty z tabulky databáze kontaktů. Entity \_výrazu. ContactSet.ToList() vrátí seznam kontaktů jako obecný seznam.

Teď, když jsme vytvořili řadič indexu, budeme dále muset vytvořit zobrazení indexu. Před vytvořením zobrazení indexu zkompilujte aplikaci výběrem možnosti nabídky **Sestavení, Sestavení řešení**. Před přidáním zobrazení byste měli vždy zkompilovat projekt, aby se seznam tříd modelu zobrazil v dialogovém okně **Přidat zobrazení.**

Zobrazení rejstříku vytvoříte klepnutím pravým tlačítkem myši na metodu Index() a výběrem možnosti nabídky **Přidat zobrazení** (viz obrázek 12). Výběrem této možnosti nabídky se otevře dialogové okno **Přidat zobrazení** (viz obrázek 13).

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**Obrázek 12**: Přidání zobrazení rejstříku[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image24.png)

V dialogovém okně **Přidat zobrazení** zaškrtněte políčko Vytvořit **zobrazení silného typu**. Vyberte zobrazit třídu dat ContactManager.Models.Kontakt a Zobrazit seznam obsahu. Výběrem těchto možností se vygeneruje zobrazení, které zobrazí seznam záznamů kontaktů.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**Obrázek 13**: Dialogové okno Přidat zobrazení[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image26.png)

Po klepnutí na tlačítko **Přidat** se vygeneruje zobrazení Rejstříku v seznamu 3. Všimněte &lt;si direktivy %@ Page %,&gt; která se zobrazí v horní části souboru. Zobrazení indexu dědí z&lt;třídy ContactManager.Models.Contact&lt;&gt; &gt; aplikace ViewPage IEnumerable. Jinými slovy, třída Model v zobrazení představuje seznam entit Kontakt.

Tělo zobrazení Index obsahuje foreach smyčky, která iterates prostřednictvím každého z kontaktů reprezentované Model třídy. Hodnota každé vlastnosti třídy Kontakt je zobrazena v tabulce HTML.

**Výpis 3 - Zobrazení\Home\Index.aspx (beze změny)**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

Musíme provést jednu změnu zobrazení indexu. Protože nevytváříme zobrazení podrobnosti, můžeme odebrat odkaz Podrobnosti. V zobrazení rejstříku vyhledejte a odeberte následující kód:

{ id=položka. Id })%&gt;

Po úpravě zobrazení rejstříku můžete spustit aplikaci Správce kontaktů. Vyberte možnost nabídky Ladění, Spustit ladění nebo jednoduše stiskněte klávesu F5. Při prvním spuštění aplikace se zobrazí dialogové okno na obrázku 14. Vyberte volbu **Změnit soubor Web.config, chcete-li povolit ladění,** a klepněte na tlačítko OK.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**Obrázek 14**: Povolení ladění[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image28.png)

Zobrazení rejstříku je vráceno ve výchozím nastavení. Toto zobrazení obsahuje seznam všech dat z tabulky databáze kontaktů (viz obrázek 15).

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**Obrázek 15**: Zobrazení rejstříku[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image30.png)

Všimněte si, že zobrazení Rejstřík obsahuje odkaz s názvem Vytvořit nový v dolní části zobrazení. V další části se dozvíte, jak vytvořit nové kontakty.

## <a name="creating-new-contacts"></a>Vytváření nových kontaktů

Abychom uživatelům umožnili vytvářet nové kontakty, musíme do domácího kontroleru přidat dvě akce Vytvořit(). Musíme vytvořit jednu akci Create(), která vrátí formulář HTML pro vytvoření nového kontaktu. Musíme vytvořit druhou Create() akce, která provádí vlastní databázi vložit nového kontaktu.

Nové Create() metody, které musíme přidat do domácího řadiče jsou obsaženy v výpisu 4.

**Výpis 4 - Controllers\HomeController.cs (s create metody)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

První Create() metoda může být vyvolána s HTTP GET, zatímco druhá Create() metoda může být vyvolána pouze HTTP POST. Jinými slovy, druhou metodu Create() lze vyvolat pouze při zaúčtování formuláře HTML. První Metoda Create() jednoduše vrátí zobrazení, které obsahuje formulář HTML pro vytvoření nového kontaktu. Druhá metoda Create() je mnohem zajímavější: přidá nový kontakt do databáze.

Všimněte si, že druhá metoda Create() byla změněna tak, aby přijala instanci třídy Contact. Hodnoty formuláře zaúčtované z formuláře HTML jsou automaticky vázány na tuto třídu Kontakt ASP.NET rozhraním MVC. Každé pole formuláře z formuláře Html Create je přiřazeno vlastnosti parametru Kontakt.

Všimněte si, že parametr Kontakt je dekorován atributem [Bind]. Atribut [Bind] se používá k vyloučení vlastnosti Contact Id z vazby. Protože Id vlastnost představuje Identity vlastnost, nechceme nastavit Id vlastnost.

V těle Create() metoda entity Framework se používá k vložení nového kontaktu do databáze. Nový Kontakt je přidán do existující sady kontaktů a SaveChanges() metoda je volána k push tyto změny zpět do podkladové databáze.

Formulář HTML pro vytváření nových kontaktů můžete vygenerovat kliknutím pravým tlačítkem myši na některou ze dvou metod Create() a výběrem možnosti nabídky **Přidat zobrazení** (viz obrázek 16).

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**Obrázek 16**: Přidání zobrazení vytvořit[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image32.png)

V dialogovém okně **Přidat zobrazení** vyberte třídu **ContactManager.Models.Contact** a volbu **Vytvořit** pro zobrazení obsahu (viz obrázek 17). Po klepnutí na tlačítko **Přidat** se automaticky vygeneruje zobrazení Vytvořit.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**Obrázek 17**: Zobrazení rozložení stránky[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image34.png)

Zobrazení Vytvořit obsahuje pole formuláře pro každou vlastnost třídy Kontakt. Kód pro vytvořit zobrazení je součástí výpisu 5.

**Výpis 5 - Zobrazení\Domů\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Po úpravě metod Create() a přidání zobrazení Vytvořit můžete spustit aplikaci Contact Manger a vytvořit nové kontakty. Kliknutím na odkaz **Vytvořit nový,** který se zobrazí v zobrazení Rejstřík, přejdete do zobrazení Vytvořit. Měli byste vidět pohled na obrázku 18.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**Obrázek 18**: Zobrazení vytvoření[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image36.png)

## <a name="editing-contacts"></a>Úpravy kontaktů

Přidání funkce pro úpravu záznamu kontaktu je velmi podobné přidání funkce pro vytváření nových záznamů kontaktů. Nejprve musíme přidat dvě nové metody úprav do třídy domácího kontroleru. Tyto nové edit() metody jsou obsaženy v výpisu 6.

**Výpis 6 - Controllers\HomeController.cs (s metodami úprav)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

První metoda Edit() je vyvolána operací HTTP GET. Parametr Id je předán této metodě, která představuje ID upravovaného záznamu kontaktu. Entity Framework se používá k načtení kontaktu, který odpovídá ID. Je vráceno zobrazení obsahující formulář HTML pro úpravy záznamu.

Druhá metoda Edit() provede skutečnou aktualizaci databáze. Tato metoda přijímá instanci Contact třídy jako parametr. Rozhraní ASP.NET MVC automaticky sváže pole formuláře z formuláře Upravit na tuto třídu. Všimněte si, že při úpravách kontaktu nezahrnete atribut [Bind] (potřebujeme hodnotu vlastnosti Id).

Entity Framework se používá k uložení upraveného kontaktu do databáze. Původní kontakt musí být nejprve načten z databáze. Dále entity Framework ApplyPropertyChanges() metoda je volána k záznamu změny Kontakt. Nakonec entity Framework SaveChanges() metoda je volána zachovat změny podkladové databáze.

Zobrazení, které obsahuje formulář Pro úpravy, můžete vygenerovat klepnutím pravým tlačítkem myši na metodu Edit() a výběrem možnosti nabídky Přidat zobrazení. V dialogovém okně Přidat zobrazení vyberte třídu **ContactManager.Models.Contact** a obsah **zobrazení pro úpravy** (viz obrázek 19).

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**Obrázek 19**: Přidání zobrazení úprav[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image38.png)

Po klepnutí na tlačítko Přidat se automaticky vygeneruje nové zobrazení úprav. Formulář HTML, který je generován, obsahuje pole, která odpovídají každé z vlastností třídy Kontakt (viz Výpis 7).

**Výpis 7 - Zobrazení\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Odstranění kontaktů

Pokud chcete odstranit kontakty, musíte přidat dvě akce Delete() do třídy Domácí ho dioda. První akce Delete() zobrazí formulář potvrzení odstranění. Druhá akce Delete() provede skutečné odstranění.

> [!NOTE] 
> 
> Později v iteraci #7, upravíme Správce kontaktů tak, aby podporuje jeden krok Ajax odstranit.

Dvě nové Delete() metody jsou obsaženy v výpisu 8.

**Výpis 8 - Controllers\HomeController.cs (Odstranit metody)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

První Delete() Metoda vrátí potvrzovací formulář pro odstranění záznamu kontaktu z databáze (viz obrázek20). Druhá Delete() Metoda provede skutečnou operaci odstranění proti databázi. Po načtení původního kontaktu z databáze jsou k odstranění databáze volány metody Entity Framework DeleteObject() a SaveChanges().

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**Obrázek 20**: Zobrazení potvrzení odstranění[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image40.png)

Potřebujeme upravit zobrazení indexu tak, aby obsahovalo odkaz pro odstranění záznamů kontaktů (viz obrázek 21). Do stejné buňky tabulky, která obsahuje odkaz Upravit, je třeba přidat následující kód:

Html.ActionLink( { id=položka. Id }) %&gt;

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**Obrázek 21**: Zobrazení rejstříku s odkazem Upravit[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image42.png)

Dále musíme vytvořit zobrazení potvrzení odstranění. Klikněte pravým tlačítkem myši na metodu Delete() ve třídě Domácí ho kontroleru a vyberte možnost Nabídky Přidat zobrazení. Zobrazí se dialogové okno Přidat zobrazení (viz obrázek 22).

Na rozdíl od zobrazení Seznam, Vytvořit a Upravit v případě zobrazení Přidat zobrazení neobsahuje možnost vytvoření zobrazení Odstranit. Místo toho vyberte třídu **ContactManager.Models.Contact** data a **obsah prázdného** zobrazení. Výběr možnosti Prázdný obsah zobrazení bude vyžadovat, abychom si zobrazení vytvořili sami.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**Obrázek 22**: Přidání zobrazení potvrzení odstranění[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image44.png)

Obsah zobrazení Odstranit je obsažen v seznamu 9. Toto zobrazení obsahuje formulář, který potvrzuje, zda má být určitý kontakt odstraněn (viz obrázek 21).

**Výpis 9 - Zobrazení\Domů\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Změna názvu výchozího řadiče

Může vás obtěžovat, že název naší třídy kontroleru pro práci s kontakty se nazývá Třída HomeController. Neměl by být řadič pojmenován ContactController?

Tento problém je dost snadné opravit. Nejprve musíme refaktorovat název domácího řadiče. Otevřete třídu HomeController v Editoru kódu sady Visual Studio, klikněte pravým tlačítkem myši na název třídy a vyberte možnost nabídky **Refactor, Přejmenovat**. Výběrem této volby nabídky se otevře dialogové okno Přejmenovat.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**Obrázek 23**: Refaktoring názvu řadiče[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image46.png)

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**Obrázek 24**: Použití dialogového okna Přejmenovat[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image48.png)

Pokud přejmenujete třídu řadiče, Visual Studio aktualizuje název složky ve složce Zobrazení také. Aplikace Visual Studio přejmenuje složku \Views\Home na složku \Views\Contact.

Po provedení této změny aplikace již nebude mít domácí ovladač. Při spuštění aplikace se zobrazí chybová stránka na obrázku 25.

[![Dialogové okno New Project (Nový projekt)](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**Obrázek 25**: Žádný výchozí řadič[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-1-create-the-application-cs/_static/image50.png)

Musíme aktualizovat výchozí trasu v souboru Global.asax, abychom místo řadiče Home použili řadič kontaktů. Otevřete soubor Global.asax a upravte výchozí řadič používaný výchozí trasou (viz Výpis 10).

**Výpis 10 - Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

Po provedeném provádění těchto změn bude Správce kontaktů pracovat správně. Nyní bude používat třídu řadiče Kontakt jako výchozí řadič.

## <a name="summary"></a>Souhrn

V této první iteraci jsme vytvořili základní aplikaci Contact Manager nejrychlejším možným způsobem. Využili jsme Visual Studio ke generování počáteční kód pro naše řadiče a zobrazení automaticky. Také jsme využili entity framework automaticky generovat naše třídy modelu databáze.

V současné době můžeme v aplikaci Správce kontaktů vypsat, vytvořit, upravit a odstranit záznamy kontaktů. Jinými slovy, můžeme provádět všechny základní databázové operace vyžadované databázovou webovou aplikací.

Bohužel, naše aplikace má nějaké problémy. Za prvé a váhám to přiznat, aplikace Contact Manager není nejatraktivnější aplikací. Potřebuje nějakou konstrukční práci. V další iteraci se podíváme na to, jak můžeme změnit výchozí stránku předlohy zobrazení a kaskádovou šablonu stylů, abychom zlepšili vzhled aplikace.

Za druhé jsme neimplementovali žádné ověření formuláře. Nic například nebrání odeslání formuláře Vytvořit kontakt bez zadání hodnot pro libovolné pole formuláře. Kromě toho můžete zadat neplatná telefonní čísla a e-mailové adresy. Začneme řešit problém ověření formuláře v iteraci #3.

Nakonec a co je nejdůležitější, aktuální iteraci aplikace Správce kontaktů nelze snadno upravit nebo udržovat. Například logika přístupu k databázi je pečené přímo do akce kontroleru. To znamená, že nemůžeme změnit náš kód pro přístup k datům bez úpravy našich správců. V pozdějších iteracích zkoumáme návrhové vzory softwaru, které můžeme implementovat, aby byl Správce kontaktů odolnější vůči změnám.

> [!div class="step-by-step"]
> [Další](iteration-2-make-the-application-look-nice-cs.md)
