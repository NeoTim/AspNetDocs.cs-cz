---
uid: whitepapers/side-by-side-with-10
title: Technologie ASP.NET na straně by-Side Execution rozhraní .NET Framework 1.0 a 1.1 | Dokumentace Microsoftu
author: rick-anderson
description: Tento dokument White Paper popisuje, jak nainstalovat na váš počítač, umožní webové aplikaci ASP.NET spustit v jedné verze od .NET 1.0 a 1.1 rozhraní .NET...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c4a371958d8de72628c037b3568551aaa91e0153
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59380701"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="a2d3a-103">ASP.NET – souběžné spuštění .NET Framework 1.0 a 1.1</span><span class="sxs-lookup"><span data-stu-id="a2d3a-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="a2d3a-104">Tento dokument White Paper popisuje postup instalace rozhraní .NET 1.0 a 1.1 rozhraní .NET na svém počítači umožní webové aplikaci ASP.NET spustit v jedné verze rozhraní framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="a2d3a-105">Platí pro technologii ASP.NET 1.0 a ASP.NET 1.1.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>


<span data-ttu-id="a2d3a-106">V technologii ASP.NET aplikace se říká, že souběžné spuštění, když jsou nainstalovány na stejném počítači, ale používají různé verze rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-107">Následující téma popisuje postup konfigurace aplikací technologie ASP.NET pro spuštění vedle sebe a obsahuje podrobný postup:</span><span class="sxs-lookup"><span data-stu-id="a2d3a-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="a2d3a-108">Udržovat mapování vaší webové aplikace .NET Framework verze 1.0 během instalace</span><span class="sxs-lookup"><span data-stu-id="a2d3a-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="a2d3a-109">Mapa webovou aplikaci na konkrétní verzi rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a2d3a-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="a2d3a-110">Najít verzi rozhraní .NET Framework, která používá webový server</span><span class="sxs-lookup"><span data-stu-id="a2d3a-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="a2d3a-111">Tradičně Když komponenta nebo aplikace se aktualizuje na počítači, starší verze je odebrat a nahradí novější verze.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="a2d3a-112">Pokud nová verze není kompatibilní s předchozí verzí, to obvykle dělí jiné aplikace, které používají součást nebo aplikace.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="a2d3a-113">Rozhraní .NET Framework poskytuje podporu pro spuštění vedle sebe, což umožňuje více verzí sestavení nebo aplikace bude nainstalována do stejného počítače ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="a2d3a-114">Protože najednou může být nainstalováno více verzí, můžete vybrat spravované aplikace která verze se má použít, aniž by to ovlivnilo aplikace, které používají jinou verzi.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="a2d3a-115">Ve výchozím nastavení během instalace rozhraní .NET Framework verze 1.1, všechny stávající aplikace ASP.NET jsou automaticky překonfigurovat tak, aby používali nejnovější verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-116">Pokud nechcete, aby vaše aplikace ASP.NET na rozhraní .NET Framework 1.1 ve výchozím nastavení, klikněte na tlačítko [tady](#1) se naučíte, pokud tomu chcete zabránit během instalace.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="a2d3a-117">Pokud aktualizovat váš webový server na rozhraní .NET Framework 1.1 a má jednu nebo více webových aplikací ke spuštění rozhraní .NET Framework 1.0, budete muset aktualizovat mapu skriptů se Internetové informační služby (IIS).</span><span class="sxs-lookup"><span data-stu-id="a2d3a-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="a2d3a-118">Mapování skriptů je mechanismus pro mapování přípona souboru .aspx pro konkrétní webové aplikace na verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-119">Klikněte na tlačítko [tady](#2) se dozvíte, jak namapovat webovou aplikaci na konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="a2d3a-120">Můžete použít správce sítě Internet informace nebo ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) k vyhledání, která verze rozhraní .NET Framework běží konkrétní webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="a2d3a-121">Klikněte na tlačítko [tady](#3) se naučíte, jak najít verzi rozhraní .NET Framework, která používá webový server.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="a2d3a-122">Jedním z faktorů import při migraci na rozhraní .NET Framework 1.1 je, že každou verzi rozhraní .NET Framework používá svůj vlastní soubor Machine.config.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="a2d3a-123">V důsledku toho Web správce provedl změny souboru Machine.config, je nutné tyto změny migrovat do souboru Machine.config 1.1 rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="a2d3a-124">Správa mapování vaší webové aplikace na rozhraní .NET Framework 1.0 během instalace</span><span class="sxs-lookup"><span data-stu-id="a2d3a-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="a2d3a-125">Ve výchozím nastavení jsou automaticky během instalace používat novější verzi rozhraní .NET Framework překonfigurovat všech existujících aplikací ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-126">Používá novější verzi rozhraní .NET Framework, aplikace můžete plně využít vylepšení a nových funkcích v nové verzi.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="a2d3a-127">Ve stejnou dobu správce webu, který může být vhodné podrobnou kontrolu nad aplikace, které se aktualizují, můžete zabránit automatické přemapování všech existujících aplikací ASP.NET během instalace rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="a2d3a-128">Pokud chcete zabránit automatickému přemapování celé aplikace ASP.NET na novější verzi rozhraní .NET Framework, můžete použít správce webu možnost příkazového řádku/noaspupgrade s instalačním programem Dotnetfx.exe.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="a2d3a-129">**Aby se zabránilo celkový přemapování aplikace ASP.NET na novější verzi**</span><span class="sxs-lookup"><span data-stu-id="a2d3a-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="a2d3a-130">Přejděte na **Start**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-130">Go to **Start**.</span></span>
2. <span data-ttu-id="a2d3a-131">Klikněte na **spustit**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-131">Click on **run**.</span></span>
3. <span data-ttu-id="a2d3a-132">Typ **cmd**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-132">Type **cmd**.</span></span>
4. <span data-ttu-id="a2d3a-133">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="a2d3a-134">Z příkazového řádku zadejte následující řádek, který spustí instalaci rozhraní .NET Framework: **Sady Dotnetfx.exe "instalace/noaspupgrade?** .</span><span class="sxs-lookup"><span data-stu-id="a2d3a-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="a2d3a-135">Klikněte na tlačítko **Ano** při instalaci rozhraní Microsoft .NET Framework 1.1.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="a2d3a-136">Tím se spustí proces instalace rozhraní .NET Framework 1.1.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="a2d3a-137">Mapa webovou aplikaci na konkrétní verzi rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a2d3a-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="a2d3a-138">Zahrnuje každá verze rozhraní .NET Framework verze nástroje ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span><span class="sxs-lookup"><span data-stu-id="a2d3a-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="a2d3a-139">Tento nástroj umožňuje správcům určit spuštění webové aplikace v rámci konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-140">To se označuje jako mapování webové aplikace na verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="a2d3a-141">Správci musí vybrat Aspnet\_regiis.exe, která odpovídá verzi rozhraní .NET Framework, která bude spojená s webovou aplikací.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="a2d3a-142">Například správce, který chce určit, že webový server používat rozhraní .NET Framework 1.1 musí použít Aspnet\_regiis.exe, který je součástí rozhraní .NET Framework 1.1.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="a2d3a-143">Aspnet\_regiis.exe pro verzi 1.0 se nachází na:</span><span class="sxs-lookup"><span data-stu-id="a2d3a-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="a2d3a-144">C:\WINDOWS\Microsoft.NET\Framework\*\*v1.0.3705\*\*\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="a2d3a-144">C:\WINDOWS\Microsoft.NET\Framework\*\*v1.0.3705\*\*\aspnet\_regiis</span></span>

