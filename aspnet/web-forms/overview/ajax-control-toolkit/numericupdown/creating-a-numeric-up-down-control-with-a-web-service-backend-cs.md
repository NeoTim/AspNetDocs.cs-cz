---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Vytváří číselnou nahoru/dolů ovládacího prvku pomocí webové služby back-endu (C#) | Dokumentace Microsoftu
author: wenz
description: Místo uživatele zadejte hodnotu do zaškrtávací políčko, by mohly být číselné směrem nahoru nebo dolů ovládací prvek (který existuje ve Windows a jiné operační systémy) jako další c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: afe712dd2b09eda49a4972e8d34fe27760d5b6f6
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115340"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a>Vytvoření ovládacího prvku Numeric Up/Down webovou službou typu back-end (C#)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)

> Místo uživatele zadejte hodnotu do zaškrtávací políčko, by mohly být číselné nahoru/dolů ovládací prvek (který existuje ve Windows a jiné operační systémy) jako další příjemné. Ve výchozím nastavení ovládací prvek NumericUpDown vždy zvýší nebo sníží hodnotu o 1, ale webová služba ukáže větší flexibilitu.

## <a name="overview"></a>Přehled

Místo uživatele zadejte hodnotu do zaškrtávací políčko, by mohly být číselné nahoru/dolů ovládací prvek (který existuje ve Windows a jiné operační systémy) jako další příjemné. Ve výchozím nastavení `NumericUpDown` ovládací prvek vždy zvýší nebo sníží hodnotu o 1, ale webová služba ukáže větší flexibilitu.

## <a name="steps"></a>Kroky

ASP.NET AJAX Control Toolkit obsahuje `NumericUpDown` rozšiřujícího objektu, který do textového pole automaticky přidá dvě tlačítka: Jeden pro zvýšení jeho hodnoty, jeden pro snížení ho. Ovládací prvek ale také podporuje volání webové služby (nebo volání metody stránky). Pokaždé, když směrem nahoru nebo dolů tlačítko dojde ke kliknutí na, JavaScript, kód se připojí k webovému serveru a provede metodu existuje. Podpis metody je následující:

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

`current` Argument je aktuální hodnota v textovém poli; `tag` atribut je další kontext dat, která můžete nastavit jako vlastnost `NumericUpDown` zařízení extender (ale není potřeba).

V tomto příkladu se číselné směrem nahoru nebo dolů ovládací prvek povolit pouze hodnoty, které jsou pro mocniny dvou: 1, 2, 4, 8, 16, 32, 64 a tak dále. Proto musí metoda spouštěny, když uživatel chce zvýšit hodnotu double stará hodnota; jiné metody musíte dělit hodnotu dvou. Tady je úplný webové služby:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

Nakonec vytvořte novou stránku ASP.NET. Obvyklým způsobem, je nutné `ScriptManager` ovládací prvek, `TextBox` ovládacího prvku a `NumericUpDownExtender` ovládacího prvku. K tomu je nutné zadat informace o webových službách:

- `ServiceDownMethod` název v seznamu webovou metodu nebo stránky – metoda
- `ServiceDownPath` Cesta k webové službě s dolů metodu služby; vynechat, pokud používáte metodu stránky
- `ServiceUpMethod` Název nahoru webovou metodu nebo stránky – metoda
- `ServiceUpPath` Cesta k webové službě s aktuálním metodu služby; vynechat, pokud používáte metodu stránky

Tady je kompletní kód pro stránky:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

Při spuštění stránky, Všimněte si, jak se hodnota v textovém poli vždy zdvojnásobí, klikněte na tlačítko nahoře, a je zkrátili na polovinu po kliknutí na tlačítko nižší.

[![Zobrazí jenom čísla, které jsou mocninou čísla 2](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

Zobrazí jenom čísla, které jsou mocninou čísla 2 ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
