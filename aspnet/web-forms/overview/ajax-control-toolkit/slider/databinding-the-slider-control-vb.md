---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Vazba ovládacího prvku posuvník (VB) | Microsoft Docs
author: wenz
description: Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit vazby aktuální Positio...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627216"
---
# <a name="databinding-the-slider-control-vb"></a>Svázání posuvníku s daty (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit navázání aktuální pozice posuvníku na jiný ovládací prvek ASP.NET.

## <a name="overview"></a>Přehled

Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit navázání aktuální pozice posuvníku na jiný ovládací prvek ASP.NET.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

Dále do stránky přidejte dva ovládací prvky `TextBox`. Jedna z nich se transformuje na grafický posuvník a druhá bude mít polohu posuvníku.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

Dalším krokem je již poslední krok. Ovládací prvek `SliderExtender` z ASP.NET AJAX Control Toolkit vytvoří posuvník od prvního textového pole a při změně pozice posuvníku automaticky aktualizuje druhé textové pole. Aby to fungovalo, musí být atribut `SliderExtender``TargetControlID` nastaven na ID prvního textového pole; atribut `BoundControlID` musí být nastaven na ID druhého textového pole.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

Jak vidíte v prohlížeči, datová vazba funguje v obou směrech: zadání nové hodnoty do textového pole aktualizuje polohu posuvníku. Pokud nastavíte druhé textové pole jen pro čtení, můžete do textového pole přidat slabou ochranu, aby byl uživatel těžší ručně aktualizovat hodnotu v této části.

[![posuvník a textové pole jsou synchronizované](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

Posuvník a textové pole jsou synchronizované ([kliknutím zobrazíte obrázek v plné velikosti).](databinding-the-slider-control-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-the-slider-control-with-auto-postback-vb.md)
