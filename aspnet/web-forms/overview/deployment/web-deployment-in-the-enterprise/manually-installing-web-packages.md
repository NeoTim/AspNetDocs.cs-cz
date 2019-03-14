---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: Ruční instalace webových balíčků | Dokumentace Microsoftu
author: jrjlee
description: Toto téma popisuje, jak k ručnímu importu balíčku pro nasazení webu v Internetové informační služby (IIS). Vytváření tématu a balení webového instalováním...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: ca85db5cfb30bc06d6d3b94001a3668088461b87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068662"
---
<a name="manually-installing-web-packages"></a><span data-ttu-id="d43a9-104">Ruční instalace webových balíčků</span><span class="sxs-lookup"><span data-stu-id="d43a9-104">Manually Installing Web Packages</span></span>
====================
<span data-ttu-id="d43a9-105">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d43a9-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d43a9-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="d43a9-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d43a9-107">Toto téma popisuje, jak k ručnímu importu balíčku pro nasazení webu v Internetové informační služby (IIS).</span><span class="sxs-lookup"><span data-stu-id="d43a9-107">This topic describes how to manually import a web deployment package into Internet Information Services (IIS).</span></span>
> 
> <span data-ttu-id="d43a9-108">Téma [sestavení a balení projektů webových aplikací](building-and-packaging-web-application-projects.md) popisuje způsob, jakým služba IIS nástroj pro nasazení webu (nasazení webu), v kombinaci s Microsoft Build Engine (MSBuild) a webových publikování kanálu (WPP), umožňuje zabalit vaše projekty webových aplikací do souboru zip jeden.</span><span class="sxs-lookup"><span data-stu-id="d43a9-108">The topic [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) described how the IIS Web Deployment Tool (Web Deploy), in conjunction with the Microsoft Build Engine (MSBuild) and the Web Publishing Pipeline (WPP), lets you package your web application projects into a single zip file.</span></span> <span data-ttu-id="d43a9-109">Tento soubor, obvykle označuje jako balíčku pro nasazení webu (nebo jednoduše pomocí balíčku nasazení), obsahuje všechny obsah a konfigurační informace, že služba IIS potřebuje, aby znovu vytvořit webové aplikace na webovém serveru.</span><span class="sxs-lookup"><span data-stu-id="d43a9-109">This file, commonly known as a web deployment package (or simply a deployment package), contains all the content and configuration information that IIS needs in order to re-create your web application on a web server.</span></span>
> 
> <span data-ttu-id="d43a9-110">Po vytvoření balíčku pro nasazení webu, můžete ji publikovat na server služby IIS různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="d43a9-110">Once you've created a web deployment package, you can publish it to an IIS server in various ways.</span></span> <span data-ttu-id="d43a9-111">V možných scénářů budete chtít využít výhod bodů integrace mezi MSBuild, WPP a nasazení webu k vytvoření a instalace webových balíčků vzdáleně jako součást krokování nebo automatizovaného sestavení a nasazení procesu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-111">In a lot of scenarios, you'll want to take advantage of the integration points between MSBuild, the WPP, and Web Deploy to create and install web packages remotely as part of an automated or single-step build and deployment process.</span></span> <span data-ttu-id="d43a9-112">Tento proces je popsán v [nasazení webových balíčků](deploying-web-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-112">This process is described in [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="d43a9-113">Ale to není vždy možné.</span><span class="sxs-lookup"><span data-stu-id="d43a9-113">However, this isn't always possible.</span></span> <span data-ttu-id="d43a9-114">Předpokládejme, že chcete nasadit webovou aplikaci do produkčního prostředí přístupem k Internetu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-114">Suppose you want to deploy a web application to an Internet-facing production environment.</span></span> <span data-ttu-id="d43a9-115">Z bezpečnostních důvodů produkčním prostředí je na velmi nejméně pravděpodobně být za bránou firewall v podsíti oddělené od serveru sestavení, v hraniční síti (označované také jako DMZ, demilitarizovaná zóna a monitorovaná podsíť).</span><span class="sxs-lookup"><span data-stu-id="d43a9-115">For security reasons, such a production environment is at the very least likely to be behind a firewall on a subnet that is separate from the build server, in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet).</span></span> <span data-ttu-id="d43a9-116">V mnoha případech bude produkčního prostředí v samostatné doméně nebo fyzicky izolované sítě.</span><span class="sxs-lookup"><span data-stu-id="d43a9-116">In lots of cases, the production environment will be on a separate domain or on a physically isolated network.</span></span>
> 
> <span data-ttu-id="d43a9-117">V těchto scénářích může být vaší jedinou možností k portu webový balíček na cílový server a ji manuálně naimportovat do služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d43a9-117">In these scenarios, your only option may be to port the web package onto the destination server and manually import it into IIS.</span></span> <span data-ttu-id="d43a9-118">Přestože tento přístup vylučuje automatického nasazení, je stále vysoce efektivní technikou pro publikování webové aplikace&#x2014;jednoduše zkopírovat soubor zip jeden webový server a pomocí Průvodce vás provede procesem importu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-118">Although this approach precludes automated deployment, it's still a highly effective technique for publishing a web application&#x2014;you simply copy a single zip file to your web server and use a wizard to guide you through the import process.</span></span>


