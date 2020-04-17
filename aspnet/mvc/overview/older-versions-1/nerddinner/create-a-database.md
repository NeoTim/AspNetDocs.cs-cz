---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Vytvoření databáze | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 2 ukazuje kroky k vytvoření databáze, která obsahuje všechna data večeře a RSVP pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541608"
---
# <a name="create-a-database"></a><span data-ttu-id="3e77b-103">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="3e77b-103">Create a Database</span></span>

<span data-ttu-id="3e77b-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3e77b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3e77b-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="3e77b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="3e77b-106">Toto je krok 2 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="3e77b-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="3e77b-107">Krok 2 ukazuje kroky k vytvoření databáze, která obsahuje všechna data večeře a RSVP pro naši aplikaci NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="3e77b-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="3e77b-108">Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="3e77b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="3e77b-109">NerdDinner Krok 2: Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="3e77b-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="3e77b-110">Budeme používat databázi pro uložení všech večeři a RSVP data pro naši aplikaci NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="3e77b-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="3e77b-111">Následující kroky ukazují vytvoření databáze pomocí bezplatné edice SQL Server Express (kterou můžete snadno nainstalovat pomocí V2 [Instalační služby webové platformy společnosti Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="3e77b-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="3e77b-112">Veškerý kód, který napíšeme, funguje jak s SQL Server Express, tak s úplným SQL Serverem.</span><span class="sxs-lookup"><span data-stu-id="3e77b-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="3e77b-113">Vytvoření nové databáze SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="3e77b-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="3e77b-114">Začneme kliknutím pravým tlačítkem myši na náš webový projekt a pak vybereme příkaz Nabídky **Přidat&gt;novou položku:**</span><span class="sxs-lookup"><span data-stu-id="3e77b-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="3e77b-115">Tím se zobrazí dialogové okno "Přidat novou položku" sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e77b-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="3e77b-116">Budeme filtrovat podle kategorie "Data" a vybereme šablonu položky "Sql Server Database":</span><span class="sxs-lookup"><span data-stu-id="3e77b-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="3e77b-117">Pojmenujeme databázi SQL Server Express, kterou chceme vytvořit "NerdDinner.mdf" a stiskneme ok.</span><span class="sxs-lookup"><span data-stu-id="3e77b-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="3e77b-118">Visual Studio se pak nás zeptá, jestli chceme\_přidat tento soubor do našeho adresáře \App Data (což je adresář, který je již nastaven s seznamy ACN zabezpečení čtení i zápisu):</span><span class="sxs-lookup"><span data-stu-id="3e77b-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="3e77b-119">Klikneme na tlačítko "Ano" a naše nová databáze bude vytvořena a přidána do našeho Průzkumníka řešení:</span><span class="sxs-lookup"><span data-stu-id="3e77b-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="3e77b-120">Vytváření tabulek v naší databázi</span><span class="sxs-lookup"><span data-stu-id="3e77b-120">Creating Tables within our Database</span></span>

<span data-ttu-id="3e77b-121">Nyní máme novou prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="3e77b-121">We now have a new empty database.</span></span> <span data-ttu-id="3e77b-122">Přidáme k tomu nějaké tabulky.</span><span class="sxs-lookup"><span data-stu-id="3e77b-122">Let's add some tables to it.</span></span>

