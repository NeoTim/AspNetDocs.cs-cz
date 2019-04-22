---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Škálování aplikace SignalR službou Azure Service Bus (SignalR 1.x) | Dokumentace Microsoftu
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: cab185ccb048a374a08f4b5d978b30675c30a60d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59383955"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="cf391-102">Škálování aplikace SignalR službou Azure Service Bus (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="cf391-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="cf391-103">podle [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="cf391-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="cf391-104">V tomto kurzu se naučíte se nasadit aplikace SignalR webové Role Windows Azure, pomocí propojovací Service Bus rozhraní k distribuci zpráv do jednotlivých instancí rolí.</span><span class="sxs-lookup"><span data-stu-id="cf391-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="cf391-105">Požadavky:</span><span class="sxs-lookup"><span data-stu-id="cf391-105">Prerequisites:</span></span>

- <span data-ttu-id="cf391-106">Účet Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cf391-106">A Windows Azure account.</span></span>
- <span data-ttu-id="cf391-107">[Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cf391-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="cf391-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="cf391-108">Visual Studio 2012.</span></span>

<span data-ttu-id="cf391-109">Propojovací service bus rozhraní je také kompatibilní s [sběrnice služby pro Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), verze 1.1.</span><span class="sxs-lookup"><span data-stu-id="cf391-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="cf391-110">To však není kompatibilní s verzí 1.0 sběrnice služby pro Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cf391-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="cf391-111">Ceny</span><span class="sxs-lookup"><span data-stu-id="cf391-111">Pricing</span></span>

<span data-ttu-id="cf391-112">Propojovací Service Bus rozhraní používá témata pro odesílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="cf391-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="cf391-113">Nejnovější informace cenách, naleznete v tématu [služby Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="cf391-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="cf391-114">V době psaní tohoto návodu můžete odeslat 1 000 000 zpráv za měsíc pro menší než 1 USD.</span><span class="sxs-lookup"><span data-stu-id="cf391-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="cf391-115">Propojovacího rozhraní pošle zprávu služby Service bus pro každé volání metody rozbočovače SignalR.</span><span class="sxs-lookup"><span data-stu-id="cf391-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="cf391-116">Existují také některé řídicí zprávy pro připojení, odpojení, spojovacího nebo odejít ze skupiny a tak dále.</span><span class="sxs-lookup"><span data-stu-id="cf391-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="cf391-117">Ve většině aplikací bude většinu přenos zpráv volání metod rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="cf391-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="cf391-118">Přehled</span><span class="sxs-lookup"><span data-stu-id="cf391-118">Overview</span></span>

<span data-ttu-id="cf391-119">Předtím, než získáme podrobný kurz, zde je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="cf391-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="cf391-120">Chcete-li vytvořit nový obor názvů služby Service Bus pomocí portálu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cf391-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="cf391-121">Přidejte tyto balíčky NuGet pro vaši aplikaci:</span><span class="sxs-lookup"><span data-stu-id="cf391-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="cf391-122">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="cf391-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="cf391-123">Microsoft.AspNet.SignalR.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="cf391-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="cf391-124">Vytvoření aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="cf391-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="cf391-125">Přidejte následující kód do souboru Global.asax konfigurace propojovacího rozhraní:</span><span class="sxs-lookup"><span data-stu-id="cf391-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="cf391-126">Pro každou aplikaci vyberte jinou hodnotu pro "YourAppName".</span><span class="sxs-lookup"><span data-stu-id="cf391-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="cf391-127">Nepoužívejte stejnou hodnotu napříč více aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="cf391-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="cf391-128">Vytvoření služby Azure</span><span class="sxs-lookup"><span data-stu-id="cf391-128">Create the Azure Services</span></span>

<span data-ttu-id="cf391-129">Vytvoření cloudové služby, jak je popsáno v [jak vytvořit a nasadit Cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="cf391-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="cf391-130">Postupujte podle kroků v části "jak: Vytvořit cloudovou službu pomocí metody rychlého vytvoření".</span><span class="sxs-lookup"><span data-stu-id="cf391-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="cf391-131">Pro účely tohoto kurzu není potřeba nahrát certifikát.</span><span class="sxs-lookup"><span data-stu-id="cf391-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="cf391-132">Vytvořte nový obor názvů služby Service Bus, jak je popsáno v [způsob použití služby Service Bus témata/předplatná](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="cf391-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="cf391-133">Postupujte podle kroků v části "Vytvoření služby Namespace".</span><span class="sxs-lookup"><span data-stu-id="cf391-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="cf391-134">Je nutné vybrat stejné oblasti pro cloudové služby a obor názvů služby Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cf391-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="cf391-135">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf391-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="cf391-136">Spusťte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf391-136">Start Visual Studio.</span></span> <span data-ttu-id="cf391-137">Z **souboru** nabídky, klikněte na tlačítko **nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="cf391-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="cf391-138">V **nový projekt** dialogového okna rozbalte **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="cf391-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="cf391-139">V části **nainstalované šablony**vyberte **cloudu** a pak vyberte **Windows Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="cf391-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="cf391-140">Ponechte výchozí rozhraní .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cf391-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="cf391-141">Pojmenujte aplikaci ChatService a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf391-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="cf391-142">V **nová Cloudová služba Windows Azure** dialogového okna, vyberte webovou roli ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="cf391-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="cf391-143">Klikněte na tlačítko se šipkou vpravo (**&gt;**) Chcete-li přidat roli do řešení.</span><span class="sxs-lookup"><span data-stu-id="cf391-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="cf391-144">Najeďte myší na novou roli proto na ikonu tužky viditelné.</span><span class="sxs-lookup"><span data-stu-id="cf391-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="cf391-145">Kliknutím na tuto ikonu přejmenujte roli.</span><span class="sxs-lookup"><span data-stu-id="cf391-145">Click this icon to rename the role.</span></span> <span data-ttu-id="cf391-146">Název role "SignalRChat" a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf391-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="cf391-147">V **nového projektu ASP.NET MVC 4** průvodce, vyberte **internetovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="cf391-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="cf391-148">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf391-148">Click **OK**.</span></span> <span data-ttu-id="cf391-149">Průvodce projektem vytvoří dva projekty:</span><span class="sxs-lookup"><span data-stu-id="cf391-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="cf391-150">ChatService: Tento projekt je aplikace Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cf391-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="cf391-151">Definuje role Azure a další možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cf391-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="cf391-152">SignalRChat: Tento projekt není projekt ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="cf391-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="cf391-153">Vytvoření chatovací SignalR aplikace</span><span class="sxs-lookup"><span data-stu-id="cf391-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="cf391-154">Vytvoření chatovací aplikace, postupujte podle kroků v tomto kurzu [Začínáme s knihovnou SignalR a MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="cf391-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="cf391-155">Instalace potřebných knihoven pomocí NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf391-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="cf391-156">Z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="cf391-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="cf391-157">V **Konzola správce balíčků** okno, zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="cf391-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="cf391-158">Použití `-ProjectName` možnost nainstalovat balíčky do projektu ASP.NET MVC, nikoli projekt Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="cf391-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="cf391-159">Konfigurace propojovacího rozhraní</span><span class="sxs-lookup"><span data-stu-id="cf391-159">Configure the Backplane</span></span>

<span data-ttu-id="cf391-160">V souboru Global.asax vaší aplikace přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="cf391-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="cf391-161">Teď budete muset získat připojovací řetězec service bus.</span><span class="sxs-lookup"><span data-stu-id="cf391-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="cf391-162">Na webu Azure Portal vyberte obor názvů služby Service bus, který jste vytvořili a klikněte na ikonu přístupový klíč.</span><span class="sxs-lookup"><span data-stu-id="cf391-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="cf391-163">Zkopírujte připojovací řetězec do schránky a vložte ho do *connectionString* proměnné.</span><span class="sxs-lookup"><span data-stu-id="cf391-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="cf391-164">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="cf391-164">Deploy to Azure</span></span>

<span data-ttu-id="cf391-165">V Průzkumníku řešení rozbalte **role** složky v projektu ChatService.</span><span class="sxs-lookup"><span data-stu-id="cf391-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="cf391-166">Klikněte pravým tlačítkem na roli SignalRChat a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="cf391-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="cf391-167">Vyberte **konfigurace** kartu. V části **instance** vyberte 2.</span><span class="sxs-lookup"><span data-stu-id="cf391-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="cf391-168">Můžete také nastavit velikost virtuálního počítače **nejmenším instancím**.</span><span class="sxs-lookup"><span data-stu-id="cf391-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="cf391-169">Uložte změny.</span><span class="sxs-lookup"><span data-stu-id="cf391-169">Save the changes.</span></span>

<span data-ttu-id="cf391-170">V Průzkumníku řešení klikněte pravým tlačítkem na projekt ChatService.</span><span class="sxs-lookup"><span data-stu-id="cf391-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="cf391-171">Vyberte **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="cf391-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="cf391-172">Pokud je toto vaše první čas publikování na platformě Windows Azure, je nutné stáhnout svoje přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cf391-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="cf391-173">V **publikovat** průvodce, klikněte na tlačítko "Přihlásit a stáhnout přihlašovací údaje".</span><span class="sxs-lookup"><span data-stu-id="cf391-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="cf391-174">To vás vyzve k přihlášení na webu Windows Azure portal a stáhněte si soubor nastavení publikování.</span><span class="sxs-lookup"><span data-stu-id="cf391-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="cf391-175">Klikněte na tlačítko **Import** a vyberte soubor nastavení publikování, který jste stáhli.</span><span class="sxs-lookup"><span data-stu-id="cf391-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="cf391-176">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="cf391-176">Click **Next**.</span></span> <span data-ttu-id="cf391-177">V **nastavení publikování** dialogového okna, v části **Cloudovou službu**, vyberte cloudovou službu, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="cf391-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="cf391-178">Klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="cf391-178">Click **Publish**.</span></span> <span data-ttu-id="cf391-179">Může trvat pár minut a nasaďte aplikaci a spustit virtuální počítače.</span><span class="sxs-lookup"><span data-stu-id="cf391-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="cf391-180">Nyní při spuštění aplikace chat instance rolí komunikovat přes Azure Service Bus pomocí tématu služby Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cf391-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="cf391-181">Téma je fronty zpráv, který umožňuje několik předplatitelů.</span><span class="sxs-lookup"><span data-stu-id="cf391-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="cf391-182">Propojovacího rozhraní automaticky vytvoří téma a předplatná.</span><span class="sxs-lookup"><span data-stu-id="cf391-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="cf391-183">Pokud chcete zobrazit předplatná a zprávu aktivity, otevřete na webu Azure portal, vyberte obor názvů služby Service Bus a klikněte na "Tématech".</span><span class="sxs-lookup"><span data-stu-id="cf391-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="cf391-184">Ujistěte se, trvat několik minut, než se aktivita zpráva se zobrazí na řídicím panelu.</span><span class="sxs-lookup"><span data-stu-id="cf391-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="cf391-185">Funkce SignalR spravuje životnost tématu.</span><span class="sxs-lookup"><span data-stu-id="cf391-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="cf391-186">Tak dlouho, dokud je vaše aplikace nasazena, nepokoušejte ručně odstraňte témata nebo změnit nastavení v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="cf391-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
