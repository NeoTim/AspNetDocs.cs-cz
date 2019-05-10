---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: Přetáhnout myší reorderlist (C#) | Dokumentace Microsoftu
author: wenz
description: Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení. Aktuální pořadí položek v seznamu se...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8adeceba0d43d6baf1af944a910750ca0682b097
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124935"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="8d055-104">Přetažení ovládacím prvkem ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="8d055-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="8d055-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8d055-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8d055-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8d055-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="8d055-107">Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="8d055-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8d055-108">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="8d055-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="8d055-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="8d055-109">Overview</span></span>

<span data-ttu-id="8d055-110">`ReorderList` Ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="8d055-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8d055-111">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="8d055-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="8d055-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="8d055-112">Steps</span></span>

<span data-ttu-id="8d055-113">`ReorderList` Ovládací prvek podporuje vazby dat z databáze do seznamu.</span><span class="sxs-lookup"><span data-stu-id="8d055-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="8d055-114">Nejlepší na tom také podporuje zápis změn pracovního element seznamu zpět do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="8d055-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="8d055-115">Tato ukázka používá jako úložiště dat Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="8d055-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="8d055-116">Databáze je součástí instalace sady Visual Studio, včetně express edition volitelné (a free).</span><span class="sxs-lookup"><span data-stu-id="8d055-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="8d055-117">Je také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="8d055-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="8d055-118">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="8d055-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="8d055-119">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="8d055-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="8d055-120">Nejjednodušší způsob, jak nastavení databáze je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="8d055-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="8d055-121">Připojení k serveru, dvakrát klikněte na `Databases` a vytvořit novou databázi (klikněte pravým tlačítkem a zvolte `New Database`) volá `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="8d055-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="8d055-122">V této databázi, vytvořte novou tabulku s názvem `AJAX` s těmito čtyřmi sloupci:</span><span class="sxs-lookup"><span data-stu-id="8d055-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="8d055-123">`id` (primární klíč, celé číslo, identitu, not NULL)</span><span class="sxs-lookup"><span data-stu-id="8d055-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="8d055-124">`char` (char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="8d055-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="8d055-125">`description` (varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="8d055-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="8d055-126">`position` (int, NULL).</span><span class="sxs-lookup"><span data-stu-id="8d055-126">`position` (int, NULL)</span></span>

<span data-ttu-id="8d055-127">[![Rozložení tabulky AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8d055-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="8d055-128">Rozložení tabulky AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8d055-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="8d055-129">V dalším kroku vyplnění tabulky pomocí několika hodnot.</span><span class="sxs-lookup"><span data-stu-id="8d055-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="8d055-130">Všimněte si, že `position` sloupec obsahuje pořadí řazení elementů.</span><span class="sxs-lookup"><span data-stu-id="8d055-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="8d055-131">[![Počáteční data v tabulce AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8d055-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="8d055-132">Počáteční data v tabulce AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8d055-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="8d055-133">Další krok se vyžaduje k vygenerování `SqlDataSource` řízení ke komunikaci s novou databázi a její tabulky.</span><span class="sxs-lookup"><span data-stu-id="8d055-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="8d055-134">Zdroj dat musí podporovat `SELECT` a `UPDATE` příkazy jazyka SQL.</span><span class="sxs-lookup"><span data-stu-id="8d055-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="8d055-135">Pokud později změníte pořadí prvků seznamu, `ReorderList` ovládací prvek automaticky odešle dvě hodnoty ke zdroji dat `Update` příkaz: novou pozici a ID elementu.</span><span class="sxs-lookup"><span data-stu-id="8d055-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="8d055-136">Proto se zdroj dat, musí `<UpdateParameters>` části tyto dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="8d055-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="8d055-137">`ReorderList` Ovládací prvek je potřeba nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="8d055-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="8d055-138">`AllowReorder`: Určuje, zda může přeskupení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="8d055-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="8d055-139">`DataSourceID`: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="8d055-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="8d055-140">`DataKeyField`: Název sloupec primárního klíče ve zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="8d055-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="8d055-141">`SortOrderField`: Zdrojový sloupec data, která poskytuje pořadí řazení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="8d055-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="8d055-142">V `<DragHandleTemplate>` a `<ItemTemplate>` oddíly, rozložení seznamu možné podrobně nastavit.</span><span class="sxs-lookup"><span data-stu-id="8d055-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="8d055-143">Datová vazba je také možné pomocí `Eval()` způsob, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="8d055-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="8d055-144">Následující šablony stylů CSS stylu informace (odkazované v `<DragHandleTemplate>` část `ReorderList` ovládací prvek) zajišťuje, že když najede myší úchyt pro přetažení změní umístění ukazatele myši odpovídajícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="8d055-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="8d055-145">A konečně `ScriptManager` inicializuje ovládací prvek ASP.NET AJAX stránky:</span><span class="sxs-lookup"><span data-stu-id="8d055-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="8d055-146">Spuštění tohoto příkladu v prohlížeči a trochu Změna uspořádání položek seznamu.</span><span class="sxs-lookup"><span data-stu-id="8d055-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="8d055-147">Potom načtěte tuto stránku a podívejte se na databázi.</span><span class="sxs-lookup"><span data-stu-id="8d055-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="8d055-148">Upravený pozice pravděpodobně nebyla zachována a odrážejí hodnoty v `position` sloupec v databázi a že všechno bez jakékoli kódu pouze s použitím značek.</span><span class="sxs-lookup"><span data-stu-id="8d055-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="8d055-149">[![Data v databázi se změní podle nového pořadí položek seznamu](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8d055-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="8d055-150">Položku dat v databázi se změní podle nového seznamu pořadí ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="8d055-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d055-151">[Předchozí](using-postbacks-with-reorderlist-cs.md)
> [další](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8d055-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
