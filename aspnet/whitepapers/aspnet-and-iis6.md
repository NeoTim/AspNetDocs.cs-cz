---
uid: whitepapers/aspnet-and-iis6
title: Spuštění ASP.NET 1.1 se službou IIS 6.0 | Dokumentace Microsoftu
author: rick-anderson
description: Sice systému Windows Server 2003, zahrnuje službu IIS 6.0 a ASP.NET 1.1, jsou ve výchozím nastavení zakázané tyto komponenty. Tento dokument White Paper popisuje, jak povolit služby IIS 6.0...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: dbdf6d2815a05465b0ffb7bb322c9f80af13a251
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59405154"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="2d57a-104">Spuštění ASP.NET 1.1 se službou IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="2d57a-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="2d57a-105">Sice systému Windows Server 2003, zahrnuje službu IIS 6.0 a ASP.NET 1.1, jsou ve výchozím nastavení zakázané tyto komponenty.</span><span class="sxs-lookup"><span data-stu-id="2d57a-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="2d57a-106">Tento dokument White Paper popisuje postup při povolování služby IIS 6.0 a ASP.NET 1.1 a doporučuje několik nastavení konfigurace, abyste získali optimální výkon služby IIS a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d57a-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="2d57a-107">Platí pro technologii ASP.NET 1.1 a IIS 6.0.</span><span class="sxs-lookup"><span data-stu-id="2d57a-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>


