---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: Přetáhnout myší reorderlist (VB) | Dokumentace Microsoftu
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 72c697bc2a2005d3ff116cf2f73d80e23bb526dd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124924"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="9fd55-103">Přetažení ovládacím prvkem ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="9fd55-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="9fd55-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9fd55-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9fd55-105">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="9fd55-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="9fd55-106">Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="9fd55-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9fd55-107">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="9fd55-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="9fd55-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="9fd55-108">Overview</span></span>

<span data-ttu-id="9fd55-109">`ReorderList` Ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="9fd55-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9fd55-110">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="9fd55-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="9fd55-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="9fd55-111">Steps</span></span>

<span data-ttu-id="9fd55-112">`ReorderList` Ovládací prvek podporuje vazby dat z databáze do seznamu.</span><span class="sxs-lookup"><span data-stu-id="9fd55-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="9fd55-113">Nejlepší na tom také podporuje zápis změn pracovního element seznamu zpět do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="9fd55-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="9fd55-114">Tato ukázka používá jako úložiště dat Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="9fd55-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="9fd55-115">Databáze je součástí instalace sady Visual Studio, včetně express edition volitelné (a free).</span><span class="sxs-lookup"><span data-stu-id="9fd55-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="9fd55-116">Je také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="9fd55-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="9fd55-117">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="9fd55-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="9fd55-118">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="9fd55-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="9fd55-119">Nejjednodušší způsob, jak nastavení databáze je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="9fd55-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="9fd55-120">Připojení k serveru, dvakrát klikněte na `Databases` a vytvořit novou databázi (klikněte pravým tlačítkem a zvolte `New Database`) volá `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="9fd55-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="9fd55-121">V této databázi, vytvořte novou tabulku s názvem `AJAX` s těmito čtyřmi sloupci:</span><span class="sxs-lookup"><span data-stu-id="9fd55-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="9fd55-122">`id` (primární klíč, celé číslo, identitu, not NULL)</span><span class="sxs-lookup"><span data-stu-id="9fd55-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="9fd55-123">`char` (char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="9fd55-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="9fd55-124">`description` (varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="9fd55-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="9fd55-125">`position` (int, NULL).</span><span class="sxs-lookup"><span data-stu-id="9fd55-125">`position` (int, NULL)</span></span>

<span data-ttu-id="9fd55-126">[![Rozložení tabulky AJAX](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9fd55-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="9fd55-127">Rozložení tabulky AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9fd55-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="9fd55-128">V dalším kroku vyplnění tabulky pomocí několika hodnot.</span><span class="sxs-lookup"><span data-stu-id="9fd55-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="9fd55-129">Všimněte si, že `position` sloupec obsahuje pořadí řazení elementů.</span><span class="sxs-lookup"><span data-stu-id="9fd55-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="9fd55-130">[![Počáteční data v tabulce AJAX](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9fd55-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="9fd55-131">Počáteční data v tabulce AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9fd55-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="9fd55-132">Další krok se vyžaduje k vygenerování `SqlDataSource` řízení ke komunikaci s novou databázi a její tabulky.</span><span class="sxs-lookup"><span data-stu-id="9fd55-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="9fd55-133">Zdroj dat musí podporovat `SELECT` a `UPDATE` příkazy jazyka SQL.</span><span class="sxs-lookup"><span data-stu-id="9fd55-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="9fd55-134">Pokud později změníte pořadí prvků seznamu, `ReorderList` ovládací prvek automaticky odešle dvě hodnoty ke zdroji dat `Update` příkaz: novou pozici a ID elementu.</span><span class="sxs-lookup"><span data-stu-id="9fd55-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="9fd55-135">Proto se zdroj dat, musí `<UpdateParameters>` části tyto dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="9fd55-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="9fd55-136">`ReorderList` Ovládací prvek je potřeba nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="9fd55-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="9fd55-137">`AllowReorder`: Určuje, zda může přeskupení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="9fd55-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="9fd55-138">`DataSourceID`: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="9fd55-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="9fd55-139">`DataKeyField`: Název sloupec primárního klíče ve zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="9fd55-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="9fd55-140">`SortOrderField`: Zdrojový sloupec data, která poskytuje pořadí řazení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="9fd55-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="9fd55-141">V `<DragHandleTemplate>` a `<ItemTemplate>` oddíly, rozložení seznamu možné podrobně nastavit.</span><span class="sxs-lookup"><span data-stu-id="9fd55-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="9fd55-142">Datová vazba je také možné pomocí `Eval()` způsob, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="9fd55-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="9fd55-143">Následující šablony stylů CSS stylu informace (odkazované v `<DragHandleTemplate>` část `ReorderList` ovládací prvek) zajišťuje, že když najede myší úchyt pro přetažení změní umístění ukazatele myši odpovídajícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="9fd55-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="9fd55-144">A konečně `ScriptManager` inicializuje ovládací prvek ASP.NET AJAX stránky:</span><span class="sxs-lookup"><span data-stu-id="9fd55-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="9fd55-145">Spuštění tohoto příkladu v prohlížeči a trochu Změna uspořádání položek seznamu.</span><span class="sxs-lookup"><span data-stu-id="9fd55-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="9fd55-146">Potom načtěte tuto stránku a podívejte se na databázi.</span><span class="sxs-lookup"><span data-stu-id="9fd55-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="9fd55-147">Upravený pozice pravděpodobně nebyla zachována a odrážejí hodnoty v `position` sloupec v databázi a že všechno bez jakékoli kódu pouze s použitím značek.</span><span class="sxs-lookup"><span data-stu-id="9fd55-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="9fd55-148">[![Data v databázi se změní podle nového pořadí položek seznamu](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9fd55-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="9fd55-149">Položku dat v databázi se změní podle nového seznamu pořadí ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="9fd55-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9fd55-150">Předchozí</span><span class="sxs-lookup"><span data-stu-id="9fd55-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
