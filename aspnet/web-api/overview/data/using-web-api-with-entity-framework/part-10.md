---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Publikujte aplikaci do Azure App Service v Azure | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: 5c1a70ceded85681046065881f62c5c95c5d8740
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076741"
---
<a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="30de7-102">Publikujte aplikaci do Azure App Service v Azure</span><span class="sxs-lookup"><span data-stu-id="30de7-102">Publish the App to Azure Azure App Service</span></span>
====================
<span data-ttu-id="30de7-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="30de7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="30de7-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="30de7-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="30de7-105">V posledním kroku budete publikovat aplikaci do Azure.</span><span class="sxs-lookup"><span data-stu-id="30de7-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="30de7-106">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="30de7-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="30de7-107">Kliknutím na **publikovat** vyvolá **publikování webu** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="30de7-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="30de7-108">Pokud jste zaškrtli možnost **hostitel v cloudu** při prvním vytvoření projektu a pak připojení a nastavení jsou už nakonfigurovaná.</span><span class="sxs-lookup"><span data-stu-id="30de7-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="30de7-109">V takovém případě stačí kliknout **nastavení** kartě a zaškrtněte &quot;spustit migrace Code First&quot;.</span><span class="sxs-lookup"><span data-stu-id="30de7-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="30de7-110">(Pokud jste nezaškrtli **hostitel v cloudu** na začátku, postupujte podle pokynů v [další části](#new-website).)</span><span class="sxs-lookup"><span data-stu-id="30de7-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="30de7-111">K nasazení aplikace, klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="30de7-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="30de7-112">Můžete zobrazit průběh publikování v **aktivita publikování webu** okna.</span><span class="sxs-lookup"><span data-stu-id="30de7-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="30de7-113">(Z **zobrazení** nabídce vyberte možnost **ostatní Windows**a pak vyberte **aktivita publikování webu**.)</span><span class="sxs-lookup"><span data-stu-id="30de7-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="30de7-114">Po dokončení nasazení aplikace Visual Studio automaticky otevře výchozí prohlížeč na adresu URL nasazené webové stránky a aplikace, kterou jste vytvořili je nyní spuštěna v cloudu.</span><span class="sxs-lookup"><span data-stu-id="30de7-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="30de7-115">Adresy URL v adresním řádku prohlížeče ukazuje, že lokality se načítá z Internetu.</span><span class="sxs-lookup"><span data-stu-id="30de7-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="30de7-116">Nasazení na nový web</span><span class="sxs-lookup"><span data-stu-id="30de7-116">Deploying to a New Website</span></span>

<span data-ttu-id="30de7-117">Pokud jste nekontrolovaly **hostitel v cloudu** při prvním vytvoření projektu, můžete nakonfigurovat novou webovou aplikaci nyní.</span><span class="sxs-lookup"><span data-stu-id="30de7-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="30de7-118">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="30de7-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="30de7-119">Vyberte **profilu** kartě a klikněte na tlačítko **Microsoft Azure Websites**.</span><span class="sxs-lookup"><span data-stu-id="30de7-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="30de7-120">Pokud ještě nejste momentálně do Azure, se výzva k přihlášení.</span><span class="sxs-lookup"><span data-stu-id="30de7-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="30de7-121">V **existující weby** dialogového okna, klikněte na tlačítko **nový**.</span><span class="sxs-lookup"><span data-stu-id="30de7-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="30de7-122">Zadejte název lokality.</span><span class="sxs-lookup"><span data-stu-id="30de7-122">Enter a site name.</span></span> <span data-ttu-id="30de7-123">Vyberte předplatné a oblast.</span><span class="sxs-lookup"><span data-stu-id="30de7-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="30de7-124">V části **databázový server**vyberte **vytvořit nový Server**, nebo vyberte existující server.</span><span class="sxs-lookup"><span data-stu-id="30de7-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="30de7-125">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="30de7-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="30de7-126">Klikněte na tlačítko **nastavení** kartě a zaškrtněte &quot;spustit migrace Code First&quot;.</span><span class="sxs-lookup"><span data-stu-id="30de7-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="30de7-127">Pak klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="30de7-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="30de7-128">Předchozí</span><span class="sxs-lookup"><span data-stu-id="30de7-128">Previous</span></span>](part-9.md)
