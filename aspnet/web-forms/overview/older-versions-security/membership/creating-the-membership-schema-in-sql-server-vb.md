---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
title: Vytvoření schématu členství v SQL Server (VB) | Microsoft Docs
author: rick-anderson
description: Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze, aby bylo možné používat SqlMembershipProvider. Po připojení k síti Wi...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 112a674d-716f-41a6-99b8-4074d65a54c0
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 3596e85f6f1e36e046011212479128229be24201
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045075"
---
# <a name="creating-the-membership-schema-in-sql-server-vb"></a>Vytvoření schématu členství v SQL Serveru (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_vb.pdf)

> Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze, aby bylo možné používat SqlMembershipProvider. V tomto případě probereme klíčové tabulky ve schématu a podíváme se na jejich účel a důležitost. V tomto kurzu se dozvíte, jak říct aplikaci ASP.NET, kterou by měl poskytovatel členství použít.

## <a name="introduction"></a>Úvod

Předchozí dva kurzy byly zkontrolovány pomocí ověřování pomocí formulářů k identifikaci návštěvníků webu. Architektura pro ověřování pomocí formulářů umožňuje vývojářům snadno přihlašovat uživatele do webu a zapamatovat si je na stránkách přes použití ověřovacích lístků. `FormsAuthentication`Třída obsahuje metody pro vygenerování lístku a jeho přidání do souborů cookie návštěvníka. `FormsAuthenticationModule`Ověří všechny příchozí požadavky a pro ně s platným ověřovacím lístkem vytvoří a přidruží `GenericPrincipal` `FormsIdentity` objekt a s aktuální žádostí. Ověřování pomocí formulářů je pouze mechanismus pro udělení ověřovacího lístku návštěvníkovi při přihlášení a v následných požadavcích na analýzu tohoto lístku za účelem určení identity uživatele. Aby webová aplikace podporovala uživatelské účty, stále musíme implementovat uživatelské úložiště a přidat funkce pro ověření přihlašovacích údajů, registraci nových uživatelů a nesčetných dalších úloh souvisejících s uživatelským účtem.

Před ASP.NET 2,0 byly vývojáři na vidlici pro implementaci všech úkolů souvisejících s uživatelským účtem. Naštěstí tým ASP.NET tyto nedostatky rozpoznal a zavedl rámec členství v ASP.NET 2,0. Rozhraní členství je sada tříd v .NET Framework, které poskytují programové rozhraní pro provádění úloh souvisejících s uživatelským účtem. Tato architektura je sestavená základem [modelem poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), který vývojářům umožňuje připojit přizpůsobenou implementaci do standardizovaného rozhraní API.

Jak je popsáno v <a id="Tutorial1"></a> kurzu [*Základy zabezpečení a ASP.NET Support*](../introduction/security-basics-and-asp-net-support-vb.md) , .NET Framework se dodává se dvěma integrovanými zprostředkovateli členství: [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) a [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) . V takovém případě `SqlMembershipProvider` používá databáze Microsoft SQL Server jako úložiště uživatele. Aby bylo možné tohoto poskytovatele použít v aplikaci, musíme poskytovatelem sdělit, jakou databázi použít jako úložiště. Jak je možné si představit, `SqlMembershipProvider` očekává, že databáze úložiště uživatelů má některé databázové tabulky, zobrazení a uložené procedury. Musíme do vybrané databáze přidat toto očekávané schéma.

Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze nástroje, aby bylo možné použít `SqlMembershipProvider` . V tomto případě probereme klíčové tabulky ve schématu a podíváme se na jejich účel a důležitost. V tomto kurzu se dozvíte, jak říct aplikaci ASP.NET, kterou by měl poskytovatel členství použít.

Pusťme se do toho.

## <a name="step-1-deciding-where-to-place-the-user-store"></a>Krok 1: rozhodnutí, kam umístit úložiště uživatele

Data aplikace ASP.NET se běžně ukládají v několika tabulkách v databázi. Při implementaci `SqlMembershipProvider` schématu databáze se musíte rozhodnout, jestli se má schéma členství umístit do stejné databáze jako data aplikace nebo do alternativní databáze.

Doporučujeme vyhledat schéma členství ve stejné databázi jako data aplikace z následujících důvodů:

- **Udržovatelnost**  aplikace, jejíž data jsou zapouzdřená v jedné databázi, je snazší pochopit, udržovat a nasazovat než aplikace, která má dvě samostatné databáze.
- **Relační integrita**  hledáním tabulek souvisejících s členstvím ve stejné databázi, jako jsou tabulky aplikace, je možné stanovit [omezení cizího klíče](http://en.wikipedia.org/wiki/Foreign_key) mezi primárními klíči v tabulkách souvisejících s členstvím a souvisejícími tabulkami aplikací.

Oddělit úložiště uživatele a data aplikací do samostatných databází dává smysl jenom v případě, že máte více aplikací, které jednotlivé databáze využívají samostatně, ale potřebují sdílet běžné uživatelské úložiště.

### <a name="creating-a-database"></a>Vytvoření databáze

Aplikace, kterou jsme sestavili, protože druhý kurz ještě nevyžadoval databázi. Pro úložiště uživatelů to ale budeme potřebovat. Pojďme ho vytvořit a potom do něj přidat schéma vyžadované `SqlMembershipProvider` zprostředkovatelem (viz krok 2).

> [!NOTE]
> V této sérii kurzů budeme k ukládání tabulek aplikací a schématu používat databázi [edice Microsoft SQL Server 2005 Express](https://msdn.microsoft.com/sql/Aa336346.aspx) `SqlMembershipProvider` . Toto rozhodnutí bylo provedeno ze dvou důvodů: první z důvodu jeho nákladu zdarma – edice Express je nejužitečnější verze SQL Server 2005; druhý SQL Server 2005 Express Edition databáze je možné umístit přímo do složky webové aplikace a `App_Data` tím učinit cinch k zabalení databáze a webové aplikace společně v jednom souboru zip a k jejímu opětovnému nasazení bez jakýchkoli zvláštních instrukcí pro instalaci nebo možností konfigurace. Pokud byste chtěli postupovat s použitím SQL Server verze non-Express edice, je to klidně. Postup je prakticky identický. `SqlMembershipProvider`Schéma bude fungovat s libovolnou verzí Microsoft SQL Server 2000 a.

V Průzkumník řešení klikněte pravým tlačítkem myši na `App_Data` složku a vyberte možnost Přidat novou položku. (Pokud v projektu nevidíte `App_Data` složku, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, vyberte Přidat složku ASP.NET a vyberte `App_Data` .) V dialogovém okně Přidat novou položku vyberte možnost Přidat novou SQL Database s názvem `SecurityTutorials.mdf` . V tomto kurzu přidáme `SqlMembershipProvider` schéma do této databáze. v dalších kurzech vytvoříme další tabulky pro zachycení dat aplikace.

[![Přidat nový SQL Database s názvem databáze SecurityTutorials. mdf do složky App_Data](creating-the-membership-schema-in-sql-server-vb/_static/image2.png)](creating-the-membership-schema-in-sql-server-vb/_static/image1.png)

**Obrázek 1**: přidání nové SQL Database s názvem `SecurityTutorials.mdf` databáze do `App_Data` složky ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-vb/_static/image3.png))

