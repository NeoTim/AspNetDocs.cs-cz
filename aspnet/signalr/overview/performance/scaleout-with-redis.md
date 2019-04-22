---
uid: signalr/overview/performance/scaleout-with-redis
title: Škálování aplikace SignalR službou Redis | Dokumentace Microsoftu
author: bradygaster
description: Verze softwaru použitým v tomto tématu Visual Studio 2013 .NET 4.5 SignalR 2 předchozí verze tohoto tématu informace o předchozích verzích...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 78efe409ab59df17ae71c26d4e280cc9971a64d2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393246"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="d5d86-103">Šklálování aplikace SignalR službou Redis</span><span class="sxs-lookup"><span data-stu-id="d5d86-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="d5d86-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d5d86-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d5d86-105">Verze softwaru použitým v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="d5d86-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d5d86-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5d86-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="d5d86-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d5d86-107">.NET 4.5</span></span>
> - <span data-ttu-id="d5d86-108">Funkce SignalR verze 2.4</span><span class="sxs-lookup"><span data-stu-id="d5d86-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d5d86-109">Předchozích verzích tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="d5d86-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d5d86-110">Informace o předchozích verzích systému SignalR naleznete v tématu [starší verze funkce SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="d5d86-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d5d86-111">Otázky a komentáře</span><span class="sxs-lookup"><span data-stu-id="d5d86-111">Questions and comments</span></span>
>
> <span data-ttu-id="d5d86-112">Napište prosím zpětnou vazbu o tom, jak vám líbilo v tomto kurzu a co můžeme zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="d5d86-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d5d86-113">Pokud máte nějaké otázky, které přímo nesouvisejí, najdete v tomto kurzu, můžete je publikovat [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="d5d86-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="d5d86-114">V tomto kurzu budete používat [Redis](http://redis.io/) k distribuci zpráv do aplikace SignalR, který je nasazen na dvou samostatných instancí služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d5d86-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="d5d86-115">Redis je úložiště klíč / hodnota v paměti.</span><span class="sxs-lookup"><span data-stu-id="d5d86-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="d5d86-116">Podporuje také systému zasílání zpráv s modelem publikování a přihlášení k odběru.</span><span class="sxs-lookup"><span data-stu-id="d5d86-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="d5d86-117">Propojovací rozhraní systému SignalR Redis používá funkci pub/sub pro předávání zpráv na jiné servery.</span><span class="sxs-lookup"><span data-stu-id="d5d86-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="d5d86-118">Pro účely tohoto kurzu budete používat tři servery:</span><span class="sxs-lookup"><span data-stu-id="d5d86-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="d5d86-119">Dva servery se systémem Windows, který použijete k nasazení aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5d86-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="d5d86-120">Jeden server se systémem Linux, který použijete ke spuštění Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="d5d86-121">Snímky obrazovky v tomto kurzu můžu použít Ubuntu 12.04 TLS.</span><span class="sxs-lookup"><span data-stu-id="d5d86-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="d5d86-122">Pokud nemáte tří fyzických serverů pro použití, můžete vytvořit virtuální počítače v Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d5d86-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="d5d86-123">Další možností je vytvořit virtuální počítače v Azure.</span><span class="sxs-lookup"><span data-stu-id="d5d86-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="d5d86-124">I když v tomto kurzu používá oficiální implementace Redis, k dispozici je také [Windows port Redis](https://github.com/MSOpenTech/redis) z MSOpenTech.</span><span class="sxs-lookup"><span data-stu-id="d5d86-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="d5d86-125">Instalace a konfigurace se liší, ale jinak kroky jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="d5d86-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d5d86-126">Škálování aplikace SignalR službou Redis nepodporuje clustery Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>


## <a name="overview"></a><span data-ttu-id="d5d86-127">Přehled</span><span class="sxs-lookup"><span data-stu-id="d5d86-127">Overview</span></span>

<span data-ttu-id="d5d86-128">Předtím, než získáme podrobný kurz, zde je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="d5d86-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="d5d86-129">Nainstalujte Redis a spusťte Redis server.</span><span class="sxs-lookup"><span data-stu-id="d5d86-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="d5d86-130">Přidejte tyto balíčky NuGet pro vaši aplikaci:</span><span class="sxs-lookup"><span data-stu-id="d5d86-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="d5d86-131">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="d5d86-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="d5d86-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="d5d86-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="d5d86-133">Vytvoření aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5d86-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="d5d86-134">Přidejte následující kód do souboru Startup.cs konfigurace propojovacího rozhraní:</span><span class="sxs-lookup"><span data-stu-id="d5d86-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="d5d86-135">Ubuntu on Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d5d86-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="d5d86-136">Pomocí Windows Hyper-V, můžete snadno vytvořit virtuální počítač s Ubuntu ve Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="d5d86-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="d5d86-137">Stáhněte si bitovou kopii ISO se systémem Ubuntu z [ http://www.ubuntu.com ](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="d5d86-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="d5d86-138">Technologie Hyper-V přidejte nový virtuální počítač.</span><span class="sxs-lookup"><span data-stu-id="d5d86-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="d5d86-139">V **připojit virtuální pevný Disk** kroku, vyberte **virtuální pevný disk vytvoříte**.</span><span class="sxs-lookup"><span data-stu-id="d5d86-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="d5d86-140">V **možnosti instalace** kroku, vyberte **soubor bitové kopie (.iso)**, klikněte na tlačítko **Procházet**a přejděte do instalační Ubuntu ISO.</span><span class="sxs-lookup"><span data-stu-id="d5d86-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="d5d86-141">Nainstalujte Redis</span><span class="sxs-lookup"><span data-stu-id="d5d86-141">Install Redis</span></span>

<span data-ttu-id="d5d86-142">Postupujte podle kroků uvedených v [ http://redis.io/download ](http://redis.io/download) ke stažení a sestavení Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="d5d86-143">Tento postup sestaví binární soubory Redis `src` adresáře.</span><span class="sxs-lookup"><span data-stu-id="d5d86-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="d5d86-144">Ve výchozím nastavení Redis, aby heslo.</span><span class="sxs-lookup"><span data-stu-id="d5d86-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="d5d86-145">Chcete-li nastavit heslo, upravte `redis.conf` soubor, který je umístěn v kořenovém adresáři zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="d5d86-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="d5d86-146">(Před zahájením úprav, vytvořili záložní kopii souboru!) Přidejte následující direktivy k `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="d5d86-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="d5d86-147">Nyní spusťte Redis server:</span><span class="sxs-lookup"><span data-stu-id="d5d86-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="d5d86-148">Otevřený port 6379, což je výchozí port, který Redis naslouchá.</span><span class="sxs-lookup"><span data-stu-id="d5d86-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="d5d86-149">(Můžete změnit číslo portu v konfiguračním souboru.)</span><span class="sxs-lookup"><span data-stu-id="d5d86-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="d5d86-150">Vytvoření aplikace SignalR</span><span class="sxs-lookup"><span data-stu-id="d5d86-150">Create the SignalR Application</span></span>

<span data-ttu-id="d5d86-151">Vytvoření aplikace SignalR pomocí některé z těchto kurzů:</span><span class="sxs-lookup"><span data-stu-id="d5d86-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="d5d86-152">Začínáme s knihovnou SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="d5d86-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="d5d86-153">Začínáme s knihovnou SignalR 2.0 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="d5d86-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="d5d86-154">V dalším kroku upravíme, aby byl chatovací aplikaci, aby podporovala škálování s využitím Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="d5d86-155">Nejprve přidejte `Microsoft.AspNet.SignalR.StackExchangeRedis` do svého projektu balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5d86-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="d5d86-156">V aplikaci Visual Studio z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="d5d86-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d5d86-157">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="d5d86-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="d5d86-158">Dále otevřete Startup.cs souboru.</span><span class="sxs-lookup"><span data-stu-id="d5d86-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="d5d86-159">Přidejte následující kód, který **konfigurace** metody:</span><span class="sxs-lookup"><span data-stu-id="d5d86-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="d5d86-160">"server" je název serveru, na kterém běží Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="d5d86-161">*port* je číslo portu</span><span class="sxs-lookup"><span data-stu-id="d5d86-161">*port* is the port number</span></span>
- <span data-ttu-id="d5d86-162">"password" je heslo, které jste definovali v souboru redis.conf.</span><span class="sxs-lookup"><span data-stu-id="d5d86-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="d5d86-163">"AppName" je jakýkoli řetězec.</span><span class="sxs-lookup"><span data-stu-id="d5d86-163">"AppName" is any string.</span></span> <span data-ttu-id="d5d86-164">Funkce SignalR vytvoří kanál pub/sub Redis s tímto názvem.</span><span class="sxs-lookup"><span data-stu-id="d5d86-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="d5d86-165">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d5d86-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="d5d86-166">Nasazení a spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="d5d86-166">Deploy and Run the Application</span></span>

<span data-ttu-id="d5d86-167">Příprava vašich instancí Windows serveru k nasazení aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5d86-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="d5d86-168">Přidejte roli služby IIS.</span><span class="sxs-lookup"><span data-stu-id="d5d86-168">Add the IIS role.</span></span> <span data-ttu-id="d5d86-169">Zahrnují funkce "Vývoj aplikací", včetně protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="d5d86-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="d5d86-170">Zahrnují taky službu správy (uvedené v části "Nástroje pro správu").</span><span class="sxs-lookup"><span data-stu-id="d5d86-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="d5d86-171">**Nainstalovat Web Deploy 3.0.**</span><span class="sxs-lookup"><span data-stu-id="d5d86-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="d5d86-172">Když spustíte Správce služby IIS, vás vyzve k instalaci webové platformy společnosti Microsoft, nebo se dají [stáhněte instalační program](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="d5d86-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="d5d86-173">Do platformy hledání pro nasazení webu a nainstalovat nasazení webu 3.0</span><span class="sxs-lookup"><span data-stu-id="d5d86-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="d5d86-174">Zkontrolujte, že je spuštěná služby webové správy.</span><span class="sxs-lookup"><span data-stu-id="d5d86-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="d5d86-175">Pokud ne, spusťte službu.</span><span class="sxs-lookup"><span data-stu-id="d5d86-175">If not, start the service.</span></span> <span data-ttu-id="d5d86-176">(Pokud nevidíte v seznamu služeb Windows služby webové správy, ujistěte se, že jste nainstalovali službu pro správu při přidání IIS role.)</span><span class="sxs-lookup"><span data-stu-id="d5d86-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="d5d86-177">Ve výchozím nastavení služby webové správy naslouchá na TCP port 8172.</span><span class="sxs-lookup"><span data-stu-id="d5d86-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="d5d86-178">V bráně Windows Firewall vytvořte nové pravidlo, které povoluje provoz TCP na port 8172.</span><span class="sxs-lookup"><span data-stu-id="d5d86-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="d5d86-179">Další informace najdete v tématu [konfigurace pravidel brány Firewall](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="d5d86-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="d5d86-180">(Pokud jsou hostiteli virtuálních počítačů v Azure, můžete provést přímo na webu Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d5d86-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="d5d86-181">Zobrazit [jak nastavit koncové body k virtuálnímu počítači](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="d5d86-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="d5d86-182">Nyní jste připraveni k nasazení projektu sady Visual Studio z vývojového počítače k serveru.</span><span class="sxs-lookup"><span data-stu-id="d5d86-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="d5d86-183">V Průzkumníku řešení klikněte pravým tlačítkem myši na řešení a klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="d5d86-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="d5d86-184">Podrobnější dokumentaci k nasazení webu, najdete v článku [mapa obsahu webové nasazení pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="d5d86-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="d5d86-185">Pokud nasadíte aplikaci do dvou serverů, můžete otevřít každou instanci v samostatném okně prohlížeče a zobrazit, že každá z jiných příjem zpráv SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5d86-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="d5d86-186">(Samozřejmě v produkčním prostředí, dva servery strávil za nástrojem pro vyrovnávání zatížení.)</span><span class="sxs-lookup"><span data-stu-id="d5d86-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="d5d86-187">Pokud vás to zajímá, zobrazíte zprávy, které se odesílají do Redis, můžete použít **rozhraní příkazového řádku redis** klienta, který se nainstaluje s využitím Redis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
