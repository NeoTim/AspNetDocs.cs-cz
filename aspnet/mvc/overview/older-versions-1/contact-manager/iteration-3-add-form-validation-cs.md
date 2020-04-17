---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '#3 iterace – přidání ověření formuláře (C#) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: Ve třetí iteraci přidáme ověření základního formuláře. Bráníme uživatelům v odesílání formuláře bez vyplnění požadovaných polí formuláře. Také jsme ověřit emai ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: c8442574d4901045f044f53ea12cd8330e8eaaa3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542375"
---
# <a name="iteration-3--add-form-validation-c"></a>Iterace č. 3 – přidání ověřovacího formuláře (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> Ve třetí iteraci přidáme ověření základního formuláře. Bráníme uživatelům v odesílání formuláře bez vyplnění požadovaných polí formuláře. Ověřujeme také e-mailové adresy a telefonní čísla.

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

V této druhé iteraci aplikace Správce kontaktů přidáme ověření základního formuláře. Bráníme uživatelům v odeslání kontaktu bez zadávání hodnot pro požadovaná pole formuláře. Ověřujeme také telefonní čísla a e-mailové adresy (viz obrázek 1).

[![Dialogové okno New Project (Nový projekt)](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**Obrázek 01**: Formulář s ověřením[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-3-add-form-validation-cs/_static/image2.png)

V této iteraci přidáme logiku ověření přímo do akce kontroleru. Obecně se nejedná o doporučený způsob přidání ověření do aplikace mvc ASP.NET. Lepším přístupem je umístění logiky ověření aplikace s do samostatné [vrstvy služby](http://martinfowler.com/eaaCatalog/serviceLayer.html). V další iteraci refaktorujeme aplikaci Contact Manager, aby byla aplikace udržovatelná.

V této iteraci, aby věci jednoduché, píšeme všechny ověřovací kód ručně. Místo psaní ověřovacího kódu sami, můžeme využít rámec ověřování. Můžete například použít blok žádosti o ověření podnikové knihovny Microsoft Enterprise (VAB) k implementaci logiky ověření pro ASP.NET aplikaci MVC. Další informace o bloku validationové aplikace najdete v následujících tématech:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Přidání ověření do zobrazení vytvořit

Umožňuje s začít přidáním logiky ověření do zobrazení Vytvořit. Naštěstí vzhledem k tomu, že jsme vygenerovali vytvořit zobrazení s Visual Studio, vytvořit zobrazení již obsahuje všechny logiky potřebné uživatelské rozhraní pro zobrazení ověřovacích zpráv. Zobrazení Vytvořit je obsaženo v seznamu 1.

**Výpis 1 - \Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

Všimněte si volání pomocné metody Html.ValidationSummary(), která se zobrazí bezprostředně nad formulářem HTML. Pokud existují chybové zprávy ověření, tato metoda zobrazí ověřovací zprávy v seznamu s odrážkami.

Všimněte si, navíc volání Html.ValidationMessage(), které se zobrazí vedle každého pole formuláře. Pomocník ValidationMessage() zobrazí individuální chybovou zprávu ověření. V případě výpisu 1 se při chybě ověření zobrazí hvězdička.

Nakonec pomocník Html.TextBox() automaticky vykreslí třídu Šablony stylů, pokud dojde k chybě ověření přidružené k vlastnosti zobrazené pomocníkem. Pomocník Html.TextBox() vykreslí třídu s názvem **input-validation-error**.

Když vytvoříte novou ASP.NET aplikaci MVC, automaticky se vytvoří šablona stylů s názvem Site.css ve složce Obsah. Tato šablona stylů obsahuje následující definice pro třídy CSS související s výskytem chybových zpráv ověření:

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

Třída chyba ověření pole se používá ke stylu výstupu vykresleného pomocníkem Html.ValidationMessage(). Vstupní ověřovací chyba třída se používá ke stylu textového pole (vstup) vykresleného pomocníkem Html.TextBox(). Třída validation-summary-errors se používá k stylování neuspořádaného seznamu vykresleného pomocníkem Html.ValidationSummary().

> [!NOTE] 
> 
> Třídy šablon stylů popsané v této části můžete upravit a přizpůsobit tak vzhled chybových zpráv ověření.

## <a name="adding-validation-logic-to-the-create-action"></a>Přidání logiky ověření do akce Vytvořit

Právě teď vytvořit zobrazení nikdy zobrazí chybové zprávy ověření, protože jsme nenapsali logiku generovat žádné zprávy. Chcete-li zobrazit chybové zprávy ověření, je třeba přidat chybové zprávy do ModelState.

> [!NOTE] 
> 
> Metoda UpdateModel() přidá chybové zprávy do Modelu, pokud dojde k chybě přiřazování hodnoty pole formuláře k vlastnosti. Pokud se například pokusíte přiřadit řetězec "apple" vlastnosti BirthDate, která přijímá hodnoty DateTime, pak metoda UpdateModel() přidá chybu do Modelu.

Metoda modified Create() v výpisu 2 obsahuje nový oddíl, který ověřuje vlastnosti Contact třídy před vložením nového kontaktu do databáze.

**Výpis 2 - Řadiče\ContactController.cs (Vytvořit s ověřením)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

Oddíl ověření vynucuje čtyři různá ověřovací pravidla:

- FirstName Vlastnost musí mít délku větší než nula (a nemůže se skládat pouze z mezery)
- Vlastnost LastName musí mít délku větší než nula (a nemůže se skládat pouze z mezer)
- Pokud Phone vlastnost má hodnotu (má délku větší než 0), pak Phone vlastnost musí odpovídat regulární výraz.
- Pokud Email vlastnost má hodnotu (má délku větší než 0), pak Email vlastnost musí odpovídat regulární výraz.

Dojde-li k porušení ověřovacího pravidla, je do modelu ModelState přidána chybová zpráva pomocí metody AddModelError(). Když přidáte zprávu ModelState, zadáte název vlastnosti a text chybové zprávy ověření. Tato chybová zpráva je zobrazena v zobrazení pomocí pomocných metod Html.ValidationSummary() a Html.ValidationMessage().

Po spuštění ověřovacích pravidel je zkontrolována vlastnost IsValid modelstate. IsValid Vlastnost vrátí false, pokud byly přidány všechny chybové zprávy ověření modelstate. Pokud se ověření nezdaří, formulář Vytvořit se znovu zobrazí s chybovými zprávami.

> [!NOTE] 
> 
> Dostal jsem regulární výrazy pro ověření telefonního čísla a e-mailové adresy z regulárního úložiště výrazů na adrese[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>Přidání logiky ověření do akce Úpravy

Akce Úpravy() aktualizuje kontakt. Akce Edit() musí provést přesně stejné ověření jako akce Vytvořit(). Namísto duplikování stejný ověřovací kód, měli bychom refaktorovat řadič kontaktu tak, aby obě Create() a Edit() akce volání stejné metody ověření.

Upravená třída kontrolora kontaktu je obsažena v výpisu 3. Tato třída má novou metodu ValidateContact(), která je volána v rámci obou Create() a Edit() akce.

**Výpis 3 - Řadiče\ContactController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>Souhrn

V této iteraci jsme přidali základní ověření formuláře do naší aplikace Správce kontaktů. Naše ověřovací logika zabraňuje uživatelům v odeslání nového kontaktu nebo úpravě existujícího kontaktu bez zadání hodnot pro vlastnosti FirstName a LastName. Kromě toho musí uživatelé zadat platná telefonní čísla a e-mailové adresy.

V této iteraci jsme přidali logiku ověření do naší aplikace Správce kontaktů nejjednodušším možným způsobem. Smíchání mašit naši logiku ověření do naší logiky řadiče nám však dlouhodobě způsobí problémy. Naše aplikace bude obtížnější udržovat a upravovat v průběhu času.

V další iteraci budeme refaktorovat naši logiku ověřování a logiku přístupu k databázi z našich řadičů. Využijeme několik principů návrhu softwaru, které nám umožní vytvořit volněji vázanou a udržovatelnější aplikaci.

> [!div class="step-by-step"]
> [Předchozí](iteration-2-make-the-application-look-nice-cs.md)
> [další](iteration-4-make-the-application-loosely-coupled-cs.md)