Přidání databáze do složky se `App_Data` automaticky zahrne do zobrazení Průzkumníka databáze. (Ve verzi aplikace Visual Studio, která není edice Express, se Průzkumník databáze nazývá Průzkumník serveru.) Přejít do Průzkumníka databáze a rozšířit právě přidanou `SecurityTutorials` databázi. Pokud nevidíte Průzkumník databáze na obrazovce, přejděte do nabídky Zobrazit a zvolte Průzkumník databáze nebo stiskněte kombinaci kláves CTRL + ALT + S. Jak ukazuje obrázek 2, `SecurityTutorials` je databáze prázdná – neobsahuje žádné tabulky, žádná zobrazení a žádné uložené procedury.

[![Databáze SecurityTutorials je aktuálně prázdná.](creating-the-membership-schema-in-sql-server-vb/_static/image5.png)](creating-the-membership-schema-in-sql-server-vb/_static/image4.png)

**Obrázek 2**: `SecurityTutorials` databáze je aktuálně prázdná ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image6.png)

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>Krok 2: přidání `SqlMembershipProvider` schématu do databáze

`SqlMembershipProvider`Vyžaduje, aby byla v databázi úložiště uživatelů nainstalována konkrétní sada tabulek, zobrazení a uložených procedur. Tyto požadované objekty databáze je možné přidat pomocí [ `aspnet_regsql.exe` nástroje](https://msdn.microsoft.com/library/ms229862.aspx). Tento soubor je umístěn ve `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` složce.

> [!NOTE]
> `aspnet_regsql.exe`Nástroj nabízí jak funkci příkazového řádku, tak grafické uživatelské rozhraní. Grafické rozhraní je uživatelsky přívětivější a podíváme se v tomto kurzu. Rozhraní příkazového řádku je užitečné v případě, že přidání `SqlMembershipProvider` schématu musí být automatizováno, například ve skriptech sestavení nebo v automatizovaných testovacích scénářích.

`aspnet_regsql.exe`Nástroj se používá k přidání nebo odebrání *ASP.NET aplikačních služeb* do zadané databáze SQL Server. Služba ASP.NET Application Services zahrnuje schémata pro `SqlMembershipProvider` a `SqlRoleProvider` spolu se schématy pro poskytovatele založené na SQL pro jiné architektury ASP.NET 2,0. K nástroji musíme poskytnout dvě bity informací `aspnet_regsql.exe` :

- Zda chceme přidat nebo odebrat aplikační služby a
- Databáze, ze které se má přidat nebo odebrat schéma služby Application Services

Při zobrazení výzvy k použití databáze `aspnet_regsql.exe` vás nástroj vyzve k zadání názvu serveru, na kterém je databáze umístěna, pověření zabezpečení pro připojení k databázi a názvu databáze. Pokud používáte SQL Server bez verze Express, měli byste již znát tyto informace, protože se jedná o stejné informace, které je nutné poskytnout prostřednictvím připojovacího řetězce při práci s databází prostřednictvím webové stránky ASP.NET. Určení názvu serveru a databáze při použití databáze SQL Server 2005 Express Edition ve `App_Data` složce se ale trochu zabývají.

V následující části je jasné, jak zadat název serveru a databáze pro databázi SQL Server 2005 Express Edition do `App_Data` složky. Pokud nepoužíváte SQL Server 2005 Express Edition bez obav, můžete přeskočit k části instalace Aplikační služby.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>Určení názvu serveru a databáze pro databázi SQL Server 2005 Express Edition ve `App_Data` složce

Aby bylo možné použít `aspnet_regsql.exe` nástroj, musíme znát název serveru a databáze. Název serveru je `localhost\InstanceName` . Nejpravděpodobněji je *instance* `SQLExpress` . Pokud jste však nainstalovali SQL Server 2005 Express Edition ručně (to znamená, že jste ho při instalaci sady Visual Studio nenainstalovali automaticky), je možné, že jste vybrali jiný název instance.

Název databáze je bitová trickier, která se má určit. Databáze ve `App_Data` složce mají obvykle název databáze, který obsahuje [globálně jedinečný identifikátor](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) spolu s cestou k databázovému souboru. Aby bylo možné přidat schéma služby Application Services přes, je nutné určit název této databáze `aspnet_regsql.exe` .

Nejjednodušší způsob, jak zjistit název databáze, je prozkoumávat ji pomocí SQL Server Management Studio. SQL Server Management Studio poskytuje grafické rozhraní pro správu databází SQL Server 2005, ale nedodává se s edicí Express verze SQL Server 2005. Dobrá zpráva je, že si [můžete stáhnout](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) bezplatnou verzi Express SQL Server Management Studio.

> [!NOTE]
> Pokud máte na počítači nainstalovanou verzi SQL Server 2005, která není edice Express Express, je pravděpodobně nainstalovaná plná verze Management Studio. Pomocí úplné verze můžete určit název databáze podle stejných kroků, jak je uvedeno níže pro edici Express.

Začněte zavřením sady Visual Studio, abyste zajistili, že všechny zámky, které Visual Studio zaručí v souboru databáze, se zavřou. Dále spusťte SQL Server Management Studio a připojte se k `localhost\InstanceName` databázi pro SQL Server 2005 Express Edition. Jak bylo uvedeno dříve, je pravděpodobné, že je název instance `SQLExpress` . Jako možnost ověřování vyberte ověřování systému Windows.

[![Připojit k instanci SQL Server 2005 Express Edition](creating-the-membership-schema-in-sql-server-vb/_static/image8.png)](creating-the-membership-schema-in-sql-server-vb/_static/image7.png)

**Obrázek 3**: Připojte se k instanci SQL Server 2005 Express Edition ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image9.png)

