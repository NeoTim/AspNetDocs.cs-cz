---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Nasazení webové aplikace v podnikové scénáře pomocí sady Visual Studio 2010 | Dokumentace Microsoftu
author: jrjlee
description: Této sérii kurzů popisuje nástroje a techniky, které slouží k nasazování webových aplikací v různých podnikových scénářích. Vysvětluje, jak nejlépe používat...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: fa06538dcd9e087df52a76588e084a527867bf84
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077479"
---
<a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a><span data-ttu-id="5284b-104">Scénáře nasazení webových aplikací v podniku pomocí sady Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="5284b-104">Deploying Web Applications in Enterprise Scenarios using Visual Studio 2010</span></span>
====================
<span data-ttu-id="5284b-105">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="5284b-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="5284b-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="5284b-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="5284b-107">Této sérii kurzů popisuje nástroje a techniky, které slouží k nasazování webových aplikací v různých podnikových scénářích.</span><span class="sxs-lookup"><span data-stu-id="5284b-107">This set of tutorials describes tools and techniques you can use to deploy web applications in various enterprise scenarios.</span></span> <span data-ttu-id="5284b-108">Vysvětluje, jak nejlépe používat technologie, jako je Visual Studio 2010, Microsoft Build Engine (MSBuild), Internetové informační služby (IIS) 7.5, nástroj nasazení webu služby IIS (Web Deploy), webové farmy Framework (WFF) a nástroje, jako je VSDBCMD.exe do Zjednodušte a spravovat proces nasazení.</span><span class="sxs-lookup"><span data-stu-id="5284b-108">It explains how to make best use of technologies like Visual Studio 2010, the Microsoft Build Engine (MSBuild), Internet Information Services (IIS) 7.5, the IIS Web Deployment Tool (Web Deploy), the Web Farm Framework (WFF), and utilities like VSDBCMD.exe to simplify and manage the deployment process.</span></span> <span data-ttu-id="5284b-109">Obsahuje koncepční přehledy a orientovaných pokyny, které vám pomůžou:</span><span class="sxs-lookup"><span data-stu-id="5284b-109">It includes conceptual overviews and task-oriented guidance that will help you to:</span></span>
> 
> - <span data-ttu-id="5284b-110">Zkontrolujte a stanovit požadavky na nasazení pro webovou aplikaci celého podniku.</span><span class="sxs-lookup"><span data-stu-id="5284b-110">Review and establish the deployment requirements for an enterprise-scale web application.</span></span>
> - <span data-ttu-id="5284b-111">Konfigurace testu, testovací a produkční prostředí serveru webové pro podporu nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="5284b-111">Configure test, staging, and production web server environments to support web deployment.</span></span>
> - <span data-ttu-id="5284b-112">Konfigurace procesů průběžné integrace (CI) Team Foundation Server (TFS) pro podporu nasazení automatizovaných webu.</span><span class="sxs-lookup"><span data-stu-id="5284b-112">Configure Team Foundation Server (TFS) continuous integration (CI) processes to support automated web deployment.</span></span>
> - <span data-ttu-id="5284b-113">Nasazení podnikových webových aplikací do různých serverových prostředích s různými požadavky a omezení.</span><span class="sxs-lookup"><span data-stu-id="5284b-113">Deploy enterprise-scale web applications to different server environments with varying requirements and restrictions.</span></span>
> - <span data-ttu-id="5284b-114">Nasazení změny do webové aplikace, které jsou spuštěny v různých serverových prostředích.</span><span class="sxs-lookup"><span data-stu-id="5284b-114">Deploy changes to web applications that are running in different server environments.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="5284b-115">Zatímco tyto kurzy popisují použití TFS jako CI server, pokyny snadno přizpůsobit na libovolný server CI.</span><span class="sxs-lookup"><span data-stu-id="5284b-115">While these tutorials describe the use of TFS as a CI server, the guidance is easily adapted to any CI server.</span></span> <span data-ttu-id="5284b-116">Není nutné podrobnou znalost TFS k pochopení a využijte kurzy.</span><span class="sxs-lookup"><span data-stu-id="5284b-116">You don't need a detailed knowledge of TFS to understand and leverage the tutorials.</span></span>
> 
> 
> <span data-ttu-id="5284b-117">Italština překlad těchto kurzů, navštivte web [ http://www.lucamorelli.it ](http://www.lucamorelli.it).</span><span class="sxs-lookup"><span data-stu-id="5284b-117">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


## <a name="about-the-authors"></a><span data-ttu-id="5284b-118">O autorech</span><span class="sxs-lookup"><span data-stu-id="5284b-118">About the Authors</span></span>

<span data-ttu-id="5284b-119">JASON Lee je hlavní vedoucí řízení s [hlavní obsah](http://www.contentmaster.com/) kde kterých pracuje s produkty společnosti Microsoft a technologie, zejména SharePoint a technologie ASP.NET, několik let.</span><span class="sxs-lookup"><span data-stu-id="5284b-119">Jason Lee is a principal technologist with [Content Master](http://www.contentmaster.com/) where he has been working with Microsoft products and technologies, especially SharePoint and ASP.NET, for several years.</span></span> <span data-ttu-id="5284b-120">JASON obsahuje titul pH.d. ve výpočetním prostředí a je v současnosti MCPD a MCTS certified.</span><span class="sxs-lookup"><span data-stu-id="5284b-120">Jason holds a PhD in computing and is currently MCPD and MCTS certified.</span></span> <span data-ttu-id="5284b-121">Si můžete přečíst na Jason technický blog na [www.jrjlee.com](http://www.jrjlee.com/).</span><span class="sxs-lookup"><span data-stu-id="5284b-121">You can read Jason's technical blog at [www.jrjlee.com](http://www.jrjlee.com/).</span></span>

<span data-ttu-id="5284b-122">Robert kari je hlavní vedoucí řízení s [hlavní obsah](http://www.contentmaster.com/) kdo během své kariéry zapsala dokumenty White Paper, dokumentace k sadě SDK, Powerpointovými prezentacemi a školení vedených instruktorem a online kurzy.</span><span class="sxs-lookup"><span data-stu-id="5284b-122">Benjamin Curry is a principal technologist with [Content Master](http://www.contentmaster.com/) who has written whitepapers, SDK documentation, PowerPoint presentations, and instructor-led and online training courses during his career.</span></span> <span data-ttu-id="5284b-123">Původní člen týmu dokumentace technologie ASP.NET, pracoval s technologiemi web společnosti Microsoft pro víc než dekádu.</span><span class="sxs-lookup"><span data-stu-id="5284b-123">An original member of the ASP.NET documentation team, he has worked with Microsoft's web technologies for over a decade.</span></span>

## <a name="target-audience"></a><span data-ttu-id="5284b-124">Cílová skupina</span><span class="sxs-lookup"><span data-stu-id="5284b-124">Target Audience</span></span>

<span data-ttu-id="5284b-125">Této sérii kurzů je pro vývojáře webových aplikací ASP.NET a architekty řešení, kteří používají Visual Studio 2010 pro vytváření webových aplikací podnikové úrovni.</span><span class="sxs-lookup"><span data-stu-id="5284b-125">This set of tutorials is for ASP.NET web application developers and solution architects who use Visual Studio 2010 to create enterprise-scale web applications.</span></span> <span data-ttu-id="5284b-126">Chcete-li získat větší hodnotu z obsahu, by měl dobře pracovat pomocí sady Visual Studio 2010 a mít základní znalost sady TFS, společně povědomí o platformu Microsoft technologie jako je ASP.NET MVC 3, Windows Communication Foundation (WCF), služby IIS, SQL Server a databázové projekty sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5284b-126">To get the most value from the content, you should be comfortable using Visual Studio 2010 and have a basic familiarity with TFS, together with an awareness of Microsoft web platform technologies like ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL Server, and Visual Studio database projects.</span></span> <span data-ttu-id="5284b-127">Není však nutné znát nástroje a technologie nasazení nebo potřebujete vědět, jak nastavit CI systémy.</span><span class="sxs-lookup"><span data-stu-id="5284b-127">However, you do not need to be familiar with deployment tools and technologies or need to know how to set up CI systems.</span></span>

## <a name="requirements"></a><span data-ttu-id="5284b-128">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5284b-128">Requirements</span></span>

<span data-ttu-id="5284b-129">Postupujte podle návody a provádět úlohy, které popisují tyto kurzy, budete muset nainstalovat tento software ve svém vývojovém počítači:</span><span class="sxs-lookup"><span data-stu-id="5284b-129">To follow the walkthroughs and perform the tasks that these tutorials describe, you'll need to install this software on your development computer:</span></span>

- <span data-ttu-id="5284b-130">Visual Studio 2010 Premium nebo Ultimate Edition s aktualizací Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="5284b-130">Visual Studio 2010 Premium or Ultimate Edition with Service Pack 1</span></span>
- <span data-ttu-id="5284b-131">.NET Framework 4.0</span><span class="sxs-lookup"><span data-stu-id="5284b-131">.NET Framework 4.0</span></span>
- <span data-ttu-id="5284b-132">Rozhraní .NET framework 3.5 s aktualizací Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="5284b-132">.NET Framework 3.5 with Service Pack 1</span></span>
- <span data-ttu-id="5284b-133">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="5284b-133">ASP.NET MVC 3.0</span></span>
- <span data-ttu-id="5284b-134">Službu IIS 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="5284b-134">IIS 7.5 Express</span></span>
- <span data-ttu-id="5284b-135">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="5284b-135">SQL Server Express 2008 R2</span></span>

<span data-ttu-id="5284b-136">Pokud chcete provést nasazení kroků popsaných v rámci těchto návodů, budete potřebovat přístup k ukázkové webové aplikaci nasazení prostředí.</span><span class="sxs-lookup"><span data-stu-id="5284b-136">To perform the deployment steps described throughout these walkthroughs, you'll need to have access to sample Web application deployment environments.</span></span> <span data-ttu-id="5284b-137">Nejlepších výsledků dosáhnete by měly odrážet tato prostředí vaší organizace podnikové deployment vzor.</span><span class="sxs-lookup"><span data-stu-id="5284b-137">For best results, these environments should reflect your organization's enterprise deployment pattern.</span></span> <span data-ttu-id="5284b-138">Poté můžete upravit návodech uvedených v této dokumentaci tak, aby odrážely nasazení prostředí a požadavky vaší vlastní organizaci.</span><span class="sxs-lookup"><span data-stu-id="5284b-138">You can then modify the walkthroughs provided in this documentation to reflect the deployment environments and requirements of your own organization.</span></span>

## <a name="series-contents"></a><span data-ttu-id="5284b-139">Obsah řady</span><span class="sxs-lookup"><span data-stu-id="5284b-139">Series Contents</span></span>

<span data-ttu-id="5284b-140">V této úvodní části skládá ze dvou dalších tématech.</span><span class="sxs-lookup"><span data-stu-id="5284b-140">This introductory section consists of two further topics.</span></span> <span data-ttu-id="5284b-141">Ty jsou navržené k poskytnutí některých širší kontext pro kurzy, které následují:</span><span class="sxs-lookup"><span data-stu-id="5284b-141">These are designed to provide some broader context for the tutorials that follow:</span></span>

- <span data-ttu-id="5284b-142">[Nasazení podnikového webu: Přehled scénářů](enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-142">[Enterprise Web Deployment: Scenario Overview](enterprise-web-deployment-scenario-overview.md).</span></span> <span data-ttu-id="5284b-143">Toto téma popisuje scénář, který představuje základní kámen služby každý z kurzů této řady.</span><span class="sxs-lookup"><span data-stu-id="5284b-143">This topic describes the scenario that underpins each of the tutorials in this series.</span></span> <span data-ttu-id="5284b-144">Tento scénář se zaměřuje na požadavky Application Lifecycle Management (ALM) fiktivní společnosti s názvem společnosti Fabrikam, Inc., jak se vyvíjí webové aplikace podnikové úrovni.</span><span class="sxs-lookup"><span data-stu-id="5284b-144">The scenario focuses on the Application Lifecycle Management (ALM) requirements of a fictional company named Fabrikam, Inc. as it develops an enterprise-scale web application.</span></span>
- <span data-ttu-id="5284b-145">[Správa životního cyklu aplikací: Od vývoje k ostrému provozu](application-lifecycle-management-from-development-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-145">[Application Lifecycle Management: From Development to Production](application-lifecycle-management-from-development-to-production.md).</span></span> <span data-ttu-id="5284b-146">Toto téma obsahuje přehled procesu nasazení vysoké úrovně, začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="5284b-146">This topic provides a high-level, end-to-end overview of a deployment process.</span></span> <span data-ttu-id="5284b-147">Ukazuje, jak společnosti Fabrikam, Inc. přejde podnikových webovou aplikaci ASP.NET pomocí testu, přípravného a produkčního prostředí jako součást procesu průběžného vývoje.</span><span class="sxs-lookup"><span data-stu-id="5284b-147">It illustrates how Fabrikam,Inc. moves an enterprise-scale ASP.NET web application through test, staging, and production environments as part of a continuous development process.</span></span>

<span data-ttu-id="5284b-148">Obsahuje čtyři kurz sady.</span><span class="sxs-lookup"><span data-stu-id="5284b-148">The series includes four tutorial sets.</span></span> <span data-ttu-id="5284b-149">Každý se zaměřuje na různé aspekty nasazení webu:</span><span class="sxs-lookup"><span data-stu-id="5284b-149">Each focuses on different aspects of web deployment:</span></span>

- <span data-ttu-id="5284b-150">[Webové nasazení v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-150">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="5284b-151">Tento kurz obsahuje koncepční Úvod do souborů projektu MSBuild, kanálu publikování webové, Web Deploy a dalších souvisejících technologiích.</span><span class="sxs-lookup"><span data-stu-id="5284b-151">This tutorial provides a conceptual introduction to MSBuild project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="5284b-152">Vysvětluje, jak můžete pomocí těchto nástrojů společně ke správě nasazení komplexních procesů.</span><span class="sxs-lookup"><span data-stu-id="5284b-152">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="5284b-153">[Konfigurace serverového prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-153">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="5284b-154">Tento kurz popisuje, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí Služba agenta nasazení webu ("vzdáleného agenta") nebo obslužná rutina webového nasazení a nasazení vzdálené databáze.</span><span class="sxs-lookup"><span data-stu-id="5284b-154">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the "remote agent") or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="5284b-155">Poskytuje rady, jak volba metody nasazení pro konkrétní prostředí, a popisuje způsob použití WFF replikovat nasazených webových aplikací ve všech webových serverů v serverové farmě.</span><span class="sxs-lookup"><span data-stu-id="5284b-155">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the WFF to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="5284b-156">[Konfigurace serveru Team Foundation Server pro nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-156">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="5284b-157">Tento kurz popisuje postup konfigurace serveru TFS pro podporu různých scénářů nasazení, včetně automatizovaného nasazení jako součást procesu CI a ručně spustit nasazení konkrétního sestavení.</span><span class="sxs-lookup"><span data-stu-id="5284b-157">This tutorial describes how to configure TFS to support various deployment scenarios, including automated deployment as part of a CI process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="5284b-158">[Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5284b-158">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="5284b-159">Tento kurz popisuje, jak k provádění různých rozšířené nasazení úkoly, jako je přizpůsobení nasazené databáze pro více prostředí, s výjimkou souborů a složek z nasazení a převedení webové aplikace do offline režimu během procesu nasazení .</span><span class="sxs-lookup"><span data-stu-id="5284b-159">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

## <a name="where-to-start"></a><span data-ttu-id="5284b-160">Kde začít</span><span class="sxs-lookup"><span data-stu-id="5284b-160">Where to Start</span></span>

<span data-ttu-id="5284b-161">Této sérii kurzů používá ukázkové řešení s realistické úroveň složitosti, společně s scénář nasazení fiktivní organizace, a zadejte referenční implementaci a poskytnout úkoly a návody pro běžné kontextu.</span><span class="sxs-lookup"><span data-stu-id="5284b-161">This set of tutorials uses a sample solution with a realistic level of complexity, together with a fictional enterprise deployment scenario, to provide a reference implementation and to give the tasks and walkthroughs a common context.</span></span> <span data-ttu-id="5284b-162">Dalším tématu s názvem [nasazení podnikového webu: Přehled scénářů](enterprise-web-deployment-scenario-overview.md), představuje scénář a ukázkové řešení.</span><span class="sxs-lookup"><span data-stu-id="5284b-162">The next topic, [Enterprise Web Deployment: Scenario Overview](enterprise-web-deployment-scenario-overview.md), introduces the scenario and the sample solution.</span></span> <span data-ttu-id="5284b-163">Odtud můžete pracovat prostřednictvím těchto kurzů a témata, které nejvíce odpovídají vašim potřebám.</span><span class="sxs-lookup"><span data-stu-id="5284b-163">From there you can work through the tutorials and topics that most closely match your needs.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5284b-164">Next</span><span class="sxs-lookup"><span data-stu-id="5284b-164">Next</span></span>](enterprise-web-deployment-scenario-overview.md)