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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Vytvoření aplikace ASP.NET MVC 5 s přihlášením přes Facebook, Twitter, LinkedIn a Google OAuth2 (C#)

podle [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se můžete naučit vytvořit ASP.NET webové aplikace MVC 5, která uživatelům umožňuje přihlásit se pomocí [aplikace OAuth 2.0](http://oauth.net/2/) pomocí přihlašovacích údajů od externího poskytovatele ověřování, jako je Facebook, Twitter, LinkedIn, Microsoft nebo Google. Pro jednoduchost se tento kurz zaměřuje na práci s pověřeními od Facebooku a Googlu.
> 
> Povolení těchto pověření na webových stránkách poskytuje významnou výhodu, protože miliony uživatelů již mají účty u těchto externích poskytovatelů. Tito uživatelé mohou být více nakloněni k registraci na vašem webu, pokud nebudou muset vytvářet a pamatovat si novou sadu pověření.
> 
> Viz také [ASP.NET aplikaci MVC 5 s SMS a e-mailem Dvoufaktorové ověřování](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> Kurz také ukazuje, jak přidat data profilu pro uživatele a jak používat rozhraní API členství k přidání rolí. Tento výukový program byl napsán [Rick Anderson](https://blogs.msdn.com/rickAndy) [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Prosím, následujte mě na Twitteru: ).

<a id="start"></a>
## <a name="getting-started"></a>začínáme

Začněte instalací a spuštěním [sady Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte visual studio [2013 aktualizace 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší. O pomoc s Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, a další, viz tento [ukázkový projekt](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Chcete-li používat Google OAuth 2 a ladit místně bez upozornění SSL, je nutné nainstalovat aktualizaci Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.

Na **úvodní** stránce klikněte na **Nový projekt,** nebo můžete použít nabídku a vybrat **Soubor**a potom **nový projekt**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Klepněte na **tlačítko Nový projekt**, potom vyberte možnost Visual **C#** vlevo, potom na **Web** a pak vyberte **ASP.NET webovou aplikaci**. Pojmenujte projekt "MvcAuth" a klepněte na tlačítko **OK**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

V dialogovém **okně Nový ASP.NET projektu** klepněte na tlačítko **MVC**. Pokud ověřování není **individuální uživatelské účty**, klepněte na tlačítko Změnit **ověřování** a vyberte jednotlivé **uživatelské účty**. Kontrolou **Hostitele v cloudu**bude velmi snadné hostovat v Azure.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Pokud jste **v cloudu**vybrali možnost Host , vyplňte dialogové okno konfigurace.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Použití NuGet k aktualizaci na nejnovější middleware OWIN

Pomocí správce balíčků NuGet aktualizujte [middleware OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md). V levé nabídce vyberte **Aktualizace.** Můžete kliknout na tlačítko **Aktualizovat vše** nebo můžete vyhledávat pouze balíčky OWIN (zobrazeno na následujícím obrázku):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

Na obrázku níže jsou zobrazeny pouze balíčky OWIN:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

Z konzoly Správce balíčků (PMC) `Update-Package` můžete zadat příkaz, který aktualizuje všechny balíčky.

Stisknutím **kláves F5** nebo **Ctrl+F5** aplikaci spusťte. Na obrázku níže je číslo portu 1234. Při spuštění aplikace se zobrazí jiné číslo portu.

V závislosti na velikosti okna prohlížeče může být nutné kliknout na ikonu **navigace,** aby se zobce, informace **o** **tom, kontakt**, **registrace** a **přihlášení.**

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Nastavení ssl v projektu

Chcete-li se připojit k poskytovatelům ověřování, jako je Google a Facebook, budete muset nastavit službu IIS-Express, aby používala protokol SSL. Je důležité, aby i po přihlášení používat SSL a neklesnout zpět na HTTP, vaše přihlašovací cookie je stejně tajné jako vaše uživatelské jméno a heslo, a bez použití SSL posíláte jej v prostém textu přes drát. Kromě toho jste již udělali čas na provedení handshake a zabezpečení kanálu (což je převážná část toho, co dělá HTTPS pomalejší než HTTP) před spuštěním kanálu MVC, takže přesměrování zpět na HTTP po přihlášení nebude provádět aktuální požadavek nebo budoucí požadavky mnohem rychleji.

1. V **Průzkumníku řešení**klepněte na projekt **MvcAuth.**
2. Chcete-li zobrazit vlastnosti projektu, stiskněte klávesu F4. Případně můžete v nabídce **Zobrazit** vybrat **možnost Vlastnosti okna**.
3. Změnit **ssl povoleno** na hodnotu True.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Zkopírujte adresu URL SSL `https://localhost:44300/` (která bude, pokud jste nevytvořili jiné projekty SSL).
5. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt **MvcAuth** a vyberte příkaz **Vlastnosti**.
6. Vyberte **webovou** kartu a vložte adresu URL SSL do pole **Adresa URL projektu.** Uložte soubor (Ctl+S). Tuto adresu URL budete potřebovat ke konfiguraci aplikací pro ověřování na Facebooku a Google.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Přidejte do `Home` řadiče atribut [RequireHttps,](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) který vyžaduje všechny požadavky, musí používat protokol HTTPS. Bezpečnější přístup je přidat [requireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtr do aplikace. Podívejte se &quot;na část Chraňte aplikaci&quot; s SSL a autorizovat atribut v mém kurzu [Vytvořit ASP.NET mvc aplikace s auth a SQL DB a nasadit do služby Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Část ovladače Home je uvedena níže.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Pokud jste certifikát nainstalovali v minulosti, můžete přeskočit zbytek této části a přejít na [vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](#goog), jinak postupujte podle pokynů, abyste důvěřovali certifikátu podepsanému svým držitelem, který služba IIS Express vygenerovala.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Přečtěte si dialogové okno **Upozornění zabezpečení** a klepněte na tlačítko **Ano,** pokud chcete nainstalovat certifikát představující localhost.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. Aplikace IE zobrazuje *domovskou* stránku a neexistují žádná upozornění SSL.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome také přijímá certifikát a zobrazuje obsah HTTPS bez varování. Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění. Pro naši aplikaci můžete bezpečně kliknout **Chápu rizika**.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu

> [!WARNING]
> Aktuální pokyny google oauth [najdete v tématu Konfigurace ověřování Google v ASP.NET jádra](/aspnet/core/security/authentication/social/google-logins).

1. Přejděte do [konzole Google Developers Console](https://console.developers.google.com/).
2. Pokud jste projekt ještě nevytvořili, vyberte na levé kartě **pověření** a pak vyberte **Vytvořit**.
3. Na levé kartě klikněte na **Pověření**.
4. Klepněte na tlačítko **Vytvořit pověření** a potom na **ID klienta OAuth**. 

    1. V dialogovém okně **Vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.
    2. Nastavte autorizované počátky **JavaScriptu** na adresu URL`https://localhost:44300/` SSL, kterou jste použili výše (pokud jste nevytvořili jiné projekty SSL)
    3. Nastavte **identifikátor URI autorizovaného přesměrování** na:  
         `https://localhost:44300/signin-google`
5. Klikněte na položku nabídky obrazovky Souhlas OAuth a nastavte e-mailovou adresu a název produktu. Po dokončení formuláře klepněte na tlačítko **Uložit**.
6. Klikněte na položku nabídky Knihovna, vyhledejte **rozhraní GOOGLE+ API**, klikněte na ni a stiskněte tlačítko Povolit.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   Na obrázku níže jsou zobrazena povolená rozhraní API.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Ve Správci rozhraní API Google navštivte kartu **Přihlašovací údaje** a získejte **ID klienta**. Stažením uložíte soubor JSON s tajnými kódy aplikací. Zkopírujte a vložte **ClientId** `UseGoogleAuthentication` a **ClientSecret** do metody nalezené v souboru *Startup.Auth.cs* ve složce *App_Start.* **ClientId** a **ClientSecret** hodnoty uvedené níže jsou ukázky a nefungují.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Zabezpečení – Nikdy neukládejte citlivá data do zdrojového kódu. Účet a pověření jsou přidány do výše uvedeného kódu, aby vzorek jednoduché. Podívejte se [na doporučené postupy pro nasazování hesel a dalších citlivých dat do ASP.NET a Služby Aplikací Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
8. Stisknutím **kláves CTRL+F5** vytvořte a spusťte aplikaci. Klikněte na odkaz **Přihlásit** se.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. V části **Přihlaste se pomocí jiné služby** **na**Google .  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Pokud zmeškáte některý z výše uvedených kroků, dostanete chybu HTTP 401. Zkontrolujte výše uvedené kroky. Pokud vám chybí požadované nastavení (například **název produktu**), přidejte chybějící položku a uložte; může trvat několik minut, než ověření funguje.
10. Budete přesměrováni na web Google, kde zadáte své přihlašovací údaje.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Po zadání přihlašovacích údajů budete vyzváni k udělení oprávnění webové aplikaci, kterou jste právě vytvořili:
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Klikněte na **Přijmout**. Nyní budete přesměrováni zpět na **registrační** stránku aplikace MvcAuth, kde můžete zaregistrovat svůj účet Google. Máte možnost změnit místní název registrace e-mailu používaný pro váš účet Gmail, ale obecně chcete zachovat výchozí e-mailový alias (to znamená ten, který jste použili pro ověřování). Klepněte na tlačítko **Registrovat**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Vytvoření aplikace na Facebooku a připojení aplikace k projektu

> [!WARNING]
> Aktuální pokyny k ověřování na Facebooku OAuth2 [najdete v tématu Konfigurace ověřování na Facebooku.](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Zkontrolujte údaje o členství

V nabídce **Zobrazení** klepněte na **položku Průzkumník serveru**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Rozbalte **možnost Výchozí připojení (MvcAuth),** rozbalte **položku Tabulky**, klepněte pravým tlačítkem myši na **položku AspNetUsers** a klepněte na příkaz **Zobrazit data tabulky**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![data tabulky aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Přidání dat profilu do třídy uživatele

V této části přidáte datum narození a rodné město k uživatelským datům při registraci, jak je znázorněno na následujícím obrázku.

![reg s domovním městem a Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Otevřete soubor *Models\IdentityModels.cs* a přidejte datum narození a vlastnosti domovského města:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Otevřete soubor *Models\AccountViewModels.cs* a nastavené datum `ExternalLoginConfirmationViewModel`narození a vlastnosti domovského města v .

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Otevřete soubor *Controllers\AccountController.cs* a přidejte kód pro `ExternalLoginConfirmation` datum narození a domovské město v metodě akce, jak je znázorněno:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Přidejte datum narození a rodné město do souboru *Views\Account\ExternalLoginConfirmation.cshtml:*

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Odstraňte databázi členství, abyste mohli znovu zaregistrovat svůj účet na Facebooku u své aplikace a ověřit, že můžete přidat nové datum narození a informace o profilu domovského města.

V **Průzkumníku řešení**klepněte na ikonu **Zobrazit všechny soubory,** potom klepněte pravým tlačítkem myši na příkaz Přidat *\_data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* a klepněte na příkaz **Odstranit**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

V nabídce **Nástroje** klikněte na **Položku Manger balíčků NuGet**a potom klikněte na **konzolu Správce balíčků** (PMC). Do pmc zadejte následující příkazy.

1. Povolit migrace
2. Init pro migraci doplňků
3. Aktualizovat databázi

Spusťte aplikaci a použijte FaceBook a Google pro přihlášení a registraci některých uživatelů.

## <a name="examine-the-membership-data"></a>Zkontrolujte údaje o členství

V nabídce **Zobrazení** klepněte na **položku Průzkumník serveru**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Klepněte pravým tlačítkem myši na **příkaz AspNetUsers** a klepněte na příkaz **Zobrazit data tabulky**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Pole `HomeTown` `BirthDate` a jsou uvedena níže.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Odhlášení aplikace a přihlášení pomocí jiného účtu

Pokud se k aplikaci přihlásíte pomocí Facebooku a pak se odhlásíte a pokusíte se znovu přihlásit pomocí jiného účtu na Facebooku (pomocí stejného prohlížeče), budete okamžitě přihlášeni k předchozímu účtu na Facebooku, který jste použili. Chcete-li používat jiný účet, musíte přejít na Facebook a odhlásit se na Facebooku. Stejné pravidlo platí pro všechny ostatní zprostředkovatele ověřování třetích stran. Případně se můžete přihlásit pomocí jiného účtu pomocí jiného prohlížeče.

## <a name="next-steps"></a>Další kroky

Viz [Představujeme Yahoo a LinkedIn OAuth poskytovatelů zabezpečení pro OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Jerrie Pelser pro Yahoo a LinkedIn pokyny. Viz Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.

Postupujte podle mého kurzu [Vytvořte aplikaci ASP.NET MVC s auth a SQL DB a nasadit do služby Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), která pokračuje v tomto kurzu a ukazuje následující:

1. Jak nasadit aplikaci do Azure.
2. Jak zabezpečit aplikaci s rolemi.
3. Jak zabezpečit aplikaci pomocí filtrů [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) a [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)
4. Jak používat rozhraní API pro členství k přidání uživatelů a rolí.

Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit. Můžete také požádat o nová témata na [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code). Můžete dokonce požádat o nové funkce, které mají být přidány do ASP.NET. Můžete například hlasovat pro nástroj pro [vytváření a správu uživatelů a rolí.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Správné vysvětlení fungování ASP.NET externích ověřovacích služeb naleznete v tématu Externí [ověřovací služby](https://asp.net/web-api/overview/security/external-authentication-services)Roberta McMurrayho . Robert článek také jde do podrobností v povolení Microsoft a Twitter ověřování. Vynikající [ef/MVC kurz](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Toma Dykstra ukazuje, jak pracovat s rámcem entity.