<span data-ttu-id="3e77b-123">K tomu přejdeme do okna karty Průzkumník serveru v sadě Visual Studio, které nám umožňuje spravovat databáze a servery.</span><span class="sxs-lookup"><span data-stu-id="3e77b-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="3e77b-124">Databáze SQL Server Express uložené\_ve složce \App Data naší aplikace se automaticky zobrazí v Průzkumníku serveru.</span><span class="sxs-lookup"><span data-stu-id="3e77b-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="3e77b-125">Volitelně můžeme použít ikonu "Připojit k databázi" v horní části okna "Průzkumník serveru" přidat další sql server databází (místní i vzdálené) do seznamu také:</span><span class="sxs-lookup"><span data-stu-id="3e77b-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="3e77b-126">Přidáme dvě tabulky do naší databáze NerdDinner – jeden pro uložení našich večeří a druhý pro sledování přijetí RSVP k nim.</span><span class="sxs-lookup"><span data-stu-id="3e77b-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="3e77b-127">Nové tabulky můžeme vytvořit kliknutím pravým tlačítkem myši na složku "Tabulky" v naší databázi a výběrem příkazu nabídky "Přidat novou tabulku":</span><span class="sxs-lookup"><span data-stu-id="3e77b-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="3e77b-128">Tím se otevře návrhář tabulky, který nám umožňuje konfigurovat schéma naší tabulky.</span><span class="sxs-lookup"><span data-stu-id="3e77b-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="3e77b-129">Pro naši tabulku "Večeře" přidáme 10 sloupců dat:</span><span class="sxs-lookup"><span data-stu-id="3e77b-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="3e77b-130">Chceme, aby sloupec "DinnerID" byl jedinečný primární klíč pro tabulku.</span><span class="sxs-lookup"><span data-stu-id="3e77b-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="3e77b-131">Můžeme to nakonfigurovat kliknutím pravým tlačítkem myši na sloupec "DinnerID" a výběrem položky nabídky "Nastavit primární klíč":</span><span class="sxs-lookup"><span data-stu-id="3e77b-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="3e77b-132">Kromě toho, že DinnerID primární klíč, chceme také nakonfigurovat jako sloupec "identity", jehož hodnota je automaticky zvýšena jako nové řádky dat jsou přidány do tabulky (což znamená, že první vložený řádek Večeře bude mít DinnerID 1, druhý vložený řádek bude mít DinnerID 2, atd.).</span><span class="sxs-lookup"><span data-stu-id="3e77b-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="3e77b-133">Můžeme to provést výběrem sloupce "DinnerID" a potom pomocí editoru "Vlastnosti sloupce" nastavit vlastnost "(Je identita)" ve sloupci na "Ano".</span><span class="sxs-lookup"><span data-stu-id="3e77b-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="3e77b-134">Použijeme výchozí hodnoty standardní identity (začínáme na 1 a přírůstek 1 na každém novém řádku večeři):</span><span class="sxs-lookup"><span data-stu-id="3e77b-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="3e77b-135">Tabulku pak uložíme zadáním ctrl-s nebo pomocí příkazu **Nabídka&gt;Soubor- Uložit.**</span><span class="sxs-lookup"><span data-stu-id="3e77b-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="3e77b-136">To nás vyzve k názvu tabulky.</span><span class="sxs-lookup"><span data-stu-id="3e77b-136">This will prompt us to name the table.</span></span> <span data-ttu-id="3e77b-137">Pojmenujeme to "Večeře":</span><span class="sxs-lookup"><span data-stu-id="3e77b-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="3e77b-138">Naše nová tabulka Večeře se pak zobrazí v naší databázi v průzkumníku serveru.</span><span class="sxs-lookup"><span data-stu-id="3e77b-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="3e77b-139">Poté zopakujeme výše uvedené kroky a vytvoříme tabulku "RSVP".</span><span class="sxs-lookup"><span data-stu-id="3e77b-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="3e77b-140">Tato tabulka má 3 sloupce.</span><span class="sxs-lookup"><span data-stu-id="3e77b-140">This table with have 3 columns.</span></span> <span data-ttu-id="3e77b-141">Jako primární klíč nastavíme sloupec RsvpID a také z něj uděláme sloupec identity:</span><span class="sxs-lookup"><span data-stu-id="3e77b-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="3e77b-142">Uložíme ho a dáme mu jméno "RSVP".</span><span class="sxs-lookup"><span data-stu-id="3e77b-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="3e77b-143">Nastavení relace cizího klíče mezi tabulkami</span><span class="sxs-lookup"><span data-stu-id="3e77b-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="3e77b-144">Nyní máme v naší databázi dvě tabulky.</span><span class="sxs-lookup"><span data-stu-id="3e77b-144">We now have two tables within our database.</span></span> <span data-ttu-id="3e77b-145">Náš poslední krok návrhu schématu bude nastavení relace "1:N" mezi těmito dvěma tabulkami – abychom mohli přidružit každý řádek Večeři s nulou nebo více řádky RSVP, které se na něj vztahují.</span><span class="sxs-lookup"><span data-stu-id="3e77b-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="3e77b-146">Provedeme to tak, že nakonfigurujeme sloupec "DinnerID" tabulky RSVP tak, aby měl vztah cizího klíče ke sloupci "DinnerID" v tabulce "Dinners".</span><span class="sxs-lookup"><span data-stu-id="3e77b-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="3e77b-147">K tomu otevřeme tabulku RSVP v návrháři tabulky poklepáním v průzkumníku serveru.</span><span class="sxs-lookup"><span data-stu-id="3e77b-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="3e77b-148">Poté v něm vybereme sloupec "DinnerID", klikněte pravým tlačítkem myši a zvolíme "Vztahy..." kontextová nabídka, příkaz:</span><span class="sxs-lookup"><span data-stu-id="3e77b-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="3e77b-149">Tím se zobrazí dialogové okno, které můžeme použít k nastavení relací mezi tabulkami:</span><span class="sxs-lookup"><span data-stu-id="3e77b-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="3e77b-150">Kliknutím na tlačítko Přidat přidáme do dialogového okna nový vztah.</span><span class="sxs-lookup"><span data-stu-id="3e77b-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="3e77b-151">Po přidání relace rozbalíme uzel stromového zobrazení "Tabulky a specifikace sloupce" v rámci mřížky vlastností napravo od dialogového okna a poté klikneme na "..." napravo od něj:</span><span class="sxs-lookup"><span data-stu-id="3e77b-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="3e77b-152">Kliknutím na tlačítko "..." tlačítko zobrazí další dialog, který nám umožní určit, které tabulky a sloupce jsou zapojeny do relace, stejně jako nám umožní pojmenovat vztah.</span><span class="sxs-lookup"><span data-stu-id="3e77b-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="3e77b-153">Změníme tabulku primárního klíče na "Večeře" a jako primární klíč vybereme sloupec DinnerID v tabulce Večeře.</span><span class="sxs-lookup"><span data-stu-id="3e77b-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="3e77b-154">Naše tabulka RSVP bude tabulka cizího klíče a RSVP. Sloupec DinnerID bude přidružen jako cizí klíč:</span><span class="sxs-lookup"><span data-stu-id="3e77b-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="3e77b-155">Nyní bude každý řádek v tabulce RSVP přidružen k řádku v tabulce Večeři.</span><span class="sxs-lookup"><span data-stu-id="3e77b-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="3e77b-156">SQL Server bude udržovat referenční integritu pro nás – a zabránit nám v přidání nového řádku RSVP, pokud neodkazuje na platný řádek Dinner.</span><span class="sxs-lookup"><span data-stu-id="3e77b-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="3e77b-157">Zabrání nám také odstranění řádku Dinner, pokud na něj stále odkazují řádky RSVP.</span><span class="sxs-lookup"><span data-stu-id="3e77b-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="3e77b-158">Přidávání dat do našich tabulek</span><span class="sxs-lookup"><span data-stu-id="3e77b-158">Adding Data to our Tables</span></span>

<span data-ttu-id="3e77b-159">Na závěr přidáme některá ukázková data do tabulky Večeře.</span><span class="sxs-lookup"><span data-stu-id="3e77b-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="3e77b-160">Data můžeme do tabulky přidat tak, že na ně klikneme pravým tlačítkem myši v Průzkumníku serveru a vyberete příkaz Zobrazit data tabulky:</span><span class="sxs-lookup"><span data-stu-id="3e77b-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="3e77b-161">Přidáme několik řádků dat večeři, které můžeme použít později, když začneme implementovat aplikaci:</span><span class="sxs-lookup"><span data-stu-id="3e77b-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="3e77b-162">Další krok</span><span class="sxs-lookup"><span data-stu-id="3e77b-162">Next Step</span></span>

<span data-ttu-id="3e77b-163">Dokončili jsme vytvoření naší databáze.</span><span class="sxs-lookup"><span data-stu-id="3e77b-163">We've finished creating our database.</span></span> <span data-ttu-id="3e77b-164">Nyní vytvoříme třídy modelů, které můžeme použít k dotazování a aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="3e77b-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e77b-165">[Předchozí](create-a-new-aspnet-mvc-project.md)
> [další](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="3e77b-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
