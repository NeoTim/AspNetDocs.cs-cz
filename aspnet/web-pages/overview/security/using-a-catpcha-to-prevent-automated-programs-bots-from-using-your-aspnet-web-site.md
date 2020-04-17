---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Použití CAPTCHA, aby se zabránilo Roboty z používání vašeho ASP.NET Web Břitva) stránek | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento článek vysvětluje, jak používat ReCaptcha (bezpečnostní opatření), aby se zabránilo automatizované programy (roboty) z provádění úkolů v ASP.NET webových stránek (Břitva) jsme ...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543753"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="33efc-103">Použití CAPTCHA, aby se zabránilo Roboty z používání vašeho ASP.NET Web Břitva) stránek</span><span class="sxs-lookup"><span data-stu-id="33efc-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="33efc-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="33efc-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="33efc-105">Tento článek vysvětluje, jak pomocí recaptcha (bezpečnostní opatření) zabránit automatizovaným programům (robotům) v provádění úloh na webu ASP.NET webových stránek (Razor).</span><span class="sxs-lookup"><span data-stu-id="33efc-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="33efc-106">**Naučíte se:**</span><span class="sxs-lookup"><span data-stu-id="33efc-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="33efc-107">Jak přidat test CAPTCHA na vaše stránky.</span><span class="sxs-lookup"><span data-stu-id="33efc-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="33efc-108">Jedná se o ASP.NET funkce uvedené v článku:</span><span class="sxs-lookup"><span data-stu-id="33efc-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="33efc-109">Pomocník. `ReCaptcha`</span><span class="sxs-lookup"><span data-stu-id="33efc-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="33efc-110">Informace v tomto článku platí pro ASP.NET webových stránek 1.0 a webových stránek 2.</span><span class="sxs-lookup"><span data-stu-id="33efc-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="33efc-111">O captchas</span><span class="sxs-lookup"><span data-stu-id="33efc-111">About CAPTCHAs</span></span>

