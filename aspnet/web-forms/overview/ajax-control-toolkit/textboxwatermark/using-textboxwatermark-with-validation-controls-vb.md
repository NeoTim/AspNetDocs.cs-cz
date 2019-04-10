---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: Použití ovládacího prvku TextBoxWatermark s validačních ovládacích prvků (VB) | Dokumentace Microsoftu
author: wenz
description: Ovládacího prvku TextBoxWatermark v sadou nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli. Když uživatel klikne do pole, to jsem...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: d83fb53ddb40a31013bc724909fa149ce2e4c713
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387365"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>Použití ovládacího prvku TextBoxWatermark s validačními ovládacími prvky (VB)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> Ovládacího prvku TextBoxWatermark v sadou nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli. Když uživatel klikne do pole, je prázdný. Pokud uživatel ponechá pole bez nutnosti zadávat text, zobrazí se předem vyplněných text. To může kolidovat s ASP.NET validačních ovládacích prvků na stejné stránce, ale může tyto problémy překonat.


## <a name="overview"></a>Přehled

`TextBoxWatermark` Ovládacího prvku AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli. Když uživatel klikne do pole, je prázdný. Pokud uživatel ponechá pole bez nutnosti zadávat text, zobrazí se předem vyplněných text. To může kolidovat s ASP.NET validačních ovládacích prvků na stejné stránce, ale může tyto problémy překonat.

## <a name="steps"></a>Kroky

Základní nastavení vzorku je následující: `TextBox` ovládací prvek je horní mezí, použití `TextBoxWatermarkExtender` ovládacího prvku. Tlačítko aktivuje zpětného odeslání a bude možné později použít k aktivaci validačních ovládacích prvků na stránce. Navíc `ScriptManager` ovládací prvek je potřebné k inicializaci technologie ASP.NET AJAX:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

Teď přidejte `RequiredFieldValidator` ovládací prvek, který kontroluje, zda je text v poli při odeslání formuláře. `InitialValue` Validátoru musí být nastavena na stejnou hodnotu, která se používá v `TextBoxWatermarkExtender` ovládacího prvku: Když se odešle formulář, beze změny textové pole hodnotu hodnoty meze v rámci něj:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

Je ale jeden problém s tímto přístupem: Pokud klient zakáže jazyka JavaScript, pole textu není proto předem s vodoznakového textu `RequiredFieldValidator` neaktivuje chybovou zprávu. Proto sekundy `RequiredFieldValidator` ovládací prvek je vyžadován, který vyhledává prázdné textové pole (vynechání `InitialValue` atributu).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

Jelikož obě validátory používat `Display` = `"Dynamic"`, koncovému uživateli nelze rozlišit z vizuálního vzhledu, která dvě validátorů se vyvolala; místo toho to vypadá, došlo jenom jeden z nich.

Nakonec přidejte nějaký kód na straně serveru do výstupního text v poli, pokud nebyl nalezen žádný validátor vydané chybová zpráva:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


[![The program pro ověření, že neexistuje žádný text v poli si bude stěžovat](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

Validátor si bude stěžovat na, že neexistuje žádný text v poli ([kliknutím ji zobrazíte obrázek v plné velikosti](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](using-textboxwatermark-in-a-formview-vb.md)