<span data-ttu-id="2d57a-108">ASP.NET 1.1 se dodává se systémem Windows Server 2003, který taky obsahuje nejnovější verzi nástroje Internet Information Server (IIS) verze 6.0.</span><span class="sxs-lookup"><span data-stu-id="2d57a-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="2d57a-109">Služba IIS 6.0 a ASP.NET 1.1 jsou navržené tak bez problémů integrovat a ASP.NET výchozí nastavení pro nový model procesu pracovního procesu služby IIS 6.0.</span><span class="sxs-lookup"><span data-stu-id="2d57a-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="2d57a-110">Ve výchozím nastavení není nainstalována technologie ASP.NET 1.1</span><span class="sxs-lookup"><span data-stu-id="2d57a-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="2d57a-111">Na rozdíl od předchozích verzí operačních systémů od Microsoftu server Internet Information Server (IIS) není povolená ve výchozím nastavení; ani je ASP.NET 1.1.</span><span class="sxs-lookup"><span data-stu-id="2d57a-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="2d57a-112">Existují dvě možnosti pro povolení služby IIS:</span><span class="sxs-lookup"><span data-stu-id="2d57a-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="2d57a-113">Povolení služby IIS, možnost #1 - Průvodce konfigurací serveru</span><span class="sxs-lookup"><span data-stu-id="2d57a-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="2d57a-114">Windows Server 2003 se dodává novou "Průvodce konfigurací serveru" vám pomohou správně nakonfigurovat váš server do požadovaného režimu.</span><span class="sxs-lookup"><span data-stu-id="2d57a-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="2d57a-115">Spustí se Průvodce – Poznámka: ke spuštění průvodce, musíte být přihlášeni jako správce – přejít na: Spuštění | Programy | Nástroje pro správu a vyberte možnost "Konfigurace serveru".</span><span class="sxs-lookup"><span data-stu-id="2d57a-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="2d57a-116">Po výběru byste měli vidět "Průvodce konfigurací serveru" úvodní obrazovce:</span><span class="sxs-lookup"><span data-stu-id="2d57a-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="2d57a-117">Klikněte na tlačítko ' Další &gt;":</span><span class="sxs-lookup"><span data-stu-id="2d57a-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="2d57a-118">Klikněte na tlačítko ' Další &gt;.</span><span class="sxs-lookup"><span data-stu-id="2d57a-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="2d57a-119">Na této obrazovce je potřeba vybrat "možnosti konfigurace aplikačního serveru (IIS, ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="2d57a-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="2d57a-120">Klikněte na tlačítko ' Další &gt;".</span><span class="sxs-lookup"><span data-stu-id="2d57a-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="2d57a-121">Po výběru konfigurace serveru jako aplikační Server, se zobrazí tato obrazovka s výzvou, jaké další možnosti, které se má nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="2d57a-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="2d57a-122">Ve výchozím nastavení je vybrána ani jedna možnost.</span><span class="sxs-lookup"><span data-stu-id="2d57a-122">Neither option is selected by default.</span></span> <span data-ttu-id="2d57a-123">Umožňuje automaticky technologie ASP.NET, je nutné vybrat "Povolit ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="2d57a-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="2d57a-124">Klikněte na tlačítko ' Další &gt;".</span><span class="sxs-lookup"><span data-stu-id="2d57a-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="2d57a-125">Tato obrazovka zobrazí, jaké možnosti jsou k instalaci.</span><span class="sxs-lookup"><span data-stu-id="2d57a-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="2d57a-126">Klikněte na tlačítko ' Další &gt;".</span><span class="sxs-lookup"><span data-stu-id="2d57a-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="2d57a-127">Během instalace možností, které jste vybrali, se zobrazí tato obrazovka.</span><span class="sxs-lookup"><span data-stu-id="2d57a-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="2d57a-128">Je normální jiné dialogové okno, které zobrazí pole, protože probíhá instalace služeb.</span><span class="sxs-lookup"><span data-stu-id="2d57a-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="2d57a-129">Kromě toho můžete být vyzváni k zadání umístění instalačního disku CD Windows serveru 2003.</span><span class="sxs-lookup"><span data-stu-id="2d57a-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="2d57a-130">Klikněte na tlačítko ' Další &gt;' po dokončení.</span><span class="sxs-lookup"><span data-stu-id="2d57a-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="2d57a-131">Klikněte na tlačítko 'Dokončit' - Windows Server 2003 je nyní nakonfigurováno pro podporu služby IIS 6.0 a ASP.NET 1.1.</span><span class="sxs-lookup"><span data-stu-id="2d57a-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="2d57a-132">Povolení služby IIS, možnost #2 – Ruční konfigurace služby IIS a ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2d57a-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="2d57a-133">Pokud nechcete použít 'Server Průvodce konfigurací' Volitelně můžete nainstalovat IIS 6.0 a ASP.NET 1.1 pomocí 'Přidat nebo odebrat programy' v Ovládacích panelech.</span><span class="sxs-lookup"><span data-stu-id="2d57a-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="2d57a-134">Nejprve otevřete ovládací Panel:</span><span class="sxs-lookup"><span data-stu-id="2d57a-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="2d57a-135">Pak klikněte na ' Přidat nebo odebrat Windows součásti' tím se otevře Průvodce součásti Windows:</span><span class="sxs-lookup"><span data-stu-id="2d57a-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="2d57a-136">Zvýrazněte a "Aplikační Server" a potom klikněte na "Podrobnosti?"</span><span class="sxs-lookup"><span data-stu-id="2d57a-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="2d57a-137">Tlačítko:</span><span class="sxs-lookup"><span data-stu-id="2d57a-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="2d57a-138">Instalace technologie ASP.NET, zkontrolujte ' ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="2d57a-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="2d57a-139">Klikněte na tlačítko "OK" se vraťte do Průvodce komponentami Windows.</span><span class="sxs-lookup"><span data-stu-id="2d57a-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="2d57a-140">Klikněte na tlačítko ' Další &gt;"z Průvodce komponentami Windows k zahájení instalace:</span><span class="sxs-lookup"><span data-stu-id="2d57a-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="2d57a-141">Je normální jiné dialogové okno, které zobrazí pole, protože probíhá instalace služeb.</span><span class="sxs-lookup"><span data-stu-id="2d57a-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="2d57a-142">Kromě toho můžete být vyzváni k zadání umístění instalačního disku CD Windows serveru 2003.</span><span class="sxs-lookup"><span data-stu-id="2d57a-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="2d57a-143">Po dokončení instalace se zobrazí poslední obrazovce Průvodce komponentami Windows:</span><span class="sxs-lookup"><span data-stu-id="2d57a-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="2d57a-144">Služba IIS 6.0 a ASP.NET 1.1 jsou teď nakonfigurované a dostupné.</span><span class="sxs-lookup"><span data-stu-id="2d57a-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="2d57a-145">Doporučená nastavení</span><span class="sxs-lookup"><span data-stu-id="2d57a-145">Recommended Settings</span></span>

