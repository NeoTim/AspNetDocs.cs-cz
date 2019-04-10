---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Nasazení webové aplikace ASP.NET s SQL serverem Compact pomocí sady Visual Studio nebo Visual Web Developer: Nasazení aktualizace kódu – 8 12 | Dokumentace Microsoftu'
author: tdykstra
description: Tato série kurzů se dozvíte, jak nasadit (publikovat) technologie ASP.NET, která obsahuje databázi systému SQL Server Compact pomocí Visual samostatného projektu webové aplikace...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: f06fd5d28613ba8f881df2d1422fead2fff8c35f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59399889"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="632f7-103">Nasazení webové aplikace ASP.NET s SQL serverem Compact pomocí sady Visual Studio nebo Visual Web Developer: Nasazení aktualizace kódu – 8 12</span><span class="sxs-lookup"><span data-stu-id="632f7-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="632f7-104">podle [Petr Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="632f7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="632f7-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="632f7-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="632f7-106">Tato série kurzů se dozvíte, jak nasadit (publikovat) technologie ASP.NET webové aplikace, která obsahuje databázi systému SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro Web.</span><span class="sxs-lookup"><span data-stu-id="632f7-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="632f7-107">Můžete také použít Visual Studio 2010 při instalaci aktualizace Publikovat Web.</span><span class="sxs-lookup"><span data-stu-id="632f7-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="632f7-108">Úvod do řady, naleznete v tématu [z prvního kurzu této série](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="632f7-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="632f7-109">Kurz ukazuje nasazení funkce zavedená po verzi RC sady Visual Studio 2012, ukazuje, jak nasadit edicích systému SQL Server než SQL Server Compact a ukazuje, jak nasadit do Azure App Service Web Apps, najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="632f7-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="632f7-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="632f7-110">Overview</span></span>

<span data-ttu-id="632f7-111">Po počátečním nasazení pokračuje v práci údržbu a vývoj webu, a před dlouho budete chtít nasazení aktualizace.</span><span class="sxs-lookup"><span data-stu-id="632f7-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="632f7-112">Tento kurz vás provede procesem nasazení aktualizace kódu aplikace.</span><span class="sxs-lookup"><span data-stu-id="632f7-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="632f7-113">Tato aktualizace nezahrnuje Změna databáze; uvidíte, co se liší o nasazení změn databází v dalším kurzu.</span><span class="sxs-lookup"><span data-stu-id="632f7-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="632f7-114">Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje tak, jak absolvovat kurz, nezapomeňte se podívat [stránka o řešení problémů](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="632f7-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="632f7-115">Změna kódu</span><span class="sxs-lookup"><span data-stu-id="632f7-115">Making a Code Change</span></span>

<span data-ttu-id="632f7-116">Jako jednoduchý příklad příkazu update pro vaši aplikaci, přidáte k **Instruktoři** stránce Seznam kurzy vedené vybrané instruktorem.</span><span class="sxs-lookup"><span data-stu-id="632f7-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="632f7-117">Při spuštění **Instruktoři** stránky, můžete si všimnout, že jsou **vyberte** odkazy v mřížce, ale jejich nic nedělají než zkontrolujte šedá zapnout pozadí řádku.</span><span class="sxs-lookup"><span data-stu-id="632f7-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

[![I<span data-ttu-id="632f7-118">nstructors_page]</span><span class="sxs-lookup"><span data-stu-id="632f7-118">nstructors_page]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

<span data-ttu-id="632f7-119">Teď přidejte kód, který spouští, když **vyberte** dojde ke kliknutí na odkaz a zobrazí seznam kurzy vedené vybrané instruktorem.</span><span class="sxs-lookup"><span data-stu-id="632f7-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="632f7-120">V *Instructors.aspx*, přidejte následující kód bezprostředně po **ErrorMessageLabel** `Label` ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="632f7-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="632f7-121">Spustit na stránku a vybrat instruktorem.</span><span class="sxs-lookup"><span data-stu-id="632f7-121">Run the page and select an instructor.</span></span> <span data-ttu-id="632f7-122">Zobrazí seznam kurzy vedené této instruktorem.</span><span class="sxs-lookup"><span data-stu-id="632f7-122">You see a list of courses taught by that instructor.</span></span>

[![I<span data-ttu-id="632f7-123">nstructors_page_with_courses]</span><span class="sxs-lookup"><span data-stu-id="632f7-123">nstructors_page_with_courses]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="632f7-124">Nasazení aktualizace kódu do testovacího prostředí</span><span class="sxs-lookup"><span data-stu-id="632f7-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="632f7-125">Nasazení do testovacího prostředí je znovu publikovat jednoduché spuštění jedním kliknutím.</span><span class="sxs-lookup"><span data-stu-id="632f7-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="632f7-126">Chcete-li tento proces urychlit, můžete použít **publikování webu jedním kliknutím** nástrojů.</span><span class="sxs-lookup"><span data-stu-id="632f7-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="632f7-127">V **zobrazení** nabídce zvolte **panely nástrojů** a pak vyberte **publikování webu jedním kliknutím**.</span><span class="sxs-lookup"><span data-stu-id="632f7-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="632f7-129">V **Průzkumníka řešení**, vyberte projekt ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="632f7-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="632f7-130">**publikování webu jedním kliknutím** nástrojů, zvolte **testovací** profil publikování a pak klikněte na tlačítko **Publikovat Web** (na ikonu šipky směřující vlevo a vpravo).</span><span class="sxs-lookup"><span data-stu-id="632f7-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="632f7-132">Visual Studio nasadí aktualizované aplikace a prohlížeč se automaticky otevře na domovskou stránku.</span><span class="sxs-lookup"><span data-stu-id="632f7-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="632f7-133">Spustit školitelů stránky a vyberte k ověření, že se aktualizace úspěšně nasadilo instruktorem.</span><span class="sxs-lookup"><span data-stu-id="632f7-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

[![I<span data-ttu-id="632f7-134">nstructors_page_with_courses_Test]</span><span class="sxs-lookup"><span data-stu-id="632f7-134">nstructors_page_with_courses_Test]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

<span data-ttu-id="632f7-135">Běžným způsobem provést také regresního testování (to znamená, že test zbytku lokality, abyste měli jistotu, že tato nová změna neměli přerušit všechny existující funkce).</span><span class="sxs-lookup"><span data-stu-id="632f7-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="632f7-136">Ale pro účely tohoto kurzu budete tento krok přeskočit a přejít k nasazení aktualizací do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="632f7-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="632f7-137">Brání počáteční stav databáze opakované nasazení do produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="632f7-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="632f7-138">V reálné aplikaci uživatelé komunikují s svoje produkční lokality po počátečním nasazení a databází se vyplní s dynamickými daty.</span><span class="sxs-lookup"><span data-stu-id="632f7-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="632f7-139">Proto nechcete znovu nasadit databázi členství v tomto počátečním stavu, který by vymazat všechny dynamická data.</span><span class="sxs-lookup"><span data-stu-id="632f7-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="632f7-140">Vzhledem k tomu, že jsou soubory v systému SQL Server Compact databáze *aplikace\_Data* složku, je nutné zabránit to změnou nastavení nasazení, které soubory v *aplikace\_Data* složky nenasadí.</span><span class="sxs-lookup"><span data-stu-id="632f7-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="632f7-141">Otevřít **vlastnosti projektu** okně ContosoUniversity projektu a vyberte **balení/publikování webu** kartu. Ujistěte se, že **konfigurace** rozevíracího seznamu se buď **aktivní (verze)** nebo **vydání** vybraná, vyberte **vyloučit soubory z aplikace\_Složky dat**.</span><span class="sxs-lookup"><span data-stu-id="632f7-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="632f7-143">V případě, že se rozhodnete nasazení ladicího buildu v budoucnu, je vhodné provést stejnou změnu pro konfiguraci sestavení ladění: Změna **konfigurace** k **ladění** a pak vyberte **vyloučit soubory z aplikace\_složka dat**.</span><span class="sxs-lookup"><span data-stu-id="632f7-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="632f7-144">Uložte a zavřete **balení/publikování webu** kartu.</span><span class="sxs-lookup"><span data-stu-id="632f7-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="632f7-145">Ujistěte se, že není nutné **odebrat další soubory v cílovém umístění** vybrané v profilech publikování.</span><span class="sxs-lookup"><span data-stu-id="632f7-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="632f7-146">Pokud vyberete tuto možnost, procesu nasazení se odstraní databáze, které máte v aplikaci\_Data v nasazené lokality který se odstraní aplikaci\_samotné složce Data.</span><span class="sxs-lookup"><span data-stu-id="632f7-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>


## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="632f7-147">Zabránění přístupu uživatelů k produkční lokality během aktualizace</span><span class="sxs-lookup"><span data-stu-id="632f7-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="632f7-148">Změna, kterou nasazujete nyní je jednoduchou změnu na jednu stránku.</span><span class="sxs-lookup"><span data-stu-id="632f7-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="632f7-149">Ale v některých případech můžete nasadit větší změny a v takovém případě web se může chovat podivné Pokud uživatel požádá o stránku předtím, než se nasazení dokončí.</span><span class="sxs-lookup"><span data-stu-id="632f7-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="632f7-150">Chcete-li tomu zabránit, můžete použít *aplikace\_offline.htm* souboru.</span><span class="sxs-lookup"><span data-stu-id="632f7-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="632f7-151">Zadaný soubor s názvem *aplikace\_offline.htm* v kořenové složce vaší aplikace, služba IIS automaticky zobrazí tento soubor namísto spuštění vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="632f7-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="632f7-152">Takže pokud chcete zabránit přístupu během nasazování, kam si ukládáte *aplikace\_offline.htm* v kořenové složce spustit proces nasazení a pak odeberte *aplikace\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="632f7-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="632f7-153">V **Průzkumníka řešení**klikněte pravým tlačítkem řešení (ne z projektů) a vyberte **novou složku řešení**.</span><span class="sxs-lookup"><span data-stu-id="632f7-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="632f7-155">Název složky *SolutionFiles*.</span><span class="sxs-lookup"><span data-stu-id="632f7-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="632f7-156">V nové složce vytvořte stránku HTML s názvem *aplikace\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="632f7-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="632f7-157">Nahraďte existující obsah následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="632f7-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="632f7-158">Můžete zkopírovat *aplikace\_offline.htm* souboru k webu pomocí připojení k serveru FTP nebo **Správce souborů** nástroj v Ovládacích panelech poskytovatele hostingu.</span><span class="sxs-lookup"><span data-stu-id="632f7-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="632f7-159">Pro účely tohoto kurzu budete používat **Správce souborů**.</span><span class="sxs-lookup"><span data-stu-id="632f7-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="632f7-160">Otevřete ovládací panely a vyberte **Správce souborů** jako jste to udělali [nasazení do produkčního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) kurzu.</span><span class="sxs-lookup"><span data-stu-id="632f7-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="632f7-161">Vyberte **contosouniversity.com** a potom **wwwroot** získat do kořenové složky vaší aplikace, a potom klikněte na **nahrát**.</span><span class="sxs-lookup"><span data-stu-id="632f7-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

[![U<span data-ttu-id="632f7-162">pload_button_in_File_Manager]</span><span class="sxs-lookup"><span data-stu-id="632f7-162">pload_button_in_File_Manager]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

<span data-ttu-id="632f7-163">V **nahrát soubor** dialogové okno, vyberte *aplikace\_offline.htm* souboru a pak klikněte na tlačítko **nahrát**.</span><span class="sxs-lookup"><span data-stu-id="632f7-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

[![U<span data-ttu-id="632f7-164">pload_dialog_box_in_File_Manager]</span><span class="sxs-lookup"><span data-stu-id="632f7-164">pload_dialog_box_in_File_Manager]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

<span data-ttu-id="632f7-165">Přejděte na adresu URL vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="632f7-165">Browse to your site's URL.</span></span> <span data-ttu-id="632f7-166">Uvidíte, že *aplikace\_offline.htm* stránky se nyní zobrazí místo domovské stránky.</span><span class="sxs-lookup"><span data-stu-id="632f7-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

[![A<span data-ttu-id="632f7-167">pp_offline.htm_page_in_production]</span><span class="sxs-lookup"><span data-stu-id="632f7-167">pp_offline.htm_page_in_production]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

<span data-ttu-id="632f7-168">Nyní jste připraveni k nasazení do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="632f7-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="632f7-169">Nasazení aktualizace kódu do produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="632f7-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="632f7-170">V **publikování webu jedním kliknutím** nástrojů, zvolte **produkční** profil publikování a pak klikněte na tlačítko **Publikovat Web**.</span><span class="sxs-lookup"><span data-stu-id="632f7-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="632f7-171">Visual Studio nasadí aktualizované aplikace a otevře prohlížeč na domovské stránce webu.</span><span class="sxs-lookup"><span data-stu-id="632f7-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="632f7-172">*Aplikace\_offline.htm* soubor se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="632f7-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="632f7-173">Předtím, než můžete otestovat a ověřit úspěšné nasazení, je nutné odebrat *aplikace\_offline.htm* souboru.</span><span class="sxs-lookup"><span data-stu-id="632f7-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="632f7-174">Vraťte se **Správce souborů** aplikace v Ovládacích panelech.</span><span class="sxs-lookup"><span data-stu-id="632f7-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="632f7-175">Vyberte **contosouniversity.com** a **wwwroot**vyberte **aplikace\_offline.htm**a potom klikněte na tlačítko **odstranit**.</span><span class="sxs-lookup"><span data-stu-id="632f7-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

[![D<span data-ttu-id="632f7-176">eleting_app_offline.htm]</span><span class="sxs-lookup"><span data-stu-id="632f7-176">eleting_app_offline.htm]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

<span data-ttu-id="632f7-177">V prohlížeči otevřete stránku školitelů v na veřejném webu a vyberte instruktorem k ověření, že se aktualizace úspěšně nasadilo.</span><span class="sxs-lookup"><span data-stu-id="632f7-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

[![I<span data-ttu-id="632f7-178">nstructors_page_with_courses_Prod]</span><span class="sxs-lookup"><span data-stu-id="632f7-178">nstructors_page_with_courses_Prod]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

<span data-ttu-id="632f7-179">Nyní jste nasadili aktualizaci aplikace, která neobsahovala Změna databáze.</span><span class="sxs-lookup"><span data-stu-id="632f7-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="632f7-180">V dalším kurzu se dozvíte, jak nasadit databázi změnit.</span><span class="sxs-lookup"><span data-stu-id="632f7-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="632f7-181">[Předchozí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [další](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="632f7-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
