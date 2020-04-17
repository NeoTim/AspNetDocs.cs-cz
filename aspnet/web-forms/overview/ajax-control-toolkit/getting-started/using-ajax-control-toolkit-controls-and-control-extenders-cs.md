---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Použití ovládacích prvků a rozšiřujících ovládacích prvků ajax control toolkit (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat ovládací prvky a nástavce AJAX Control Toolkit na ASP.NET stránky.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543714"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Použití ovládacích prvků a rozšiřujících ovládacích prvků AJAX Control Toolkit (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak přidat ovládací prvky a nástavce AJAX Control Toolkit na ASP.NET stránky.

Sada nástrojů AJAX Control Toolkit obsahuje sadu ovládacích prvků a rozšiřujících ovládacích prvků. V tomto stručném kurzu se dozvíte, jak přidat ovládací prvky a rozšiřující ovládací prvky na stránku ASP.NET.

> [!NOTE] 
> 
> Pokyny k instalaci sady nástrojů AJAX Control Toolkit a přidání sady nástrojů AJAX Control Toolkit do sady nástrojů Visual Studio/Visual Web Developer naleznete v kurzu [Začínáme s sadou nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).

## <a name="using-ajax-control-toolkit-controls"></a>Použití ovládacích prvků ajax control toolkit

Ovládací prvek AJAX Control Toolkit funguje stejně jako normální ASP.NET řízení. Ovládací prvek můžete přetáhnout z panelu nástrojů na stránku ASP.NET. Ovládací prvek můžete přidat na stránku v návrhovém zobrazení nebo ve zdrojovém zobrazení.

Existuje jeden zvláštní požadavek při použití ovládacích prvků z AJAX Control Toolkit. Stránka musí obsahovat ovládací prvek ScriptManager. Ovládací prvek ScriptManager je zodpovědný za zahrnutí všech potřebných JavaScriptu požadovaných ovládacími prvky AJAX Control Toolkit.

Například karta AJAX Control Toolkit obsahuje ovládací prvek s názvem Editor ovládacíprvek. Tento ovládací prvek zobrazí rozšířený editor HTML. Chcete-li přidat ovládací prvek Editor na stránku, postupujte takto:

1. Vytvoření nové stránky ASP.NET s názvem ShowEditor.aspx
2. Vyberte ovládací prvek ScriptManager pod kartou Rozšíření AJAX v panelu nástrojů a přetáhněte ovládací prvek na stránku.
3. Vyberte ovládací prvek Editor pod kartou AJAX Control Toolkit v panelu nástrojů a přetáhněte ovládací prvek na stránku (viz obrázek 1). Návrhář by měl vypadat jako obrázek 2.
4. Spusťte web výběrem možnosti nabídky **Ladění, Spustit ladění** nebo stisknutím klávesy F5.
5. Měli byste vidět stránku na obrázku 3.

[![Výběr ovládacího prvku Editor HTML](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Obrázek 01**: Výběr ovládacího prvku Editor[HTML(Kliknutím zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)

[![Návrhář visual studia s scriptmanagerem a ovládacím prvkem Úpravy](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Obrázek 02**: Visual Studio Designer s ScriptManager a upravit ovládací[prvek(Klikněte pro zobrazení obrázku v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)

[![Stránka DisplayEditor.aspx](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Obrázek 03**: Stránka DisplayEditor.aspx([Kliknutím zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)

## <a name="using-ajax-control-toolkit-control-extenders"></a>Použití rozšiřujících zařízení AJAX Control Toolkit Control Extender

Sada nástrojů AJAX Control Toolkit také obsahuje ovládací nástavce. Jak již název napovídá, rozšiřující ovládací prvek rozšiřuje funkce existujícího ovládacího prvku. Například rozšiřující ovládací prvek ConfirmButton rozšiřuje standardní ovládací prvek ASP.NET Button. Extender změní chování ovládacího prvku Button tak, aby se na tlačítko po klepnutí zosakřuje dialogové okno.

Rozšiřující ovládací prvek, stejně jako ovládací prvek AJAX Control Toolkit, vyžaduje ovládací prvek ScriptManager. Před zahájením používání rozšiřujících ovládacích programů ovládacích prvku na stránce je nutné přidat na stránku ovládací prvek ScriptManager.

Chcete-li použít rozšiřovač ovládacího prvku ConfirmButton, postupujte takto:

1. Vytvoření nové ASP.NET stránky s názvem ShowConfirmButton.aspx
2. Přidejte na stránku ovládací prvek ScriptManager přetažením ovládacího prvku na stránku pod záložkou Rozšíření AJAX.
3. Přidejte na stránku standardní ovládací prvek Button přetažením tlačítka pod kartu Standard v panelu nástrojů na povrch návrháře.
4. Klepněte na možnost **Přidat možnost úlohy zařízení Extender** (viz obrázek 4).
5. V dialogovém okně Zvolit zařízení extender vyberte ConfirmButtonExtender (viz obrázek 5) a klepněte na tlačítko OK.
6. Vyberte ovládací prvek Button v návrháři a\_rozbalte uzel Extender, Button1 ConfirmButtonExtender v okně Vlastnosti (viz obrázek 6). Přiřaďte hodnotu *Opravdu?* vlastnosti ConfirmText.
7. Spusťte stránku výběrem možnosti nabídky **Ladění, Spustit ladění** nebo stiskněte klávesu F5.

[![Možnost Přidat úlohu zařízení Extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Obrázek 04**: Možnost Přidat možnost úlohy extenderu([Kliknutím zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)

[![Výběr rozšiřovače ovládacího prvku ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Obrázek 05**: Výběr rozšiřovače ovládacího prvku ConfirmButton(Klepnutím[zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)

[![Nastavení vlastnosti ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Obrázek 06**: Nastavení vlastnosti ConfirmButton[(Klepnutím zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)

Po otevření stránky by se mělo zobrazit tlačítko. Po kliknutí na tlačítko se zobrazí potvrzovací dialog na obrázku 7.

[![Zobrazení potvrzovacího dialogového okna](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Obrázek 07**: Zobrazení potvrzovacího dialogu ([Kliknutím zobrazíte obrázek v plné velikosti)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)

Všimněte si, že obvykle nepřetahujete rozšiřující zařízení ovládacího prvku na stránku. Místo toho použijete možnost **Přidat úlohu zařízení Extender** k přidání rozšiřovače do ovládacího prvku, který jste již přidali na stránku. Všimněte si navíc, že nastavíte vlastnosti rozšiřujícího ovládacího prvku otevřením seznamu vlastností pro rozšíření ovládacího prvku.

Jeden ovládací prvek ASP.NET lze rozšířit o více ovládacích nástavců. Seznam vlastností pro ovládací prvek, který je rozšířen, zobrazí seznam všech rozšiřujících zařízení ovládacího prvku přidružených k ovládacímu prvku.

> [!div class="step-by-step"]
> [Předchozí](get-started-with-the-ajax-control-toolkit-cs.md)
> [další](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
