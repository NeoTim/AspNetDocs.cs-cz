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
ms.openlocfilehash: 988aa9252cfd93067888734006e6003347f1fb5e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414748"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="9a14b-104">Přetažení ovládacím prvkem ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="9a14b-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="9a14b-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9a14b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9a14b-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9a14b-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="9a14b-107">Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="9a14b-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9a14b-108">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="9a14b-108">The current order of the list shall be persisted on the server.</span></span>


## <a name="overview"></a><span data-ttu-id="9a14b-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="9a14b-109">Overview</span></span>

<span data-ttu-id="9a14b-110">`ReorderList` Ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="9a14b-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="9a14b-111">Aktuální pořadí položek v seznamu se na serveru zachován.</span><span class="sxs-lookup"><span data-stu-id="9a14b-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="9a14b-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="9a14b-112">Steps</span></span>

<span data-ttu-id="9a14b-113">`ReorderList` Ovládací prvek podporuje vazby dat z databáze do seznamu.</span><span class="sxs-lookup"><span data-stu-id="9a14b-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="9a14b-114">Nejlepší na tom také podporuje zápis změn pracovního element seznamu zpět do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="9a14b-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="9a14b-115">Tato ukázka používá jako úložiště dat Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="9a14b-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="9a14b-116">Databáze je součástí instalace sady Visual Studio, včetně express edition volitelné (a free).</span><span class="sxs-lookup"><span data-stu-id="9a14b-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="9a14b-117">Je také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="9a14b-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="9a14b-118">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="9a14b-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="9a14b-119">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="9a14b-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="9a14b-120">Nejjednodušší způsob, jak nastavení databáze je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="9a14b-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="9a14b-121">Připojení k serveru, dvakrát klikněte na `Databases` a vytvořit novou databázi (klikněte pravým tlačítkem a zvolte `New Database`) volá `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="9a14b-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="9a14b-122">V této databázi, vytvořte novou tabulku s názvem `AJAX` s těmito čtyřmi sloupci:</span><span class="sxs-lookup"><span data-stu-id="9a14b-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- `id` <span data-ttu-id="9a14b-123">(primární klíč, celé číslo, identitu, not NULL)</span><span class="sxs-lookup"><span data-stu-id="9a14b-123">(primary key, integer, identity, not NULL)</span></span>
- `char` <span data-ttu-id="9a14b-124">(char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="9a14b-124">(char(1), NULL)</span></span>
- `description` <span data-ttu-id="9a14b-125">(varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="9a14b-125">(varchar(50), NULL)</span></span>
- `position` <span data-ttu-id="9a14b-126">(int, NULL).</span><span class="sxs-lookup"><span data-stu-id="9a14b-126">(int, NULL)</span></span>


[![T<span data-ttu-id="9a14b-127">he rozložení tabulky AJAX]</span><span class="sxs-lookup"><span data-stu-id="9a14b-127">he layout of the AJAX table]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

<span data-ttu-id="9a14b-128">Rozložení tabulky AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9a14b-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>


<span data-ttu-id="9a14b-129">V dalším kroku vyplnění tabulky pomocí několika hodnot.</span><span class="sxs-lookup"><span data-stu-id="9a14b-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="9a14b-130">Všimněte si, že `position` sloupec obsahuje pořadí řazení elementů.</span><span class="sxs-lookup"><span data-stu-id="9a14b-130">Note that the `position` column holds the sort order of the elements.</span></span>


[![T<span data-ttu-id="9a14b-131">he počáteční data v tabulce AJAX]</span><span class="sxs-lookup"><span data-stu-id="9a14b-131">he initial data in the AJAX table]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

<span data-ttu-id="9a14b-132">Počáteční data v tabulce AJAX ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9a14b-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>


<span data-ttu-id="9a14b-133">Další krok se vyžaduje k vygenerování `SqlDataSource` řízení ke komunikaci s novou databázi a její tabulky.</span><span class="sxs-lookup"><span data-stu-id="9a14b-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="9a14b-134">Zdroj dat musí podporovat `SELECT` a `UPDATE` příkazy jazyka SQL.</span><span class="sxs-lookup"><span data-stu-id="9a14b-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="9a14b-135">Pokud později změníte pořadí prvků seznamu, `ReorderList` ovládací prvek automaticky odešle dvě hodnoty ke zdroji dat `Update` příkaz: novou pozici a ID elementu.</span><span class="sxs-lookup"><span data-stu-id="9a14b-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="9a14b-136">Proto se zdroj dat, musí `<UpdateParameters>` části tyto dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="9a14b-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="9a14b-137">`ReorderList` Ovládací prvek je potřeba nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="9a14b-137">The `ReorderList` control needs to set the following attributes:</span></span>

- `AllowReorder`<span data-ttu-id="9a14b-138">: Určuje, zda může přeskupení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="9a14b-138">: Whether the list items may be rearranged</span></span>
- `DataSourceID`<span data-ttu-id="9a14b-139">: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="9a14b-139">: The ID of the data source</span></span>
- `DataKeyField`<span data-ttu-id="9a14b-140">: Název sloupec primárního klíče ve zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="9a14b-140">: The name of the primary key column in the data source</span></span>
- `SortOrderField`<span data-ttu-id="9a14b-141">: Zdrojový sloupec data, která poskytuje pořadí řazení položek seznamu</span><span class="sxs-lookup"><span data-stu-id="9a14b-141">: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="9a14b-142">V `<DragHandleTemplate>` a `<ItemTemplate>` oddíly, rozložení seznamu možné podrobně nastavit.</span><span class="sxs-lookup"><span data-stu-id="9a14b-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="9a14b-143">Datová vazba je také možné pomocí `Eval()` způsob, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="9a14b-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="9a14b-144">Následující šablony stylů CSS stylu informace (odkazované v `<DragHandleTemplate>` část `ReorderList` ovládací prvek) zajišťuje, že když najede myší úchyt pro přetažení změní umístění ukazatele myši odpovídajícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="9a14b-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="9a14b-145">A konečně `ScriptManager` inicializuje ovládací prvek ASP.NET AJAX stránky:</span><span class="sxs-lookup"><span data-stu-id="9a14b-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="9a14b-146">Spuštění tohoto příkladu v prohlížeči a trochu Změna uspořádání položek seznamu.</span><span class="sxs-lookup"><span data-stu-id="9a14b-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="9a14b-147">Potom načtěte tuto stránku a podívejte se na databázi.</span><span class="sxs-lookup"><span data-stu-id="9a14b-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="9a14b-148">Upravený pozice pravděpodobně nebyla zachována a odrážejí hodnoty v `position` sloupec v databázi a že všechno bez jakékoli kódu pouze s použitím značek.</span><span class="sxs-lookup"><span data-stu-id="9a14b-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>


[![T<span data-ttu-id="9a14b-149">má data v databázi se změní podle nového pořadí položek seznamu]</span><span class="sxs-lookup"><span data-stu-id="9a14b-149">he data in the database changes according to the new list item order]</span></span>(drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

<span data-ttu-id="9a14b-150">Položku dat v databázi se změní podle nového seznamu pořadí ([kliknutím ji zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="9a14b-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a14b-151">[Předchozí](using-postbacks-with-reorderlist-cs.md)
> [další](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9a14b-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
