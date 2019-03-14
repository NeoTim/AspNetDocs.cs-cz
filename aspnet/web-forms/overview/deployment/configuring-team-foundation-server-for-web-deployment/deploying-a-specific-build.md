---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: Nasazení konkrétního sestavení | Dokumentace Microsoftu
author: jrjlee
description: Toto téma popisuje postup nasazení webových balíčků a databázové skripty z konkrétního předchozí sestavení na nové umístění, jako je pracovní nebo produkční enviro...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: e788f02795fc83ac98c5a0ba307f16b0f506e489
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077314"
---
<a name="deploying-a-specific-build"></a><span data-ttu-id="8027f-103">Nasazení konkrétního sestavení</span><span class="sxs-lookup"><span data-stu-id="8027f-103">Deploying a Specific Build</span></span>
====================
<span data-ttu-id="8027f-104">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8027f-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8027f-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="8027f-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8027f-106">Toto téma popisuje postup nasazení webových balíčků a databázové skripty z konkrétního předchozí sestavení na nové umístění, jako jsou testovací nebo produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="8027f-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>


<span data-ttu-id="8027f-107">Toto téma je součástí série kurzů podle požadavků na nasazení enterprise fiktivní společnosti s názvem společnosti Fabrikam, Inc. V této sérii kurzů používá ukázkové řešení&#x2014; [řešení Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;představující webovou aplikaci s realistické úroveň složitosti, včetně aplikace ASP.NET MVC 3, komunikace Windows Služba Foundation (WCF) a databázový projekt.</span><span class="sxs-lookup"><span data-stu-id="8027f-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="8027f-108">Metody nasazení v srdci těchto kurzů je založen na rozdělení přístupu soubor projektu je popsáno v [vysvětlení souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je řízena procesem sestavení a nasazení dva soubory projektu&#x2014;jeden obsahuje pokyny pro sestavení, které platí pro všechny cílové prostředí a jeden obsahuje nastavení pro konkrétní prostředí sestavení a nasazení.</span><span class="sxs-lookup"><span data-stu-id="8027f-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="8027f-109">V okamžiku sestavení souboru projektu specifických pro prostředí se sloučí do souboru projektu bez ohledu na prostředí a vytvoří kompletní sadu pokynů sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="8027f-110">Přehled úloh</span><span class="sxs-lookup"><span data-stu-id="8027f-110">Task Overview</span></span>

<span data-ttu-id="8027f-111">Až doteď témata v této sérii kurzů zaměřené na tom, jak sestavit, balení a nasazení webových aplikací a databází v rámci jednoho kroku nebo automatizovat proces.</span><span class="sxs-lookup"><span data-stu-id="8027f-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="8027f-112">Ale v některé běžné scénáře, třeba vyberte prostředky, které nasadíte ze seznamu sestavení v odkládací složce.</span><span class="sxs-lookup"><span data-stu-id="8027f-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="8027f-113">Jinými slovy nejnovějšího buildu nemusí být sestavení, které chcete nasadit.</span><span class="sxs-lookup"><span data-stu-id="8027f-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="8027f-114">Vezměte v úvahu scénář kontinuální integrace (CI) je popsáno v předchozím tématu [vytvoření sestavení definice, že podporuje nasazení](creating-a-build-definition-that-supports-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8027f-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="8027f-115">Vytvořili jste definici sestavení v Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="8027f-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="8027f-116">Pokaždé, když vývojář kontroluje kód do TFS, Team Build se vytváření kódu, vytváření balíčků pro webové a databázové skripty jako součást procesu sestavení, spuštění všech testů jednotek a nasadit prostředky do testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="8027f-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="8027f-117">V závislosti na zásady uchovávání informací, které jste nakonfigurovali při vytváření definice sestavení si zachovají TFS určitého počtu předchozích sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="8027f-118">Nyní předpokládejme, že jste provedli ověření a ověřovací testování s některou z těchto sestavení v testovacím prostředí a jste připraveni nasadit aplikaci do přípravného prostředí.</span><span class="sxs-lookup"><span data-stu-id="8027f-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="8027f-119">Do té doby vývojáři mohou se změnami nový kód.</span><span class="sxs-lookup"><span data-stu-id="8027f-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="8027f-120">Nechcete, aby znovu sestavte řešení a nasazení do přípravného prostředí a nechcete, aby k nasazení na nejnovější verzi do přípravného prostředí.</span><span class="sxs-lookup"><span data-stu-id="8027f-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="8027f-121">Místo toho kterou chcete nasadit konkrétní sestavení, které jste ověření a ověření na testovacích serverech.</span><span class="sxs-lookup"><span data-stu-id="8027f-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="8027f-122">K tomu budete muset zjistit Microsoft Build Engine (MSBuild), kde najdete balíčky webové a databázové skripty, které generují konkrétního sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="8027f-123">Přepisování vlastnosti OutputRoot</span><span class="sxs-lookup"><span data-stu-id="8027f-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="8027f-124">V [ukázkové řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), *Publish.proj* souboru deklaruje vlastnost s názvem **OutputRoot**.</span><span class="sxs-lookup"><span data-stu-id="8027f-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="8027f-125">Jak název napovídá, to je kořenová složka, která obsahuje všechno, co se generuje procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="8027f-126">V *Publish.proj* souboru, můžete zobrazit, který **OutputRoot** vlastnost odkazuje na kořenový adresář pro všechny prostředky pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="8027f-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="8027f-127">**OutputRoot** je běžně používaný vlastnost název.</span><span class="sxs-lookup"><span data-stu-id="8027f-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="8027f-128">Soubory Visual C# a Visual Basic projektu tuto vlastnost k uložení umístění kořenového adresáře pro všechna výstupní sestavení také deklarovat.</span><span class="sxs-lookup"><span data-stu-id="8027f-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