<span data-ttu-id="a2d3a-145">Aspnet\_regiis.exe pro verzi 1,1 se nachází na:</span><span class="sxs-lookup"><span data-stu-id="a2d3a-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="a2d3a-146">C:\WINDOWS\Microsoft.NET\Framework\*\*v1.1.4322\*\*\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="a2d3a-146">C:\WINDOWS\Microsoft.NET\Framework\*\*v1.1.4322\*\*\aspnet\_regiis</span></span>

<span data-ttu-id="a2d3a-147">Aspnet\_regiis.exe poskytuje dvě možnosti pro skript mapování webové aplikace:</span><span class="sxs-lookup"><span data-stu-id="a2d3a-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="a2d3a-148">**-s** Nastaví mapu skriptů se v cestě a v jeho podřízených adresáře.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="a2d3a-149">**-sn** Nastaví mapu skriptů se pouze na cestě.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="a2d3a-150">Definuje cestu webové aplikace služby IIS metadat cesty, která je definována v podobě W3SVC/ROOT / {WebSiteNumber} / {aplikace\_Name}.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="a2d3a-151">Cesta metabáze je pro webové aplikace volá Portal nachází v rámci výchozí webový server, W3SVC/1/ROOT/portál.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="a2d3a-152">Všimněte si, že nástroj zvaný editoru metabáze můžete také použít k získání cesty metabáze.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="a2d3a-153">Tento nástroj si můžete stáhnout z webu Microsoft Support na [ https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="a2d3a-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="a2d3a-154">Spustit Aspnet\_mapy a jeho subapplication skriptu regiis.exe -s W3SVC/1/ROOT/portál aktualizovat na portálu služby IIS.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="a2d3a-155">Spustit Aspnet\_regiis.exe -sn namapovat W3SVC/1/ROOT/portál aktualizovat portál skriptů služby IIS, aniž by to ovlivnilo aplikací na portálu? s podadresářů.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="a2d3a-156">Najít verzi rozhraní .NET Framework, která používá webovou aplikaci</span><span class="sxs-lookup"><span data-stu-id="a2d3a-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="a2d3a-157">Správce může pomocí Správce služeb sítě Internet k vyhledání, která verze rozhraní .NET Framework běží webový server.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="a2d3a-158">Různé verze operačního systému jinak spusťte Správce služeb sítě Internet.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="a2d3a-159">Ke spuštění portálu service manager, postupujte podle kroků uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="a2d3a-160">**Chcete-li spustit Správce služeb sítě Internet**</span><span class="sxs-lookup"><span data-stu-id="a2d3a-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="a2d3a-161">Přejděte na **Start**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-161">Go to **Start**.</span></span>
2. <span data-ttu-id="a2d3a-162">Klikněte na **spustit**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-162">Click on **run**.</span></span>
3. <span data-ttu-id="a2d3a-163">Typ **inetmgr**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="a2d3a-164">Ze Správce služeb Internetu vyberte webovou aplikaci, jejíž verze rozhraní .NET Framework, budete chtít vědět.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="a2d3a-165">Klikněte pravým tlačítkem na webovou aplikaci a klikněte na **vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="a2d3a-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="a2d3a-166">V okně Vlastnosti vyberte **konfigurace.**</span><span class="sxs-lookup"><span data-stu-id="a2d3a-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="a2d3a-167">V tabulce mapování aplikace vyberte **.aspx**a klikněte na tlačítko **upravit**.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="a2d3a-168">Z **spustitelný soubor** textového pole, najdete v adresáři verze posunutím.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="a2d3a-169">Pokud adresář verze je v.1.1.4322, aplikace se mapuje na rozhraní .NET Framework 1.1.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="a2d3a-170">Naopak pokud adresář verze je v1.0.3705, aplikace se mapuje na rozhraní .NET Framework 1.0.</span><span class="sxs-lookup"><span data-stu-id="a2d3a-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
