---
uid: mvc/overview/deployment/docker-aspnetmvc
title: Migrace aplikací ASP.NET MVC do kontejnerů s Windows
description: Zjistěte, jak vzít existující ASP.NET aplikaci MVC a spustit ji v kontejneru Windows Dockeru
keywords: Kontejnery systému Windows,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675186"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="6268a-104">Migrace aplikací ASP.NET MVC do kontejnerů s Windows</span><span class="sxs-lookup"><span data-stu-id="6268a-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="6268a-105">Spuštění existující aplikace založené na rozhraní .NET Framework v kontejneru windows nevyžaduje žádné změny vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="6268a-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="6268a-106">Chcete-li aplikaci spustit v kontejneru windows, vytvořte bitovou kopii Dockeru obsahující vaši aplikaci a spusťte kontejner.</span><span class="sxs-lookup"><span data-stu-id="6268a-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="6268a-107">Toto téma vysvětluje, jak vzít existující [ASP.NET aplikace MVC](http://www.asp.net/mvc) a nasadit ji v kontejneru systému Windows.</span><span class="sxs-lookup"><span data-stu-id="6268a-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="6268a-108">Začnete s existující aplikací ASP.NET MVC a pak publikujete publikované datové zdroje pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6268a-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="6268a-109">Docker uděláte k vytvoření bitové kopie, která obsahuje a spouští vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6268a-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="6268a-110">Přejdete na web spuštěný v kontejneru windows a ověříte, že aplikace funguje.</span><span class="sxs-lookup"><span data-stu-id="6268a-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="6268a-111">Tento článek předpokládá základní znalost Dockeru.</span><span class="sxs-lookup"><span data-stu-id="6268a-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="6268a-112">Informace o Dockeru najdete v článku [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Přehled Dockeru).</span><span class="sxs-lookup"><span data-stu-id="6268a-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="6268a-113">Aplikace, kterou spustíte v kontejneru, je jednoduchý web, který odpovídá na otázky náhodně.</span><span class="sxs-lookup"><span data-stu-id="6268a-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="6268a-114">Tato aplikace je základní MVC aplikace bez ověřování nebo databázové úložiště; umožňuje zaměřit se na přesunutí webové vrstvy do kontejneru.</span><span class="sxs-lookup"><span data-stu-id="6268a-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="6268a-115">Budoucí témata ukáží, jak přesunout a spravovat trvalé úložiště v kontejnerizovaných aplikacích.</span><span class="sxs-lookup"><span data-stu-id="6268a-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="6268a-116">Přesunutí aplikace zahrnuje následující kroky:</span><span class="sxs-lookup"><span data-stu-id="6268a-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="6268a-117">Vytvoření úlohy publikování k vytvoření datových zdrojů pro bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="6268a-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="6268a-118">Vytváření image Dockeru, který bude spuštěn a aplikace.</span><span class="sxs-lookup"><span data-stu-id="6268a-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="6268a-119">Spuštění kontejneru Dockeru, který spouští vaši image.</span><span class="sxs-lookup"><span data-stu-id="6268a-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="6268a-120">Ověření aplikace pomocí prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="6268a-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="6268a-121">[Dokončená aplikace](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) je na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="6268a-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6268a-122">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6268a-122">Prerequisites</span></span>

<span data-ttu-id="6268a-123">Vývojový stroj musí mít následující software:</span><span class="sxs-lookup"><span data-stu-id="6268a-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="6268a-124">[Aktualizace Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (nebo vyšší) nebo [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (nebo vyšší)</span><span class="sxs-lookup"><span data-stu-id="6268a-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="6268a-125">[Docker pro Windows](https://docs.docker.com/docker-for-windows/) - verze Stable 1.13.0 nebo 1.12 Beta 26 (nebo novější verze)</span><span class="sxs-lookup"><span data-stu-id="6268a-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="6268a-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6268a-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="6268a-127">Pokud používáte Windows Server 2016, postupujte podle pokynů pro [nasazení hostitele kontejnerů – Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span><span class="sxs-lookup"><span data-stu-id="6268a-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="6268a-128">Po nainstalování a spuštění Dockeru klikněte pravým tlačítkem myši na ikonu na hlavním panelu a vyberte **Switch to Windows containers** (Přepnout na kontejnery Windows).</span><span class="sxs-lookup"><span data-stu-id="6268a-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="6268a-129">To se vyžaduje pro spuštění imagí Dockeru založených na Windows.</span><span class="sxs-lookup"><span data-stu-id="6268a-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="6268a-130">Spuštění tohoto příkazu trvá několik sekund:</span><span class="sxs-lookup"><span data-stu-id="6268a-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="6268a-131">![Kontejner systému Windows][windows-container]</span><span class="sxs-lookup"><span data-stu-id="6268a-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="6268a-132">Publikovat skript</span><span class="sxs-lookup"><span data-stu-id="6268a-132">Publish script</span></span>

<span data-ttu-id="6268a-133">Shromážděte na jednom místě všechny prostředky, které potřebujete nahrát do image Dockeru.</span><span class="sxs-lookup"><span data-stu-id="6268a-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="6268a-134">Pomocí příkazu **Publikování** v sadě Visual Studio můžete vytvořit profil publikování pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6268a-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="6268a-135">Tento profil vloží všechny datové zdroje do jednoho adresářového stromu, který zkopírujete do cílovébitové bitové kopie později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="6268a-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="6268a-136">**Kroky publikování**</span><span class="sxs-lookup"><span data-stu-id="6268a-136">**Publish Steps**</span></span>

1. <span data-ttu-id="6268a-137">Klikněte pravým tlačítkem myši na webový projekt v sadě Visual Studio a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="6268a-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="6268a-138">Klepněte na **tlačítko Vlastní profil**a potom jako metodu vyberte Systém **souborů.**</span><span class="sxs-lookup"><span data-stu-id="6268a-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="6268a-139">Zvolte adresář.</span><span class="sxs-lookup"><span data-stu-id="6268a-139">Choose the directory.</span></span> <span data-ttu-id="6268a-140">Podle konvence používá `bin\Release\PublishOutput`stažená ukázka .</span><span class="sxs-lookup"><span data-stu-id="6268a-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="6268a-141">![Publikovat připojení][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="6268a-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="6268a-142">Otevřete část **Precompile during publishing** **Možnosti publikování souboru** na kartě **Nastavení.**</span><span class="sxs-lookup"><span data-stu-id="6268a-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="6268a-143">Tato optimalizace znamená, že budete kompilaci zobrazení v kontejneru Dockeru, kopírujete předkompilovaná zobrazení.</span><span class="sxs-lookup"><span data-stu-id="6268a-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="6268a-144">![Nastavení publikování][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="6268a-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="6268a-145">Klepněte na tlačítko **Publikovat**a Visual Studio zkopíruje všechny potřebné datové zdroje do cílové složky.</span><span class="sxs-lookup"><span data-stu-id="6268a-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="6268a-146">Sestavení image</span><span class="sxs-lookup"><span data-stu-id="6268a-146">Build the image</span></span>

<span data-ttu-id="6268a-147">Vytvořte nový soubor s názvem *Dockerfile* k definování image Dockeru.</span><span class="sxs-lookup"><span data-stu-id="6268a-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="6268a-148">*Dockerfile* obsahuje pokyny k vytvoření konečné image a obsahuje všechny základní image názvy, požadované součásti, aplikace, kterou chcete spustit, a další image konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6268a-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="6268a-149">*Dockerfile* je vstup `docker build` do příkazu, který vytvoří image.</span><span class="sxs-lookup"><span data-stu-id="6268a-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="6268a-150">Pro toto cvičení vytvoříte bitovou `microsoft/aspnet` kopii na základě image umístěné v [Docker Hubu](https://hub.docker.com/r/microsoft/aspnet/).</span><span class="sxs-lookup"><span data-stu-id="6268a-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="6268a-151">Základní bitová `microsoft/aspnet`kopie , bitová kopie systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6268a-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="6268a-152">Obsahuje windows server core, službu IIS a ASP.NET 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="6268a-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="6268a-153">Když spustíte tuto bitovou kopii v kontejneru, automaticky spustí iis a nainstalované weby.</span><span class="sxs-lookup"><span data-stu-id="6268a-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="6268a-154">Dockerfile, který vytvoří obrázek vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="6268a-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="6268a-155">V tomto souboru Dockerfile není žádný příkaz `ENTRYPOINT`.</span><span class="sxs-lookup"><span data-stu-id="6268a-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="6268a-156">Žádný nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="6268a-156">You don't need one.</span></span> <span data-ttu-id="6268a-157">Při spuštění systému Windows Server se službou IIS je proces služby IIS vstupním bodem, který je nakonfigurován tak, aby se spouštěl v základní bitové kopii aspnet.</span><span class="sxs-lookup"><span data-stu-id="6268a-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="6268a-158">Spusťte příkaz sestavení Dockeru a vytvořte bitovou kopii, která spustí vaši ASP.NET aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6268a-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="6268a-159">Chcete-li to provést, otevřete okno Prostředí PowerShell v adresáři projektu a do adresáře řešení zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="6268a-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="6268a-160">Tento příkaz vytvoří novou bitovou kopii pomocí pokynů v souboru Dockerfile a pojmenuje (-t tagging) bitovou kopii jako mvcrandomanswers.</span><span class="sxs-lookup"><span data-stu-id="6268a-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="6268a-161">To může zahrnovat vytažení základní image z [Docker Hubu](http://hub.docker.com)a přidání aplikace do této image.</span><span class="sxs-lookup"><span data-stu-id="6268a-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="6268a-162">Po dokončení tohoto příkazu můžete `docker images` příkaz spustit a zobrazit informace o novém obrázku:</span><span class="sxs-lookup"><span data-stu-id="6268a-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="6268a-163">ID obrázku se bude v počítači lišit.</span><span class="sxs-lookup"><span data-stu-id="6268a-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="6268a-164">Teď spusťme aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6268a-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="6268a-165">Spuštění kontejneru</span><span class="sxs-lookup"><span data-stu-id="6268a-165">Start a container</span></span>

<span data-ttu-id="6268a-166">Spusťte kontejner provedením `docker run` následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="6268a-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="6268a-167">Argument `-d` říká Docker spustit image v odpojeném režimu.</span><span class="sxs-lookup"><span data-stu-id="6268a-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="6268a-168">To znamená, že image Dockeru běží odpojenod aktuálního prostředí.</span><span class="sxs-lookup"><span data-stu-id="6268a-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="6268a-169">V mnoha příkladech dockeru se může zobrazit -p pro mapování kontejneru a hostitelských portů.</span><span class="sxs-lookup"><span data-stu-id="6268a-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="6268a-170">Výchozí bitová kopie aspnet již nakonfigurovala kontejner tak, aby naslouchal na portu 80 a zpřístupnioval jej.</span><span class="sxs-lookup"><span data-stu-id="6268a-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="6268a-171">Poskytuje `--name randomanswers` název spuštěného kontejneru.</span><span class="sxs-lookup"><span data-stu-id="6268a-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="6268a-172">Tento název můžete použít místo ID kontejneru ve většině příkazů.</span><span class="sxs-lookup"><span data-stu-id="6268a-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="6268a-173">Je `mvcrandomanswers` název obrázku, který má být zahájen.</span><span class="sxs-lookup"><span data-stu-id="6268a-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="6268a-174">Ověřit v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="6268a-174">Verify in the browser</span></span>

<span data-ttu-id="6268a-175">Po spuštění kontejneru se připojte `http://localhost` k běžícímu kontejneru pomocí uvedeného příkladu.</span><span class="sxs-lookup"><span data-stu-id="6268a-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="6268a-176">Zadejte tuto adresu URL do prohlížeče a měli byste vidět spuštěný web.</span><span class="sxs-lookup"><span data-stu-id="6268a-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="6268a-177">Některé VPN nebo proxy software vám může zabránit v navigaci na vaše stránky.</span><span class="sxs-lookup"><span data-stu-id="6268a-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="6268a-178">Můžete jej dočasně zakázat, abyste se ujistili, že kontejner funguje.</span><span class="sxs-lookup"><span data-stu-id="6268a-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="6268a-179">Ukázkový adresář na GitHubu obsahuje [skript PowerShellu,](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) který tyto příkazy provede za vás.</span><span class="sxs-lookup"><span data-stu-id="6268a-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="6268a-180">Otevřete okno PowerShellu, změňte adresář do adresáře řešení a zadejte:</span><span class="sxs-lookup"><span data-stu-id="6268a-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="6268a-181">Výše uvedený příkaz vytvoří bitovou kopii, zobrazí seznam obrázků v počítači a spustí kontejner.</span><span class="sxs-lookup"><span data-stu-id="6268a-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="6268a-182">Chcete-li kontejner zastavit, vydejte `docker stop` příkaz:</span><span class="sxs-lookup"><span data-stu-id="6268a-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="6268a-183">Chcete-li kontejner odebrat, vydejte `docker rm` příkaz:</span><span class="sxs-lookup"><span data-stu-id="6268a-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Přepnutí do kontejneru Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Publikovat do systému souborů"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Nastavení publikování"
