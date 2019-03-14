---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: Vytvoření ASP.NET Web Forms aplikace pomocí Dvojúrovňového ověřování pomocí SMS (C#) | Dokumentace Microsoftu
author: Erikre
description: V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET s dvoufaktorovým ověřováním. V tomto kurzu je navržená k doplnění kurz s názvem Cr...
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 7ad3b7a453a40f2708902ae5b9e5cb75b931d54d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067228"
---
<a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a><span data-ttu-id="5b066-104">Vytvoření aplikace webových formulářů ASP.NET s dvoufaktorovým ověřováním prostřednictvím SMS (C#)</span><span class="sxs-lookup"><span data-stu-id="5b066-104">Create an ASP.NET Web Forms app with SMS Two-Factor Authentication (C#)</span></span>
====================
<span data-ttu-id="5b066-105">by [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="5b066-105">by [Erik Reitan](https://github.com/Erikre)</span></span>

[<span data-ttu-id="5b066-106">Stáhněte si aplikaci rozhraní ASP.NET Web Forms s e-mailu a Dvojúrovňového ověřování pomocí SMS</span><span class="sxs-lookup"><span data-stu-id="5b066-106">Download ASP.NET Web Forms App with Email and SMS Two-Factor Authentication</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> <span data-ttu-id="5b066-107">V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET s dvoufaktorovým ověřováním.</span><span class="sxs-lookup"><span data-stu-id="5b066-107">This tutorial shows you how to build an ASP.NET Web Forms app with Two-Factor Authentication.</span></span> <span data-ttu-id="5b066-108">V tomto kurzu je navržená k doplnění kurz s názvem [vytvoření zabezpečené aplikace webových formulářů ASP.NET s registrací uživatele, e-mailové potvrzení a resetováním hesla](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).</span><span class="sxs-lookup"><span data-stu-id="5b066-108">This tutorial was designed to complement the tutorial titled [Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).</span></span> <span data-ttu-id="5b066-109">Kromě toho tento kurz je založený na Rick Anderson [kurz ASP.NET MVC](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5b066-109">In addition, this tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>


## <a name="introduction"></a><span data-ttu-id="5b066-110">Úvod</span><span class="sxs-lookup"><span data-stu-id="5b066-110">Introduction</span></span>

<span data-ttu-id="5b066-111">Tento kurz vás provede kroky potřebné k vytvoření aplikace webových formulářů ASP.NET, která podporuje Dvojúrovňového ověřování pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b066-111">This tutorial guides you through the steps required to create an ASP.NET Web Forms application that supports Two-Factor Authentication using Visual Studio.</span></span> <span data-ttu-id="5b066-112">Dvoufaktorové ověřování je krok ověřování navíc uživatele.</span><span class="sxs-lookup"><span data-stu-id="5b066-112">Two-Factor Authentication is an extra user authentication step.</span></span> <span data-ttu-id="5b066-113">Tento další krok vygeneruje jedinečné osobní identifikační číslo (PIN) během přihlašování.</span><span class="sxs-lookup"><span data-stu-id="5b066-113">This extra step generates a unique personal identification number (PIN) during sign-in.</span></span> <span data-ttu-id="5b066-114">PIN kód se obvykle odesílají uživateli jako e-mailu nebo SMS zprávy.</span><span class="sxs-lookup"><span data-stu-id="5b066-114">The PIN is commonly sent to the user as an email or SMS message.</span></span> <span data-ttu-id="5b066-115">Při přihlášení uživatele vaší aplikace potom zadá PIN kód jako opatření další ověřování.</span><span class="sxs-lookup"><span data-stu-id="5b066-115">The user of your app then enters the PIN as an extra authentication measure when signing-in.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="5b066-116">Kurz úkoly a informace:</span><span class="sxs-lookup"><span data-stu-id="5b066-116">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="5b066-117">Vytvoření aplikace ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="5b066-117">Create an ASP.NET Web Forms App</span></span>](#createWebForms)
- [<span data-ttu-id="5b066-118">Instalace služby SMS a dvoufaktorového ověřování</span><span class="sxs-lookup"><span data-stu-id="5b066-118">Setup SMS and Two-Factor Authentication</span></span>](#SMS)
- [<span data-ttu-id="5b066-119">Povolení dvoufaktorového ověřování pro registrovaný uživatel</span><span class="sxs-lookup"><span data-stu-id="5b066-119">Enable Two-Factor Authentication for Registered User</span></span>](#use2FA)
- [<span data-ttu-id="5b066-120">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="5b066-120">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="5b066-121">Vytvoření aplikace ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="5b066-121">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="5b066-122">Začněte tím, že instalaci a používání [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="5b066-122">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="5b066-123">Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší také.</span><span class="sxs-lookup"><span data-stu-id="5b066-123">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span> <span data-ttu-id="5b066-124">Kromě toho budete muset vytvořit [Twilio](https://www.twilio.com/try-twilio) účtu, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="5b066-124">Also, you will need to create a [Twilio](https://www.twilio.com/try-twilio) account, as explained below.</span></span>

> [!NOTE]
> <span data-ttu-id="5b066-125">Důležité: Je nutné nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší, k dokončení tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="5b066-125">Important: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="5b066-126">Vytvoření nového projektu (**souboru**  - &gt; **nový projekt**) a vyberte **webová aplikace ASP.NET** šablony spolu s rozhraní .NET Framework od verze 4.5.2 **nový projekt** dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="5b066-126">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template along with the .NET Framework version 4.5.2 from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="5b066-127">Z **nový projekt ASP.NET** dialogové okno, vyberte **webových formulářů** šablony.</span><span class="sxs-lookup"><span data-stu-id="5b066-127">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="5b066-128">Ponechte výchozí ověřování jako **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="5b066-128">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="5b066-129">Potom klikněte na **OK** k vytvoření nového projektu.</span><span class="sxs-lookup"><span data-stu-id="5b066-129">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="5b066-130">![Dialogové okno Nový projekt ASP.NET](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5b066-130">![New ASP.NET Project dialog box](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)</span></span>
3. <span data-ttu-id="5b066-131">Povolte vrstvy SSL (Secure Sockets) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="5b066-131">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="5b066-132">Postupujte podle kroků uvedených v **povolit šifrování SSL pro projekt** část [Začínáme s webovými formuláři sérii](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span><span class="sxs-lookup"><span data-stu-id="5b066-132">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="5b066-133">V sadě Visual Studio, otevřete **Konzola správce balíčků** (**nástroje**  - &gt; **Správce balíčků NuGet**  - &gt; **Konzola správce balíčků**) a zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="5b066-133">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a><span data-ttu-id="5b066-134">Instalace služby SMS a dvoufaktorového ověřování</span><span class="sxs-lookup"><span data-stu-id="5b066-134">Setup SMS and Two-Factor Authentication</span></span>

<span data-ttu-id="5b066-135">Tento kurz používá Twilio, ale můžete použít jakýkoli poskytovatel serveru SMS.</span><span class="sxs-lookup"><span data-stu-id="5b066-135">This tutorial uses Twilio, but you can use any SMS provider.</span></span>

1. <span data-ttu-id="5b066-136">Vytvoření [Twilio](https://www.twilio.com/try-twilio) účtu.</span><span class="sxs-lookup"><span data-stu-id="5b066-136">Create a [Twilio](https://www.twilio.com/try-twilio) account.</span></span>
2. <span data-ttu-id="5b066-137">Z **řídicí panel** kartu svého účtu Twilio, kopie **SID účtu** a **ověřovací Token.**</span><span class="sxs-lookup"><span data-stu-id="5b066-137">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth Token.**</span></span> <span data-ttu-id="5b066-138">Přidáte je do své aplikace později.</span><span class="sxs-lookup"><span data-stu-id="5b066-138">You will add them to your app later.</span></span>
3. <span data-ttu-id="5b066-139">Z **čísla** kartu, zkopírujte váš Twilio **telefonní číslo** také.</span><span class="sxs-lookup"><span data-stu-id="5b066-139">From the **Numbers** tab, copy your Twilio **phone number** as well.</span></span>
4. <span data-ttu-id="5b066-140">Ujistěte se, Twilio **SID účtu**, **ověřovací Token** a **telefonní číslo** k dispozici pro aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5b066-140">Make the Twilio **Account SID**, **Auth Token** and **phone number** available to the app.</span></span> <span data-ttu-id="5b066-141">Pro zjednodušení budete ukládat tyto hodnoty *web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="5b066-141">To keep things simple you will store these values in the *web.config* file.</span></span> <span data-ttu-id="5b066-142">Při nasazování do Azure můžete ukládat bezpečně v hodnot **appSettings** karta Konfigurace části na webové stránce. Navíc když přidáte telefonní číslo, používejte pouze čísla.</span><span class="sxs-lookup"><span data-stu-id="5b066-142">When you deploy to Azure, you can store the values securely in the **appSettings** section on the web site configure tab. Also, when adding the phone number, only use numbers.</span></span>   
   <span data-ttu-id="5b066-143">Všimněte si, že můžete také přidat přihlašovací údaje služby SendGrid.</span><span class="sxs-lookup"><span data-stu-id="5b066-143">Notice that you can also add SendGrid credentials.</span></span> <span data-ttu-id="5b066-144">SendGrid je služba e-mailové oznámení.</span><span class="sxs-lookup"><span data-stu-id="5b066-144">SendGrid is an email notification service.</span></span> <span data-ttu-id="5b066-145">Podrobnosti o tom, jak povolit SendGrid, naleznete v části "Hook nahoru SendGrid" kurzu s názvem [vytvořit zabezpečené webové formuláře aplikace v ASP.NET s registrací uživatele, e-mailové potvrzení a resetováním hesla.](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)</span><span class="sxs-lookup"><span data-stu-id="5b066-145">For details about how to enable SendGrid, see the 'Hook Up SendGrid' section of the tutorial titled [Create a Secure ASP.NET Web Forms App with user registration, email confirmation and password reset.](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)</span></span>

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > <span data-ttu-id="5b066-146">Zabezpečení – nikdy ukládání citlivých dat ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="5b066-146">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="5b066-147">V tomto příkladu účtu a přihlašovací údaje jsou uloženy v **appSettings** část *Web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="5b066-147">In this example, the account and credentials are stored in the **appSettings** section of the *Web.config* file.</span></span> <span data-ttu-id="5b066-148">V Azure, můžete bezpečně uložit tyto hodnoty na **[konfigurovat](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** karta na portálu Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5b066-148">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="5b066-149">Související informace naleznete v tématu Rick Anderson s názvem [osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span><span class="sxs-lookup"><span data-stu-id="5b066-149">For related information, see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
5. <span data-ttu-id="5b066-150">Konfigurace `SmsService` třídy v *aplikace\_Start\IdentityConfig.cs* změně žlutě zvýrazněné v souboru tak, že následující:</span><span class="sxs-lookup"><span data-stu-id="5b066-150">Configure the `SmsService` class in the *App\_Start\IdentityConfig.cs* file by making the following changes highlighted in yellow:</span></span> 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. <span data-ttu-id="5b066-151">Přidejte následující `using` příkazy na začátek *IdentityConfig.cs* souboru:</span><span class="sxs-lookup"><span data-stu-id="5b066-151">Add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. <span data-ttu-id="5b066-152">Aktualizace *Account/Manage.aspx* souboru odebráním zvýrazněné žlutou barvou řádky:</span><span class="sxs-lookup"><span data-stu-id="5b066-152">Update the *Account/Manage.aspx* file by removing the lines highlighted in yellow:</span></span>  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. <span data-ttu-id="5b066-153">V `Page_Load` obslužná rutina *Manage.aspx.cs* použití modelu code-behind, Odkomentujte řádek kódu zvýrazněn žlutou barvou, tak že se objeví jako následující:</span><span class="sxs-lookup"><span data-stu-id="5b066-153">In the `Page_Load` handler of the *Manage.aspx.cs* code-behind, uncomment the line of code highlighted in yellow so that it appears as follows:</span></span> 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. <span data-ttu-id="5b066-154">V codebehind z *účet*/*TwoFactorAuthenticationSignIn.aspx.cs*, aktualizujte `Page_Load` obslužná rutina přidáním následujícího kódu zvýrazněné žlutou barvou:</span><span class="sxs-lookup"><span data-stu-id="5b066-154">In the codebehind of *Account*/*TwoFactorAuthenticationSignIn.aspx.cs*, update the `Page_Load` handler by adding the following code highlighted in yellow:</span></span> 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   <span data-ttu-id="5b066-155">Tím, že ve výše uvedeném kódu změňte, nebude "Zprostředkovatele" DropDownList obsahující možnosti ověřování nastavena na první hodnota.</span><span class="sxs-lookup"><span data-stu-id="5b066-155">By making the above code change, the "Providers" DropDownList containing the authentication options will not be reset to the first value.</span></span> <span data-ttu-id="5b066-156">To vám umožní uživateli vybrat úspěšně všechny možnosti pro použití při ověřování, nikoli jen na prvním.</span><span class="sxs-lookup"><span data-stu-id="5b066-156">This will allow the user to successfully select all options to use when authenticating, not just the first.</span></span>
10. <span data-ttu-id="5b066-157">V **Průzkumníka řešení**, klikněte pravým tlačítkem na *Default.aspx* a vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="5b066-157">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
11. <span data-ttu-id="5b066-158">Při testování vaší aplikace, nejprve vytvořte aplikaci (**Ctrl**+**Shift**+**B**) a pak spusťte aplikaci (**F5**) a Vyberte buď **zaregistrovat** a vytvořte nový uživatelský účet nebo vyberte **přihlášení** Pokud uživatelský účet už je zaregistrovaný.</span><span class="sxs-lookup"><span data-stu-id="5b066-158">By testing your app, first build the app (**Ctrl**+**Shift**+**B**) and then run the app (**F5**) and either select **Register** to create a new user account or select **Log in** if the user account has already been registered.</span></span>
12. <span data-ttu-id="5b066-159">Jakmile (jako uživatel) se přihlásíte, klikněte na uživatelské ID (e-mailovou adresu) v navigačním panelu se zobrazí **spravovat účet** stránky (Manage.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b066-159">Once you (as the user) have logged in, click on the User ID (email address) in the navigation bar to display the **Manage Account** page (Manage.aspx).</span></span>  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. <span data-ttu-id="5b066-160">Klikněte na tlačítko **přidat** vedle **telefonní číslo** na **spravovat účet** stránky.</span><span class="sxs-lookup"><span data-stu-id="5b066-160">Click **Add** next to **Phone Number** on the **Manage Account** page.</span></span>  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. <span data-ttu-id="5b066-161">Přidat telefonní číslo, kde (jako uživatel) chcete přijímat zprávy SMS (text zprávy) a klikněte na tlačítko **odeslat** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5b066-161">Add the phone number where you (as the user) would like to receive SMS messages (text messages) and click the **Submit** button.</span></span>   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    <span data-ttu-id="5b066-162">V tomto okamžiku bude aplikace používat přihlašovací údaje z *Web.config* kontaktovat Twilio.</span><span class="sxs-lookup"><span data-stu-id="5b066-162">At this point, the app will use the credentials from the *Web.config* to contact Twilio.</span></span> <span data-ttu-id="5b066-163">Zpráva SMS (textová zpráva) se odešlou do telefonu přiřazeném k uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="5b066-163">A SMS message (text message) will be sent to the phone associated with the user account.</span></span> <span data-ttu-id="5b066-164">Můžete ověřit, že Twilio zpráva byla odeslána tím, že zobrazíte řídicí panel Twilio.</span><span class="sxs-lookup"><span data-stu-id="5b066-164">You can verify that the Twilio message was sent by viewing the Twilio dashboard.</span></span>
15. <span data-ttu-id="5b066-165">Během několika sekund telefonu přiřazeném k uživatelský účet získá textovou zprávu obsahující ověřovací kód.</span><span class="sxs-lookup"><span data-stu-id="5b066-165">In a few seconds, the phone associated with the user account will get a text message containing the verification code.</span></span> <span data-ttu-id="5b066-166">Zadejte ověřovací kód a stiskněte klávesu **odeslat**.</span><span class="sxs-lookup"><span data-stu-id="5b066-166">Enter the verification code and press **Submit**.</span></span>  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a><span data-ttu-id="5b066-167">Povolení dvoufaktorového ověřování pro registrovaný uživatel</span><span class="sxs-lookup"><span data-stu-id="5b066-167">Enable Two-Factor Authentication for a Registered User</span></span>

<span data-ttu-id="5b066-168">V tomto okamžiku jste povolili dvoufaktorového ověřování pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5b066-168">At this point, you have enabled two-factor authentication for your app.</span></span> <span data-ttu-id="5b066-169">Uživatel chce použít dvojúrovňové ověřování mohou jednoduše změnit jejich nastavení pomocí uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="5b066-169">For a user to use two-factor authentication, they can simply change their settings using the UI.</span></span> 

1. <span data-ttu-id="5b066-170">Jako uživatel aplikace můžete povolit dvoufaktorové ověřování pro konkrétní účet kliknutím na ID uživatele (e-mailový alias) v navigačním panelu se zobrazí **spravovat účet** stránky. Potom klikněte na **povolit** odkaz pro povolení dvoufaktorového ověřování pro účet.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="5b066-170">As a user of your app you can enable two-factor authentication for your specific account by clicking on the user ID (email alias) in the navigation bar to display the **Manage Account** page.Then, click on the **Enable** link to enable two-factor authentication for the account.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)</span></span>
2. <span data-ttu-id="5b066-171">Odhlásit a znovu přihlásit.</span><span class="sxs-lookup"><span data-stu-id="5b066-171">Log off, then log back in.</span></span> <span data-ttu-id="5b066-172">Pokud jste povolili e-mailu, můžete vybrat, SMS nebo e-mailu pro dvoufaktorové ověřování.</span><span class="sxs-lookup"><span data-stu-id="5b066-172">If you've enabled email, you can select either SMS or email for two-factor authentication.</span></span> <span data-ttu-id="5b066-173">Pokud jste ještě nepovolili e-mailu, najdete v kurzu s názvem [vytvořit zabezpečené webové formuláře aplikace v ASP.NET s registrací uživatele, e-mailové potvrzení a resetování hesla](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5b066-173">If you haven't enabled email, see the tutorial titled [Create a Secure ASP.NET Web Forms App with User Registration, Email Confirmation and Password Reset](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)</span></span>
3. <span data-ttu-id="5b066-174">Zobrazí se stránka dvojúrovňové ověřování, ve kterém můžete zadat kód (z SMS nebo e-mailu).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="5b066-174">The Two-Factor Authentication page is displayed where you can enter the code (from SMS or email).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)</span></span>  
 <span data-ttu-id="5b066-175">Kliknutím na **chcete Zapamatovat tento prohlížeč** zaškrtávacího políčka můžete před nutností přihlášení při používání prohlížeče a zařízení, kde zaškrtnuté políčko pomocí dvojúrovňového ověřování vyloučit.</span><span class="sxs-lookup"><span data-stu-id="5b066-175">Clicking on the **Remember this browser** check box will exempt you from needing to use two-factor authentication to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="5b066-176">Za předpokladu, uživateli se zlými úmysly nemůže získat přístup k zařízení, povolení dvoufaktorového ověřování a kliknete na **chcete Zapamatovat tento prohlížeč** vám poskytne pohodlný přístup heslo jeden krok, při zachování strong dvoufaktorové ověřování ochrana pro veškerý přístup z jiných důvěryhodných zařízení.</span><span class="sxs-lookup"><span data-stu-id="5b066-176">As long as malicious users can't gain access to your device, enabling two-factor authentication and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong two-factor authentication protection for all access from non-trusted devices.</span></span> <span data-ttu-id="5b066-177">Můžete to provést na libovolném privátní zařízení, kterou používáte pravidelně.</span><span class="sxs-lookup"><span data-stu-id="5b066-177">You can do this on any private device you regularly use.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="5b066-178">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="5b066-178">Additional Resources</span></span>

- [<span data-ttu-id="5b066-179">Dvoufaktorové ověřování pomocí SMS a e-mailu s ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5b066-179">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [<span data-ttu-id="5b066-180">Odkazy na ASP.NET Identity doporučené zdroje informací</span><span class="sxs-lookup"><span data-stu-id="5b066-180">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="5b066-181">Nasaďte aplikaci zabezpečení rozhraní ASP.NET Web Forms s nástroji Membership, OAuth a SQL Database na web Azure</span><span class="sxs-lookup"><span data-stu-id="5b066-181">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Website</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="5b066-182">Série kurzů webových formulářů ASP.NET – přidání poskytovatele OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="5b066-182">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="5b066-183">Technologie ASP.NET webové formuláře sérii - povolit šifrování SSL pro projekt</span><span class="sxs-lookup"><span data-stu-id="5b066-183">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [<span data-ttu-id="5b066-184">Potvrzení účtu a obnovení hesla s ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5b066-184">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="5b066-185">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="5b066-185">Creating the app in Facebook and connecting the app to the project</span></span>](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)