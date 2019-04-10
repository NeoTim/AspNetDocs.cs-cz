---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Animace závislá na podmínce (C#) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Určuje, zda je animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: c05f0976a135615f7a272b8057eb4c56677e5117
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412421"
---
# <a name="animation-depending-on-a-condition-c"></a>Animace závislá na podmínce (C#)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Určuje, zda je animaci spustit nebo ne může také záviset na podmínky v podobě kódu jazyka JavaScript.


## <a name="overview"></a>Přehled

Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Určuje, zda je animaci spustit nebo ne může také záviset na podmínky v podobě kódu jazyka JavaScript.

## <a name="steps"></a>Kroky

Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

Animace se použijí pro panel text, který vypadá takto:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

V přidružené třídy šablony stylů CSS pro panel definovat barvu pozadí nice a také nastavit Pevná šířka panelu:

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

V rámci `<Animations>` uzlu, použijte `<OnLoad>` ke spuštění animací, jakmile úplným načtením stránky. Místo jednoho regulární animací `<Condition>` element vstupu do play. Kód jazyka JavaScript ve formě hodnoty `ConditionScript` atribut je proveden za běhu. Pokud je vyhodnocen jako true, animace provádí, v opačném případě ne. Následující kód obsahuje dvě animace, každý z nich prováděný 50 % případů na náhodné. Protože může existovat jenom jeden animace v rámci `<OnLoad>`, dva `<Condition>` animace se propojují s použitím `<Sequence>` element:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

Všimněte si, že menší než znaménko (`<`) v `ConditionScript` atribut musí být uvozený uvozovacím znakem (). Při spuštění tohoto skriptu, buď žádná spuštění animace, nebo jeden z nich nemá, nebo obě.


[![The panel je mizení bez změny velikosti, takže druhého spuštění animace, první z nich nebyl](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

Je panelu mizení bez změny velikosti, takže druhého spuštění animace, první z nich nebyl ([kliknutím ji zobrazíte obrázek v plné velikosti](animation-depending-on-a-condition-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](executing-several-animations-after-each-other-cs.md)
> [další](picking-one-animation-out-of-a-list-cs.md)