<span data-ttu-id="d43a9-119">Toto téma je součástí série kurzů podle požadavků na nasazení enterprise fiktivní společnosti s názvem společnosti Fabrikam, Inc. V této sérii kurzů používá ukázkové řešení&#x2014; [řešení Správce kontaktů](the-contact-manager-solution.md)&#x2014;představující webovou aplikaci s realistické úroveň složitosti, včetně aplikace ASP.NET MVC 3, komunikace Windows Služba Foundation (WCF) a databázový projekt.</span><span class="sxs-lookup"><span data-stu-id="d43a9-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="d43a9-120">Přehled úloh</span><span class="sxs-lookup"><span data-stu-id="d43a9-120">Task Overview</span></span>

<span data-ttu-id="d43a9-121">Budete potřebovat k dokončení těchto úloh k importu balíčku pro nasazení webu do služby IIS:</span><span class="sxs-lookup"><span data-stu-id="d43a9-121">You'll need to complete these high-level tasks to import a web deployment package into IIS:</span></span>

- <span data-ttu-id="d43a9-122">Vytvoření balíčku pro nasazení webu pomocí nástroje MSBuild příkazového řádku, Team Build nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="d43a9-122">Create a web deployment package using the MSBuild command line, Team Build, or Visual Studio 2010.</span></span>
- <span data-ttu-id="d43a9-123">Webový balíček zkopírujte na cílový webový server.</span><span class="sxs-lookup"><span data-stu-id="d43a9-123">Copy the web package to the destination web server.</span></span>
- <span data-ttu-id="d43a9-124">Pomocí Průvodce importem balíčku aplikace k instalaci balíčku webu a zadejte hodnoty pro proměnné, jako jsou připojovací řetězce a koncových bodů služby ve Správci služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d43a9-124">Use the Import Application Package Wizard in IIS Manager to install the web package and provide values for variables like connection strings and service endpoints.</span></span>

<span data-ttu-id="d43a9-125">Toto téma se ukazují, jak provést tyto postupy.</span><span class="sxs-lookup"><span data-stu-id="d43a9-125">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="d43a9-126">Úlohy a názorné postupy v tomto tématu se předpokládá, že jste již obeznámeni s principy webových balíčků, Web Deploy a WPP.</span><span class="sxs-lookup"><span data-stu-id="d43a9-126">The tasks and walkthroughs in this topic assume that you're already familiar with the concepts behind web packages, Web Deploy, and the WPP.</span></span> <span data-ttu-id="d43a9-127">Další informace najdete v tématu [sestavení a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-127">For more information, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d43a9-128">Toto téma je nejlepší použít ve spojení s [nakonfigurovat webový Server pro nasazení publikování na webu (Offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), který vysvětluje, jak nainstalovat požadované součásti a přípravě webu služby IIS k importu balíčku naimportovány.</span><span class="sxs-lookup"><span data-stu-id="d43a9-128">This topic is best used in conjunction with [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), which explains how to install the required components and prepare an IIS website for package import.</span></span>


