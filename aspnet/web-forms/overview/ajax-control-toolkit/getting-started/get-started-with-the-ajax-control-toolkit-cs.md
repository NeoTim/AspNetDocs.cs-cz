---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Začínáme s AJAX Control Toolkit (C#) | Dokumentace Microsoftu
author: microsoft
description: Přečtěte si všechno, co potřebujete vědět, abyste mohli začít používat sadou nástrojů AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bbbe0c8240a2a77edee8d39a76bf865c95f345e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381091"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>Začínáme se sadou nástrojů AJAX Control Toolkit (C#)

by [Microsoft](https://github.com/microsoft)

> Přečtěte si všechno, co potřebujete vědět, abyste mohli začít používat sadou nástrojů AJAX Control Toolkit.


Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatné ovládací prvky, které můžete použít ve svých aplikacích technologie ASP.NET. V tomto kurzu se dozvíte, jak stáhnout sadou nástrojů AJAX Control Toolkit a přidání ovládacích prvků nástrojů do vašich nástrojů Visual Studio nebo Visual Web Developer Express.

## <a name="downloading-the-ajax-control-toolkit"></a>Stahuje se sadou nástrojů AJAX Control Toolkit

[Sadou nástrojů AJAX Control Toolkit](http://devexpress.com/act) projekt open source vyvinutý členy komunity technologie ASP.NET a tým ASP.NET. 


[![DSada nástrojů AJAX Control Toolkit ownloading](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**Obrázek 01**: Stahuje se sadou nástrojů AJAX Control Toolkit ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))


Po stažení souboru, budete muset odblokovat soubor. Klikněte pravým tlačítkem na soubor, vyberte vlastnosti a klikněte na tlačítko **Odblokovat** tlačítko (viz obrázek 2).


[![Usoubor ZIP Toolkit ovládacího prvku AJAX nblocking](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**Obrázek 02**: Odblokování souboru ZIP se sada nástrojů AJAX ovládacího prvku ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))


Po odblokování ho mohli rozbalit soubor: Klikněte pravým tlačítkem na soubor a vyberte **Extrahovat vše** nabídky. Nyní jsme připraveni přidat sadu nástrojů do panelu nástrojů Visual Studio nebo Visual Web Developer.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Přidávání do panelu nástrojů AJAX Control Toolkit

Přidat sadu nástrojů do vašich nástrojů Visual Studio nebo Visual Web Developer je nejjednodušší způsob, jak používat sadou nástrojů AJAX Control Toolkit (viz obrázek 3). Tímto způsobem můžete jednoduše přetáhnout toolkit ovládacího prvku do stránky Pokud chcete použít.


[![AJAX Control Toolkit se zobrazí v panelu nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**Obrázek 03**: V panelu nástrojů zobrazí se sadou nástrojů AJAX Control Toolkit ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))


Nejprve budete muset přidat kartu sadou nástrojů AJAX Control Toolkit do panelu nástrojů. Postupujte podle těchto kroků.

1. Vytvoření nového webu ASP.NET tak, že vyberete možnost nabídky soubor, nový web. Klikněte dvakrát na Default.aspx v okně Průzkumník řešení otevřete soubor v editoru.
2. Panel pod na kartě Obecné klikněte pravým tlačítkem a vyberte možnost nabídky **přidat kartu** (viz obrázek 4).
3. Zadejte novou kartu s názvem sadou nástrojů AJAX Control Toolkit.


[![Ana nové kartě dding](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**Obrázek 04**: Přidání nové karty ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))


Dále je třeba k přidávání ovládacích prvků AJAX Control Toolkit na nové kartě. Postupujte podle těchto kroků:

- Klikněte pravým tlačítkem na pod kartě sadou nástrojů AJAX Control Toolkit a vyberte možnost nabídky **zvolit položky (viz obrázek 5)**.
- Přejděte do umístění, kde rozzipoval. Sada nástrojů AJAX Control Toolkit a vyberte AjaxControlToolkit.dll sestavení.


[![CZvolte položky, které chcete přidat do panelu nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**Obrázek 05**: Zvolte položky, které chcete přidat do panelu nástrojů ([kliknutím ji zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))


Po dokončení těchto kroků všechny ovládací prvky nástrojů se zobrazí ve vašich dovedností.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Upgrade na novou verzi sady nástrojů

Pokud byly pomocí starší verze sady nástrojů a teď potřebujete přesunout do novější verze jsou doporučené kroky:

- Binární soubory – odstranit starou verzi AjaxControlToolkit.dll sestavení ze složky koše vašeho webu.
- Položky panelu nástrojů – odstranit kartu sadou nástrojů AJAX Control Toolkit a postupujte podle výše uvedené kroky a znovu vytvořit na kartu s novou verzi AjaxControlToolkit.dll sestavení.

> [!div class="step-by-step"]
> [Next](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