Po připojení k instanci SQL Server 2005 Express Edition Management Studio zobrazí složky pro databáze, nastavení zabezpečení, objekty serveru atd. Pokud rozbalíte kartu databáze, zjistíte, že `SecurityTutorials.mdf` databáze není *not* zaregistrovaná v instanci databáze. je potřeba nejdřív připojit databázi.

Klikněte pravým tlačítkem na složku databáze a v místní nabídce vyberte připojit. Tím se zobrazí dialogové okno připojit databáze. Odsud klikněte na tlačítko Přidat, přejděte do `SecurityTutorials.mdf` databáze a klikněte na tlačítko OK. Obrázek 4: po výběru databáze se zobrazí dialogové okno připojit databáze `SecurityTutorials.mdf` . Po úspěšném připojení databáze se na obrázku 5 zobrazuje Průzkumník objektů Management Studio.

[![Připojení databáze SecurityTutorials. mdf](creating-the-membership-schema-in-sql-server-vb/_static/image11.png)](creating-the-membership-schema-in-sql-server-vb/_static/image10.png)

**Obrázek 4**: připojení `SecurityTutorials.mdf` databáze ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-vb/_static/image12.png))

[![Databáze SecurityTutorials. mdf se zobrazí ve složce databáze.](creating-the-membership-schema-in-sql-server-vb/_static/image14.png)](creating-the-membership-schema-in-sql-server-vb/_static/image13.png)

**Obrázek 5**: `SecurityTutorials.mdf` databáze se zobrazí ve složce databáze ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image15.png)

Jak ukazuje obrázek 5, `SecurityTutorials.mdf` má databáze spíše abstruse název. Pojďme změnit na srozumitelnější (a jednodušší typ) názvu. Klikněte pravým tlačítkem na databázi, v místní nabídce vyberte Přejmenovat a přejmenujte ji `SecurityTutorialsDatabase` . Tento název souboru se nezmění, stačí pouze název, který databáze používá k identifikaci SQL Server.

[![Přejmenujte databázi na SecurityTutorialsDatabase](creating-the-membership-schema-in-sql-server-vb/_static/image17.png)](creating-the-membership-schema-in-sql-server-vb/_static/image16.png)

**Obrázek 6**: Přejmenování databáze na `SecurityTutorialsDatabase` ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-vb/_static/image18.png))

V tomto okamžiku víme, že název serveru a databáze pro `SecurityTutorials.mdf` soubor databáze: `localhost\InstanceName` a v `SecurityTutorialsDatabase` uvedeném pořadí. Nyní jsme připraveni nainstalovat aplikační služby prostřednictvím tohoto `aspnet_regsql.exe` nástroje.

### <a name="installing-the-application-services"></a>Instalace Aplikační služby

Chcete-li spustit `aspnet_regsql.exe` nástroj, přejděte do nabídky Start a klikněte na příkaz Spustit. `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`Do textového pole zadejte a klikněte na OK. Případně můžete použít Průzkumníka Windows k přechodu k podrobnostem do příslušné složky a dvakrát kliknout na `aspnet_regsql.exe` soubor. Při obou přístupech dojde k rozhledání stejných výsledků.

Spuštění `aspnet_regsql.exe` nástroje bez argumentů příkazového řádku spustí grafické uživatelské rozhraní průvodce ASP.NET SQL Server Setup. Průvodce usnadňuje přidání nebo odebrání aplikačních služeb ASP.NET v zadané databázi. První obrazovka průvodce, zobrazená na obrázku 7, popisuje účel tohoto nástroje.

[![Pomocí Průvodce instalací SQL Server ASP.NET můžete přidat schéma členství.](creating-the-membership-schema-in-sql-server-vb/_static/image20.png)](creating-the-membership-schema-in-sql-server-vb/_static/image19.png)

**Obrázek 7**: pomocí průvodce instalací SQL Server ASP.NET můžete přidat schéma členství ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image21.png)

Druhý krok v Průvodci vás zeptá, jestli chceme přidat aplikační služby nebo je odebrat. Vzhledem k tomu, že chceme přidat tabulky, zobrazení a uložené procedury, které jsou nezbytné pro `SqlMembershipProvider` , vyberte možnost konfigurace SQL Server pro aplikační služby. Pokud později chcete toto schéma z databáze odebrat, spusťte tohoto průvodce znovu, ale místo toho vyberte možnost odebrat informace o službě aplikace z existující databáze.

[![Vyberte možnost konfigurovat SQL Server pro Aplikační služby](creating-the-membership-schema-in-sql-server-vb/_static/image23.png)](creating-the-membership-schema-in-sql-server-vb/_static/image22.png)