## <a name="create-a-web-deployment-package"></a><span data-ttu-id="d43a9-129">Vytvoření balíčku pro nasazení webu</span><span class="sxs-lookup"><span data-stu-id="d43a9-129">Create a Web Deployment Package</span></span>

<span data-ttu-id="d43a9-130">První úloha je vytvoření balíčku pro nasazení webu pro projekt webové aplikace, kterou chcete nasadit.</span><span class="sxs-lookup"><span data-stu-id="d43a9-130">The first task is to create a web deployment package for the web application project you want to deploy.</span></span> <span data-ttu-id="d43a9-131">Webových balíčků můžete vytvořit mnoha různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="d43a9-131">You can create web packages in a variety of ways.</span></span>

<span data-ttu-id="d43a9-132">**Způsob 1: Vytvoření balíčku jako součást procesu sestavení pomocí sady Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="d43a9-132">**Approach 1: Create a package as part of the build process with Visual Studio**</span></span>

<span data-ttu-id="d43a9-133">Můžete nakonfigurovat projektu webové aplikace k vytvoření balíčku pro nasazení webu po každém sestavení prostřednictvím **balení/publikování webu** karty na stránkách vlastností projektu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-133">You can configure your web application project to create a web deployment package after every build through the **Package/Publish Web** tab on the project property pages.</span></span> <span data-ttu-id="d43a9-134">Tento proces je popsán v [sestavení a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-134">This process is described in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="d43a9-135">**Způsob 2: Vytvoření balíčku jako součást procesu sestavení pomocí nástroje MSBuild**</span><span class="sxs-lookup"><span data-stu-id="d43a9-135">**Approach 2: Create a package as part of the build process with MSBuild**</span></span>

