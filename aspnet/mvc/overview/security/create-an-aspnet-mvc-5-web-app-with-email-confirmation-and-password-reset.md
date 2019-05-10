---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, e-mailu potvrzení a resetováním hesla (C#) | Dokumentace Microsoftu
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 s e-mailové potvrzení a resetování hesla pomocí systém členství technologie ASP.NET Identity. Můžete certifikační autority...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: ebdae3f4d1261407feecd50ec81b3f329b2a3c0c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117130"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="887ef-104">Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla (C#)</span><span class="sxs-lookup"><span data-stu-id="887ef-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="887ef-105">Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="887ef-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="887ef-106">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 s e-mailové potvrzení a resetování hesla pomocí systém členství technologie ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="887ef-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="887ef-107">Můžete stáhnout hotovou aplikaci [tady](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="887ef-107">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="887ef-108">Položka ke stažení obsahuje ladění pomocné rutiny, které umožňují otestovat bez nastavení e-mailem nebo poskytovatele služby SMS serveru SMS a e-mailové potvrzení.</span><span class="sxs-lookup"><span data-stu-id="887ef-108">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="887ef-109">V tomto kurzu zapsal [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="887ef-109">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="887ef-110">Vytvoření aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="887ef-110">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="887ef-111">Začněte tím, že instalaci a používání [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="887ef-111">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="887ef-112">Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="887ef-112">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="887ef-113">Upozornění: Je nutné nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší, k dokončení tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="887ef-113">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="887ef-114">Vytvoření nového projektu ASP.NET Web a vyberte šablonu MVC.</span><span class="sxs-lookup"><span data-stu-id="887ef-114">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="887ef-115">Webové formuláře také podporuje ASP.NET Identity, takže může podle podobných kroků ve webové aplikaci formulářů.</span><span class="sxs-lookup"><span data-stu-id="887ef-115">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="887ef-116">Ponechte výchozí ověřování jako **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="887ef-116">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="887ef-117">Pokud chcete hostovat aplikace ve službě Azure, ponechte políčko zaškrtnuté.</span><span class="sxs-lookup"><span data-stu-id="887ef-117">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="887ef-118">Později v tomto kurzu nasadíme do Azure.</span><span class="sxs-lookup"><span data-stu-id="887ef-118">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="887ef-119">Je možné [zdarma otevřít účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="887ef-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="887ef-120">Nastavte [projektu pro použití protokolu SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="887ef-120">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="887ef-121">Spuštění aplikace, klikněte na tlačítko **zaregistrovat** propojit a zaregistrovat uživatele.</span><span class="sxs-lookup"><span data-stu-id="887ef-121">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="887ef-122">V tomto okamžiku je pouze ověření na e-mailu [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) atribut.</span><span class="sxs-lookup"><span data-stu-id="887ef-122">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="887ef-123">V Průzkumníku serveru přejděte do **Data Connections\DefaultConnection\Tables\AspNetUsers**, klikněte pravým tlačítkem myši a vyberte **Otevřít definici tabulky**.</span><span class="sxs-lookup"><span data-stu-id="887ef-123">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="887ef-124">Na následujícím obrázku `AspNetUsers` schématu:</span><span class="sxs-lookup"><span data-stu-id="887ef-124">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="887ef-125">Klikněte pravým tlačítkem na **AspNetUsers** tabulce a vybrat **zobrazit Data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="887ef-125">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="887ef-126">V tomto okamžiku není potvrzena e-mailu.</span><span class="sxs-lookup"><span data-stu-id="887ef-126">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="887ef-127">Klikněte na řádek a vyberte odstranit.</span><span class="sxs-lookup"><span data-stu-id="887ef-127">Click on the row and select delete.</span></span> <span data-ttu-id="887ef-128">Budete znovu přidat tuto e-mailu v dalším kroku a odeslat e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="887ef-128">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="887ef-129">Potvrzení e-mailu</span><span class="sxs-lookup"><span data-stu-id="887ef-129">Email confirmation</span></span>

<span data-ttu-id="887ef-130">Je osvědčeným postupem je potvrďte e-mailu nové registrace uživatele k ověření, nejsou někdo zosobnění (to znamená, že se ještě nezaregistrovali někoho jiného e-mailu).</span><span class="sxs-lookup"><span data-stu-id="887ef-130">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="887ef-131">Předpokládejme, že jste měli diskusní fórum, chcete zabránit `"bob@example.com"` registroval jako `"joe@contoso.com"`.</span><span class="sxs-lookup"><span data-stu-id="887ef-131">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="887ef-132">Bez potvrzení e-mailu `"joe@contoso.com"` může získat nežádoucí e-mailu vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="887ef-132">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="887ef-133">Předpokládejme, že Bob omylem zaregistrovaný jako `"bib@example.com"` a kdyby si všimli, že nebudou moci používat obnovit heslo, protože aplikace nemá správnou e-mailovou.</span><span class="sxs-lookup"><span data-stu-id="887ef-133">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="887ef-134">Potvrzení e-mailu zajišťuje pouze omezenou ochranu před roboty a neposkytuje ochranu z určené spammery, mají mnoho pracovní e-mailu aliasů můžete použít k registraci.</span><span class="sxs-lookup"><span data-stu-id="887ef-134">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="887ef-135">Obvykle chcete novým uživatelům zabránit v účtování žádná data k webu předtím, než byly potvrzeny e-mailem, textovou zprávu SMS nebo jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="887ef-135">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="887ef-136">V následujících částech budeme povolit e-mailové potvrzení a upravovat kód, který nově zaregistrovaný uživatelům zabránit v přihlašování až do svého e-mailu byl potvrzen.</span><span class="sxs-lookup"><span data-stu-id="887ef-136">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="887ef-137">Připojení SendGrid</span><span class="sxs-lookup"><span data-stu-id="887ef-137">Hook up SendGrid</span></span>

<span data-ttu-id="887ef-138">Pokyny v této části nejsou aktuální.</span><span class="sxs-lookup"><span data-stu-id="887ef-138">The instructions in this section are not current.</span></span> <span data-ttu-id="887ef-139">Zobrazit [poskytovatele e-mailu Sendgridu konfigurace](/aspnet/core/security/authentication/accconfirm#configure-email-provider) pro aktualizace pokynů.</span><span class="sxs-lookup"><span data-stu-id="887ef-139">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="887ef-140">Tento kurz vysvětluje pouze přidání e-mailové oznámení prostřednictvím [SendGrid](http://sendgrid.com/), můžete poslat e-mailu pomocí protokolu SMTP a další mechanismy (naleznete v tématu [další prostředky](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="887ef-140">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="887ef-141">V konzole Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="887ef-141">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="887ef-142">Přejděte [Azure SendGrid registrační stránku](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) a zaregistrujte si bezplatný účet SendGrid.</span><span class="sxs-lookup"><span data-stu-id="887ef-142">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="887ef-143">Konfigurace služby SendGrid přidáním podobně jako v následujícím kódu *App_Start/IdentityConfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="887ef-143">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="887ef-144">Bude potřeba přidat následující zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="887ef-144">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="887ef-145">Pro zjednodušení této ukázku, uložíme nastavení aplikace v *web.config* souboru:</span><span class="sxs-lookup"><span data-stu-id="887ef-145">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="887ef-146">Zabezpečení – nikdy ukládání citlivých dat ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="887ef-146">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="887ef-147">Účet a přihlašovací údaje jsou uložené v nastavení appSetting.</span><span class="sxs-lookup"><span data-stu-id="887ef-147">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="887ef-148">V Azure, můžete bezpečně uložit tyto hodnoty na **[konfigurovat](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** karta na portálu Azure portal.</span><span class="sxs-lookup"><span data-stu-id="887ef-148">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="887ef-149">Zobrazit [osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="887ef-149">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="887ef-150">Povolení e-mailové potvrzení v kontroleru účtu</span><span class="sxs-lookup"><span data-stu-id="887ef-150">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="887ef-151">Ověřte, *Views\Account\ConfirmEmail.cshtml* soubor nemá správnou syntaxí.</span><span class="sxs-lookup"><span data-stu-id="887ef-151">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="887ef-152">(@ Znaků v prvním řádku můžou chybět.</span><span class="sxs-lookup"><span data-stu-id="887ef-152">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="887ef-153">)</span><span class="sxs-lookup"><span data-stu-id="887ef-153">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="887ef-154">Spusťte aplikaci a klikněte na odkaz zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="887ef-154">Run the app and click the Register link.</span></span> <span data-ttu-id="887ef-155">Jakmile odešlete registrační formulář jste přihlášeni.</span><span class="sxs-lookup"><span data-stu-id="887ef-155">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="887ef-156">Zkontrolujte e-mailový účet a klikněte na odkaz pro potvrzení e-mailu.</span><span class="sxs-lookup"><span data-stu-id="887ef-156">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="887ef-157">Vyžadovat e-mailové potvrzení před přihlášení</span><span class="sxs-lookup"><span data-stu-id="887ef-157">Require email confirmation before log in</span></span>

<span data-ttu-id="887ef-158">Aktuálně po dokončení registrační formulář uživatele se přihlásí.</span><span class="sxs-lookup"><span data-stu-id="887ef-158">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="887ef-159">Chcete obecně potvrzení jejich e-mailu před jejich přihlášení.</span><span class="sxs-lookup"><span data-stu-id="887ef-159">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="887ef-160">V níže uvedené části upravíme kód tak, aby vyžadovala nové uživatele, aby potvrzeno e-mailu předtím, než se přihlásí (ověřit).</span><span class="sxs-lookup"><span data-stu-id="887ef-160">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="887ef-161">Aktualizace `HttpPost Register` metodu s následující zvýrazněný změny:</span><span class="sxs-lookup"><span data-stu-id="887ef-161">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="887ef-162">Tak `SignInAsync` metoda, nebude uživatel přihlášený pomocí registrace.</span><span class="sxs-lookup"><span data-stu-id="887ef-162">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="887ef-163">`TempData["ViewBagLink"] = callbackUrl;` Řádku je možné použít k [ladit aplikaci](#dbg) a testování registrace bez odeslání e-mailu.</span><span class="sxs-lookup"><span data-stu-id="887ef-163">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="887ef-164">`ViewBag.Message` slouží k zobrazení pokynů potvrzení.</span><span class="sxs-lookup"><span data-stu-id="887ef-164">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="887ef-165">[Stáhněte si ukázky](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) obsahuje kód pro testování potvrzení e-mailu bez nastavení e-mailu a můžete také použít k ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="887ef-165">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="887ef-166">Vytvoření `Views\Shared\Info.cshtml` a přidejte následující kód razor:</span><span class="sxs-lookup"><span data-stu-id="887ef-166">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="887ef-167">Přidat [Authorize atribut](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) k `Contact` metody akce kontroleru Domovská stránka.</span><span class="sxs-lookup"><span data-stu-id="887ef-167">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="887ef-168">Můžete kliknout na **kontakt** odkaz pro ověření anonymní uživatelé nemají přístup a ověření uživatelé mají přístup.</span><span class="sxs-lookup"><span data-stu-id="887ef-168">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="887ef-169">Také musíte aktualizovat `HttpPost Login` metody akce:</span><span class="sxs-lookup"><span data-stu-id="887ef-169">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="887ef-170">Aktualizace *Views\Shared\Error.cshtml* zobrazení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="887ef-170">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="887ef-171">Odstranit některé účty **AspNetUsers** tabulce, která obsahuje e-mailový alias, který chcete otestovat s.</span><span class="sxs-lookup"><span data-stu-id="887ef-171">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="887ef-172">Spusťte aplikaci a ověřte, že se nemůže přihlásit až se ujistíte e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="887ef-172">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="887ef-173">Jakmile potvrdíte, e-mailovou adresu, klikněte na tlačítko **kontakt** odkaz.</span><span class="sxs-lookup"><span data-stu-id="887ef-173">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="887ef-174">Obnovení/obnovení hesla</span><span class="sxs-lookup"><span data-stu-id="887ef-174">Password recovery/reset</span></span>

<span data-ttu-id="887ef-175">Odebere znaky komentáře z `HttpPost ForgotPassword` metody akce v kontroleru účtu:</span><span class="sxs-lookup"><span data-stu-id="887ef-175">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="887ef-176">Odebere znaky komentáře z `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) v *Views\Account\Login.cshtml* soubor zobrazení razor:</span><span class="sxs-lookup"><span data-stu-id="887ef-176">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="887ef-177">Přihlašovací stránky se nyní zobrazí odkaz resetovat heslo.</span><span class="sxs-lookup"><span data-stu-id="887ef-177">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="887ef-178">Znovu poslat potvrzovací odkaz e-mailu</span><span class="sxs-lookup"><span data-stu-id="887ef-178">Resend email confirmation link</span></span>

<span data-ttu-id="887ef-179">Jakmile uživatel vytvoří nový místní účet, jsou e-mailem odkaz pro potvrzení, které je potřeba použít dřív, než se můžou přihlašovat</span><span class="sxs-lookup"><span data-stu-id="887ef-179">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="887ef-180">Pokud uživatel omylem odstraní potvrzovací e-mail nebo nikdy přijde e-mailu, potřebují potvrzovací odkaz odeslán znovu.</span><span class="sxs-lookup"><span data-stu-id="887ef-180">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="887ef-181">Následující změny kódu ukazují, jak ji povolit.</span><span class="sxs-lookup"><span data-stu-id="887ef-181">The following code changes show how to enable this.</span></span>

<span data-ttu-id="887ef-182">Přidejte následující pomocnou metodu k dolnímu okraji *Controllers\AccountController.cs* souboru:</span><span class="sxs-lookup"><span data-stu-id="887ef-182">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="887ef-183">Aktualizujte metodu registrace pomocí nového pomocníka:</span><span class="sxs-lookup"><span data-stu-id="887ef-183">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="887ef-184">Aktualizujte metodu přihlášení se opětovné poslání heslo, pokud nebyla potvrzena uživatelský účet:</span><span class="sxs-lookup"><span data-stu-id="887ef-184">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="887ef-185">Sloučit účty sociálních sítí a místní přihlášení</span><span class="sxs-lookup"><span data-stu-id="887ef-185">Combine social and local login accounts</span></span>

<span data-ttu-id="887ef-186">Kliknutím na odkaz na vaši e-mailu můžete kombinovat místní a sociální účty.</span><span class="sxs-lookup"><span data-stu-id="887ef-186">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="887ef-187">V následujícím pořadí **RickAndMSFT@gmail.com** se nejprve vytvoří jako místní přihlášení, ale můžete vytvořit účet jako sociální protokolu v prvním a pak přidat místní přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="887ef-187">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="887ef-188">Klikněte na **spravovat** odkaz.</span><span class="sxs-lookup"><span data-stu-id="887ef-188">Click on the **Manage** link.</span></span> <span data-ttu-id="887ef-189">Poznámka: **externí přihlášení: 0** spojený s tímto účtem.</span><span class="sxs-lookup"><span data-stu-id="887ef-189">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="887ef-190">Klikněte na odkaz na jiný protokol služby a přijímání požadavků aplikace.</span><span class="sxs-lookup"><span data-stu-id="887ef-190">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="887ef-191">Byli sloučeni dva účty, budou moct přihlásit pomocí obou.</span><span class="sxs-lookup"><span data-stu-id="887ef-191">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="887ef-192">Můžete chtít uživatelům přidat místní účty v případě jejich sociálních sítí protokolu ve službě ověřování je mimo provoz nebo spíše se ztratili přístup k jejich účtu na sociální síti.</span><span class="sxs-lookup"><span data-stu-id="887ef-192">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="887ef-193">Na následujícím obrázku je Petr sociální přihlášení (které si můžete všimnout **externí přihlášení: 1** zobrazený na stránce).</span><span class="sxs-lookup"><span data-stu-id="887ef-193">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="887ef-194">Kliknutím na **výběru hesla** umožňuje přidat místního protokolu na spojené se stejným účtem.</span><span class="sxs-lookup"><span data-stu-id="887ef-194">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="887ef-195">Potvrzení e-mailu do větší hloubky</span><span class="sxs-lookup"><span data-stu-id="887ef-195">Email confirmation in more depth</span></span>

<span data-ttu-id="887ef-196">Tento kurz [potvrzení účtu a obnovení hesla s ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) přejde do tohoto tématu, s dalšími podrobnostmi.</span><span class="sxs-lookup"><span data-stu-id="887ef-196">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="887ef-197">Ladění aplikace</span><span class="sxs-lookup"><span data-stu-id="887ef-197">Debugging the app</span></span>

<span data-ttu-id="887ef-198">Pokud se vám e-mail s odkazem:</span><span class="sxs-lookup"><span data-stu-id="887ef-198">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="887ef-199">Zkontrolujte složku s nevyžádanou nebo nevyžádané pošty.</span><span class="sxs-lookup"><span data-stu-id="887ef-199">Check your junk or spam folder.</span></span>
- <span data-ttu-id="887ef-200">Přihlaste se do účtu SendGrid a klikněte na [odkaz e-mailu aktivita](https://sendgrid.com/logs/index).</span><span class="sxs-lookup"><span data-stu-id="887ef-200">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="887ef-201">Chcete-li otestovat odkaz pro ověření bez e-mailu, stáhněte si [úplnou vzorovou](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="887ef-201">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="887ef-202">Potvrzovací odkaz potvrzení kódy se zobrazí na stránce.</span><span class="sxs-lookup"><span data-stu-id="887ef-202">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="887ef-203">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="887ef-203">Additional Resources</span></span>

- [<span data-ttu-id="887ef-204">Odkazy na ASP.NET Identity doporučené zdroje informací</span><span class="sxs-lookup"><span data-stu-id="887ef-204">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="887ef-205">[Potvrzení účtu a obnovení hesla s ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) obsahuje větší podrobnosti o potvrzení hesla obnovení a účtu.</span><span class="sxs-lookup"><span data-stu-id="887ef-205">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="887ef-206">[Aplikace MVC 5 s Facebook, Twitter, LinkedIn a Google OAuth2 přihlašování](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) v tomto kurzu se dozvíte, jak psát aplikace ASP.NET MVC 5 s autorizací Facebook nebo Google OAuth 2.</span><span class="sxs-lookup"><span data-stu-id="887ef-206">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="887ef-207">Také ukazuje, jak přidat další data do databáze nástroje Identity.</span><span class="sxs-lookup"><span data-stu-id="887ef-207">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="887ef-208">[Nasaďte zabezpečené aplikace ASP.NET MVC pomocí členství, OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="887ef-208">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="887ef-209">V tomto kurzu přidá nasazení v Azure, jak zabezpečit vaši aplikaci s rolemi, jak můžete členské rozhraní API přidávat uživatele a role a další funkce zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="887ef-209">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="887ef-210">Vytvoření aplikace služby Google OAuth 2 a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="887ef-210">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="887ef-211">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="887ef-211">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="887ef-212">Nastavení protokolu SSL v projektu</span><span class="sxs-lookup"><span data-stu-id="887ef-212">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