<span data-ttu-id="8027f-129">Pokud chcete, aby váš soubor projektu pro nasazení webových balíčků a databázové skripty z jiného umístění&#x2014;výstupy předchozích sestavení TFS, jako jsou&#x2014;jednoduše je potřeba přepsat **OutputRoot** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="8027f-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="8027f-130">Do složky relevantní sestavení byste měli nastavit hodnotu vlastnosti na serveru Team Build.</span><span class="sxs-lookup"><span data-stu-id="8027f-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="8027f-131">Pokud jste používali nástroj MSBuild z příkazového řádku, můžete zadat hodnotu pro **OutputRoot** jako argument příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="8027f-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


<span data-ttu-id="8027f-132">V praxi, ale také chcete přeskočit **sestavení** cílové&#x2014;neexistuje bod v sestavení vašeho řešení, pokud nemáte v úmyslu použít výstupy sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="8027f-133">Může to provedete tak, že určíte cíle, které chcete spustit z příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="8027f-133">You could do this by specifying the targets you want to execute from the command line:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


<span data-ttu-id="8027f-134">Ale ve většině případů budete chtít vytvořit svoji logiku nasazení do definice sestavení TFS.</span><span class="sxs-lookup"><span data-stu-id="8027f-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="8027f-135">To umožňuje uživatelům s **zařazovat sestavení do fronty** oprávnění k aktivaci nasazení z jakékoli instalaci sady Visual Studio s připojením k serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="8027f-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="8027f-136">Vytvoření definice sestavení pro nasazení konkrétní sestavení</span><span class="sxs-lookup"><span data-stu-id="8027f-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="8027f-137">Následující postup popisuje, jak vytvořit definici sestavení, která umožňuje uživatelům aktivační události nasazení do přípravného prostředí pomocí jediného příkazu.</span><span class="sxs-lookup"><span data-stu-id="8027f-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="8027f-138">V takovém případě nechcete, aby definice sestavení nic sestavit&#x2014;je vhodné ji ke spuštění v souboru projektu vlastní logiku nasazení.</span><span class="sxs-lookup"><span data-stu-id="8027f-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="8027f-139">*Publish.proj* soubor obsahuje podmíněnou logiku, který přeskočí **sestavení** cílit, pokud soubor běží ve službě Team Build.</span><span class="sxs-lookup"><span data-stu-id="8027f-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="8027f-140">Dělá to tak, že vyhodnocení vestavěných **BuildingInTeamBuild** vlastnost, která se automaticky nastaví na **true** při spuštění souboru projektu v Team Build.</span><span class="sxs-lookup"><span data-stu-id="8027f-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="8027f-141">V důsledku toho můžete přeskočit procesu sestavení a spusťte soubor projektu a nasazení existujícího sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="8027f-142">**Chcete-li vytvořit definici sestavení k ruční aktivaci nasazení**</span><span class="sxs-lookup"><span data-stu-id="8027f-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="8027f-143">V sadě Visual Studio 2010 v **Team Exploreru** okna, rozbalte uzel týmového projektu, klikněte pravým tlačítkem na **sestavení**a potom klikněte na tlačítko **nová definice sestavení**.</span><span class="sxs-lookup"><span data-stu-id="8027f-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="8027f-144">Na **Obecné** kartu, zadejte název definice sestavení (například **DeployToStaging**) a volitelně také popis.</span><span class="sxs-lookup"><span data-stu-id="8027f-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="8027f-145">Na **aktivační událost** kartu, vyberte možnost **manuálně – vrácení se změnami nespouštějí nového sestavení**.</span><span class="sxs-lookup"><span data-stu-id="8027f-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="8027f-146">Na **výchozí hodnoty sestavení** kartě **Kopírovat výstup sestavení na následující odkládací složky** zadejte cestu (Universal Naming Convention) odkládací složky (například  **\\TFSBUILD\Drops**).</span><span class="sxs-lookup"><span data-stu-id="8027f-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="8027f-147">Na **procesu** kartě **soubor procesu sestavení** rozevíracího seznamu, ponechejte tuto položku **DefaultTemplate.xaml** vybrané.</span><span class="sxs-lookup"><span data-stu-id="8027f-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="8027f-148">Toto je jedna z výchozích šablon procesů sestavení, které se přidají do všech nových týmových projektů.</span><span class="sxs-lookup"><span data-stu-id="8027f-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="8027f-149">V **parametry procesu sestavení** tabulku, klikněte na tlačítko v **položky k sestavení** řádku a potom klikněte na tlačítko **tlačítko se třemi tečkami** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="8027f-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="8027f-150">V **položky k sestavení** dialogové okno, klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="8027f-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="8027f-151">V **položky typu** rozevíracího seznamu vyberte **soubory projektu MSBuild**.</span><span class="sxs-lookup"><span data-stu-id="8027f-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="8027f-152">Přejděte do umístění souboru vlastních projektů, pomocí kterého řízení procesu nasazení, vyberte ho a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="8027f-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="8027f-153">V **položky k sestavení** dialogové okno, klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="8027f-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="8027f-154">V **parametry procesu sestavení** tabulky, rozbalte **Upřesnit** oddílu.</span><span class="sxs-lookup"><span data-stu-id="8027f-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="8027f-155">V **argumenty nástroje MSBuild** řádek, zadejte umístění vašeho souboru projektu pro konkrétní prostředí a přidáte zástupný symbol pro umístění složky sestavení:</span><span class="sxs-lookup"><span data-stu-id="8027f-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="8027f-156">Je potřeba přepsat **OutputRoot** hodnotu pokaždé, když se zařadit sestavení do fronty.</span><span class="sxs-lookup"><span data-stu-id="8027f-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="8027f-157">Je to popsané v dalším postupu.</span><span class="sxs-lookup"><span data-stu-id="8027f-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="8027f-158">Klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="8027f-158">Click **Save**.</span></span>