<span data-ttu-id="2d57a-146">Při spuštění ASP.NET 1.1 se službou IIS 6.0, existuje několik nastavení konfigurace, které se doporučuje, abyste získali optimální výkon z technologie ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="2d57a-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="2d57a-147">Konfigurace omezení paměti pracovního procesu</span><span class="sxs-lookup"><span data-stu-id="2d57a-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="2d57a-148">Konfigurace pracovní proces recykluje</span><span class="sxs-lookup"><span data-stu-id="2d57a-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="2d57a-149">Konfigurace omezení paměti pracovního procesu</span><span class="sxs-lookup"><span data-stu-id="2d57a-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="2d57a-150">Ve výchozím nastavení služby IIS 6.0 omezený objem paměti, které může IIS používat nenastaví.</span><span class="sxs-lookup"><span data-stu-id="2d57a-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="2d57a-151">ASP. NET vaší mezipaměti funkce závisí na omezení paměti, proto do mezipaměti proaktivně odebrat nepoužité položky z paměti.</span><span class="sxs-lookup"><span data-stu-id="2d57a-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="2d57a-152">Doporučuje se, že nakonfigurujete funkce služby IIS 6.0 recyklace paměti.</span><span class="sxs-lookup"><span data-stu-id="2d57a-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="2d57a-153">Ke konfiguraci této otevřete Správce Internetové informační služby (spuštění | Programy | Nástroje pro správu | Internetová informační služba).</span><span class="sxs-lookup"><span data-stu-id="2d57a-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="2d57a-154">Jakmile otevřené, rozbalte složku "Fondy aplikací":</span><span class="sxs-lookup"><span data-stu-id="2d57a-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="2d57a-155">Pro každý fond aplikací:</span><span class="sxs-lookup"><span data-stu-id="2d57a-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="2d57a-156">Klikněte pravým tlačítkem na fond aplikací, například "DefaultAppPool" a vyberte 'vlastnosti':</span><span class="sxs-lookup"><span data-stu-id="2d57a-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="2d57a-157">Dál povolte recyklace paměti po kliknutí na buď "maximální využité paměti (v megabajtech):".</span><span class="sxs-lookup"><span data-stu-id="2d57a-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="2d57a-158">Hodnota by neměla být delší než množství fyzické paměti (ne virtual) na serveru, je dobré aproximace 60 % fyzické paměti, například pro server s 512 MB fyzické paměti, vyberte 310.</span><span class="sxs-lookup"><span data-stu-id="2d57a-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="2d57a-159">Doporučuje se také, že maximální nepřekročí 800MB při použití adresní prostor 2GB.</span><span class="sxs-lookup"><span data-stu-id="2d57a-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="2d57a-160">Pokud se adresní prostor paměť serveru je 3GB, maximální limit paměti pro pracovní proces může být až 1 800MB:</span><span class="sxs-lookup"><span data-stu-id="2d57a-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="2d57a-161">Klikněte na tlačítko 'Použít' a 'OK' ukončíte dialogové okno Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="2d57a-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="2d57a-162">Tento postup opakujte pro všechny fondy aplikací k dispozici.</span><span class="sxs-lookup"><span data-stu-id="2d57a-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="2d57a-163">Konfigurace recyklování pracovního procesu</span><span class="sxs-lookup"><span data-stu-id="2d57a-163">Configuring worker recycling</span></span>

<span data-ttu-id="2d57a-164">Ve výchozím nastavení služby IIS 6.0 konfigurován recyklaci jeho pracovní proces každých 29 hodin.</span><span class="sxs-lookup"><span data-stu-id="2d57a-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="2d57a-165">Toto je o něco agresivní pro aplikace používající technologii ASP.NET a je doporučeno, recyklace automatické pracovních procesů je zakázané.</span><span class="sxs-lookup"><span data-stu-id="2d57a-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="2d57a-166">Chcete-li zakázat recyklace automatického pracovního procesu, nejprve otevřete Správce Internetové informační služby (spuštění | Programy | Nástroje pro správu | Internetová informační služba).</span><span class="sxs-lookup"><span data-stu-id="2d57a-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="2d57a-167">Jakmile otevřené, rozbalte složku "Fondy aplikací":</span><span class="sxs-lookup"><span data-stu-id="2d57a-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="2d57a-168">Pro každý fond aplikací:</span><span class="sxs-lookup"><span data-stu-id="2d57a-168">For each application pool:</span></span>

