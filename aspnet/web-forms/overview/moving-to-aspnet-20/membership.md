---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Členství | Dokumenty společnosti Microsoft
author: rick-anderson
description: členství ASP.NET vychází z úspěchu modelu ověřování pomocí formulářů od ASP.NET 1.x. ASP.NET ověřování pomocí formulářů poskytuje pohodlný způsob, jak incorp ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543766"
---
# <a name="membership"></a>Členství

podle [společnosti Microsoft](https://github.com/microsoft)

> členství ASP.NET vychází z úspěchu modelu ověřování pomocí formulářů od ASP.NET 1.x. ověřování ASP.NET formulářů poskytuje pohodlný způsob, jak začlenit přihlašovací formulář do ASP.NET aplikace a ověřit uživatele proti databázi nebo jinému úložišti dat.

členství ASP.NET vychází z úspěchu modelu ověřování pomocí formulářů od ASP.NET 1.x. ověřování ASP.NET formulářů poskytuje pohodlný způsob, jak začlenit přihlašovací formulář do ASP.NET aplikace a ověřit uživatele proti databázi nebo jinému úložišti dat. Členové třídy FormsAuthentication umožňují zpracovávat soubory cookie pro ověření, kontrolovat platné přihlášení, odhlásit uživatele atd. Implementace ověřování pomocí formulářů v aplikaci ASP.NET 1.x však může vyžadovat slušné množství kódu.

Členství v ASP.NET 2.0 je zásadní pokrok v používání ověřování pomocí formulářů sám. (Členství je nejrobustnější ve spojení s ověřováním pomocí formulářů, ale použití ověřování pomocí formulářů není podmínkou.) Jak brzy uvidíte, můžete použít ASP.NET členství a ovládací prvky přihlášení v ASP.NET 2.0 k implementaci výkonného systému členství bez psaní velkého kódu vůbec.

## <a name="implementing-membership-in-aspnet-20"></a>Implementace členství v ASP.NET 2.0

Členství je implementováno následujícími čtyřmi kroky. Mějte na paměti, že existuje mnoho dílčích kroků, které jsou zapojeny, stejně jako volitelné konfigurace, které lze také implementovat. Tyto kroky jsou určeny pro ilustraci velký obrázek konfigurace členství.

1. Vytvořte databázi členství (pokud sql server se používá jako úložiště členství.)
2. Zadejte možnosti členství v konfiguračních souborech aplikací. (Členství je ve výchozím nastavení povoleno.)
3. Určete typ úložiště členství, které chcete použít. Dostupné možnosti: 

    - Microsoft SQL Server (verze 7.0 nebo novější)
    - Úložiště služby Active Directory
    - Vlastní poskytovatel členství
4. Nakonfigurujte aplikaci pro ověřování ASP.NET formulářů. Členství je opět navrženo tak, aby využívalo ověřování pomocí formulářů, ale použití ověřování pomocí formulářů není podmínkou.
5. Definujte uživatelské účty pro členství a v případě potřeby nakonfigurujte role.

## <a name="creating-the-membership-database"></a>Vytvoření databáze členství

Pokud používáte SQL Server 7.0 nebo novější jako úložiště členství,\_můžete ke konfiguraci databáze použít nástroj aspnet regsql (který je nejsnadněji dostupný z příkazového řádku sady Visual Studio .NET 2005). Nástroj aspnet\_regsql lze použít jako nástroj příkazového řádku nebo pomocí průvodce GUI. Metoda průvodce je nejjednodušší způsob konfigurace databáze. Chcete-li získat přístup k průvodci, jednoduše spusťte následující příkaz:

`aspnet_regsql W`

Po spuštění tohoto příkazu se zobrazí Průvodce instalací ASP.NET serveru SQL Server, jak je znázorněno níže.

![](membership/_static/image1.jpg)

**Obrázek 1**

Průvodce instalací serveru ASP.NET SQL Server vytvoří web v instanci zadané v průvodci. ASP.NET však použije připojovací řetězec v souboru machine.config pro připojení k databázi. Ve výchozím nastavení bude tento připojovací řetězec přeukazovat na instanci serveru SQL Server 2005, takže pokud používáte instanci serveru SQL Server 2000 nebo 7.0 serveru SQL Server 7.0, budete muset připojovací řetězec v souboru machine.config upravit. Tento připojovací řetězec lze nalézt zde:

[!code-xml[Main](membership/samples/sample1.xml)]

Bohužel, pokud nechcete změnit připojovací řetězec, ASP.NET vám neposkytne popisnou chybu. Bude si jen nadále stěžovat, že jste databázi nevytvořili. Ve výše uvedeném případě jsem upravil připojovací řetězec tak, aby ukazoval na místní instanci serveru SQL Server 2000.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Určení konfigurace a přidání uživatelů a rolí

Dalším krokem při konfiguraci členství je přidání potřebných informací do souboru web.config aplikace. V ASP.NET 1.x, úprava souboru web.config byla někdy obtížná kvůli použití lowerCamelCase a nedostatku Intellisense. Visual Studio .NET 2005 usnadňuje úlohu s Intellisense pro konfigurační soubory, ale ASP.NET 2.0 jde ještě o krok dále tím, že poskytuje webové rozhraní pro úpravy konfiguračních souborů.

Webové rozhraní můžete spustit klepnutím na tlačítko ASP.NET konfigurace na panelu nástrojů Průzkumníka řešení, jak je znázorněno níže. Webové rozhraní můžete také spustit pomocí automaticky otevíraných líacích, která se zobrazí při vložení ovládacích prvků Přihlášení.

![](membership/_static/image2.jpg)

**Obrázek 2**

Tím se spustí nástroj pro správu webových stránek ASP.NET uvedený níže. Správa webových stránek ASP.NET je rozhraní se čtyřmi kartami, které usnadňuje správu nastavení aplikací. K dispozici jsou následující karty:

- **Domů**
- **Bezpečnost** Konfigurace uživatelů, rolí a přístupu.
- **Přihláška** Konfigurace nastavení aplikace.
- **Poskytovatel** Konfigurace a testování poskytovatele členství v aplikacích.

Nástroj pro správu webu umožňuje snadno vytvářet nové uživatele, vytvářet nové role a spravovat uživatele a role. Tato možnost není k dispozici v rozhraní systému Windows. Rozhraní systému Windows umožňuje snadno definovat nastavení autorizace a přidávat, odstraňovat a spravovat zprostředkovatele, což nejsou funkce, které nejsou v nástroji pro správu webu.

Chcete-li spustit rozhraní systému Windows, otevřete modul snap-in Internetová informační služba, klikněte pravým tlačítkem myši na aplikaci a zvolte Vlastnosti. Klikněte na kartu ASP.NET a potom klikněte na tlačítko Upravit konfiguraci. (Aby bylo možné povolit tlačítko Upravit konfiguraci, musí být aplikace spuštěna pod ASP.NET 2.0. Verzi ASP.NET můžete nakonfigurovat také v dialogovém okně ASP.NET.) Dialogové okno nastavení konfigurace ASP.NET zobrazí, jak je znázorněno níže.

![](membership/_static/image3.jpg)

**Obrázek 3**

Na kartě Obecné jsou uvedeny připojovací řetězce a nastavení aplikace. Všechna nastavení kurzívou jsou definována v nadřazeném konfiguračním souboru (buď v souboru machine.config nebo web.config na vyšší úrovni) a nastavení, která nejsou kurzívou, pocházejí z konfiguračního souboru aplikací. Pokud je nastavení přidáno, odebráno nebo upraveno na úrovni aplikace, ASP.NET přidá, odebere nebo upraví nastavení na úrovni aplikace web.config namísto odebrání nastavení z konfiguračního souboru, ze kterého je zděděno.

Karta Ověřování je uvedena níže. Zde nakonfigurujete nastavení členství. Zde lze nakonfigurovat nastavení ověřování pomocí formulářů, poskytovatele členství a zprostředkovatele rolí.

![](membership/_static/image4.jpg)

**Obrázek 4**

## <a name="implementing-membership-in-your-application"></a>Implementace členství ve vaší aplikaci

Nejjednodušší způsob, jak implementovat členství ASP.NET 2.0 ve vaší aplikaci, je použít zadaný ovládací prvky přihlášení. Tato metoda umožňuje implementovat základy členství ASP.NET 2.0 bez psaní kódu vůbec.

V ASP.NET 2.0 jsou k dispozici následující ovládací prvky přihlášení:

## <a name="login-control"></a>Řízení přihlášení

Ovládací prvek Přihlášení poskytuje rozhraní pro někoho, kdo se přihlásit do vašeho členského systému. Poskytuje vám textové pole s uživatelským jménem a heslem a přihlašovací tlačítko. Mnoho dalších společných funkcí, jako je odkaz na registraci pro lidi, kteří tak dosud neučinili, zaškrtávací políčko, které umožňuje uživateli automaticky přihlásit na následné návštěvy, odkaz na připomenutí hesla, atd. Všechny funkce ovládacího prvku Login jsou přizpůsobitelné prostřednictvím vlastností ovládacího prvku.

V ASP.NET 1.x museli vývojáři napsat slušné množství kódu, aby provedli vyhledávání při použití ověřování pomocí formulářů. S členstvím ASP.NET 2.0 můžete ověřit uživatele bez psaní kódu vůbec. ASP.NET bude automaticky dělat vyhledávání uživatele za vás. (Pokud používáte ovládací prvek Přihlásit bez použití ASP.NET členství, můžete použít **Metodu OnAuthenticate** k ověření uživatele.)

## <a name="loginview-control"></a>Ovládací prvek LoginView

Ovládací prvek LoginView je ovládací prvek s šablonami, který ve výchozím nastavení poskytuje dvě šablony. AnonymousTemplate a LoggedInTemplate. Zobrazená šablona je určena tím, zda je uživatel přihlášen do vašeho členského systému. Tento ovládací prvek se obvykle používá k zobrazení ovládacího prvku Login, když se uživatel ještě nepřihlásil, a ovládací prvek LoginStatus a/nebo jiné ovládací prvky přihlášení, když se uživatel přihlásil. Pokud používáte správu rolí ve vaší ASP.NET aplikaci, ovládací prvek LoginView může zobrazit konkrétní šablonu založenou na roli uživatelů. (Další informace o řízení rolí ASP.NET budou zahrnuty později.)

## <a name="passwordrecovery-control"></a>Ovládací prvek Obnovení hesla

Ovládací prvek PasswordRecovery umožňuje uživatelům přijímat e-maily s aktuálním heslem nebo resetovat jeho heslo. Čistý text a šifrovaná hesla lze obnovit a odeslat e-mailem uživatelům. Pokud je heslo zapisováno, nelze jej obnovit. Místo toho bude uživatel muset provést resetování hesla.

## <a name="loginstatus-control"></a>Ovládací prvek LoginStatus

Ovládací prvek LoginStatus se používá k zobrazení indikátoru přihlášení uživatelům, kteří nejsou přihlášeni, a indikátoru odhlášení pro uživatele, kteří jsou aktuálně přihlášeni. Vlastnost Request.IsAuthenticated se používá k určení, který indikátor se má zobrazit. Indikátor zobrazený ovládacím prvkem LoginStatus může být text (implementován pomocí vlastností **LoginText** a **LogoutText)** nebo obrázky (implementované pomocí vlastností **LoginImageUrl** a **LogoutImageUrl.)**

Když se uživatel odhlásí prostřednictvím ovládacího prvku LoginStatus, je přesměrován na adresu URL určenou vlastností **LogoutPageUrl.** Pokud tato vlastnost není nastavena, aktuální stránka se aktualizuje. Vzhledem k tomu, že web je pravděpodobně chráněn ověřováním pomocí formulářů, aktualizace aktuální stránky přesměruje uživatele na přihlašovací stránku webu.

## <a name="loginname-control"></a>Ovládací prvek LoginName

Ovládací prvek LoginName zobrazuje uživatelské jméno uživatele aktuálně přihlášeného k webu.

## <a name="createuserwizard-control"></a>Ovládací prvek CreateUserWizard

Ovládací prvek CreateUserWizard poskytuje uživatelům pohodlný způsob registrace pro váš systém členství. Můžete přidat kroky (implementované jako kolekce WizardSteps) prostřednictvím rozhraní uvedeného níže.

![](membership/_static/image5.jpg)

**Obrázek 5**

CreateUserWizard je šablonovaný ovládací prvek, který je odvozen od třídy Wizard a poskytuje následující šablony:

- **Šablona záhlaví** Tato šablona řídí vzhled záhlaví průvodce.
- **Šablona postranního panelu** Tato šablona řídí vzhled postranního panelu průvodce.
- **Šablona StartNavigation** Tato šablona řídí vzhled navigace průvodce v kroku zahájení.
- **Šablona stepnavigace** Tato šablona řídí vzhled navigační oblasti, když není v kroku zahájení nebo dokončení.
- **Dokončitnavigační šablonu** Tato šablona řídí vzhled navigační oblasti v kroku dokončení.

Navíc pro každý krok, který přidáte do průvodce, ASP.NET vytvoří vlastní šablonu, která obsahuje šablonu ContentTemplate a CustomNavigationTemplate pro tento krok. Podrobné informace o přizpůsobení Průvodce vytvořením uživatele naleznete v dokumentaci VS.NET 2005:

## <a name="changepassword-control"></a>Ovládací prvek ChangePassword

Ovládací prvek ChangePassword umožňuje uživatelům změnit své heslo. Pokud je vlastnost DisplayUserName true (ve výchozím nastavení je nepravdivá), může uživatel změnit své heslo, pokud není přihlášen. Pokud *je* uživatel již přihlášen a vlastnost DisplayUserName je true, uživatel bude moci změnit heslo jiného uživatele, který není přihlášen za předpokladu, že zná ID uživatele tohoto uživatele.

Mějte na paměti, že pokud chcete, aby uživatelé mohli měnit hesla bez nutnosti přihlášení, budete muset zajistit, že stránka, na které je zobrazen ovládací prvek ChangePassword umožňuje anonymní přístup. Je zřejmé, že uživatelé budou muset zadat své staré heslo, aby změnili své heslo.

## <a name="role-management"></a>Správa rolí

Správa rolí umožňuje přiřadit uživatele k určité roli a potom omezit přístup k určitým souborům nebo složkám na základě této role. Správa rolí také poskytuje rozhraní API, takže můžete programově určit něčí roli nebo určit všechny uživatele v určité roli a odpovídajícím způsobem reagovat.

Správa rolí není požadavkem v ASP.NET členství, ani členství není požadavek pro použití správy rolí. Nicméně, dva doplněk navzájem pěkně a je pravděpodobné, že vývojáři budou používat ve spojení s sebou.

Chcete-li povolit správu rolí v aplikaci, proveďte v souboru web.config následující změny:

[!code-xml[Main](membership/samples/sample2.xml)]

Pokud je atribut **cacheRolesInCookie** nastaven na hodnotu true, ASP.NET uloží členství v roli uživatele do mezipaměti v souboru cookie v klientovi. To umožňuje vyhledávání rolí dojít bez volání do RoleProvider. Při použití tohoto atributu se vývojářům doporučujeme zajistit, aby atribut **cookieProtection** byl nastaven na všechny. (Toto je výchozí nastavení.) Tím je zajištěno, že data souborů cookie jsou šifrována, a pomáhá zajistit, že obsah souborů cookie nebyl změněn. Role lze přidat pomocí Nástroje pro správu webu. Umožňuje snadno definovat role, konfigurovat přístup k částem webu na základě těchto rolí a přiřazovat uživatele k rolím.

![](membership/_static/image6.jpg)

**Obrázek 6**

Jak je uvedeno výše, nové role lze přidat jednoduše zadáním názvu role a kliknutím na přidat roli. Existující role lze spravovat nebo odstranit kliknutím na příslušný odkaz v seznamu existujících rolí.

Při správě role můžete přidávat nebo odebírat uživatele, jak je znázorněno níže.

![](membership/_static/image7.jpg)

**Obrázek 7**

Zaškrtnutím políčka Uživatel je v roli, můžete snadno přidat uživatele do určité role. ASP.NET automaticky aktualizuje databázi členství příslušnými položkami. Budete také chtít nakonfigurovat pravidla přístupu pro vaši aplikaci. ASP.NET vývojáři 1.x jsou obeznámeni&gt; s tím prostřednictvím autorizačního &lt;prvku v souboru web.config a tato možnost je stále k dispozici v ASP.NET 2.0. Jeho snadnější správa pravidel přístupu pomocí Nástroje pro správu webu, jak je znázorněno níže.

![](membership/_static/image8.jpg)

**Obrázek 8**

V tomto případě je zvýrazněna složka Správa (je obtížné ji zobrazit, protože nástroj ji zvýrazní světle šedě) a roli Administrators byl udělen přístup. Všichni ostatní uživatelé jsou odmítnuti. Kliknutím na ikonu hlavy můžete vybrat pravidlo a pak pomocí tlačítek Přesunout nahoru a Přesunout dolů uspořádat pravidla. Stejně jako &lt;&gt; u ASP.NET autorizační prvek jsou pravidla zpracována v pořadí, ve kterém se zobrazují. Jinými slovy, pokud pořadí pravidel v shot výše byly obráceny, nikdo by měl přístup ke složce správa, protože první pravidlo, které by ASP.NET setkat by pravidlo, které odepře všichni do složky.

ASP.NET 2.0 přidá soubor web.config do složky, pro kterou zadáváte pravidlo přístupu. Pravidla přístupu lze upravovat pomocí konfiguračního souboru nebo pomocí nástroje pro správu webu. Jinými slovy, Nástroj pro správu webu je jednoduše rozhraní, jehož prostřednictvím lze konfigurační soubor upravovat v uživatelsky přívětivém prostředí.

## <a name="using-roles-in-code"></a>Použití rolí v kódu

Rozhraní API pro správu rolí se od verze 1.x nezměnilo. **IsInRole** Metoda se používá k určení, pokud je uživatel v určité roli.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET také vytvoří instance RolePrincipal jako člen aktuálního kontextu. Objekt RolePrincipal lze získat všechny role, do kterých uživatel patří následujícím způsobem:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>Použití skupin rolí s ovládacím prvkem LoginView

Nyní, když máte pochopení správy rolí a členství, umožňuje stručně diskutovat o tom, jak LoginView ovládací prvek využívá této funkce v ASP.NET 2.0. Jak již bylo popsáno, Ovládací prvek LoginView je šablonovaný ovládací prvek, který ve výchozím nastavení obsahuje dvě šablony; AnonymousTemplate a LoggedInTemplate. V dialogovém okně Úlohy loginview je odkaz (viz níže), který umožňuje upravovat rolegroups.

![](membership/_static/image9.jpg)

**Obrázek 9**

Každý objekt RoleGroup obsahuje pole řetězců, které definuje, které role, které RoleGroup se vztahuje. Pokud chcete do ovládacího prvku LoginView přidat novou skupinu rolí, klikněte na odkaz Upravit skupiny rolí. Na obrázku výše vidíte, že jsem přidal novou skupinu rolí pro správce. Výběrem této skupiny rolí (RoleGroup[0]) v rozevíracím seznamu Zobrazení lze nakonfigurovat šablonu, která bude zobrazena pouze členům role Administrators. Na obrázku níže jsem přidal novou skupinu rolí, která se vztahuje na členy role Prodej a Distribuční role. Tím přidáte druhou skupinu rolí do rozevíracího seznamu Zobrazení v dialogovém okně Úlohy zobrazení přihlášení a vše, co je přidáno do této šablony, bude viditelné libovolným uživatelem v roli Prodej nebo Distribuce.

![](membership/_static/image10.jpg)

**Obrázek 10**

## <a name="overriding-the-existing-membership-provider"></a>Přepsání stávajícího poskytovatele členství

Existuje několik způsobů, jak můžete rozšířit funkce členství ASP.NET. Za prvé, můžete samozřejmě změnit existující funkce Třídy SqlMembershipProvider děděním z ní a přepsáním jeho metod. Například pokud chcete implementovat vlastní funkce při vytváření uživatelů, můžete vytvořit vlastní třídu, která dědí z SqlMembershipProvider takto:

[!code-csharp[Main](membership/samples/sample5.cs)]

Pokud na druhou stranu chcete vytvořit vlastního poskytovatele (například pro uložení informací o členství v databázi aplikace Access), můžete vytvořit vlastního poskytovatele.

## <a name="creating-your-own-membership-provider"></a>Vytvoření vlastního poskytovatele členství

Chcete-li vytvořit vlastní poskytovatele členství, budete muset nejprve vytvořit třídu, která dědí z Třídy MembershipProvider. Pokud používáte VB.NET, Visual Studio 2005 přidá zástupné procedury pro všechny metody, které je třeba přepsat. Pokud používáte C#, jeho na vás přidat zástupné procedury.

Budete muset přepsat následující:

- ApplicationName, vlastnost
- ChangePassword
- ChangePasswordQuestionAndAnswer
- CreateUser
- Odstranituser
- EnablePasswordReset, vlastnost
- Vlastnost EnablePasswordRetrieval
- FindUsersByEmail funkce
- FindUsersByName
- GetAllUsers,
- Funkce GetNumberOfUsersOnline
- GetPassword
- GetUser
- Funkce GetUserNameByEmail
- MaxInvalidPasswordAttempts, vlastnost
- Vlastnost MinRequiredNonAlphanumericCharacters
- Vlastnost MinRequiredPasswordLength
- PasswordAttemptWindow, vlastnost
- PasswordFormat, vlastnost
- PasswordStrengthRegularExpression, vlastnost
- Vlastnost RequiresQuestionAndAnswer
- Vlastnost RequiresUniqueEmail
- Funkce ResetPassword
- Odemknout uživatelskou funkci
- UpdateUser
- OvěřitUživatel

To je docela seznam implementovat jako vývojář C#. Může být jednodušší vytvořit třídu v VB.NET bez jakékoli implementace a potom použít .NET Reflector nebo podobný nástroj pro převod kódu na C#.

Připojovací řetězec a další vlastnosti by měly být nastaveny na jejich výchozí hodnoty v metodě Initialize. (Initialize Metoda je aktivována při načtení zprostředkovatele za běhu.) Druhý parametr metody Initialize je typu System.Collections.Specialized.NameValueCollection a je &lt;&gt; odkazem na prvek add, který je přidružen k vašemu vlastnímu zprostředkovateli v souboru web.config. Tento záznam vypadá takto:

[!code-xml[Main](membership/samples/sample6.xml)]

Zde je příklad metody Initialize.

[!code-csharp[Main](membership/samples/sample7.cs)]

Chcete-li ověřit uživatele při odeslání přihlašovacího formuláře, budete muset použít Metodu ValidateUser. Tato metoda se aktivuje, když uživatel klepne na tlačítko přihlášení v ovládacím prvku Přihlášení. Umístíte kód, který provede vyhledávání uživatele v této metodě.

Jak můžete vidět, psaní vlastního poskytovatele členství není obtížné a umožňuje rozšířit tuto výkonnou funkci on-ASP.NET 2.0.
