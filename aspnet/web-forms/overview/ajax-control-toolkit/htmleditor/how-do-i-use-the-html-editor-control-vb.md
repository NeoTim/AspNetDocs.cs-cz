---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: Jak se používá ovládací prvek editoru HTML? (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: HTMLEditor je ASP.NET AJAX Control, který vám umožní snadno vytvářet a upravovat html obsah pomocí tlačítek v panelu nástrojů.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542830"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>Jak se používá ovládací prvek editoru HTML? (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> HTMLEditor je ASP.NET AJAX Control, který vám umožní snadno vytvářet a upravovat html obsah pomocí tlačítek v panelu nástrojů.

Cílem tohoto kurzu je poskytnout vám přehled ovládacího prvku EDITOR HTML, který je součástí sady nástrojů AJAX Control Toolkit. Editor HTML obsahuje možnosti pro změnu velikosti písma, výběr písma, změnu barvy pozadí, úpravu barvy popředí, přidávání odkazů, přidávání obrázků, změnu zarovnání textu a provádění operací vyjmutí, kopírování a vkládání (viz obrázek 1).

[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**Obrázek 01:** Editor HTML([Klikněte pro zobrazení obrázku v plné velikosti)](how-do-i-use-the-html-editor-control-vb/_static/image2.png)

Editor HTML umožňuje zadávat obsah pomocí návrhového režimu nebo můžete zadat HTML přímo. Máte také možnost zobrazit náhled obsahu HTML (viz obrázek 2).

[![Tlačítka návrhu, HTML a náhledu](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**Obrázek 02**: Tlačítka Návrh, HTML a[Náhled(Klepnutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-html-editor-control-vb/_static/image4.png)

V tomto kurzu se dozvíte, jak zobrazit editor HTML, jak přizpůsobit tlačítka panelu nástrojů, které se zobrazují v editoru HTML, a jak se vyhnout útokům skriptování mezi webovými servery.

## <a name="displaying-the-html-editor"></a>Zobrazení editoru HTML

Před použitím editoru HTML na stránce ASP.NET musíte nejprve přidat ovládací prvek ScriptManager na stránku. Ovládací prvek ScriptManager je umístěn pod kartou Rozšíření AJAX v panelu nástrojů Visual Studio/Visual Web Developer Express.

Ovládací prvek ScriptManager byste měli umístit do horní části stránky před všechny ostatní ovládací prvky na stránce. Můžete jej například umístit bezprostředně pod otevírací &lt;&gt; značku formuláře na straně serveru.

Ovládací prvek Editor HTML je umístěn v panelu nástrojů se zbytkem ovládacích prvků AJAX Control Toolkit. Je pojmenován ovládací prvek Editor (viz obrázek 3).

[![Ovládací prvek Editor HTML](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**Obrázek 03**: Ovládací prvek Editor[HTML(Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-html-editor-control-vb/_static/image6.png)

Po přetažení editoru HTML na stránku můžete nastavit jeho vlastnosti v seznamu vlastností. Například obvykle chcete nastavit vlastnosti Šířka a Výška. Výpis 1 obsahuje zdroj pro stránku ASP.NET, která obsahuje editor HTML.

**Výpis 1 - SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

Stránka v výpisu 1 obsahuje ovládací prvek editorhtml, ovládací prvek Button a literál ovládací prvek. Po klepnutí na tlačítko se obsah editoru HTML zobrazí v ovládacím prvku Literal (viz obrázek 4).

[![Odeslání formuláře pomocí editoru HTML](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**Obrázek 04**: Odeslání formuláře s editorem[HTML(Kliknutím zobrazíte obrázek v plné velikosti)](how-do-i-use-the-html-editor-control-vb/_static/image8.png)

Vlastnost Obsah editoru HTML se používá k načtení obsahu HTML zadaného do editoru HTML. Uvědomte si, že tento obsah HTML může obsahovat JavaScript. V další části se zabýváme tím, jak můžete zabránit útokům injektáže javascriptu.

## <a name="customizing-the-html-editor-toolbar"></a>Přizpůsobení panelu nástrojů Editor HTML

Můžete přesně přizpůsobit, která tlačítka se zobrazí v editoru. Můžete například odebrat kartu HTML, abyste zabránili uživatelům přepnout editor HTML do režimu HTML. Nebo můžete chtít odebrat rozevírací seznam velikosti písma, abyste zabránili uživatelům ve vytváření příliš velkého textu v příspěvku zprávy na fóru (viz obrázek 5).

[![Přizpůsobený editor HTML](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**Obrázek 05**: Vlastní HTML Editor[(Klikněte pro zobrazení full-size image)](how-do-i-use-the-html-editor-control-vb/_static/image10.png)

Tlačítka panelu nástrojů můžete přizpůsobit odvozením nového editoru HTML ze základní třídy Editor. Například vlastní editor v seznamu 2 obsahuje pouze tlačítka panelu nástrojů pro tučné písmo a kurzívu. Všechna ostatní tlačítka panelu nástrojů byla odebrána. Karta HTML byla navíc odebrána ze spodní části editoru (ale karty Návrh a náhled jsou stále k dispozici).

**Výpis 2\_– Kód aplikace\CustomEditor.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

Třídu v výpisu 2 je\_nutné přidat do složky Kód aplikace, aby se třída zkompilovala automaticky. Pokud složka\_Kód aplikace na vašem webu neexistuje, můžete ji jednoduše přidat.

Po vytvoření vlastního editoru jej můžete přidat na ASP.NET stránku stejným způsobem jako normální editor HTML (viz Výpis 3).

**Výpis 3 - ShowCustomEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Předcházení útokům na skriptování mezi pracemi (XSS)

Kdykoli přijmete vstup od uživatele a znovu zobrazíte tento vstup na vašem webu, můžete potenciálně otevřít svůj web útokům xss (Cross-Site Scripting). Teoreticky by škodlivý hacker mohl odeslat kód JavaScript, který se spustí při opětovném zobrazení vstupu. JavaScript lze použít ke krádeži uživatelských hesel nebo jiných citlivých informací.

Za normálních okolností můžete porazit XSS útoky html kódování bez ohledu na vstup, který načtete od uživatele před zobrazením na webové stránce. Html kódování výstupu editoru HTML by však &lt;nejen&gt; kódovat značky skriptů, ale také kódovat všechny značky HTML. Jinými slovy, ztratíte veškeré formátování, jako je typ písma, velikost písma a barva pozadí.

Pokud shromažďujete citlivé informace od uživatelů, jako jsou hesla, čísla kreditních karet a čísla sociálního pojištění, neměli byste zobrazovat nekódovaný obsah, který načtete od uživatele pomocí editoru HTML. Editor HTML byste měli používat pouze v situacích, kdy obsah HTML znovu nezobrazujete nebo obsah HTML je odeslán na váš web důvěryhodnou stranou.

Představte si například, že vytváříte blogovou aplikaci. V této situaci má smysl používat editor HTML při vytváření blogových příspěvků. Jste jediný, kdo odešle blog post a, pravděpodobně, můžete věřit sami nepředloží škodlivý JavaScript. Nemá však smysl používat editor HTML, když anonymním uživatelům umožňuje zveřejňovat komentáře. Měli byste být obzvláště opatrní v situacích, kdy uživatelé odesílají citlivé informace, jako jsou hesla. Potenciálně, může uživatel se zlými úmysly psát komentář, který obsahuje právo JavaScript pro krádež hesla.

## <a name="summary"></a>Souhrn

V tomto kurzu jste dostali stručný přehled ovládacího prvku editoru HTML, který je součástí sady nástrojů AJAX Control Toolkit. Naučili jste se používat editor HTML k přijímání bohatého obsahu od uživatele a odeslání obsahu na server. Také jsme diskutovali o tom, jak můžete přizpůsobit tlačítka panelu nástrojů, které jsou zobrazeny editorem HTML. Nakonec jste se naučili, jak se vyhnout útokům skriptování mezi webovými servery při použití editoru HTML k přijetí potenciálně škodlivého vstupu.

> [!div class="step-by-step"]
> [Předchozí](how-do-i-use-the-html-editor-control-cs.md)