**Obrázek 8**: vyberte možnost konfigurovat SQL Server pro aplikační služby ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-vb/_static/image24.png)).

Třetí krok vás vyzve k zadání informací o databázi: název serveru, ověřovací informace a název databáze. Pokud jste spolu s tímto kurzem pojmenovali a Přidali jste `SecurityTutorials.mdf` databázi do, `App_Data` připojili ji k `localhost\InstanceName` a přejmenovali ji na `SecurityTutorialsDatabase` , pak použijte následující hodnoty:

- WebServer `localhost\InstanceName`
- Ověřování systému Windows
- Databáze `SecurityTutorialsDatabase`

[![Zadejte informace o databázi.](creating-the-membership-schema-in-sql-server-vb/_static/image26.png)](creating-the-membership-schema-in-sql-server-vb/_static/image25.png)

**Obrázek 9**: zadání informací o databázi ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-vb/_static/image27.png))

Po zadání informací o databázi klikněte na další. Poslední krok shrnuje kroky, které se provedou. Kliknutím na tlačítko Další nainstalujte aplikační služby a pak dokončete průvodce.

> [!NOTE]
> Pokud jste použili Management Studio k připojení databáze a přejmenování souboru databáze, nezapomeňte před znovu otevřením sady Visual Studio odpojit databázi a zavřít Management Studio. Databázi odpojíte tak `SecurityTutorialsDatabase` , že kliknete pravým tlačítkem na název databáze a v nabídce úlohy zvolíte odpojit.

Po dokončení průvodce se vraťte do sady Visual Studio a přejděte do Průzkumníka databáze. Rozbalte složku tabulky. Měla by se zobrazit řada tabulek, jejichž názvy začínají předponou `aspnet_` . Podobně je možné najít řadu zobrazení a uložených procedur ve složkách zobrazení a uložené procedury. Tyto databázové objekty tvoří schéma služby Application Services. V kroku 3 prověříme objekty databáze pro členství a pro konkrétní role.

[![Do databáze se přidala celá řada tabulek, zobrazení a uložených procedur.](creating-the-membership-schema-in-sql-server-vb/_static/image29.png)](creating-the-membership-schema-in-sql-server-vb/_static/image28.png)

**Obrázek 10**: do databáze se přidala celá řada tabulek, zobrazení a uložených procedur ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image30.png)

> [!NOTE]
> `aspnet_regsql.exe`Grafické uživatelské rozhraní nástroje nainstaluje celé schéma služby Application Services. Ale při provádění `aspnet_regsql.exe` z příkazového řádku můžete určit, jaké konkrétní součásti aplikačních služeb nainstalovat (nebo odebrat). Proto pokud chcete přidat pouze tabulky, zobrazení a uložené procedury, které jsou nezbytné pro `SqlMembershipProvider` `SqlRoleProvider` poskytovatele a, spusťte `aspnet_regsql.exe` z příkazového řádku. Alternativně můžete ručně spustit vhodnou podmnožinu rutin T-SQL Create Scripts, kterou používá `aspnet_regsql.exe` . Tyto skripty se nachází ve `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` složce s názvy, jako jsou,,, `InstallCommon.sql` `InstallMembership.sql` `InstallRoles.sql` `InstallProfile.sql` , `InstallSqlState.sql` a tak dále.

V tuto chvíli jsme vytvořili databázové objekty, které potřebuje `SqlMembershipProvider` . Stále ale musíme instruovat rámec členství, který by měl používat `SqlMembershipProvider` (vs, říkáme `ActiveDirectoryMembershipProvider` ) a který `SqlMembershipProvider` by měl `SecurityTutorials` databázi používat. Podíváme se na to, jak určit poskytovatele, který se má použít, a jak přizpůsobit nastavení vybraného poskytovatele v kroku 4. Nejdřív se podíváme na objekty databáze, které jste právě vytvořili.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>Krok 3: Prohlédněte si základní tabulky schématu

Při práci s architekturou členství a rolí v aplikaci ASP.NET jsou podrobnosti implementace zapouzdřeny zprostředkovatelem. V budoucích kurzech se s těmito rozhraními přihlásíme prostřednictvím .NET Framework `Membership` a `Roles` tříd. Pokud používáte tato rozhraní API na vysoké úrovni, nemusíte se v dodržovali s podrobnostmi na nízké úrovni, jako jsou třeba dotazy, které jsou spouštěny nebo které tabulky upravují `SqlMembershipProvider` a `SqlRoleProvider` .

V tomto případě jsme mohli bez obav použít rámec členství a rolí, aniž byste prozkoumali schéma databáze vytvořené v kroku 2. Při vytváření tabulek pro ukládání aplikačních dat ale můžeme potřebovat vytvořit entity, které se vztahují na uživatele nebo role. Pomáhá znát `SqlMembershipProvider` `SqlRoleProvider` schémata a při určování omezení cizího klíče mezi tabulkami dat aplikace a tabulkami vytvořenými v kroku 2. Kromě toho může být někdy nutné použít rozhraní s uživateli a rolemi role přímo na úrovni databáze (místo přes `Membership` `Roles` třídy nebo).

### <a name="partitioning-the-user-store-into-applications"></a>Rozdělení uživatelského úložiště do aplikací

Rozhraní pro členství a role jsou navržena tak, aby bylo možné sdílet jediné úložiště uživatelů a rolí mezi mnoha různými aplikacemi. Aplikace ASP.NET, která používá rámec členství nebo rolí, musí určovat, který oddíl aplikace se má použít. V krátkém případě může více webových aplikací používat stejné úložiště uživatelů a rolí. Obrázek 11 znázorňuje úložiště uživatelů a rolí, která jsou rozdělená na tři aplikace: HRSite, CustomerSite a SalesSite. Každá z těchto tří webových aplikací má své vlastní jedinečné uživatele a role, ale všechny fyzicky ukládají informace o uživatelských účtech a rolích ve stejných databázových tabulkách.

