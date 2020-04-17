---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: 'Iterace #2 – aby aplikace vypadala hezky (C#) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: V této iteraci vylepšujeme vzhled aplikace úpravou výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: ee1d7c92524f6cbdb0f2d7facf85b629e0d91318
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542440"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>Iterace č. 2 – vylepšení vzhledu aplikace (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> V této iteraci vylepšujeme vzhled aplikace úpravou výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Vytvoření aplikace pro správu kontaktů ASP.NET MVC (C#)

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

Cílem této iterace je zlepšit vzhled aplikace Správce kontaktů. V současné době správce kontaktů používá výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů (viz obrázek 1). Tyto dont vypadat špatně, ale já nechci, aby Contact Manager vypadat stejně jako každý jiný ASP.NET webových stránkách MVC. Chci tyto soubory nahradit vlastními soubory.

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**Obrázek 01**: Výchozí vzhled aplikace mvc ASP.NET[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image2.png)

V této iteraci diskutuji o dvou přístupech ke zlepšení vizuálního návrhu naší aplikace. Za prvé, ukážu vám, jak využít ASP.NET Galerie MVC Design ke stažení zdarma ASP.NET mvc design šablony. Galerie ASP.NET MVC Design vám umožní vytvořit profesionální webovou aplikaci bez jakékoli práce.

Rozhodl jsem se nepoužívat šablonu z ASP.NET Galerie MVC Design pro aplikaci Contact Manager. Místo toho jsem měl vlastní design vytvořený profesionální designovou firmou. Ve druhé části tohoto tutoriálu, vysvětlím, jak jsem pracoval s profesionální design společnosti vytvořit finální ASP.NET MVC design.

## <a name="the-aspnet-mvc-design-gallery"></a>Galerie designu MVC ASP.NET

ASP.NET MVC Design Gallery je bezplatný zdroj poskytovaný společností Microsoft. Galerie ASP.NET MVC se nachází na následující adrese:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC Design Gallery hostí sbírku bezplatných návrhů webových stránek, které byly vytvořeny speciálně pro použití v projektu ASP.NET MVC. Návrhy jsou nahrávány členy komunity. Návštěvníci galerie mohou hlasovat pro své oblíbené návrhy (viz obrázek 2).

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**Obrázek 02**: ASP.NET Galerie návrhů MVC[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image4.png)

Jak píšu tento výukový program, nejpopulárnější design v galerii je design s názvem října David Hauser. Tento návrh můžete použít pro projekt ASP.NET MVC provedením následujících kroků:

1. Klepnutím na tlačítko **Stáhnout** stáhněte soubor October.zip do počítače.
2. Klikněte pravým tlačítkem myši na stažený soubor October.zip a klikněte na tlačítko **Odblokovat** (viz obrázek 3).
3. Rozbalte soubor do složky s názvem Říjen.
4. Vyberte všechny soubory ze složky DesignTemplate obsažené ve složce Říjen, klepněte pravým tlačítkem myši na soubory a vyberte možnost nabídky **Kopírovat**.
5. Klepněte pravým tlačítkem myši na uzel projektu ContactManager v okně Průzkumník řešení sady Visual Studio a vyberte možnost nabídky **Vložit** (viz obrázek 4).
6. Vyberte možnost nabídky Visual Studio **Upravit, Najít a nahradit, Rychle nahradit** a nahradit *[MyProjectName]* *contactmanagerem* (viz obrázek 5).

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**Obrázek 03**: Odblokování souboru staženého z webu[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image6.png)

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**Obrázek 04**: Přepsání souborů v Průzkumníku řešení[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image8.png)

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**Obrázek 05**: Nahrazení [Název_projektu] contactmanagerem[(Klepnutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image10.png)

Po dokončení těchto kroků bude vaše webová aplikace používat nový návrh. Stránka na obrázku 6 znázorňuje vzhled aplikace Správce kontaktů s říjnovým návrhem.

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**Obrázek 06**: ContactManager se šablonou říjen[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image12.png)

## <a name="creating-a-custom-aspnet-mvc-design"></a>Vytvoření vlastního ASP.NET návrhu MVC

ASP.NET MVC Design Gallery má dobrý výběr různých stylů designu. Galerie vám poskytuje bezbolestný způsob, jak přizpůsobit vzhled vašich aplikací ASP.NET MVC. A samozřejmě, galerie má velkou výhodu, že je zcela zdarma.

Možná však budete muset vytvořit zcela jedinečný design pro vaše webové stránky. V takovém případě má smysl pracovat s firmou zabývající se navrhováním webových stránek. Rozhodl jsem se přijmout tento přístup pro návrh aplikace Contact Manager.

I zip do Contact Manager z iterace #1 a poslal projekt na návrh společnosti. Neměli vlastní Visual Studio (hanba na ně!), Ale to nepředstavovalo problém. Z [https://www.asp.net](https://www.asp.net) webu mohli zdarma stáhnout aplikaci Microsoft Visual Web Developer a otevřít aplikaci Contact Manager v aplikaci Visual Web Developer. Za pár dní, oni produkovali design na obrázku 7.

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**Obrázek 07**: Návrh správce kontaktů ASP.NET MVC[(klepnutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image14.png)

Nový návrh se skládal ze dvou hlavních souborů: nového souboru šablony stylů a nového souboru stránky předlohy zobrazení. Stránka předlohy zobrazení obsahuje rozložení a sdílený obsah pro zobrazení v ASP.NET aplikace MVC. Stránka předlohy zobrazení například obsahuje záhlaví, navigační karty a zápatí, které se zobrazují na obrázku 7. Přepsal jsem existující stránku předlohy zobrazení Site.Master ve složce Zobrazení\Sdílené s novým souborem Site.Master od návrhářské společnosti,

Návrhářská společnost také vytvořila novou kaskádovou šablonu stylů a sadu obrázků. Umístil jsem tyto nové soubory do složky Obsah a přepsal existující soubor Site.css. Do složky Obsah byste měli umístit veškerý statický obsah.

Všimněte si, že nový návrh Správce kontaktů obsahuje obrázky pro úpravy a odstranění kontaktů. Vedle každého kontaktu v tabulce kontaktů html se zobrazí obrázek Upravit a odstranit.

Původně tyto odkazy, které byly vykresleny s HTML. ActionLink() pomocník takhle:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

Metoda Html.ActionLink() nepodporuje obrázky (metoda HTML z bezpečnostních důvodů kóduje text odkazu). Proto jsem nahradil volání Html.ActionLink() s voláníurl.Action() takto:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

Metoda Html.ActionLink() vykreslí celý hypertextový odkaz HTML. Url.Action() metoda, na druhé straně, vykreslí &lt;pouze&gt; URL bez značky.

Všimněte si dále, že nový návrh obsahuje vybrané i nevybrané karty. Například na obrázku 8 je vybrána karta **Vytvořit nový kontakt** a karta Moje **kontakty** není vybraná.

[![Dialogové okno New Project (Nový projekt)](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**Obrázek 08**: Vybrané a nevybrané karty([Kliknutím zobrazíte obrázek v plné velikosti)](iteration-2-make-the-application-look-nice-cs/_static/image16.png)

Pro podporu vykreslování vybraných i nevybraných karet jsem vytvořil vlastní pomocník HTML s názvem MenuItemHelper. Tato pomocná metoda vykreslí buď &lt;značku&gt; li nebo značku &lt;li class="selected"&gt; v závislosti na tom, zda aktuální kontroler a akce odpovídají kontroleru a názvu akce předané pomocni. Kód pro MenuItemHelper je obsažen v výpisu 1.

**Výpis 1 - Helpers\MenuItemHelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

MenuItemHelper používá tagbuilder třídy interně &lt;&gt; k vytvoření značky li HTML. Třída TagBuilder je velmi užitečná třída nástrojů, kterou můžete použít vždy, když potřebujete vytvořit novou značku HTML. Zahrnuje metody pro přidávání atributů, přidávání tříd CSS, generování ID a úpravu vnitřního HTML značky.

## <a name="summary"></a>Souhrn

V této iteraci jsme vylepšili vizuální návrh naší aplikace ASP.NET MVC. Nejprve jste byli představeni ASP.NET MVC Design Gallery. Naučili jste se stahovat bezplatné šablony návrhů z ASP.NET MVC Design Gallery, které můžete použít ve svých ASP.NET aplikací MVC.

Dále jsme probrali, jak můžete vytvořit vlastní návrh úpravou výchozího souboru šablony stylů a stránkového souboru předlohy. Abychom podpořili nový návrh, museli jsme provést drobné změny v naší aplikaci Contact Manager. Například jsme přidali nový pomocník HTML s názvem MenuItemHelper, který zobrazuje vybrané a nevybrané karty.

V další iteraci se zabýváme velmi důležitým tématem ověřování. Do naší aplikace přidáme ověřovací kód, aby uživatel nemohl vytvořit nový kontakt bez zadání požadovaných hodnot, jako je jméno a příjmení osoby.

> [!div class="step-by-step"]
> [Předchozí](iteration-1-create-the-application-cs.md)
> [další](iteration-3-add-form-validation-cs.md)