1. <span data-ttu-id="2d57a-169">Klikněte pravým tlačítkem na fond aplikací, například "DefaultAppPool" a vyberte 'vlastnosti':</span><span class="sxs-lookup"><span data-stu-id="2d57a-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="2d57a-170">Zrušte zaškrtnutí políčka ' recyklovat pracovní proces (v minutách): ":</span><span class="sxs-lookup"><span data-stu-id="2d57a-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="2d57a-171">Klikněte na tlačítko 'Použít' a 'OK' ukončíte dialogové okno Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="2d57a-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="2d57a-172">Tento postup opakujte pro všechny fondy aplikací k dispozici.</span><span class="sxs-lookup"><span data-stu-id="2d57a-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="2d57a-173">Udělení oprávnění k zápisu do systému souborů</span><span class="sxs-lookup"><span data-stu-id="2d57a-173">Granting write access to the file system</span></span>

<span data-ttu-id="2d57a-174">Pokud vaše aplikace vyžaduje oprávnění k zápisu do systému souborů a používáte je potřeba upravit řízení přístupu seznamu (ACL) na složku nebo soubor udělit technologii ASP.NET přístup do systému souborů NTFS.</span><span class="sxs-lookup"><span data-stu-id="2d57a-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="2d57a-175">Například udělit ASP.NET oprávnění k zápisu do c:\inetpub\wwwroot nejprve otevřete Průzkumníka a přejděte do adresáře:</span><span class="sxs-lookup"><span data-stu-id="2d57a-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="2d57a-176">Pak klikněte pravým tlačítkem na adresář, např "wwwroot" a vyberte možnost Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="2d57a-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="2d57a-177">Po otevření dialogového okna Vlastnosti vyberte kartu "Zabezpečení":</span><span class="sxs-lookup"><span data-stu-id="2d57a-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="2d57a-178">Adresář c:\inetpub\wwwroot\ je zvláštní v dané speciální skupinu služby IIS 6.0 "IIS\_WPG' je již oprávnění ke čtení &amp; oprávnění spouštět, zobrazovat obsah složky a číst.</span><span class="sxs-lookup"><span data-stu-id="2d57a-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="2d57a-179">Ale pokud chcete udělit oprávnění k zápisu, potřebujete klikněte na zaškrtávací políčko Povolit pro zápis:</span><span class="sxs-lookup"><span data-stu-id="2d57a-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="2d57a-180">Služba IIS 6.0 teď má oprávnění k zápisu pro tuto složku.</span><span class="sxs-lookup"><span data-stu-id="2d57a-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="2d57a-181">Udělení oprávnění k zápisu v jiných složkách, postupujte podle těchto kroků – mějte na paměti, budete muset přidat IIS\_WPG skupina, pokud ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="2d57a-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="2d57a-182">Udělení oprávnění zapisovat do služby IIS\_WPG vám umožní libovolné aplikaci ASP.NET k zápisu do tohoto adresáře.</span><span class="sxs-lookup"><span data-stu-id="2d57a-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="2d57a-183">Podpora integrované ověřování s využitím SQL serveru</span><span class="sxs-lookup"><span data-stu-id="2d57a-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="2d57a-184">Integrované ověřování umožňuje serveru SQL Server využívat ověřování systému Windows NT pro ověření serveru SQL Server při účty přihlášení.</span><span class="sxs-lookup"><span data-stu-id="2d57a-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="2d57a-185">To umožňuje uživateli obejít standardní proces přihlášení serveru SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2d57a-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="2d57a-186">S tímto přístupem sítě uživatel může přistupovat k databázi serveru SQL Server bez poskytnutí samostatné přihlašovací identifikátor nebo heslo, protože systém SQL Server získá uživatele a informace o hesle z procesu zabezpečení sítě systému Windows NT.</span><span class="sxs-lookup"><span data-stu-id="2d57a-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="2d57a-187">Výběr integrované ověřování pro aplikace ASP.NET je dobrou volbou, protože žádné přihlašovací údaje se nikdy neuloží do připojovacího řetězce pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2d57a-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="2d57a-188">Připojovací řetězec použitý pro připojení k SQL místo toho bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="2d57a-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="2d57a-189">Tento připojovací řetězec říká systému SQL Server pomocí přihlašovacích údajů Windows aplikace pokusu o přístup k systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2d57a-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="2d57a-190">V případě ASP.NET/IIS 6, to může být účet ve službě IIS\_WPG skupiny.</span><span class="sxs-lookup"><span data-stu-id="2d57a-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="2d57a-191">Pokud chcete povolit integrované ověřování mezi SQL serverem a technologie ASP.NET, budete muset nejprve zkontrolujte, že systém SQL Server je nakonfigurován pro integrované ověřování nebo smíšený režim ověřování – obraťte se na správce databáze ke zjištění.</span><span class="sxs-lookup"><span data-stu-id="2d57a-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="2d57a-192">Pokud je SQL Server v jednom z těchto dvou režimů, můžete použít integrované ověřování.</span><span class="sxs-lookup"><span data-stu-id="2d57a-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="2d57a-193">Otevřete správce systému SQL Server Enterprise (Start | Programy | Microsoft SQL Server | Správce rozlehlé sítě), vyberte příslušný server a rozbalte složku zabezpečení:</span><span class="sxs-lookup"><span data-stu-id="2d57a-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="2d57a-194">Pokud se BUILTINT\IIS\_WPG "skupina není uvedena, klikněte pravým tlačítkem na přihlášení a výběr nového přihlašovacího jména:</span><span class="sxs-lookup"><span data-stu-id="2d57a-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="2d57a-195">V "název:" textového pole zadejte "[název serveru/domény] \IIS\_WPG" nebo kliknutím na tlačítko se třemi tečkami otevřete nástroj pro výběr uživatele nebo skupiny systému Windows NT:</span><span class="sxs-lookup"><span data-stu-id="2d57a-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="2d57a-196">Vyberte aktuálního počítače IIS\_WPG skupiny a klikněte na tlačítko "Přidat" a OK zavřete Nástroj pro výběr.</span><span class="sxs-lookup"><span data-stu-id="2d57a-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="2d57a-197">Pak musíte také nastavit výchozí databáze a oprávnění pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="2d57a-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="2d57a-198">Nastavit výchozí databázi vyberte z rozevíracího seznamu, například Northwind níže je vybrána:</span><span class="sxs-lookup"><span data-stu-id="2d57a-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="2d57a-199">Pak klikněte na kartě přístup k databázi:</span><span class="sxs-lookup"><span data-stu-id="2d57a-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="2d57a-200">Klikněte na zaškrtávací políčko Povolit pro každou databázi, kterou chcete povolit přístup k.</span><span class="sxs-lookup"><span data-stu-id="2d57a-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="2d57a-201">Budete také muset vyberte databázové role, kontrola db\_vlastníka zajistí vaše přihlašovací údaje má všechna potřebná oprávnění ke správě a použít vybraná databáze.</span><span class="sxs-lookup"><span data-stu-id="2d57a-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="2d57a-202">Klikněte na tlačítko OK zavřete dialogové okno vlastností.</span><span class="sxs-lookup"><span data-stu-id="2d57a-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="2d57a-203">Vaše aplikace ASP.NET je nyní nakonfigurováno pro podporu integrované ověřování systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2d57a-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="2d57a-204">Nelze spustit ASP.NET 1.0 v nativním režimu služby IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="2d57a-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="2d57a-205">ASP.NET 1.0 ve službě IIS 6.0 je podporována pouze v režimu kompatibility služby IIS 5.</span><span class="sxs-lookup"><span data-stu-id="2d57a-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="2d57a-206">Ke konfiguraci ASP.NET 1.0 ke spuštění v režimu kompatibility služby IIS 5.0, otevřete Správce internetové služby a klikněte pravým tlačítkem myši klikněte na tlačítko weby a vyberte vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="2d57a-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="2d57a-207">Přepněte na kartu služby a zkontrolujte? Spustit webovou službu v režimu izolace 5.0 IIS?</span><span class="sxs-lookup"><span data-stu-id="2d57a-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
