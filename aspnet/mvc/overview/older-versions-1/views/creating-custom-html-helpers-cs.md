---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Vytváření vlastních pomocníků HTML (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC. Využitím HTML Pomocník ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542557"
---
# <a name="creating-custom-html-helpers-c"></a>Vytvoření vlastních pomocných rutin HTML (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC. Využitím nápovědy HTML můžete snížit množství únavného psaní značek HTML, které je nutné provést, abyste vytvořili standardní stránku HTML.

Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC. Využitím nápovědy HTML můžete snížit množství únavného psaní značek HTML, které je nutné provést, abyste vytvořili standardní stránku HTML.

V první části tohoto kurzu, jsem popsat některé ze stávajících HTML pomocníků součástí ASP.NET MVC framework. Dále jsem popsat dvě metody vytváření vlastních HTML pomocníků: I vysvětlit, jak vytvořit vlastní HTML pomocníky vytvořením statické metody a vytvořením metody rozšíření.

## <a name="understanding-html-helpers"></a>Principy pomocníků HTML

Pomocník HTML je pouze metoda, která vrací řetězec. Řetězec může představovat libovolný typ obsahu, který chcete. Můžete například použít pomocné soubory HTML k `<input>` vykreslení standardních značek HTML, jako jsou HTML a `<img>` tagy. Pomocí pomocníků HTML můžete také vykreslit složitější obsah, například proužka tabulátoru nebo tabulka HTML s daty databáze.

Rozhraní ASP.NET MVC obsahuje následující sadu standardních pomocníků HTML (nejedná se o úplný seznam):

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropdownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

Zvažte například formulář v seznamu 1. Tento formulář je vykreslen pomocí dvou standardních pomocníků HTML (viz obrázek 1). Tento formulář `Html.BeginForm()` používá `Html.TextBox()` metody a Helper k vykreslení jednoduchého formuláře HTML.

[![Stránka vykreslená pomocí pomocných modulů HTML](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Obrázek 01**: Stránka vykreslená pomocí pomocných zařízení HTML[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-custom-html-helpers-cs/_static/image3.png)

**Výpis 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Metoda Html.BeginForm() Helper se používá k vytvoření `<form>` otevíracích a uzavíracích značek HTML. Všimněte `Html.BeginForm()` si, že metoda je volána v rámci using prohlášení. Příkaz using zajišťuje, `<form>` že značka se zavře na konci bloku using.

Pokud dáváte přednost, namísto vytvoření using block, můžete volat Html.EndForm() Helper metoda zavřít `<form>` značku. Použijte podle toho, jaký přístup `<form>` k vytvoření otevírací a uzavírací značky, která se vám bude jevit jako nejintuitivnější.

Pomocné `Html.TextBox()` metody se používají v výpisu 1 k vykreslení značek HTML. `<input>` Pokud vyberete zdroj zobrazení ve vašem prohlížeči, pak se zobrazí zdroj HTML v výpisu 2. Všimněte si, že zdroj obsahuje standardní značky HTML.

> [!IMPORTANT]
> všimněte `Html.TextBox()`si, že pomocník -HTML je vykreslen pomocí `<%= %>` značek namísto `<% %>` značek. Pokud nezahrnete znaménko rovná se, nic se do prohlížeče nezobrazí.

Rozhraní ASP.NET MVC obsahuje malou sadu pomocníků. S největší pravděpodobností budete muset rozšířit architekturu MVC o vlastní pomocné moduly HTML. Ve zbývající části tohoto kurzu se naučíte dvě metody vytváření vlastních pomocníků HTML.

**Výpis 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Vytváření pomocníků HTML pomocí statických metod

Nejjednodušší způsob, jak vytvořit nový pomocník HTML, je vytvořit statickou metodu, která vrátí řetězec. Představte si například, že se rozhodnete vytvořit nový pomocník `<label>` HTML, který vykreslí značku HTML. Třídu v výpisu 2 můžete `<label>` použít k vykreslení .

**Výpis 2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

Na třídě v seznamu 2 není nic zvláštního. Metoda `Label()` jednoduše vrátí řetězec.

Upravené zobrazení indexu v seznamu `LabelHelper` 3 `<label>` používá k vykreslení značek HTML. Všimněte si, `<%@ imports %>` že zobrazení obsahuje `Application1.Helpers` direktivu, která importuje obor názvů.

**Výpis 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Vytváření pomocníků HTML pomocí rozšiřujících metod

Pokud chcete vytvořit HTML pomocníky, které fungují stejně jako standardní HTML pomocníky obsažené v ASP.NET mvc framework pak je třeba vytvořit metody rozšíření. Rozšiřující metody umožňují přidat nové metody do existující třídy. Při vytváření metody HTML Helper přidáte nové metody do třídy HtmlHelper reprezentované vlastností Html zobrazení.

Třída v listingu 3 přidá `HtmlHelper` metodu `Label()`rozšíření do třídy s názvem . Existuje několik věcí, které byste si měli všimnout o této třídě. Nejprve si všimněte, že třída je statickou třídou. Je nutné definovat metodu rozšíření se statickou třídou.

Za druhé, všimněte si, že první `Label()` parametr `this`metody předchází klíčové slovo . První parametr metody rozšíření označuje třídu, kterou rozšiřuje metoda rozšíření.

**Výpis 3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Po vytvoření metody rozšíření a sestavení aplikace úspěšně, metoda rozšíření se zobrazí v aplikaci Visual Studio Intellisense stejně jako všechny ostatní metody třídy (viz obrázek 2). Jediným rozdílem je, že metody rozšíření se zobrazí se speciálním symbolem vedle nich (ikona šipky dolů).

[![Použití metody rozšíření Html.Label()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Obrázek 02**: Použití metody rozšíření Html.Label()[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-custom-html-helpers-cs/_static/image6.png)

Upravené zobrazení indexu v seznamu 4 používá metodu rozšíření Html.Label() k vykreslení všech jeho `<label>` značek.

**Výpis 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili dvě metody vytváření vlastních pomocníků HTML. Nejprve jste se naučili, jak vytvořit vlastní `Label()` nápovědu HTML vytvořením statické metody, která vrátí řetězec. Dále jste se dozvěděli, `Label()` jak vytvořit vlastní metodu nápovědy HTML vytvořením metody rozšíření ve `HtmlHelper` třídě.

V tomto tutoriálu jsem se zaměřil na budování velmi jednoduché metody HTML Helper. Uvědomte si, že pomocník HTML může být tak složitý, jak chcete. Můžete vytvářet pomocné soubory HTML, které vykreslují bohatý obsah, jako jsou stromová zobrazení, nabídky nebo tabulky databázových dat.

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-views-overview-cs.md)
> [další](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
