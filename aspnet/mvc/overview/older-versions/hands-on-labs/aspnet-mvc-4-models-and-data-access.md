---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 – modely a přístup k datům | Dokumentace Microsoftu
author: rick-anderson
description: 'Poznámka: Tohoto praktického testovacího prostředí se předpokládá, že máte základní znalosti ASP.NET MVC. Pokud jste ještě nepoužívali ASP.NET MVC před, doporučujeme si projít ASP.NET MVC 4...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129694"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="1c590-104">ASP.NET MVC 4 – modely a přístup k datům</span><span class="sxs-lookup"><span data-stu-id="1c590-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="1c590-105">podle [Campy Web týmu](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="1c590-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="1c590-106">Stáhněte si Web Campy školení Kit</span><span class="sxs-lookup"><span data-stu-id="1c590-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="1c590-107">Tohoto praktického testovacího prostředí předpokládá, že máte základní znalosti o **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="1c590-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="1c590-108">Pokud jste ještě nepoužívali **ASP.NET MVC** před, doporučujeme si projít **základy ASP.NET MVC 4** praktického testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="1c590-109">Tato laboratoř vás provede vylepšení a nových funkcí popsaných dříve použitím menší změny na ukázkovou webovou aplikaci ve zdrojové složce k dispozici.</span><span class="sxs-lookup"><span data-stu-id="1c590-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-110">Všechny ukázky kódu a fragmenty kódu jsou součástí této webové Campy školicí sady, k dispozici na [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="1c590-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="1c590-111">Projekt specifické pro toto testovací prostředí je k dispozici na [ASP.NET MVC 4 modely a přístup k datům](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span><span class="sxs-lookup"><span data-stu-id="1c590-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="1c590-112">V **základy ASP.NET MVC** praktického testovacího prostředí, budete mít se předávání pevně zakódované dat z řadičů zobrazit šablony.</span><span class="sxs-lookup"><span data-stu-id="1c590-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="1c590-113">Ale, aby bylo možné sestavit aplikace skutečný webu, můžete chtít použít skutečné databázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="1c590-114">Použití databázového stroje, aby bylo možné ukládat a načítat data potřebná pro aplikace Music Store se zobrazí tohoto praktického testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="1c590-115">Chcete-li provést tuto akci, bude začínat existující databázi a vytvoření modelu Entity Data Model z něj.</span><span class="sxs-lookup"><span data-stu-id="1c590-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="1c590-116">V tomto testovacím prostředí, se bude splňovat **Database First** přístup také **Code First** přístup.</span><span class="sxs-lookup"><span data-stu-id="1c590-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="1c590-117">Ale můžete také použít **první Model** přístup, vytvořit stejný model pomocí nástrojů a pak z něj vygenerovala databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="1c590-118">![První vs databáze. Model první](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. První model")</span><span class="sxs-lookup"><span data-stu-id="1c590-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="1c590-119">*První vs databáze. První model*</span><span class="sxs-lookup"><span data-stu-id="1c590-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="1c590-120">Po vygenerování modelu, budou v StoreController poskytnout dat získaných z databáze, místo použití pevně zakódované data Store zobrazení správné nastavení.</span><span class="sxs-lookup"><span data-stu-id="1c590-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="1c590-121">Nebudete muset provádět změny do zobrazení šablon vzhledem k tomu, že StoreController se vrací stejný modely ViewModels do zobrazení šablon, ale tentokrát data budou přicházet z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="1c590-122">**Přístupu Code First**</span><span class="sxs-lookup"><span data-stu-id="1c590-122">**The Code First Approach**</span></span>

<span data-ttu-id="1c590-123">Přístupu Code First umožňuje definovat model z kódu bez generování třídy, které jsou obvykle svázány s použitím rozhraní framework.</span><span class="sxs-lookup"><span data-stu-id="1c590-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="1c590-124">V kódu nejprve modelu objekty jsou definovány pomocí POCOs, &quot;prostý starší objekty CLR&quot;.</span><span class="sxs-lookup"><span data-stu-id="1c590-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="1c590-125">POCOs jsou jednoduché prostý třídy, které jste žádné dědičnosti a neimplementují rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1c590-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="1c590-126">Databázi jsme můžete vygenerovat automaticky z nich, nebo můžeme použít stávající databázi a generovat mapování tříd z kódu.</span><span class="sxs-lookup"><span data-stu-id="1c590-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="1c590-127">Výhody použití tohoto přístupu je, že zůstane modelu nezávisle na stálost framework (v tomto případě Entity Framework), jako POCOs třídy nejsou doplňuje rozhraní mapování.</span><span class="sxs-lookup"><span data-stu-id="1c590-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-128">Toto testovací prostředí je založena na technologii ASP.NET MVC 4 a verzi vzorové aplikace Music Store přizpůsobit a minimalizaci podle pouze funkce, které jsou zobrazené ve tohoto praktického testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="1c590-129">Pokud chcete prozkoumat celé **Music Store** aplikace se nachází v [MVC. Music Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="1c590-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="1c590-130">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1c590-130">Prerequisites</span></span>

<span data-ttu-id="1c590-131">Musíte mít následující položky k dokončení tohoto testovacího prostředí:</span><span class="sxs-lookup"><span data-stu-id="1c590-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="1c590-132">[Microsoft Visual Studio Express 2012 pro Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo i vyšší (čtení [příloha A](#AppendixA) pokyny k jeho instalaci).</span><span class="sxs-lookup"><span data-stu-id="1c590-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="1c590-133">Instalace</span><span class="sxs-lookup"><span data-stu-id="1c590-133">Setup</span></span>

