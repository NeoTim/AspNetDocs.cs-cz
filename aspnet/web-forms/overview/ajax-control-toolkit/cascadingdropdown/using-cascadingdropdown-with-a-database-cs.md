---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: Použití ovládacího prvku CascadingDropDown s databází (C#) | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: ef40d71828237a3d086c7c1bb05de56e0770f588
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391270"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="1cedd-103">Použití ovládacího prvku CascadingDropDown s databází (C#)</span><span class="sxs-lookup"><span data-stu-id="1cedd-103">Using CascadingDropDown with a Database (C#)</span></span>

<span data-ttu-id="1cedd-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1cedd-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1cedd-105">[Stáhněte si kód](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1cedd-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="1cedd-106">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="1cedd-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1cedd-107">V pořadí, aby to fungovalo musí být vytvořeny speciální webové služby.</span><span class="sxs-lookup"><span data-stu-id="1cedd-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="1cedd-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="1cedd-108">Overview</span></span>

<span data-ttu-id="1cedd-109">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="1cedd-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1cedd-110">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) V pořadí, aby to fungovalo musí být vytvořeny speciální webové služby.</span><span class="sxs-lookup"><span data-stu-id="1cedd-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="1cedd-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="1cedd-111">Steps</span></span>

<span data-ttu-id="1cedd-112">Za prvé zdroj dat je povinný.</span><span class="sxs-lookup"><span data-stu-id="1cedd-112">First of all, a data source is required.</span></span> <span data-ttu-id="1cedd-113">Tato ukázka používá databázi AdventureWorks a Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="1cedd-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="1cedd-114">Databáze je volitelná součást instalace sady Visual Studio (včetně express edition) a jsou také dostupné jako samostatný soubor ke stažení v rámci [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="1cedd-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="1cedd-115">Databáze AdventureWorks je součástí sad SQL Server 2005 ukázky a Sample Databases (stáhnout na [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="1cedd-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="1cedd-116">Nejjednodušší způsob, jak nastavit databázi je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit `AdventureWorks.mdf` databázový soubor.</span><span class="sxs-lookup"><span data-stu-id="1cedd-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="1cedd-117">V tomto příkladu předpokládáme, že název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a je umístěn ve stejném počítači jako webový server; to je taky výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="1cedd-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="1cedd-118">Pokud vaše nastavení se liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="1cedd-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="1cedd-119">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci &lt; `form` &gt; element):</span><span class="sxs-lookup"><span data-stu-id="1cedd-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="1cedd-120">V dalším kroku jsou povinné dvou ovládacích prvků DropDownList.</span><span class="sxs-lookup"><span data-stu-id="1cedd-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="1cedd-121">V této ukázce používáme dodavatele a kontaktní údaje z AdventureWorks, proto vytvoříme jeden seznam dostupných dodavatelů a jeden pro dostupných kontaktů:</span><span class="sxs-lookup"><span data-stu-id="1cedd-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="1cedd-122">Pak dvě zařízení Extender CascadingDropDown musí přidat na stránku.</span><span class="sxs-lookup"><span data-stu-id="1cedd-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="1cedd-123">Jeden vyplní seznamu první (dodavatelé) a druhý vyplní druhém seznamu (kontakty).</span><span class="sxs-lookup"><span data-stu-id="1cedd-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="1cedd-124">Musí být nastaveny následující atributy:</span><span class="sxs-lookup"><span data-stu-id="1cedd-124">The following attributes must be set:</span></span>

- `ServicePath`<span data-ttu-id="1cedd-125">: Adresa URL webové služby doručování položky seznamu</span><span class="sxs-lookup"><span data-stu-id="1cedd-125">: URL of a web service delivering the list entries</span></span>
- `ServiceMethod`<span data-ttu-id="1cedd-126">: Metodu webové zajištění položky seznamu</span><span class="sxs-lookup"><span data-stu-id="1cedd-126">: Web method delivering the list entries</span></span>
- `TargetControlID`<span data-ttu-id="1cedd-127">: ID seznamu, rozevíracího seznamu</span><span class="sxs-lookup"><span data-stu-id="1cedd-127">: ID of the dropdown list</span></span>
- `Category`<span data-ttu-id="1cedd-128">: Informace o kategoriích, které je odeslána do webové metody při volání</span><span class="sxs-lookup"><span data-stu-id="1cedd-128">: Category information that is submitted to the web method when called</span></span>
- `PromptText`<span data-ttu-id="1cedd-129">: Text zobrazovaný v případě asynchronní načítání seznamu data ze serveru</span><span class="sxs-lookup"><span data-stu-id="1cedd-129">: Text displayed when asynchronously loading list data from the server</span></span>
- `ParentControlID`<span data-ttu-id="1cedd-130">: (nepovinný) nadřazené rozevírací seznam této aktivační události načítání aktuálního seznamu.</span><span class="sxs-lookup"><span data-stu-id="1cedd-130">: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="1cedd-131">V závislosti na programovací jazyk se používá se změní název příslušné webové služby, ale všechny ostatní hodnoty atributů jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="1cedd-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="1cedd-132">Tady je prvku CascadingDropDown pro první rozevírací seznam:</span><span class="sxs-lookup"><span data-stu-id="1cedd-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="1cedd-133">Ovládací prvek extenderů pro druhý seznam potřeba nastavit `ParentControlID` atribut tak, že vyberete položku v seznamu triggerů dodavatelů načítání přidružených elementů v seznamu kontaktů.</span><span class="sxs-lookup"><span data-stu-id="1cedd-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="1cedd-134">Ve webové službě, která se nastavuje takto se pak provádí samotnou práci.</span><span class="sxs-lookup"><span data-stu-id="1cedd-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="1cedd-135">Všimněte si, `[ScriptService]` atribut se používá, jinak technologie ASP.NET AJAX nelze vytvořit proxy server JavaScript pro přístup k webové metody v kódu skriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="1cedd-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="1cedd-136">Podpis metody webové volány CascadingDropDown vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="1cedd-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="1cedd-137">Takže vrácená hodnota musí být pole typu `CascadingDropDownNameValue` je definován Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="1cedd-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="1cedd-138">`GetVendors()` Metoda je poměrně snadno implementovat: Kód se připojí k databázi AdventureWorks a dotazy prvních 25 dodavatelů.</span><span class="sxs-lookup"><span data-stu-id="1cedd-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="1cedd-139">První parametr v `CascadingDropDownNameValue` konstruktor titulek položky seznamu, je druhý řádek je jeho hodnota (hodnotu atributu v HTML &lt; `option` &gt; element).</span><span class="sxs-lookup"><span data-stu-id="1cedd-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="1cedd-140">Zde je kód:</span><span class="sxs-lookup"><span data-stu-id="1cedd-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="1cedd-141">Získávání přidružené kontakty pro dodavatele (název metody: `GetContactsForVendor()`) je o něco trickier.</span><span class="sxs-lookup"><span data-stu-id="1cedd-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="1cedd-142">Za prvé musí být určena dodavatele, který byl vybrán v prvním rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="1cedd-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="1cedd-143">Control Toolkit definuje pomocnou metodu pro tuto úlohu: `ParseKnownCategoryValuesString()` Metoda vrátí hodnotu `StringDictionary` element s daty rozevíracího seznamu:</span><span class="sxs-lookup"><span data-stu-id="1cedd-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="1cedd-144">Z bezpečnostních důvodů se musí nejdřív ověřit tato data.</span><span class="sxs-lookup"><span data-stu-id="1cedd-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="1cedd-145">Ano, pokud je položka dodavatele (protože `Category` prvního prvku CascadingDropDown je nastavena na `"Vendor"`), ID vybraného dodavatele může načíst:</span><span class="sxs-lookup"><span data-stu-id="1cedd-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="1cedd-146">Zbývající část metody je poměrně přímočaré, potom.</span><span class="sxs-lookup"><span data-stu-id="1cedd-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="1cedd-147">ID dodavatele se používá jako parametr dotazu SQL, který načte všechny přidružené kontakty pro příslušného dodavatele.</span><span class="sxs-lookup"><span data-stu-id="1cedd-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="1cedd-148">Ještě jednou, metoda vrátí pole typu `CascadingDropDownNameValue`.</span><span class="sxs-lookup"><span data-stu-id="1cedd-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="1cedd-149">Načtení stránky technologie ASP.NET a po nějakou dobu seznamu dodavatele vyplněno 25 položky.</span><span class="sxs-lookup"><span data-stu-id="1cedd-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="1cedd-150">Vyberte jednu položku a Všimněte si, jak je druhý rozevírací seznam naplněný daty.</span><span class="sxs-lookup"><span data-stu-id="1cedd-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


[![T<span data-ttu-id="1cedd-151">první seznam he se vyplní automaticky]</span><span class="sxs-lookup"><span data-stu-id="1cedd-151">he first list is filled automatically]</span></span>(using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

<span data-ttu-id="1cedd-152">První seznam se vyplní automaticky ([kliknutím ji zobrazíte obrázek v plné velikosti](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1cedd-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


[![T<span data-ttu-id="1cedd-153">druhý seznam he zaplněný podle výběru v prvním seznamu]</span><span class="sxs-lookup"><span data-stu-id="1cedd-153">he second list is filled according to the selection in the first list]</span></span>(using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

<span data-ttu-id="1cedd-154">Druhý seznam se vyplní podle výběru v prvním seznamu ([kliknutím ji zobrazíte obrázek v plné velikosti](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1cedd-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1cedd-155">[Předchozí](filling-a-list-using-cascadingdropdown-cs.md)
> [další](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1cedd-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