<span data-ttu-id="8027f-159">Po aktivaci sestavení, je potřeba aktualizovat **OutputRoot** vlastnost tak, aby odkazoval na sestavení, které chcete nasadit.</span><span class="sxs-lookup"><span data-stu-id="8027f-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="8027f-160">**K nasazení konkrétního sestavení z definice sestavení**</span><span class="sxs-lookup"><span data-stu-id="8027f-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="8027f-161">V **Team Exploreru** okna, klikněte pravým tlačítkem na definici sestavení a pak klikněte na tlačítko **zařadit nové sestavení**.</span><span class="sxs-lookup"><span data-stu-id="8027f-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="8027f-162">V **zařadit sestavení do fronty** dialogovém okně **parametry** kartu, rozbalte **Upřesnit** oddílu.</span><span class="sxs-lookup"><span data-stu-id="8027f-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="8027f-163">V **argumenty nástroje MSBuild** řádek, nahraďte hodnotu **OutputRoot** vlastnost umístění složky sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="8027f-164">Příklad:</span><span class="sxs-lookup"><span data-stu-id="8027f-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="8027f-165">Nezapomeňte zahrnout adresy koncové lomítko na konci cesty ke složce sestavení.</span><span class="sxs-lookup"><span data-stu-id="8027f-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="8027f-166">Klikněte na tlačítko **fronty**.</span><span class="sxs-lookup"><span data-stu-id="8027f-166">Click **Queue**.</span></span>

<span data-ttu-id="8027f-167">Při vložení sestavení do fronty, soubor projektu bude nasazení databázové skripty a webových balíčků ze složky pro přetažení sestavení, kterou jste zadali v **OutputRoot** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="8027f-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8027f-168">Závěr</span><span class="sxs-lookup"><span data-stu-id="8027f-168">Conclusion</span></span>

<span data-ttu-id="8027f-169">Toto téma popisuje, jak chcete publikovat nasazení prostředky, jako jsou webové balíčky a skripty databáze, z konkrétní předchozí sestavení pomocí modelu nasazení souboru projektu rozdělení.</span><span class="sxs-lookup"><span data-stu-id="8027f-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="8027f-170">Vysvětlení postupu přepsání **OutputRoot** definice sestavení pro vlastnost a tom, jak začlenit logiky nasazení do TFS.</span><span class="sxs-lookup"><span data-stu-id="8027f-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8027f-171">Další čtení</span><span class="sxs-lookup"><span data-stu-id="8027f-171">Further Reading</span></span>

<span data-ttu-id="8027f-172">Další informace o vytvoření definice sestavení, naleznete v tématu [vytvořit a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) a [definovat svůj proces sestavení](https://msdn.microsoft.com/library/ms181715.aspx).</span><span class="sxs-lookup"><span data-stu-id="8027f-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="8027f-173">Další pokyny k řazení sestavení do fronty, naleznete v tématu [zařadit sestavení do fronty](https://msdn.microsoft.com/library/ms181722.aspx).</span><span class="sxs-lookup"><span data-stu-id="8027f-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8027f-174">[Předchozí](creating-a-build-definition-that-supports-deployment.md)
> [další](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="8027f-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
