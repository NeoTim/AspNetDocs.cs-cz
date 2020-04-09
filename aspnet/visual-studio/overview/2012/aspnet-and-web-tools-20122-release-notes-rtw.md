---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET a webové nástroje 2012.2 Poznámky k verzi | Dokumenty společnosti Microsoft
author: rick-anderson
description: Poznámky k verzi pro ASP.NET a webové nástroje 2012.2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676305"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET a webové nástroje – poznámky k verzi 2012.2

> Tento dokument popisuje vydání ASP.NET a webových nástrojů 2012.2. Jedná se o aktualizaci webových nástrojů a ASP.NET sady Visual Studio.

- [Poznámky k instalaci](#_Installation)
- [Dokumentace](#_Documentation)
- [Podpora](#_Support)
- [Požadavky na software](#_Software_Requirements)
- [Nové funkce v ASP.NET a webových nástrojích 2012.2](#_New_Features_in)

    - [Nástroje](#_Tooling)
    - [Publikování na webu](#_Web_Publishing)
    - [ASP.NET šablony MVC](#_Templates)
    - [Webové rozhraní API ASP.NET](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET adres URL](#_ASP.NET_Friendly_URLs)
- [Známé problémy a nejnovější změny](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET a webových nástrojů 2012.2 pro Visual Studio 2012 lze nainstalovat pomocí [instalačního programu webové platformy](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2). Toto je aktualizace Visual Studio 2012 nebo Visual Studio Express 2012 pro web, který je povinný. Pokud nemáte nainstalovanou aplikaci Visual Studio, bude nainstalována aplikace Visual Studio Express 2012 for Web.

Můžete také nainstalovat ASP.NET a webové nástroje 2012.2 ručně. Musíte mít nainstalovanou Visual Studio 2012 nebo Visual Studio Express 2012 for Web. Poté postupujte podle následujících pokynů: 

1. Stáhněte si instalační program [ASP.NET a Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) ze služby Stažení softwaru.
2. Po zobrazení výzvy klikněte na Spustit. Soubor můžete také uložit a spustit jej později.
3. Ověřte verzi sady Visual Studio, kterou aktualizujete. Můžete to provést spuštěním sady Visual Studio, kterou chcete aktualizovat. Potom klepněte na položku nabídky Nápověda.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Pokud se zobrazí &quot;položka nabídky O aplikaci Microsoft&quot; Visual Studio 2012 for Web, stáhněte si [nástroje pro vývojáře web 2012.2 – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228). V opačném případě stáhnout [Nástroje pro vývojáře webu 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. Po zobrazení výzvy klikněte na Spustit. Soubor můžete také uložit a spustit jej později.

> [!NOTE]
> ASP.NET a webtools 2012.2 neobsahuje sql server datové nástroje. SQL Server a Windows Azure SQL Databases poskytují bohatší sadu databázových nástrojů, včetně offline vývoje podporovaného projektem, porovnání schémat a rozšířených možností nasazení databáze. Další informace nebo instalaci nástrojů SQL [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)Server Data Tools naleznete na adrese .

<a id="_Documentation"></a>
## <a name="documentation"></a>Dokumentace

Návody a další informace o ASP.NET a webových nástrojích 2012.2 jsou k dispozici na webových stránkách ASP.NET ( https://www.asp.net).

<a id="_Support"></a>
## <a name="support"></a>Podpora

ASP.NET a webových nástrojů 2012.2 je oficiálně vydána a podporována. Můžete použít svůj normální kanál podpory. Můžete také psát otázky na fórech ASP.NET ([https://forums.asp.net/](https://forums.asp.net/)), kde jsou členové ASP.NET komunity často schopni poskytovat neformální podporu.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Požadavky na software

ASP.NET a webových nástrojů 2012.2 vyžaduje Visual Studio 2012 nebo Visual Studio Express 2012 pro web.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Nové funkce v ASP.NET a webových nástrojích 2012.2

Tato část popisuje funkce, které byly zavedeny v ASP.NET a webových nástrojích 2012.2.

<a id="_Tooling"></a>
### <a name="tooling"></a>Nástroje

- Inspektor stránek 

    - Podpora mapování výběru JavaScriptu umožňuje Inspektoru stránky mapovat položky, které byly dynamicky přidány na stránku zpět na odpovídající kód JavaScriptu.
    - Možnost zobrazit aktualizace CSS v reálném čase.
    - Další informace naleznete [v části CsS Auto-Sync a Mapování výběru javascriptu v Inspektoru stránky](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Editor 

    - Podpora zvýraznění syntaxe pro CoffeeScript, Knír, Řídítka a JsRender.
    - Editor HTML poskytuje Intellisense pro knockout vazby.
    - Méně editace a kompilátor podporu povolit budování dynamické CSS pomocí LESS.
    - Vložte JSON jako třídu .NET. Pomocí tohoto příkazu Speciální vložit vložit Do souboru kódu Jazyka C# nebo VB.NET a Visual Studio automaticky vygeneruje třídy .NET odvozené z JSON.
- Podpora mobilního emulátoru přidává háky rozšiřitelnosti, takže emulátory třetích stran mohou být instalovány jako VSIX. Nainstalované emulátory se zobrazí v rozbalovací nabídce F5, takže vývojáři mohou zobrazit náhled svých webových stránek na různých mobilních zařízeních. Přečtěte si více o této funkci v blogu Scott Hanselman na [nové BrowserStack integrace s Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Publikování na webu

- Projekty webu mají nyní stejné možnosti publikování jako projekty webových aplikací, včetně publikování na webech Windows Azure.
- Selektivní publikování &#8211; pro jeden nebo více souborů můžete provést následující akce (po publikování do koncového bodu nasazení webu): 

    - Publikujte vybrané soubory.
    - Podívejte se na rozdíl mezi místním a vzdáleným souborem.
    - Aktualizujte místní soubor pomocí vzdáleného souboru nebo aktualizujte vzdálený soubor místním souborem.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET šablony MVC

- Nová šablona aplikace Facebook usnadňuje psaní aplikací Facebook Canvas. V několika jednoduchých krocích můžete vytvořit aplikaci Facebook, která získává data od přihlášeného uživatele a integruje se se svými přáteli. Šablona obsahuje novou knihovnu, která se postará o všechny instalace, které se podílejí na vytváření aplikace Facebook, včetně ověřování, oprávnění, přístupu k datům facebooku a dalších. Další informace o používání šablony [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)aplikace Facebook najdete v tématu .
- Nová jednostránková šablona MVC aplikace umožňuje vývojářům vytvářet interaktivní webové aplikace na straně klienta pomocí HTML 5, CSS 3 a populárních knokautových a jQuery JavaScriptových knihoven nad ASP.NET webové rozhraní API. Šablona obsahuje aplikaci seznamu úkolů, která demonstruje běžné postupy pro vytváření aplikace JAVAScript HTML5, která používá rozhraní API serveru RESTful. Můžete si přečíst více na . [https://www.asp.net/single-page-application](../../../single-page-application/index.md)
- Nyní můžete vytvořit VSIX, který přidá nové šablony do dialogového okna ASP.NET MVC Nový projekt. Zde se dozvíte, jak:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes balíček &#8211; šablony projektu MVC byly aktualizovány tak, aby zahrnovaly nový balíček NuGet "FixedDisplayModes", který obsahuje řešení pro chybu v MVC 4. Další informace o opravě obsažené v balíčku naleznete v[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)tomto příspěvku blogu ( ) od týmu MVC.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

ASP.NET webové rozhraní API bylo vylepšeno o několik nových funkcí:

- ASP.NET Web API OData
- trasování webového rozhraní API ASP.NET
- Stránka nápovědy webového rozhraní ASP.NET API

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Webové rozhraní API OData poskytuje flexibilitu, kterou potřebujete k vytváření koncových bodů OData s bohatou obchodní logikou přes libovolný zdroj dat. Pomocí ASP.NET Web API OData řídíte množství sémantiky OData, které chcete vystavit. ASP.NET Web API OData je součástí ASP.NET šablony projektu MVC 4[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)a je také k dispozici z NuGet ( ).

ASP.NET Web API OData aktuálně podporuje následující funkce:

- Povolte sémantiku dotazu OData použitím atributu [Queryable].
- Snadno ověřte dotazy OData a omezte sadu podporovaných možností dotazů, operátorů a funkcí.
- Parametr bind to ODataQueryOptions directly to get abstrakt syntax estrofie stromu dotazu, který pak může být ověřena a použita na IQueryable nebo IEnumerable.
- Povolte stránkování řízené službou a generování dalšího propojení stránky zadáním omezení výsledků na atributu [Queryable].
- Požádejte o vložený počet celkového počtu odpovídajících prostředků pomocí $inlinecount.
- Řízení šíření null.
- Všechny/Všechny operátory v $filter.
- Odvodit datový model entity podle konvence nebo explicitně přizpůsobit model způsobem podobným entity framework code-first.
- Vystavit entity sady odvozením z EntitySetController.
- Jednoduché, přizpůsobitelné konvence pro vystavení navigačních vlastností, manipulaci s odkazy a implementaci akcí OData.
- Zjednodušené směrování pomocí metody rozšíření MapODataRoute.
- Podpora pro správu verzí vystavením více modelů EDM.
- Vystavit servisní dokument a $metadata, abyste mohli generovat klienty (.NET, Windows Phone, Windows Store atd.) pro webové rozhraní API.
- Podpora pro formáty OData Atom, JSON a JSON.
- Vytvořte, aktualizujte, částečně aktualizujte (PATCH) a odstraňte entity.
- Dotazovat se a manipulovat s relacemi mezi entitami.
- Vytvořte propojení vztahů, které se spojí s vašimi trasami.
- Komplexní typy.
- Dědičnost typu entity.
- Vlastnosti kolekce.
- Výčty.
- OData akce.
- Postavenna stejném základě jako WCF Data Services,[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)a to ODataLib ( ).

Další informace o ASP.NET webovém [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)rozhraní API OData naleznete v tématu .

#### <a name="aspnet-web-api-tracing"></a>trasování webového rozhraní API ASP.NET

ASP.NET trasování webového rozhraní INTEGRUje trasovací data z webových rozhraní API s trasování matné řazené.ASP.NET Web API Trasování integruje trasování dat z webových rozhraní API s .NET Trasování. Nyní je ve výchozím nastavení povolena v šabloně projektu webového rozhraní API. Trasování dat pro webové rozhraní API je odeslána do okna Výstup a je k dispozici prostřednictvím IntelliTrace. ASP.NET trasování webového rozhraní umožňuje sledovat informace o webovém rozhraní API při hostování ve Windows Azure prostřednictvím integrace s [Diagnostikou Windows Azure](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx). Můžete také nainstalovat a povolit ASP.NET trasování webového rozhraní API v[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)libovolné aplikaci pomocí balíčku NuGet ASP.NET web API Tracing ( ).

Další informace o konfiguraci a používání ASP.NET [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)trasování webového rozhraní NALEZNETE V TÉMATU .

#### <a name="aspnet-web-api-help-page"></a>Stránka nápovědy webového rozhraní ASP.NET API

Stránka nápovědy webového rozhraní ASP.NET api je nyní ve výchozím nastavení zahrnuta v šabloně projektu webového rozhraní API. Stránka nápovědy webového rozhraní API ASP.NET automaticky generuje dokumentaci pro webová rozhraní API, včetně koncových bodů HTTP, podporovaných metod HTTP, parametrů a ukázkových datových částí zpráv požadavků a odpovědí. Dokumentace se automaticky vyžádá z komentářů ve vašem kódu. Stránku nápovědy ASP.NET webového rozhraní API můžete také přidat do libovolné[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)aplikace pomocí balíčku NuGet stránky nápovědy webového rozhraní ASP.NET API ( ).

Další informace o nastavení a přizpůsobení stránky nápovědy [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)k webovému rozhraní ASP.NET naleznete v tématu .

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR usnadňuje přidání webových funkcí v reálném čase do aplikace ASP.NET pomocí WebSockets, pokud je k dispozici, a automaticky se vrací k jiným technikám, když není.

Další informace o používání ASP.NET [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)SignalR naleznete v tématu .

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET adres URL

ASP.NET FriendlyURLs umožňuje vývojářům webových formulářů vytvářet čistě vypadající adresy URL (bez rozšíření .aspx). Vyžaduje malou nebo žádnou konfiguraci a lze ji použít s existujícími aplikacemi ASP.NET v4.0. Funkce FriendlyURLs také usnadňuje vývojářům přidávat mobilní podporu do svých aplikací tím, že podporuje přepínání mezi zobrazeními pro stolní počítače a mobilní zařízení.

Další informace o instalaci a používání ASP.NET [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)adresy URL naleznete v tématu .

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a nejnovější změny

Tato část popisuje známé problémy a nejnovější změny, které jsou v ASP.NET a webových nástrojů 2012.2 vydání.

### <a name="installation-issues"></a>Problémy s instalací

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Mimoobista instalace Visual Studia 2012

Instalace další skladové položky sady Visual Studio 2012 po instalaci ASP.NET a webových nástrojů 2012.2 bude vyžadovat operaci opravy. Zvažte následující pořadí:

1. Instalace visual studia 2012 Express pro web
2. Instalace ASP.NET a webových nástrojů 2012.2
3. Instalace Visual Studia 2012 Professional, Premium nebo Ultimate

Krok 2 by vedl pouze k instalaci aktualizací pro Express for Web. Chcete-li zajistit, aby další skladová položka nainstalovaná během kroku 3 obsahovala aktualizaci, budete muset opravit ASP.NET a webových nástrojů 2012.2, abyste nainstalovali aktualizace pro poslední nainstalovanou skladovou položku. To platí také v případě, že skum v kroku 1 a 3 jsou obrácené.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Instalace microsoft ASP.NET a webových nástrojů 2012.2 při otevření sady Visual Studio

Pokud je v systému VS otevřen během instalace microsoft ASP.NET a webových nástrojů 2012.2, Visual Studio může skončit ve špatném stavu. Doporučujeme, aby uživatelé před instalací zavřeli všechny instance sady Visual Studio.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Zrušení instalace ASP.NET a webových nástrojů 2012.2 uprostřed instalace

Zrušení ASP.NET a webtools 2012.2 nastavení uprostřed instalace opustí Visual Studio ve špatném stavu. Chcete-li tento problém vyřešit, postupujte takto: 

- Přejít na Přidat odebrat programy
- Odinstalujte microsoft ASP.NET a webové nástroje 2012.2, pokud jsou k dispozici.
- Přeinstalace ASP.NET a webových nástrojů společnosti Microsoft 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>Po odinstalování ASP.NET a webových nástrojů 2012.2 chybí ASP.NET šablony MVC 4 a šablony webu Razor v2

Odinstalováním ASP.NET a webových nástrojů 2012.2 také odinstalujete všechny šablony webu ASP.NET MVC 4 a Razor v2 z visual studia 2012.

Řešení je opravit instalaci sady Visual Studio 2012 přeinstalovat ASP.NET šablony webu MVC 4 a Razor v2.

### <a name="tooling-issues"></a>Problémy s nástroji

#### <a name="nuget-error-reported-during-project-creation"></a>Chyba NuGet hlášená během vytváření projektu

Po instalaci ASP.NET a Webových nástrojů 2012.2 se může zobrazit následující chyba při vytváření projektu MVC 4

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET a Web Tools 2012.2 je dodáván nuget 2.1 a bude upgradovat rozšíření v sadě Visual Studio 2012. V některých případech instalační program VSIX se nezdaří správně aktualizovat VSIX. Následující kroky vám umožní tento problém vyřešit:

1. Spuštění Visual Studia 2012 jako správce
2. Přejděte na&gt;Nástroje - Rozšíření a aktualizace a odinstalujte NuGet.
3. Zavřete Visual Studio.
4. Přejděte do instalační složky ASP.NET a Webových nástrojů 2012.2:

    1. Pro Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**
    2. Pro sadu Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**
5. Poklepáním na Soubor NuGet.Tools.vsix přeinstalujte soubor NuGet.

### <a name="web-api-issues"></a>Problémy s webovým rozhraním API

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Analýza problémů v literály $filter a DateTime

Analyzátoru Identifikátoru URI oDate se nepodaří správně analyzovat literály částečné datetime. Například $filter=start eq datetime'2012-12-31T12:00' se nepodaří správně analyzovat. Řešení je použít celý literál, $filter=start eq datetime'2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData nepodporuje názvy vlastností bez rozlišování velkých a malých písmen.

OData nepodporuje názvy vlastností bez rozlišování velkých a malých písmen v dotazech OData a cestě odata. Viz pracovní položky:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Pokud uživatelé mají různé kryty na straně klienta javascriptu a serveru, pravděpodobně narazí na tento problém. Tento problém je záměrné v protokolu odata. Mnoho uživatelů však hlásí tento problém. Chcete-li jej obejít, uživatelé musí opravit své případy v adrese URL.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Výchozí konvence směrování OData nepodporují vlastnost POST/PUT.

Výchozí konvence směrování OData nepodporují vlastnost POST/PUT. Viz pracovní [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)položka . Chybí nám tato běžně používaná konvence ve výchozích konvencích.

Chcete-li jej obejít, uživatelé musí rozšířit novou konvenci směrování, aby ji podpořili.

### <a name="facebook-template-issues"></a>Problémy se šablonami na Facebooku

#### <a name="facebook-application-template-only-works-using-net-45"></a>Šablona aplikace Facebook funguje pouze pomocí rozhraní .NET 4.5

Chcete-li zobrazit šablonu aplikace Facebook v ASP.NET MVC 4, musíte v rozevíracím seznamu Vytvořit možnost .NET 4.5 v rozevíracím seznamu rozhraní v dialogovém okně Nový projekt.

#### <a name="real-time-update-controller"></a>Řadič aktualizací v reálném čase

Šablona aplikace Facebook umožňuje uživateli snadno vytvořit řadič webového rozhraní API pro zpracování aktualizací z Facebooku v reálném čase. Pokud je váš vývojový počítač za NAT, ovladač nemusí fungovat bez další konfigurace sítě. Podrobnosti naleznete zde:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Hodnoty řetězce dotazu jsou v konfliktu s parametry Facebook OAuth

Následující pole jsou v konfliktu s adresou URL zpětného volání dialogového okna Facebook OAuth. Nepřidávejte vlastní hodnoty řetězce dotazu s následujícími\_názvy:\_kód, chyba, popis chyby, důvod chyby.

#### <a name="using-page-inspector-with-facebook-template"></a>Použití Inspektoru stránky se šablonou Facebooku

Při ladění facebookové aplikace nelze v Sadě Visual Studio 2012 používat funkci Inspektor stránky. Inspektor stránky aktuálně nepodporuje rámce iframe.

### <a name="single-page-application-template-issues"></a>Problémy se šablonou aplikace na jedné stránce

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>S aktualizací JQuery 1.9/Knockout 2.2.1 při spuštění výchozího projektu MVC SPA není správně zpracována událost úpravy položky todo enter focus.

S aktualizací JQuery 1.9/Knockout 2.2.1 při spuštění výchozího projektu MVC SPA již nové úpravy položek todo zadávají po zadání nového pole pro úpravu položky úkolů po zadání nové položky úkolů do seznamu úkolů již nelze zaostřit zpět do nového pole pro úpravu položky todo.

Chcete-li [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)na odkazovat na řešení a provést podobnou opravu následujícímu ukázkovému kódu:

Soubor todo.model.js  
 funkce todolist(data), přidejte následující:  
 **self.isSelected = ko.observable(false);**

funkce todoList.prototype.addTodo, přidejte následující černý text:  
 **self.isSelected(true);**  
 self.newTodoTitle(&quot;&quot;);

Soubor index.cshtml, přidejte následující černý text:  
 &lt;formulář data-bind=&quot;odeslat: addTodo&quot;&gt;  
 &lt;input&quot;class= addTodo&quot; type=&quot;&quot; text&quot;data-bind= value: newTodoTitle, zástupný symbol: 'Typ zde přidat', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;  
 &lt;/formulář&gt;