<span data-ttu-id="d43a9-136">Při sestavování projektu webové aplikace s použitím přímo, MSBuild, buď prostřednictvím vlastního souboru projektu nástroje MSBuild nebo z příkazového řádku, můžete vytvořit balíček nasazení webu jako součást procesu sestavení zahrnutím **DeployOnBuild = true** a **DeployTarget = balíček** vlastnosti ve svých rukou.</span><span class="sxs-lookup"><span data-stu-id="d43a9-136">If you build your web application project by using MSBuild directly, either through a custom MSBuild project file or from the command line, you can create a web deployment package as part of the build process by including the **DeployOnBuild=true** and **DeployTarget=Package** properties in your command.</span></span> <span data-ttu-id="d43a9-137">Tento proces je popsán v [Principy procesu sestavení](understanding-the-build-process.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-137">This process is described in [Understanding the Build Process](understanding-the-build-process.md).</span></span>

<span data-ttu-id="d43a9-138">**Způsob 3: Vytvoření balíčku na vyžádání v sadě Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="d43a9-138">**Approach 3: Create a package on demand in Visual Studio**</span></span>

<span data-ttu-id="d43a9-139">Kdykoli v sadě Visual Studio 2010 můžete vytvořit balíček nasazení webu pro webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="d43a9-139">You can create a web deployment package for a web application project at any time in Visual Studio 2010.</span></span> <span data-ttu-id="d43a9-140">Chcete-li to provést, v **Průzkumníka řešení** okna, klikněte pravým tlačítkem na projekt webové aplikace a pak klikněte na tlačítko **sestavení balíčku pro nasazení**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-140">To do this, in the **Solution Explorer** window, right-click your web application project, and then click **Build Deployment Package**.</span></span>

![](manually-installing-web-packages/_static/image1.png)

<span data-ttu-id="d43a9-141">**Způsob 4: Vytvoření balíčku na vyžádání z příkazového řádku**</span><span class="sxs-lookup"><span data-stu-id="d43a9-141">**Approach 4: Create a package on demand from the command line**</span></span>

<span data-ttu-id="d43a9-142">Můžete vytvořit balíček nasazení webu z příkazového řádku vyvoláním **balíčku** cíl v projektu webové aplikace pomocí nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d43a9-142">You can create a web deployment package from the command line by invoking the **Package** target on your web application project using MSBuild.</span></span> <span data-ttu-id="d43a9-143">Příkaz by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="d43a9-143">The command should resemble this:</span></span>


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


<span data-ttu-id="d43a9-144">Podle toho, co můžete přistupovat použít, konečný výsledek je stejný.</span><span class="sxs-lookup"><span data-stu-id="d43a9-144">Whichever approach you use, the end result is the same.</span></span> <span data-ttu-id="d43a9-145">WPP vytvoří balíčku pro nasazení webu jako soubor zip, spolu s různými Podpůrné prostředky ve výstupní složce pro váš projekt webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="d43a9-145">The WPP creates a web deployment package as a zip file, together with various supporting resources, in the output folder for your web application project.</span></span>

![](manually-installing-web-packages/_static/image2.png)

<span data-ttu-id="d43a9-146">Pokud plánujete Ruční import webový balíček, budete potřebovat pouze soubor zip.</span><span class="sxs-lookup"><span data-stu-id="d43a9-146">When you're planning to import the web package manually, you require only the zip file.</span></span> <span data-ttu-id="d43a9-147">Tento soubor zkopírovat na cílový webový server a můžete začít proces importu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-147">Copy this file to your target web server and you can begin the import process.</span></span>

## <a name="import-a-web-package-into-iis"></a><span data-ttu-id="d43a9-148">Importovat webový balíček do služby IIS</span><span class="sxs-lookup"><span data-stu-id="d43a9-148">Import a Web Package into IIS</span></span>

<span data-ttu-id="d43a9-149">Následující postup slouží k importu balíčku pro nasazení webu z místního systému souborů do webu služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d43a9-149">You can use the next procedure to import a web deployment package from the local file system into an IIS website.</span></span> <span data-ttu-id="d43a9-150">Před provedením tohoto postupu, ujistěte se, že máte:</span><span class="sxs-lookup"><span data-stu-id="d43a9-150">Before you perform this procedure, ensure that you have:</span></span>

- <span data-ttu-id="d43a9-151">Zkopírovat balíčku pro nasazení webu na webový server.</span><span class="sxs-lookup"><span data-stu-id="d43a9-151">Copied the web deployment package to the web server.</span></span>
- <span data-ttu-id="d43a9-152">Nakonfigurovat webový server služby IIS pro hostování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="d43a9-152">Configured an IIS web server to host your application.</span></span>

<span data-ttu-id="d43a9-153">Další informace o konfiguraci webový server služby IIS pro podporu balíčky nasazení webu, naleznete v tématu [nakonfigurovat webový Server pro nasazení publikování na webu (Offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-153">For more information on configuring an IIS web server to support web deployment packages, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span>

<span data-ttu-id="d43a9-154">**K importu balíčku pro nasazení webu pomocí Správce služby IIS**</span><span class="sxs-lookup"><span data-stu-id="d43a9-154">**To import a web deployment package using IIS Manager**</span></span>

1. <span data-ttu-id="d43a9-155">Ve Správci služby IIS v **připojení** podokně klikněte pravým tlačítkem na váš web služby IIS, přejděte na **nasadit**a potom klikněte na tlačítko **importovat aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-155">In IIS Manager, in the **Connections** pane, right-click your IIS website, point to **Deploy**, and then click **Import Application**.</span></span>

    ![](manually-installing-web-packages/_static/image3.png)
2. <span data-ttu-id="d43a9-156">V Průvodci importem aplikace balíčku na **vyberte balíček** stránce, přejděte do umístění balíčku pro nasazení webu a pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-156">In the Import Application Package Wizard, on the **Select the Package** page, browse to the location of your web deployment package, and then click **Next**.</span></span>
3. <span data-ttu-id="d43a9-157">Na **vybrat obsah balíčku** stránce, zrušte zaškrtnutí políčka veškerý obsah, který není mají a potom klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-157">On the **Select the Contents of the Package** page, clear any content that you don't require, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="d43a9-158">V mnoha případech nemusíte chtít importovat, vše, který je součástí balíčku pro nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-158">In a lot of cases, you may not want to import everything that comes with a web deployment package.</span></span> <span data-ttu-id="d43a9-159">Například možná chcete povolit nasazení webu k nahrazení příslušné databáze.</span><span class="sxs-lookup"><span data-stu-id="d43a9-159">For example, you may not want to allow Web Deploy to replace the associated database.</span></span>  
    > <span data-ttu-id="d43a9-160">**Udělit oprávnění** položky nastavit oprávnění pro cílový systém souborů k Ujistěte se, že identita fondu aplikací přístup k fyzické složce, která ukládá obsah webu.</span><span class="sxs-lookup"><span data-stu-id="d43a9-160">The **Grant permissions** entries set permissions on the destination file system to ensure that the application pool identity can access the physical folder that stores the website content.</span></span> <span data-ttu-id="d43a9-161">Kromě toho uživatel anonymní ověřování je udělení oprávnění ke čtení do složky umožňuje aplikaci poskytovat soubory typu Multipurpose Internet Mail Extensions (MIME).</span><span class="sxs-lookup"><span data-stu-id="d43a9-161">In addition, the anonymous authentication user is granted read permission to the folder to let the application serve Multipurpose Internet Mail Extensions (MIME) type files.</span></span> <span data-ttu-id="d43a9-162">Pokud dáváte přednost, můžete odebrat tyto položky a ruční konfigurace oprávnění.</span><span class="sxs-lookup"><span data-stu-id="d43a9-162">If you prefer, you can remove these entries and configure permissions manually.</span></span>
4. <span data-ttu-id="d43a9-163">Na **zadání informací o balíčku aplikace** stránky, zadejte požadované informace.</span><span class="sxs-lookup"><span data-stu-id="d43a9-163">On the **Enter Application Package Information** page, provide the requested information.</span></span>

    ![](manually-installing-web-packages/_static/image5.png)
5. <span data-ttu-id="d43a9-164">Při vytváření webového balíčku WPP analyzuje konfiguračního souboru pro vaši aplikaci a detekuje všechny proměnné, jako jsou připojovací řetězce a koncových bodů služby.</span><span class="sxs-lookup"><span data-stu-id="d43a9-164">When you create a web package, the WPP analyzes the configuration file for your application and detects any variables, like connection strings and service endpoints.</span></span> <span data-ttu-id="d43a9-165">V tomto případě:</span><span class="sxs-lookup"><span data-stu-id="d43a9-165">In this case:</span></span>

    1. <span data-ttu-id="d43a9-166">**Cesta k aplikaci** je cesta služby IIS, ve které chcete nainstalovat aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d43a9-166">**Application Path** is the IIS path where you want to install your application.</span></span> <span data-ttu-id="d43a9-167">Toto nastavení je společné pro všechny balíčky pro nasazení, které vytvoří WPP.</span><span class="sxs-lookup"><span data-stu-id="d43a9-167">This setting is common to all deployment packages that the WPP creates.</span></span>
    2. <span data-ttu-id="d43a9-168">**Adresa koncového bodu služby ContactService** je adresa, která by aplikace měla použít pro komunikaci s nasazenou službu WCF.</span><span class="sxs-lookup"><span data-stu-id="d43a9-168">**ContactService Service Endpoint Address** is the address that the application should use to communicate with the deployed WCF service.</span></span> <span data-ttu-id="d43a9-169">Toto nastavení odpovídá položce v *web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="d43a9-169">This setting corresponds to an entry in the *web.config* file.</span></span>
    3. <span data-ttu-id="d43a9-170">První **připojovací řetězec** nastavení je připojovací řetězec, nasazení webu by měl použít k nasazení databáze přidružené k aplikaci (v tomto případě členské databáze ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="d43a9-170">The first **Connection String** setting is the connection string that Web Deploy should use to deploy the database associated with the application (in this case an ASP.NET membership database).</span></span> <span data-ttu-id="d43a9-171">Toto nastavení odpovídá nastavení na **balení/publikování kódu SQL** kartu v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d43a9-171">This setting corresponds to the setting on the **Package/Publish SQL** tab in Visual Studio.</span></span>
    4. <span data-ttu-id="d43a9-172">Druhá **připojovací řetězec** nastavení je připojovací řetězec, který bude aplikace ve skutečnosti používat pro komunikaci s databází, když je zprovozněný.</span><span class="sxs-lookup"><span data-stu-id="d43a9-172">The second **Connection String** setting is the connection string that your application will actually use to communicate with the database when it's up and running.</span></span> <span data-ttu-id="d43a9-173">To odpovídá připojovací řetězec v *web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="d43a9-173">This corresponds to a connection string entry in the *web.config* file.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d43a9-174">Další informace o odkud pochází těchto parametrů najdete v tématu [konfigurace parametrů nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-174">For more information on where these parameters come from, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md).</span></span>
6. <span data-ttu-id="d43a9-175">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-175">Click **Next**.</span></span>
7. <span data-ttu-id="d43a9-176">Pokud to není při prvním nasazení aplikace na tento web, budete vyzváni k určení, zda chcete odstranit veškerý existující obsah před instalací.</span><span class="sxs-lookup"><span data-stu-id="d43a9-176">If this is not the first time you've deployed the application to this website, you'll be prompted to specify whether you want to delete all existing content prior to installation.</span></span> <span data-ttu-id="d43a9-177">Zvolte možnost, která je vhodná pro vaše požadavky a pak klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-177">Choose the option that's appropriate for your requirements, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image6.png)
8. <span data-ttu-id="d43a9-178">Po dokončení instalace balíčku služby IIS klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="d43a9-178">When IIS has finished installing the package, click **Finish**.</span></span>

    ![](manually-installing-web-packages/_static/image7.png)

<span data-ttu-id="d43a9-179">V tomto okamžiku jste úspěšně publikovala webové aplikace do služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d43a9-179">At this point, you've successfully published your web application to IIS.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d43a9-180">Závěr</span><span class="sxs-lookup"><span data-stu-id="d43a9-180">Conclusion</span></span>

<span data-ttu-id="d43a9-181">Toto téma popisuje postup při importu balíčku pro nasazení webu na webu služby IIS pomocí Správce služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d43a9-181">This topic described how to import a web deployment package into an IIS website using IIS Manager.</span></span> <span data-ttu-id="d43a9-182">Tento přístup k publikování aplikace na webu je vhodné, pokud omezení zabezpečení nebo infrastrukturou vzdálené nasazení nemožné nebo nežádoucí.</span><span class="sxs-lookup"><span data-stu-id="d43a9-182">This approach to web application publishing is appropriate when security or infrastructure constraints make remote deployment impossible or undesirable.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d43a9-183">Další čtení</span><span class="sxs-lookup"><span data-stu-id="d43a9-183">Further Reading</span></span>

<span data-ttu-id="d43a9-184">Pokyny o tom, jak nakonfigurovat webový server služby IIS pro podporu ručním importu webového balíčku najdete v tématu [nakonfigurovat webový Server pro nasazení publikování na webu (Offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d43a9-184">For guidance on how to configure an IIS web server to support manually importing a web package, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="d43a9-185">Další obecné informace o nasazení webových balíčků naleznete v tématu [názorný postup: Nasazení webové aplikace pomocí balíčku pro nasazení webu (část 1 ze 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span><span class="sxs-lookup"><span data-stu-id="d43a9-185">For more general guidance on deploying web packages, see [Walkthrough: Deploying a Web Application Project Using a Web Deployment Package (Part 1 of 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d43a9-186">Předchozí</span><span class="sxs-lookup"><span data-stu-id="d43a9-186">Previous</span></span>](creating-and-running-a-deployment-command-file.md)