---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: Ověřování uživatelských přihlašovacích údajů proti uživatelskému úložišti členství (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele proti úložišti uživatelů členství pomocí programových prostředků a přihlašovacího ovládacího prvku....
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: fd50f4e63c75cf77eb21629d0c11a859da6b357d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045231"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>Ověření přihlašovacích údajů uživatele v úložišti uživatelů, kteří jsou členy (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele pro uživatelské úložiště členství pomocí programových prostředků a přihlašovacího ovládacího prvku. Také se podíváme na to, jak přizpůsobit vzhled a chování ovládacího prvku pro přihlášení.

## <a name="introduction"></a>Úvod

V <a id="Tutorial05"></a> [předchozím kurzu](creating-user-accounts-cs.md) jsme se podívali na postup vytvoření nového uživatelského účtu v rámci sady členství. Nejdříve jsme prohlédli programově vytváření uživatelských účtů prostřednictvím `Membership` metody třídy `CreateUser` a pak prozkoumali pomocí webového ovládacího prvku ovládacím CreateUserWizard. Přihlašovací stránka teď ale ověřuje zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelských jmen a hesel. Musíme aktualizovat logiku přihlašovací stránky tak, aby ověřovala přihlašovací údaje pro uživatelské úložiště v rozhraní .NET Framework.

Podobně jako při vytváření uživatelských účtů lze přihlašovací údaje ověřit programově nebo deklarativně. Rozhraní API pro členství zahrnuje metodu pro programové ověření přihlašovacích údajů uživatele proti uživatelskému úložišti. A ASP.NET se dodává s přihlašovacím webovým ovládacím prvkem, který vykreslí uživatelské rozhraní s textovým polem pro uživatelské jméno a heslo a tlačítko pro přihlášení.

V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele pro uživatelské úložiště členství pomocí programových prostředků a přihlašovacího ovládacího prvku. Také se podíváme na to, jak přizpůsobit vzhled a chování ovládacího prvku pro přihlášení. Pusťme se do toho.

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>Krok 1: ověření přihlašovacích údajů proti uživatelskému úložišti členství

Pro weby, které používají ověřování pomocí formulářů, se uživatel přihlašuje k webu návštěvou přihlašovací stránky a zadáním jejich přihlašovacích údajů. Tyto přihlašovací údaje se pak porovnají s uživatelským úložištěm. Pokud jsou platné, pak se uživateli udělí lístek ověřování pomocí formulářů, což je token zabezpečení, který označuje identitu a pravost návštěvníka.

Chcete-li ověřit uživatele v rámci rozhraní členství, použijte `Membership` [ `ValidateUser` metodu](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)třídy. `ValidateUser`Metoda přijímá dva vstupní parametry- *`username`* a *`password`* a vrátí logickou hodnotu, která označuje, zda byla pověření platná. Podobně jako u `CreateUser` metody, kterou jsme prozkoumali v předchozím kurzu, `ValidateUser` Metoda deleguje skutečné ověření nakonfigurovanému zprostředkovateli členství.

`SqlMembershipProvider`Ověří zadané přihlašovací údaje tím, že získá heslo zadaného uživatele prostřednictvím `aspnet_Membership_GetPasswordWithFormat` uložené procedury. Zajistěte, aby `SqlMembershipProvider` ukládala hesla uživatelů pomocí jednoho ze tří formátů: Clear, Encrypted nebo hash. `aspnet_Membership_GetPasswordWithFormat`Uložená procedura vrátí heslo v nezpracovaném formátu. Pro šifrovaná hesla nebo hesla s algoritmem hash `SqlMembershipProvider` transformuje *`password`* hodnotu předanou do `ValidateUser` metody do jejího ekvivalentu nebo ve stavu hash a pak ji porovná s tím, co bylo vráceno z databáze. Pokud heslo uložené v databázi odpovídá formátovanému heslu zadanému uživatelem, přihlašovací údaje jsou platné.

Pojďme aktualizovat přihlašovací stránku (~/ `Login.aspx` ), aby ověřila zadané přihlašovací údaje v úložišti uživatelů rozhraní .NET Framework. Tuto přihlašovací stránku jsme vytvořili zpátky v <a id="Tutorial02"></a> [*přehledu kurzu ověřování pomocí formulářů*](../introduction/an-overview-of-forms-authentication-cs.md) , vytváření rozhraní se dvěma textboxy pro uživatelské jméno a heslo, zaškrtávací políčko pro zapamatování identity a přihlašovací tlačítko (viz obrázek 1). Kód ověří zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelského jména a hesla (Scott/Password, Jisun/Password a Sam/Password). V kurzu <a id="Tutorial03"></a> [*Konfigurace ověřování a Pokročilá témata*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) jsme aktualizovali kód přihlašovací stránky pro ukládání dalších informací do vlastnosti ověřovacího lístku formuláře `UserData` .

[![Rozhraní přihlašovací stránky obsahuje dvě textová pole, CheckBoxList a tlačítko.](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**Obrázek 1**: rozhraní přihlašovací stránky obsahuje dvě textová pole, CheckBoxList a tlačítko ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)

Uživatelské rozhraní přihlašovací stránky může zůstat beze změny, ale musíme nahradit `Click` obslužnou rutinu události přihlašovacího tlačítka kódem, který ověřuje uživatele v úložišti uživatelů rozhraní .NET Framework. Aktualizujte obslužnou rutinu události tak, aby se její kód zobrazoval takto:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

Tento kód je výjimečně jednoduchý. Začneme voláním `Membership.ValidateUser` metody a předáním zadaného uživatelského jména a hesla. Pokud tato metoda vrátí hodnotu true, pak je uživatel přihlášen k webu prostřednictvím `FormsAuthentication` metody RedirectFromLoginPage třídy. (Jak je popsáno v části <a id="Tutorial2"></a> [*Přehled kurzu ověřování na základě formulářů*](../introduction/an-overview-of-forms-authentication-cs.md) `FormsAuthentication.RedirectFromLoginPage` vytvoří lístek ověřování formuláře a pak přesměruje uživatele na příslušnou stránku.) Pokud přihlašovací údaje nejsou platné, ale zobrazí se `InvalidCredentialsMessage` popisek, který uživatele informuje, že uživatelské jméno nebo heslo je nesprávné.

A je to!

Pokud chcete otestovat, jestli přihlašovací stránka funguje podle očekávání, zkuste se přihlásit pomocí jednoho z uživatelských účtů, které jste vytvořili v předchozím kurzu. Nebo, pokud jste ještě nevytvořili účet, pokračujte a vytvořte si ho ze `~/Membership/CreatingUserAccounts.aspx` stránky.

> [!NOTE]
> Když uživatel zadá své přihlašovací údaje a odešle formulář přihlašovací stránky, přihlašovací údaje, včetně jejího hesla, se přenáší přes Internet na webový server v *prostém textu*. To znamená, že uživatelské jméno a heslo může sledovat jakýkoli počítačový podvodník, který bude sledovat síťový provoz. Aby k tomu nedocházelo, je nezbytné šifrovat síťový provoz pomocí [protokolu SSL (Secure Socket Layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer). Tím se zajistí, že přihlašovací údaje (stejně jako kód HTML celé stránky) budou šifrovány od okamžiku, kdy prohlížeč opustí, dokud je webový server neobdrží.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Způsob, jakým rozhraní členství zpracovává neplatné pokusy o přihlášení

Když návštěvník dostane přihlašovací stránku a odešle své přihlašovací údaje, prohlížeč vytvoří požadavek HTTP na přihlašovací stránku. Pokud jsou přihlašovací údaje platné, odpověď protokolu HTTP zahrnuje ověřovací lístek do souboru cookie. Proto by počítačový podvodník pokoušející se o přemístění do vaší lokality mohl vytvořit program, který vyčerpá požadavky HTTP na přihlašovací stránku s platným uživatelským jménem a odhadem v hesle. Pokud je odhad hesla správný, přihlašovací stránka vrátí soubor cookie ověřovacího lístku, u kterého bude program vědět, že má stumbled na platný pár uživatelského jména a hesla. Díky útokům hrubou silou může být takový program Stumble na heslo uživatele, zejména v případě, že je heslo slabé.

Aby nedocházelo k takovým útokům hrubou silou, rozhraní pro členství zamkne uživatele, pokud v určitém časovém období dojde k určitému počtu neúspěšných pokusů o přihlášení. Přesné parametry lze konfigurovat prostřednictvím následujících dvou nastavení konfigurace zprostředkovatele členství:

- `maxInvalidPasswordAttempts` – Určuje, kolik neplatných pokusů o zadání hesla pro uživatele v časovém období, než je účet uzamčen. Výchozí hodnota je 5.
- `passwordAttemptWindow` – Určuje časové období v minutách, během kterého se zadaný počet neplatných pokusů o přihlášení pokusí o uzamčení účtu. Výchozí hodnota je 10.

Pokud uživatel byl uzamčen, nemůže se přihlásit, dokud správce neodemkne svůj účet. Když je uživatel uzamčený, bude `ValidateUser` Metoda *vždycky* vracet `false` , i když jsou dodány platné přihlašovací údaje. I když toto chování snižuje pravděpodobnost, že se hacker do vaší lokality přeruší prostřednictvím metod hrubou silou, může ukončit uzamykání platného uživatele, který jednoduše zapomene heslo, nebo neúmyslně má na začátku neplatný den zápisu.

Bohužel není k dispozici žádný integrovaný nástroj pro odemknutí uživatelského účtu. Chcete-li odemknout účet, můžete databázi změnit přímo, změnit `IsLockedOut` pole v `aspnet_Membership` tabulce pro příslušný uživatelský účet – nebo vytvořit webové rozhraní se seznamem uzamčených účtů s možnostmi jejich odemknutí. Podíváme se na vytváření rozhraní pro správu pro provádění běžných úloh souvisejících s uživatelským účtem a rolemi v budoucím kurzu.

> [!NOTE]
> Jednou z Nevýhodou `ValidateUser` metody je, že pokud jsou zadané přihlašovací údaje neplatné, neposkytuje žádné vysvětlení k tomu, proč. Přihlašovací údaje mohou být neplatné, protože v úložišti uživatele není žádné párování uživatelského jména a hesla, nebo protože uživatel nebyl dosud schválen, nebo protože byl uživatel uzamčen. V kroku 4 se dozvíte, jak zobrazit uživateli podrobnější zprávu, když se jejich pokus o přihlášení nezdaří.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>Krok 2: shromažďování přihlašovacích údajů prostřednictvím přihlašovacího webového ovládacího prvku

[Přihlašovací webový ovládací prvek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) vykresluje výchozí uživatelské rozhraní velmi podobné jako ten, který jsme vytvořili zpátky v <a id="SKM5"></a> [*přehledu kurzu ověřování pomocí formulářů*](../introduction/an-overview-of-forms-authentication-cs.md) . Použití přihlašovacího ovládacího prvku uloží nám práci s vytvořením rozhraní ke shromáždění přihlašovacích údajů návštěvníka. Kromě toho přihlašovací ovládací prvek automaticky přihlašuje uživatele (za předpokladu, že odeslaná pověření jsou platná), a tím šetříme, že je potřeba psát jakýkoliv kód.

Pojďme aktualizovat a `Login.aspx` nahradit ručně vytvořené rozhraní a kód ovládacím prvkem pro přihlášení. Začněte odebráním stávajících značek a kódu v `Login.aspx` . Můžete ho odstranit hned nebo jednoduše komentovat. Chcete-li komentovat deklarativní označení, uzavřete ho pomocí `<%--` `--%>` oddělovačů a. Tyto oddělovače můžete zadat ručně, nebo jak vidíte na obrázku 2, můžete vybrat text, který chcete komentovat, a pak na panelu nástrojů kliknout na ikonu odkomentovat vybrané řádky. Podobně můžete použít ikonu odkomentovat vybrané řádky a komentovat vybraný kód v třídě Code-na pozadí.

[![Odkomentovat existující deklarativní značky a zdrojový kód v Login. aspx](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**Obrázek 2**: Odkomentujte existující deklarativní označení a zdrojový kód v `Login.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png)

> [!NOTE]
> Při zobrazení deklarativních značek v aplikaci Visual Studio 2005 není k dispozici ikona komentovat vybrané řádky. Pokud nepoužíváte Visual Studio 2008, budete muset ručně přidat `<%--` `--%>` oddělovače a.

Dále přetáhněte ovládací prvek Login ze sady nástrojů na stránku a nastavte jeho `ID` vlastnost na `myLogin` . V tuto chvíli by vaše obrazovka měla vypadat podobně jako na obrázku 3. Všimněte si, že výchozí rozhraní ovládacího prvku pro přihlášení obsahuje ovládací prvky TextBox pro uživatelské jméno a heslo, zaškrtávací políčko Zapamatovat mě v dalším čase a tlačítko přihlásit. K dispozici jsou také `RequiredFieldValidator` ovládací prvky pro dvě textová pole.

[![Přidání ovládacího prvku pro přihlášení na stránku](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**Obrázek 3**: Přidání ovládacího prvku pro přihlášení na stránku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png))

A hotovi! Po kliknutí na tlačítko Přihlásit se k ovládacímu prvku přihlašování dojde k postbacku a přihlašovací ovládací prvek zavolá `Membership.ValidateUser` metodu, která předá zadané uživatelské jméno a heslo. Pokud jsou přihlašovací údaje neplatné, ovládací prvek přihlášení zobrazí zprávu s oznámením, že. Pokud jsou však přihlašovací údaje platné, ovládací prvek přihlášení vytvoří lístek ověřování formuláře a přesměruje uživatele na příslušnou stránku.

Řízení přihlášení používá ke zjištění vhodné stránky pro přesměrování uživatele na základě úspěšného přihlášení čtyři faktory:

- Určuje, zda je ovládací prvek přihlášení na přihlašovací stránce definovaný `loginUrl` nastavením v konfiguraci ověřování pomocí formulářů; výchozí hodnota tohoto nastavení je `Login.aspx`
- Přítomnost `ReturnUrl` parametru QueryString
- Hodnota [ `DestinationUrl` vlastnosti](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) ovládacího prvku přihlašovacího jména
- `defaultUrl`Hodnota zadaná v nastaveních konfigurace ověřování formulářů; výchozí hodnota tohoto nastavení je`Default.aspx`

Obrázek 4 znázorňuje, jak ovládací prvek Login používá tyto čtyři parametry k přijetí na příslušné stránce rozhodnutí.

[![Přidání ovládacího prvku pro přihlášení na stránku](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**Obrázek 4**: Přidání ovládacího prvku pro přihlášení na stránku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png))

Chvíli počkejte, než se otestuje přihlašovací řízení, a to tak, že navštívíte web prostřednictvím prohlížeče a přihlásíte se jako stávající uživatel v rámci systému členství.

Vykreslené rozhraní ovládacího prvku přihlášení je vysoce konfigurovatelné. Existuje mnoho vlastností, které ovlivňují jeho vzhled. a co víc, ovládací prvek pro přihlášení se dá převést na šablonu, aby se přes rozložení prvky uživatelského rozhraní poskytovala přesnou kontrolu. Zbývající část tohoto kroku zjistí, jak přizpůsobit vzhled a rozložení.

### <a name="customizing-the-login-controls-appearance"></a>Přizpůsobení vzhledu přihlašovacího ovládacího prvku

Nastavení výchozí vlastnosti ovládacího prvku pro přihlášení vykreslí uživatelské rozhraní s nadpisem (přihlásit se), textovým polem a popiskem pro zadání uživatelského jména a hesla, zaškrtávací políčko Zapamatovat mě Next Time a přihlašovací tlačítko. Vzhled těchto prvků je možné konfigurovat prostřednictvím mnoha vlastností ovládacího prvku přihlašovacího jména. Kromě toho je možné přidat další prvky uživatelského rozhraní, například odkaz na stránku pro vytvoření nového uživatelského účtu, a to nastavením vlastnosti nebo dvou.

Pojďme si za chvíli Gussy vzhled našeho přihlašovacího řízení. Vzhledem k tomu, že `Login.aspx` stránka již obsahuje text v horní části stránky, která říká přihlášení, je název ovládacího prvku přihlašovacího jména nadbytečný. Proto vymažte hodnotu [ `TitleText` vlastnosti](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) , aby se odstranil název ovládacího prvku přihlašovacího jména.

Uživatelské jméno: a heslo: popisky vlevo od dvou ovládacích prvků TextBox lze přizpůsobit pomocí [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) [ `PasswordLabelText` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)a v uvedeném pořadí. Pojďme změnit uživatelské jméno: popisek pro čtení uživatelského jména:. Styly popisku a TextBox lze konfigurovat prostřednictvím [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) [ `TextBoxStyle` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)a v uvedeném pořadí.

Vlastnost text v poli zapamatovat mě v dalším čase se dá nastavit prostřednictvím ovládacího prvku pro přihlášení [`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx) a její výchozí stav zaškrtnutí se dá nakonfigurovat přes [`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) (což je výchozí hodnota false). Pokračujte a nastavte `RememberMeSet` vlastnost na hodnotu true, aby se ve výchozím nastavení kontrolovalo zaškrtávací políčko Zapamatovat mě v dalším čase.

Ovládací prvek Login nabízí dvě vlastnosti pro úpravu rozložení ovládacích prvků uživatelského rozhraní. [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)Určuje, zda jsou popisky zobrazeny vlevo od jejich odpovídajících textových polí (výchozí nastavení), nebo nad nimi. [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)Určuje, zda jsou vstupy uživatelského jména a hesla umístěny svisle (jedna nad druhou) nebo horizontálně. Nechám tyto dvě vlastnosti nastavené na výchozí hodnoty, ale doporučujeme, abyste si vyzkoušeli nastavení těchto dvou vlastností na jiné než výchozí hodnoty, aby se zobrazil výsledný efekt.

> [!NOTE]
> V další části Konfigurace rozložení přihlašovacího ovládacího prvku se podíváme na použití šablon k definování přesného rozložení prvků uživatelského rozhraní ovládacího prvku rozložení.

Zabalte nastavení vlastností ovládacího prvku pro přihlášení nastavením [`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) [ `CreateUserUrl` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) a, které ještě nejsou zaregistrované? Vytvořte si účet! a `~/Membership/CreatingUserAccounts.aspx` v uvedeném pořadí. Tím se přidá hypertextový odkaz na rozhraní ovládacího prvku pro přihlášení ukazující na stránku, kterou jsme vytvořili v <a id="SKM6"></a> [předchozím kurzu](creating-user-accounts-cs.md). Ovládací prvky pro přihlášení [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) a [ `HelpPageUrl` vlastnosti](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) a [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) [ `PasswordRecoveryUrl` vlastnosti](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) fungují stejným způsobem, vykreslování odkazů na stránku s usnadněním a stránku pro obnovení hesla.

Po provedení změn těchto vlastností by deklarativní značení a vzhled ovládacího prvku přihlašovacího jména měly vypadat podobně jako na obrázku 5.

[![Hodnoty vlastností ovládacího prvku přihlašovacího jména určují jeho vzhled.](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**Obrázek 5**: hodnoty vlastností ovládacího prvku pro přihlašovací údaje určují jeho vzhled ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png)).

### <a name="configuring-the-login-controls-layout"></a>Konfigurace rozložení ovládacího prvku přihlašovacího jména

Výchozí uživatelské rozhraní pro přihlašovací webové ovládací prvky rozloží rozhraní v HTML `<table>` . Ale co když potřebujeme lepší kontrolu nad vykresleným výstupem? Možná chceme nahradit `<table>` řadu `<div>` značek. Nebo co když naše aplikace vyžaduje pro ověřování další přihlašovací údaje? Mnoho finančních webů vyžaduje, aby uživatelé zadali nejen uživatelské jméno a heslo, ale také osobní identifikační číslo (PIN) nebo jiné identifikační údaje. Bez ohledu na to, jak je možné, lze ovládací prvek přihlášení převést na šablonu, ze které můžeme explicitně definovat deklarativní označení rozhraní.

Abychom mohli aktualizovat přihlašovací ovládací prvek pro shromažďování dalších přihlašovacích údajů, musíme udělat dvě věci:

1. Aktualizujte rozhraní ovládacího prvku přihlášení tak, aby zahrnovalo webové ovládací prvky, aby se shromáždily další přihlašovací údaje.
2. Přepište logiku interního ověřování ovládacího prvku přihlášení tak, aby byl uživatel ověřen pouze v případě, že jsou jeho uživatelské jméno a heslo platné a že jsou také platné jejich další přihlašovací údaje.

Abychom mohli dosáhnout prvního úkolu, musíme převést ovládací prvek Login na šablonu a přidat potřebné webové ovládací prvky. Jako u druhé úlohy lze logiku ověřování ovládacího prvku přihlášení nahradit vytvořením obslužné rutiny události pro [ `Authenticate` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)ovládacího prvku.

Pojďme aktualizovat přihlašovací ovládací prvek tak, aby vyzvat uživatele k zadání uživatelského jména, hesla a e-mailové adresy a ověří uživatele jenom v případě, že zadaná e-mailová adresa odpovídá své e-mailové adrese v souboru. Nejdřív je potřeba převést rozhraní ovládacího prvku Login na šablonu. V inteligentní značce ovládacího prvku přihlašovací jméno vyberte možnost převést na šablonu.

[![Převod ovládacího prvku pro přihlášení na šablonu](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**Obrázek 6**: převod ovládacího prvku pro přihlášení na šablonu ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png))

> [!NOTE]
> Chcete-li vrátit ovládací prvek přihlášení ke své předběžné verzi šablony, klikněte na odkaz Obnovit z inteligentní značky ovládacího prvku.

Převedení přihlašovacího ovládacího prvku na šablonu přidá `LayoutTemplate` k deklarativní značce ovládacího prvku ovládací prvky HTML a webové ovládací prvky definující uživatelské rozhraní. Jak ukazuje obrázek 7, převod ovládacího prvku na šablonu odebere z okno Vlastnosti několik vlastností, například `TitleText` , `CreateUserUrl` a tak dále, protože tyto hodnoty vlastností jsou při použití šablony ignorovány.

[![V případě, že je ovládací prvek přihlášení převeden na šablonu, je k dispozici méně vlastností.](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**Obrázek 7**: k dispozici je méně vlastností, pokud je ovládací prvek přihlášení převeden na šablonu ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png)

Značky HTML v lze podle `LayoutTemplate` potřeby upravit. Stejně tak můžete do šablony přidat jakékoli nové webové ovládací prvky. Je ale důležité, aby hlavní webové ovládací prvky přihlašovacího ovládacího prvku zůstaly v šabloně a zůstaly přiřazené `ID` hodnoty. Konkrétně neodstraňujte ani neměňte pole `UserName` ani `Password` textová pole, `RememberMe` zaškrtávací políčko, `LoginButton` tlačítko, `FailureText` popisek ani `RequiredFieldValidator` ovládací prvky.

Abychom mohli shromažďovat e-mailovou adresu návštěvníka, musíme do šablony přidat textové pole. Přidejte následující deklarativní značku mezi řádek tabulky ( `<tr>` ), který obsahuje `Password` textové pole a řádek tabulky, který má zaškrtávací políčko Zapamatovat mě v dalším čase:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

Po přidání `Email` textového pole navštivte stránku v prohlížeči. Jak ukazuje obrázek 8, uživatelské rozhraní ovládacího prvku Login nyní obsahuje třetí textové pole.

[![Přihlašovací ovládací prvek teď obsahuje textové pole pro e-mailovou adresu uživatele.](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**Obrázek 8**: přihlašovací ovládací prvek teď obsahuje textové pole pro e-mailovou adresu uživatele ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png)

V tomto okamžiku přihlašovací ovládací prvek stále používá `Membership.ValidateUser` metodu k ověření zadaných přihlašovacích údajů. Odpovídající hodnota, která se zadává do `Email` textového pole, nemá žádný vliv na to, jestli se uživatel může přihlásit. V kroku 3 se podíváme na to, jak přepsat logiku ověřování ovládacího prvku přihlášení, aby se přihlašovací údaje považovaly jenom za platné, pokud jsou uživatelské jméno a heslo platné a zadaná e-mailová adresa se shoduje s e-mailovou adresou v souboru.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>Krok 3: změna logiky ověřování ovládacího prvku přihlášení

Když návštěvník poskytne své přihlašovací údaje a klikne na tlačítko Přihlásit se, vystavení se provede a přihlašovací řízení pokračuje prostřednictvím pracovního postupu ověřování. Pracovní postup se spustí vyvoláním [ `LoggingIn` události](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx). Jakékoli obslužné rutiny události přidružené k této události mohou zrušit operaci přihlášení nastavením `e.Cancel` vlastnosti na hodnotu `true` .

Pokud není operace přihlášení zrušena, pracovní postup se doplní tím, že [ `Authenticate` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)vyvyvolává. Pokud pro událost dojde k obslužné rutině události `Authenticate` , zodpovídá za určení, zda jsou zadaná pověření platná nebo nikoli. Pokud není zadána žádná obslužná rutina události, ovládací prvek Login používá `Membership.ValidateUser` metodu k určení platnosti přihlašovacích údajů.

Pokud jsou zadané přihlašovací údaje platné, vytvoří se lístek ověřování formulářů, [ `LoggedIn` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) se vyvolá a uživatel se přesměruje na příslušnou stránku. Pokud se však přihlašovací údaje považují za neplatné, vyvolá se [ `LoginError` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) a zobrazí se zpráva informující o tom, že jejich přihlašovací údaje byly neplatné. Ve výchozím nastavení při selhání ovládací prvek pro přihlášení jednoduše nastaví `FailureText` vlastnost text ovládacího prvku popisek na zprávu o selhání (váš pokus o přihlášení nebyl úspěšný. Zkuste to prosím znovu. Pokud je však [ `FailureAction` vlastnost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) ovládacího prvku přihlašovacího ovládacího prvku nastavena na `RedirectToLoginPage` , pak řízení přihlášení vydá `Response.Redirect` přihlašovací stránku, která připojuje parametr QueryString `loginfailure=1` (což způsobí, že ovládacímu prvku pro přihlášení dojde k zobrazení zprávy o selhání).

Obrázek 9 nabízí vývojový diagram pracovního postupu ověřování.

[![Pracovní postup ověřování ovládacího prvku přihlášení](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**Obrázek 9**: pracovní postup ověření přihlašovacího ovládacího prvku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png))

> [!NOTE]
> Pokud vás zajímá, kdy byste použili `FailureAction` `RedirectToLogin` možnost stránky, zvažte následující scénář. Nyní naše `Site.master` Hlavní stránka má v současné době text, Hello, v levém sloupci, když je navštíven anonymní uživatel, ale Představme si, že jsme chtěli tento text nahradit ovládacím prvkem pro přihlášení. To umožňuje anonymnímu uživateli přihlásit se ze všech stránek na webu, aniž by musel navštěvovat přihlašovací stránku přímo. Pokud se ale uživatel nemůže přihlásit prostřednictvím ovládacího prvku pro přihlášení, který vygenerovala stránka předlohy, může to mít smysl ho přesměrovat na přihlašovací stránku ( `Login.aspx` ), protože tato stránka pravděpodobně obsahuje další pokyny, odkazy a další nápovědě – například odkazy k vytvoření nového účtu nebo načtení ztraceného hesla – které nebyly přidány do hlavní stránky.

### <a name="creating-theauthenticateevent-handler"></a>Vytvoření `Authenticate` obslužné rutiny události

Aby bylo možné připojit vlastní logiku ověřování, musíme vytvořit obslužnou rutinu události pro událost ovládacího prvku Login `Authenticate` . Vytvořením obslužné rutiny události pro `Authenticate` událost dojde k vygenerování následující definice obslužné rutiny události:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

Jak vidíte, `Authenticate` obslužná rutina události je předána objektu typu [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) jako jeho druhý vstupní parametr. `AuthenticateEventArgs`Třída obsahuje logickou vlastnost s názvem `Authenticated` , která se používá k určení, zda jsou zadaná pověření platná. Náš úkol, pak je zde napsat kód, který určuje, zda jsou dodané přihlašovací údaje platné, nebo nikoli a nastavte `e.Authenticate` vlastnost odpovídajícím způsobem.

### <a name="determining-and-validating-the-supplied-credentials"></a>Určení a ověření zadaných přihlašovacích údajů

Pomocí vlastností ovládacího prvku [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) a [ `Password` vlastnosti](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) přihlášení Určete přihlašovací údaje uživatele a hesla zadané uživatelem. Aby bylo možné určit hodnoty zadané do jakýchkoli dalších webových ovládacích prvků (například `Email` textové pole, které jsme přidali v předchozím kroku), použijte *`LoginControlID`* `.FindControl` (" *`controlID`* ") k získání programového odkazu na webový ovládací prvek v šabloně, jejíž `ID` vlastnost je rovna *`controlID`* . Chcete-li například získat odkaz na `Email` textové pole, použijte následující kód:

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

Aby bylo možné ověřit přihlašovací údaje uživatele, musíme udělat dvě věci:

1. Ujistěte se, že zadané uživatelské jméno a heslo jsou platné.
2. Zajistěte, aby zadaná e-mailová adresa odpovídala e-mailové adrese v souboru, aby se uživatel pokusil přihlásit.

Pro provedení první kontroly můžeme jednoduše použít `Membership.ValidateUser` metodu, jako bychom viděli v kroku 1. Pro druhou kontrolu musíme určit e-mailovou adresu uživatele, abychom ji mohli porovnat s e-mailovou adresou, kterou zadal do ovládacího prvku TextBox. Chcete-li získat informace o konkrétním uživateli, použijte `Membership` [ `GetUser` metodu](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)třídy.

`GetUser`Metoda má počet přetížení. Pokud se tato funkce použije bez předání jakýchkoli parametrů, vrátí informace o aktuálně přihlášeném uživateli. Chcete-li získat informace o konkrétním uživateli, zavolejte `GetUser` na své uživatelské jméno. V obou případech `GetUser` vrátí [ `MembershipUser` objekt](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), který má vlastnosti jako `UserName` , `Email` , `IsApproved` , `IsOnline` a tak dále.

Následující kód implementuje tyto dvě kontroly. Pokud `e.Authenticate` je nastaveno na `true` , v opačném případě je přiřazeno `false` .

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

V případě tohoto kódu se pokuste přihlásit jako platný uživatel a zadat správné uživatelské jméno, heslo a e-mailovou adresu. Zkuste to znovu, ale tentokrát záměrně použít nesprávnou e-mailovou adresu (viz obrázek 10). Nakonec se pomocí neexistujícího uživatelského jména pokuste použít jiný čas. V prvním případě byste měli být úspěšně přihlášení k lokalitě, ale v posledních dvou případech byste měli vidět zprávu neplatných přihlašovacích údajů ovládacího prvku přihlašovací jméno.

[![Tito se nemůže přihlásit, když se zadává nesprávná e-mailová adresa.](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**Obrázek 10**: Tito se nemůže přihlásit při zadání nesprávné e-mailové adresy ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)

> [!NOTE]
> Jak je popsáno v části jak rozhraní členství zpracovává neúspěšné pokusy o přihlášení v kroku 1, pokud `Membership.ValidateUser` je metoda volána a prošla neplatnými přihlašovacími údaji, sleduje Neplatný pokus o přihlášení a zamkne uživatele, pokud překročí určitou prahovou hodnotu neplatných pokusů v zadaném časovém intervalu. Vzhledem k tomu, že naše vlastní logika ověřování volá `ValidateUser` metodu, nesprávným heslem pro platné uživatelské jméno se zvýší neplatný čítač pokusů o přihlášení, ale tento čítač se nezvýší v případě, že uživatelské jméno a heslo jsou platné, ale e-mailová adresa není správná. Důvodem je to, že toto chování je vhodné, protože je pravděpodobné, že hacker bude znát uživatelské jméno a heslo, ale musí použít techniky hrubou silou k určení e-mailové adresy uživatele.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>Krok 4: vylepšení zprávy s neplatnými přihlašovacími údaji ovládacího prvku pro přihlášení

Když se uživatel pokusí přihlásit pomocí neplatných přihlašovacích údajů, zobrazí ovládací prvek přihlášení zprávu s vysvětlením, že se pokus o přihlášení nezdařil. Konkrétně ovládací prvek zobrazuje zprávu určenou [ `FailureText` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx), která má výchozí hodnotu pokusu o přihlášení nebylo úspěšné. Zkuste to prosím znovu.

Odvolat, že existuje mnoho důvodů, proč přihlašovací údaje uživatele mohou být neplatné:

- Uživatelské jméno možná neexistuje.
- Uživatelské jméno existuje, ale heslo je neplatné.
- Uživatelské jméno a heslo jsou platné, ale uživatel se ještě neschválil.
- Uživatelské jméno a heslo jsou platné, ale uživatel je uzamčený (pravděpodobně proto, že překročil počet neplatných pokusů o přihlášení v rámci zadaného časového rámce).

A při použití vlastní logiky ověřování mohou nastat jiné důvody. Například s kódem, který jsme napsali v kroku 3, může být uživatelské jméno a heslo platné, ale e-mailová adresa může být nesprávná.

Bez ohledu na to, proč jsou přihlašovací údaje neplatné, zobrazí ovládací prvek přihlášení stejnou chybovou zprávu. Tato nedostatečná zpětná vazba může být matoucí pro uživatele, jehož účet ještě nebyl schválen nebo byl uzamčen. I když máme trochu práci, můžeme ovládacímu prvku přihlášení zobrazit vhodnější zprávu.

Pokaždé, když se uživatel pokusí přihlásit s neplatnými přihlašovacími údaji, vyvolá řízení přihlášení jeho `LoginError` událost. Pokračujte a vytvořte obslužnou rutinu události pro tuto událost a přidejte následující kód:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

Výše uvedený kód začíná nastavením vlastnosti přihlašovacího ovládacího prvku `FailureText` na výchozí hodnotu (váš pokus o přihlášení nebyl úspěšný. Zkuste to prosím znovu. Pak zkontroluje, jestli je zadané uživatelské jméno namapováno na existující uživatelský účet. V takovém případě se poraďte se výsledným `MembershipUser` objektem `IsLockedOut` a `IsApproved` vlastnostmi a určí, zda byl účet uzamčen nebo dosud nebyl schválen. V obou případech `FailureText` je vlastnost aktualizována na odpovídající hodnotu.

K otestování tohoto kódu se záměrně pokus o přihlášení jako stávající uživatel, ale použijte nesprávné heslo. Udělejte to pětkrát za řádek během 10 minut a účet se zablokuje. Jak ukazuje obrázek 11, následné pokusy o přihlášení vždy selžou (i se správným heslem), ale teď se zobrazí podrobnější popis, který váš účet byl uzamčen z důvodu příliš velkého počtu neplatných pokusů o přihlášení. Kontaktujte prosím správce, aby se Váš účet odemkl.

[![Tito provedl příliš mnoho neplatných pokusů o přihlášení a byl uzamčen.](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**Obrázek 11**: tito provedl příliš mnoho neplatných pokusů o přihlášení a byl uzamčen ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png)

## <a name="summary"></a>Souhrn

Před tímto kurzem přihlašovací stránka ověřila zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelských jmen a hesel. V tomto kurzu jsme aktualizovali stránku, aby ověřila přihlašovací údaje proti členskému rozhraní. V kroku 1 jsme si vyhledali použití `Membership.ValidateUser` metody programově. V kroku 2 jsme nahradili naše ručně vytvořené uživatelské rozhraní a kód pomocí přihlašovacího ovládacího prvku.

Přihlašovací ovládací prvek vykreslí standardní přihlašovací uživatelské rozhraní a automaticky ověří přihlašovací údaje uživatele v rámci architektury členství. V případě platných přihlašovacích údajů navíc přihlašovací ovládací prvek podepisuje uživatele prostřednictvím ověřování pomocí formulářů. V krátkém případě je k dispozici plně funkční uživatelské prostředí přihlášení pouhým přetažením ovládacího prvku pro přihlášení na stránku bez nutnosti dalšího deklarativního kódu. A co více, ovládací prvek přihlašování je vysoce přizpůsobitelný, což umožňuje jemný stupeň kontroly nad vykresleným uživatelským rozhraním a logikou ověřování.

V tomto okamžiku můžou Návštěvníci na našem webu vytvořit nový uživatelský účet a přihlásit se k webu, ale ještě jsme si vyhledali omezení přístupu k stránkám na základě ověřeného uživatele. V současné době může libovolný uživatel, ověřený nebo anonymní zobrazit jakoukoli stránku na našem webu. Společně s řízením přístupu na stránky našeho webu na základě uživatele můžeme mít určité stránky, jejichž funkce závisí na uživateli. V dalším kurzu se podíváme na to, jak omezit přístup a funkce na stránce na základě přihlášeného uživatele.

Šťastné programování!

### <a name="further-reading"></a>Další materiály

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Zobrazení vlastních zpráv pro zamčené a neschválené uživatele](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [Zkoumání členství, rolí a profilů v ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Postupy: vytvoření přihlašovací stránky ASP.NET](https://msdn.microsoft.com/library/ms178331.aspx)
- [Technická dokumentace k řízení přihlašování](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Používání ovládacích prvků přihlášení](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott se dá kontaktovat na [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) blogu nebo přes jeho blog na adrese [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Michael Olivero. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, umístěte mi čáru na [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [Předchozí](creating-user-accounts-cs.md) 
>  [Další](user-based-authorization-cs.md)
