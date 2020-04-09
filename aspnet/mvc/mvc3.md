---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (zahrnuje aktualizaci nástrojů z dubna 2011) ASP.NET MVC 3 je rámec pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedeného návrhového vzoru...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675142"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(zahrnuje aktualizaci nástrojů z dubna 2011)*
> 
> ASP.NET MVC 3 je rámec pro vytváření škálovatelných webových aplikací založených na standardech pomocí zavedených návrhových vzorů a výkonu ASP.NET a rozhraní .NET Framework.
> 
> Instaluje se vedle sebe s ASP.NET MVC 2, takže jej můžete začít používat ještě dnes!
> 
> Stáhněte si [instalační program zde](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>Nejlepší funkce

- Integrovaný systém lešení rozšiřitelný přes NuGet
- Šablony projektů s povoleným HTML 5
- Expresivní pohledy včetně nového stroje Razor View Engine
- Výkonné háčky s vstřikováním závislostí a filtry globálních akcí
- Podpora bohatého Jazyka JavaScript s nenápadnou vazbou JavaScriptu, jQuery Validation a JSON
- *Přečtěte si úplný seznam funkcí [níže](#overview)*

## <a name="top-links"></a>Nejlepší odkazy

Co je nového v ASP.NET MVC 3

- Phil Haack: [ASP.NET MVC 3 Vydáno](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express a Orchard vydáno - Microsoft ledna Web Release v kontextu](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [Oznámení vydání ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [Poznámky k verzi pro ASP.NET MVC 3](../whitepapers/mvc3-release-notes.md)

Instalace a nápověda

- Instalace ASP.NET MVC 3 pomocí [Instalační služby webové platformy (doporučeno)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- Instalace ASP.NET MVC 3 pomocí [spustitelného souboru instalačního programu](https://go.microsoft.com/fwlink/?LinkID=208140)
- Instalace [ASP.NET MVC 3 pro Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)
- Přečtěte si [úvodní ASP.NET kurzu MVC 3](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- Získejte pomoc a diskutujte o ASP.NET MVC 3 ve [fórech](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 – přehled

ASP.NET MVC 3 staví na ASP.NET MVC 1 a 2 a přidává skvělé funkce, které zjednodušují váš kód a umožňují hlubší rozšiřitelnost. Toto téma obsahuje přehled mnoha nových funkcí, které jsou součástí této verze, uspořádané do následujících částí:

- [Rozšiřitelné lešení s integrací MvcScaffold](#BM_MvcScaffolding)
- [Šablony projektů s povoleným HTML 5](#BM_HTML5)
- [Stroj na pohled na holicí stroje](#BM_TheRazorViewEngine)
- [Podpora pro více zobrazení motorů](#BM_Support_for_Multiple_View_Engines)
- [Vylepšení řadiče](#BM_Controller_Improvements)
- [JavaScript a Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Vylepšení ověření modelu](#BM_Model_Validation_Improvements)
- [Vylepšení vkládání závislostí](#BM_Dependency_Injection_Improvements)
- [Další nové funkce](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>Rozšiřitelné lešení s integrací MvcScaffold

Nový systém lešení usnadňuje vyzvednutí a produktivní používání, pokud jste v rámci zcela noví, a automatizovat běžné vývojové úkoly, pokud jste zkušení a již víte, co děláte.

To je podporováno novým balíčkem *lešení* NuGet s názvem **MvcScaffolding**. Termín "Lešení" je používán mnoha softwarových technologií znamenat "rychle generování základní nástin vašeho softwaru, který pak můžete upravit a přizpůsobit". Balíček lešení, který vytváříme pro ASP.NET MVC, je velmi přínosný v několika scénářích:

- **Pokud se učíte ASP.NET MVC poprvé**, protože to vám dává rychlý způsob, jak získat nějaké užitečné, pracovní kód, který pak můžete upravit a přizpůsobit podle vašich potřeb. To vás ušetří od traumatu při pohledu na prázdnou stránku a nemají ponětí, kde začít!
- **Pokud víte, ASP.NET MVC dobře a nyní zkoumáte některé nové doplňkové technologie,** jako je objekt-relační mapovač, zobrazení motoru, testovací knihovny, atd., protože tvůrce této technologie může mít také vytvořil lešení balíček pro něj.
- **Pokud vaše práce zahrnuje opakované vytváření podobných tříd nebo souborů nějakého druhu**, protože můžete vytvořit vlastní složky scaffolders, které výstup testovací příslušenství, nasazení skripty nebo cokoli jiného, co potřebujete. Každý ve vašem týmu může také používat vaše vlastní složky šaškárna.

Mezi další funkce mvcscaffoldingpatří:

- Podpora projektů C# a VB
- Podpora pro stroje razor a ASPX zobrazit motory
- Podporuje lešení do oblastí MVC ASP.NET a pomocí vlastních rozvržení/předloh zobrazení
- Výstup můžete snadno přizpůsobit úpravou šablon T4
- Můžete přidat zcela nové složky vzorníku pomocí vlastní logiky prostředí PowerShell a vlastních šablon T4. Tyto (a všechny vlastní parametry, které jste jim zadali) se automaticky zobrazí v seznamu dokončení karty konzoly.
- Můžete získat Balíčky NuGet obsahující další složky scaffolders pro různé technologie (např. je tu proof-of-concept jeden pro LINQ na SQL nyní) a kombinovat je dohromady

Aktualizace nástrojů ASP.NET MVC 3 obsahuje skvělou podporu sady Visual Studio pro tento systém lešení, například:

- Dialogové okno Přidat řadič nyní podporuje plné automatické generování uživatelského okna akcí vytvořit, číst, aktualizovat a odstranit kontroleru a odpovídající zobrazení. Ve výchozím nastavení toto kód přístupu k datům ve sešitech pomocí kódu EF First.
- Přidat dialog řadiče podporuje *rozšiřitelná lešení* prostřednictvím balíčků NuGet, jako je *MvcScaffolding*. To umožňuje připojení vlastních lešení do dialogu, které by vám umožnilo vytvořit lešení pro jiné technologie přístupu k datům, jako je NHibernate nebo dokonce JET s ODBCDirect, pokud jste tak nakloněni!

Další informace o lešení v ASP.NET MVC 3 naleznete v následujících zdrojích:

- Steve Sanderson post série, včetně: 

    1. [Úvod: Scaffold vaše ASP.NET MVC 3 projekt s balíčkem MvcScaffolding](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Standardní použití: Typické případy použití a možnosti](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Vztahy 1:N](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Akce lešení a testy jednotek](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [Přepsání šablon T4](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Tento příspěvek: Vytvoření vlastních složky lenochodů](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman příspěvek z jeho zasedání PDC 2010 [Stavební Blog s Microsoft "Nepojmenovaný balíček Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 Šablony projektů

Dialogové okno Nový projekt obsahuje zaškrtávací políčko povolit html 5 verze šablon projektů. Tyto šablony využívají Modernizr 1.7 k poskytování podpory kompatibility pro HTML 5 a CSS 3 v prohlížečích nižší úrovně.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Stroj na pohled na holicí stroje

ASP.NET MVC 3 přichází s novým view engine s názvem Razor, který nabízí následující výhody:

- Syntaxe břitvy je čistá a stručná, což vyžaduje minimální počet úhozů.
- Holicí strojek se snadno učí, částečně proto, že je založen na existujících jazycích, jako je C# a Visual Basic.
- Visual Studio obsahuje IntelliSense a zbarvení kódu pro syntaxi Razor.
- Zobrazení holicí strojek lze testovat bez nutnosti spuštění aplikace nebo spuštění webového serveru.

Některé nové funkce Razor zahrnují následující:

- `@model`syntaxe pro určení typu předávaný do zobrazení.
- `@* *@`syntaxe komentáře.
- Možnost zadat výchozí hodnoty (například `layoutpage`) jednou pro celý web.
- Metoda `Html.Raw` pro zobrazení textu bez kódování HTML.
- Podpora pro sdílení kódu mezi více zobrazeními*\_(viewstart.cshtml* nebo * \_viewstart.vbhtml* soubory).

Razor také obsahuje nové html pomocníky, jako jsou následující:

- `Chart`. Vykreslí graf, který nabízí stejné funkce jako ovládací prvek grafu v ASP.NET 4.
- `WebGrid`. Vykreslí datovou mřížku doplněnou funkcí stránkování a řazení.
- `Crypto`. Používá algoritmy hash k vytvoření správně nasolených a zahashovaných hesel.
- `WebImage`. Vykreslí obraz.
- `WebMail`. Odešle e-mailovou zprávu.

Další informace o razor, naleznete v následujících zdrojích:

- [Scott Guthrie blog post zavedení Břitva](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie blog post @model zavedení klíčové slovo](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie blog post zavedení Razor rozložení](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API Stručný přehled](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Podpora pro více zobrazení motorů

Dialogové okno **Přidat zobrazení** v ASP.NET MVC 3 umožňuje vybrat modul zobrazení, se kterým chcete pracovat, a dialogové okno **Nový projekt** umožňuje určit výchozí modul zobrazení pro projekt. Můžete zvolit modul zobrazení webových formulářů (ASPX), břitvu nebo modul zobrazení s otevřeným zdrojovým kódem, například [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/)nebo [NDjango](http://ndjango.org/).

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Vylepšení řadiče

### <a name="global-action-filters"></a>Filtry globálních akcí

Někdy chcete provést logiku před spuštěním metody akce nebo po spuštění metody akce. Pro podporu tohoto, ASP.NET MVC 2 za předpokladu, filtry akcí. Filtry akcí jsou vlastní atributy, které poskytují deklarativní prostředky pro přidání chování před akcí a po akci do konkrétních metod akce kontroleru. V některých případech však můžete chtít určit chování před akcí nebo po akci, které se vztahuje na všechny metody akce. MVC 3 umožňuje určit globální filtry `GlobalFilters` jejich přidáním do kolekce. Další informace o filtrech globálních akcí naleznete v následujících zdrojích:

- [Scott Guthrie blog na MVC 3 Náhled](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [Filtrování v ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Nová vlastnost "ViewBag"

Řadiče MVC 2 `ViewData` podporují vlastnost, která umožňuje předat data do šablony zobrazení pomocí rozhraní API slovníku s pozdní vazbou. V MVC 3 můžete také použít poněkud `ViewBag` jednodušší syntaxe s vlastností k dosažení stejného účelu. Například místo psaní `ViewData["Message"]="text"`můžete psát `ViewBag.Message="text"`. Není nutné definovat žádné třídy silného typu `ViewBag` pro použití vlastnosti. Vzhledem k tomu, že se jedná o dynamickou vlastnost, můžete místo toho pouze získat nebo nastavit vlastnosti a bude je dynamicky řešit za běhu. Interně `ViewBag` vlastnosti jsou uloženy jako dvojice `ViewData` název/hodnota ve slovníku. (Poznámka: ve většině předběžných verzí MVC `ViewBag` 3 byla `ViewModel` vlastnost pojmenována.)

### <a name="new-actionresult-types"></a>Nové typy "ActionResult"

Následující `ActionResult` typy a odpovídající pomocné metody jsou nové nebo vylepšené v MVC 3:

- [httpnotfoundresult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). Vrátí klientovi stavový kód 404 HTTP.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Vrátí dočasné přesměrování (stavový kód HTTP 302) nebo trvalý přesměrovací kód (stavový kód HTTP 301) v závislosti na logickém parametru. Ve spojení s touto změnou má třída [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) nyní tři `RedirectPermanent`metody `RedirectToRoutePermanent`pro `RedirectToActionPermanent`provádění trvalých přesměrování: , , a . Tyto metody vrátí `RedirectResult` instanci s vlastností `Permanent` nastavenou na `true`.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Vrátí uživatelem zadaný stavový kód HTTP.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript a Ajax Vylepšení

Ve výchozím nastavení používají pomocníci Ajax a ověřování v MVC 3 nenápadný přístup javascriptu. Nenápadný JavaScript zabraňuje vstřikování vloženého JavaScriptu do HTML. Díky tomu je váš KÓD HTML menší a méně přeplněný a usnadňuje výměnu nebo přizpůsobení knihoven JavaScriptu. Pomocníci ověření v MVC `jQueryValidate` 3 také používat plugin ve výchozím nastavení. Pokud chcete chování MVC 2, můžete zakázat nenápadný JavaScript pomocí nastavení souboru *web.config.* Další informace o vylepšeních jazyka JavaScript a Ajax naleznete v následujících zdrojích:

- [Základní úvod do nenápadného JavaScriptu na webu Wikipedie](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson je nenápadný JavaScript post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson je nenápadný JavaScript Validační příspěvek](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Vytvoření Aplikace MVC 3 s břitvou a nenápadným JavaScriptem](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (návod na ASP.NET stránkách)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Ověřování na straně klienta je ve výchozím nastavení povoleno

V dřívějších verzích MVC je třeba `Html.EnableClientValidation` explicitně volat metodu ze zobrazení, aby bylo možné ověření na straně klienta. V MVC 3 to již není nutné, protože ověření na straně klienta je ve výchozím nastavení povoleno. (Tuto funkci můžete zakázat pomocí nastavení v souboru *web.config.)*

Aby ověření na straně klienta fungovalo, musíte na příslušných knihovnách jQuery a jQuery Validation na vašem webu odkazovat. Tyto knihovny můžete hostovat na vlastním serveru nebo na ně odkazovat ze sítě pro doručování obsahu (CDN), jako jsou sítě CDN od společnosti Microsoft nebo Google.

### <a name="remote-validator"></a>Vzdálený validátor

ASP.NET MVC 3 podporuje novou třídu [RemoteAttribute,](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) která umožňuje využít výhod podpory vzdáleného validátoru modulu plug-in pro ověření dotazu. To umožňuje knihovně ověření na straně klienta automaticky volat vlastní metodu, kterou definujete na serveru, aby bylo možné provést ověřovací logiku, kterou lze provést pouze na straně serveru.

V následujícím příkladu `Remote` atribut určuje, že ověření klienta zavolá akci pojmenovanou `UserNameAvailable` ve `UsersController` třídě za účelem `UserName` ověření pole.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

Následující příklad ukazuje odpovídající řadič.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Další informace o použití `Remote` atributu naleznete v tématu [How to: Implement vzdálené ověření v ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) v knihovně MSDN.

### <a name="json-binding-support"></a>Podpora vazby JSON

ASP.NET MVC 3 obsahuje integrovanou podporu vazeb JSON, která umožňuje metody akce přijímat data kódovaná jsonem a vázat je na parametry metody akce. Tato funkce je užitečná ve scénářích zahrnujících šablony klientů a datové vazby. (Šablony klienta umožňují formátovat a zobrazit jednu datovou položku nebo sadu datových položek pomocí šablon, které se provádějí v klientovi.) MVC 3 umožňuje snadno připojit klientské šablony s metodami akce na serveru, které odesílají a přijímají data JSON. Další informace o podpoře vazeb JSON naleznete v části **JavaScript a AJAX Improvements** v [příspěvku blogu MVC 3 preview Scotta Guthrieho](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Vylepšení ověření modelu

### <a name="dataannotations-metadata-attributes"></a>Atributy metadat DataAnnotations

ASP.NET MVC `DataAnnotations` 3 podporuje atributy `DisplayAttribute`metadat, například .

### <a name="validationattribute-class"></a>Třída "ValidationAttribute"

Třída `ValidationAttribute` byla vylepšena v rozhraní .NET `IsValid` Framework 4 pro podporu nové přetížení, které poskytuje další informace o aktuální kontext ověření, například jaký objekt je ověřován. To umožňuje bohatší scénáře, kde můžete ověřit aktuální hodnotu na základě jiné vlastnosti modelu. Nový `CompareAttribute` atribut například umožňuje porovnat hodnoty dvou vlastností modelu. V následujícím příkladu `ComparePassword` musí vlastnost `Password` odpovídat poli, aby byla platná.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Ověřovací rozhraní

[Rozhraní IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) umožňuje provádět ověření na úrovni modelu a umožňuje poskytovat chybové zprávy ověření, které jsou specifické pro stav celkového modelu nebo mezi dvěma vlastnostmi v rámci modelu. MVC 3 nyní načítá `IValidatableObject` chyby z rozhraní při vazbě modelu a automaticky označí nebo zvýrazní ovlivněná pole v zobrazení pomocí předdefinovaných pomocníků formuláře HTML.

[Rozhraní IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) umožňuje ASP.NET MVC zjistit za běhu, zda validátor má podporu pro ověření klienta. Toto rozhraní bylo navrženo tak, aby bylo možné jej integrovat s různými ověřovacími rámci.

Další informace o ověřovacích rozhraních naleznete v části **Vylepšení ověřování modelu** v [příspěvku blogu MVC 3 aplikace Scott Guthrie .](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) (Všimněte si však, že odkaz na "IValidateObject" v blogu by měl být "IValidatableObject".)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Vylepšení vkládání závislostí

ASP.NET MVC 3 poskytuje lepší podporu pro použití vkládání závislostí (DI) a pro integraci s kontejnery vkládání závislostí nebo inverze řízení (IOC). Podpora pro DI byla přidána v těchto oblastech:

- Regulátory (registrace a vstřikování řadičů, vstřikovací regulátory).
- Zobrazení (registrace a vkládání modulů zobrazení, vkládání závislostí do zobrazení stránek).
- Akční filtry (vyhledání a vstřikování filtrů).
- Modelová pojiva (registrace a injektáž).
- Poskytovatelé ověření modelu (registrace a vkládání).
- Zprostředkovatelé metadat modelu (registrace a vkládání).
- Poskytovatelé hodnot (registrace a injekční aplikace).

MVC 3 podporuje [knihovnu Common Service Locator](https://github.com/unitycontainer/commonservicelocator) a jakýkoli `IServiceLocator` kontejner DI, který podporuje rozhraní této knihovny. Podporuje také nové `IDependencyResolver` rozhraní, které usnadňuje integraci architektur DI.

Další informace o DI v MVC 3 naleznete v následujících zdrojích:

- [Brad Wilson série blogu na umístění služby](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Další nové funkce

### <a name="nuget-integration"></a>Integrace NuGet

ASP.NET MVC 3 automaticky nainstaluje a povolí NuGet jako součást jeho nastavení. NuGet je bezplatný open source správce balíčků, který usnadňuje hledání, instalaci a používání knihoven a nástrojů .NET ve vašich projektech. Pracuje se všemi typy projektů sady Visual Studio (včetně ASP.NET webových formulářů a ASP.NET MVC).

NuGet umožňuje vývojářům, kteří udržují open source projekty (například projekty jako Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks a Elmah) zabalit své knihovny a zaregistrovat je v online galerii. Je pak snadné pro vývojáře rozhraní .NET, kteří chtějí použít jednu z těchto knihoven k nalezení balíčku a jeho instalaci do projektů, na kterých pracují.

S ASP.NET 3 Tools Update, šablony projektu patří JavaScript knihovny předinstalované Balíčky NuGet, takže jsou aktualizovatelné přes NuGet. Entity Framework Code First je také předinstalovaný jako balíček NuGet.

Další informace o NuGet naleznete v [dokumentaci NuGet](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Ukládání výstupu částečné stránky do mezipaměti

ASP.NET MVC podporuje ukládání odpovědí na celou stránku od verze 1 do mezipaměti. MVC 3 také podporuje ukládání do mezipaměti výstupu s částečnou stránkou, což umožňuje snadno ukládat do mezipaměti oblasti nebo fragmenty odpovědi. Další informace o ukládání do mezipaměti naleznete v části **Částečné ukládání výstupu stránky do mezipaměti** blogu [Scotta Guthrieho na kandidátovi na vydání MVC 3](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) a v části Ukládání výstupu dítěte do **mezipaměti** [v poznámkách k verzi MVC 3](../whitepapers/mvc3-release-notes.md).

### <a name="granular-control-over-request-validation"></a>Podrobná kontrola nad ověřením požadavku

ASP.NET MVC má integrované ověření požadavků, které automaticky pomáhá chránit před útoky xss a HTML injektáží. Někdy však chcete explicitně zakázat ověření žádosti, například pokud chcete uživatelům pokázat obsah HTML (například v položkách blogu nebo obsahu CMS). Nyní můžete přidat [Atribut AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) do modelů nebo zobrazit modely zakázat ověření požadavku na základě vlastnosti během vazby modelu. Další informace o ověření žádosti naleznete v následujících zdrojích:

- **Nenápadný JavaScript a ověření** sekce v [blogu Scott Guthrie na MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Rozšiřitelné dialogové okno Nový projekt

V ASP.NET MVC 3 můžete přidat šablony projektu, zobrazit motory a rozhraní projektu testování částí do dialogového okna **Nový projekt.**

### <a name="template-scaffolding-improvements"></a>Vylepšení šablonového lešení

ASP.NET šablony lešení MVC 3 lépe identifikují vlastnosti primárního klíče u modelů a vhodně s nimi manipulují než v předchozích verzích MVC. (Například šablony lešení nyní ujistěte se, že primární klíč není skládaný jako upravitelné pole formuláře.)

Ve výchozím nastavení vytvořit a upravit veselací lišty nyní používají `Html.EditorFor` pomocníka namísto pomocníka. `Html.TextBoxFor` To zlepšuje podporu metadat v modelu ve formě atributů anotace dat, když dialogové okno **Přidat zobrazení** generuje zobrazení.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>New Overloads for "Html.LabelFor" a "Html.LabelForModel"

Pro `LabelFor` pomocné `LabelForModel` metody byly přidány nové přetížení metody. Nová přetížení umožňují určit nebo přepsat text popisku.

### <a name="sessionless-controller-support"></a>Podpora řadiče bez sessionless

V ASP.NET MVC 3 můžete určit, zda chcete, aby třída řadiče používala stav relace, a pokud ano, zda má být stav relace jen pro čtení nebo zápis. Další informace o podpoře řadiče bez relace naleznete v [tématu MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Nová třída "AdditionalMetadataAttribute"

Atribut [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) můžete použít k `ModelMetadata.AdditionalValues` naplnění slovníku pro vlastnost modelu. Pokud má například model zobrazení vlastnost, která by měla být zobrazena pouze správci, můžete tuto vlastnost opatří poznámkami, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Tato metadata jsou k dispozici pro libovolnou šablonu zobrazení nebo editoru při vykreslení modelu zobrazení výrobku. Je na vás, abyste vyložili informace o metadatech.

### <a name="accountcontroller-improvements"></a>Vylepšení accountcontroller

AccountController v šabloně projektu Internetu byla výrazně vylepšena.

### <a name="new-intranet-project-template"></a>Nová intranetová šablona projektu

Je zahrnuta nová intranetová šablona projektu, která umožňuje ověřování systému Windows a odebere AccountController.
