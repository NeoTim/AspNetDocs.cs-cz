---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET a webové nástroje 2013.2 pro poznámky k verzi sady Visual Studio 2013 | Dokumenty společnosti Microsoft
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543623"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET a webové nástroje 2013.2 pro Visual Studio 2013 – poznámky k verzi

podle [společnosti Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET a webové nástroje pro Visual Studio 2013.2 jsou součástí hlavního instalačního programu a lze je stáhnout jako součást [aktualizace Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521).

## <a name="documentation"></a>Dokumentace

Výukové programy a další informace o ASP.NET a webových nástrojích pro visual studio 2013.2 jsou k dispozici na [webu ASP.NET](https://www.asp.net/).

## <a name="software-requirements"></a>Požadavky na software

ASP.NET a webové nástroje pro Visual Studio 2013.2 vyžaduje Visual Studio 2013.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Nové funkce v ASP.NET a webových nástrojích pro Visual Studio 2013.2

Následující části popisují funkce, které byly zavedeny ve verzi.

- [Jedna ASP.NET šablon projektů](#oneaspnet)
- [Podpora ssl při spouštění webových aplikací ve službě IIS Express](#ssl)
- [Vylepšení webového editoru sady Visual Studio](#vswebeditor)
- [Browser Link](#browserlink)
- [Podpora webových aplikací služby Azure App Service ve Visual Studiu](#waws)
- [Vytvoření vzdálených prostředků Azure při vytváření nového webového projektu](#AzureResources)
- [Vylepšení publikování webu](#webpublish)
- [ASP.NET lešení](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET – webové formuláře](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET webové rozhraní API 2.1.2](#webapi)
- [ASP.NET webové stránky 3.1.2](#webpages)
- [Účetní rámec 6.1](#ef)
- [ASP.NET identita 2.0.0](#identity)
- [Součásti Microsoft OWIN](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Jedna ASP.NET šablon projektů

- Aktualizace ASP.NET šablon projektu pro podporu potvrzení účtu a resetování hesla.
- Aktualizace ASP.NET šablonu webového rozhraní API pro podporu ověřování pomocí místních organizačních účtů.
- Šablona ASP.NET SPA nyní obsahuje ověřování, které je založeno na zobrazeních na straně mvc a serveru. Šablona má řadič WebAPI, ke kterému mají přístup pouze ověření uživatelé.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>Podpora ssl při spouštění webových aplikací ve službě IIS Express

Abychom odstranili upozornění zabezpečení při procházení a ladění protokolu HTTPS na localhost, přidali jsme dialogové okno, které umožňuje aplikaci Internet Explorer a Chromu důvěřovat certifikátu SSL express služby IIS podepsanému svým držitelem.

Například vlastnost webového projektu lze nastavit na použití SSL. Klepnutím na tlačítko F4 zobrazíte dialogové okno vlastností. Změnit **SSL Povoleno** na true. Zkopírujte adresu URL SSL.

![Vlastnost s povolenou protokolem SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Nastavte webovou kartu stránky vlastností webového projektu tak, aby `https://localhost:44300/` používala adresu URL založenou na protokolu HTTPS (Adresa URL SSL bude, pokud jste dříve nevytvořili webové servery SSL.)

![Nastavení adresy URL projektu (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Podle pokynů důvěřujte certifikátu podepsanému svým držitelem, který vygenerovala služba IIS Express.

![Upozornění SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Přečtěte si dialogové okno **Upozornění zabezpečení** a klepněte na tlačítko **Ano,** pokud chcete nainstalovat certifikát představující localhost.

![Bezpečnostní upozornění](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Stránky se zobrazí v IE nebo Chrome bez upozornění na certifikát v prohlížeči.

![Stránka HTTPS bez varování](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Vylepšení webového editoru sady Visual Studio

- **Nová položka a editor projektu JSON**: Do sady Visual Studio jsme přidali položku a editor projektu JSON. Aktuální funkce editoru JSON zahrnují vybarvení, ověření syntaxe, dokončení složených závorek, osnovu, nastavení možností nástrojů a další.

    ![JSON Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    Technologie IntelliSense nyní podporuje [schema JSON](http://json-schema.org/) v3 a v4. Existuje pole se seznamem schémat, které umožňuje zvolit existující schémata, upravit cestu místního schématu nebo jednoduše přetáhnout soubor JSON projektu, abyste získali relativní cestu.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![Editor schématu JSON](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Nový editor Sass (SCSS):** Přidali jsme LESS v VS2013 RTM a nyní máme položku a editor projektu Sass. Funkce editoru Sass jsou srovnatelné s editorem LESS a zahrnují zbarvení, proměnné a Mixins IntelliSense, komentář / komentář, rychlé informace, formátování, ověření syntaxe, osnovu, definici goto, výběr barev, nastavení možností nástrojů atd.

    ![Přidat novou položku: Šablona stylů SCSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Editor šablon stylů](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **Nový výběr adres URL v dokumentech HTML, Razor, CSS, LESS a Sass:** VS 2013 dodáván bez výběru adres URL mimo stránky webových formulářů. Nový výběr adres URL pro editory HTML, Razor, CSS, LESS a Sass je dialog-free, plynulý výběr psaní, který rozumí '.. a filtruje seznamy souborů vhodně pro img značky a odkazy.

    ![Výběr adresy URL pro značku obrázku](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Výběr adres URL pro zobrazení](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![Výběr adres URL pro CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Aktualizace editoru LESS přidáním dalších funkcí**
- **Knockout Intellisense Upgrade**: Přidali jsme nestandardní knockout syntaxi pro VS intelliSense, "ko-vs-editor viewModel:" syntaxe. Lze jej použít k vytvoření vazby na více modelů zobrazení na stránce pomocí komentářů ve formuláři:

    ![Vyřazovací technologie Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Přidali jsme také podporu pro vnořené ViewModel IntelliSense, takže můžete přejít k podrobnostem do hluboce vnořené objekty na ViewModel.

    `<div data-bind="text: foo.bar.baz.etc" />`

    Zobrazená technologie IntelliSense je úplná technologie IntelliSense objektu JavaScript.

    ![Intellisense zobrazující úplný objekt JavaScriptu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **Nový výběr adres URL v dokumentech HTML, Razor, CSS, LESS a Sass**: VS 2013 byl dodán bez výběru adres URL mimo stránky webových formulářů. Nový výběr adres URL pro editory HTML, Razor, CSS, LESS a Sass je dialog-free, plynulý výběr psaní, který rozumí '.. a filtruje seznamy souborů vhodně pro img značky a odkazy.

    ![Výběr adresy URL pro značku obrázku](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Výběr adres URL pro zobrazení](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![Výběr adres URL pro CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Browser Link

- Odkaz prohlížeče nyní podporuje připojení HTTPS a zobrazí seznam, který v řídicím panelu s jinými připojeními, pokud je certifikát důvěryhodný prohlížečem.
- Statické mapování zdrojů HTML
- Spa podpora pro mapování dat
- Automatická aktualizace mapových dat

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Podpora webových aplikací služby Azure App Service ve Visual Studiu

- **Podporujte přihlášení k Azure.**
- **Vzdálené ladění a vzdálené zobrazení pro webové aplikace**: Teď podporujeme vzdálené ladění [webových aplikací ve službě Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) a vzdálené zobrazení souborů obsahu webových aplikací v průzkumníku serveru.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Vytvoření vzdálených prostředků Azure při vytváření nového webového projektu

Do nového dialogového okna webové aplikace jsme přidali zaškrtávací políčko Azure ["Vytvořit vzdálené prostředky".](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) Výběrem ji budete moci integrovat prostředí vytváření nové webové aplikace, nastavení webu publikování Azure pro testování a vytvoření profilu publikování v několika jednoduchých krocích.

![Nový projekt s prostředky Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Publikování do Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Vylepšení publikování webu

- Zlepšete uživatelské prostředí pro publikování.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET lešení

- **Podpora enum:** Pokud váš model používá výčty, pak MVC scaffolder vygeneruje rozevírací seznam pro výčtu. To používá pomocné položky výčtu v MVC.
- **Bootstrap podpora:** Aktualizováno EditorFor šablony v MVC scaffolding tak, aby používaly Bootstrap třídy.
- **Podpora balíčků**: Složky MVC a Web API přidají balíčky 5.1 pro MVC a web API

Následující snímky obrazovky ukazují modely lešení.

- Kód modelu:

     ![Kód modelu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Zkompilujte kód modelu, klepněte pravým tlačítkem myši a vyberte **přidat**, **Novou položku scaffolded .**

     ![Přidat novou položku scaffolded](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- Zvolte **řadič MVC5 se zobrazeními pomocí entity Framework**:

     ![Přidání nového ovladače MVC5 se zobrazeními](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **Přidat řadič** pomocí modelu:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Zkontrolujte generovaný kód, například Zobrazení/WeekdayModels/Edit.cshtml obsahuje `@Html.EnumDropDownListFor`: ![Zobrazení obsahující EnumDropDownListFor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- Spusťte stránku zobrazíte výčet combobox generované, všimněte si, že pokud hodnota může být null, prázdný řetězec lze zvolit pro pole se seznamem. Například stránka **Vytvořit** zobrazuje následující:

    ![Pole se seznamem umožňující prázdný řetězec](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM bude vydána v dubnu 2014. Zde jsou hlavní body z poznámek k verzi, ale zkontrolujte [úplné poznámky k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.8) pro více informací o těchto změnách.

- **Cílové aplikace pro Windows Phone 8.1**: NuGet 2.8.1 nyní podporuje cílení na aplikace pro Windows Phone 8.1 pomocí názvů target framework "WindowsPhoneApp", "WPA", "WindowsPhoneApp81" a "WPA81".

- **Řešení opravy pro závislosti**: Při řešení závislostí balíčku NuGet historicky implementoval strategii výběru nejnižší hlavní a dílčí verze balíčku, která splňuje závislosti na balíčku. Na rozdíl od hlavní a dílčí verze však byla verze opravy vždy vyřešena na nejvyšší verzi. Ačkoli chování bylo dobře míněné, vytvořilo nedostatek determinismu pro instalaci balíčků se závislostmi.
- **Přepínač dependencyVersion**: Přestože NuGet 2.8 změní *výchozí* chování pro řešení závislostí, přidá také přesnější kontrolu nad procesem řešení závislostí prostřednictvím přepínače -DependencyVersion v konzoli správce balíčků. Přepínač umožňuje řešení závislostí na nejnižší možnou verzi (výchozí chování), nejvyšší možnou verzi nebo nejvyšší dílčí nebo verzi opravy. Tento přepínač funguje pouze pro instalační balíček v příkazu powershellu.
- **DependencyVersion Atribut**: Kromě -DependencyVersion přepínač podrobně popsané výše, NuGet také povoleno pro možnost nastavit nový atribut v nuget.config souboru definující, co je výchozí hodnota, pokud -DependencyVersion přepínač není zadán v vyvolání instalačního balíčku. Tato hodnota bude také respektována dialogem Správce balíčků NuGet pro všechny operace instalačního balíčku. Chcete-li tuto hodnotu nastavit, přidejte níže uvedený atribut do souboru nuget.config:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Preview NuGet Operations With -WhatIf**: Některé balíčky NuGet může mít hluboké závislosti grafy a jako takové může být užitečné při instalaci, odinstalovat nebo aktualizovat operace nejprve zobrazit, co se stane. NuGet 2.8 přidá standardní PowerShell -co když přepnout do instalačníbalíček, odinstalovat balíček a update-package příkazy povolit vizualizaci celé uzavření balíčků, na které bude použit příkaz.
- **Downgrade Package**: Není neobvyklé nainstalovat předběžnou verzi balíčku, aby bylo možné prozkoumat nové funkce a pak se rozhodnout vrátit zpět na poslední stabilní verzi. Před NuGet 2.8 se jednalo o vícekrokový proces odinstalace předběžné verze balíčku a jeho závislostí a následné instalace starší verze. S NuGet 2.8 však balíček aktualizace nyní vrátí zpět celý balíček uzavření (např. strom závislostí balíčku) na předchozí verzi.
- **Závislosti vývoje**: Mnoho různých typů funkcí lze doručit jako balíčky NuGet – včetně nástrojů, které se používají k optimalizaci procesu vývoje. Tyto součásti, i když mohou být nápomocny při vývoji nového balíčku, by neměly být považovány za závislost na novém balíčku, když je později publikován. NuGet 2.8 umožňuje balíček identifikovat v souboru .nuspec jako developmentDependency. Po instalaci budou tato metadata přidána také do souboru packages.config projektu, do kterého byl balíček nainstalován. Když je tento soubor packages.config později analyzován pro závislosti NuGet během balíčku nuget.exe, vyloučí tyto závislosti označené jako závislosti vývoje.
- **Jednotlivé packages.config Soubory pro různé platformy**: Při vývoji aplikací pro více cílových platforem, je běžné mít různé soubory projektu pro každý z příslušných prostředí sestavení. Je také běžné využívat různé balíčky NuGet v různých souborech projektu, protože balíčky mají různé úrovně podpory pro různé platformy. NuGet 2.8 poskytuje vylepšenou podporu pro tento scénář vytvořením různých souborů packages.config pro různé soubory projektu specifické pro platformu.
- **Záložní k místní mezipaměti**: Přestože Balíčky NuGet jsou obvykle spotřebovány ze vzdálené galerie, jako je [například galerie NuGet](http://www.nuget.org) pomocí síťového připojení, existuje mnoho scénářů, kde klient není připojen. Bez síťového připojení klientNuGet nebyl schopen úspěšně nainstalovat balíčky – i když tyto balíčky byly již v počítači klienta v místní mezipaměti NuGet. NuGet 2.8 přidává automatické mezipaměti záložní do konzoly správce balíčků.

    Záložní funkce mezipaměti nevyžaduje žádné konkrétní argumenty příkazu. Záložní mezipaměti navíc aktuálně funguje pouze v konzole správce balíčků – chování aktuálně nefunguje v dialogovém okně správce balíčků.
- **Opravy chyb**: Jednou z hlavních oprav chyb bylo zlepšení výkonu v příkazu update-package -reinstall.

    Kromě těchto funkcí a výše uvedené opravy výkonu tato verze NuGet také obsahuje mnoho dalších oprav chyb. Ve vydání bylo řešeno celkem 181 problémů. Úplný seznam pracovních položek opravených v NuGet 2.8, naleznete [NuGet Problém Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) pro tuto verzi.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

- Šablony webových formulářů nyní ukazují, jak provést potvrzení účtu a resetování hesla pro ASP.NET identitu.
- Řízení zdroje dat entity a zprostředkovatele dynamických dat pro rozhraní Entity Framework 6. Další podrobnosti naleznete v následujícím blogu MSDN: [Zprostředkovatel dynamických dat a EntityDataSource ovládací prvek pro entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Vylepšení směrování atributů](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Podpora bootstrapu pro šablony editorů](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Podpora výčtu v zobrazeních](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Nenápadná podpora atributů MinLength/ MaxLength](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Podpora 'tento' kontext v nenápadné Ajax](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET webové rozhraní API 2.1.2

- [Globální zpracování chyb](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Vylepšení směrování atributů](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Vylepšení stránky nápovědy](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [Podpora pro IgnoreRoute](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [Modul pro formátování typu média BSON](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Lepší podpora asynchronních filtrů](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [Analýza dotazů pro knihovnu formátování klienta](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET webové stránky 3.1.2

- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Účetní rámec 6.1

Entity Framework byl aktualizován na verzi 6.1 pro běh ový čas i nástroje. Entity Framework (EF) 6.1 je menší aktualizace entity Framework 6 a obsahuje řadu oprav chyb a nové funkce. Podrobné informace o ef6.1, včetně odkazů na dokumentaci k novým funkcím, naleznete [v tématu Historie verzí entity Framework](https://msdn.microsoft.com/data/jj574253). Mezi nové funkce v této verzi patří:

- **Konsolidace nástrojů** poskytuje konzistentní způsob, jak vytvořit nový model EF. Tato funkce rozšiřuje průvodce ADO.NET entity datový model pro podporu vytváření modelů Code First, včetně zpětné ho inženýrství z existující databáze. Tyto funkce byly dříve k dispozici v kvalitě beta verze v EF Power Tools.
- **Zpracování selhání potvrzení transakce** poskytuje nový [System.Data.Entity.Infrastructure.CommitFailureHandler,](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) který využívá nově zavedenou schopnost zachytit transakční operace. **CommitFailureHandler** umožňuje automatické obnovení z selhání připojení při potvrzení transakce.
- **IndexAttribute** umožňuje indexy, které mají být zadány umístěním atributu na vlastnost (nebo vlastnosti) v modelu Code First. Code First pak vytvoří odpovídající index v databázi.
- **Veřejné mapování ROZHRANÍ API** poskytuje přístup k informacím EF má o tom, jak jsou namapovány vlastnosti a typy na sloupce a tabulky v databázi. V minulých verzích bylo toto rozhraní API interní.
- **Možnost konfigurace zachycovačů prostřednictvím souboru App/Web.config**(umožňuje přidání zachycovačů bez nutnosti opětovné kompilace aplikace).
- **DatabaseLogger** je nový interceptor, který usnadňuje protokolování všech databázových operací do souboru. V kombinaci s předchozí funkcí to umožňuje snadno přepnout protokolování databázových operací pro nasazenou aplikaci bez nutnosti překompilovat.
- Bylo vylepšeno **zjišťování změn modelu migrace,** takže migrace scaffolded jsou přesnější; výkon procesu detekce změn byl také značně vylepšen.
- **Vylepšení výkonu,** včetně snížení databázové operace během inicializace, optimalizace pro porovnání rovnosti null v dotazech LINQ, rychlejší generování zobrazení (vytváření modelu) ve více scénářích a efektivnější materializace sledovaných entit s více přidruženími.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET identita 2.0.0

- **Dvoufaktorové ověřování**: ASP.NET Identita nyní podporuje dvoufaktorové ověřování. Dvoufaktorové ověřování poskytuje další vrstvu zabezpečení pro vaše uživatelské účty v případě, že dojde k ohrožení hesla. K dispozici je také ochrana pro útoky hrubou silou proti dvěma kódům faktorů.
- **Uzamčení účtu:** Poskytuje způsob, jak uživatele uzamknout, pokud uživatel nesprávně zadá své heslo nebo dvoufaktorové kódy. Počet neplatných pokusů a časový rozsah pro uživatele jsou uzamčeny lze nakonfigurovat. Vývojář může volitelně vypnout uzamčení účtu pro určité uživatelské účty, pokud je to nutné.
- **Potvrzení účtu:** Systém ASP.NET identitnyní podporuje potvrzení účtu. To je poměrně běžný scénář ve většině webových stránek dnes, kde, když se zaregistrujete na nový účet na webových stránkách, jste povinni potvrdit svůj e-mail, než budete moci dělat něco na webových stránkách. Potvrzení e-mailu je užitečné, protože zabraňuje vytváření falešných účtů. To je velmi užitečné, pokud používáte e-mail jako způsob komunikace s uživateli vašich webových stránek, jako jsou stránky fóra, bankovnictví, elektronický obchod nebo sociální webové stránky.
- **Resetování hesla:** Resetování hesla je funkce, kde uživatel může obnovit svá hesla, pokud zapomněli své heslo.
- **Bezpečnostní razítko (Odhlaste se všude):** Podporuje způsob, jak obnovit token zabezpečení pro uživatele v případech, kdy uživatel změní své heslo nebo jiné informace související se zabezpečením, jako je odebrání přidruženého přihlášení (například Facebook, Google, účet Microsoft a tak dále). To je potřeba zajistit, že všechny tokeny generované se starým heslem jsou zneplatněny. V ukázkovém projektu, pokud změníte heslo uživatele pak nový token je generován pro uživatele a všechny předchozí tokeny jsou zrušeny. Tato funkce poskytuje další vrstvu zabezpečení vaší aplikace, protože když změníte heslo, budete odhlášeni ze všech stran (všechny ostatní prohlížeče), kde jste se přihlásili do této aplikace.
- **Nastavení, aby byl typ primárního klíče rozšiřitelný pro uživatele a role**: V ASP.NET identity 1.0 byl typ primárního klíče pro tabulku Uživatelé a role řetězce. To znamená, že když byl ASP.NET identity systému trvalé v SQL Server pomocí Entity Framework, jsme používali nvarchar. Tam bylo mnoho diskusí kolem této výchozí implementace na přetečení zásobníku a na základě příchozí zpětnou vazbu. Poskytli jsme háček rozšiřitelnosti, kde můžete určit, co by mělo být primárním klíčem tabulky Uživatelé a role. Tento hák rozšiřitelnosti je zvláště užitečné, pokud migrujete aplikaci a aplikace byla ukládání UserIds jsou IDENTIFIKÁTORY GUID nebo ints.
- **Podpora IQueryable na uživatele a role:** Přidána podpora pro IQueryable na UsersStore a RolesStore, můžete snadno získat seznam uživatelů a rolí.
- **Podpora operace odstranění prostřednictvím usermanageru**
- **Indexování na UserName**: V ASP.NET implementace entity identity, jsme přidali jedinečný index na uživatelské jméno pomocí nového IndexAttribute v EF 6.1.0. Tím zajistíte, že uživatelská jména jsou vždy jedinečná a nedošlo k žádnému sporu, ve kterém byste mohli skončit s duplicitními uživatelskými jmény.
- **Rozšířený validátor hesla:** Validátor hesla, který byl dodán v ASP.NET identity 1.0 byl poměrně základní identity identity, který byl pouze ověření minimální délky. K dispozici je nový validátor hesla, který vám dává větší kontrolu nad složitostí hesla. Vezměte prosím na vědomí, že i když zapnete všechna nastavení v tomto hesle, doporučujeme vám povolit dvoufaktorové ověřování pro uživatelské účty.
- **IdentityFactory Middleware/ CreatePerOwinContext**:

    - **Správce uživatelů**: Implementaci z výroby můžete použít k získání instance UserManager z kontextu OWIN. Tento vzor je podobný tomu, co používáme pro získání AuthenticationManager z kontextu OWIN pro přihlášení a přihlášení. Toto je doporučený způsob získání instance UserManager na požadavek pro aplikaci.
    - **DbContextFactory**: ASP.NET Identity používá entity Framework pro uchování systému identity v SQL Server. Chcete-li to provést systém identit má odkaz na ApplicationDbContext. DbContextFactory Middleware vrátí instanci ApplicationDbContext na požadavek, který můžete použít ve vaší aplikaci.
- **ASP.NET vzorky identity NuGet balíček**: Ukázky NuGet balíček můžete usnadnit instalaci a spuštění ukázky pro ASP.NET identity a postupujte podle osvědčených postupů. Toto je ukázka ASP.NET aplikace MVC. Před nasazením této aplikace v produkčním prostředí upravte kód tak, aby vyhovoval vaší aplikaci. Vzorek by měl být nainstalován v aplikaci prázdné ASP.NET. Další informace o balíčku najdete v následujícím příspěvku na blogu: [Oznámení RTM ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Součásti Microsoft OWIN

V této verzi bylo opraveno mnoho chyb. Podrobnější informace naleznete [v poznámkách k verzi verze verze 2.1.0.](https://katanaproject.codeplex.com/releases/view/113281)

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

V této verzi bylo opraveno mnoho chyb. Podrobnější informace naleznete [v poznámkách k verzi verze verze 2.0.2.](https://github.com/SignalR/SignalR/releases/tag/2.0.2)
