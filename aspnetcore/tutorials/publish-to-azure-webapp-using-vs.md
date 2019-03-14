---
title: Publikování aplikace ASP.NET Core do Azure pomocí sady Visual Studio
author: rick-anderson
description: Zjistěte, jak publikovat aplikace ASP.NET Core do služby Azure App Service pomocí sady Visual Studio.
ms.author: riande
ms.custom: mvc
ms.date: 12/06/2018
uid: tutorials/publish-to-azure-webapp-using-vs
ms.openlocfilehash: e71cb8badbbc852685c845e6bbb0bbb12ab5499f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075391"
---
# <a name="publish-an-aspnet-core-app-to-azure-with-visual-studio"></a><span data-ttu-id="985a7-103">Publikování aplikace ASP.NET Core do Azure pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="985a7-103">Publish an ASP.NET Core app to Azure with Visual Studio</span></span>

<span data-ttu-id="985a7-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesarovi Blum Silveira](https://github.com/cesarbs)</span><span class="sxs-lookup"><span data-stu-id="985a7-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs)</span></span>

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

<span data-ttu-id="985a7-105">Zobrazit [publikovat do Azure ze sady Visual Studio pro Mac](https://blog.xamarin.com/publish-azure-visual-studio-mac/) Pokud pracujete v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="985a7-105">See [Publish to Azure from Visual Studio for Mac](https://blog.xamarin.com/publish-azure-visual-studio-mac/) if you are working on macOS.</span></span>

<span data-ttu-id="985a7-106">Poradce při potížích chybu nasazení služby App Service, najdete v článku <xref:host-and-deploy/azure-apps/troubleshoot>.</span><span class="sxs-lookup"><span data-stu-id="985a7-106">To troubleshoot an App Service deployment issue, see <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>

## <a name="set-up"></a><span data-ttu-id="985a7-107">Nastavení</span><span class="sxs-lookup"><span data-stu-id="985a7-107">Set up</span></span>

* <span data-ttu-id="985a7-108">Otevřít [bezplatný účet Azure](https://azure.microsoft.com/free/dotnet/) pokud ho nemáte.</span><span class="sxs-lookup"><span data-stu-id="985a7-108">Open a [free Azure account](https://azure.microsoft.com/free/dotnet/) if you don't have one.</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="985a7-109">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="985a7-109">Create a web app</span></span>

<span data-ttu-id="985a7-110">V aplikaci Visual Studio úvodní stránky, vyberte **soubor > Nový > projekt...**</span><span class="sxs-lookup"><span data-stu-id="985a7-110">In the Visual Studio Start Page, select **File > New > Project...**</span></span>

![nabídka Soubor](publish-to-azure-webapp-using-vs/_static/file_new_project.png)

<span data-ttu-id="985a7-112">Dokončení **nový projekt** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="985a7-112">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="985a7-113">V levém podokně vyberte **.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="985a7-113">In the left pane, select **.NET Core**.</span></span>
* <span data-ttu-id="985a7-114">V prostředním podokně vyberte **webové aplikace ASP.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="985a7-114">In the center pane, select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="985a7-115">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="985a7-115">Select **OK**.</span></span>

![Dialogové okno nového projektu](publish-to-azure-webapp-using-vs/_static/new_prj.png)

<span data-ttu-id="985a7-117">V **nová webová aplikace ASP.NET Core** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="985a7-117">In the **New ASP.NET Core Web Application** dialog:</span></span>

* <span data-ttu-id="985a7-118">Vyberte **webovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="985a7-118">Select **Web Application**.</span></span>
* <span data-ttu-id="985a7-119">Vyberte **změnit ověřování**.</span><span class="sxs-lookup"><span data-stu-id="985a7-119">Select **Change Authentication**.</span></span>

![Dialogové okno nového projektu](publish-to-azure-webapp-using-vs/_static/new_prj_2.png)

<span data-ttu-id="985a7-121">**Změna ověřování** se zobrazí dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="985a7-121">The **Change Authentication** dialog appears.</span></span> 

* <span data-ttu-id="985a7-122">Vyberte **jednotlivých uživatelských účtů**.</span><span class="sxs-lookup"><span data-stu-id="985a7-122">Select **Individual User Accounts**.</span></span>
* <span data-ttu-id="985a7-123">Vyberte **OK** se vrátíte **nová webová aplikace ASP.NET Core**a pak vyberte **OK** znovu.</span><span class="sxs-lookup"><span data-stu-id="985a7-123">Select **OK** to return to the **New ASP.NET Core Web Application**, then select **OK** again.</span></span>

![Nové dialogové okno ověřování webové aplikace ASP.NET Core](publish-to-azure-webapp-using-vs/_static/new_prj_auth.png) 

<span data-ttu-id="985a7-125">Visual Studio vytvoří řešení.</span><span class="sxs-lookup"><span data-stu-id="985a7-125">Visual Studio creates the solution.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="985a7-126">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="985a7-126">Run the app</span></span>

* <span data-ttu-id="985a7-127">Stiskněte kombinaci kláves CTRL + F5 ke spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="985a7-127">Press CTRL+F5 to run the project.</span></span>
* <span data-ttu-id="985a7-128">Test **o** a **kontakt** odkazy.</span><span class="sxs-lookup"><span data-stu-id="985a7-128">Test the **About** and **Contact** links.</span></span>

![Otevření webové aplikace v Microsoft Edge na místního hostitele](publish-to-azure-webapp-using-vs/_static/show.png)

### <a name="register-a-user"></a><span data-ttu-id="985a7-130">Registrace uživatele</span><span class="sxs-lookup"><span data-stu-id="985a7-130">Register a user</span></span>

* <span data-ttu-id="985a7-131">Vyberte **zaregistrovat** a registraci nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="985a7-131">Select **Register** and register a new user.</span></span> <span data-ttu-id="985a7-132">Můžete použít fiktivní e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="985a7-132">You can use a fictitious email address.</span></span> <span data-ttu-id="985a7-133">Když odešlete, na stránce se zobrazí následující chyba:</span><span class="sxs-lookup"><span data-stu-id="985a7-133">When you submit, the page displays the following error:</span></span>

    <span data-ttu-id="985a7-134">*"Vnitřní chyba serveru: Databázová operace selhala při zpracování požadavku. Výjimka SQL: Nejde otevřít databázi. Použití existující migrace pro kontext databáze aplikace může tento problém vyřešit."*</span><span class="sxs-lookup"><span data-stu-id="985a7-134">*"Internal Server Error: A database operation failed while processing the request. SQL exception: Cannot open the database. Applying existing migrations for Application DB context may resolve this issue."*</span></span>
* <span data-ttu-id="985a7-135">Vyberte **použít migrace** a jakmile se aktualizace stránky, aktualizujte stránku.</span><span class="sxs-lookup"><span data-stu-id="985a7-135">Select **Apply Migrations** and, once the page updates, refresh the page.</span></span>

![Vnitřní chyba serveru: Databázová operace selhala při zpracování požadavku.](publish-to-azure-webapp-using-vs/_static/mig.png)

<span data-ttu-id="985a7-139">Aplikace zobrazí e-mail použitý k registraci nového uživatele a **Odhlásit** odkaz.</span><span class="sxs-lookup"><span data-stu-id="985a7-139">The app displays the email used to register the new user and a **Log out** link.</span></span>

![Webová aplikace otevřít v Microsoft Edge.](publish-to-azure-webapp-using-vs/_static/hello.png)

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="985a7-142">Nasazení aplikace do Azure</span><span class="sxs-lookup"><span data-stu-id="985a7-142">Deploy the app to Azure</span></span>

<span data-ttu-id="985a7-143">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **publikování...** .</span><span class="sxs-lookup"><span data-stu-id="985a7-143">Right-click on the project in Solution Explorer and select **Publish...**.</span></span>

![Kontextová nabídka otevřít se zvýrazněným odkazem publikovat](publish-to-azure-webapp-using-vs/_static/pub.png)

<span data-ttu-id="985a7-145">V **publikovat** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="985a7-145">In the **Publish** dialog:</span></span>

* <span data-ttu-id="985a7-146">Vyberte **služby Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="985a7-146">Select **Microsoft Azure App Service**.</span></span>
* <span data-ttu-id="985a7-147">Vyberte ikonu ozubeného kola a pak vyberte **vytvořit profil**.</span><span class="sxs-lookup"><span data-stu-id="985a7-147">Select the gear icon and then select **Create Profile**.</span></span>
* <span data-ttu-id="985a7-148">Vyberte **vytvořit profil**.</span><span class="sxs-lookup"><span data-stu-id="985a7-148">Select **Create Profile**.</span></span>

![Dialogové okno pro publikování](publish-to-azure-webapp-using-vs/_static/maas1.png)

### <a name="create-azure-resources"></a><span data-ttu-id="985a7-150">Vytvoření prostředků Azure</span><span class="sxs-lookup"><span data-stu-id="985a7-150">Create Azure resources</span></span>

<span data-ttu-id="985a7-151">**Vytvořit službu App Service** se zobrazí dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="985a7-151">The **Create App Service** dialog appears:</span></span>

* <span data-ttu-id="985a7-152">Zadejte vaše předplatné.</span><span class="sxs-lookup"><span data-stu-id="985a7-152">Enter your subscription.</span></span>
* <span data-ttu-id="985a7-153">**Název aplikace**, **skupiny prostředků**, a **plán služby App Service** zaplnění vstupní pole.</span><span class="sxs-lookup"><span data-stu-id="985a7-153">The **App Name**, **Resource Group**, and **App Service Plan** entry fields are populated.</span></span> <span data-ttu-id="985a7-154">Můžete ponechat tyto názvy nebo je změnit.</span><span class="sxs-lookup"><span data-stu-id="985a7-154">You can keep these names or change them.</span></span>

![Dialogové okno služby App Service](publish-to-azure-webapp-using-vs/_static/newrg1.png)

* <span data-ttu-id="985a7-156">Vyberte **služby** kartu a vytvořte novou databázi.</span><span class="sxs-lookup"><span data-stu-id="985a7-156">Select the **Services** tab to create a new database.</span></span>

* <span data-ttu-id="985a7-157">Vyberte zelené **+** ikonu pro vytvoření nové databáze SQL</span><span class="sxs-lookup"><span data-stu-id="985a7-157">Select the green **+** icon to create a new SQL Database</span></span>

![Nová databáze SQL](publish-to-azure-webapp-using-vs/_static/sql.png)

* <span data-ttu-id="985a7-159">Vyberte **nové...**  na **konfigurace služby SQL Database** dialogové okno pro vytvoření nové databáze.</span><span class="sxs-lookup"><span data-stu-id="985a7-159">Select **New...** on the **Configure SQL Database** dialog to create a new database.</span></span>

![Nová databáze SQL a server](publish-to-azure-webapp-using-vs/_static/conf.png)

<span data-ttu-id="985a7-161">**Nakonfigurujte systém SQL Server** se zobrazí dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="985a7-161">The **Configure SQL Server** dialog appears.</span></span>

* <span data-ttu-id="985a7-162">Zadejte uživatelské jméno správce a heslo a pak vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="985a7-162">Enter an administrator user name and password, and then select **OK**.</span></span> <span data-ttu-id="985a7-163">Můžete ponechat výchozí **název serveru**.</span><span class="sxs-lookup"><span data-stu-id="985a7-163">You can keep the default **Server Name**.</span></span> 

> [!NOTE]
> <span data-ttu-id="985a7-164">"admin" není povolen jako uživatelské jméno správce.</span><span class="sxs-lookup"><span data-stu-id="985a7-164">"admin" isn't allowed as the administrator user name.</span></span>

![Konfigurace systému SQL Server dialogového okna](publish-to-azure-webapp-using-vs/_static/conf_servername.png)

* <span data-ttu-id="985a7-166">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="985a7-166">Select **OK**.</span></span>

<span data-ttu-id="985a7-167">Vrátí sady Visual Studio **vytvořit službu App Service** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="985a7-167">Visual Studio returns to the **Create App Service** dialog.</span></span>

* <span data-ttu-id="985a7-168">Vyberte **vytvořit** na **vytvořit službu App Service** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="985a7-168">Select **Create** on the **Create App Service** dialog.</span></span>

![Konfigurace SQL Database dialogového okna](publish-to-azure-webapp-using-vs/_static/conf_final.png)

<span data-ttu-id="985a7-170">Visual Studio vytvoří webovou aplikaci a SQL Server v Azure.</span><span class="sxs-lookup"><span data-stu-id="985a7-170">Visual Studio creates the Web app and SQL Server on Azure.</span></span> <span data-ttu-id="985a7-171">Tento krok může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="985a7-171">This step can take a few minutes.</span></span> <span data-ttu-id="985a7-172">Informace o prostředky vytvořené v tématu [další prostředky](#additonal-resources).</span><span class="sxs-lookup"><span data-stu-id="985a7-172">For information on the resources created, see [Additional resources](#additonal-resources).</span></span>

<span data-ttu-id="985a7-173">Po dokončení nasazení vyberte **nastavení**:</span><span class="sxs-lookup"><span data-stu-id="985a7-173">When deployment completes, select **Settings**:</span></span>

![Konfigurace systému SQL Server dialogového okna](publish-to-azure-webapp-using-vs/_static/set.png)

<span data-ttu-id="985a7-175">Na **nastavení** stránku **publikovat** dialogové okno:</span><span class="sxs-lookup"><span data-stu-id="985a7-175">On the **Settings** page of the **Publish** dialog:</span></span>

  * <span data-ttu-id="985a7-176">Rozbalte **databází** a zkontrolujte **použít tento připojovací řetězec za běhu**.</span><span class="sxs-lookup"><span data-stu-id="985a7-176">Expand **Databases** and check **Use this connection string at runtime**.</span></span>
  * <span data-ttu-id="985a7-177">Rozbalte **migrace rozhraní Entity Framework** a zkontrolujte **použít tuto migraci na publikování**.</span><span class="sxs-lookup"><span data-stu-id="985a7-177">Expand **Entity Framework Migrations** and check **Apply this migration on publish**.</span></span>

* <span data-ttu-id="985a7-178">Vyberte **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="985a7-178">Select **Save**.</span></span> <span data-ttu-id="985a7-179">Vrátí sady Visual Studio **publikovat** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="985a7-179">Visual Studio returns to the **Publish** dialog.</span></span> 

![Dialogové okno pro publikování: Panel nastavení](publish-to-azure-webapp-using-vs/_static/pubs.png)

<span data-ttu-id="985a7-181">Klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="985a7-181">Click **Publish**.</span></span> <span data-ttu-id="985a7-182">Visual Studio publikuje vaši aplikaci do Azure.</span><span class="sxs-lookup"><span data-stu-id="985a7-182">Visual Studio publishes your app to Azure.</span></span> <span data-ttu-id="985a7-183">Po dokončení nasazení aplikace se otevře v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="985a7-183">When the deployment completes, the app is opened in a browser.</span></span>

### <a name="test-your-app-in-azure"></a><span data-ttu-id="985a7-184">Testování aplikace v Azure</span><span class="sxs-lookup"><span data-stu-id="985a7-184">Test your app in Azure</span></span>

* <span data-ttu-id="985a7-185">Test **o** a **kontakt** odkazy</span><span class="sxs-lookup"><span data-stu-id="985a7-185">Test the **About** and **Contact** links</span></span>

* <span data-ttu-id="985a7-186">Registrace nového uživatele</span><span class="sxs-lookup"><span data-stu-id="985a7-186">Register a new user</span></span>

![Otevřít v Microsoft Edge ve službě Azure App Service webovou aplikaci](publish-to-azure-webapp-using-vs/_static/register.png)

### <a name="update-the-app"></a><span data-ttu-id="985a7-188">Aktualizace aplikace</span><span class="sxs-lookup"><span data-stu-id="985a7-188">Update the app</span></span>

* <span data-ttu-id="985a7-189">Upravit *Pages/About.cshtml* Razor stránce a změňte jeho obsah.</span><span class="sxs-lookup"><span data-stu-id="985a7-189">Edit the *Pages/About.cshtml* Razor page and change its contents.</span></span> <span data-ttu-id="985a7-190">Například můžete upravit odstavec říct "Dobrý den ASP.NET Core!":</span><span class="sxs-lookup"><span data-stu-id="985a7-190">For example, you can modify the paragraph to say "Hello ASP.NET Core!":</span></span>

    [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]

* <span data-ttu-id="985a7-191">Klikněte pravým tlačítkem na projekt a vyberte **publikování...**  znovu.</span><span class="sxs-lookup"><span data-stu-id="985a7-191">Right-click on the project and select **Publish...** again.</span></span>

![Kontextová nabídka otevřít se zvýrazněným odkazem publikovat](publish-to-azure-webapp-using-vs/_static/pub.png)

* <span data-ttu-id="985a7-193">Po publikování aplikace, ověřte, zda jsou k dispozici v Azure, provedené změny.</span><span class="sxs-lookup"><span data-stu-id="985a7-193">After the app is published, verify the changes you made are available on Azure.</span></span>

![Ověřte, zda je úkol dokončený](publish-to-azure-webapp-using-vs/_static/final.png)

### <a name="clean-up"></a><span data-ttu-id="985a7-195">Vyčištění</span><span class="sxs-lookup"><span data-stu-id="985a7-195">Clean up</span></span>

<span data-ttu-id="985a7-196">Po dokončení testování aplikace, přejděte [webu Azure portal](https://portal.azure.com/) a odstranit ji.</span><span class="sxs-lookup"><span data-stu-id="985a7-196">When you have finished testing the app, go to the [Azure portal](https://portal.azure.com/) and delete the app.</span></span>

* <span data-ttu-id="985a7-197">Vyberte **skupiny prostředků**, pak vyberte skupinu prostředků, kterou jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="985a7-197">Select **Resource groups**, then select the resource group you created.</span></span>

![Azure Portal: Skupiny prostředků v nabídce bočního panelu](publish-to-azure-webapp-using-vs/_static/portalrg.png)

* <span data-ttu-id="985a7-199">V **skupiny prostředků** stránce **odstranit**.</span><span class="sxs-lookup"><span data-stu-id="985a7-199">In the **Resource groups** page, select **Delete**.</span></span>

![Azure Portal: Stránka s materiály pro skupiny](publish-to-azure-webapp-using-vs/_static/rgd.png)

* <span data-ttu-id="985a7-201">Zadejte název skupiny prostředků a vyberte **odstranit**.</span><span class="sxs-lookup"><span data-stu-id="985a7-201">Enter the name of the resource group and select **Delete**.</span></span> <span data-ttu-id="985a7-202">Vaše aplikace a všechny další prostředky vytvořené v tomto kurzu se teď odstraní z Azure.</span><span class="sxs-lookup"><span data-stu-id="985a7-202">Your app and all other resources created in this tutorial are now deleted from Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="985a7-203">Další kroky</span><span class="sxs-lookup"><span data-stu-id="985a7-203">Next steps</span></span>

* <xref:host-and-deploy/azure-apps/azure-continuous-deployment>

## <a name="additonal-resources"></a><span data-ttu-id="985a7-204">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="985a7-204">Additonal resources</span></span>

* [<span data-ttu-id="985a7-205">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="985a7-205">Azure App Service</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="985a7-206">Skupiny prostředků Azure</span><span class="sxs-lookup"><span data-stu-id="985a7-206">Azure resource groups</span></span>](/azure/azure-resource-manager/resource-group-overview#resource-groups)
* [<span data-ttu-id="985a7-207">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="985a7-207">Azure SQL Database</span></span>](/azure/sql-database/)
* <xref:host-and-deploy/visual-studio-publish-profiles>
* <xref:host-and-deploy/azure-apps/troubleshoot>