<span data-ttu-id="33efc-112">Kdykoli vynecháte lidi zaregistrovat na vašem webu, nebo dokonce jen zadat jméno a URL (jako pro blog komentář), můžete získat záplavu falešných jmen.</span><span class="sxs-lookup"><span data-stu-id="33efc-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="33efc-113">Ty jsou často ponechány automatizovanými programy (roboty), které se pokoušejí nechat adresy URL na všech webových stránkách, které mohou najít.</span><span class="sxs-lookup"><span data-stu-id="33efc-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="33efc-114">(Běžnou motivací je zveřejňovat adresy URL produktů na prodej.)</span><span class="sxs-lookup"><span data-stu-id="33efc-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="33efc-115">Můžete pomoci zajistit, že uživatel je skutečná osoba a není počítačový program pomocí *CAPTCHA* k ověření uživatelů při registraci nebo jinak zadat jejich jméno a web.</span><span class="sxs-lookup"><span data-stu-id="33efc-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="33efc-116">CAPTCHA je zkratka pro zcela automatizovaný veřejný Turingův test, který říká počítačům a lidem.</span><span class="sxs-lookup"><span data-stu-id="33efc-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="33efc-117">CAPTCHA je *test výzvy a odezvy,* ve kterém je uživatel požádán, aby udělal něco, co je pro člověka snadné, ale pro automatizovaný program je těžké.</span><span class="sxs-lookup"><span data-stu-id="33efc-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="33efc-118">Nejběžnějšítyp CAPTCHA je ten, kde vidíte některé zkreslené písmena a jsou vyzváni k jejich zadání.</span><span class="sxs-lookup"><span data-stu-id="33efc-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="33efc-119">(Zkreslení má ztížit botům rozluštit písmena.)</span><span class="sxs-lookup"><span data-stu-id="33efc-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="33efc-120">Přidání testu ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="33efc-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="33efc-121">V ASP.NET stránek můžete `ReCaptcha` pomocí pomocné položky vykreslit test CAPTCHA, který[http://recaptcha.net](http://recaptcha.net)je založen na službě ReCaptcha ( ).</span><span class="sxs-lookup"><span data-stu-id="33efc-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="33efc-122">Pomocník `ReCaptcha` zobrazí obrázek dvou zkreslených slov, které musí uživatelé zadat správně před ověřením stránky.</span><span class="sxs-lookup"><span data-stu-id="33efc-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="33efc-123">Odpověď uživatele je ověřena službou ReCaptcha.Net.</span><span class="sxs-lookup"><span data-stu-id="33efc-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="33efc-124">Zaregistrujte své webové[http://recaptcha.net](http://recaptcha.net)stránky na ReCaptcha.Net ( ).</span><span class="sxs-lookup"><span data-stu-id="33efc-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="33efc-125">Po dokončení registrace získáte veřejný a soukromý klíč.</span><span class="sxs-lookup"><span data-stu-id="33efc-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="33efc-126">Pokud jste tak ještě neučinili , přidejte na web knihovnu ASP.NET webových [pomocníků,](https://go.microsoft.com/fwlink/?LinkId=252372)jak je popsáno v části Instalace pomocníků na webu ASP.NET , pokud jste tak již neučinili.</span><span class="sxs-lookup"><span data-stu-id="33efc-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="33efc-127">Pokud ještě nemáte soubor \* \_AppStart.cshtml,\* vytvořte v kořenové složce webu soubor s názvem \* \_AppStart.cshtml\*.</span><span class="sxs-lookup"><span data-stu-id="33efc-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="33efc-128">Do souboru `Recaptcha` \* \_AppStart.cshtml\* přidejte následující nastavení pomocníka:</span><span class="sxs-lookup"><span data-stu-id="33efc-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="33efc-129">Nastavte `PublicKey` vlastnosti a `PrivateKey` pomocí vlastních veřejných a soukromých klíčů.</span><span class="sxs-lookup"><span data-stu-id="33efc-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="33efc-130">Uložte soubor \* \_AppStart.cshtml\* a zavřete jej.</span><span class="sxs-lookup"><span data-stu-id="33efc-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="33efc-131">V kořenové složce webu vytvořte novou stránku s názvem *Recaptcha.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="33efc-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="33efc-132">Nahraďte existující obsah následujícím:</span><span class="sxs-lookup"><span data-stu-id="33efc-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="33efc-133">Spusťte stránku *Recaptcha.cshtml* v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="33efc-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="33efc-134">Pokud `PrivateKey` je hodnota platná, stránka zobrazí ovládací prvek ReCaptcha a tlačítko.</span><span class="sxs-lookup"><span data-stu-id="33efc-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="33efc-135">Pokud jste nenastavili klíče globálně v \* \_AppStart.html\*, stránka by se zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="33efc-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="33efc-136">Zadejte slova pro test.</span><span class="sxs-lookup"><span data-stu-id="33efc-136">Enter the words for the test.</span></span> <span data-ttu-id="33efc-137">Pokud projdete testrecaptcha, zobrazí se zpráva v tomto smyslu.</span><span class="sxs-lookup"><span data-stu-id="33efc-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="33efc-138">V opačném případě se zobrazí chybová zpráva a ovládací prvek ReCaptcha se znovu zobrazí.</span><span class="sxs-lookup"><span data-stu-id="33efc-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="33efc-139">Pokud je počítač v doméně, která používá proxy `defaultproxy` server, bude pravděpodobně nutné nakonfigurovat prvek souboru *Web.config.*</span><span class="sxs-lookup"><span data-stu-id="33efc-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="33efc-140">Následující příklad ukazuje soubor *Web.config* s `defaultproxy` prvkem nakonfigurovaným tak, aby služba ReCaptcha fungovala.</span><span class="sxs-lookup"><span data-stu-id="33efc-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="33efc-141">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="33efc-141">Additional Resources</span></span>

- [<span data-ttu-id="33efc-142">Přizpůsobení chování na celém webu pro ASP.NET weby webových stránek</span><span class="sxs-lookup"><span data-stu-id="33efc-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="33efc-143">Web ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="33efc-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