[![Uživatelské účty můžou být rozdělené mezi několik aplikací.](creating-the-membership-schema-in-sql-server-vb/_static/image32.png)](creating-the-membership-schema-in-sql-server-vb/_static/image31.png)

**Obrázek 11**: uživatelské účty můžou být rozdělené mezi více aplikací ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-vb/_static/image33.png)

V `aspnet_Applications` tabulce jsou tyto oddíly definovány. Každá aplikace, která používá databázi k ukládání informací o uživatelském účtu, je reprezentována řádkem v této tabulce. `aspnet_Applications`Tabulka obsahuje čtyři sloupce: `ApplicationId` , `ApplicationName` , `LoweredApplicationName` a `Description` .`ApplicationId` je typu [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) a je primární klíč tabulky; `ApplicationName` poskytuje jedinečný popisný název pro každou aplikaci.

Ostatní tabulky vztahující se k členství a rolím odkazují zpátky na `ApplicationId` pole v `aspnet_Applications` . Například `aspnet_Users` tabulka, která obsahuje záznam pro každý uživatelský účet, má `ApplicationId` pole cizího klíče; Ditto pro `aspnet_Roles` tabulku. `ApplicationId`Pole v těchto tabulkách určuje oddíl aplikace, ke kterému patří uživatelský účet nebo role.

### <a name="storing-user-account-information"></a>Ukládání informací o uživatelském účtu

Informace o uživatelském účtu jsou umístěné ve dvou tabulkách: `aspnet_Users` a `aspnet_Membership` . `aspnet_Users`Tabulka obsahuje pole, která obsahují základní informace o uživatelském účtu. Tři nejvíce relevantní sloupce jsou:

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` je primární klíč (a typu `uniqueidentifier` ). `UserName` je typu `nvarchar(256)` a společně s heslem, tvoří přihlašovací údaje uživatele. (Heslo uživatele je uloženo v `aspnet_Membership` tabulce.) `ApplicationId` propojí uživatelský účet s konkrétní aplikací v nástroji `aspnet_Applications` . Na sloupcích a je složené [ `UNIQUE` omezení](https://msdn.microsoft.com/library/ms191166.aspx) `UserName` `ApplicationId` . Tím je zajištěno, že v dané aplikaci je každé uživatelské jméno jedinečné, ale umožňuje použití stejného typu `UserName` v různých aplikacích.

`aspnet_Membership`Tabulka obsahuje další informace o uživatelském účtu, například heslo, e-mailovou adresu, poslední datum a čas přihlášení a tak dále. Mezi záznamy v tabulkách a se vyskytuje jedna souvislost `aspnet_Users` `aspnet_Membership` . Tento vztah je zajištěný `UserId` polem v `aspnet_Membership` , které slouží jako primární klíč tabulky. Podobně jako v `aspnet_Users` tabulce `aspnet_Membership` obsahuje `ApplicationId` pole, které spojuje tyto informace s konkrétním oddílem aplikace.

### <a name="securing-passwords"></a>Zabezpečení hesel

Informace o heslech jsou uloženy v `aspnet_Membership` tabulce. `SqlMembershipProvider`Umožňuje ukládat hesla v databázi pomocí jedné z následujících tří postupů:

- **Clear** – heslo je uloženo v databázi jako prostý text. Tuto možnost rozhodně neodrazí. Pokud je databáze ohrožená hackerem, který vyhledává zadní vrátka nebo Disgruntled zaměstnanec, který má přístup k databázi, jsou k dispozici pouze pověření jednotlivých uživatelů.
- **Hash** – hesla se používají pomocí jednosměrného algoritmu hash a náhodně generované hodnoty Salt. Tato hodnota hash (spolu s hodnotou Salt) je uložená v databázi.
- **Šifrované** – zašifrovaná verze hesla je uložená v databázi.

Použitá technika úložiště hesla závisí na `SqlMembershipProvider` nastaveních uvedených v `Web.config` . Podíváme se na přizpůsobení `SqlMembershipProvider` nastavení v kroku 4. Výchozím chováním je uložení hodnoty hash hesla.

Sloupce zodpovědné za uložení hesla jsou `Password` , `PasswordFormat` a `PasswordSalt` . `PasswordFormat` je pole typu, `int` jehož hodnota označuje techniku použitou pro uložení hesla: 0 pro Clear; 1 pro hodnotu Hashed; 2 pro šifrování. `PasswordSalt` je přiřazen náhodně vygenerovaný řetězec bez ohledu na použitou techniku úložiště hesla; hodnota `PasswordSalt` se používá jenom v případě, že se počítá hodnota hash hesla. Nakonec `Password` sloupec obsahuje skutečná data o heslech, jedná se o heslo s prostým textem, hodnotu hash hesla nebo šifrované heslo.

Tabulka 1 znázorňuje, jaké tři sloupce můžou vypadat jako u různých technik úložiště při ukládání hesla MySecret! .

| **O3a techniky úložiště &lt; \_ \_ p/&gt;** | **Heslo &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **PasswordSalt &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Vymazat | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| Rozdělí | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| Šifrované | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/AA/oqAXGLHJNBw = = |

**Tabulka 1**: příklad hodnot polí souvisejících s heslem při ukládání hesla MySecret!

> [!NOTE]
> Konkrétní šifrování nebo algoritmus hash, který používá, `SqlMembershipProvider` je určen nastavením v `<machineKey>` elementu. Tento prvek konfigurace jsme probrali v kroku 3 <a id="Tutorial3"></a> kurzu [*Konfigurace ověřování formulářů a Pokročilá témata*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) .

### <a name="storing-roles-and-role-associations"></a>Ukládání rolí a přidružení rolí

Rozhraní role umožňují vývojářům definovat sadu rolí a určit, co uživatelé patří k rolím. Tyto informace jsou zachyceny v databázi prostřednictvím dvou tabulek: `aspnet_Roles` a `aspnet_UsersInRoles` . Každý záznam v `aspnet_Roles` tabulce představuje roli pro konkrétní aplikaci. Podobně jako u `aspnet_Users` tabulky `aspnet_Roles` má tabulka tři sloupce, které jsou relevantní pro naši diskuzi:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` je primární klíč (a typu `uniqueidentifier` ). `RoleName` je typu `nvarchar(256)` . A `ApplicationId` propojí uživatelský účet s konkrétní aplikací v nástroji `aspnet_Applications` . Ve `UNIQUE` sloupcích a je složené omezení `RoleName` `ApplicationId` , které zajišťuje, že v dané aplikaci je název každé role jedinečný.

