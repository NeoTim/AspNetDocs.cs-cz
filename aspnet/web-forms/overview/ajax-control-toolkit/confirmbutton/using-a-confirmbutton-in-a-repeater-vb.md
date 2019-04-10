---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Použití extenderu ConfirmButton v Repeateru (VB) | Dokumentace Microsoftu
author: wenz
description: Zařízení extender ConfirmButton v sadou nástrojů AJAX Control Toolkit vytvoří Ano/žádnou místní nabídku, když uživatel klikne na tlačítko (včetně prvek LinkButton). Ano pouze tehdy, pokud je...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 4850493e7a16aa9364396d1bbd3fe3e0db0f47db
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59388098"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a><span data-ttu-id="ec901-104">Použití ovládacího prvku ConfirmButton v repeateru (VB)</span><span class="sxs-lookup"><span data-stu-id="ec901-104">Using a ConfirmButton In a Repeater (VB)</span></span>

<span data-ttu-id="ec901-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ec901-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ec901-106">[Stáhněte si kód](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ec901-106">[Download Code](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span></span>

> <span data-ttu-id="ec901-107">Zařízení extender ConfirmButton v sadou nástrojů AJAX Control Toolkit vytvoří Ano/žádnou místní nabídku, když uživatel klikne na tlačítko (včetně prvek LinkButton).</span><span class="sxs-lookup"><span data-stu-id="ec901-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="ec901-108">Pouze Ano po kliknutí na tlačítka akce provádí, jinak zrušena.</span><span class="sxs-lookup"><span data-stu-id="ec901-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="ec901-109">To je možné v repeateru.</span><span class="sxs-lookup"><span data-stu-id="ec901-109">This is also possible in a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="ec901-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="ec901-110">Overview</span></span>

<span data-ttu-id="ec901-111">Zařízení extender ConfirmButton v sadou nástrojů AJAX Control Toolkit vytvoří Ano/žádnou místní nabídku, když uživatel klikne na tlačítko (včetně prvek LinkButton).</span><span class="sxs-lookup"><span data-stu-id="ec901-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="ec901-112">Pouze Ano po kliknutí na tlačítka akce provádí, jinak zrušena.</span><span class="sxs-lookup"><span data-stu-id="ec901-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="ec901-113">To je možné v repeateru.</span><span class="sxs-lookup"><span data-stu-id="ec901-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="ec901-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="ec901-114">Steps</span></span>

<span data-ttu-id="ec901-115">Za prvé zdroj dat je povinný.</span><span class="sxs-lookup"><span data-stu-id="ec901-115">First of all, a data source is required.</span></span> <span data-ttu-id="ec901-116">Tato ukázka používá databázi AdventureWorks a Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="ec901-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="ec901-117">Databáze je volitelná součást instalace sady Visual Studio (včetně express edition) a jsou také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="ec901-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="ec901-118">Databáze AdventureWorks je součástí sad SQL Server 2005 ukázky a Sample Databases (stáhnout na [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="ec901-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="ec901-119">Nejjednodušší způsob, jak nastavit databázi je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit `AdventureWorks.mdf` databázový soubor.</span><span class="sxs-lookup"><span data-stu-id="ec901-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="ec901-120">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="ec901-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="ec901-121">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="ec901-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="ec901-122">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):</span><span class="sxs-lookup"><span data-stu-id="ec901-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

<span data-ttu-id="ec901-123">Potom zdroj dat je povinný.</span><span class="sxs-lookup"><span data-stu-id="ec901-123">Then, a data source is required.</span></span> <span data-ttu-id="ec901-124">Z důvodu zjednodušení jsou načteny pouze prvních pět položky v tabulce dodavatelů AdventureWorks'.</span><span class="sxs-lookup"><span data-stu-id="ec901-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="ec901-125">Všimněte si, že při použití průvodce Visual Studio k vytvoření zdroje dat, název tabulky (`Vendors`) není aktuálně správně s předponou `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="ec901-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="ec901-126">Následující kód je ten správný:</span><span class="sxs-lookup"><span data-stu-id="ec901-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="ec901-127">Tento zdroj dat je pak možné v rámci repeateru.</span><span class="sxs-lookup"><span data-stu-id="ec901-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="ec901-128">Obvyklým způsobem `DataBinder.Eval()` metoda načte data ze zdroje dat.</span><span class="sxs-lookup"><span data-stu-id="ec901-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="ec901-129">`ConfirmButtonExtender` Ovládací prvek musí být umístěn pak v rámci `<ItemTemplate>` části opakovače tak, že se zobrazí pro každou položku ve zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="ec901-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]


[![T<span data-ttu-id="ec901-130">si potvrďte, že se zobrazí tlačítko vedle každé položky ze zdroje dat]</span><span class="sxs-lookup"><span data-stu-id="ec901-130">he confirm button appears next to each entry from the data source]</span></span>(using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

<span data-ttu-id="ec901-131">Tlačítko potvrzení se zobrazí vedle každé položky ze zdroje dat ([kliknutím ji zobrazíte obrázek v plné velikosti](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ec901-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ec901-132">Předchozí</span><span class="sxs-lookup"><span data-stu-id="ec901-132">Previous</span></span>](using-a-confirmbutton-in-a-repeater-cs.md)
