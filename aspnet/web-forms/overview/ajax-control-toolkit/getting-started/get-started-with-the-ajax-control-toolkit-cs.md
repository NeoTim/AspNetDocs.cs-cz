---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Začínáme s ajax ovládací sady (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Naučte se vše, co potřebujete vědět, abyste mohli začít používat ajax control toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543584"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>Začínáme se sadou nástrojů AJAX Control Toolkit (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> Naučte se vše, co potřebujete vědět, abyste mohli začít používat ajax control toolkit.

Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatných ovládacích prvků, které můžete použít ve svých ASP.NET aplikacích. V tomto kurzu se dozvíte, jak stáhnout sadu nástrojů AJAX Control Toolkit a přidat ovládací prvky sady nástrojů do sady nástrojů Visual Studio/Visual Web Developer Express.

## <a name="downloading-the-ajax-control-toolkit"></a>Stažení sady nástrojů ajax control

[AJAX Control Toolkit](http://devexpress.com/act) je open source projekt vyvinutý členy ASP.NET komunity a ASP.NET týmu. 

[![Stažení sady nástrojů ajax control](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**Obrázek 01**: Stažení AJAX Control Toolkit[(Klikněte pro zobrazení full-size image)](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)

Po stažení souboru je třeba soubor odblokovat. Klikněte pravým tlačítkem myši na soubor, vyberte Vlastnosti a klikněte na tlačítko **Odblokovat** (viz obrázek 2).

[![Odblokování souboru ZIP sady NÁSTROJŮ ovládacího prvku AJAX](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**Obrázek 02**: Odblokování AJAX Control Toolkit ZIP soubor[(Klikněte pro zobrazení full-size image)](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)

Po odblokování souboru můžete rozbalit soubor: Klikněte pravým tlačítkem myši na soubor a vyberte volbu **Rozbalit vše.** Nyní jsme připraveni přidat sadu nástrojů do sady nástrojů Visual Studio/Visual Web Developer.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Přidání sady nástrojů AJAX Control Toolkit do sady nástrojů

Nejjednodušší způsob, jak použít sadu nástrojů AJAX Control Toolkit, je přidat sadu nástrojů do sady nástrojů Visual Studio/Visual Web Developer (viz obrázek 3). Tímto způsobem můžete jednoduše přetáhnout ovládací prvek sady nástrojů na stránku, když jej chcete použít.

[![V sadě nástrojů se zobrazí sada nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**Obrázek 03**: Ajax Control Toolkit se objeví v sadě[nástrojů(Klikněte pro zobrazení obrázku v plné velikosti)](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)

Nejprve je třeba přidat kartu AJAX Control Toolkit do sady nástrojů. Postupujte následovně.

1. Vytvořte nový ASP.NET web výběrem možnosti menu Soubor, Nový web. Poklepáním na soubor Default.aspx v okně Průzkumník řešení otevřete soubor v editoru.
2. Klikněte pravým tlačítkem myši na panel nástrojů pod kartou Obecné a vyberte možnost nabídky **Přidat kartu** (viz obrázek 4).
3. Zadejte novou kartu s názvem AJAX Control Toolkit.

[![Přidání nové karty](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**Obrázek 04**: Přidání nové karty[(Kliknutím zobrazíte obrázek v plné velikosti)](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)

Dále je třeba přidat ovládací prvky AJAX Control Toolkit na novou kartu. Postupujte takto:

- Klepněte pravým tlačítkem myši pod kartu Ajax Control Toolkit a vyberte volbu nabídky **Zvolit položky (viz obrázek 5).**
- Přejděte do umístění, kde jste rozbalili sadu nástrojů AJAX Control Toolkit, a vyberte sestavu AjaxControlToolkit.dll.

[![Výběr položek, které chcete přidat do panelu nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**Obrázek 05**: Vyberte položky, které chcete přidat do panelu nástrojů([Kliknutím zobrazíte obrázek v plné velikosti)](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)

Po dokončení těchto kroků se v sadě nástrojů zobrazí všechny ovládací prvky sady nástrojů.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Upgrade na novou verzi sady nástrojů

Pokud jste používali starší verzi sady Toolkit a nyní potřebujete přejít na novější verzi, postupujte podle následujících kroků:

- Binární soubory – Odstraňte starou verzi sestavení AjaxControlToolkit.dll ze složky Bin webu.
- Položky panelu nástrojů - Odstraňte kartu AJAX Control Toolkit a postupujte podle výše uvedených kroků a znovu vytvořte kartu s novou verzí sestavení AjaxControlToolkit.dll.

> [!div class="step-by-step"]
> [Další](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