Tato `aspnet_UsersInRoles` tabulka slouží jako mapování mezi uživateli a rolemi. Existují pouze dva sloupce – `UserId` a `RoleId` společně tvoří složený primární klíč.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>Krok 4: určení poskytovatele a přizpůsobení jeho nastavení

Všechny architektury, které podporují model poskytovatele – jako jsou například rozhraní pro členství a role – neobsahují detaily implementace samy a místo toho deleguje tuto zodpovědnost na třídu poskytovatele. V případě rozhraní členství `Membership` definuje Třída rozhraní API pro správu uživatelských účtů, ale nekomunikuje přímo s žádným uživatelským úložištěm. Místo toho `Membership` metody třídy předají požadavek nakonfigurovanému poskytovateli – budeme používat `SqlMembershipProvider` . Když vyvoláme jednu z metod ve `Membership` třídě, jak rozhraní členství zná, aby bylo volání delegováno `SqlMembershipProvider` ?

`Membership`Třída má [ `Providers` vlastnost](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) , která obsahuje odkaz na všechny třídy registrovaných zprostředkovatelů, které jsou k dispozici pro použití v rámci architektury členství. Každý registrovaný zprostředkovatel má přidružené jméno a typ. Název nabízí uživatelsky přívětivý způsob, jak odkazovat na konkrétního poskytovatele v `Providers` kolekci, zatímco typ identifikuje třídu poskytovatele. Každý registrovaný zprostředkovatel navíc může obsahovat nastavení konfigurace. Nastavení konfigurace pro rámec členství zahrnuje `PasswordFormat` a `requiresUniqueEmail` , mezi mnoho dalších. Úplný seznam konfiguračních nastavení používaných nástrojem najdete v tabulce 2 `SqlMembershipProvider` .

`Providers`Obsah vlastnosti se určuje prostřednictvím nastavení konfigurace webové aplikace. Ve výchozím nastavení mají všechny webové aplikace poskytovatele s názvem `AspNetSqlMembershipProvider` typu `SqlMembershipProvider` . Tento výchozí zprostředkovatel členství je zaregistrován v `machine.config` (umístěný v `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG` ):

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample1.xml)]

Jak ukazuje kód uvedený výše, [ `<membership>` prvek](https://msdn.microsoft.com/library/1b9hw62f.aspx) definuje nastavení konfigurace pro rozhraní členství, zatímco [ `<providers>` podřízený prvek](https://msdn.microsoft.com/library/6d4936ht.aspx) určuje registrované zprostředkovatele. Poskytovatelé mohou být přidáni nebo odebráni pomocí [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) prvků nebo; pomocí [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) elementu odebrat všechny aktuálně registrované zprostředkovatele. Jak ukazuje kód uvedený výše, `machine.config` přidá poskytovatele s názvem `AspNetSqlMembershipProvider` typu `SqlMembershipProvider` .

Kromě `name` `type` atributů a `<add>` obsahuje element atributy, které definují hodnoty pro různá nastavení konfigurace. Tabulka 2 obsahuje seznam dostupných `SqlMembershipProvider` nastavení konfigurace spolu s popisem každého z nich.

> [!NOTE]
> Všechny výchozí hodnoty zaznamenané v tabulce 2 odkazují na výchozí hodnoty definované ve `SqlMembershipProvider` třídě. Všimněte si, že ne všechna nastavení konfigurace v nástroji `AspNetSqlMembershipProvider` odpovídají výchozím hodnotám `SqlMembershipProvider` třídy. Pokud není například zadáno ve zprostředkovateli členství, je `requiresUniqueEmail` výchozí nastavení nastaveno na hodnotu true. Nicméně `AspNetSqlMembershipProvider` přepíše tuto výchozí hodnotu explicitním zadáním hodnoty `false` .

| **Nastavení &lt; \_ o3a \_ p/&gt;** | **Popis &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | Odvolání, že rozhraní členství umožňuje rozdělit jednotlivé úložiště uživatelů na oddíly mezi více aplikacemi. Toto nastavení označuje název oddílu aplikace používaného poskytovatelem členství. Pokud tato hodnota není explicitně zadána, je nastavena za běhu na hodnotu pro virtuální kořenovou cestu aplikace. |
| `commandTimeout` | Určuje hodnotu časového limitu příkazu SQL (v sekundách). Výchozí hodnota je 30. |
| `connectionStringName` | Název připojovacího řetězce v `<connectionStrings>` elementu, který se má použít pro připojení k databázi úložiště uživatele. Tato hodnota se vyžaduje. |
| `description` | Poskytuje uživatelsky přívětivý popis zaregistrovaného poskytovatele. |
| `enablePasswordRetrieval` | Určuje, jestli uživatelé můžou načítat zapomenuté heslo. Výchozí hodnota je `false`. |
| `enablePasswordReset` | Určuje, jestli uživatelé můžou resetovat svoje heslo. Výchozí hodnota je `true` . |
| `maxInvalidPasswordAttempts` | Maximální počet neúspěšných pokusů o přihlášení, které se můžou vyskytnout pro daného uživatele během zadaného období, `passwordAttemptWindow` než se uživatel zamkne. Výchozí hodnota je 5. |
| `minRequiredNonalphanumericCharacters` | Minimální počet nealfanumerických znaků, které se musí objevit v uživatelském hesle. Tato hodnota musí být v rozmezí od 0 do 128. Výchozí hodnota je 1. |
| `minRequiredPasswordLength` | Minimální počet znaků vyžadovaných v hesle. Tato hodnota musí být v rozmezí od 0 do 128. Výchozí hodnota je 7. |
| `name` | Název zaregistrovaného poskytovatele. Tato hodnota se vyžaduje. |
| `passwordAttemptWindow` | Počet minut, během kterých jsou sledovány neúspěšné pokusy o přihlášení Pokud uživatel `maxInvalidPasswordAttempts` do tohoto zadaného okna zadá neplatné přihlašovací údaje, budou uzamčeny. Výchozí hodnota je 10. |
| `PasswordFormat` | Formát úložiště hesla: `Clear` , `Hashed` nebo `Encrypted` . Výchozí formát je `Hashed`. |
| `passwordStrengthRegularExpression` | Pokud je tento regulární výraz k dispozici, slouží k vyhodnocení síly vybraného hesla uživatele při vytváření nového účtu nebo při změně hesla. Výchozí hodnota je prázdný řetězec. |
| `requiresQuestionAndAnswer` | Určuje, jestli uživatel musí při načítání nebo resetování hesla odpovědět na jeho bezpečnostní otázku. Výchozí hodnota je `true`. |
| `requiresUniqueEmail` | Uvádí, zda všechny uživatelské účty v daném oddílu aplikace musí mít jedinečnou e-mailovou adresu. Výchozí hodnota je `true`. |
| `type` | Určuje typ poskytovatele. Tato hodnota se vyžaduje. |

**Tabulka 2**: nastavení členství a `SqlMembershipProvider` konfigurací

Kromě `AspNetSqlMembershipProvider` toho mohou být jiní poskytovatelé členství zaregistrovaní na základě aplikace tak, že do souboru přidají podobný kód `Web.config` .

> [!NOTE]
> Architektura rolí funguje v podstatě stejným způsobem: je k dispozici výchozí registrovaný zprostředkovatel rolí v nástroji `machine.config` a zaregistrovaná zprostředkovatelé mohou být přizpůsobeni na základě aplikace v nástroji `Web.config` . V budoucím kurzu podíváme se na podrobné informace o architektuře rolí a o konfiguraci.

### <a name="customizing-thesqlmembershipprovidersettings"></a>Přizpůsobení `SqlMembershipProvider` nastavení

Výchozí `SqlMembershipProvider` ( `AspNetSqlMembershipProvider` ) má svůj `connectionStringName` atribut nastavený na `LocalSqlServer` . Podobně jako u `AspNetSqlMembershipProvider` poskytovatele je název připojovacího řetězce `LocalSqlServer` definován v `machine.config` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample2.xml)]