<span data-ttu-id="1c590-134">**Instalace fragmenty kódu**</span><span class="sxs-lookup"><span data-stu-id="1c590-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="1c590-135">Pro usnadnění práce velkou část kódu, které budete spravovat podél tohoto testovacího prostředí je k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c590-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="1c590-136">K instalaci spustit fragmenty kódu **.\Source\Setup\CodeSnippets.vsi** souboru.</span><span class="sxs-lookup"><span data-stu-id="1c590-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="1c590-137">Pokud nejste obeznámeni s fragmenty kódu Visual Studio a chcete další informace o jejich použití, najdete dodatku z tohoto dokumentu &quot; [příloha C: Používání fragmentů kódu](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="1c590-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="1c590-138">Cvičení</span><span class="sxs-lookup"><span data-stu-id="1c590-138">Exercises</span></span>

<span data-ttu-id="1c590-139">Podle následující praktická cvičení se skládá tohoto praktického testovacího prostředí:</span><span class="sxs-lookup"><span data-stu-id="1c590-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="1c590-140">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="1c590-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="1c590-141">Cvičení 2: Vytvoření databáze pomocí Code First</span><span class="sxs-lookup"><span data-stu-id="1c590-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="1c590-142">Cvičení 3: Dotazování na databázi s parametry</span><span class="sxs-lookup"><span data-stu-id="1c590-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="1c590-143">Se sadou každý cvičení **koncové** složku, která obsahuje výsledný řešení byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="1c590-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="1c590-144">Toto řešení můžete použít jako vodítko, pokud potřebujete další pomoc prostřednictvím praktická cvičení.</span><span class="sxs-lookup"><span data-stu-id="1c590-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="1c590-145">Odhadovaný čas dokončení tohoto testovacího prostředí: **35 minut**.</span><span class="sxs-lookup"><span data-stu-id="1c590-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="1c590-146">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="1c590-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="1c590-147">V tomto cvičení se dozvíte, jak přidat databázi s tabulkami aplikace MusicStore k řešení, aby bylo možné využívat svoje data.</span><span class="sxs-lookup"><span data-stu-id="1c590-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="1c590-148">Jakmile databáze je generována s modelem a přidán do řešení, upravíte třídy StoreController poskytli šablonu zobrazení s daty z databáze, místo pevně definovaných hodnot.</span><span class="sxs-lookup"><span data-stu-id="1c590-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="1c590-149">Úloha 1 – přidání databáze</span><span class="sxs-lookup"><span data-stu-id="1c590-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="1c590-150">V této úloze přidá již vytvořené databáze s hlavním tabulkami MusicStore aplikace do řešení.</span><span class="sxs-lookup"><span data-stu-id="1c590-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="1c590-151">Otevřít **začít** řešení nachází v **zdroj/Ex1-AddingADatabaseDBFirst/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="1c590-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="1c590-152">Budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="1c590-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="1c590-153">Chcete-li to provést, klikněte na tlačítko **projektu** nabídky a vybereme **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1c590-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1c590-154">V **spravovat balíčky NuGet** dialogového okna, klikněte na tlačítko **obnovení** aby bylo možné stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="1c590-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="1c590-155">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="1c590-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1c590-156">Jednou z výhod pomocí nástroje NuGet je, že není nutné dodávat všechny knihovny ve vašem projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="1c590-157">Pomocí nástroje NuGet zadáním verze balíčku v souboru Packages.config, budete moct stáhnout požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="1c590-158">To je důvod, proč budete muset projít tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="1c590-159">Přidat **MvcMusicStore** databázový soubor.</span><span class="sxs-lookup"><span data-stu-id="1c590-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="1c590-160">Ve tohoto praktického testovacího prostředí, budete používat již vytvořené databázi s názvem **MvcMusicStore.mdf**.</span><span class="sxs-lookup"><span data-stu-id="1c590-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="1c590-161">Pokud chcete udělat, klikněte pravým tlačítkem na **aplikace\_Data** složku, přejděte na **přidat** a potom klikněte na tlačítko **existující položku**.</span><span class="sxs-lookup"><span data-stu-id="1c590-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="1c590-162">Přejděte do **\Source\Assets** a vyberte **MvcMusicStore.mdf** souboru.</span><span class="sxs-lookup"><span data-stu-id="1c590-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="1c590-163">![Přidání existující položky](aspnet-mvc-4-models-and-data-access/_static/image2.png "přidat existující položku")</span><span class="sxs-lookup"><span data-stu-id="1c590-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="1c590-164">*Přidat existující položku*</span><span class="sxs-lookup"><span data-stu-id="1c590-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="1c590-165">![Soubor databáze MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf databázový soubor")</span><span class="sxs-lookup"><span data-stu-id="1c590-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="1c590-166">*MvcMusicStore.mdf databázový soubor*</span><span class="sxs-lookup"><span data-stu-id="1c590-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="1c590-167">Databáze je přidaný do projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-167">The database has been added to the project.</span></span> <span data-ttu-id="1c590-168">I v případě, že databáze nachází v řešení, můžete dotazovat a aktualizovat ji podle hostovaný v jiném databázovém serveru.</span><span class="sxs-lookup"><span data-stu-id="1c590-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="1c590-169">![MvcMusicStore databázi v Průzkumníku řešení](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore databázi v Průzkumníku řešení")</span><span class="sxs-lookup"><span data-stu-id="1c590-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="1c590-170">*MvcMusicStore databázi v Průzkumníku řešení*</span><span class="sxs-lookup"><span data-stu-id="1c590-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="1c590-171">Ověření připojení k databázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-171">Verify the connection to the database.</span></span> <span data-ttu-id="1c590-172">Chcete-li to provést, dvakrát klikněte na **MvcMusicStore.mdf** k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="1c590-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="1c590-173">![Připojení k MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "propojíte MvcMusicStore.mdf")</span><span class="sxs-lookup"><span data-stu-id="1c590-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="1c590-174">*Připojení k MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="1c590-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="1c590-175">Úloha 2 – Vytvoření datového modelu</span><span class="sxs-lookup"><span data-stu-id="1c590-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="1c590-176">V této úloze vytvoříte datový model pro interakci s databází přidali v předchozím úkolu.</span><span class="sxs-lookup"><span data-stu-id="1c590-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="1c590-177">Vytvoření datového modelu, která bude představovat databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="1c590-178">Chcete-li to provést, v Průzkumníku řešení klikněte pravým tlačítkem **modely** složku, přejděte na příkaz **přidat** a potom klikněte na tlačítko **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="1c590-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="1c590-179">V **přidat novou položku** dialogového okna, vyberte **Data** šablony a potom **datový Model Entity ADO.NET** položky.</span><span class="sxs-lookup"><span data-stu-id="1c590-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="1c590-180">Změňte název modelu dat na **StoreDB.edmx** a klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="1c590-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="1c590-181">![Přidání datového modelu ADO.NET Entity StoreDB](aspnet-mvc-4-models-and-data-access/_static/image6.png "přidání StoreDB ADO.NET Entity Data Model")</span><span class="sxs-lookup"><span data-stu-id="1c590-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="1c590-182">*Přidání StoreDB ADO.NET Entity Data Model*</span><span class="sxs-lookup"><span data-stu-id="1c590-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="1c590-183">**Průvodce datovým modelem Entity** se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="1c590-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="1c590-184">Tento průvodce vás provede vytvořením modelu vrstvy.</span><span class="sxs-lookup"><span data-stu-id="1c590-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="1c590-185">Protože model by měl vytvořit podle existující databázi nedávno přidali, vyberte **Generovat z databáze** a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="1c590-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="1c590-186">![Výběr obsahu modelu](aspnet-mvc-4-models-and-data-access/_static/image7.png "výběr obsahu modelu")</span><span class="sxs-lookup"><span data-stu-id="1c590-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="1c590-187">*Výběr modelu obsahu*</span><span class="sxs-lookup"><span data-stu-id="1c590-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="1c590-188">Protože jsou generování modelu z databáze, je potřeba zadat připojení se má používat.</span><span class="sxs-lookup"><span data-stu-id="1c590-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="1c590-189">Klikněte na tlačítko **nové připojení**.</span><span class="sxs-lookup"><span data-stu-id="1c590-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="1c590-190">Vyberte **soubor databáze Microsoft SQL Server** a klikněte na tlačítko **pokračovat**.</span><span class="sxs-lookup"><span data-stu-id="1c590-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="1c590-191">![Zvolit zdroj dat](aspnet-mvc-4-models-and-data-access/_static/image8.png "zvolit zdroj dat")</span><span class="sxs-lookup"><span data-stu-id="1c590-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="1c590-192">*Vyberte zdroj dat dialogového okna*</span><span class="sxs-lookup"><span data-stu-id="1c590-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="1c590-193">Klikněte na tlačítko **Procházet** a vyberte databázi **MvcMusicStore.mdf** jste vyhledali v **aplikace\_Data** složky a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c590-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="1c590-194">![Vlastnosti připojení](aspnet-mvc-4-models-and-data-access/_static/image9.png "vlastnosti připojení")</span><span class="sxs-lookup"><span data-stu-id="1c590-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="1c590-195">*Vlastnosti připojení*</span><span class="sxs-lookup"><span data-stu-id="1c590-195">*Connection properties*</span></span>
6. <span data-ttu-id="1c590-196">Generované třídy by měly mít stejný název jako připojovací řetězec entity, proto změňte její název na **MusicStoreEntities** a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="1c590-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="1c590-197">![Výběr datové připojení](aspnet-mvc-4-models-and-data-access/_static/image10.png "volba připojení dat")</span><span class="sxs-lookup"><span data-stu-id="1c590-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="1c590-198">*Výběr datové připojení*</span><span class="sxs-lookup"><span data-stu-id="1c590-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="1c590-199">Zvolte objekty databáze, které chcete použít.</span><span class="sxs-lookup"><span data-stu-id="1c590-199">Choose the database objects to use.</span></span> <span data-ttu-id="1c590-200">Jako Entity Model se použít jenom databázové tabulky, vyberte **tabulky** možnosti a ujistěte se, že **zahrnout do modelu sloupce cizích klíčů** a **Pluralize jednotné nebo množné číslo vygenerována názvy objektů** jsou vybrané možnosti.</span><span class="sxs-lookup"><span data-stu-id="1c590-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="1c590-201">Změňte Model Namespace k **MvcMusicStore.Model** a klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="1c590-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="1c590-202">![Volba databázové objekty](aspnet-mvc-4-models-and-data-access/_static/image11.png "výběr databázových objektů")</span><span class="sxs-lookup"><span data-stu-id="1c590-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="1c590-203">*Volba databázové objekty*</span><span class="sxs-lookup"><span data-stu-id="1c590-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-204">Pokud se zobrazí dialogové okno upozornění zabezpečení, klikněte na tlačítko **OK** danou šablonou spustit a generovat třídy pro model entity.</span><span class="sxs-lookup"><span data-stu-id="1c590-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="1c590-205">Diagramu entity pro databáze se zobrazí, když se vytvoří samostatné třídy, která mapuje každé tabulky do databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="1c590-206">Například **alb** tabulky budou mít stejné **alba** třídy, ve kterém bude každý sloupec v tabulce mapovat na vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="1c590-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="1c590-207">To vám umožní dotazovat a práci s objekty, které představují řádků v databázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="1c590-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span><span class="sxs-lookup"><span data-stu-id="1c590-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="1c590-209">*Entity diagram*</span><span class="sxs-lookup"><span data-stu-id="1c590-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-210">Šablony T4 (.tt) spustit kód pro generování tříd entit a přepíše existující třídy se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="1c590-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="1c590-211">V tomto příkladu třídy &quot;alba&quot;, &quot;žánr&quot; a &quot;interpreta&quot; byly přepsat vygenerovaný kód.</span><span class="sxs-lookup"><span data-stu-id="1c590-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="1c590-212">Úloha 3 – vytvoření aplikace</span><span class="sxs-lookup"><span data-stu-id="1c590-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="1c590-213">V této úloze bude zaškrtnete, i když generování modelu odebraly **alba**, **žánr** a **interpreta** tříd modelu projektu sestavení úspěšně pomocí nové tříd datových modelů.</span><span class="sxs-lookup"><span data-stu-id="1c590-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="1c590-214">Sestavte projekt výběrem **sestavení** položky nabídky a pak **sestavení MvcMusicStore**.</span><span class="sxs-lookup"><span data-stu-id="1c590-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="1c590-215">![Sestavení projektu](aspnet-mvc-4-models-and-data-access/_static/image13.png "sestavení projektu")</span><span class="sxs-lookup"><span data-stu-id="1c590-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="1c590-216">*Sestavení projektu*</span><span class="sxs-lookup"><span data-stu-id="1c590-216">*Building the project*</span></span>
2. <span data-ttu-id="1c590-217">Úspěšně se sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-217">The project builds successfully.</span></span> <span data-ttu-id="1c590-218">Proč to pořád funguje?</span><span class="sxs-lookup"><span data-stu-id="1c590-218">Why does it still work?</span></span> <span data-ttu-id="1c590-219">To funguje, protože databázové tabulky obsahuje pole, která zahrnují vlastnosti, které jste používali ve třídách odebrané **alba** a **žánr**.</span><span class="sxs-lookup"><span data-stu-id="1c590-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="1c590-220">![Sestavení proběhlo úspěšně](aspnet-mvc-4-models-and-data-access/_static/image14.png "sestavení proběhlo úspěšně")</span><span class="sxs-lookup"><span data-stu-id="1c590-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="1c590-221">*Sestavení bylo úspěšné.*</span><span class="sxs-lookup"><span data-stu-id="1c590-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="1c590-222">Návrhář zobrazí entity ve formátu diagramu, ale jsou ve skutečnosti třídy jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="1c590-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="1c590-223">Rozbalte **StoreDB.edmx** uzlu v Průzkumníku řešení a potom **StoreDB.tt**, zobrazí se nové entity vygenerované.</span><span class="sxs-lookup"><span data-stu-id="1c590-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="1c590-224">![Generované soubory](aspnet-mvc-4-models-and-data-access/_static/image15.png "generovaných souborů")</span><span class="sxs-lookup"><span data-stu-id="1c590-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="1c590-225">*Generované soubory*</span><span class="sxs-lookup"><span data-stu-id="1c590-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="1c590-226">Úloha 4 – dotazování na databázi</span><span class="sxs-lookup"><span data-stu-id="1c590-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="1c590-227">V této úloze budete aktualizovat StoreController třídy tak, aby místo použití pevně zakódované data, dotáže se na databázi a načte informace.</span><span class="sxs-lookup"><span data-stu-id="1c590-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="1c590-228">Otevřít **Controllers\StoreController.cs** a přidejte následující pole do třídy pro uložení instance **MusicStoreEntities** třídu s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="1c590-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="1c590-229">(Fragment - kódu *modely a přístup k datům – Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="1c590-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="1c590-230">**MusicStoreEntities** třída zveřejňuje vlastnosti kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="1c590-231">Aktualizace **Procházet** metody akce k načtení žánr se všemi **alb**.</span><span class="sxs-lookup"><span data-stu-id="1c590-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="1c590-232">(Fragment - kódu *modely a přístup k datům – procházení Store Ex1*)</span><span class="sxs-lookup"><span data-stu-id="1c590-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="1c590-233">Používáte funkce .NET volá **LINQ** (jazyka integrované dotazu) k zápisu výrazy dotazu silného typu pomocí těchto kolekcí – které spustí kód na databázi a vrátí objekty, které můžete naprogramovat proti.</span><span class="sxs-lookup"><span data-stu-id="1c590-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="1c590-234">Další informace o dotazech technologie LINQ, navštivte prosím [web msdn](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c590-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="1c590-235">Aktualizace **Index** metody akce k načtení všech žánrů.</span><span class="sxs-lookup"><span data-stu-id="1c590-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="1c590-236">(Fragment - kódu *modely a přístup k datům – Ex1 Store Index*)</span><span class="sxs-lookup"><span data-stu-id="1c590-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="1c590-237">Aktualizace **Index** metody akce k načtení všech žánry a transformovat kolekci do seznamu.</span><span class="sxs-lookup"><span data-stu-id="1c590-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="1c590-238">(Fragment - kódu *modely a přístup k datům – Ex1 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="1c590-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="1c590-239">Úloha 5: spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="1c590-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="1c590-240">V této úloze zkontroluje, že Store indexovou stránku se teď budou zobrazovat žánry uložených v databázi namísto pevně zakódované značky.</span><span class="sxs-lookup"><span data-stu-id="1c590-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="1c590-241">Není nutné měnit zobrazit šablonu, protože **StoreController** vrací stejné entity jako předtím, ale tentokrát data budou přicházet z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="1c590-242">Znovu sestavte řešení a stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="1c590-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="1c590-243">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="1c590-243">The project starts in the Home page.</span></span> <span data-ttu-id="1c590-244">Ověřte, že v nabídce **žánry** už není pevně zakódované seznamu a data se načtou přímo z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="1c590-246">*Procházení žánry z databáze*</span><span class="sxs-lookup"><span data-stu-id="1c590-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="1c590-247">Teď přejděte do jakékoli žánr a ověřte, že že alb budou naplněny z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="1c590-248">![Z databáze procházení alb](aspnet-mvc-4-models-and-data-access/_static/image17.png "procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="1c590-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="1c590-249">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="1c590-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="1c590-250">Cvičení 2: Vytváří se databáze nejprve pomocí kódu</span><span class="sxs-lookup"><span data-stu-id="1c590-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="1c590-251">V tomto cvičení se dozvíte, jak vytvořit databázi s tabulkami aplikace MusicStore pomocí přístupu Code First a jak přistupovat k jeho datům.</span><span class="sxs-lookup"><span data-stu-id="1c590-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="1c590-252">Po vygenerování modelu upravíte StoreController poskytnout dat získaných z databáze, místo hodnot pevně zakódované zobrazit šablonu.</span><span class="sxs-lookup"><span data-stu-id="1c590-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-253">Pokud dokončení cvičení 1 a už pracovali s Database First přístup, se teď naučíte stejné výsledky s jiným procesem.</span><span class="sxs-lookup"><span data-stu-id="1c590-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="1c590-254">Úlohy, které jsou společné s cvičení 1 byly označeny pro usnadnění vaší čtení.</span><span class="sxs-lookup"><span data-stu-id="1c590-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="1c590-255">Pokud jste nedokončili vykonávat 1 ale chtěli dozvědět přístupu Code First, můžete spustit z tohoto cvičení a získat úplné vysvětlení tohoto tématu.</span><span class="sxs-lookup"><span data-stu-id="1c590-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="1c590-256">Úloha 1 – naplnění ukázkových dat</span><span class="sxs-lookup"><span data-stu-id="1c590-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="1c590-257">V této úloze naplníte databázi s ukázkovými daty při počátečním vytvoření pomocí založeno na kódu.</span><span class="sxs-lookup"><span data-stu-id="1c590-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="1c590-258">Otevřít **začít** řešení nachází v **zdroj/Ex2-CreatingADatabaseCodeFirst/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="1c590-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="1c590-259">V opačném případě může nadále používat **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="1c590-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="1c590-260">Pokud jste otevřeli zadaných **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="1c590-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="1c590-261">Chcete-li to provést, klikněte na tlačítko **projektu** nabídky a vybereme **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1c590-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1c590-262">V **spravovat balíčky NuGet** dialogového okna, klikněte na tlačítko **obnovení** aby bylo možné stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="1c590-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="1c590-263">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="1c590-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1c590-264">Jednou z výhod pomocí nástroje NuGet je, že není nutné dodávat všechny knihovny ve vašem projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="1c590-265">Pomocí nástroje NuGet zadáním verze balíčku v souboru Packages.config, budete moct stáhnout požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="1c590-266">To je důvod, proč budete muset projít tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="1c590-267">Přidat **SampleData.cs** do souboru **modely** složky.</span><span class="sxs-lookup"><span data-stu-id="1c590-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="1c590-268">Pokud chcete udělat, klikněte pravým tlačítkem na **modely** složku, přejděte na příkaz **přidat** a potom klikněte na tlačítko **existující položku**.</span><span class="sxs-lookup"><span data-stu-id="1c590-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="1c590-269">Přejděte do **\Source\Assets** a vyberte **SampleData.cs** souboru.</span><span class="sxs-lookup"><span data-stu-id="1c590-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="1c590-270">![Ukázková data naplnit kód](aspnet-mvc-4-models-and-data-access/_static/image18.png "kód naplnění ukázkových dat")</span><span class="sxs-lookup"><span data-stu-id="1c590-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="1c590-271">*Ukázková data naplnit kódu*</span><span class="sxs-lookup"><span data-stu-id="1c590-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="1c590-272">Otevřít **Global.asax.cs** soubor a přidejte následující *pomocí* příkazy.</span><span class="sxs-lookup"><span data-stu-id="1c590-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="1c590-273">(Fragment - kódu *modely a přístup k datům – Ex2 globální direktivy using Asax*)</span><span class="sxs-lookup"><span data-stu-id="1c590-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="1c590-274">V **aplikace\_Start()** metody přidejte následující řádek nastavit inicializátor databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="1c590-275">(Fragment - kódu *modely a přístup k datům – globální Asax SetInitializer Ex2*)</span><span class="sxs-lookup"><span data-stu-id="1c590-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="1c590-276">Úloha 2 – konfigurace připojení k databázi</span><span class="sxs-lookup"><span data-stu-id="1c590-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="1c590-277">Teď, když jste už přidali do databáze na našem projektu, budete psát **Web.config** souboru připojovací řetězec.</span><span class="sxs-lookup"><span data-stu-id="1c590-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="1c590-278">Přidat připojovací řetězec na **Web.config**. Chcete-li to mohli udělat, otevřete **Web.config** v kořenu projektu a nahraďte připojovací řetězec s názvem možnost DefaultConnection se tento řádek v **&lt;connectionStrings&gt;** části:</span><span class="sxs-lookup"><span data-stu-id="1c590-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="1c590-279">![Umístění souboru Web.config](aspnet-mvc-4-models-and-data-access/_static/image19.png "umístění souboru Web.config")</span><span class="sxs-lookup"><span data-stu-id="1c590-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="1c590-280">*Umístění souboru Web.config*</span><span class="sxs-lookup"><span data-stu-id="1c590-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="1c590-281">Úloha 3 – práce s modelem</span><span class="sxs-lookup"><span data-stu-id="1c590-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="1c590-282">Teď, když jste už nakonfigurovali připojení k databázi, bude propojovat modelu s tabulkami databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="1c590-283">V této úloze vytvoříte třídu, která se propojí s databáze s Code First.</span><span class="sxs-lookup"><span data-stu-id="1c590-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="1c590-284">Mějte na paměti, že je existující třídy modelu POCO, který by měl být upraven.</span><span class="sxs-lookup"><span data-stu-id="1c590-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-285">Pokud jste dokončili cvičení 1, Všimněte si, že byl tento krok provést pomocí průvodce.</span><span class="sxs-lookup"><span data-stu-id="1c590-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="1c590-286">Tímto způsobem Code First, vytvořte ručně třídy, které budou připojeny k datovým entitám.</span><span class="sxs-lookup"><span data-stu-id="1c590-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="1c590-287">Otevřete třídu modelu POCO **žánr** z **modely** složce projektu a obsahovat identifikátor.</span><span class="sxs-lookup"><span data-stu-id="1c590-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="1c590-288">Použijte int vlastnost s názvem **GenreId**.</span><span class="sxs-lookup"><span data-stu-id="1c590-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="1c590-289">(Fragment - kódu *modely a přístup k datům – první žánr Ex2 kód*)</span><span class="sxs-lookup"><span data-stu-id="1c590-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="1c590-290">Pro práci s Code First vytváření názvů, třída rozšířením podle tematických musí mít vlastnost primárního klíče, který bude automaticky zjistit.</span><span class="sxs-lookup"><span data-stu-id="1c590-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="1c590-291">Další informace o první konvence kódu v tomto [článku na webu msdn](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c590-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="1c590-292">Nyní, otevřete třídu modelu POCO **alba** z **modely** složce projektu a zahrnují cizí klíče, vytvoření vlastnosti s názvy **GenreId** a  **ArtistId**.</span><span class="sxs-lookup"><span data-stu-id="1c590-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="1c590-293">Tato třída již **GenreId** pro primární klíč.</span><span class="sxs-lookup"><span data-stu-id="1c590-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="1c590-294">(Fragment - kódu *modely a přístup k datům – první alba Ex2 kód*)</span><span class="sxs-lookup"><span data-stu-id="1c590-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="1c590-295">Otevřete třídu modelu POCO **interpreta** a zahrnout **ArtistId** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1c590-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="1c590-296">(Fragment - kódu *modely a přístup k datům – první interpreta Ex2 kód*)</span><span class="sxs-lookup"><span data-stu-id="1c590-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="1c590-297">Klikněte pravým tlačítkem myši **modely** složky projektu a vyberte **přidat | Třída**.</span><span class="sxs-lookup"><span data-stu-id="1c590-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="1c590-298">Název souboru **MusicStoreEntities.cs**.</span><span class="sxs-lookup"><span data-stu-id="1c590-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="1c590-299">Potom klikněte na **přidat.**</span><span class="sxs-lookup"><span data-stu-id="1c590-299">Then, click **Add.**</span></span>

    <span data-ttu-id="1c590-300">![Přidání třídy](aspnet-mvc-4-models-and-data-access/_static/image20.png "přidání třídy")</span><span class="sxs-lookup"><span data-stu-id="1c590-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="1c590-301">*Přidání nové položky*</span><span class="sxs-lookup"><span data-stu-id="1c590-301">*Adding a new item*</span></span>

    <span data-ttu-id="1c590-302">![Přidávání class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "přidávání class2")</span><span class="sxs-lookup"><span data-stu-id="1c590-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="1c590-303">*Přidání třídy*</span><span class="sxs-lookup"><span data-stu-id="1c590-303">*Adding a class*</span></span>
5. <span data-ttu-id="1c590-304">Otevřete třídu, kterou jste právě vytvořili, **MusicStoreEntities.cs**a obory názvů **System.Data.Entity** a **System.Data.Entity.Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="1c590-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="1c590-305">Nahraďte deklaraci třídy pro rozšíření **DbContext** třídy: deklarovat veřejnou **DBSet** a přepsat **OnModelCreating** metody.</span><span class="sxs-lookup"><span data-stu-id="1c590-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="1c590-306">Po provedení tohoto kroku získáte doménovou třídou, která propojí váš model s rozhraním Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1c590-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="1c590-307">Aby bylo možné provést, nahraďte kód třídy následujícími způsoby:</span><span class="sxs-lookup"><span data-stu-id="1c590-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="1c590-308">(Fragment - kódu *modely a přístup k datům – první MusicStoreEntities kód Ex2*)</span><span class="sxs-lookup"><span data-stu-id="1c590-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="1c590-309">S Entity Framework **DbContext** a **DBSet** budete moci dotaz na třídu POCO žánr.</span><span class="sxs-lookup"><span data-stu-id="1c590-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="1c590-310">Tím, že rozšíří **OnModelCreating** metoda, zadáváte v **kód** mapovány žánr do databázové tabulky.</span><span class="sxs-lookup"><span data-stu-id="1c590-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="1c590-311">Další informace o kontext databáze a DBSet najdete v článku na webu msdn: [odkaz](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="1c590-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="1c590-312">Úloha 4 – dotazování na databázi</span><span class="sxs-lookup"><span data-stu-id="1c590-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="1c590-313">V této úloze budete aktualizovat StoreController třídy tak, aby místo použití pevně zakódované dat, načte se z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-314">Tato úloha je společné s cvičení 1.</span><span class="sxs-lookup"><span data-stu-id="1c590-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="1c590-315">Pokud jste dokončili cvičení 1 se nezapomeňte tyto kroky jsou stejné v obou metod (první databáze nebo kód nejprve).</span><span class="sxs-lookup"><span data-stu-id="1c590-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="1c590-316">Jsou odlišné v jak se data propojené s modelem, ale přístup k datovým entitám se ještě transparentní z kontroleru.</span><span class="sxs-lookup"><span data-stu-id="1c590-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="1c590-317">Otevřít **Controllers\StoreController.cs** a přidejte následující pole do třídy pro uložení instance **MusicStoreEntities** třídu s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="1c590-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="1c590-318">(Fragment - kódu *modely a přístup k datům – Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="1c590-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="1c590-319">**MusicStoreEntities** třída zveřejňuje vlastnosti kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="1c590-320">Aktualizace **Procházet** metody akce k načtení žánr se všemi **alb**.</span><span class="sxs-lookup"><span data-stu-id="1c590-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="1c590-321">(Fragment - kódu *modely a přístup k datům – procházení Store Ex2*)</span><span class="sxs-lookup"><span data-stu-id="1c590-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="1c590-322">Používáte funkce .NET volá **LINQ** (jazyka integrované dotazu) k zápisu výrazy dotazu silného typu pomocí těchto kolekcí – které spustí kód na databázi a vrátí objekty, které můžete naprogramovat proti.</span><span class="sxs-lookup"><span data-stu-id="1c590-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="1c590-323">Další informace o dotazech technologie LINQ, navštivte prosím [web msdn](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="1c590-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="1c590-324">Aktualizace **Index** metody akce k načtení všech žánrů.</span><span class="sxs-lookup"><span data-stu-id="1c590-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="1c590-325">(Fragment - kódu *modely a přístup k datům – Ex2 Store Index*)</span><span class="sxs-lookup"><span data-stu-id="1c590-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="1c590-326">Aktualizace **Index** metody akce k načtení všech žánry a transformovat kolekci do seznamu.</span><span class="sxs-lookup"><span data-stu-id="1c590-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="1c590-327">(Fragment - kódu *modely a přístup k datům – Ex2 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="1c590-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="1c590-328">Úloha 5: spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="1c590-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="1c590-329">V této úloze zkontroluje, že Store indexovou stránku se teď budou zobrazovat žánry uložených v databázi namísto pevně zakódované značky.</span><span class="sxs-lookup"><span data-stu-id="1c590-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="1c590-330">Není nutné měnit zobrazit šablonu, protože **StoreController** vrací stejný **StoreIndexViewModel** stejně jako předtím, ale tentokrát budou data přicházet z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="1c590-331">Znovu sestavte řešení a stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="1c590-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="1c590-332">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="1c590-332">The project starts in the Home page.</span></span> <span data-ttu-id="1c590-333">Ověřte, že v nabídce **žánry** už není pevně zakódované seznamu a data se načtou přímo z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="1c590-335">*Procházení žánry z databáze*</span><span class="sxs-lookup"><span data-stu-id="1c590-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="1c590-336">Teď přejděte do jakékoli žánr a ověřte, že že alb budou naplněny z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="1c590-337">![Z databáze procházení alb](aspnet-mvc-4-models-and-data-access/_static/image23.png "procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="1c590-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="1c590-338">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="1c590-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="1c590-339">Cvičení 3: Dotazování na databázi s parametry</span><span class="sxs-lookup"><span data-stu-id="1c590-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="1c590-340">V tomto cvičení se dozvíte, jak zadávat dotazy na databázi pomocí parametrů a jak používat tvarování výsledku dotazu, funkce, která snižuje počet databázi přistupuje k načítání dat v efektivnější.</span><span class="sxs-lookup"><span data-stu-id="1c590-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-341">Další informace o strukturování výsledku dotazu, navštivte následující [článku na webu msdn](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c590-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="1c590-342">Úloha 1 - změna StoreController alb načíst z databáze</span><span class="sxs-lookup"><span data-stu-id="1c590-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="1c590-343">V této úloze se změní **StoreController** třídy pro přístup do databáze načíst z konkrétní žánr alb.</span><span class="sxs-lookup"><span data-stu-id="1c590-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="1c590-344">Otevřít **začít** umístění řešení **Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin** složky, pokud chcete použít přístup Code-First nebo **Source\ EX3. QueryingTheDatabaseWithParametersDBFirst\Begin** složky, pokud chcete použít první databázi přístup.</span><span class="sxs-lookup"><span data-stu-id="1c590-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="1c590-345">V opačném případě může nadále používat **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="1c590-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="1c590-346">Pokud jste otevřeli zadaných **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="1c590-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="1c590-347">Chcete-li to provést, klikněte na tlačítko **projektu** nabídky a vybereme **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1c590-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1c590-348">V **spravovat balíčky NuGet** dialogového okna, klikněte na tlačítko **obnovení** aby bylo možné stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="1c590-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="1c590-349">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="1c590-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1c590-350">Jednou z výhod pomocí nástroje NuGet je, že není nutné dodávat všechny knihovny ve vašem projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="1c590-351">Pomocí nástroje NuGet zadáním verze balíčku v souboru Packages.config, budete moct stáhnout požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="1c590-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="1c590-352">To je důvod, proč budete muset projít tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1c590-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="1c590-353">Otevřít **StoreController** třídy změnit **Procházet** metody akce.</span><span class="sxs-lookup"><span data-stu-id="1c590-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="1c590-354">Chcete-li to provést, v **Průzkumníka řešení**, rozbalte **řadiče** složky a dvojím kliknutím **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="1c590-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="1c590-355">Změnit **Procházet** metody akce k načtení alb pro konkrétní žánr.</span><span class="sxs-lookup"><span data-stu-id="1c590-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="1c590-356">Chcete-li to provést, nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="1c590-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="1c590-357">(Fragment - kódu *modely a přístup k datům – EX3. StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="1c590-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="1c590-358">K naplnění kolekce entit, budete muset použít **zahrnout** metodu k určení, které chcete načíst alb příliš.</span><span class="sxs-lookup"><span data-stu-id="1c590-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="1c590-359">Můžete použít. **Metoda Single()** rozšíření v technologii LINQ vzhledem k tomu, že v tomto případě se očekává pouze jeden žánr pro alba.</span><span class="sxs-lookup"><span data-stu-id="1c590-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="1c590-360">**Metoda Single()** metoda má výraz Lambda jako parametr, který v tomto případě Určuje jeden objekt žánr tak, aby jeho název odpovídá hodnota definovaná.</span><span class="sxs-lookup"><span data-stu-id="1c590-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="1c590-361">Bude využít výhod funkce, která umožňuje určit další související entity, které chcete načíst i když je načten objekt žánr.</span><span class="sxs-lookup"><span data-stu-id="1c590-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="1c590-362">Tato funkce se nazývá **tvarování výsledek dotazu**a umožňuje zkrátit dobu potřebnou pro přístup do databáze k načtení informací.</span><span class="sxs-lookup"><span data-stu-id="1c590-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="1c590-363">V tomto scénáři budete chtít předběžného načítání pro žánr načtete alb.</span><span class="sxs-lookup"><span data-stu-id="1c590-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="1c590-364">Dotaz obsahuje **Genres.Include (&quot;alb&quot;)** k označení, má také související alb.</span><span class="sxs-lookup"><span data-stu-id="1c590-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="1c590-365">Výsledkem bude aplikace efektivnější, protože ho se načtou data žánr a alb v požadavku izolované databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="1c590-366">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="1c590-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="1c590-367">V této úloze se spustit aplikaci a alb konkrétní žánr načíst z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="1c590-368">Stisknutím klávesy **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="1c590-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="1c590-369">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="1c590-369">The project starts in the Home page.</span></span> <span data-ttu-id="1c590-370">Změňte adresu URL na **/Store/procházet? žánr = Pop** k ověření, že se výsledky načtou z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="1c590-371">![Procházení podle žánru](aspnet-mvc-4-models-and-data-access/_static/image24.png "procházením podle žánru")</span><span class="sxs-lookup"><span data-stu-id="1c590-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="1c590-372">*Procházení/Store/procházet? žánr = Pop*</span><span class="sxs-lookup"><span data-stu-id="1c590-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="1c590-373">Úloha 3 – přístup k alb podle Id</span><span class="sxs-lookup"><span data-stu-id="1c590-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="1c590-374">V této úloze bude opakujte předchozí postup pro získání alb podle jejich Id.</span><span class="sxs-lookup"><span data-stu-id="1c590-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="1c590-375">Zavřete prohlížeč v případě potřeby se vraťte do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c590-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="1c590-376">Otevřít **StoreController** třídy změnit **podrobnosti** metody akce.</span><span class="sxs-lookup"><span data-stu-id="1c590-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="1c590-377">Chcete-li to provést, v **Průzkumníka řešení**, rozbalte **řadiče** složky a dvojím kliknutím **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="1c590-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="1c590-378">Změnit **podrobnosti** metody akce k načtení podrobností alb na základě jejich **Id**. Chcete-li to provést, nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="1c590-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="1c590-379">(Fragment - kódu *modely a přístup k datům – EX3. StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="1c590-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="1c590-380">Úloha 4 – spouštění aplikace</span><span class="sxs-lookup"><span data-stu-id="1c590-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="1c590-381">V této úloze spusťte aplikaci ve webovém prohlížeči a získání podrobných informací o alba podle jejich Id.</span><span class="sxs-lookup"><span data-stu-id="1c590-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="1c590-382">Stisknutím klávesy **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="1c590-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="1c590-383">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="1c590-383">The project starts in the Home page.</span></span> <span data-ttu-id="1c590-384">Změňte adresu URL na **/Store/Details/51** nebo žánry procházením vyberte alba k ověření, že se výsledky načtou z databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="1c590-385">![Procházení podrobností](aspnet-mvc-4-models-and-data-access/_static/image25.png "procházení podrobností")</span><span class="sxs-lookup"><span data-stu-id="1c590-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="1c590-386">*Procházení /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="1c590-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="1c590-387">Kromě toho můžete nasadit tuto aplikaci následující weby Windows Azure [příloha B: Publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="1c590-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="1c590-388">Souhrn</span><span class="sxs-lookup"><span data-stu-id="1c590-388">Summary</span></span>

<span data-ttu-id="1c590-389">Za dokončení tohoto praktického testovacího prostředí jste se naučili základy ASP.NET MVC modely a přístup k datům, pomocí **Database First** přístup také **Code First** přístup:</span><span class="sxs-lookup"><span data-stu-id="1c590-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="1c590-390">Jak do řešení přidat databáze, aby bylo možné využívat svoje data</span><span class="sxs-lookup"><span data-stu-id="1c590-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="1c590-391">Postup aktualizace řadiče poskytnout dat získaných z databáze místo pevně zakódované zobrazení šablony</span><span class="sxs-lookup"><span data-stu-id="1c590-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="1c590-392">Jak dotazovat databázi pomocí parametrů</span><span class="sxs-lookup"><span data-stu-id="1c590-392">How to query the database using parameters</span></span>
- <span data-ttu-id="1c590-393">Použití dotazu výsledek tvarování, funkce, která snižuje počet přístupů databáze, načítání dat v efektivnější způsob</span><span class="sxs-lookup"><span data-stu-id="1c590-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="1c590-394">Použití Database First a Code First pracuje Microsoft Entity Framework, která propojí databázi s modelem</span><span class="sxs-lookup"><span data-stu-id="1c590-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="1c590-395">Příloha A: Instalace sady Visual Studio Express 2012 pro Web</span><span class="sxs-lookup"><span data-stu-id="1c590-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="1c590-396">Můžete nainstalovat **Microsoft Visual Studio Express 2012 pro Web** nebo jiném &quot;Express&quot; verzí pomocí **[instalačního programu webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="1c590-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="1c590-397">Postupujte podle následujících pokynů vás provede kroky potřebné k instalaci *Visual studio Express 2012 pro Web* pomocí *instalačního programu webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="1c590-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="1c590-398">Přejděte na [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="1c590-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="1c590-399">Případně, pokud jste již nainstalovali instalačního programu webové platformy, můžete otevřít a vyhledejte produkt &quot; <em>Visual Studio Express 2012 pro Web se sadou Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="1c590-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="1c590-400">Klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="1c590-400">Click on **Install Now**.</span></span> <span data-ttu-id="1c590-401">Pokud nemáte **instalačního programu webové platformy** budete přesměrováni na stáhněte a nainstalujte ji jako první.</span><span class="sxs-lookup"><span data-stu-id="1c590-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="1c590-402">Jednou **instalačního programu webové platformy** je otevřený, klikněte na tlačítko **nainstalovat** spustit instalační program.</span><span class="sxs-lookup"><span data-stu-id="1c590-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="1c590-403">![Instalace sady Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "instalace sady Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="1c590-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="1c590-404">*Instalace sady Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="1c590-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="1c590-405">Čtení všech produktů licence a podmínky a klikněte na tlačítko **souhlasím** pokračujte.</span><span class="sxs-lookup"><span data-stu-id="1c590-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí podmínek licence](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="1c590-407">*Přijetí podmínek licence*</span><span class="sxs-lookup"><span data-stu-id="1c590-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="1c590-408">Počkejte na dokončení procesu stahování a instalaci.</span><span class="sxs-lookup"><span data-stu-id="1c590-408">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="1c590-410">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="1c590-410">*Installation progress*</span></span>
6. <span data-ttu-id="1c590-411">Až instalace skončí, klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="1c590-411">When the installation completes, click **Finish**.</span></span>

    ![Instalace byla dokončena.](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="1c590-413">*Instalace byla dokončena.*</span><span class="sxs-lookup"><span data-stu-id="1c590-413">*Installation completed*</span></span>
7. <span data-ttu-id="1c590-414">Klikněte na tlačítko **ukončovací** zavřete instalačního programu webové platformy.</span><span class="sxs-lookup"><span data-stu-id="1c590-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="1c590-415">Chcete-li spustit nástroj Visual Studio Express for Web, přejděte **Start** obrazovky a začít psát &quot; **VS Express**&quot;, klikněte na **VS Express for Web** dlaždice.</span><span class="sxs-lookup"><span data-stu-id="1c590-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web dlaždice](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="1c590-417">*VS Express for Web dlaždice*</span><span class="sxs-lookup"><span data-stu-id="1c590-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="1c590-418">Příloha B: Publikování aplikace ASP.NET MVC 4 pomocí nasazení webu</span><span class="sxs-lookup"><span data-stu-id="1c590-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="1c590-419">Tento dodatek se ukazují, jak vytvořit nový web z portálu správy Windows Azure a publikovat aplikace, kterou jste získali podle testovacího prostředí, využít Webdeploy funkce publikování ve Windows Azure k dispozici.</span><span class="sxs-lookup"><span data-stu-id="1c590-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="1c590-420">Úloha 1 – Vytvoření nového webu z Windows webu Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c590-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="1c590-421">Přejděte [Windows Azure Management Portal](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoft spojených s vaším předplatným.</span><span class="sxs-lookup"><span data-stu-id="1c590-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-422">Windows Azure můžete zadarmo hostovat 10 webů ASP.NET a pak škálujte podle rozšiřujícího se provozu.</span><span class="sxs-lookup"><span data-stu-id="1c590-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="1c590-423">Můžete se zaregistrovat [tady](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="1c590-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="1c590-424">![Přihlaste se k portálu Windows Azure](aspnet-mvc-4-models-and-data-access/_static/image31.png "Přihlaste se k portálu Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="1c590-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="1c590-425">*Přihlaste se k portálu pro správu Azure Windows*</span><span class="sxs-lookup"><span data-stu-id="1c590-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="1c590-426">Klikněte na tlačítko **nový** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="1c590-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="1c590-427">![Vytvoření nového webu](aspnet-mvc-4-models-and-data-access/_static/image32.png "vytváření nového webu")</span><span class="sxs-lookup"><span data-stu-id="1c590-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="1c590-428">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="1c590-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="1c590-429">Klikněte na tlačítko **Compute** | **webu**.</span><span class="sxs-lookup"><span data-stu-id="1c590-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="1c590-430">Potom vyberte **rychlé vytvoření** možnost.</span><span class="sxs-lookup"><span data-stu-id="1c590-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="1c590-431">Zadejte adresu URL k dispozici pro nový web a klikněte na tlačítko **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="1c590-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-432">Hostitel pro webovou aplikaci spuštěnou v cloudu, který může řídit a spravovat je web Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="1c590-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="1c590-433">Možnost rychle vytvořit můžete nasadit hotové webové aplikace na Windows Azure web z mimo portál.</span><span class="sxs-lookup"><span data-stu-id="1c590-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="1c590-434">Nezahrnuje kroky pro vytvoření databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="1c590-435">![Vytvoření nového webu pomocí metody rychlého vytvoření](aspnet-mvc-4-models-and-data-access/_static/image33.png "vytváření nového webu pomocí metody rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="1c590-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="1c590-436">*Vytvoření nového webu pomocí metody rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="1c590-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="1c590-437">Počkejte, dokud nové **webu** se vytvoří.</span><span class="sxs-lookup"><span data-stu-id="1c590-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="1c590-438">Po vytvoření webové stránky, klikněte na odkaz v části **URL** sloupce.</span><span class="sxs-lookup"><span data-stu-id="1c590-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="1c590-439">Zkontrolujte, jestli funguje nový web.</span><span class="sxs-lookup"><span data-stu-id="1c590-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="1c590-440">![Na nový web](aspnet-mvc-4-models-and-data-access/_static/image34.png "přechodu na nový web")</span><span class="sxs-lookup"><span data-stu-id="1c590-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="1c590-441">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="1c590-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="1c590-442">![Spuštění webu](aspnet-mvc-4-models-and-data-access/_static/image35.png "spuštění webové stránky")</span><span class="sxs-lookup"><span data-stu-id="1c590-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="1c590-443">*Spuštění webové stránky*</span><span class="sxs-lookup"><span data-stu-id="1c590-443">*Web site running*</span></span>
6. <span data-ttu-id="1c590-444">Přejděte zpět na portál a klikněte na název webové stránky v části **název** sloupec, který se zobrazí na stránkách správy.</span><span class="sxs-lookup"><span data-stu-id="1c590-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="1c590-445">![Otevřete správu webových stránek](aspnet-mvc-4-models-and-data-access/_static/image36.png "otevřete správu webových stránek")</span><span class="sxs-lookup"><span data-stu-id="1c590-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="1c590-446">*Otevřete správu webových stránek*</span><span class="sxs-lookup"><span data-stu-id="1c590-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="1c590-447">V **řídicí panel** stránce v části **rychlý přehled** klikněte na tlačítko **stáhnout profil publikování** odkaz.</span><span class="sxs-lookup"><span data-stu-id="1c590-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-448">*Profil publikování* obsahuje všechny informace požadované pro publikování webových aplikací na webu Windows Azure pro každou metodu povoleno publikování.</span><span class="sxs-lookup"><span data-stu-id="1c590-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="1c590-449">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce požadované k připojení a ověřování na základě jednotlivých koncových bodů, u kterých je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="1c590-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="1c590-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení publikační profily k automatizaci konfigurace z těchto programů pro publikování webových aplikací na Windows Azure websites.</span><span class="sxs-lookup"><span data-stu-id="1c590-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="1c590-451">![Stahování webové stránky publikovat profil](aspnet-mvc-4-models-and-data-access/_static/image37.png "stahování webové stránky profil publikování")</span><span class="sxs-lookup"><span data-stu-id="1c590-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="1c590-452">*Na webu stažení profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="1c590-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="1c590-453">Stáhněte si soubor profilu publikování do vhodného umístění.</span><span class="sxs-lookup"><span data-stu-id="1c590-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="1c590-454">Dále v tomto cvičení uvidíte jak publikovat webovou aplikaci na weby Windows Azure ze sady Visual Studio pomocí tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="1c590-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="1c590-455">![Ukládání souboru profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image38.png "ukládá se profil publikování")</span><span class="sxs-lookup"><span data-stu-id="1c590-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="1c590-456">*Ukládá se profil publikování*</span><span class="sxs-lookup"><span data-stu-id="1c590-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="1c590-457">Úloha 2 – konfigurování serveru databáze</span><span class="sxs-lookup"><span data-stu-id="1c590-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="1c590-458">Pokud vaše aplikace využívá SQL Server databáze, budete muset vytvořit server služby SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1c590-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="1c590-459">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server může tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="1c590-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="1c590-460">Pro uložení databáze aplikace budete potřebovat databázi SQL serveru.</span><span class="sxs-lookup"><span data-stu-id="1c590-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="1c590-461">Servery SQL Database můžete zobrazit ze svého předplatného na portálu správy Windows Azure na **databází Sql** | **servery** | **serveru Řídicí panel**.</span><span class="sxs-lookup"><span data-stu-id="1c590-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="1c590-462">Pokud nemáte server vytvořili, můžete vytvořit jednu **přidat** tlačítko na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="1c590-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="1c590-463">Poznamenejte si **název serveru a adresu URL, správce přihlašovací jméno a heslo**, jak je použijete v další úkoly.</span><span class="sxs-lookup"><span data-stu-id="1c590-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="1c590-464">Nevytvářet databáze, protože vytvoří se v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="1c590-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="1c590-465">![Řídicí panel serveru SQL Database](aspnet-mvc-4-models-and-data-access/_static/image39.png "řídicího panelu serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="1c590-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="1c590-466">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="1c590-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="1c590-467">V dalším úkolem budete testovat připojení k databázi ze sady Visual Studio z tohoto důvodu je nutné zahrnout místní IP adresa serveru seznamu **povolené IP adresy**.</span><span class="sxs-lookup"><span data-stu-id="1c590-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="1c590-468">Chcete-li to mohli udělat, klikněte na tlačítko **konfigurovat**, vyberte IP adresu z **aktuální IP adresa klienta** a vložte ho na **počáteční IP adresa** a **Koncová IP adresa** textová pole a klikněte na tlačítko ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) tlačítko.</span><span class="sxs-lookup"><span data-stu-id="1c590-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![Přidat IP adresu klienta](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="1c590-470">*Přidat IP adresu klienta*</span><span class="sxs-lookup"><span data-stu-id="1c590-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="1c590-471">Jednou **IP adresa klienta** je přidat do povolených IP adres klikněte na tlačítko na **Uložit** potvrďte provedené změny.</span><span class="sxs-lookup"><span data-stu-id="1c590-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrzení změn](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="1c590-473">*Potvrzení změn*</span><span class="sxs-lookup"><span data-stu-id="1c590-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="1c590-474">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí nasazení webu</span><span class="sxs-lookup"><span data-stu-id="1c590-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="1c590-475">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="1c590-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="1c590-476">V **Průzkumníka řešení**, klikněte pravým tlačítkem na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="1c590-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="1c590-477">![Publikování aplikace](aspnet-mvc-4-models-and-data-access/_static/image43.png "publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="1c590-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="1c590-478">*Publikování na webu*</span><span class="sxs-lookup"><span data-stu-id="1c590-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="1c590-479">Importujte profil publikování, který jste uložili v první úloze.</span><span class="sxs-lookup"><span data-stu-id="1c590-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="1c590-480">![Import profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image44.png "import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="1c590-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="1c590-481">*Import publikačního profilu*</span><span class="sxs-lookup"><span data-stu-id="1c590-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="1c590-482">Klikněte na tlačítko **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="1c590-482">Click **Validate Connection**.</span></span> <span data-ttu-id="1c590-483">Po dokončení ověření klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="1c590-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c590-484">Ověření bylo dokončeno, jakmile se zobrazí zelené zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="1c590-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="1c590-485">![Ověřuje se připojení](aspnet-mvc-4-models-and-data-access/_static/image45.png "ověřuje se připojení")</span><span class="sxs-lookup"><span data-stu-id="1c590-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="1c590-486">*Ověřuje se připojení*</span><span class="sxs-lookup"><span data-stu-id="1c590-486">*Validating connection*</span></span>
4. <span data-ttu-id="1c590-487">V **nastavení** stránce v části **databází** klikněte na tlačítko vedle textového pole připojení k databázi (to znamená **objekt DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="1c590-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="1c590-488">![Konfigurace nasazení webu](aspnet-mvc-4-models-and-data-access/_static/image46.png "konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="1c590-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="1c590-489">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="1c590-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="1c590-490">Konfigurace připojení k databázi následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1c590-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="1c590-491">V **název serveru** zadejte vaše pomocí adresy URL databáze SQL serveru *tcp:* předponu.</span><span class="sxs-lookup"><span data-stu-id="1c590-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="1c590-492">V **uživatelské jméno** zadejte vaše přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="1c590-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="1c590-493">V **heslo** zadejte heslo pro přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="1c590-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="1c590-494">Zadejte nový název databáze.</span><span class="sxs-lookup"><span data-stu-id="1c590-494">Type a new database name.</span></span>

     <span data-ttu-id="1c590-495">![Konfigurace cílový připojovací řetězec](aspnet-mvc-4-models-and-data-access/_static/image47.png "konfigurace cílový připojovací řetězec")</span><span class="sxs-lookup"><span data-stu-id="1c590-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="1c590-496">*Konfigurace cílový připojovací řetězec*</span><span class="sxs-lookup"><span data-stu-id="1c590-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="1c590-497">Pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c590-497">Then click **OK**.</span></span> <span data-ttu-id="1c590-498">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="1c590-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="1c590-499">![Vytvoření databáze](aspnet-mvc-4-models-and-data-access/_static/image48.png "vytvoření řetězce databáze")</span><span class="sxs-lookup"><span data-stu-id="1c590-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="1c590-500">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="1c590-500">*Creating the database*</span></span>
7. <span data-ttu-id="1c590-501">Připojovací řetězec, který budete používat pro připojení k databázi SQL ve službě Windows Azure se zobrazí v textovém poli výchozí připojení.</span><span class="sxs-lookup"><span data-stu-id="1c590-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="1c590-502">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="1c590-502">Then click **Next**.</span></span>

    <span data-ttu-id="1c590-503">![Připojovací řetězec odkazující na SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "připojovací řetězec odkazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="1c590-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="1c590-504">*Připojovací řetězec odkazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="1c590-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="1c590-505">V **ve verzi Preview** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="1c590-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="1c590-506">![Publikování webové aplikace](aspnet-mvc-4-models-and-data-access/_static/image50.png "publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="1c590-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="1c590-507">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="1c590-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="1c590-508">Až se proces publikování dokončí, otevře se váš výchozí prohlížeč publikovaného webu.</span><span class="sxs-lookup"><span data-stu-id="1c590-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="1c590-509">Příloha C: Používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="1c590-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="1c590-510">Pomocí fragmentů kódu máte všechny kód, který je třeba na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="1c590-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="1c590-511">Testovací prostředí dokumentu zjistíte přesně kdy je můžete využít, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="1c590-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="1c590-512">![Používání fragmentů kódu sady Visual Studio pro vložení kódu do projektu](aspnet-mvc-4-models-and-data-access/_static/image51.png "pomocí sady Visual Studio fragmenty kódu pro vložení kódu do projektu")</span><span class="sxs-lookup"><span data-stu-id="1c590-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="1c590-513">*Používání fragmentů kódu sady Visual Studio pro vložení kódu do projektu*</span><span class="sxs-lookup"><span data-stu-id="1c590-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="1c590-514">***Chcete-li přidat fragment kódu pomocí klávesnice (C# jenom)***</span><span class="sxs-lookup"><span data-stu-id="1c590-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="1c590-515">Umístěte kurzor, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="1c590-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="1c590-516">Začněte psát název fragmentu kódu (bez mezer nebo pomlčky).</span><span class="sxs-lookup"><span data-stu-id="1c590-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="1c590-517">Podívejte se na jako IntelliSense zobrazí odpovídající názvy fragmenty kódu.</span><span class="sxs-lookup"><span data-stu-id="1c590-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="1c590-518">Vyberte správný fragment kódu (nebo pokračujte v psaní dokud nebude vybraný celý fragment název).</span><span class="sxs-lookup"><span data-stu-id="1c590-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="1c590-519">Stiskněte klávesu Tabulátor dvakrát pro vložení fragmentu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="1c590-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="1c590-520">![Začněte psát název fragmentu kódu](aspnet-mvc-4-models-and-data-access/_static/image52.png "začněte psát název fragmentu kódu")</span><span class="sxs-lookup"><span data-stu-id="1c590-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="1c590-521">*Začněte psát název fragmentu kódu*</span><span class="sxs-lookup"><span data-stu-id="1c590-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="1c590-522">![Stiskněte klávesu Tab k vybrání fragmentu zvýrazněné](aspnet-mvc-4-models-and-data-access/_static/image53.png "stisknutím klávesy Tab k výběru zvýrazněné fragment kódu")</span><span class="sxs-lookup"><span data-stu-id="1c590-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="1c590-523">*Stiskněte klávesu Tab k výběru zvýrazněné fragment kódu*</span><span class="sxs-lookup"><span data-stu-id="1c590-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="1c590-524">![Stisknutím klávesy Tab znovu a fragment kódu se rozbalí](aspnet-mvc-4-models-and-data-access/_static/image54.png "znovu stisknutím klávesy Tab a fragment kódu se rozbalí.")</span><span class="sxs-lookup"><span data-stu-id="1c590-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="1c590-525">*Stisknutím klávesy Tab znovu a fragment kódu se rozbalí.*</span><span class="sxs-lookup"><span data-stu-id="1c590-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="1c590-526">***Chcete-li přidat fragment kódu pomocí myši (C#, Visual Basic a XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="1c590-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="1c590-527">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="1c590-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="1c590-528">Vyberte **Vložit fragment** následovaný **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="1c590-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="1c590-529">Kliknutím na vyberte relevantní fragment kódu ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="1c590-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="1c590-530">![Klikněte pravým tlačítkem, ve které chcete vložit fragment kódu a vyberte Vložit fragment](aspnet-mvc-4-models-and-data-access/_static/image55.png "klikněte pravým tlačítkem, ve které chcete vložit fragment kódu a vyberte Vložit fragment")</span><span class="sxs-lookup"><span data-stu-id="1c590-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="1c590-531">*Klikněte pravým tlačítkem na, ve které chcete vložit fragment kódu a vyberte Vložit fragment*</span><span class="sxs-lookup"><span data-stu-id="1c590-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="1c590-532">![Vyberte si relevantní fragment kódu ze seznamu, kliknutím na](aspnet-mvc-4-models-and-data-access/_static/image56.png "relevantní fragment kódu ze seznamu vyberte kliknutím na")</span><span class="sxs-lookup"><span data-stu-id="1c590-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="1c590-533">*Vyberte si relevantní fragment kódu ze seznamu, kliknutím na*</span><span class="sxs-lookup"><span data-stu-id="1c590-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
