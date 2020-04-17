---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: Jak se používá ovládací prvek ComboBox? (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: ComboBox je ASP.NET ajax ovládací prvek, který kombinuje flexibilitu TextBox se seznamem možností, ze kterých si uživatelé mohou vybrat.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543802"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>Jak se používá ovládací prvek ComboBox? (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> ComboBox je ASP.NET ajax ovládací prvek, který kombinuje flexibilitu TextBox se seznamem možností, ze kterých si uživatelé mohou vybrat.

Cílem tohoto kurzu je vysvětlit ovládací prvek AJAX Control Toolkit ComboBox. ComboBox funguje jako kombinace mezi standardní ASP.NET Ovládací prvek DropDownList a Ovládací prvek TextBox. Můžete buď vybrat z již existujícího seznamu položek, nebo zadat novou položku.

ComboBox je podobný rozšíření ovládacího prvku automatického dokončování, ale ovládací prvky se používají v různých scénářích. Zařízení pro automatické dokončování se dotazuje webové služby, aby získalo odpovídající položky. Ovládací prvek ComboBox, naopak, je inicializován se sadou položek. Použití zařízení pro automatické dokončování má smysl, když pracujete s velkou sadou dat (miliony automobilových dílů) při použití ovládacího prvku ComboBox, který má smysl při práci s malou sadou dat (desítky automobilových dílů).

## <a name="selecting-from-a-static-list-of-items"></a>Výběr ze statického seznamu položek

Začněme jednoduchým vzorkem použití ovládacího prvku ComboBox. Představte si, že chcete zobrazit statický seznam položek v rozevíracím seznamu. Chcete však ponechat otevřenou možnost, že seznam není úplný. Chcete povolit uživateli zadat vlastní hodnotu do seznamu.

Vytvoříme novou stránku ASP.NET webových formulářů a na stránce použijeme ovládací prvek ComboBox. Přidejte novou stránku ASP.NET do projektu a přepněte do návrhového zobrazení.

Pokud chcete použít ovládací prvek ComboBox na stránce, musíte na stránku přidat ovládací prvek ScriptManager. Přetáhněte ovládací prvek ScriptManager z dolní části karty Rozšíření AJAX na povrch návrháře. Ovládací prvek ScriptManager byste měli přidat v horní části stránky. můžete jej přidat bezprostředně pod otevírací &lt;&gt; značku formuláře na straně serveru.

Dále přetáhněte ovládací prvek ComboBox na stránku. Ovládací prvek ComboBox najdete v panelu nástrojů s ostatními ovládacími prvky a rozšiřujícími zařízeními nástrojů AJAX Control Toolkit (viz obrázek1).

[![Jednoduchý formulář pro vytvoření vizitky](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**Obrázek 01**: Výběr ovládacího prvku ComboBox z panelu nástrojů[(Klepnutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image2.png)

Použijeme ovládací prvek ComboBox k zobrazení statického seznamu možností. Uživatel si může vybrat určitou úroveň kořeněnosti pro své jídlo ze seznamu tří možností: Mírné, Střední a Horké (viz obrázek 2).

[![Výběr ze statického seznamu položek](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**Obrázek 02**: Výběr ze statického seznamu položek([Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image4.png)

Existují dva způsoby, které můžete přidat tyto možnosti do ovládacího prvku ComboBox. Nejprve vyberete možnost Upravit možnost úlohy při najetí myší na ovládací prvek v návrhovém zobrazení a otevřete Editor položek (viz obrázek 3).

[![Úpravy položek comboboxu](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**Obrázek 03**: Editace ComboBox položky[(Klikněte pro zobrazení full-size image)](how-do-i-use-the-combobox-control-cs/_static/image6.png)

Druhou možností je přidání seznamu položek mezi otevírací &lt;a uzavírací značky asp:ComboBox&gt; ve zdrojovém zobrazení. Stránka v výpisu 1 obsahuje aktualizovaný ComboBox, který má seznam položek.

**Výpis 1 - Static.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

Když otevřete stránku v seznamu 1, můžete vybrat jednu z již existujících možností z comboboxu. Jinými slovy ComboBox funguje stejně jako ovládací prvek DropDownList.

Máte však také možnost zadat novou volbu (například Super Spicy), která není v existujícím seznamu. Takže ComboBox také funguje jako ovládací prvek TextBox.

Bez ohledu na to, zda vyberete již existující položku nebo zadáte vlastní položku, při odeslání formuláře se vaše volba zobrazí v ovládacím prvku popisku. Při odeslání formuláře se spustí\_obslužná rutina btnSubmit Click a aktualizuje popisek (viz obrázek 4).

[![Zobrazení vybrané položky](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**Obrázek 04**: Zobrazení vybrané položky([Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image8.png)

ComboBox podporuje stejné vlastnosti jako ovládací prvek DropDownList pro načítání vybrané položky po odeslání formuláře:

- SelectedItem.Text - Zobrazí hodnotu Vlastnost Text vybrané položky.
- SelectedItem.Value - Zobrazí hodnotu vlastnosti Value vybrané položky nebo zobrazí text zadaný do pole ComboBox.
- SelectedValue - Same as SelectedItem.Value s tím rozdílem, že tato vlastnost umožňuje zadat výchozí (počáteční) vybranou položku.

Pokud zadáte vlastní volbu do ComboBox pak vlastní volba je přiřazena k oběma SelectedItem.Text a SelectedItem.Value vlastnosti.

## <a name="selecting-the-list-of-items-from-the-database"></a>Výběr seznamu položek z databáze

Seznam položek, které comboBox zobrazí, můžete načíst z databáze. Můžete například svázat combobox s ovládacím prvkem SqlDataSource, ovládacím prvkem ObjectDataSource, LinqDataSource nebo EntityDataSource.

Představte si, že chcete zobrazit seznam filmů v ComboBox. Chcete načíst seznam filmů z tabulky databáze Filmy. Postupujte následovně:

1. Vytvoření stránky s názvem Movies.aspx
2. Přidejte na stránku ovládací prvek ScriptManager přetažením správce skriptů z karty Rozšíření AJAX v panelu nástrojů na stránku.
3. Přidejte ovládací prvek ComboBox na stránku přetažením ComboBox na stránku.
4. V návrhovém zobrazení najeďte myší na ovládací prvek ComboBox a vyberte možnost **Zvolit úlohu zdroje dat** (viz obrázek 5). Je spuštěn Průvodce konfigurací zdroje dat.
5. V kroku **Zvolit zdroj dat** &lt;vyberte&gt; možnost Nový zdroj dat.
6. V kroku **Zvolit typ zdroje dat** vyberte Databáze.
7. V kroku **Zvolit datové připojení** vyberte databázi (například MoviesDB.mdf).
8. V kroku **Uložit připojovací řetězec do konfiguračního souboru aplikace** vyberte možnost uložení připojovacího řetězce.
9. V kroku **Konfigurovat příkaz Vybrat vyberte** vyberte databázovou tabulku Filmy a vyberte všechny sloupce.
10. V kroku **Testovací dotaz** klikněte na tlačítko Dokončit.
11. V kroku **Zvolit zdroj dat** vyberte sloupec Název pro pole, které se má zobrazit, a sloupec ID pro datové pole (viz obrázek).
12. Kliknutím na tlačítko OK průvodce zavřete.

[![Výběr zdroje dat](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**Obrázek 05**: Výběr zdroje dat([Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image10.png)

[![Výběr polí textu a hodnoty dat](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**Obrázek 06**: Výběr polí textu a hodnoty dat([Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image12.png)

Po dokončení výše uvedených kroků comboBox je vázán na Ovládací prvek SqlDataSource, který představuje filmy z tabulky databáze Filmy. Zdroj pro stránku vypadá výpis 2 (I vyčistit formátování trochu).

**Výpis 2 - Movies.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

Všimněte si, že ovládací prvek ComboBox má vlastnost DataSourceID, která odkazuje na ovládací prvek SqlDataSource. Když otevřete stránku v prohlížeči, zobrazí se seznam filmů z databáze (viz obrázek 7). Můžete buď vybrat film ze seznamu, nebo zadat nový film zadáním filmu do comboboxu.

[![Zobrazení seznamu filmů](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**Obrázek 07**: Zobrazení seznamu[filmů(Klikněte pro zobrazení obrázku v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image14.png)

## <a name="setting-the-dropdownstyle"></a>Nastavení dropdownstylu

Můžete použít ComboBox DropDownStyle vlastnost změnit chování ComboBox. Tato vlastnost přijímá možné hodnoty:

- DropDown - (výchozí hodnota) ComboBox zobrazí rozevírací seznam, když kliknete na šipku a můžete zadat vlastní hodnotu.
- Jednoduché - ComboBox zobrazí rozbalovací seznam automaticky a můžete zadat vlastní hodnotu.
- DropDownList - ComboBox funguje stejně jako ovládací prvek DropDownList.

Rozdíl mezi dropdown a simple je při zobrazení seznamu položek. V případě Simple, seznam se zobrazí okamžitě při přesunutí fokusu na ComboBox. V případě rozevíracího seznamu musíte klepnutím na šipku zobrazit seznam položek.

DropDownList Hodnota způsobí, že ovládací prvek ComboBox pracovat stejně jako standardní ovládací prvek DropDownList. Je zde však důležitý rozdíl. Starší verze aplikace Internet Explorer zobrazují ovládací prvek DropDownList s nekonečným z-indexem, takže se ovládací prvek zobrazí před libovolným ovládacím prvkem umístěným před ním. Vzhledem k tomu, že &lt;&gt; ComboBox vykreslí značku HTML div namísto značky výběru &lt;&gt; HTML, comboBox správně respektuje z-ordering.

## <a name="setting-the-autocompletemode"></a>Nastavení režimu automatického dokončování

Pomocí vlastnosti ComboBox AutoCompleteMode můžete určit, co se stane, když někdo zadá text do comboboxu. Tato vlastnost přijímá následující možné hodnoty:

- Žádné - (výchozí hodnota) ComboBox neposkytuje žádné chování automatického dokončování.
- Navrhnout - ComboBox zobrazí seznam a zvýrazní odpovídající položku v seznamu (viz obrázek 8).
- Připojit - ComboBox nezobrazí seznam a připojí odpovídající položku ze seznamu na to, co jste zadali (viz obrázek 9).
- SuggestAppend - ComboBox zobrazí seznam a připojí odpovídající položku ze seznamu na to, co jste zadali (viz obrázek 10).

[![ComboBox je návrh](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**Obrázek 08**: ComboBox dělá[návrh(Klikněte pro zobrazení full-size image)](how-do-i-use-the-combobox-control-cs/_static/image16.png)

[![ComboBox připojí odpovídající text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**Obrázek 09**: ComboBox připojí odpovídající[text(Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-combobox-control-cs/_static/image18.png)

[![ComboBox navrhuje a připojí](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**Obrázek 10**: ComboBox navrhuje a připojí[(Klikněte pro zobrazení full-size image)](how-do-i-use-the-combobox-control-cs/_static/image20.png)

## <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili, jak pomocí ovládacího prvku ComboBox zobrazit pevnou sadu položek. Je provázán ovládací prvek ComboBox statickou sadou položek i databázovou tabulkou. Nakonec jste se dozvěděli, jak změnit chování ComboBox nastavením jeho DropDownStyle a AutoCompleteMode vlastnosti.

> [!div class="step-by-step"]
> [Další](how-do-i-use-the-combobox-control-vb.md)