Jak vidíte, tento připojovací řetězec definuje databázi edice SQL 2005 Express v umístění | DataDirectory | Aspnetdb. mdf. Řetězec | Adresář DataDirectory | se převede za běhu tak, aby odkazovala na `~/App_Data/` adresář, a tak cestu k databázi | DataDirectory | Aspnetdb. mdf se převede na `~/App_Data` / `aspnet.mdf` .

Pokud v souboru aplikace neurčíme žádné informace o poskytovateli členství `Web.config` , aplikace použije výchozího registrovaného poskytovatele členství `AspNetSqlMembershipProvider` . Pokud `~/App_Data/aspnet.mdf` databáze neexistuje, modul runtime ASP.NET ho automaticky vytvoří a přidá schéma služby Application Services. Nechce ale používat `aspnet.mdf` databázi. místo toho chceme použít databázi, kterou `SecurityTutorials.mdf` jsme vytvořili v kroku 2. Tuto úpravu lze provést jedním ze dvou způsobů:

- <strong>Zadejte hodnotu pro</strong> <strong>`LocalSqlServer`</strong> <strong>název připojovacího řetězce v</strong> <strong>`Web.config`</strong> <strong>.</strong> Přepsáním `LocalSqlServer` hodnoty názvu připojovacího řetězce v `Web.config` můžete použít výchozího registrovaného poskytovatele členství ( `AspNetSqlMembershipProvider` ) a správně pracovat s `SecurityTutorials.mdf` databází. Tento přístup je v případě, že se jedná o obsah s nastavením konfigurace specifikovaným, v pořádku `AspNetSqlMembershipProvider` . Další informace o této technice najdete v příspěvku na blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/), [konfigurace ASP.NET 2,0 Aplikační služby pro použití SQL Server 2000 nebo SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>Přidat nového registrovaného poskytovatele typu</strong> <strong>`SqlMembershipProvider`</strong> <strong>a nakonfigurujte</strong> <strong>`connectionStringName`</strong> <strong>nastavení, které odkazuje</strong> <strong>`SecurityTutorials.mdf`</strong> na <strong>databáze.</strong> Tento přístup je užitečný ve scénářích, kdy chcete kromě připojovacího řetězce databáze upravit i další vlastnosti konfigurace. V mých vlastních projektech tento přístup vždycky používám z důvodu jeho flexibility a čitelnosti.

Předtím, než můžeme přidat nového registrovaného poskytovatele, který odkazuje na `SecurityTutorials.mdf` databázi, musíme nejdřív přidat odpovídající hodnotu připojovacího řetězce v `<connectionStrings>` části v tématu `Web.config` . Následující kód přidá nový připojovací řetězec s názvem `SecurityTutorialsConnectionString` , který odkazuje na `SecurityTutorials.mdf` databázi SQL Server 2005 Express Edition ve `App_Data` složce.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample3.xml)]

