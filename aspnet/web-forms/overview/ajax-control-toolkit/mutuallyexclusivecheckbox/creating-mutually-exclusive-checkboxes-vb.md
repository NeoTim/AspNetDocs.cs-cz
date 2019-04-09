---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Vytvoření vzájemně se vylučujících zaškrtávacích políček (VB) | Dokumentace Microsoftu
author: wenz
description: 'Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají. Existuje navracení, i když: Jednou jednu skupinu je přepínač vybrán...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 45ea3c3dbcf7816f67081a61230c4b055a90fcf5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393623"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>Vytvoření vzájemně se vylučujících zaškrtávacích políček (VB)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají. Existuje navracení, i když: Po výběru jedné přepínací tlačítka ve skupině není možné zrušit zaškrtnutí všech přepínačů. Zaškrtávací políčka v každém okamžiku může nezaškrtnuté, ale nejsou vzájemně vylučují. Tento kurz nabízí to nejlepší z obou přístupů: zaškrtávací políčka, které se vzájemně vylučují.


## <a name="overview"></a>Přehled

Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají. Existuje navracení, i když: Po výběru jedné přepínací tlačítka ve skupině není možné zrušit zaškrtnutí všech přepínačů. Zaškrtávací políčka v každém okamžiku může nezaškrtnuté, ale nejsou vzájemně vylučují. Tento kurz nabízí to nejlepší z obou přístupů: zaškrtávací políčka, které se vzájemně vylučují.

## <a name="steps"></a>Kroky

ASP.NET AJAX Control Toolkit obsahuje MutuallyExclusiveCheckBox zařízení extender. To umožňuje programátorům přiřadit libovolný zaškrtávací políčko na název skupiny (`Key` atributu). Ze všech políček v rámci stejné skupiny může najednou vybrat pouze jeden.

Začněme se umísťování dvě zaškrtávací políčka na novou stránku ASP.NET. Může existovat více, ale dva z nich stačí k předvedení se zásadou:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

U obou políček MutuallyExclusiveCheckBoxExtender ovládací prvek je třeba umístit na stránce. Oba atributy klíč musí mít stejnou hodnotu, stejně jako hodnota, kterou atributy prvků HTML tlačítko přepínače musí být stejný jako označují skupiny, do kterých patří. Vlastnost TargetControlID rozšiřujícího objektu, který odkazuje na Identifikátor zaškrtávacího políčka.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

A konečně, zahrnují technologie ASP.NET AJAX `ScriptManager` kterou všechny prvky technologie ASP.NET AJAX Control Toolkit vyžaduje:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

Uložte a spusťte: Můžete zkontrolovat a zrušit zaškrtnutí obou políček, ale současně může obě políčka kontrolovat.


[![Onajednou lze zkontrolovat jen pro jeden checkbox](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

Pouze jeden checkbox můžete zkontrolovat v čase ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](creating-mutually-exclusive-checkboxes-cs.md)
