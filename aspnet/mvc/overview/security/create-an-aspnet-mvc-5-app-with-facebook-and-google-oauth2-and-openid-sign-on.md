---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Vytvořte aplikaci MVC 5 s facebookem, twitterem, linkedinem a přihlášením Google OAuth2 (C#) | Dokumenty společnosti Microsoft
author: Rick-Anderson
description: Tento výukový program vám ukáže, jak vytvořit ASP.NET MVC 5 webové aplikace, která umožňuje uživatelům přihlásit pomocí OAuth 2.0 s pověřeními z externíauaulce...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676319"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="ca5ad-103">Vytvoření aplikace ASP.NET MVC 5 s přihlášením přes Facebook, Twitter, LinkedIn a Google OAuth2 (C#)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="ca5ad-104">podle [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ca5ad-105">V tomto kurzu se můžete naučit vytvořit ASP.NET webové aplikace MVC 5, která uživatelům umožňuje přihlásit se pomocí [aplikace OAuth 2.0](http://oauth.net/2/) pomocí přihlašovacích údajů od externího poskytovatele ověřování, jako je Facebook, Twitter, LinkedIn, Microsoft nebo Google.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="ca5ad-106">Pro jednoduchost se tento kurz zaměřuje na práci s pověřeními od Facebooku a Googlu.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="ca5ad-107">Povolení těchto pověření na webových stránkách poskytuje významnou výhodu, protože miliony uživatelů již mají účty u těchto externích poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="ca5ad-108">Tito uživatelé mohou být více nakloněni k registraci na vašem webu, pokud nebudou muset vytvářet a pamatovat si novou sadu pověření.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="ca5ad-109">Viz také [ASP.NET aplikaci MVC 5 s SMS a e-mailem Dvoufaktorové ověřování](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="ca5ad-110">Kurz také ukazuje, jak přidat data profilu pro uživatele a jak používat rozhraní API členství k přidání rolí.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="ca5ad-111">Tento výukový program byl napsán [Rick Anderson](https://blogs.msdn.com/rickAndy) [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Prosím, následujte mě na Twitteru: ).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="ca5ad-112">začínáme</span><span class="sxs-lookup"><span data-stu-id="ca5ad-112">Getting Started</span></span>

<span data-ttu-id="ca5ad-113">Začněte instalací a spuštěním [sady Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="ca5ad-114">Nainstalujte visual studio [2013 aktualizace 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="ca5ad-115">O pomoc s Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, a další, viz tento [ukázkový projekt](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="ca5ad-116">Chcete-li používat Google OAuth 2 a ladit místně bez upozornění SSL, je nutné nainstalovat aktualizaci Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="ca5ad-117">Na **úvodní** stránce klikněte na **Nový projekt,** nebo můžete použít nabídku a vybrat **Soubor**a potom **nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="ca5ad-118">Vytvoření první aplikace</span><span class="sxs-lookup"><span data-stu-id="ca5ad-118">Creating Your First Application</span></span>

<span data-ttu-id="ca5ad-119">Klepněte na **tlačítko Nový projekt**, potom vyberte možnost Visual **C#** vlevo, potom na **Web** a pak vyberte **ASP.NET webovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ca5ad-120">Pojmenujte projekt "MvcAuth" a klepněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="ca5ad-121">V dialogovém **okně Nový ASP.NET projektu** klepněte na tlačítko **MVC**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="ca5ad-122">Pokud ověřování není **individuální uživatelské účty**, klepněte na tlačítko Změnit **ověřování** a vyberte jednotlivé **uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="ca5ad-123">Kontrolou **Hostitele v cloudu**bude velmi snadné hostovat v Azure.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="ca5ad-124">Pokud jste **v cloudu**vybrali možnost Host , vyplňte dialogové okno konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="ca5ad-125">Použití NuGet k aktualizaci na nejnovější middleware OWIN</span><span class="sxs-lookup"><span data-stu-id="ca5ad-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="ca5ad-126">Pomocí správce balíčků NuGet aktualizujte [middleware OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="ca5ad-127">V levé nabídce vyberte **Aktualizace.**</span><span class="sxs-lookup"><span data-stu-id="ca5ad-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="ca5ad-128">Můžete kliknout na tlačítko **Aktualizovat vše** nebo můžete vyhledávat pouze balíčky OWIN (zobrazeno na následujícím obrázku):</span><span class="sxs-lookup"><span data-stu-id="ca5ad-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="ca5ad-129">Na obrázku níže jsou zobrazeny pouze balíčky OWIN:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="ca5ad-130">Z konzoly Správce balíčků (PMC) `Update-Package` můžete zadat příkaz, který aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="ca5ad-131">Stisknutím **kláves F5** nebo **Ctrl+F5** aplikaci spusťte.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="ca5ad-132">Na obrázku níže je číslo portu 1234.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="ca5ad-133">Při spuštění aplikace se zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="ca5ad-134">V závislosti na velikosti okna prohlížeče může být nutné kliknout na ikonu **navigace,** aby se zobce, informace **o** **tom, kontakt**, **registrace** a **přihlášení.**</span><span class="sxs-lookup"><span data-stu-id="ca5ad-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="ca5ad-135">Nastavení ssl v projektu</span><span class="sxs-lookup"><span data-stu-id="ca5ad-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="ca5ad-136">Chcete-li se připojit k poskytovatelům ověřování, jako je Google a Facebook, budete muset nastavit službu IIS-Express, aby používala protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="ca5ad-137">Je důležité, aby i po přihlášení používat SSL a neklesnout zpět na HTTP, vaše přihlašovací cookie je stejně tajné jako vaše uživatelské jméno a heslo, a bez použití SSL posíláte jej v prostém textu přes drát.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="ca5ad-138">Kromě toho jste již udělali čas na provedení handshake a zabezpečení kanálu (což je převážná část toho, co dělá HTTPS pomalejší než HTTP) před spuštěním kanálu MVC, takže přesměrování zpět na HTTP po přihlášení nebude provádět aktuální požadavek nebo budoucí požadavky mnohem rychleji.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="ca5ad-139">V **Průzkumníku řešení**klepněte na projekt **MvcAuth.**</span><span class="sxs-lookup"><span data-stu-id="ca5ad-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="ca5ad-140">Chcete-li zobrazit vlastnosti projektu, stiskněte klávesu F4.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="ca5ad-141">Případně můžete v nabídce **Zobrazit** vybrat **možnost Vlastnosti okna**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="ca5ad-142">Změnit **ssl povoleno** na hodnotu True.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="ca5ad-143">Zkopírujte adresu URL SSL `https://localhost:44300/` (která bude, pokud jste nevytvořili jiné projekty SSL).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="ca5ad-144">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt **MvcAuth** a vyberte příkaz **Vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="ca5ad-145">Vyberte **webovou** kartu a vložte adresu URL SSL do pole **Adresa URL projektu.**</span><span class="sxs-lookup"><span data-stu-id="ca5ad-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="ca5ad-146">Uložte soubor (Ctl+S).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="ca5ad-147">Tuto adresu URL budete potřebovat ke konfiguraci aplikací pro ověřování na Facebooku a Google.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="ca5ad-148">Přidejte do `Home` řadiče atribut [RequireHttps,](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) který vyžaduje všechny požadavky, musí používat protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="ca5ad-149">Bezpečnější přístup je přidat [requireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtr do aplikace.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="ca5ad-150">Podívejte se &quot;na část Chraňte aplikaci&quot; s SSL a autorizovat atribut v mém kurzu [Vytvořit ASP.NET mvc aplikace s auth a SQL DB a nasadit do služby Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ca5ad-151">Část ovladače Home je uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="ca5ad-152">Stiskněte klávesy CTRL+F5 a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="ca5ad-153">Pokud jste certifikát nainstalovali v minulosti, můžete přeskočit zbytek této části a přejít na [vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](#goog), jinak postupujte podle pokynů, abyste důvěřovali certifikátu podepsanému svým držitelem, který služba IIS Express vygenerovala.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="ca5ad-154">Přečtěte si dialogové okno **Upozornění zabezpečení** a klepněte na tlačítko **Ano,** pokud chcete nainstalovat certifikát představující localhost.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="ca5ad-155">Aplikace IE zobrazuje *domovskou* stránku a neexistují žádná upozornění SSL.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="ca5ad-156">Google Chrome také přijímá certifikát a zobrazuje obsah HTTPS bez varování.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="ca5ad-157">Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="ca5ad-158">Pro naši aplikaci můžete bezpečně kliknout **Chápu rizika**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ca5ad-159">Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="ca5ad-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ca5ad-160">Aktuální pokyny google oauth [najdete v tématu Konfigurace ověřování Google v ASP.NET jádra](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="ca5ad-161">Přejděte do [konzole Google Developers Console](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="ca5ad-162">Pokud jste projekt ještě nevytvořili, vyberte na levé kartě **pověření** a pak vyberte **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="ca5ad-163">Na levé kartě klikněte na **Pověření**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="ca5ad-164">Klepněte na tlačítko **Vytvořit pověření** a potom na **ID klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="ca5ad-165">V dialogovém okně **Vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="ca5ad-166">Nastavte autorizované počátky **JavaScriptu** na adresu URL`https://localhost:44300/` SSL, kterou jste použili výše (pokud jste nevytvořili jiné projekty SSL)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="ca5ad-167">Nastavte **identifikátor URI autorizovaného přesměrování** na:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="ca5ad-168">Klikněte na položku nabídky obrazovky Souhlas OAuth a nastavte e-mailovou adresu a název produktu.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="ca5ad-169">Po dokončení formuláře klepněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="ca5ad-170">Klikněte na položku nabídky Knihovna, vyhledejte **rozhraní GOOGLE+ API**, klikněte na ni a stiskněte tlačítko Povolit.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="ca5ad-171">Na obrázku níže jsou zobrazena povolená rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="ca5ad-172">Ve Správci rozhraní API Google navštivte kartu **Přihlašovací údaje** a získejte **ID klienta**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="ca5ad-173">Stažením uložíte soubor JSON s tajnými kódy aplikací.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="ca5ad-174">Zkopírujte a vložte **ClientId** `UseGoogleAuthentication` a **ClientSecret** do metody nalezené v souboru *Startup.Auth.cs* ve složce *App_Start.*</span><span class="sxs-lookup"><span data-stu-id="ca5ad-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="ca5ad-175">**ClientId** a **ClientSecret** hodnoty uvedené níže jsou ukázky a nefungují.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="ca5ad-176">Zabezpečení – Nikdy neukládejte citlivá data do zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="ca5ad-177">Účet a pověření jsou přidány do výše uvedeného kódu, aby vzorek jednoduché.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="ca5ad-178">Podívejte se [na doporučené postupy pro nasazování hesel a dalších citlivých dat do ASP.NET a Služby Aplikací Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="ca5ad-179">Stisknutím **kláves CTRL+F5** vytvořte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="ca5ad-180">Klikněte na odkaz **Přihlásit** se.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="ca5ad-181">V části **Přihlaste se pomocí jiné služby** **na**Google .</span><span class="sxs-lookup"><span data-stu-id="ca5ad-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="ca5ad-182">Pokud zmeškáte některý z výše uvedených kroků, dostanete chybu HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="ca5ad-183">Zkontrolujte výše uvedené kroky.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-183">Recheck your steps above.</span></span> <span data-ttu-id="ca5ad-184">Pokud vám chybí požadované nastavení (například **název produktu**), přidejte chybějící položku a uložte; může trvat několik minut, než ověření funguje.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="ca5ad-185">Budete přesměrováni na web Google, kde zadáte své přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="ca5ad-186">Po zadání přihlašovacích údajů budete vyzváni k udělení oprávnění webové aplikaci, kterou jste právě vytvořili:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="ca5ad-187">Klikněte na **Přijmout**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-187">Click **Accept**.</span></span> <span data-ttu-id="ca5ad-188">Nyní budete přesměrováni zpět na **registrační** stránku aplikace MvcAuth, kde můžete zaregistrovat svůj účet Google.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="ca5ad-189">Máte možnost změnit místní název registrace e-mailu používaný pro váš účet Gmail, ale obecně chcete zachovat výchozí e-mailový alias (to znamená ten, který jste použili pro ověřování).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="ca5ad-190">Klepněte na tlačítko **Registrovat**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ca5ad-191">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="ca5ad-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ca5ad-192">Aktuální pokyny k ověřování na Facebooku OAuth2 [najdete v tématu Konfigurace ověřování na Facebooku.](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="ca5ad-193">Zkontrolujte údaje o členství</span><span class="sxs-lookup"><span data-stu-id="ca5ad-193">Examine the Membership Data</span></span>

<span data-ttu-id="ca5ad-194">V nabídce **Zobrazení** klepněte na **položku Průzkumník serveru**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="ca5ad-195">Rozbalte **možnost Výchozí připojení (MvcAuth),** rozbalte **položku Tabulky**, klepněte pravým tlačítkem myši na **položku AspNetUsers** a klepněte na příkaz **Zobrazit data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![data tabulky aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="ca5ad-197">Přidání dat profilu do třídy uživatele</span><span class="sxs-lookup"><span data-stu-id="ca5ad-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="ca5ad-198">V této části přidáte datum narození a rodné město k uživatelským datům při registraci, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg s domovním městem a Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="ca5ad-200">Otevřete soubor *Models\IdentityModels.cs* a přidejte datum narození a vlastnosti domovského města:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="ca5ad-201">Otevřete soubor *Models\AccountViewModels.cs* a nastavené datum `ExternalLoginConfirmationViewModel`narození a vlastnosti domovského města v .</span><span class="sxs-lookup"><span data-stu-id="ca5ad-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="ca5ad-202">Otevřete soubor *Controllers\AccountController.cs* a přidejte kód pro `ExternalLoginConfirmation` datum narození a domovské město v metodě akce, jak je znázorněno:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="ca5ad-203">Přidejte datum narození a rodné město do souboru *Views\Account\ExternalLoginConfirmation.cshtml:*</span><span class="sxs-lookup"><span data-stu-id="ca5ad-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="ca5ad-204">Odstraňte databázi členství, abyste mohli znovu zaregistrovat svůj účet na Facebooku u své aplikace a ověřit, že můžete přidat nové datum narození a informace o profilu domovského města.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="ca5ad-205">V **Průzkumníku řešení**klepněte na ikonu **Zobrazit všechny soubory,** potom klepněte pravým tlačítkem myši na příkaz Přidat *\_data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* a klepněte na příkaz **Odstranit**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="ca5ad-206">V nabídce **Nástroje** klikněte na **Položku Manger balíčků NuGet**a potom klikněte na **konzolu Správce balíčků** (PMC).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="ca5ad-207">Do pmc zadejte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="ca5ad-208">Povolit migrace</span><span class="sxs-lookup"><span data-stu-id="ca5ad-208">Enable-Migrations</span></span>
2. <span data-ttu-id="ca5ad-209">Init pro migraci doplňků</span><span class="sxs-lookup"><span data-stu-id="ca5ad-209">Add-Migration Init</span></span>
3. <span data-ttu-id="ca5ad-210">Aktualizovat databázi</span><span class="sxs-lookup"><span data-stu-id="ca5ad-210">Update-Database</span></span>

<span data-ttu-id="ca5ad-211">Spusťte aplikaci a použijte FaceBook a Google pro přihlášení a registraci některých uživatelů.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="ca5ad-212">Zkontrolujte údaje o členství</span><span class="sxs-lookup"><span data-stu-id="ca5ad-212">Examine the Membership Data</span></span>

<span data-ttu-id="ca5ad-213">V nabídce **Zobrazení** klepněte na **položku Průzkumník serveru**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="ca5ad-214">Klepněte pravým tlačítkem myši na **příkaz AspNetUsers** a klepněte na příkaz **Zobrazit data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="ca5ad-215">Pole `HomeTown` `BirthDate` a jsou uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="ca5ad-216">Odhlášení aplikace a přihlášení pomocí jiného účtu</span><span class="sxs-lookup"><span data-stu-id="ca5ad-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="ca5ad-217">Pokud se k aplikaci přihlásíte pomocí Facebooku a pak se odhlásíte a pokusíte se znovu přihlásit pomocí jiného účtu na Facebooku (pomocí stejného prohlížeče), budete okamžitě přihlášeni k předchozímu účtu na Facebooku, který jste použili.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="ca5ad-218">Chcete-li používat jiný účet, musíte přejít na Facebook a odhlásit se na Facebooku.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="ca5ad-219">Stejné pravidlo platí pro všechny ostatní zprostředkovatele ověřování třetích stran.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="ca5ad-220">Případně se můžete přihlásit pomocí jiného účtu pomocí jiného prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca5ad-221">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ca5ad-221">Next Steps</span></span>

<span data-ttu-id="ca5ad-222">Viz [Představujeme Yahoo a LinkedIn OAuth poskytovatelů zabezpečení pro OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Jerrie Pelser pro Yahoo a LinkedIn pokyny.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="ca5ad-223">Viz Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="ca5ad-224">Postupujte podle mého kurzu [Vytvořte aplikaci ASP.NET MVC s auth a SQL DB a nasadit do služby Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), která pokračuje v tomto kurzu a ukazuje následující:</span><span class="sxs-lookup"><span data-stu-id="ca5ad-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="ca5ad-225">Jak nasadit aplikaci do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="ca5ad-226">Jak zabezpečit aplikaci s rolemi.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="ca5ad-227">Jak zabezpečit aplikaci pomocí filtrů [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) a [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="ca5ad-228">Jak používat rozhraní API pro členství k přidání uživatelů a rolí.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="ca5ad-229">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="ca5ad-230">Můžete také požádat o nová témata na [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="ca5ad-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="ca5ad-231">Můžete dokonce požádat o nové funkce, které mají být přidány do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="ca5ad-232">Můžete například hlasovat pro nástroj pro [vytváření a správu uživatelů a rolí.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="ca5ad-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="ca5ad-233">Správné vysvětlení fungování ASP.NET externích ověřovacích služeb naleznete v tématu Externí [ověřovací služby](https://asp.net/web-api/overview/security/external-authentication-services)Roberta McMurrayho .</span><span class="sxs-lookup"><span data-stu-id="ca5ad-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="ca5ad-234">Robert článek také jde do podrobností v povolení Microsoft a Twitter ověřování.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="ca5ad-235">Vynikající [ef/MVC kurz](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Toma Dykstra ukazuje, jak pracovat s rámcem entity.</span><span class="sxs-lookup"><span data-stu-id="ca5ad-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