> [!NOTE]
> Pokud používáte alternativní databázový soubor, podle potřeby aktualizujte připojovací řetězec. Další informace o vytváření správného připojovacího řetězce najdete v tématu [connectionStrings.com](http://www.connectionstrings.com/).

Dále přidejte do souboru následující označení konfigurace členství `Web.config` . Tento kód zaregistruje nového poskytovatele s názvem `SecurityTutorialsSqlMembershipProvider` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample4.xml)]

Kromě registrace `SecurityTutorialsSqlMembershipProvider` poskytovatele je výše uvedený kód definován `SecurityTutorialsSqlMembershipProvider` jako výchozí zprostředkovatel (prostřednictvím `defaultProvider` atributu v `<membership>` elementu). Odvolání, že rozhraní členství může mít více registrovaných zprostředkovatelů. Vzhledem k tomu `AspNetSqlMembershipProvider` , že je zaregistrován jako první zprostředkovatel v nástroji `machine.config` , slouží jako výchozí zprostředkovatel, pokud neurčíte jinak.

V současné době má naše aplikace dva registrované zprostředkovatele: `AspNetSqlMembershipProvider` a `SecurityTutorialsSqlMembershipProvider` . Před registrací zprostředkovatele však `SecurityTutorialsSqlMembershipProvider` můžeme vymazal všechny dříve registrované poskytovatele přidáním [ `<clear />` prvku](https://msdn.microsoft.com/library/t062y6yc.aspx) bezprostředně před náš `<add>` element. Tím se vymaže `AspNetSqlMembershipProvider` ze seznamu registrovaných zprostředkovatelů, což znamená, že se jedná o `SecurityTutorialsSqlMembershipProvider` jediného registrovaného poskytovatele členství. Pokud jsme použili tento přístup, nemuseli byste označit `SecurityTutorialsSqlMembershipProvider` jako výchozího zprostředkovatele, protože by to byl jediný registrovaný poskytovatel členství. Další informace o použití nástroje `<clear />` najdete v tématu [použití `<clear />` při přidávání zprostředkovatelů](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx).

Všimněte si, `SecurityTutorialsSqlMembershipProvider` že `connectionStringName` Nastavení 's odkazuje na název právě přidávaného `SecurityTutorialsConnectionString` připojovacího řetězce a že jeho `applicationName` nastavení bylo nastaveno na hodnotu SecurityTutorials. Nastavení je navíc `requiresUniqueEmail` nastavené na `true` . Všechny ostatní možnosti konfigurace se shodují s hodnotami v `AspNetSqlMembershipProvider` . Pokud chcete, můžete tady dělat jakékoli změny konfigurace. Například můžete zvýšit sílu hesla vyžadováním dvou než alfanumerických znaků místo jednoho nebo zvýšením délky hesla na osm znaků namísto sedmi.

> [!NOTE]
> Odvolání, že rozhraní členství umožňuje rozdělit jednotlivé úložiště uživatelů na oddíly mezi více aplikacemi. Nastavení poskytovatele členství `applicationName` Určuje, jaká aplikace poskytovatel používá při práci s úložištěm uživatele. Je důležité, abyste explicitně nastavili hodnotu pro `applicationName` nastavení konfigurace, protože pokud `applicationName` není explicitně nastavená, přiřadí se k virtuální kořenové cestě webové aplikace za běhu. To funguje, pokud se nemění virtuální kořenová cesta aplikace, ale pokud přesunete aplikaci na jinou cestu, `applicationName` změní se také nastavení. Pokud k tomu dojde, zprostředkovatel členství začne pracovat s jiným oddílem aplikace, než se dřív používal. Uživatelské účty vytvořené před přesunem se budou nacházet v jiném oddílu aplikace a uživatelé se už nebudou moct k lokalitě přihlašovat. Podrobnější diskusi k této problematice najdete v tématu [vždy nastavte `applicationName` vlastnost při konfiguraci členství ASP.NET 2,0 a jiných poskytovatelů](https://weblogs.asp.net/scottgu/443634).

## <a name="summary"></a>Souhrn

V tuto chvíli máme databázi s nakonfigurovanými aplikačními službami ( `SecurityTutorials.mdf` ) a nakonfigurovali jsme naši webovou aplikaci tak, aby rozhraní členství používalo `SecurityTutorialsSqlMembershipProvider` poskytovatele, kterého jsme právě zaregistrovali. Tento registrovaný zprostředkovatel je typu `SqlMembershipProvider` a má `connectionStringName` nastaven na příslušný připojovací řetězec ( `SecurityTutorialsConnectionString` ) a jeho `applicationName` hodnotu explicitně nastavuje.

Nyní jsme připraveni použít rozhraní pro členství z naší aplikace. V dalším kurzu podíváme se, jak vytvořit nové uživatelské účty. Po prozkoumání ověření uživatelů, provádění ověřování na základě uživatelů a ukládání dalších informací souvisejících s uživatelem do databáze.

Šťastné programování!

### <a name="further-reading"></a>Další materiály

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vždy nastavit `applicationName` vlastnost při konfiguraci členství ASP.NET 2,0 a jiných poskytovatelů](https://weblogs.asp.net/scottgu/443634)
- [Konfigurace ASP.NET 2,0 Aplikační služby pro použití SQL Server 2000 nebo SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Stáhnout SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [Zkoumání členství, rolí a profilů v ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>`Element pro poskytovatele pro členství](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>`Element](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>`Element pro členství](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [Použití `<clear />` při přidávání zprostředkovatelů](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [Práce přímo s `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Výukové video o tématech obsažených v tomto kurzu

- [Principy členství v ASP.NET](../../../videos/authentication/understanding-aspnet-memberships.md)
- [Konfigurace SQL kvůli spolupráci se schématy členství](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [Změna nastavení členství ve výchozím schématu členství](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott se dá kontaktovat na [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) blogu nebo přes jeho blog na adrese [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Alicja Maziarz. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, umístěte mi čáru na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) .

> [!div class="step-by-step"]
> [Předchozí](storing-additional-user-information-cs.md) 
>  [Další](creating-user-accounts-vb.md)
