---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: Přehled ověřování pomocí formulářů (VB) | Dokumentace Microsoftu
author: rick-anderson
description: V tomto kurzu Změníme z pouhé Diskuze k provádění; Konkrétně se podíváme na provádění ověřování pomocí formulářů. Webové aplikace w...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: ca290c6b7b6b4f8da92b9658519d716651d46341
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072841"
---
<a name="an-overview-of-forms-authentication-vb"></a>Přehled ověřování pomocí formulářů (VB)
====================
podle [Scott Meisnerová](https://twitter.com/ScottOnWriting)

[Stáhněte si kód](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> V tomto kurzu Změníme z pouhé Diskuze k provádění; Konkrétně se podíváme na provádění ověřování pomocí formulářů. Webová aplikace začneme vytváření v tomto kurzu se bude nadále být: založené na řešení v dalších kurzech se přesunu z jednoduchého ověřování pomocí formulářů do členství a rolí.
> 
> V tomto tématu najdete v článku tohoto videa pro další informace: [Základní ověřování pomocí formulářů v ASP.NET](# "using-basic-forms-authentication-in-aspnet").


## <a name="introduction"></a>Úvod

V [předchozím kurzu](security-basics-and-asp-net-support-vb.md) jsme probírali různé možnosti účtu ověřování, autorizaci a uživatel poskytovaných technologií ASP.NET. V tomto kurzu Změníme z pouhé Diskuze k provádění; Konkrétně se podíváme na provádění ověřování pomocí formulářů. Webová aplikace začneme vytváření v tomto kurzu se bude nadále být: založené na řešení v dalších kurzech se přesunu z jednoduchého ověřování pomocí formulářů do členství a rolí.

V tomto kurzu začíná podrobný rozbor toho ověřovací pracovní postup systému formuláře, na téma, které jsme některé po v předchozím kurzu. Pod vytvoříme webu ASP.NET pomocí kterého je možné ukázka koncepty ověřování pomocí formulářů. Dále jsme se konfigurace lokality pro ověřování pomocí formulářů, vytvořit jednoduchý přihlašovací stránku a zjistit, jak zjistit, v kódu, zda je uživatel ověřený, a pokud ano, uživatelské jméno se protokolují v.

Principy formulářů ověřovací pracovní postup povolení ve webové aplikaci a vytvoření přihlášení a odhlášení stránky jsou všechny důležité kroky při vytváření aplikace technologie ASP.NET, která podporuje uživatelské účty a ověřování uživatelů prostřednictvím webové stránky. Kvůli tomu – a vzhledem k tomu, že tyto kurzy vycházejí z jiného - by neváhejte práci kroky v tomto kurzu v plné výši před přechodem k dalšímu i v případě, že už máte prostředí pro konfiguraci ověřování formulářů v posledních projektů.

## <a name="understanding-the-forms-authentication-workflow"></a>Principy formulářů ověřovací pracovní postup

Pokud modul runtime ASP.NET zpracovává žádost o prostředek technologie ASP.NET, například stránky technologie ASP.NET nebo webové služby ASP.NET, vyvolá požadavek počet událostí během životního cyklu. Existují událostí vyvolaných na konci velmi počáteční a velmi žádosti, které se vyvolá, když požadavek je se ověří a autorizuje, Událost aktivovaná v případě neošetřené výjimky a tak dále. Pokud chcete zobrazit úplný seznam událostí, najdete [události objektu HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx).

*Z modulů HTTP* jsou spravované třídy, jejíž kód je prováděn v reakci na konkrétní událost v životního cyklu požadavku. Technologie ASP.NET se dodává s celou řadou z modulů HTTP, který provádění základních úloh na pozadí. Jsou dva integrované moduly protokolu HTTP, které jsou obzvláště důležité pro naše diskuse:

- **[FormsAuthenticationModule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)**  -ověřuje uživatele zkontrolováním lístek ověřování pomocí formulářů, který je obvykle součástí kolekce souborů cookie uživatele. Pokud je k dispozici žádné ověřovací lístek, je anonymní uživatel.
- **[UrlAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)**  – Určuje, zda je aktuální uživatel oprávnění pro přístup k požadované adrese URL. Tento modul určuje oprávnění, o consulting autorizační pravidla zadaná v konfiguračních souborech aplikace. Technologie ASP.NET obsahuje také [FileAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) , který určuje o požadované soubory seznamů řízení přístupu autorita.

FormsAuthenticationModule pokus o ověření uživatelů před UrlAuthorizationModule (a FileAuthorizationModule) provádění. Pokud uživatel zadal žádost nemá oprávnění pro přístup k požadovanému prostředku, modul autorizace ukončí požadavek a vrátí [HTTP 401 neoprávněný](http://www.checkupdown.com/status/E401.html) stav. Ve scénářích ověřování Windows je vrácen stav HTTP 401 do prohlížeče. Tento stavový kód způsobí, že prohlížeč zobrazí výzvu k zadání přihlašovacích údajů prostřednictvím modální dialogové okno. Pomocí ověřování pomocí formulářů, ale HTTP 401 Unauthorized status je nikdy neodesílá do prohlížeče vzhledem k tomu, FormsAuthenticationModule zjistí tento stav a změní ho přesměrovat uživatele na přihlašovací stránku místo toho (prostřednictvím [HTTP 302 přesměrovat](http://www.checkupdown.com/status/E302.html) stav).

Na přihlašovací stránku zodpovědností je určení, zda přihlašovací údaje uživatele jsou platné, a pokud ano, vytvořit lístek ověřování formulářů a přesměruje uživatele zpět na stránku se pokoušeli navštívit. Lístek ověřování je zahrnuta v následné žádosti na stránky na webu, který FormsAuthenticationModule používá k identifikaci uživatele.


[![Ověřovací pracovní postup formulářů](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**Obrázek 01**: Ověřovací pracovní postup formulářů ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image3.png))


### <a name="remembering-the-authentication-ticket-across-page-visits"></a>Zapamatování lístek ověřování napříč návštěv stránky

Po přihlášení musí být ověřovací lístek odesílaných zpět do webového serveru na každý požadavek tak, aby uživatel zůstane přihlášený jako procházení webu. To je obvykle provedeno umístěním ověřovací lístek do kolekce souborů cookie uživatele. [Soubory cookie](http://en.wikipedia.org/wiki/HTTP_cookie) jsou malé textové soubory, které jsou umístěny v počítači uživatele a přenášejí v hlavičkách protokolu HTTP pro každý požadavek na webu, který vytvoří soubor cookie. Proto Jakmile ověřovací lístek byly vytvořeny a uloženy v souborech cookie v prohlížeči, každé následné návštěvě této lokality odešle lístek ověřování spolu s požadavkem, a ne k identifikaci uživatelů.

> [!NOTE]
> Ukázkové webové aplikaci používá v každém kurzu, je k dispozici ke stažení. Tato aplikace ke stažení někdo vytvořil v aplikaci Visual Web Developer 2008 určené pro rozhraní .NET Framework verze 3.5. Protože aplikace je určená pro .NET 3.5, jeho soubor Web.config obsahuje další, 3.5 konkrétní konfigurační prvky. Dlouhý text krátký, pokud ještě nemáte k instalaci rozhraní .NET 3.5 na počítači poté ke stažení webové aplikace nebude fungovat bez první odebrání 3.5 konkrétní značku ze souboru Web.config.


Jeden aspekt souborů cookie je jejich vypršení platnosti, což je datum a čas, kdy prohlížeč odstraní soubor cookie. Když vyprší platnost souboru cookie pro ověřování pomocí formulářů, může uživatel již ověření a proto budou anonymní. Když je uživatel navštívit z veřejného terminálu, je pravděpodobné, že chtějí jejich lístku ověřování vyprší po uzavření prohlížeče. Při návštěvě z domova, ale tento stejný uživatel může být vhodné lístek ověřování, chcete-li být uloží napříč prohlížeči restartování, takže není nutné znovu přihlásit pokaždé, když se na webu. Toto rozhodnutí je často provedené uživatelem v podobě zapamatovat zaškrtávací políčko na přihlašovací stránce. V kroku 3 prozkoumáme implementace zaškrtávací políčko pamatovat si mě na přihlašovací stránce. V následujícím kurzu řeší nastavení časového limitu lístek ověřování podrobně.

> [!NOTE]
> Je možné, že uživatelský agent použitý k přihlášení na web pravděpodobně nepodporuje soubory cookie. V takovém případě můžete použít technologie ASP.NET lístků pro ověřování pomocí formulářů bez souborů cookie. V tomto režimu se lístek ověřování je zakódovaný do adresy URL. Podíváme se na při použití lístků pro ověřování bez souborů cookie a jak se vytváří a spravují v dalším kurzu.


### <a name="the-scope-of-forms-authentication"></a>Rozsah ověřování pomocí formulářů

FormsAuthenticationModule je spravovaný kód, který je součástí modulu runtime ASP.NET. Starší než verze 7 od Microsoftu [Internetové informační služby (IIS)](https://www.iis.net/) webový server, se liší bariéru mezi kanálu protokolu HTTP služby IIS a modulu runtime ASP.NET kanálu. Stručně řečeno, ve službě IIS 6 a starší FormsAuthenticationModule provede jenom v případě požadavku se deleguje ze služby IIS na modul runtime ASP.NET. Ve výchozím nastavení služba IIS zpracovává statické samotného obsahu – například stránky HTML a CSS a soubory obrázků – a pouze hands vypnout požadavky na modul runtime ASP.NET při požadavku na stránku s příponou .aspx, .asmx a ASHX.

Integrované služby IIS a ASP.NET IIS 7, ale umožňuje spouštění kanálů. S několika nastavení konfigurace můžete nastavit službu IIS 7, který má být vyvolán FormsAuthenticationModule pro *všechny* požadavky. Kromě toho pomocí služby IIS 7 můžete definovat autorizačních pravidel adres URL pro soubory libovolného typu. Další informace najdete v tématu [změny mezi IIS6 a zabezpečení služby IIS7](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [váš Web zabezpečení platformy](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements), a [autorizace adres URL pro službu IIS7 Principy](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization).

Dlouhý text krátkého ve verzích před IIS 7, ověřování pomocí formulářů můžete použít jenom k ochraně prostředků zpracování modulem ASP.NET runtime. Obdobně autorizačních pravidel adres URL platí pouze pro prostředky, zpracovává modul runtime ASP.NET. Ale se službou IIS 7 je možné integrovat FormsAuthenticationModule a UrlAuthorizationModule do kanálu HTTP služby IIS, tím rozšiřuje tuto funkci pro všechny požadavky.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>Krok 1: Vytvoření webu ASP.NET pro tuto řadu kurzů

Pokud chcete oslovit širokou cílovou skupinu je to možné, se vytvoří web ASP.NET jsme se sestavování v celé této sérii s společnosti Microsoft bezplatnou verzi Visual Studio 2008 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/). Implementujeme SqlMembershipProvider úložišti uživatelů v [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) databáze. Pokud používáte Visual Studio 2005 nebo jinou edici sady Visual Studio 2008 nebo SQL Server, Nedělejte si starosti – kroky budou téměř identické a bude třeba zdůraznit, nejsou v netriviálních rozdíly.

Než budeme moct nakonfigurovat nastavení ověřování pomocí formulářů, musíme nejprve webové stránky ASP.NET. Začněte vytvořením nového webu souboru na základě systému technologie ASP.NET. K tomu, spusťte aplikaci Visual Web Developer a přejděte do nabídky soubor a vyberte nový web zobrazení dialogového okna Nový web. Výběr šablony webové stránky ASP.NET, nastavte rozevírací seznam umístění do systému souborů, zvolte složku, ve které umístíte na webu a nastavte jazyk na VB. Tím se vytvoří nový web s stránku Default.aspx ASP.NET, aplikace\_složka dat a v souboru Web.config.

> [!NOTE]
> Visual Studio podporuje dva režimy správy projektu: Webové projekty a projekty webových aplikací. Webové projekty chybí soubor projektu, že projekty webových aplikací napodobuje architekturu projektu v aplikaci Visual Studio .NET 2002/2003 – zahrnout soubor projektu a kompilaci zdrojového kódu v projektu do jednoho sestavení, který je umístěn ve složce/Bin. Visual Studio 2005 zpočátku pouze podporované projekty webů, i když s aktualizací Service Pack 1; byl znovuzavedeno modelu projektu webové aplikace Visual Studio 2008 nabízí oba modely projektu. Visual Web Developer 2005 a edice 2008, ale podporují pouze webové projekty. Můžu použijete model projektu webové stránky. Pokud používáte jiné Express edition a chcete použít [modelu projektu webové aplikace](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) místo toho můžete tak učinit, ale mějte na paměti, že mohou být některé nesrovnalosti mezi zobrazí na obrazovce a kroky musíte provést porovnání Zobrazí snímky obrazovky a pokyny uvedené v následujících kurzech.


[![Vytvoření nového souboru na základě systému webového serveru](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**Obrázek 02**: Vytvoření webu New File System-Based ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image6.png))


### <a name="adding-a-master-page"></a>Přidání stránky předlohy

V dalším kroku přidejte novou stránku předlohy v kořenovém adresáři s názvem Site.master k webu. [Stránky předlohy](https://msdn.microsoft.com/library/wtxbf3hh.aspx) umožňují vývojářům definovat šablony webu, který lze použít na stránky ASP.NET. Hlavní výhodou hlavní stránky je, že celkový vzhled lokality lze definovat na jednom místě, a tím vám usnadní aktualizovat nebo upravit rozložení tohoto webu.


[![Přidat stránku předlohy s názvem Site.master na web](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**Obrázek 03**: Přidat k webu hlavní stránku s názvem Site.master ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image9.png))


Definování rozložení stránky webu tady na hlavní stránce. Můžete použít zobrazení návrhu a přidat libovolné rozložení webové ovládací prvky nebo potřebujete, nebo můžete ručně přidat značky můžete rozšířit ručně v zobrazení zdroje. Můžu strukturované hlavní stránku rozložení tak, aby napodoboval rozložení používaných pro moje *[pracovat s daty v ASP.NET 2.0](../../data-access/index.md)* sérii (viz obrázek 4). Hlavní stránka používá [šablony stylů CSS](http://www.w3schools.com/css/default.asp) pro umístění a styly CSS nastavení definované v souboru Style.css (který je součástí přidruženého ke stažení v tomto kurzu). Zatímco nelze zjistit z kódu je uvedeno níže, se definují pravidla šablon stylů CSS tak, aby navigaci &lt;div&gt;jeho obsah je absolutně umístěné tak, aby se zobrazí na levé straně a má pevnou šířku 200 pixelů.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

Hlavní stránka definuje statickou stránku rozložení a oblasti, které lze upravovat pomocí stránek ASP.NET, které používají stránky předlohy. Tyto obsahu upravitelné oblasti jsou označeny ovládací prvek ContentPlaceHolder, který lze zobrazit v rámci obsahu &lt;div&gt;. Naší hlavní stránka má jeden prvek ContentPlaceHolder (MainContent), ale hlavní stránka může obsahovat několik prvků ContentPlaceHolder.

Se značkami výše ukazuje přepnutí na zobrazení návrhu rozložení stránky předlohy. Všechny stránky technologie ASP.NET, které pomocí této hlavní stránky bude mít toto jednotné rozložení s možností určit značky pro oblasti MainContent.


[![Stránky předlohy se stránkou, při zobrazení v okně návrhu](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**Obrázek 04**: stránku předlohy, při prohlížení prostřednictvím the návrhové zobrazení ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image12.png))


### <a name="creating-content-pages"></a>Vytváření obsahu stránek

V tuto chvíli máme stránku Default.aspx na našem webu, ale nepoužívá stránky předlohy, kterou jsme právě vytvořili. I když je možné k manipulaci s deklarativní webové stránky pro stránku předlohy, pokud na stránce neobsahuje žádný obsah zatím je snazší stačí stránku odstranit a znovu ji přidat do projektu, určení stránky předlohy k použití. Proto začněte tak, že odstraníte Default.aspx z projektu.

V dalším kroku klikněte pravým tlačítkem na název projektu v Průzkumníku řešení a zvolte Přidat nový webový formulář s názvem Default.aspx. Tentokrát zaškrtnout políčko vyberte stránky předlohy a stránky předlohy Site.master zvolte ze seznamu.


[![Přidejte novou stránku Default.aspx zvolíte-li vybrat hlavní stránku](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**Obrázek 05**: Přidat nové Default.aspx stránky zvolíte-li vybrat hlavní stránku ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image15.png))


[![Na stránce předlohy Site.master](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**Obrázek 06**: Na stránce předlohy Site.master ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image18.png))


> [!NOTE]
> Pokud použijete Model projektu webové aplikace neobsahuje dialogového okna Přidat novou položku zaškrtávací políčko Vybrat hlavní stránku. Místo toho budete muset přidat položku typu webový formulář obsahu. Visual Studio se zobrazí po výběru možnosti webový formulář obsahu a kliknutím na Přidat, vyberte stejný hlavní dialogové okno je znázorněno na obrázku 6.


Deklarativní novou stránku Default.aspx zahrnuje jenom @Page směrnice zadání cesty k hlavní stránce souboru a ovládací prvek obsahu MainContent ContentPlaceHolder stránky předlohy.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

Prozatím ponechejte Default.aspx prázdný. Vrátíme se k němu později v tomto kurzu přidáte obsah.

> [!NOTE]
> Naší hlavní stránky obsahuje oddíl pro nabídky nebo jiných rozhraní navigace. Vytvoříme toto rozhraní v budoucích kurzech.


## <a name="step-2-enabling-forms-authentication"></a>Krok 2: Povolení ověřování pomocí formulářů

S vytvořit web ASP.NET naše další úlohou je povolení ověřování pomocí formulářů. Konfigurace ověřování aplikace se specifikuje prostřednictvím [ &lt;ověřování&gt; element](https://msdn.microsoft.com/library/532aee0e.aspx) v souboru Web.config. &lt;Ověřování&gt; prvek obsahuje jeden atribut s názvem režim, který určuje model ověřování v aplikaci použít. Tento atribut může mít jednu z následujících čtyř hodnot:

- **Windows** – jak je popsáno v předchozím kurzu, pokud aplikace používá ověřování Windows zodpovídá za webový server k ověření návštěvníka, a to se obvykle provádí prostřednictvím Basic, Digest nebo integrované Windows ověřování.
- **Formuláře**-dojde k ověření uživatelů prostřednictvím formuláře na webové stránce.
- **Passport**-dojde k ověření uživatelů pomocí společnosti Microsoft Passport Network.
- **Žádný**-není použit žádný model ověřování; všechny návštěvníky jsou anonymní.

Aplikace ASP.NET ve výchozím nastavení, použijte ověřování Windows. Chcete-li změnit typ ověřování pro ověřování pomocí formulářů, pak musíme upravit &lt;ověřování&gt; atribut mode elementu do formulářů.

Pokud váš projekt zatím neobsahuje soubor Web.config, přidejte jeden nyní kliknutím pravým tlačítkem na název projektu v Průzkumníku řešení, vyberete Přidat novou položku a následným přidáním souboru webové konfigurace.


[![Pokud váš projekt zatím neobsahuje soubor Web.config, přidejte ji nyní](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**Obrázek 07**: Pokud váš projekt nemá není ještě zahrnují Web.config, přidejte ji nyní ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image21.png))


Dále vyhledejte &lt;ověřování&gt; elementu a aktualizovat ho na použití ověřování pomocí formulářů. Po této změně souboru Web.config značek by měl vypadat nějak takto:

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> Vzhledem k tomu, že soubor Web.config je soubor XML, je důležité velká a malá písmena. Ujistěte se, že, nastavte atribut mode do formulářů, s velkým F. Pokud používáte jinou velikostí písmen, jako jsou formuláře, obdržíte chybu konfigurace při návštěvě webu prostřednictvím prohlížeče.


&lt;Ověřování&gt; element může volitelně zahrnovat &lt;forms&gt; podřízený element, který obsahuje nastavení specifické pro ověřování pomocí formulářů. Teď použijeme výchozí nastavení ověřování formulářů. Se podíváme &lt;forms&gt; podřízený element podrobněji v dalším kurzu.

## <a name="step-3-building-the-login-page"></a>Krok 3: Vytváření přihlašovací stránky

Pro podporu ověřování pomocí formulářů našeho webu musí přihlašovací stránku. Jak je popsáno v vysvětlení části formuláře ověřovací pracovní postup FormsAuthenticationModule automaticky přesměruje uživatele na přihlašovací stránku Pokud pokus o přístup k stránku, která nejsou oprávnění k zobrazení. Existují také ovládacích prvků technologie ASP.NET, které se zobrazí odkaz na přihlašovací stránku pro anonymní uživatele. To si žádá na otázku, jaká je adresa URL přihlašovací stránky?

Ve výchozím nastavení systému ověřování formulářů očekává, že přihlašovací stránku s názvem Login.aspx a umístěné v kořenovém adresáři webové aplikace. Pokud chcete používat jiné přihlašovací adresu URL stránky, Uděláte to tak, že zadáte v souboru Web.config. Uvidíme, jak to udělat v následujícím kurzu.

Přihlašovací stránka má tři odpovědnosti:

1. Poskytují rozhraní, která umožňuje návštěvníka k zadání přihlašovacích údajů.
2. Určete, jestli zadané přihlašovací údaje jsou platné.
3. Přihlášení uživatele tak, že vytvoříte lístek ověřování formulářů.

### <a name="creating-the-login-pages-user-interface"></a>Vytvoření uživatelského rozhraní pro přihlašovací stránku

Pusťme se do práce s prvním úkolem. Přidejte novou stránku ASP.NET do kořenového adresáře webu s názvem Login.aspx a přidružte jej k hlavní stránce Site.master.


[![Přidejte novou stránku ASP.NET s názvem Login.aspx](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**Obrázek 08**: Přidat nové technologie ASP.NET stránky s názvem Login.aspx ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image24.png))


Typické přihlašovací stránky rozhraní se skládá z dvou textových polí – jeden pro uživatelské jméno, jeden pro svoje heslo – tlačítka a tlačítka Odeslat. Websites často zahrnují zapamatovat zaškrtávací políčko, pokud je zaškrtnuto, se uchovávají napříč prohlížeči restartování výsledný lístek ověřování.

Přidejte dvě textová pole stránce Login.aspx a nastavte jejich vlastnosti ID na uživatelské jméno a heslo, v uvedeném pořadí. Také vlastnost hesla v textovém režimu heslo. Dále přidejte ovládací prvek zaškrtávací políčko, nastavením jeho vlastnosti ID RememberMe a její vlastnost textu na Zapamatovat si mě. Pod přidejte tlačítko s názvem LoginButton, jejichž Text je nastavena na přihlášení. A nakonec přidání ovládacího prvku popisek a nastavte jeho vlastnost ID InvalidCredentialsMessage, její vlastnost textu na uživatelské jméno nebo heslo je neplatné. Zkuste to prosím znovu., jeho barva popředí vlastnost na hodnotu Red a jeho vlastnost Visible na hodnotu False.

V tomto okamžiku vaše obrazovka by měla vypadat podobně jako na obrázku 9 snímek obrazovky a vaše stránka deklarativní syntaxe by měl jako následující:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]


[![Na přihlašovací stránku obsahuje dvě textová pole, zaškrtávací políčko, tlačítko a popisek](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**Obrázek 09**: Přihlašovací stránku obsahuje dvě textová pole, zaškrtávací políčko, tlačítko a popisek ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image27.png))


Nakonec vytvořte obslužnou rutinu události pro kliknutí LoginButton událostí. Z Návrháře poklepejte na ovládací prvek tlačítka pro vytvoření této obslužné rutiny události.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>Určení, jestli zadané přihlašovací údaje jsou platné

Nyní potřebujeme k implementaci úkolu 2 kliknutím na tlačítko obslužná rutina události – určení, jestli zadané přihlašovací údaje jsou platné. Pokud to chcete udělat musí být úložiště uživatele, který obsahuje všechny přihlašovací údaje uživatelů, takže můžeme určit, pokud zadané přihlašovací údaje neodpovídají žádné známých přihlašovacích údajů.

Před ASP.NET 2.0 tým byl zodpovědný za implementace své vlastní úložiště uživatele a psaní kódu k ověření zadané přihlašovací údaje úložišti uživatelů, kteří vývojáři. Většina vývojářů by implementovat úložiště uživatele v databázi, vytvoření tabulky s názvem uživatelů se sloupci stejně jako uživatelské jméno, heslo, e-mailu, LastLoginDate a tak dále. Tuto tabulku a potom, má jeden záznam na uživatelský účet. Dotazování na databázi k vyhledání uživatelského jména a pak zajistit, že heslo v databázi odpovídaly zadané heslo by vyžadovalo ověřování zadané přihlašovací údaje uživatele.

S prostředím ASP.NET 2.0, vývojáři by měli používat jednu zprostředkovatelů členství spravovat úložiště uživatele. V této řadě kurzů použijeme SqlMembershipProvider, která používá databázi serveru SQL Server pro úložiště uživatelů. Při použití SqlMembershipProvider musíme implementovat konkrétní databázové schéma, které obsahuje tabulky, zobrazení a uložených procedur, byl očekáván zprostředkovatelem. Prozkoumáme jak implementovat v tomto schématu *[vytvoření schématu členství v SQL serveru](../membership/creating-the-membership-schema-in-sql-server-vb.md)* kurzu. U poskytovatele členství v místě, ověřují se přihlašovací údaje uživatele je stejně jednoduché jako volání funkce [třída členství](https://msdn.microsoft.com/library/system.web.security.membership.aspx)společnosti [ValidateUser (*uživatelské jméno*, *heslo*) Metoda](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx), která vrací logickou hodnotu označující, zda platnost *uživatelské jméno* a *heslo* kombinaci. Zjistíte, jak jsme dosud nebyla implementována SqlMembershipProvider uživatele v úložišti, jsme třída členství ValidateUser metodu nelze použít v tuto chvíli.

Spíše než je určitý čas věnovat vytváření naší vlastní uživatelé databázové tabulky (které bude zastaralé po jsme implementovali SqlMembershipProvider), můžeme místo pevně zakódovat platné přihlašovací údaje v rámci přihlašovací stránky samotný. LoginButton obslužné rutiny kliknutí, přidejte následující kód:

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

Jak je vidět, existují tři platné uživatelské účty – Scott, Jisun a Sam - a všechny tři mají stejné heslo (heslo). Kód prochází uživatelů a hesel pole hledání shody platné uživatelské jméno a heslo. Pokud jsou platné uživatelské jméno a heslo, musíme přihlásit uživatele a přesměruje je na příslušnou stránku. Pokud přihlašovací údaje jsou neplatné, zobrazíme InvalidCredentialsMessage popisek.

Když uživatel zadá platné přihlašovací údaje, jsem se zmiňoval, že se pak přesměrují na příslušnou stránku. Co je na příslušnou stránku, i když? Připomínáme, že když uživatel navštíví stránku, kterou uživatel nemá oprávnění k zobrazení, FormsAuthenticationModule automaticky ho přesměruje na přihlašovací stránku. Přitom obsahuje požadovanou adresu URL v řetězci dotazu pomocí parametr ReturnUrl. To znamená pokud uživatel se pokusil o navštivte ProtectedPage.aspx a nebyly autorizovány Uděláte to tak, FormsAuthenticationModule by přesměruje je na:

Login.aspx?ReturnUrl=ProtectedPage.aspx

Na úspěšně přihlášení, by měl být uživatel přesměrován zpět na ProtectedPage.aspx. Uživatelé také navštívit stránku pro přihlášení na své vlastní vůle. V takovém případě po přihlášení uživatele se odesílaných do kořenové složky stránku Default.aspx.

### <a name="logging-in-the-user"></a>Přihlášení uživatele

Za předpokladu, že zadané přihlašovací údaje jsou platné, potřebujeme vytvořit ověřovací lístek, a tím přihlášení uživatele k webu. [FormsAuthentication třídy](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) v [obor názvů System.Web.Security](https://msdn.microsoft.com/library/system.web.security.aspx) poskytuje různé metody pro protokolování v a odhlašování uživatelů prostřednictvím formulářů ověřovacího systému. Existuje několik metod ve třídě FormsAuthentication, jsou tři, kterými se v tomto okamžiku zajímat:

- [GetAuthCookie (*uživatelské jméno*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -vytvoří lístek ověřování formulářů pro zadaný název *uživatelské jméno*. V dalším kroku tato metoda vytvoří a vrátí objekt HttpCookie, který obsahuje obsah lístek ověřování. Pokud *persistCookie* má hodnotu True, je vytvoření trvalého souboru cookie.
- [SetAuthCookie (*uživatelské jméno*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) – zavolá GetAuthCookie (*uživatelské jméno*, *persistCookie*) Metoda ke generování souboru cookie pro ověřování pomocí formulářů. Tato metoda přidá soubor cookie vrácený GetAuthCookie do kolekce souborů cookie (za předpokladu, že ověřování pomocí formulářů na základě souborů cookie se používá; jinak vrátí hodnotu, tato metoda volá vnitřní třída, která zpracovává logiku bez souborů cookie lístek).
- [RedirectFromLoginPage (*uživatelské jméno*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) – tato metoda volá SetAuthCookie (*uživatelské jméno*, *persistCookie*) a pak přesměruje uživatele na příslušnou stránku.

GetAuthCookie je užitečné, když budete muset upravit lístek ověřování před zápisem souboru cookie do kolekce souborů cookie. SetAuthCookie je užitečné, pokud chcete vytvořit lístek ověřování formulářů a přidejte ho do kolekce souborů cookie, ale nechcete, aby přesměrovat uživatele na příslušnou stránku. Možná budete chtít zachovat na přihlašovací stránce nebo odeslání na některé alternativní stránku.

Protože chceme přihlásit uživatele a přesměruje je na příslušnou stránku, použijeme RedirectFromLoginPage. Aktualizujte kliknutím LoginButton obslužná rutina události, nahraďte dva řádky komentářů TODO následující řádek kódu:

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked)

Při vytváření lístku ověřování formulářů používáme vlastnost Text textového pole uživatelské jméno pro lístek ověřování pomocí formulářů *uživatelské jméno* parametr a stavu zaškrtnutí políčka RememberMe  *persistCookie* parametru.

Otestovat stránku pro přihlášení, najdete ji v prohlížeči. Začněte tak, že zadáte neplatné přihlašovací údaje, jako je například Nope uživatelské jméno a heslo nesprávné. Po klepnutí na tlačítka pro přihlášení zpětného odeslání dojde a zobrazí se popisek InvalidCredentialsMessage.


[![InvalidCredentialsMessage popisek se zobrazí při zadávání neplatné přihlašovací údaje](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**Obrázek 10**: InvalidCredentialsMessage popisek se zobrazí při zadávání neplatné přihlašovací údaje ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image30.png))


Dále zadejte platné přihlašovací údaje a klikněte na tlačítko pro přihlášení. Tentokrát při výskytu postback lístek ověřování formulářů se a budete automaticky přesměrováni zpět na stránku Default.aspx. V tomto okamžiku jste byli přihlášeni k webu, i když neexistují žádné vizuálních podnětů k označení, že jste aktuálně přihlášeni. V kroku 4, uvidíme, jak prostřednictvím kódu programu určit, jestli uživatel přihlášen v nebo není a také jak k identifikaci uživatele na stránce.

Krok 5 prozkoumá techniky pro protokolování uživatele z webu.

### <a name="securing-the-login-page"></a>Zabezpečení na přihlašovací stránce

Když uživatel zadá své přihlašovací údaje a přihlašovací stránky formulář odešle, přenosu přihlašovacích údajů – včetně své heslo – přes Internet na webový server v *prostý text*. To znamená, že všechny kyberzločinci pro analýzu sítě síťový provoz můžete zobrazit uživatelské jméno a heslo. Chcete-li tomu zabránit, je nezbytné k šifrování síťového provozu s využitím [vrstvy SSL (Secure Socket)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer). Tím se zajistí, že jsou zašifrované přihlašovací údaje (stejně jako značka jazyka HTML celé stránky) od okamžiku, kdy nechají prohlížeč, dokud nedorazí k příjemci webový server.

Pokud váš web neobsahuje citlivé informace, musíte se pouze na používání protokolu SSL na přihlašovací stránce a na jiných stránkách, kde heslo uživatele by se odeslaly jinak přenosu ve formátu prostého textu. Nemusíte se obávat o zabezpečení formuláře lístek ověřování, protože ve výchozím nastavení, je i šifrovaný a digitálně podepsané (Chcete-li zabránit manipulaci). V následujícím kurzu se zobrazí podrobnější informace týkající se zabezpečení lístek ověřování formulářů.

> [!NOTE]
> Mnohé weby finančních a lékařské jsou nakonfigurovány pro použití protokolu SSL na *všechny* stránky přístupné pro ověřené uživatele. Pokud sestavujete web, systém ověřování formulářů můžete nakonfigurovat tak, aby ověřovací lístek přenášena pouze prostřednictvím zabezpečeného připojení. V dalším kurzu se podíváme na různé možnosti konfigurace ověřování formulářů  *[konfigurace ověřování formulářů a témata pokročilé](../membership/creating-the-membership-schema-in-sql-server-vb.md)*.


## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>Krok 4: Zjišťování ověřeného návštěvníci a určení Identity

V tuto chvíli jsme povolili jste ověřování pomocí formulářů a vytvoří základní přihlašovací stránku, ale musíme ještě prozkoumejte, jak můžete určíme, zda je uživatel ověřený nebo anonymní. V některých případech může chceme zobrazit jiná data nebo informace v závislosti na tom, zda je ověřený nebo anonymní uživatel navštívit stránky. Kromě toho často potřebujeme znát identitu ověřeného uživatele.

Můžeme rozšířit existující stránku Default.aspx pro ilustraci těchto technik. V Default.aspx přidejte dva ovládací prvky Panel, jednu s názvem AuthenticatedMessagePanel a jiné pojmenované AnonymousMessagePanel. Přidejte ovládací prvek popisek s názvem WelcomeBackMessage v prvním panelu. V druhém panelu Přidat ovládací prvek hypertextového odkazu, nastavte její vlastnost textu na přihlásit a jeho vlastnost NavigateUrl na ~ / Login.aspx. Deklarativní Default.aspx v tomto okamžiku by měl vypadat nějak takto:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

Jak budete mít pravděpodobně uhodnout nyní, cílem zde je se budou zobrazovat jenom AuthenticatedMessagePanel ověřeného návštěvníci a právě AnonymousMessagePanel návštěvníkům anonymní. K tomu potřebujeme k nastavení těchto panelů viditelné vlastnosti v závislosti na tom, jestli je uživatel přihlášen či nikoli.

[Request.IsAuthenticated vlastnost](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) vrátí logickou hodnotu označující, zda žádost o ověření. Zadejte následující kód do stránky\_načíst kód obslužné rutiny události:

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

S tímto kódem na místě navštivte Default.aspx prostřednictvím prohlížeče. Za předpokladu, že ještě nemáte pro přihlášení, zobrazí se odkaz na stránku pro přihlášení (viz obrázek 11). Kliknutím na tento odkaz a přihlaste se k webu. Jak jsme viděli v kroku 3, po zadání přihlašovacích údajů budete přesměrováni zpět na stránku Default.aspx, ale tentokrát zobrazuje na stránce Vítejte zpátky! zprávy (viz obrázek 12).


[![Při návštěvě anonymně, protokolu v odkazu se zobrazí](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**Obrázek 11**: Při návštěvě anonymně, zobrazí se v odkazu protokolu ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image33.png))


[![Ověření uživatelé jsou uvedeny Vítejte zpátky! Zpráva](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**Obrázek 12**: Ověření uživatelé jsou uvedeny Vítejte zpátky! Zpráva ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image36.png))


Můžeme určit identitu aktuálně přihlášeného uživatele prostřednictvím [objektu HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)společnosti [vlastnosti uživatele](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx). Objektu HttpContext představuje informace o aktuálním požadavku a je domovská stránka pro takové běžně používané objekty technologie ASP.NET jako odpovědí, žádost a relace, mimo jiné. Představuje kontext zabezpečení aktuální požadavek HTTP a implementuje vlastnost uživatele [rozhraní IPrincipal](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx).

Vlastnost uživatele se nastavil FormsAuthenticationModule. Když FormsAuthenticationModule vyhledá lístek ověřování formulářů v příchozím požadavku, konkrétně vytvoří nový objekt objektů GenericPrincipal a přiřadí vlastnosti uživatele.

Instanční objekty (třeba GenericPrincipal) poskytují informace o identitu uživatele a role, do kterých patří. Rozhraní IPrincipal definuje dva členy:

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) – metodu, která vrátí hodnotu typu Boolean označující, zda objekt zabezpečení patří do zadané role.
- [Identita](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) – vlastnost, která vrací objekt, který implementuje [IIdentity rozhraní](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx). IIdentity rozhraní definuje tři vlastnosti: [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [ověření identity](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx), a [název](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx).

Můžeme určit název aktuální návštěvníka pomocí následujícího kódu:

Dim currentUsersName As String = User.Identity.Name

Při ověřování pomocí formulářů [FormsIdentity objektu](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) pro vlastnost Identity GenericPrincipal se vytvoří. Třída FormsIdentity vždy vrací řetězec formuláře pro jeho vlastnost AuthenticationType a hodnotu True pro jeho vlastnost ověření identity. Vlastnost Name vrátí uživatelské jméno zadané při vytváření lístku ověřování formulářů. Kromě tyto tři vlastnosti FormsIdentity zahrnuje přístup k základní lístek ověřování prostřednictvím jeho [lístku podpory vlastnost](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx). Vrátí objekt typu vlastnosti Ticket [FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx), který má vlastnosti, jako je vypršení platnosti, IsPersistent, IssueDate, název a tak dále.

Důležité odnést zde je, že *uživatelské jméno* parametr zadaný v FormsAuthentication.GetAuthCookie (*uživatelské jméno*, *persistCookie*), FormsAuthentication.SetAuthCookie (*uživatelské jméno*, *persistCookie*) a FormsAuthentication.RedirectFromLoginPage (*uživatelské jméno*, *persistCookie*) metody je stejná jako hodnota vrácený User.Identity.Name. Lístek ověřování, které jsou vytvořené pomocí těchto metod je navíc k dispozici přetypování User.Identity FormsIdentity objektu a pak přístup k vlastnosti Ticket:

Dim ident As FormsIdentity = CType(User.Identity, FormsIdentity)

Dim authTicket jako FormsAuthenticationTicket = ident. Lístek

Umožňuje zadat zprávu vyšší míra personalizace v Default.aspx. Aktualizujte stránku\_načíst obslužnou rutinu události tak, aby vlastnost textu popisku WelcomeBackMessage se přiřadí řetězec Vítejte zpět, *uživatelské jméno*!

WelcomeBackMessage.Text = "Vítejte zpět," &amp; User.Identity.Name &amp; "!"

Obrázek 13 demonstruje účinek této změny (při přihlášení se jako uživatel Scott).


[![Zobrazení uvítací zprávy zahrne aktuálně přihlášeného uživatelského jména](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**Obrázek 13**: Uvítací zpráva obsahuje aktuálně zaznamenána v uživatelské jméno ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image39.png))


### <a name="using-the-loginview-and-loginname-controls"></a>Pomocí prvku LoginView a LoginName ovládacích prvků

Zobrazení rozdílný obsah ověřený a anonymním uživatelům je běžné požadavky; Proto se zobrazuje název aktuálně přihlášeného uživatele. Z tohoto důvodu technologie ASP.NET obsahuje dva webové ovládací prvky, které poskytují stejné funkce uvedené na obrázku 13, ale bez nutnosti napsat jediný řádek kódu.

[Ovládacího prvku LoginView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) je založené na šablonách webové ovládací prvek, který umožňuje snadno zobrazit jiná data ověřený a anonymním uživatelům. Prvku LoginView obsahuje dvě předdefinované šablony:

- AnonymousTemplate – všechny značky, přidat do této šablony se zobrazí jenom anonymní návštěvníků.
- LoggedInTemplate - značek této šablony se zobrazí pouze ověřeným uživatelům.

Přidáme náš web stránku předlohy, Site.master ovládacího prvku LoginView. Místo přidávání pouze ovládacího prvku LoginView, ale přidáme i nový prvek ContentPlaceHolder a potom se spojí ovládacího prvku LoginView v rámci tohoto nového ContentPlaceHolder. Důvody pro toto rozhodnutí se stanou zjevnými za chvíli.

> [!NOTE]
> Kromě AnonymousTemplate a LoggedInTemplate může zahrnovat ovládacího prvku LoginView šablony pro konkrétní role. Kód šablony pro konkrétní role zobrazit pouze pro uživatele, kteří patří do zadané role. Funkce ovládacího prvku LoginView na základě rolí prozkoumáme v budoucích kurzech.


Začněte přidáním ContentPlaceHolder na hlavní stránku v rámci navigace s názvem LoginContent &lt;div&gt; elementu. Ovládací prvek ContentPlaceHolder může jednoduše přetáhněte z panelu nástrojů do zobrazení zdroje, uvedení výsledný kód přímo nad TODO: Nabídka tady bude text.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

Dále přidejte ovládací prvek zobrazení přihlášení v rámci LoginContent ContentPlaceHolder. Jsou považovány za obsah umístí do ovládacích prvků ContentPlaceHolder na hlavní stránce *výchozí obsah* pro ContentPlaceHolder. Stránky technologie ASP.NET, které používají tuto stránku předlohy to znamená, můžete zadat vlastní obsah pro každý prvek ContentPlaceHolder nebo použít výchozí obsah stránky předlohy.

Zobrazení přihlášení a další související s přihlášením ovládací prvky jsou umístěny v přihlášení kartu panelu nástrojů.


[![Ovládacího prvku LoginView na panelu nástrojů](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**Obrázek 14**: Ovládacího prvku LoginView na panelu nástrojů ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image42.png))


V dalším kroku přidejte dva &lt;br /&gt; prvky ihned po ovládacího prvku LoginView, ale pořád se nachází v ContentPlaceHolder. V tomto okamžiku navigace &lt;div&gt; elementu značek by měl vypadat nějak takto:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

Z Návrháře nebo deklarativní lze definovat LoginView šablony. Z návrháře aplikace Visual Studio rozbalte zobrazení přihlášení inteligentní značky, který obsahuje seznam nakonfigurované šablony v rozevíracím seznamu. Zadejte text Hello, cizím do AnonymousTemplate; v dalším kroku přidejte ovládací prvek hypertextového odkazu a nastavit jeho vlastnosti Text a NavigateUrl pro přihlášení a ~ / Login.aspx, v uvedeném pořadí.

Po dokončení konfigurace AnonymousTemplate, přepněte LoggedInTemplate a zadejte text, "Vítejte zpět,". Přetáhněte ovládací prvek přihlašovacího jména ze sady nástrojů do LoggedInTemplate, že ho umístíte bezprostředně po "Vítejte zpět," textu. [Prvek přihlašovacího jména](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx), již jako její název napovídá, zobrazí jméno aktuálně přihlášeného uživatele. Interně jednoduše prvek přihlašovacího jména výstupy vlastnost User.Identity.Name

Po provedení těchto dodatky k prvku LoginView šablony, značky by měl vypadat nějak takto:

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

Tato uveďte na hlavní stránku Site.master každá stránka v našem webu se zobrazí různé zprávy v závislosti na tom, jestli je uživatel ověřený. Obrázek 15 zobrazuje stránku Default.aspx při návštěvě uživatele Jisun prostřednictvím prohlížeče. Vítejte zpět, Jisun dvakrát opakuje zpráva: jednou v části navigace stránky předlohy na levé straně (prostřednictvím ovládacího prvku LoginView jsme právě přidali) a jednou v Default.aspx obsahu oblasti (přes ovládací prvky panelu a programovou logiku).


[![LoginView ovládací prvek zobrazí Vítejte zpět Jisun.](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**Obrázek 15**: LoginView ovládací prvek zobrazí Vítejte zpět Jisun. ([Kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image45.png))


Protože LoginView jsme přidali na stránku předlohy, může se objevit v každé stránky na našem webu. Nicméně mohou existovat webové stránky kde nechceme zobrazit tato zpráva. Jeden takový stránky je na přihlašovací stránku, protože odkaz na přihlašovací stránku zdá se, že mimo místo existuje. Protože jsme umístili ovládacího prvku LoginView ContentPlaceHolder na stránce předlohy, jsme naši stránku obsahu přepsat tato výchozí značka. Otevřete Login.aspx a přejděte do návrháře. Protože jsme nejsou explicitně definovány ovládací prvek obsahu v Login.aspx pro LoginContent ContentPlaceHolder na stránce předlohy, přihlašovací stránky se zobrazí na hlavní stránce výchozí značky pro tento prvek ContentPlaceHolder. Zobrazí se to prostřednictvím návrháře - LoginContent ContentPlaceHolder ukazuje výchozí značky (ovládacího prvku LoginView).


[![Přihlašovací stránky zobrazí výchozí obsahu pro LoginContent ContentPlaceHolder na stránce předlohy](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**Obrázek 16**: Přihlašovací stránky zobrazí výchozí obsah pro LoginContent ContentPlaceHolder na stránce předlohy ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image48.png))


K přepsání pro LoginContent ContentPlaceHolder výchozí značky, jednoduše klikněte pravým tlačítkem na oblast v návrháři a zvolte možnost vytvořit vlastní obsah v místní nabídce. (Když pomocí sady Visual Studio 2008 ContentPlaceHolder zahrnuje smart značek, které, pokud je vybráno, nabízí stejná možnost.) Tím se přidá nový prvek obsahu pro na stránce značek a tím současně umožňuje definovat vlastní obsah pro tuto stránku. Může přidat vlastní zprávu, jako je například Přihlaste se, ale teď právě toto pole nechat prázdné.

> [!NOTE]
> V sadě Visual Studio 2005, vytváření vlastního obsahu vytvoří prázdnou obsah ovládacího prvku do stránky ASP.NET. V sadě Visual Studio 2008 ale vytváření vlastního obsahu zkopíruje obsah výchozí stránky předlohy do nově vytvořený ovládací prvek obsahu. Pokud používáte Visual Studio 2008, pak po vytvoření nového obsahu ovládacího prvku Ujistěte se, že chcete vymazat obsah zkopíruje ze stránky předlohy.


Obrázek 17 ukazuje na stránku Login.aspx, když uživatel přejde v prohlížeči po provedení této změny. Všimněte si, že neexistuje žádný dobrý den, cizím nebo vás vítá zpět *uživatelské jméno* zprávy v levém navigačním panelu &lt;div&gt; jako v případě navštívit Default.aspx.


[![Na přihlašovací stránku skryje LoginContent ContentPlaceHolder výchozí značky](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**Obrázek 17**: Na přihlašovací stránku skryje výchozí LoginContent ContentPlaceHolder jeho značky ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image51.png))


## <a name="step-5-logging-out"></a>Krok 5: Odhlášení

V kroku 3 jsme se podívali na vytváření přihlašovací stránku pro přihlášení uživatele v lokalitě, ale máme ještě se dozvíte, jak se odhlásit uživatele. Kromě metod pro uživatele v protokolování FormsAuthentication třída rovněž poskytuje [metody SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx). Metody SignOut jednoduše zničí lístek ověřování pomocí formulářů, a tím odhlášení uživatele mimo lokalitu.

Nabídka odhlášení odkaz je běžnou funkcí této technologie ASP.NET obsahuje ovládací prvek speciálně pro odhlášení uživatele. [Ovládací prvek stavu přihlášení](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) zobrazí LinkButton přihlášení nebo odhlášení LinkButton, v závislosti na stavu ověřování uživatele. LinkButton přihlášení je vykreslen pro anonymní uživatele, že LinkButton odhlášení se zobrazí ověřeným uživatelům. Text pro přihlášení a odhlášení LinkButtons můžete nakonfigurovat přes stavu přihlášení LoginText a LogoutText vlastnosti.

Kliknutí na prvek LinkButton přihlášení způsobí, že zpětné volání, ze kterého je vydaný přesměrování na přihlašovací stránku. Kliknutí na prvek LinkButton odhlášení způsobí, že ovládací prvek stavu přihlášení k vyvolání metody FormsAuthentication.SignOff a pak přesměruje uživatele na stránku. Na stránce přihlášeného vypnout uživatel se přesměruje na závisí na vlastnost LogoutAction, které můžete přiřadit na jednu ze tří následujících hodnot:

- Aktualizace – výchozí hodnota; přesměruje uživatele na stránku, kterou právě navštívit. Pokud stránku, kterou právě navštívit nedovoluje anonymní uživatele, pak FormsAuthenticationModule automaticky přesměruje uživatele na přihlašovací stránku.

Je možné zajímá vás, proč se zde provádí přesměrování. Pokud uživatel chce zůstat na stejné stránce, proč potřebu explicitní přesměrování? Důvodem je, protože při kliknutí na prvek LinkButton odhlášení uživatele obsahuje ověřovací lístek v jejich kolekce souborů cookie. V důsledku toho se žádosti o postback ověřeného požadavku. Ovládací prvek stavu přihlášení volá metody SignOut, ale, který se stane po FormsAuthenticationModule ověření uživatele. Proto explicitní přesměrování způsobí, že prohlížeč, aby znovu požádat o stránce. Podle času prohlížeč znovu požaduje na stránce byla odebrána ověřovací lístek a proto je k anonymní příchozího požadavku.

- Přesměrování - uživatel je přesměrován na adrese URL zadané hodnotou vlastnosti LogoutPageUrl stavu přihlášení.
- RedirectToLoginPage – uživatel se přesměruje na přihlašovací stránku.

Pojďme přidat ovládací prvek stavu přihlášení k hlavní stránce a nakonfigurujte ho na použití možnost přesměrování pro uživatele poslat na stránku, která se zobrazí se zpráva s potvrzením, že jejich odhlášení bylo úspěšné. Začněte tím, že v kořenovém adresáři s názvem Logout.aspx vytvoření stránky. Nezapomeňte si tuto stránku přidružit Site.master stránky předlohy. Pak zadejte zprávu v kódu stránky vysvětlující uživateli, který byl odhlášen.

V dalším kroku zpět na hlavní stránku Site.master a přidejte ovládací prvek stavu přihlášení pod LoginView v LoginContent ContentPlaceHolder. Nastavte vlastnost LogoutAction ovládací prvek stavu přihlášení přesměrování a jeho vlastnost LogoutPageUrl na ~/Logout.aspx.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

Stavu přihlášení je mimo ovládací prvek zobrazení přihlášení, se zobrazí pro anonymní i ověřené uživatele, ale to nevadí vzhledem k tomu, stavu přihlášení se zobrazí správně přihlášení nebo odhlášení odkazem (LinkButton). Uveďte ovládací prvek stavu přihlášení protokolu v hypertextový odkaz AnonymousTemplate je nadbytečný, takže jej odebrat.

Obrázek 18 zobrazuje Default.aspx, když navštíví Jisun. Všimněte si, že v levém sloupci zobrazí zprávu, Vítejte zpět, Jisun spolu s odkazem na odhlášení. Kliknutím na odhlášení odkazem (LinkButton) vyvolá zpětné volání, podepíše Jisun přístup do systému a přesměruje jí Logout.aspx. Jak ukazuje obrázek 19, v době, kdy Jisun dosáhne Logout.aspx, která již byl podepsán navýšení kapacity a proto je anonymní. V důsledku toho v levém sloupci zobrazí text Uvítacího cizím a odkaz na přihlašovací stránku.


[![Vítejte zpět, Jisun spolu odkazem (LinkButton) odhlášení ukazuje default.aspx](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**Obrázek 18**: Default.aspx ukazuje Vítejte zpět, Jisun spolu s LinkButton odhlášení ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image54.png))


[![Logout.aspx ukazuje úvodní, cizím spolu odkazem (LinkButton) přihlášení](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**Obrázek 19**: Logout.aspx ukazuje úvodní, cizím spolu s přihlašovací LinkButton ([kliknutím ji zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-vb/_static/image57.png))


> [!NOTE]
> Neváhejte se přizpůsobit stránce Logout.aspx skrýt LoginContent ContentPlaceHolder stránky předlohy (jak jsme to udělali pro Login.aspx v kroku 4). Důvodem je to proto, že přihlášení LinkButton generovány ovládací prvek stavu přihlášení (ten pod text Hello, cizím) odešle uživatele na přihlašovací stránku předáním aktuální adresy URL v parametru querystring ReturnUrl. Stručně řečeno pokud uživatel, který je odhlášen kliknutí odkazem (LinkButton) tohoto stavu přihlášení přihlášení a pak přihlásí, že budete přesměrováni zpět na Logout.aspx, který může snadno zmást uživatele.


## <a name="summary"></a>Souhrn

V tomto kurzu budeme pracovat s prozkoumání workflowu ověřování formulářů a pak ji vypnuli k implementaci ověřování pomocí formulářů v aplikaci technologie ASP.NET. Ověřování pomocí formulářů využívá k tomu FormsAuthenticationModule, který má dva odpovědnosti: identifikace uživatelů podle jejich lístek ověřování pomocí formulářů a přesměrování na přihlašovací stránku neoprávnění uživatelé.

Rozhraní .NET Framework FormsAuthentication třída obsahuje metody pro vytváření, kontrolu a odstranění lístků pro ověřování pomocí formulářů. Vlastnost Request.IsAuthenticated a objekt uživatele poskytovat další podporu prostřednictvím kódu programu k určení, zda je žádost o ověření a informace o identitě uživatele. Existují také LoginView, stavu přihlášení a LoginName webové ovládací prvky, které dávají vývojářům tak rychle a bez kódu pro provádění mnoha běžných úkolů související s přihlášením. Prozkoumáme tyto a další související s přihlášením webové ovládací prvky podrobněji v budoucích kurzech.

Tento kurz poskytuje zběžné Přehled ověřování pomocí formulářů. Jsme není podívejte se na možnosti různé konfigurace, podívejte se na jak cookieless pracovní lístky ověřování formulářů nebo prozkoumat, jak ASP.NET chrání obsah lístek ověřování pomocí formulářů. Pojednává o těchto tématech a další funkce do [další kurz](forms-authentication-configuration-and-advanced-topics-vb.md).

Všechno nejlepší programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech, které jsou popsané v tomto kurzu najdete na následujících odkazech:

- [Změny mezi IIS6 a zabezpečení služby IIS7](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Přihlašovací ovládací prvky ASP.NET](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Profesionální ASP.NET 2.0 zabezpečení, členství a rolí správy](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [&lt;Ověřování&gt; – Element](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;Forms&gt; – Element pro &lt;ověřování&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Video od Pluralsightu na témata, které jsou obsažené v tomto kurzu

- [Použití ověřování založeného na základních formulářích v ASP.NET](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>O autorovi

Scott Meisnerová, Autor více ASP/ASP.NET knih a zakladatelem 4GuysFromRolla.com, má pracovali Microsoft webových technologiích od roku 1998. Scott funguje jako nezávislý konzultant, trainer a zapisovače. Jeho nejnovější knihy  *[Edice nakladatelství Sams naučit sami ASP.NET 2.0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott může být dostupný na adrese [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím na svém blogu [ http://ScottOnWriting.NET ](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Speciální k

V této sérii kurzů byl recenzován uživatelem mnoho užitečných revidující. Vedoucí revidující pro účely tohoto kurzu zahrnují Alicja Maziarz, Jan Suru a Teresy Murphy. Zajímat téma Moje nadcházejících článcích MSDN? Pokud ano, vyřaďte mě řádek na [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com).

> [!div class="step-by-step"]
> [Předchozí](security-basics-and-asp-net-support-vb.md)
> [další](forms-authentication-configuration-and-advanced-topics-vb.md)
