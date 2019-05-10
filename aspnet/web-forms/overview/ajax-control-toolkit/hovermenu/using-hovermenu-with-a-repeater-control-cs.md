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
ms.openlocfilehash: 01f8d71ef07bd48c16c2e9eb1bb12cd051f7a9e4
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127044"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="f2e6a-103">Použití nabídky HoverMenu s ovládacím prvkem Repeater (C#)</span><span class="sxs-lookup"><span data-stu-id="f2e6a-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="f2e6a-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f2e6a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f2e6a-105">[Stáhněte si kód](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f2e6a-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="f2e6a-106">Nabídky HoverMenu ovládacího prvku AJAX Control Toolkit obsahuje efekt jednoduché místní nabídky: Při umístění ukazatele myši nad prvkem, zobrazí se na určené pozici automaticky otevíraného okna.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f2e6a-107">Je také možné použít tento ovládací prvek v rámci prvku repeater.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="f2e6a-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="f2e6a-108">Overview</span></span>

<span data-ttu-id="f2e6a-109">`HoverMenu` Ovládacího prvku AJAX Control Toolkit obsahuje efekt jednoduché místní nabídky: Při umístění ukazatele myši nad prvkem, zobrazí se na určené pozici automaticky otevíraného okna.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="f2e6a-110">Je také možné použít tento ovládací prvek v rámci prvku repeater.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="f2e6a-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="f2e6a-111">Steps</span></span>

<span data-ttu-id="f2e6a-112">Za prvé zdroj dat je povinný.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-112">First of all, a data source is required.</span></span> <span data-ttu-id="f2e6a-113">Tato ukázka používá databázi AdventureWorks a Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="f2e6a-114">Databáze je volitelná součást instalace sady Visual Studio (včetně express edition) a jsou také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="f2e6a-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f2e6a-115">Databáze AdventureWorks je součástí sad SQL Server 2005 ukázky a Sample Databases (stáhnout na [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="f2e6a-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="f2e6a-116">Nejjednodušší způsob, jak nastavit databázi je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit `AdventureWorks.mdf` databázový soubor.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="f2e6a-117">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f2e6a-118">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f2e6a-119">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):</span><span class="sxs-lookup"><span data-stu-id="f2e6a-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="f2e6a-120">Zadejte zdroj dat na stránku.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-120">Then, add a data source to the page.</span></span> <span data-ttu-id="f2e6a-121">Chcete-li použít omezené množství dat, vybereme pouze prvních pět záznamů v tabulce dodavatele databáze AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="f2e6a-122">Pokud používáte Pomocníka s nastavením Visual Studio k vytvoření zdroje dat, mějte na paměti, že chyby v aktuální verzi předponu názvu tabulky (`Vendor`) s `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="f2e6a-123">Následující kód ukazuje správná syntaxe:</span><span class="sxs-lookup"><span data-stu-id="f2e6a-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="f2e6a-124">V dalším kroku přidejte panel, který slouží jako modální místní nabídky:</span><span class="sxs-lookup"><span data-stu-id="f2e6a-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="f2e6a-125">Nyní `HoverMenuExtender` vstupu do play.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="f2e6a-126">Tak, aby každý prvek ve zdroji dat získá svůj vlastní místní nabídky, zařízení extender musíte vložit v rámci prvku repeater `<ItemTemplate>` oddílu.</span><span class="sxs-lookup"><span data-stu-id="f2e6a-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="f2e6a-127">Toto je zápis:</span><span class="sxs-lookup"><span data-stu-id="f2e6a-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="f2e6a-128">Teď všechny položky ve zdroji dat se zobrazí automaticky otevíraného okna na pravé straně (`PopupPosition` atribut) po prodlevě 50 MS (`PopDelay` atributu).</span><span class="sxs-lookup"><span data-stu-id="f2e6a-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="f2e6a-129">[![V nabídce při najetí myší se zobrazí vedle každé položky v opakovači](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f2e6a-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="f2e6a-130">V nabídce při najetí myší se zobrazí vedle každé položky v opakovači ([kliknutím ji zobrazíte obrázek v plné velikosti](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f2e6a-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f2e6a-131">Next</span><span class="sxs-lookup"><span data-stu-id="f2e6a-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
