---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Jednotné přihlašování (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 1ca93cce22487295a24aae95437b3e69dfc5b504
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457138"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="e1d6b-104">Jednotné přihlašování (vytváření skutečných cloudových aplikací s Azure)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="e1d6b-105">[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="e1d6b-106">[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="e1d6b-107">**Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="e1d6b-108">Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="e1d6b-109">Informace o elektronické příručce najdete v [první kapitole](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="e1d6b-110">Při vývoji cloudové aplikace je potřeba vzít v úvahu mnoho problémů se zabezpečením, ale pro tuto řadu se zaměříme jenom na jedno: jednotné přihlašování.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="e1d6b-111">Lidé se často dotazují: "Já jsem sestavovat aplikace pro zaměstnance mojí společnosti; Jak můžu hostovat tyto aplikace v cloudu a pořád jim povolit, aby používali stejný model zabezpečení, který mají zaměstnanci vědět a používají v místním prostředí, když běží aplikace, které jsou hostované v bráně firewall? "</span><span class="sxs-lookup"><span data-stu-id="e1d6b-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="e1d6b-112">Jedním z způsobů, jak tento scénář povolit, se říká Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e1d6b-113">Azure AD umožňuje zpřístupnit podnikovým podnikovým aplikacím přístup přes Internet a umožňuje zpřístupnit tyto aplikace i obchodním partnerům.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="e1d6b-114">Seznámení s Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d6b-114">Introduction to Azure AD</span></span>

<span data-ttu-id="e1d6b-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) poskytuje [službu Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) v cloudu.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="e1d6b-116">Mezi klíčové funkce patří následující:</span><span class="sxs-lookup"><span data-stu-id="e1d6b-116">Key features include the following:</span></span>

- <span data-ttu-id="e1d6b-117">Integruje se s místní službou Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="e1d6b-118">Umožňuje jednotné přihlašování s vašimi aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="e1d6b-119">Podporuje otevřené standardy, jako je [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-dokrmený](http://en.wikipedia.org/wiki/WS-Federation)a [OAuth 2,0](http://oauth.net/2/).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="e1d6b-120">Podporuje REST API podnikového [grafu](https://msdn.microsoft.com/library/hh974476.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="e1d6b-121">Předpokládejme, že máte místní prostředí Windows serveru Active Directory, které se používá k tomu, aby se zaměstnanci mohli přihlašovat k intranetovým aplikacím:</span><span class="sxs-lookup"><span data-stu-id="e1d6b-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="e1d6b-122">To, co Azure AD umožňuje, je vytvořit adresář v cloudu.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="e1d6b-123">Je to bezplatná funkce a snadno se nastavuje.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="e1d6b-124">Může být zcela nezávislá na vaší místní službě Active Directory. můžete do něj umístit libovolného někoho a ověřit je v internetových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Microsoft Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="e1d6b-126">Nebo ho můžete integrovat s místní službou AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-126">Or you can integrate it with your on-premises AD.</span></span>

![Integrace AD a WAAD](single-sign-on/_static/image3.png)

<span data-ttu-id="e1d6b-128">Všichni zaměstnanci, kteří se můžou místně ověřovat v místním prostředí, se teď můžou ověřit přes Internet – bez nutnosti otevírat bránu firewall nebo nasazovat nové servery v datovém centru.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="e1d6b-129">Můžete dál využívat všechny existující prostředí Active Directory, které znáte a dnes používáte, a poskytnout tak interním aplikacím možnost jednotného přihlašování.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="e1d6b-130">Jakmile provedete toto propojení mezi službami AD a Azure AD, můžete také povolit vašim webovým aplikacím a mobilním zařízením ověřování zaměstnanců v cloudu a povolit aplikace třetích stran, jako je například Office 365, SalesForce.com nebo Google, přijmout vaše přihlašovací údaje zaměstnanců.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="e1d6b-131">Pokud používáte Office 365, už jste si nastavili Azure AD, protože Office 365 používá k ověřování a autorizaci službu Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![aplikace třetích stran](single-sign-on/_static/image4.png)

<span data-ttu-id="e1d6b-133">Krásy tohoto přístupu je to, že kdykoli vaše organizace přidá nebo odstraní uživatele nebo když uživatel změní heslo, použijete stejný proces, který dnes využijete v místním prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="e1d6b-134">Všechny změny vaší místní služby Active Directory se automaticky rozšíří do cloudového prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="e1d6b-135">Pokud vaše společnost používá nebo přesouvá sadu Office 365, dobrá zpráva je, že budete mít službu Azure AD nastavenou automaticky, protože sada Office 365 pro ověřování používá službu Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="e1d6b-136">Takže můžete snadno použít ve svých aplikacích stejné ověřování, které používá sada Office 365.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="e1d6b-137">Nastavení tenanta Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1d6b-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="e1d6b-138">adresář služby Azure AD se nazývá [tenant](https://technet.microsoft.com/library/jj573650.aspx)Azure AD a nastavení tenanta je poměrně snadné.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="e1d6b-139">Ukážeme vám, jak se to provede v Azure Portál pro správu, aby bylo možné ilustrovat koncepty, ale samozřejmě jako jiné funkce portálu to můžete udělat také pomocí skriptu nebo rozhraní API pro správu.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="e1d6b-140">Na portálu pro správu klikněte na kartu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-140">In the management portal click the Active Directory tab.</span></span>

![WAAD na portálu](single-sign-on/_static/image5.png)

<span data-ttu-id="e1d6b-142">Pro svůj účet Azure máte automaticky jednoho tenanta Azure AD a můžete kliknout na tlačítko **Přidat** v dolní části stránky a vytvořit další adresáře.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="e1d6b-143">Můžete chtít jeden pro testovací prostředí a jeden pro produkční prostředí, například.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="e1d6b-144">Zamyslete se nad tím, co pojmenujte nový adresář.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="e1d6b-145">Pokud pro tento adresář použijete své jméno a potom pro jednoho z nich použijete své jméno, může to být matoucí.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![Přidat adresář](single-sign-on/_static/image6.png)

<span data-ttu-id="e1d6b-147">Portál má úplnou podporu pro vytváření, odstraňování a správu uživatelů v rámci tohoto prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="e1d6b-148">Pokud například chcete přidat uživatele, přejděte na kartu **Uživatelé** a klikněte na tlačítko **Přidat uživatele** .</span><span class="sxs-lookup"><span data-stu-id="e1d6b-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![Tlačítko Přidat uživatele](single-sign-on/_static/image7.png)

![Přidat uživatelský dialog](single-sign-on/_static/image8.png)

<span data-ttu-id="e1d6b-151">Můžete vytvořit nového uživatele, který existuje pouze v tomto adresáři, nebo můžete zaregistrovat účet Microsoft jako uživatele v tomto adresáři nebo zaregistrovat nebo uživatele z jiného adresáře služby Azure AD jako uživatel v tomto adresáři.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="e1d6b-152">(Ve skutečném adresáři by se ContosoTest.onmicrosoft.com výchozí doména.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="e1d6b-153">Můžete také použít doménu podle vlastního výběru, například contoso.com.)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![Uživatelské typy](single-sign-on/_static/image9.png)

![Přidat uživatelský dialog](single-sign-on/_static/image10.png)

<span data-ttu-id="e1d6b-156">Uživatele můžete přiřadit k roli.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-156">You can assign the user to a role.</span></span>

![Profil uživatele](single-sign-on/_static/image11.png)

<span data-ttu-id="e1d6b-158">A účet se vytvoří s dočasným heslem.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-158">And the account is created with a temporary password.</span></span>

![Dočasné heslo](single-sign-on/_static/image12.png)

<span data-ttu-id="e1d6b-160">Uživatelé, které vytváříte tímto způsobem, se můžou ke svým webovým aplikacím přihlašovat hned pomocí tohoto adresáře cloudu.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="e1d6b-161">To je skvělé pro podnikové jednotné přihlašování, ale je to karta **integrace adresáře** :</span><span class="sxs-lookup"><span data-stu-id="e1d6b-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![Karta integrace adresáře](single-sign-on/_static/image13.png)

<span data-ttu-id="e1d6b-163">Pokud povolíte integraci adresáře a [stáhnete nástroj](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), můžete tento cloudový adresář synchronizovat se stávající místní službou Active Directory, kterou už ve vaší organizaci používáte.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="e1d6b-164">Pak se v tomto cloudovém adresáři zobrazí všichni uživatelé, kteří jsou v adresáři.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="e1d6b-165">Vaše cloudové aplikace teď můžou ověřit všechny vaše zaměstnance pomocí svých stávajících přihlašovacích údajů služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="e1d6b-166">A všechno je zdarma – jak synchronizační nástroj, tak i služba Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="e1d6b-167">Tento nástroj je průvodcem, který se snadno používá, jak můžete vidět z těchto snímků obrazovky.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="e1d6b-168">Tyto pokyny nejsou kompletní, jenom příklad, který vám ukáže základní proces.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="e1d6b-169">Podrobnější informace o tom, jak to udělat, najdete v odkazech v části [Resources (prostředky](#resources) ) na konci kapitoly.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image14.png)

<span data-ttu-id="e1d6b-171">Klikněte na **Další**a potom zadejte přihlašovací údaje Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image15.png)

<span data-ttu-id="e1d6b-173">Klikněte na **Další**a potom zadejte svoje místní přihlašovací údaje služby AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image16.png)

<span data-ttu-id="e1d6b-175">Klikněte na **Další**a pak určete, jestli chcete v cloudu ukládat hodnoty hash hesel služby AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image17.png)

<span data-ttu-id="e1d6b-177">Hodnota hash hesla, kterou můžete uložit v cloudu, je jednosměrná hodnota hash. Skutečná hesla se nikdy neukládají v Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="e1d6b-178">Pokud se rozhodnete ukládat hodnoty hash v cloudu, budete muset použít [Active Directory Federation Services (AD FS)](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="e1d6b-179">K dispozici jsou také [Další faktory, které byste měli vzít v úvahu při rozhodování, zda používat službu AD FS](https://technet.microsoft.com/library/jj573653.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="e1d6b-180">Možnost ADFS vyžaduje několik dalších kroků konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="e1d6b-181">Pokud se rozhodnete ukládat hodnoty hash do cloudu, jste hotovi a nástroj po kliknutí na **Další**spustí synchronizaci adresářů.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image18.png)

<span data-ttu-id="e1d6b-183">A za pár minut jste hotovi.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-183">And in a few minutes you're done.</span></span>

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image19.png)

<span data-ttu-id="e1d6b-185">Stačí ho spustit na jednom řadiči domény v organizaci ve Windows 2003 nebo novějším.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="e1d6b-186">A není nutné restartovat počítač.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-186">And no need to reboot.</span></span> <span data-ttu-id="e1d6b-187">Až to budete mít, všichni uživatelé budou v cloudu a můžete provádět jednotné přihlašování z libovolné webové nebo mobilní aplikace, pomocí SAML, OAuth nebo WS-dodávání.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="e1d6b-188">V některých případech se dozvíte, jak se to dělá, protože ho Microsoft používá pro vlastní citlivá firemní data?</span><span class="sxs-lookup"><span data-stu-id="e1d6b-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="e1d6b-189">A odpověď je Ano.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-189">And the answer is yes we do.</span></span> <span data-ttu-id="e1d6b-190">Například pokud přejdete na interní web Microsoft SharePointu na adrese [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), zobrazí se výzva k přihlášení.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Přihlášení k Office 365](single-sign-on/_static/image20.png)

<span data-ttu-id="e1d6b-192">Společnost Microsoft povolila službu AD FS, takže když zadáte ID Microsoftu, budete přesměrováni na přihlašovací stránku služby AD FS.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![Přihlášení k ADFS](single-sign-on/_static/image21.png)

<span data-ttu-id="e1d6b-194">A když zadáte přihlašovací údaje uložené v interním účtu Microsoft AD, budete mít přístup k této interní aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![Web služby SharePoint společnosti Microsoft](single-sign-on/_static/image22.png)

<span data-ttu-id="e1d6b-196">K dispozici je server pro přihlášení k reklamě, protože už jsme nastavili službu AD FS dřív, než se služba Azure AD stala dostupná, ale proces přihlášení projde adresářem služby Azure AD v cloudu.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="e1d6b-197">Naše důležité dokumenty, Správa zdrojového kódu, soubory pro správu výkonu, prodejní sestavy a další jsou v cloudu a používají toto přesné řešení k zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="e1d6b-198">Vytvoření aplikace ASP.NET, která používá Azure AD pro jednotné přihlašování</span><span class="sxs-lookup"><span data-stu-id="e1d6b-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="e1d6b-199">Visual Studio umožňuje opravdu snadno vytvořit aplikaci, která používá Azure AD pro jednotné přihlašování, jak vidíte z několika snímků obrazovky.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="e1d6b-200">Při vytváření nové aplikace ASP.NET, MVC nebo webových formulářů, je výchozí metoda ověřování ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="e1d6b-201">Pokud ho chcete změnit na Azure AD, klikněte na tlačítko **změnit ověřování** .</span><span class="sxs-lookup"><span data-stu-id="e1d6b-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![Změnit ověřování](single-sign-on/_static/image23.png)

<span data-ttu-id="e1d6b-203">Vyberte účty organizace, zadejte název domény a pak vyberte jednotné přihlašování.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![Dialogové okno Konfigurace ověřování](single-sign-on/_static/image24.png)

<span data-ttu-id="e1d6b-205">Můžete taky udělit oprávnění ke čtení nebo čtení a zápisu pro data adresáře aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="e1d6b-206">Pokud to uděláte, může k vyhledání telefonního čísla uživatele použít [REST API Azure Graph](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) , zjistit, jestli jsou v kanceláři, kdy se naposledy přihlásili atd.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="e1d6b-207">To je všechno, co musíte udělat – Visual Studio si vyžádá pověření pro správce vašeho tenanta Azure AD a potom nakonfiguruje projekt i tenanta Azure AD pro novou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="e1d6b-208">Při spuštění projektu se zobrazí přihlašovací stránka a můžete se přihlásit pomocí přihlašovacích údajů uživatele v adresáři služby Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![Přihlášení k účtu org](single-sign-on/_static/image25.png)

![Přihlášen](single-sign-on/_static/image26.png)

<span data-ttu-id="e1d6b-211">Když nasadíte aplikaci do Azure, stačí, když zaškrtnete políčko **Povolit ověřování organizace** , a jakmile se Visual Studio bude starat o veškerou konfiguraci za vás.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![Publikování webu](single-sign-on/_static/image27.png)

<span data-ttu-id="e1d6b-213">Tyto snímky obrazovky pocházejí z kompletního podrobného kurzu, který ukazuje, jak vytvořit aplikaci, která používá ověřování Azure AD: [vývoj aplikací ASP.NET pomocí Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="e1d6b-214">Souhrn</span><span class="sxs-lookup"><span data-stu-id="e1d6b-214">Summary</span></span>

<span data-ttu-id="e1d6b-215">V této kapitole jste viděli, že Azure Active Directory, Visual Studio a ASP.NET usnadňují nastavení jednotného přihlašování v internetových aplikacích pro uživatele vaší organizace.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="e1d6b-216">Uživatelé se můžou k internetovým aplikacím přihlašovat pomocí stejných přihlašovacích údajů, které používají k přihlášení pomocí služby Active Directory ve vaší interní síti.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="e1d6b-217">[Další kapitola](data-storage-options.md) si vyhledá možnosti úložiště dat dostupné pro cloudovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="e1d6b-218">Prostředky</span><span class="sxs-lookup"><span data-stu-id="e1d6b-218">Resources</span></span>

<span data-ttu-id="e1d6b-219">Další informace naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="e1d6b-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="e1d6b-220">[Azure Active Directory dokumentaci](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="e1d6b-221">Stránka portálu pro dokumentaci k Azure AD na webu windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="e1d6b-222">Podrobné kurzy najdete v části **vývoj** .</span><span class="sxs-lookup"><span data-stu-id="e1d6b-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="e1d6b-223">[Multi-Factor Authentication Azure](https://docs.microsoft.com/azure/multi-factor-authentication/).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="e1d6b-224">Stránka portálu pro dokumentaci k Multi-Factor Authentication v Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="e1d6b-225">[Možnosti ověřování účtu organizace](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="e1d6b-226">Vysvětlení možností ověřování Azure AD v dialogovém okně Visual Studio 2013 nový projekt.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="e1d6b-227">[Vzory a postupy Microsoft – model federované identity](https://msdn.microsoft.com/library/dn589790.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="e1d6b-228">[Postupy: Nainstalujte nástroj Azure Active Directory Sync](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="e1d6b-229">[Mapa obsahu Active Directory Federation Services (AD FS) 2,0](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="e1d6b-230">Odkazy na dokumentaci ke službě ADFS 2,0.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="e1d6b-231">[Ověřování na základě rolí a ACL v aplikaci Windows Azure AD](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="e1d6b-232">Ukázková aplikace</span><span class="sxs-lookup"><span data-stu-id="e1d6b-232">Sample application.</span></span>
- <span data-ttu-id="e1d6b-233">[Azure Active Directory Graph API Blog](https://blogs.msdn.com/b/aadgraphteam/).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="e1d6b-234">[Access Control v integraci BYOD a adresáře v hybridní infrastruktuře identit](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span><span class="sxs-lookup"><span data-stu-id="e1d6b-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="e1d6b-235">Video o relaci Tech Ed 2014 od Gayana Bagdasaryan.</span><span class="sxs-lookup"><span data-stu-id="e1d6b-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e1d6b-236">[Předchozí](web-development-best-practices.md)
> [Další](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="e1d6b-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
