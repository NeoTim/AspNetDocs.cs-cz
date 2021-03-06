---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Provádění několika animací po sobě (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit sever...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614280"
---
# <a name="executing-several-animations-after-each-other-c"></a>Postupné provedení několika animací (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit několik animací za sebou.

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit několik animací za sebou.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Obecně `<OnLoad>` akceptuje pouze jednu animaci. Rozhraní animace umožňuje připojit několik animací k jednomu pomocí elementu `<Sequence>`. Všechny animace v rámci `<Sequence>` jsou spouštěny jednou po druhém. Zde je možné označení pro ovládací prvek `AnimationExtender`, nejprve panel Rozšiřte a poté zmenšete jeho výšku:

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

Když spustíte tento skript, panel se nejprve rozšíří a pak zmenší.

[![první šířka se zvyšuje.](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)

Nejprve se zvětší Šířka ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-cs/_static/image3.png)

[![pak se výška zmenší.](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)

Pak se výška zmenší ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-cs/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](executing-several-animations-at-the-same-time-cs.md)
> [Další](animation-depending-on-a-condition-cs.md)
