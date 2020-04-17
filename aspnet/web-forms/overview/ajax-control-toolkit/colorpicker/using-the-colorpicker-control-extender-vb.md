---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: Použití zařízení ColorPicker Control Extender (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: ColorPicker je ASP.NET rozšiřovač AJAX, který poskytuje funkce pro vychystávání barev na straně klienta s ui v ovládacím prvku popup. Může být připojen k libovolnému ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542843"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>Použití zařízení ColorPicker Control Extender (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> ColorPicker je ASP.NET rozšiřovač AJAX, který poskytuje funkce pro vychystávání barev na straně klienta s ui v ovládacím prvku popup. Může být připojen k libovolnému ovládacímu prvku ASP.NET TextBox. To je ono.

Cílem tohoto kurzu je vysvětlit, jak můžete použít ajax ovládací prvek Nástroje ColorPicker rozšiřující prvek. Rozšiřující ovládací prvek ColorPicker zobrazuje vyskakovací dialogové okno, které umožňuje vybrat barvu. ColorPicker je užitečné, kdykoli chcete poskytnout intuitivní uživatelské rozhraní pro uživatele vybrat barvu.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>Rozšíření ovládacího prvku TextBox pomocí rozšiřovače ovládacího prvku ColorPicker

Představte si například, že chcete vytvořit web, který návštěvníkům umožní vytvářet vlastní vizitky. Návštěvníci mohou zadat text vizitky a vybrat barvu. Stránka ASP.NET v výpisu 1 obsahuje dva ovládací prvky TextBox s názvem txtCardText a txtCardColor. Při odeslání formuláře se zobrazí vybrané hodnoty (viz obrázek 1).

[![Jednoduchý formulář pro vytvoření vizitky](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**Obrázek 01**: Jednoduchý formulář pro vytvoření vizitky[(Kliknutím zobrazíte obrázek v plné velikosti)](using-the-colorpicker-control-extender-vb/_static/image2.png)

**Výpis 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

Formulář v výpisu 1 funguje, ale neposkytuje skvělé uživatelské prostředí. Uživatel musí zadat barvu do textového pole. Pokud uživatel chce specializovanou barvu - například ten správný odstín hrášku zelená - pak uživatel musí zjistit html barevný kód bez pomoci.

Pomocí rozšiřujícího ovládacího prvku ColorPicker můžete vytvořit lepší uživatelské prostředí. Ovládací prvek ColorPicker zobrazí dialogové okno barev, když přesunete fokus na ovládací prvek TextBox (viz obrázek 2).

[![Rozšiřovač ovládacího prvku ColorPicker](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**Obrázek 02**: Zařízení Pro rozšíření ovládacího prvku ColorPicker[(Klepnutím zobrazíte obrázek v plné velikosti)](using-the-colorpicker-control-extender-vb/_static/image4.png)

Chcete-li použít rozšiřující ovládací prvek ColorPicker s formulářem v seznamu 1, je třeba provést dva kroky:

1. Přidání ovládacího prvku ScriptManager na stránku
2. Přidání rozšiřovače ovládacího prvku ColorPicker na stránku

Před použitím nástroje ColorPicker je nutné na stránku přidat správce skriptů. Dobré místo pro přidání ScriptManager je přímo pod &lt;&gt; otevřením značky formuláře na straně serveru. Skriptmanager můžete přetáhnout na stránku z panelu nástrojů (ScriptManager je umístěn pod záložkou Rozšíření AJAX). Případně můžete zadat následující značku do zobrazení zdroje pod otevírací značkou formuláře na straně serveru:

&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;

Nejjednodušší způsob, jak přidat rozšiřující ovládací prvek ColorPicker na stránku, je v návrhovém zobrazení. Pokud najedete myší na txtCardColor TextBox, zobrazí se inteligentní možnost úlohy, která vám umožní přidat extender (viz obrázek 3). Pokud vyberete tuto možnost, zobrazí se Průvodce rozkolem (viz obrázek 4).

[![Přidání extenderu](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**Obrázek 03**: Přidání extenderu[(Kliknutím zobrazíte obrázek v plné velikosti)](using-the-colorpicker-control-extender-vb/_static/image6.png)

[![Výběr rozšiřovače ovládacího prvku pomocí Průvodce rozšiřovačem](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**Obrázek 04**: Výběr rozšiřovače ovládacího prvku pomocí Průvodce rozkládací mise[(Klepnutím zobrazíte obrázek v plné velikosti)](using-the-colorpicker-control-extender-vb/_static/image8.png)

Můžete vybrat extender ColorPicker pro rozšíření textového pole txtCardColor pomocí zařízení ColorPicker Extender. Klepnutím na tlačítko OK zavřete dialogové okno.

Po provedeném provádění těchto změn bude zdroj stránky vypadat jako Výpis 2.

**Výpis 2 - CreateCard.aspx (s ColorPicker)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

Všimněte si, že stránka nyní obsahuje ovládací prvek ColorPickerExtender, který se zobrazí přímo pod ovládacím prvkem txtCardColor TextBox. Ovládací prvek ColorPickerExtender rozšiřuje ovládací prvek txtCardColor tak, aby zobrazoval dialogové okno pro výběr barvy.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Spuštění dialogového okna výběru barvy pomocí tlačítka

Zařízení ColorPicker podporuje následující vlastnosti:

- PopupButtonId - ID tlačítka na stránce, která způsobí, že dialogové okno pro výběr barvy se zobrazí.
- PopupPosition - Pozice vzhledem k cílovému ovládacímu prvku dialogového okna výběru barev. Možné hodnoty jsou Absolutní, Nastředit, BottomLeft, BottomRight, Vlevo nahoře, Vpravo nahoře, Vpravo a Vlevo (výchozí hodnota je BottomLeft).
- SampleControlId - ID ovládacího prvku, který zobrazuje vybranou barvu.
- SelectedColor - Počáteční barva vybraná v colorpickeru.

Tyto vlastnosti můžete použít k přizpůsobení způsobu zobrazení dialogového okna pro výběr barvy a zobrazení vybrané barvy. Stránka v seznamu 3 ukazuje, jak můžete použít několik z těchto vlastností.

**Výpis 3 - CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

Stránka v seznamu 3 obsahuje tlačítko Vybrat barvu (viz obrázek 5). Po klepnutí na toto tlačítko se nad textovým polem zobrazí dialogové okno pro výběr barvy. Pokud vyberete barvu z dialogového okna, vybraná barva se zobrazí jako barva pozadí ovládacího prvku lblSample Label.

Vlastnost ColorPicker PopupButtonID se používá k přidružení tlačítka Vybrat barvu k zařízení ColorPicker Extender. Když zadáte hodnotu vlastnosti PopupButtonID, dialogové okno pro výběr barvy se již nezobrazí, když má cílový ovládací prvek fokus. Chcete-li zobrazit dialogové okno, musíte klepnout na tlačítko.

Vlastnost SampleControlID se používá k přidružení ovládacího prvku, který zobrazuje vybranou barvu k ovládacímu prvku ColorPicker. Ovládací prvek ColorPicker změní barvu pozadí tohoto ovládacího prvku na aktuálně vybranou barvu.

[![Zobrazení dialogového okna pro výběr barvy pomocí tlačítka](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**Obrázek 05**: Zobrazení dialogového okna výběru barev pomocí tlačítka[(Klepnutím zobrazíte obrázek v plné velikosti)](using-the-colorpicker-control-extender-vb/_static/image10.png)

## <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili, jak pomocí rozšiřujícího ovládacího prvku ColorPicker zobrazit dialogové okno pro výběr barev. Nejprve jsme zkoumali, jak můžete zobrazit dialogové okno při přesunutí fokusu na ovládací prvek TextBox. Dále jste se naučili, jak vytvořit tlačítko, které zobrazí dialogové okno pro výběr barvy po klepnutí na tlačítko.

> [!div class="step-by-step"]
> [Předchozí](using-the-colorpicker-control-extender-cs.md)
