---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: Pokladna a platba přes PayPal | Dokumenty společnosti Microsoft
author: Erikre
description: Tato série kurzů vás naučí základy vytváření aplikace ASP.NET Web Forms pomocí ASP.NET 4.5 a Microsoft Visual Studio Express 2013 pro We...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676053"
---
# <a name="checkout-and-payment-with-paypal"></a>Pokladna a platba přes PayPal

podle [Erik Reitan](https://github.com/Erikre)

[Stáhněte si wingtip hračky ukázkový projekt (C #)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [stáhnout e-knihy (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Tato série kurzů vás naučí základy vytváření aplikace ASP.NET webových formulářů pomocí ASP.NET 4.5 a Microsoft Visual Studio Express 2013 pro web. Projekt Visual Studio 2013 [se zdrojovým kódem jazyka C#](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) je k dispozici jako doprovodný k této sérii kurzů.

Tento kurz popisuje, jak upravit ukázkovou aplikaci Wingtip Toys tak, aby zahrnovala autorizaci uživatele, registraci a platbu pomocí služby PayPal. K nákupu produktů budou mít oprávnění pouze uživatelé, kteří jsou přihlášeni. Vestavěná funkce registrace uživatelů šablony projektu ASP.NET 4.5 4.5 Web Forms již obsahuje velkou část toho, co potřebujete. Přidáte funkci PayPal Express Checkout. V tomto tutoriálu budete používat testovací prostředí pro vývojáře PayPal, takže nebudou převedeny žádné skutečné finanční prostředky. Na konci tutoriálu otestujete aplikaci výběrem produktů, které chcete přidat do nákupního košíku, kliknutím na tlačítko pokladny a přenosem dat na testovací web PayPal. Na testovacíwebové stránce PayPal potvrdíte své dodací a platební údaje a poté se vrátíte do místní ukázkové aplikace Wingtip Toys, abyste potvrdili a dokončili nákup.

Existuje několik zkušených zpracovatelů plateb třetích stran, kteří se specializují na online nakupování, které řeší škálovatelnost a zabezpečení. ASP.NET vývojáři by měli zvážit výhody využití platebního řešení třetí strany před implementací nákupního a nákupního řešení.

> [!NOTE] 
> 
> Ukázková aplikace Wingtip Toys byla navržena tak, aby zobrazovala specifické ASP.NET koncepty a funkce, které jsou k dispozici ASP.NET webovým vývojářům. Tato ukázková aplikace nebyla optimalizována pro všechny možné okolnosti s ohledem na škálovatelnost a zabezpečení.

## <a name="what-youll-learn"></a>Naučíte se:

- Jak omezit přístup k určitým stránkám ve složce.
- Jak vytvořit známý nákupní košík z anonymního nákupního košíku.
- Jak povolit SSL pro projekt.
- Jak přidat zprostředkovatele OAuth do projektu.
- Jak používat službu PayPal k nákupu produktů pomocí testovacího prostředí PayPal.
- Jak zobrazit podrobnosti z PayPal v ovládacím prvku **DetailsView.**
- Jak aktualizovat databázi aplikace Wingtip Toys s podrobnostmi získanými z PayPal.

## <a name="adding-order-tracking"></a>Přidání sledování objednávek

V tomto kurzu vytvoříte dvě nové třídy pro sledování dat z objednávky, kterou uživatel vytvořil. Třídy budou sledovat údaje týkající se informací o přepravě, celkové částky nákupu a potvrzení o platbě.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Přidání tříd modelu Order a OrderDetail

Dříve v této sérii kurzů jste definovali schéma pro kategorie, produkty a `Category` `Product`položky `CartItem` nákupního košíku vytvořením , a třídy ve složce *Modely.* Nyní přidáte dvě nové třídy k definování schématu pro objednávku produktu a podrobnosti objednávky.

1. Ve složce **Modely** přidejte novou třídu s názvem *Order.cs*.   
   Nový soubor třídy se zobrazí v editoru.
2. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. Přidejte *třídu OrderDetail.cs* do složky *Modely.*
4. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order` Třídy `OrderDetail` a obsahují schéma k definování informací o objednávce použitých pro nákup a expedici.

Kromě toho budete muset aktualizovat třídu kontextu databáze, která spravuje třídy entit a která poskytuje přístup k datům do databáze. Chcete-li to provést, přidáte nově `OrderDetail` vytvořené `ProductContext` Třídy Order a model do třídy.

1. V **Průzkumníku řešení**vyhledejte a otevřete soubor *ProductContext.cs.*
2. Přidejte zvýrazněný kód do *souboru ProductContext.cs,* jak je znázorněno níže:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Jak již bylo zmíněno dříve v této sérii `System.Data.Entity` kurzů, kód v *souboru ProductContext.cs* přidá obor názvů, takže máte přístup ke všem základním funkcím entity frameworku. Tato funkce zahrnuje možnost dotazování, vkládání, aktualizace a odstraňování dat pomocí objektů silného typu. Výše uvedený kód `ProductContext` ve třídě přidá entity `Order` framework `OrderDetail` přístup k nově přidané a třídy.

## <a name="adding-checkout-access"></a>Přidání přístupu k pokladně

Ukázková aplikace Wingtip Toys umožňuje anonymním uživatelům kontrolovat a přidávat produkty do nákupního košíku. Pokud se však anonymní uživatelé rozhodnou zakoupit produkty, které přidali do nákupního košíku, musí se přihlásit k webu. Jakmile se přihlásí, mají přístup k omezeným stránkám webové aplikace, které zpracovávají proces nákupu a nákupu. Tyto stránky s omezeným přístupem jsou obsaženy ve složce *Pokladna* aplikace.

### <a name="add-a-checkout-folder-and-pages"></a>Přidání složky a stránek pokladny

Nyní vytvoříte složku *Pokladna* a stránky v ní, které zákazník uvidí během procesu pokladny. Tyto stránky budete aktualizovat později v tomto kurzu.

1. Klepněte pravým tlačítkem myši na název projektu **(Wingtip Toys**) v **Průzkumníku řešení** a vyberte **přidat novou složku**. 

    ![Pokladna a platba s PayPal - Nová složka](checkout-and-payment-with-paypal/_static/image1.png)
2. Pojmenujte novou složku *Pokladna*.
3. Klikněte pravým tlačítkem myši na složku *Pokladna* a potom vyberte **Přidat**-&gt;**novou položku**. 

    ![Pokladna a platba přes PayPal - Nová položka](checkout-and-payment-with-paypal/_static/image2.png)
4. Zobrazí se dialogové okno **Přidat novou položku**.
5. Vyberte skupinu **webových** šablon **Visual C#**  - &gt; vlevo. Potom v prostředním podokně vyberte **webový formulář se stránkou předlohy**a pojmenujte jej *CheckoutStart.aspx*. 

    ![Pokladna a platba přes PayPal - Dialog přidat novou položku](checkout-and-payment-with-paypal/_static/image3.png)
6. Stejně jako dříve vyberte jako stránku předlohy soubor *Site.Master.*
7. Přidejte následující další stránky do složky *Pokladna* pomocí stejných kroků výše:   

    - PokladníRecenze.aspx
    - PokladnaComplete.aspx
    - CheckoutCancel.aspx
    - Soubor CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Přidání souboru Web.config

Přidáním nového souboru *Web.config* do složky *Pokladna* budete moci omezit přístup ke všem stránkám obsaženým ve složce.

1. Klepněte pravým tlačítkem myši na složku *Pokladna* a vyberte **přidat**  - &gt; **novou položku**.  
   Zobrazí se dialogové okno **Přidat novou položku**.
2. Vyberte skupinu **webových** šablon **Visual C#**  - &gt; vlevo. Potom v prostředním podokně vyberte **možnost Webový konfigurační soubor**, přijměte výchozí název *souboru Web.config*a pak vyberte **Přidat**.
3. Nahraďte existující obsah XML v souboru *Web.config* následujícími:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. Uložte soubor *Web.config*.

Soubor *Web.config* určuje, že všem neznámým uživatelům webové aplikace musí být odepřen přístup ke stránkám obsaženým ve složce *Pokladna.* Pokud však uživatel zaregistroval účet a je přihlášen, bude známým uživatelem a bude mít přístup ke stránkám ve složce *Pokladna.*

Je důležité si uvědomit, že konfigurace ASP.NET se řídí hierarchií, kde každý soubor *Web.config* aplikuje nastavení konfigurace na složku, ve které se nachází, a na všechny podřízené adresáře pod ním.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Povolení ssl pro projekt

 Secure Sockets Layer (SSL) je protokol definovaný tak, aby webové servery a weboví klienti mohli bezpečněji komunikovat pomocí šifrování. Pokud není využito ssl, data odeslaná mezi klientem a serverem jsou otevřena pro paketování všemi, kdo mají fyzický přístup k síti. Kromě toho několik běžných schémat ověřování nejsou zabezpečené přes prosté HTTP. Zejména základní ověřování a ověřování pomocí formulářů odesílají nešifrovaná pověření. Chcete-li být bezpečné, musí tato schémata ověřování používat Protokol SSL. 

1. V **Průzkumníku řešení**klepněte na projekt **WingtipToys** a stisknutím **klávesy F4** zobrazte okno **Vlastnosti.**
2. Změnit **ssl** `true`povoleno na .
3. Zkopírujte **adresu URL SSL,** abyste ji mohli později použít.   
 Adresa URL ssl `https://localhost:44300/` bude, pokud jste dříve nevytvořili webové servery SSL (jak je znázorněno níže).   
    ![Vlastnosti projektu](checkout-and-payment-with-paypal/_static/image4.png)
4. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt **WingtipToys** a klepněte na příkaz **Vlastnosti**.
5. Na levé kartě klikněte na **Web**.
6. Změňte **adresu URL projektu** tak, aby používala adresu URL **SSL,** kterou jste uložili dříve.   
    ![Webové vlastnosti projektu](checkout-and-payment-with-paypal/_static/image5.png)
7. Stránku uložte stisknutím **kombinace kláves CTRL+S**.
8. Stisknutím **kláves Ctrl+F5** spusťte aplikaci. Visual Studio zobrazí možnost, která vám umožní vyhnout se upozornění ssl.
9. Chcete-li důvěřovat certifikátu SSL služby IIS Express a pokračovat, klepněte na tlačítko **Ano.**   
    ![Podrobnosti o certifikátu SSL služby IIS Express](checkout-and-payment-with-paypal/_static/image6.png)  
 Zobrazí se upozornění zabezpečení.
10. Chcete-li certifikát nainstalovat do místního hostitele, klepněte na tlačítko **Ano.**   
    ![Dialogové okno Upozornění zabezpečení](checkout-and-payment-with-paypal/_static/image7.png)  
 Zobrazí se okno prohlížeče.

Nyní můžete snadno testovat webové aplikace místně pomocí SSL.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>Přidat zprostředkovatele OAuth 2.0

ASP.NET web forms poskytuje rozšířené možnosti členství a ověřování. Tato vylepšení zahrnují OAuth. OAuth je otevřený protokol, který umožňuje bezpečnou autorizaci jednoduchou a standardní metodou z webových, mobilních a desktopových aplikací. Šablona ASP.NET Webových formulářů používá oAuth k odhalení Facebooku, Twitteru, Googlu a Microsoftu jako poskytovatelů ověřování. Ačkoli tento kurz používá pouze Google jako zprostředkovatele ověřování, můžete snadno upravit kód tak, aby používal některého z poskytovatelů. Kroky k implementaci jiných zprostředkovatelů jsou velmi podobné krokům, které se zobrazí v tomto kurzu.

Kromě ověřování bude kurz také používat role k implementaci autorizace. Data (vytváření, úpravy nebo odstraňování kontaktů) budou moci měnit pouze uživatelé, které přidáte do `canEdit` role.

> [!NOTE] 
> 
> Aplikace služby Windows Live přijímají pouze živou adresu URL pro pracovní web, takže k testování přihlášení nelze použít místní adresu URL webu.

Následující kroky vám umožní přidat poskytovatele ověřování Google.

1. Otevřete soubor *Start\Startup.Auth.cs.\_*
2. Odeberte znaky `app.UseGoogleAuthentication()` komentáře z metody tak, aby se metoda zobrazí takto: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. Přejděte do [konzole Google Developers Console](https://console.developers.google.com/). Budete se také muset přihlásit pomocí svého e-mailového účtu pro vývojáře Google (gmail.com). Pokud nemáte účet Google, vyberte odkaz **Vytvořit účet.**   
   Dále se zobrazí **google vývojářská konzola**.   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. Klepněte na tlačítko **Vytvořit projekt** a zadejte název projektu a ID (můžete použít výchozí hodnoty). Potom klikněte na **zaškrtávací políčko smlouvy** a na tlačítko **Vytvořit.**  

    ![Google - Nový projekt](checkout-and-payment-with-paypal/_static/image9.png)

   Během několika sekund bude vytvořen nový projekt a váš prohlížeč zobrazí stránku nových projektů.
5. Na levé kartě klikněte na **auth &amp; s ustálená**a potom na **položku Pověření**.
6. Klepněte na **tlačítko Vytvořit nové ID klienta** v části **OAuth**.   
   Zobrazí se dialogové okno **Vytvořit ID klienta.**   
    ![Google - Vytvořit ID klienta](checkout-and-payment-with-paypal/_static/image10.png)
7. V dialogovém okně **Vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.
8. Nastavte **autorizované počátky JavaScriptu** na adresu URL SSL, kterou jste použili dříve v tomto kurzu (pokud`https://localhost:44300/` jste nevytvořili jiné projekty SSL).   
   Tato adresa URL je původem vaší aplikace. Pro tuto ukázku zadáte pouze adresu URL testu localhost. Můžete však zadat více adres URL pro účet localhost a produkční.
9. Nastavte **identifikátor URI autorizovaného přesměrování** na následující: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Tato hodnota je identifikátor URI, který ASP.NET uživatelům OAuth ke komunikaci se serverem Google OAuth. Zapamatujte si adresu URL SSL, kterou jste použili výše (pokud `https://localhost:44300/` jste nevytvořili jiné projekty SSL).
10. Klepněte na tlačítko **Vytvořit ID klienta.**
11. V levé nabídce konzole Google Developers Console klikněte na položku nabídky **obrazovky Souhlas** a nastavte e-mailovou adresu a název produktu. Po dokončení formuláře klepněte na tlačítko **Uložit**.
12. Klikněte na položku nabídky **rozhraní API,** posuňte se dolů a klikněte na tlačítko **off** vedle **rozhraní Google+ API**.   
    Přijetím této možnosti umožníte rozhraní Google+ API.
13. Je také nutné aktualizovat balíček **Microsoft.Owin** NuGet na verzi 3.0.0.   
    V nabídce **Nástroje** vyberte **Správce balíčků NuGet** a pak vyberte **Spravovat balíčky NuGet pro řešení**.  
    V okně **Spravovat balíčky NuGet** vyhledejte a aktualizujte balíček **Microsoft.Owin** na verzi 3.0.0.
14. V sadě Visual `UseGoogleAuthentication` Studio aktualizujte metodu *Startup.Auth.cs* stránce zkopírováním a vložením **ID klienta** a **tajného klíče klienta** do metody. Níže uvedené **hodnoty ID klienta** a **tajný klíč klienta** jsou ukázky a nebudou fungovat. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Stisknutím **kláves CTRL+F5** vytvořte a spusťte aplikaci. Klikněte na odkaz **Přihlásit** se.
16. V části **Přihlaste se pomocí jiné služby** **na**Google .  
    ![Přihlásit se](checkout-and-payment-with-paypal/_static/image11.png)
17. Pokud potřebujete zadat své přihlašovací údaje, budete přesměrováni na web Google, kde zadáte své přihlašovací údaje.  
    ![Google – přihlášení](checkout-and-payment-with-paypal/_static/image12.png)
18. Po zadání přihlašovacích údajů budete vyzváni k udělení oprávnění webové aplikaci, kterou jste právě vytvořili.  
    ![Výchozí účet služby projektu](checkout-and-payment-with-paypal/_static/image13.png)
19. Klikněte na **Přijmout**. Nyní budete přesměrováni zpět na stránku **Registrovat** aplikace **WingtipToys,** kde můžete zaregistrovat svůj účet Google.  
    ![Zaregistrujte se pomocí účtu Google](checkout-and-payment-with-paypal/_static/image14.png)
20. Máte možnost změnit místní název registrace e-mailu používaný pro váš účet Gmail, ale obecně chcete zachovat výchozí e-mailový alias (to znamená ten, který jste použili pro ověřování). Klikněte **na Přihlásit,** jak je uvedeno výše.

### <a name="modifying-login-functionality"></a>Změna funkce přihlášení

Jak již bylo zmíněno v této sérii kurzů, velká část funkce registrace uživatelů byla ve výchozím nastavení zahrnuta do šablony ASP.NET webových formulářů. Nyní změníte výchozí *login.aspx* a *Register.aspx* `MigrateCart` stránky volat metodu. Metoda `MigrateCart` přidruží nově přihlášeného uživatele k anonymnímu nákupnímu košíku. Přisuzováním uživatele a nákupního košíku bude ukázková aplikace Wingtip Toys schopna udržovat nákupní košík uživatele mezi návštěvami.

1. V **Průzkumníku řešení**vyhledejte a otevřete složku *Účet.*
2. Upravte stránku s názvem Login.aspx.cs s názvem *Login.aspx.cs* tak, aby obsahovala kód zvýrazněný žlutě, aby se zobrazil a zobrazil se takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. Uložte *soubor Login.aspx.cs.*

Prozatím můžete ignorovat upozornění, že neexistuje žádná `MigrateCart` definice pro metodu. Budete přidávat o něco později v tomto kurzu.

Soubor *Login.aspx.cs* kód na pozadí podporuje metodu Přihlášení. Kontrolou Login.aspx stránky, uvidíte, že tato stránka obsahuje tlačítko "Přihlásit", `LogIn` které po kliknutí aktivuje obslužnou rutinu na kód na pozadí.

Při `Login` volání metody na *Login.aspx.cs* je vytvořena nová instance `usersShoppingCart` nákupního košíku s názvem. ID nákupního košíku (GUID) je načtena `cartId` a nastavena na proměnnou. Potom `MigrateCart` je volána metoda, `cartId` předávání a název přihlášeného uživatele do této metody. Při migraci nákupního košíku je identifikátor GUID použitý k identifikaci anonymního nákupního košíku nahrazen uživatelským jménem.

Kromě úpravy souboru *Login.aspx.cs* kódu na pozadí pro migraci nákupního košíku při přihlášení uživatele, musíte také upravit *soubor Register.aspx.cs kód na pozadí* pro migraci nákupního košíku, když uživatel vytvoří nový účet a přihlásí se.

1. Ve složce *Účet* otevřete soubor s názvem *Register.aspx.cs*.
2. Upravte soubor s kódem na pozadí zahrnutím kódu žlutě tak, aby se zobrazil takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. Uložte *soubor Register.aspx.cs.* Opět ignorujte upozornění o `MigrateCart` metodě.

Všimněte si, že `CreateUser_Click` kód, který jste použili v `LogIn` obslužné rutině události, je velmi podobný kódu, který jste použili v metodě. Když se uživatel zaregistruje nebo přihlásí k webu, `MigrateCart` bude provedeno volání metody.

## <a name="migrating-the-shopping-cart"></a>Migrace nákupního košíku

Nyní, když máte aktualizovaný proces přihlášení a registrace, můžete přidat kód pro `MigrateCart` migraci nákupního košíku pomocí metody.

1. V **Průzkumníku řešení**vyhledejte složku *Logika* a otevřete soubor *třídy ShoppingCartActions.cs.*
2. Přidejte kód zvýrazněný žlutě do existujícího kódu v *souboru ShoppingCartActions.cs,* aby se kód v *ShoppingCartActions.cs* souboru zobrazil takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

Metoda `MigrateCart` používá existující cartId najít nákupní košík uživatele. Dále kód prochází všechny položky nákupního košíku `CartId` a nahradí vlastnost `CartItem` (jak je určeno schématem) přihlášené uživatelské jméno.

### <a name="updating-the-database-connection"></a>Aktualizace připojení k databázi

Pokud používáte tento kurz pomocí **předdefinované** ukázkové aplikace Wingtip Toys, musíte znovu vytvořit výchozí databázi členství. Změnou výchozího připojovacího řetězce bude při příštím spuštění aplikace vytvořena databáze členství.

1. Otevřete soubor *Web.config* v kořenovém adresáři projektu.
2. Aktualizujte výchozí připojovací řetězec tak, aby se zobrazil takto:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>Integrace PayPal

PayPal je webová fakturační platforma, která přijímá platby online obchodníky. Tento kurz dále vysvětluje, jak integrovat funkci Express Checkout společnosti PayPal do vaší aplikace. Express Checkout umožňuje vašim zákazníkům používat PayPal k placení za položky, které přidali do svého nákupního košíku.

### <a name="create-paypal-test-accounts"></a>Vytvořit testovací účty PayPal

Chcete-li používat testovací prostředí PayPal, musíte vytvořit a ověřit testovací účet pro vývojáře. Pomocí testovacího účtu vývojáře vytvoříte testovací účet kupujícího a testovací účet prodejce. Přihlašovací údaje testovacího účtu pro vývojáře také umožní ukázkové aplikaci Wingtip Toys přístup k testovacímu prostředí PayPal.

1. V prohlížeči přejděte na testovací web pro vývojáře PayPal:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. Pokud nemáte vývojářský účet PayPal, vytvořte si nový účet kliknutím na **Zaregistrovat se**a podle kroků registrace. Pokud máte existující vývojářský účet PayPal, přihlaste se kliknutím na **Přihlásit se**. Budete potřebovat svůj vývojářský účet PayPal k testování ukázkové aplikace Wingtip Toys dále v tomto kurzu.
3. Pokud jste se právě zaregistrovali ke svému vývojářskému účtu PayPal, možná budete muset ověřit svůj vývojářský účet PayPal u služby PayPal. Svůj účet můžete ověřit podle kroků, které vám společnost PayPal odeslala na váš e-mailový účet. Po ověření vývojářského účtu PayPal se znovu přihlaste na testovací web pro vývojáře PayPal.
4. Poté, co jste přihlášeni na web pro vývojáře PayPal pomocí svého vývojářského účtu PayPal, musíte si vytvořit testovací účet kupujícího PayPal, pokud ho ještě nemáte. Pokud chcete vytvořit testovací účet kupujícího, klikněte na webu PayPal na kartu **Aplikace** a potom klikněte na **účty izolovaného prostoru**.   
 Zobrazí se stránka **Testovací účty izolovaného** prostoru.   

    > [!NOTE] 
    > 
    > Web pro vývojáře služby PayPal již poskytuje testovací účet obchodníka.

    ![Pokladna a platba pomocí testovacích účtů PayPal - Sandbox](checkout-and-payment-with-paypal/_static/image15.png)
5. Na stránce Testovací účty sandboxu klikněte na **Vytvořit účet**.
6. Na stránce **Vytvořit testovací účet** zvolte e-mail a heslo testovacího účtu kupujícího podle vašeho výběru.   

    > [!NOTE] 
    > 
    > Budete potřebovat e-mailové adresy a heslo kupujícího k testování ukázkové aplikace Wingtip Toys na konci tohoto kurzu.

    ![Pokladna a platba pomocí testovacích účtů PayPal - Sandbox](checkout-and-payment-with-paypal/_static/image16.png)
7. Vytvořte testovací účet kupujícího kliknutím na tlačítko **Vytvořit účet.**  
 Zobrazí se stránka **Účty testu izolovaného** prostoru. 

    ![Pokladna a platba pomocí paypal - PayPal účty](checkout-and-payment-with-paypal/_static/image17.png)
8. Na stránce **Testovací účty sandboxu** klikněte na e-mailový účet **zprostředkovatele.**  
    Zobrazí se možnosti **profilu** a **oznámení.**
9. Vyberte možnost **Profil** a kliknutím na **přihlašovací údaje rozhraní API** zobrazte přihlašovací údaje rozhraní API pro testovací účet obchodníka.
10. Zkopírujte pověření rozhraní API TEST do poznámkového bloku.

K volání rozhraní API z ukázkové aplikace Wingtip Toys do testovacího prostředí PayPal budete potřebovat zobrazená pověření rozhraní API Classic TEST API (uživatelské jméno, heslo a podpis). Pověření přidáte v dalším kroku.

### <a name="add-paypal-class-and-api-credentials"></a>Přidání přihlašovacích údajů ke třídě PayPal a rozhraní API

Většinu kódu PayPal umístíte do jedné třídy. Tato třída obsahuje metody používané ke komunikaci s PayPal. Také přidáte své paypal pověření do této třídy.

1. V ukázkové aplikaci Wingtip Toys v sadě Visual Studio klikněte pravým tlačítkem myši na složku **Logika** a pak vyberte **Přidat**  - &gt; **novou položku**.   
   Zobrazí se dialogové okno **Přidat novou položku**.
2. V **části Visual C#** v **podokně Nainstalováno** vlevo vyberte **kód**.
3. Ve středním podokně vyberte **Třídu**. Pojmenujte tuto novou třídu **PayPalFunctions.cs**.
4. Klikněte na **Přidat**.  
   Nový soubor třídy se zobrazí v editoru.
5. Nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. Přidejte přihlašovací údaje rozhraní API obchodníka (uživatelské jméno, heslo a podpis), které jste zobrazili dříve v tomto kurzu, abyste mohli volat funkce do testovacího prostředí PayPal.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> V této ukázkové aplikaci jednoduše přidáváte pověření do souboru Jazyka C# (.cs). V implementovaném řešení byste však měli zvážit šifrování pověření v konfiguračním souboru.

Třída NVPAPICaller obsahuje většinu funkcí PayPal. Kód ve třídě poskytuje metody potřebné k nákupu testu z testovacího prostředí PayPal. Následující tři funkce PayPal se používají k nákupu:

- `SetExpressCheckout`Funkce
- `GetExpressCheckoutDetails`Funkce
- `DoExpressCheckoutPayment`Funkce

Metoda `ShortcutExpressCheckout` shromažďuje informace o testovacím nákupu a podrobnosti `SetExpressCheckout` o produktu z nákupního košíku a volá funkci PayPal. Metoda `GetCheckoutDetails` potvrzuje podrobnosti o `GetExpressCheckoutDetails` nákupu a volá funkci PayPal před provedením testovacího nákupu. Metoda `DoCheckoutPayment` dokončí testovací nákup z testovacího prostředí `DoExpressCheckoutPayment` voláním funkce PayPal. Zbývající kód podporuje metody a proces PayPal, jako jsou kódovací řetězce, dekódovací řetězce, pole zpracování a určení pověření.

> [!NOTE] 
> 
> PayPal umožňuje zahrnout volitelné podrobnosti o nákupu na základě [specifikace rozhraní API společnosti PayPal](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout). Rozšířením kódu v ukázkové aplikaci Wingtip Toys můžete zahrnout podrobnosti lokalizace, popisy produktů, daň, číslo zákaznického servisu a mnoho dalších volitelných polí.

Všimněte si, že vrácené a zrušit adresy URL, které jsou zadány v **metodě ShortcutExpressCheckout,** používají číslo portu.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Pokud visual web developer spustí webový projekt pomocí ssl, obvykle port 44300 se používá pro webový server. Jak je uvedeno výše, číslo portu je 44300. Při spuštění aplikace se může zobrazit jiné číslo portu. Číslo portu musí být správně nastaveno v kódu, abyste mohli úspěšně spustit ukázkovou aplikaci Wingtip Toys na konci tohoto kurzu. Další část tohoto kurzu vysvětluje, jak načíst číslo místního portu hostitele a aktualizovat třídu PayPal.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>Aktualizace čísla portu LocalHost ve třídě PayPal

Ukázková aplikace Wingtip Toys nakupuje produkty tak, že přejdete na testovací web PayPal a vrátíte se k místní instanci ukázkové aplikace Wingtip Toys. Chcete-li, aby se paypal vrátil na správnou adresu URL, musíte zadat číslo portu místně spuštěné ukázkové aplikace ve výše uvedeném kódu PayPal.

1. Klepněte pravým tlačítkem myši na název projektu **(WingtipToys**) v **Průzkumníku řešení** a vyberte **vlastnosti**.
2. V levém sloupci vyberte **webovou** kartu.
3. Načtěte číslo portu z pole **Adresa URL projektu.**
4. V případě potřeby `returnURL` `cancelURL` aktualizujte třídu`NVPAPICaller`a ve třídě PayPal ( ) v *souboru PayPalFunctions.cs,* abyste použili číslo portu webové aplikace:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Nyní kód, který jste přidali bude odpovídat očekávaný port pro místní webové aplikace. Společnost PayPal se bude moci vrátit na správnou adresu URL ve vašem místním počítači.

### <a name="add-the-paypal-checkout-button"></a>Přidat tlačítko PayPal Checkout

Nyní, když primární PayPal funkce byly přidány do ukázkové aplikace, můžete začít přidávat značky a kód potřebný k volání těchto funkcí. Nejprve je nutné přidat tlačítko pro nákup, které se uživateli zobrazí na stránce nákupního košíku.

1. Otevřete soubor *ShoppingCart.aspx.*
2. Přejděte do dolní části souboru a vyhledejte `<!--Checkout Placeholder -->` komentář.
3. Nahraďte komentář `ImageButton` ovládacím prvkem tak, aby byla značka nahrazena následujícím způsobem:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. V *souboru ShoppingCart.aspx.cs* `UpdateBtn_Click` po obslužné rutině `CheckOutBtn_Click` události ke konci souboru přidejte obslužnou rutinu události:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. Také v *ShoppingCart.aspx.cs* souboru přidejte `CheckoutBtn`odkaz na , tak, aby nové tlačítko obrázku je odkazováno takto:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Uložte změny do souboru *ShoppingCart.aspx* i *do ShoppingCart.aspx.cs* souboru.
7. V nabídce vyberte **Ladit**-&gt;**build wingtiptoys**.  
   Projekt bude znovu sestaven s nově přidaným ovládacím prvkem **ImageButton.**

### <a name="send-purchase-details-to-paypal"></a>Odeslat podrobnosti o nákupu na PayPal

Když uživatel klikne na tlačítko **Pokladna** na stránce nákupního košíku *(ShoppingCart.aspx*), zahájí proces nákupu. Následující kód volá první funkci PayPal potřebnou k nákupu produktů.

1. Ve složce *Pokladna* otevřete soubor s kódem na pozadí s názvem *CheckoutStart.aspx.cs*.   
   Nezapomeňte otevřít soubor s kódem na pozadí.
2. Nahraďte existující kód následujícími:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Když uživatel aplikace klikne na tlačítko **Pokladna** na stránce nákupního košíku, prohlížeč přejde na stránku *CheckoutStart.aspx.* Když se načte stránka *CheckoutStart.aspx,* `ShortcutExpressCheckout` je volána metoda. V tomto okamžiku je uživatel převeden na testovací web PayPal. Na webu PayPal uživatel zadá své přihlašovací údaje paypal, zkontroluje podrobnosti o nákupu, přijme smlouvu `ShortcutExpressCheckout` PayPal a vrátí se do ukázkové aplikace Wingtip Toys, kde se metoda dokončí. Po `ShortcutExpressCheckout` dokončení metody přesměruje uživatele na stránku *CheckoutReview.aspx* `ShortcutExpressCheckout` zadanou v metodě. To umožňuje uživateli zkontrolovat podrobnosti objednávky z ukázkové aplikace Wingtip Toys.

### <a name="review-order-details"></a>Zkontrolovat podrobnosti objednávky

Po návratu z PayPal, *CheckoutReview.aspx* stránky Wingtip hračky ukázkové aplikace zobrazí podrobnosti objednávky. Tato stránka umožňuje uživateli zkontrolovat podrobnosti objednávky před nákupem produktů. Stránka *CheckoutReview.aspx* musí být vytvořena následujícím způsobem:

1. Ve složce *Pokladna* otevřete stránku s názvem *CheckoutReview.aspx*.
2. Nahraďte existující značky následujícími značkami:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. Otevřete stránku s názvem *CheckoutReview.aspx.cs* a nahraďte existující kód následujícím:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

Ovládací prvek **DetailsView** slouží k zobrazení podrobností objednávky, které byly vráceny z PayPal. Výše uvedený kód také uloží podrobnosti objednávky do `OrderDetail` databáze Wingtip Toys jako objekt. Když uživatel klikne na tlačítko **Dokončit objednávku,** bude přesměrován na stránku *CheckoutComplete.aspx.*

> [!NOTE] 
> 
> **Tip**
> 
> Ve značkách na stránce *CheckoutReview.aspx* si `<ItemStyle>` všimněte, že značka se používá ke změně stylu položek v ovládacím prvku **DetailsView** v dolní části stránky. Zobrazením stránky v **návrhovém zobrazení** (výběrem **možnosti Návrh** v levém dolním rohu sady Visual Studio), výběrem ovládacího prvku **DetailsView** a výběrem **inteligentní značky** (ikona šipky v pravém horním rohu ovládacího prvku) budete moci zobrazit **funkce DetailsView Tasks**.
> 
> ![Pokladna a platba přes PayPal - Upravit pole](checkout-and-payment-with-paypal/_static/image18.png)
> 
> Výběrem **možnosti Upravit pole**se zobrazí dialogové okno **Pole.** V tomto dialogovém okně můžete snadno řídit vizuální vlastnosti ovládacího prvku **DetailView,** například **ItemStyle**.
> 
> ![Pokladna a platba pomocí paypalu - dialog Pole](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Kompletní nákup

*Stránka CheckoutComplete.aspx* provádí nákup od společnosti PayPal. Jak bylo uvedeno výše, uživatel musí kliknout na tlačítko **Dokončit objednávku,** než aplikace přejde na stránku *CheckoutComplete.aspx.*

1. Ve složce *Pokladna* otevřete stránku s názvem *CheckoutComplete.aspx*.
2. Nahraďte existující značky následujícími značkami:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. Otevřete stránku s názvem *CheckoutComplete.aspx.cs* a nahraďte existující kód následujícím:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

Při načtení stránky *CheckoutComplete.aspx* je `DoCheckoutPayment` volána metoda. Jak již bylo `DoCheckoutPayment` zmíněno dříve, metoda dokončí nákup z testovacího prostředí PayPal. Po dokončení nákupu objednávky společností PayPal se na stránce *CheckoutComplete.aspx* zobrazí kupujícímu platební transakce. `ID`

### <a name="handle-cancel-purchase"></a>Zpracovat zrušit nákup

Pokud se uživatel rozhodne nákup zrušit, bude přesměrován na stránku *CheckoutCancel.aspx,* kde uvidí, že jejich objednávka byla zrušena.

1. Otevřete stránku s názvem *CheckoutCancel.aspx* ve složce *Pokladna.*
2. Nahraďte existující značky následujícími značkami:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Zpracování chyb nákupu

Chyby během procesu nákupu budou zpracovány stránkou *CheckoutError.aspx.* Kód na pozadí stránky *CheckoutStart.aspx,* stránka *CheckoutReview.aspx* a stránka *CheckoutComplete.aspx* budou přesměrovávat na stránku *CheckoutError.aspx,* pokud dojde k chybě.

1. Otevřete stránku s názvem *CheckoutError.aspx* ve složce *Pokladna.*
2. Nahraďte existující značky následujícími značkami:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

Stránka *CheckoutError.aspx* se zobrazí s podrobnostmi o chybě, když dojde k chybě během procesu pokladny.

## <a name="running-the-application"></a>Spuštění aplikace

Spusťte aplikaci a zjistěte, jak nakupovat produkty. Všimněte si, že budete spuštěnv testovacím prostředí PayPal. Žádné skutečné peníze se nevyměňují.

1. Ujistěte se, že jsou všechny soubory uloženy v sadě Visual Studio.
2. Otevřete webový prohlížeč [https://developer.paypal.com](https://developer.paypal.com/)a přejděte na stránku .
3. Přihlaste se pomocí vývojářského účtu PayPal, který jste vytvořili dříve v tomto kurzu.  
   Pro sandbox pro vývojáře PayPal musíte být [https://developer.paypal.com](https://developer.paypal.com/) přihlášeni k testování expresní pokladny. To platí pouze pro testování izolovaného prostoru společnosti PayPal, nikoli pro živé prostředí služby PayPal.
4. V sadě Visual Studio spusťte klávesu **F5** ukázkovou aplikaci Wingtip Toys.  
   Po znovuvytvoření databáze se prohlížeč otevře a zobrazí stránku *Default.aspx.*
5. Přidejte do nákupního košíku tři různé produkty tak, že vyberete kategorii produktu, například "Auta", a pak kliknete **na Přidat do košíku** vedle každého produktu.  
   V nákupním košíku se zobrazí vybraný produkt.
6. Klikněte na tlačítko **PayPal** k pokladně. 

    ![Pokladna a platba přes PayPal - Košík](checkout-and-payment-with-paypal/_static/image20.png)

   Odhlášení bude vyžadovat, abyste měli uživatelský účet pro ukázkovou aplikaci Wingtip Toys.
7. Kliknutím na odkaz **Google** vpravo od stránky se přihlaste pomocí existujícího gmail.com e-mailového účtu.  
   Pokud nemáte gmail.com účet, můžete jej vytvořit pro testovací účely na [www.gmail.com](https://www.gmail.com/). Můžete také použít standardní místní účet kliknutím na tlačítko "Registrovat". 

    ![Pokladna a platba přes PayPal - Přihlaste se](checkout-and-payment-with-paypal/_static/image21.png)
8. Přihlaste se pomocí svého účtu gmail a hesla. 

    ![Pokladna a platba přes PayPal - Přihlášení do Gmailu](checkout-and-payment-with-paypal/_static/image22.png)
9. Klikněte na tlačítko **Přihlásit** se zaregistrovat svůj účet gmail s wingtip hračky ukázkové aplikace uživatelské jméno. 

    ![Pokladna a platba přes PayPal - Registrační účet](checkout-and-payment-with-paypal/_static/image23.png)
10. Na testovacím webu PayPal přidejte e-mailovou adresu a heslo **kupujícího,** které jste vytvořili dříve v tomto kurzu, a klikněte na tlačítko **Přihlásit se.** 

    ![Pokladna a platba přes PayPal – přihlášení přes PayPal](checkout-and-payment-with-paypal/_static/image24.png)
11. Souhlasíte se zásadami paypal a klikněte na tlačítko **Souhlasit a pokračovat.**  
    Upozorňujeme, že tato stránka se zobrazuje pouze při prvním použití tohoto účtu PayPal. Opět si všimněte, že se jedná o testovací účet, žádné skutečné peníze se vyměňují. 

    ![Pokladna a platba přes PayPal – zásady pro paypal](checkout-and-payment-with-paypal/_static/image25.png)
12. Zkontrolujte informace o objednávce na stránce kontroly testovacího prostředí PayPal a klepněte na tlačítko **Pokračovat**. 

    ![Pokladna a platba přes PayPal - Informace o kontrole](checkout-and-payment-with-paypal/_static/image26.png)
13. Na stránce *CheckoutReview.aspx* ověřte částku objednávky a zobrazte vygenerovanou dodací adresu. Potom klikněte na tlačítko **Dokončit objednávku.** 

    ![Pokladna a platba s PayPal - Recenze objednávky](checkout-and-payment-with-paypal/_static/image27.png)
14. Stránka **CheckoutComplete.aspx** se zobrazí s ID platební transakce. 

    ![Pokladna a platba s PayPal - Pokladna dokončena](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Kontrola databáze

Kontrolou aktualizovaných dat v databázi ukázkové aplikace Wingtip Toys po spuštění aplikace uvidíte, že aplikace úspěšně zaznamenala nákup produktů.

Data obsažená v databázovém souboru *Wingtiptoys.mdf* můžete zkontrolovat pomocí okna **Průzkumník databáze** (Okno**Průzkumníka serveru** v sadě Visual Studio) jako dříve v této sérii kurzů.

1. Pokud je okno prohlížeče stále otevřené, zavřete okno prohlížeče.
2. V Sadě Visual Studio vyberte ikonu **Zobrazit všechny soubory** v horní části **Průzkumníka řešení,** abyste mohli rozbalit složku **Data\_aplikace.**
3. Rozbalte složku **Data aplikace.\_**  
 Možná budete muset vybrat ikonu **Zobrazit všechny soubory** pro složku.
4. Klepněte pravým tlačítkem myši na databázový soubor *Wingtiptoys.mdf* a vyberte **příkaz Otevřít**.  
    Zobrazí se **Průzkumník serveru.**
5. Rozbalte složku **Tabulky.**
6. Klikněte pravým tlačítkem myši na tabulku **Objednávky**a vyberte **zobrazit data tabulky**.  
 Zobrazí se tabulka **Objednávky.**
7. Zkontrolujte sloupec **PaymentTransactionID** a potvrďte úspěšné transakce. 

    ![Pokladna a platba s PayPal - Recenze databáze](checkout-and-payment-with-paypal/_static/image29.png)
8. Zavřete okno tabulky **Objednávky.**
9. V Průzkumníkovi serveru klepněte pravým tlačítkem myši na tabulku **OrderDetails** a vyberte **zobrazit data tabulky**.
10. Zkontrolujte `OrderId` `Username` hodnoty a v tabulce **OrderDetails.** Všimněte si, `OrderId` že `Username` tyto hodnoty odpovídají hodnotám a zahrnutým v tabulce **Objednávky.**
11. Zavřete okno tabulky **OrderDetails.**
12. Klepněte pravým tlačítkem myši na databázový soubor Wingtip Toys (*Wingtiptoys.mdf*) a vyberte **příkaz Zavřít připojení**.
13. Pokud se okno **Průzkumník řešení** nezobrazuje, klikněte v dolní části okna **Průzkumníkserveru** na **Průzkumníkřešení** a průzkumník **řešení** znovu zobrazte.

## <a name="summary"></a>Souhrn

V tomto kurzu jste přidali schémata podrobností objednávky a objednávky ke sledování nákupu produktů. Také jste integrovali funkci PayPal do ukázkové aplikace Wingtip Toys.

## <a name="additional-resources"></a>Další zdroje

[ASP.NET konfigurace – přehled](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Nasazení zabezpečené aplikace ASP.NET webových formulářů s členstvím, oauth a databází SQL do služby Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure – bezplatná zkušební verze](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Disclaimer

Tento kurz obsahuje ukázkový kód. Takový ukázkový kód je poskytován "tak, jak je" bez jakékoli záruky. Společnost Microsoft tedy nezaručuje přesnost, integritu ani kvalitu ukázkového kódu. Souhlasíte s použitím ukázkového kódu na vlastní nebezpečí. Společnost Microsoft vůči vám nebude za žádných okolností odpovědná za žádný ukázkový kód, obsah, včetně, ale nikoli výhradně, jakýchkoli chyb nebo opomenutí v jakémkoli ukázkovém kódu, obsahu nebo jakékoli ztrátě nebo poškození jakéhokoli druhu, které vznikly v důsledku použití jakéhokoli ukázkového kódu. Tímto jste informováni a tímto souhlasíte s tím, že odškodníte, uložíte a ochráníte společnost Microsoft před jakoukoli ztrátou, nároky na ztrátu, zranění nebo poškození jakéhokoli druhu, včetně, bez omezení, těch, které jsou způsobeny nebo které vyplývají z materiálu, který zveřejníte, předáte, použijete nebo spoléháte na včetně, ale nikoli výhradně, názorů vyjádřených v nich.

> [!div class="step-by-step"]
> [Předchozí](shopping-cart.md)
> [další](membership-and-administration.md)
