---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Použití nabídky HoverMenu s ovládacím prvkem Repeater (C#) | Dokumentace Microsoftu
author: wenz
description: 'Nabídky HoverMenu ovládacího prvku AJAX Control Toolkit obsahuje efekt jednoduché místní nabídky: Při umístění ukazatele myši nad prvkem, se zobrazí automaticky otevíraného okna na specifi...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f64e90eb2f8f87e2f382cb7897793e7071d305d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59384497"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>Použití nabídky HoverMenu s ovládacím prvkem Repeater (C#)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> Nabídky HoverMenu ovládacího prvku AJAX Control Toolkit obsahuje efekt jednoduché místní nabídky: Při umístění ukazatele myši nad prvkem, zobrazí se na určené pozici automaticky otevíraného okna. Je také možné použít tento ovládací prvek v rámci prvku repeater.


## <a name="overview"></a>Přehled

`HoverMenu` Ovládacího prvku AJAX Control Toolkit obsahuje efekt jednoduché místní nabídky: Při umístění ukazatele myši nad prvkem, zobrazí se na určené pozici automaticky otevíraného okna. Je také možné použít tento ovládací prvek v rámci prvku repeater.

## <a name="steps"></a>Kroky

Za prvé zdroj dat je povinný. Tato ukázka používá databázi AdventureWorks a Microsoft SQL Server 2005 Express Edition. Databáze je volitelná součást instalace sady Visual Studio (včetně express edition) a jsou také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí sad SQL Server 2005 ukázky a Sample Databases (stáhnout na [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit `AdventureWorks.mdf` databázový soubor.

V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení. Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.

K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

Zadejte zdroj dat na stránku. Chcete-li použít omezené množství dat, vybereme pouze prvních pět záznamů v tabulce dodavatele databáze AdventureWorks. Pokud používáte Pomocníka s nastavením Visual Studio k vytvoření zdroje dat, mějte na paměti, že chyby v aktuální verzi předponu názvu tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správná syntaxe:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

V dalším kroku přidejte panel, který slouží jako modální místní nabídky:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

Nyní `HoverMenuExtender` vstupu do play. Tak, aby každý prvek ve zdroji dat získá svůj vlastní místní nabídky, zařízení extender musíte vložit v rámci prvku repeater `<ItemTemplate>` oddílu. Toto je zápis:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

Teď všechny položky ve zdroji dat se zobrazí automaticky otevíraného okna na pravé straně (`PopupPosition` atribut) po prodlevě 50 MS (`PopDelay` atributu).


[![V nabídce při najetí myší se zobrazí vedle každé položky v opakovači](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

V nabídce při najetí myší se zobrazí vedle každé položky v opakovači ([kliknutím ji zobrazíte obrázek v plné velikosti](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](using-hovermenu-with-a-repeater-control-vb.md)
