---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: Povolení pouze určitých znaků v textovém poli (VB) | Microsoft Docs
author: wenz
description: Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky. To ale pořád nezabrání uživatelům v zadávání neplatných...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613510"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>Povolení určitých znaků v textovém poli (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky. Přesto však nebrání uživatelům v zadávání neplatných znaků a pokusu o odeslání formuláře.

## <a name="overview"></a>Přehled

Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky. Přesto však nebrání uživatelům v zadávání neplatných znaků a pokusu o odeslání formuláře.

## <a name="steps"></a>Kroky

ASP.NET AJAX Control Toolkit obsahuje ovládací prvek `FilteredTextBox`, který rozšiřuje textové pole. Po aktivaci lze do pole zadat pouze určitou sadu znaků.

Aby to fungovalo, musíme nejdřív potřebovat běžný ASP.NET AJAX `ScriptManager`, který načte knihovny JavaScriptu, které jsou také používány ASP.NET AJAX Control Toolkit:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

Pak budeme potřebovat textové pole:

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

Nakonec se `FilteredTextBoxExtender` ovládací prvek postará o omezení znaků, které může uživatel zadat. Nejprve nastavte atribut `TargetControlID` na `ID` ovládacího prvku `TextBox`. Pak zvolte jednu z dostupných hodnot `FilterType`:

- `Custom` výchozí nastavení; je nutné zadat seznam platných znaků.
- jenom `LowercaseLetters` jenom malá písmena
- jenom `Numbers` číslice
- `UppercaseLetters` pouze velká písmena

Pokud se používá `Custom FilterType`, musí být nastavena vlastnost `ValidChars` a obsahovat seznam znaků, které mohou být zadány. Způsobem: Pokud se pokusíte vložit text do textového pole, odeberou se všechny neplatné znaky.

Zde je značka pro ovládací prvek `FilteredTextBoxExtender`, který povoluje pouze číslice (něco, co by bylo také možné s `FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

Spusťte stránku a pokuste se zadat písmeno, pokud je jazyk JavaScript povolený, nebude fungovat. číslice se ale zobrazí na stránce. Upozorňujeme však, že `FilteredTextBox` ochrany nejsou v odrážce. Pokud je JavaScript povolený, můžou být do textového pole vložená nějaká data, takže musíte použít další ověřování, tj. ASP. Ovládací prvky ověřování netto.

[![zadat lze pouze číslice.](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

Zadat lze pouze číslice ([kliknutím zobrazíte obrázek v plné velikosti).](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](allowing-only-certain-characters-in-a-text-box-cs.md)
