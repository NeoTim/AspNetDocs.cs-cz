---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET a webové nástroje pro poznámky k verzi sady Visual Studio 2013 | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET a webových nástrojů pro Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543493"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>ASP.NET a webové nástroje pro Visual Studio 2013 – poznámky k verzi

podle [společnosti Microsoft](https://github.com/microsoft)

> Tento dokument popisuje vydání ASP.NET a webových nástrojů pro Visual Studio 2013.

## <a name="contents"></a>Obsah

- [Poznámky k instalaci](#TOC1)
- [Dokumentace](#TOC2)
- [Požadavky na software](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Nové funkce v ASP.NET a webových nástrojích pro Visual Studio 2013

- [Jedna ASP.NET](#TOC6)
- [Nové prostředí webového projektu](#newproj)
- [ASP.NET lešení](#scaffold)
- [Browser Link](#browser-link)
- [Vylepšení webového editoru sady Visual Studio](#web-editor)
- [Podpora webových aplikací služby Azure App Service ve Visual Studiu](#waws)
- [Vylepšení publikování webu](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET – webové formuláře](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [Rozhraní API pro ASP.NET Web 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Součásti Microsoft OWIN](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Břitva 3](#TOC14)
- [ASP.NET pozastavení aplikace](#TOC15)
- [Známé problémy a nejnovější změny](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET a webových nástrojů pro Visual Studio 2013 jsou dodávány v hlavním instalačním programu a lze je stáhnout [zde](https://www.asp.net/downloads).

<a id="TOC2"></a>
## <a name="documentation"></a>Dokumentace

Výukové programy a další informace o ASP.NET a webových nástrojích pro visual studio 2013 jsou k dispozici na [webu ASP.NET](https://www.asp.net/).

<a id="TOC4"></a>
## <a name="software-requirements"></a>Požadavky na software

ASP.NET a webových nástrojů vyžaduje Visual Studio 2013.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Nové funkce v ASP.NET a webových nástrojích pro Visual Studio 2013

Následující části popisují funkce, které byly zavedeny ve verzi.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Jedna ASP.NET

S vydáním Visual Studia 2013 jsme udělali krok ke sjednocení prostředí s používáním ASP.NET technologií, takže můžete snadno kombinovat ty, které chcete. Můžete například zahájit projekt pomocí mvc a snadno přidat stránky webových formulářů do projektu později nebo ve windows web oválná síť API v projektu webových formulářů. Jedním ASP.NET je především o tom, aby bylo pro vás jako vývojáře snazší dělat věci, které máte rádi v ASP.NET. Bez ohledu na to, jakou technologii si vyberete, můžete mít jistotu, že stavíte na důvěryhodném základním rámci One ASP.NET.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Nové prostředí webového projektu

Vylepšili jsme možnosti vytváření nových webových projektů v sadě Visual Studio 2013. V dialogovém **okně Nový ASP.NET webový projekt** můžete vybrat požadovaný typ projektu, nakonfigurovat libovolnou kombinaci technologií (webové formuláře, MVC, webové rozhraní API), nakonfigurovat možnosti ověřování a přidat projekt testování částí.

![Nový projekt ASP.NET](release-notes/_static/image1.png)

Nové dialogové okno umožňuje změnit výchozí možnosti ověřování pro mnoho šablon. Pokud například vytvoříte projekt ASP.NET webových formulářů, můžete vybrat některou z následujících možností:

- Bez ověřování
- Individuální uživatelské účty (ASP.NET členství nebo přihlášení poskytovatele mno žití)
- Organizační účty (Služba Active Directory v internetové aplikaci)
- Ověřování systému Windows (služba Active Directory v intranetové aplikaci)

![Možnosti ověřování](release-notes/_static/image2.png)

Další informace o novém procesu vytváření webových projektů naleznete [v tématu Vytváření ASP.NET webových projektů v sadě Visual Studio 2013](creating-web-projects-in-visual-studio.md). Další informace o nových možnostech ověřování naleznete [v tématu ASP.NET identity](#TOC8) dále v tomto dokumentu.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET lešení

ASP.NET generování uživatelského rozhraní je rozhraní pro generování kódu pro ASP.NET webových aplikací. Usnadňuje přidání často používaný kód do projektu, který spolupracuje s datovým modelem.

V předchozích verzích sady Visual Studio bylo lešení omezeno na ASP.NET projekty MVC. V sadě Visual Studio 2013 teď můžete používat přisychávací období pro všechny ASP.NET projektu, včetně webových formulářů. Visual Studio 2013 aktuálně nepodporuje generování stránek pro projekt webových formulářů, ale stále můžete použít generování uživatelského formuláře s webovými formuláři přidáním závislostí MVC do projektu. Podpora generování stránek pro webové formuláře bude přidána v budoucí aktualizaci.

Při použití uživatelského přilechrápění zajišťujeme, že jsou v projektu nainstalovány všechny požadované závislosti. Pokud například začnete s projektem ASP.NET webových formulářů a potom pomocí uživatelského rozhraní přidáte řadič webového rozhraní API, budou do projektu automaticky přidány požadované balíčky nuget a odkazy.

Chcete-li přidat uživatelské rozhraní MVC do projektu webových formulářů, přidejte **novou položku scaffolded a** v dialogovém okně vyberte **závislosti MVC 5.** Existují dvě možnosti pro lešení MVC; Minimální a plná. Pokud vyberete Minimální, do projektu se přidají pouze balíčky NuGet a odkazy pro ASP.NET MVC. Pokud vyberete možnost Úplné, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.

Podpora asynchronních řadičů lešení používá nové asynchronní funkce z entity Framework 6.

Další informace a kurzy naleznete [v tématu ASP.NET Přehled lešení](aspnet-scaffolding-overview.md).

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Odkaz na prohlížeč – kanál SignalR mezi prohlížečem a visual studio

Nová funkce [Odkaz prohlížeče](using-browser-link.md) umožňuje připojit více prohlížečů k sadě Visual Studio a aktualizovat je všem klepnutím na tlačítko na panelu nástrojů. K vývojovému webu můžete připojit více prohlížečů, včetně mobilních emulátorů, a kliknutím na aktualizovat aktualizovat všechny prohlížeče najednou. Odkaz prohlížeče také zveřejňuje rozhraní API, které vývojářům umožňuje psát rozšíření odkazu prohlížeče.

![](release-notes/_static/image3.png)

Povolením vývojářům využít rozhraní API odkazu prohlížeče, je možné vytvořit velmi pokročilé scénáře, které překračuje hranice mezi Visual Studio a libovolný prohlížeč, který je připojen. Web Essentials využívá rozhraní API k vytvoření integrovaného prostředí mezi aplikací Visual Studio a vývojářskými nástroji prohlížeče, vzdálenými mobilními emulátory a mnoha dalšími.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Vylepšení webového editoru sady Visual Studio

Visual Studio 2013 obsahuje nový editor HTML pro soubory Razor a soubory HTML ve webových aplikacích. Nový editor HTML poskytuje jedno jednotné schéma založené na HTML5. Má automatické dokončení ortézy, jQuery UI a AngularJS atribut IntelliSense, atribut IntelliSense Seskupení, ID a název třídy Intellisense a další vylepšení, včetně lepšího výkonu, formátování a SmartTags.

Následující snímek obrazovky ukazuje použití bootstrap atribut IntelliSense v editoru HTML.

![Intellisense v editoru HTML](release-notes/_static/image4.png)

Visual Studio 2013 také přichází s vestavěnými editory CoffeeScript a LESS. Méně editor je dodáván se všemi skvělými funkcemi z editoru CSS a má specifický Intellisense pro proměnné a mixiny ve všech dokumentech LESS v řetězci. @import

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Podpora webových aplikací služby Azure App Service ve Visual Studiu

Ve Visual Studiu 2013 s sadou Azure SDK pro .NET 2.2 můžete pomocí **Průzkumníka serveru** pracovat přímo se vzdálenými webovými aplikacemi. Můžete se přihlásit ke svému účtu Azure, vytvářet nové webové aplikace, konfigurovat aplikace, zobrazovat protokoly v reálném čase a další. Brzy po vydání sady SDK 2.2 budete moct běžet v režimu ladění vzdáleně v Azure. Většina nových funkcí pro Azure App Service Web Apps funguje taky ve Visual Studiu 2012 při instalaci aktuální verze sady Azure SDK pro .NET.

Další informace najdete v následujících materiálech:

- [Vytvoření webové aplikace ASP.NET ve službě Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Poradce při potížích s webovou aplikací ve službě Azure App Service pomocí Visual Studia](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Vylepšení publikování webu

Visual Studio 2013 obsahuje nové a vylepšené funkce publikování webu. Zde je několik z nich:

- Snadno [automatizujte šifrování souborů Web.config](https://go.microsoft.com/fwlink/?LinkId=325529). (Tento odkaz a následující dva bod dokumentace na MSDN, které nemusí být k dispozici až pozdě v den na 10/17.)
- Snadno [automatizujte přepychaplikace aplikace během nasazení](https://go.microsoft.com/fwlink/?LinkId=325530).
- Nakonfigurujte nasazení webu tak, aby [místo naposledy změněného data](https://go.microsoft.com/fwlink/?LinkId=325531) používalo kontrolní součet souborů pro určení, které soubory mají být zkopírovány na server.
- Rychle publikujte jednotlivé vybrané soubory (včetně web.config) při použití metod publikování ftp nebo systému souborů a také při nasazení webu.

Další informace o nasazení ASP.NET webu naleznete [na webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány na [NuGet 2.7 Poznámky k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Tato verze NuGet také odstraňuje potřebu poskytnout výslovný souhlas pro nuget je funkce obnovení balíčku ke stažení balíčky. Souhlas (a přidružené zaškrtávací políčko v dialogu předvoleb NuGet) je nyní udělena instalací NuGet. Nyní balíček obnovit prostě funguje ve výchozím nastavení.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

### <a name="one-aspnet"></a>Jedna ASP.NET

Šablony projektů Webových formulářů se bezproblémově integrují s novým prostředím One ASP.NET. Do projektu webových formulářů můžete přidat podporu mvc a webového rozhraní API a ověřování můžete nakonfigurovat pomocí průvodce vytvořením projektu One ASP.NET. Další informace naleznete v [tématu Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Šablony projektu Webových formulářů podporují novou architekturu identity ASP.NET. Kromě toho šablony nyní podporují vytvoření intranetového projektu webových formulářů. Další informace naleznete v [tématu Metody ověřování](creating-web-projects-in-visual-studio.md#auth) v **tématu Creating ASP.NET Web Projects in Visual Studio 2013**.

### <a name="bootstrap"></a>Bootstrap

Šablony webových formulářů používají [Bootstrap](http://twitter.github.io/bootstrap/) k zajištění elegantního a citlivého vzhledu a pocitu, který můžete snadno přizpůsobit. Další informace najdete [v tématu Bootstrap v šablonách webového projektu sady Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Jedna ASP.NET

Šablony projektu Web MVC se bezproblémově integrují s novým prostředím One ASP.NET. Projekt MVC můžete přizpůsobit a nakonfigurovat ověřování pomocí průvodce vytvořením projektu One ASP.NET. Úvodní výukový program pro ASP.NET MVC 5 lze nalézt na [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

Informace o inovaci projektů MVC 4 na MVC 5 naleznete [v tématu Jak upgradovat ASP.NET mvc 4 a projekt webového rozhraní API pro ASP.NET MVC 5 a Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Šablony projektu MVC byly aktualizovány tak, aby používaly ASP.NET identity pro ověřování a správu identit. Výukový program s ověřováním na Facebooku a Google a novým rozhraním API pro členství najdete na stránce [Vytvoření aplikace ASP.NET MVC 5 s Facebookem a Google OAuth2 a přihlášením k OpenID](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) a [vytvoření ASP.NET aplikace MVC s auth a SQL DB a nasazení mapp služby Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).

### <a name="bootstrap"></a>Bootstrap

Šablona projektu MVC byla aktualizována tak, aby používala [Bootstrap,](http://getbootstrap.com/) aby poskytovala elegantní a citlivý vzhled a pocit, který můžete snadno přizpůsobit. Další informace najdete [v tématu Bootstrap v šablonách webového projektu sady Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Filtry ověřování

Filtry ověřování jsou nový druh filtru v ASP.NET MVC, které běží před filtry autorizace v kanálu ASP.NET MVC a umožňují zadat logiku ověřování na akci, na řadič nebo globálně pro všechny řadiče. Ověřování filtruje pověření procesu v požadavku a poskytují odpovídající objekt zabezpečení. Filtry ověřování mohou také přidávat výzvy ověřování v reakci na neoprávněné požadavky.

### <a name="filter-overrides"></a>Přepsání filtru

Nyní můžete přepsat, které filtry platí pro danou metodu akce nebo kontroleru zadáním přepsání filtru. Přepsání filtrů určuje sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo řadič). To umožňuje konfigurovat filtry, které platí globálně, ale pak vyloučit určité globální filtry z použití na konkrétní akce nebo řadiče.

### <a name="attribute-routing"></a>Směrování atributů

ASP.NET MVC nyní podporuje atribut směrování, a to díky [http://attributerouting.net](http://attributerouting.net)příspěvku Tim McCall, autor . Pomocí směrování atributů můžete zadat trasy anotací vašich akcí a kontrolorů.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>Rozhraní API pro ASP.NET Web 2

### <a name="attribute-routing"></a>Směrování atributů

ASP.NET Web API nyní podporuje směrování atributů, [http://attributerouting.net](http://attributerouting.net)a to díky příspěvku TimMcCall, autor . Pomocí směrování atributů můžete zadat trasy webového rozhraní API tak, že opatříte své akce a ovladače takto:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

Směrování atributů poskytuje větší kontrolu nad identifikátory URI ve webovém rozhraní API. Hierarchii prostředků můžete například snadno definovat pomocí jediného řadiče rozhraní API:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

Směrování atributů také poskytuje vhodnou syntaxi pro určení volitelných parametrů, výchozích hodnot a omezení trasy:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Další informace o směrování atributů naleznete [v tématu Směrování atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).

### <a name="oauth-20"></a>OAuth 2.0

Šablony projektu webového rozhraní API a jednostránkové aplikace nyní podporují autorizaci pomocí oauth 2.0. OAuth 2.0 je rámec pro autorizaci přístupu klienta k chráněným prostředkům. Funguje to pro různé klienty, včetně prohlížečů a mobilních zařízení.

Podpora pro OAuth 2.0 je založena na novém bezpečnostním middlewaru poskytovaném komponentami Microsoft OWIN pro ověřování nosičů a implementaci role autorizačního serveru. Alternativně lze klienty autorizovat pomocí autorizačního serveru organizace, jako je Azure Active Directory nebo ADFS v systému Windows Server 2012 R2.

### <a name="odata-improvements"></a>Vylepšení OData

**Podpora pro $select, $expand, $batch a $value**

ASP.NET Web API OData má nyní plnou podporu pro $select, $expand a $value. Můžete také použít $batch pro dávkování požadavků a zpracování sad změn.

Volby $select a $expand umožňují změnit tvar dat vrácených z koncového bodu OData. Další informace naleznete [v tématu Představujeme $select a $expand podporu ve webovém rozhraní API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).

**Lepší rozšiřitelnost**

OData formatters jsou nyní rozšiřitelné. Můžete přidat metadata položky Atom, podporovat pojmenované položky datových proudů a mediálních odkazů, přidávat poznámky instancí a přizpůsobit způsob generování odkazů.

**Podpora bez typů**

Nyní můžete vytvářet služby OData bez nutnosti definovat typy CLR pro typy entit. Místo toho vaše řadiče OData můžete trvat nebo vrátit instance **IEdmObject**, které jsou OData formatters serializovat/deserializovat.

**Opětovné použití existujícího modelu**

Pokud již máte existující datový model entity (EDM), můžete jej nyní znovu použít přímo, místo toho, abyste museli vytvořit nový. Například pokud používáte entity Framework, můžete použít EDM, který EF staví pro vás.

### <a name="request-batching"></a>Dávkování požadavku

Dávkování požadavku kombinuje více operací do jednoho požadavku HTTP POST, aby se snížil síťový provoz a poskytlo hladší a méně upovídané uživatelské rozhraní. ASP.NET webové rozhraní API nyní podporuje několik strategií pro dávkování požadavků:

- Použijte $batch koncový bod služby OData.
- Balíček více požadavků do jednoho vícedílného požadavku MIME.
- Použijte vlastní formát dávkování.

Chcete-li povolit dávkování požadavků, jednoduše přidejte do konfigurace webového rozhraní API trasu s obslužnou rutinou dávkování:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Můžete také řídit, zda požadavky nebo provedeny postupně nebo v libovolném pořadí.

### <a name="portable-aspnet-web-api-client"></a>Přenosný ASP.NET webový klient API

Nyní můžete pomocí ASP.NET webového rozhraní API vytvářet přenosné knihovny tříd, které fungují v aplikacích pro Windows Store a Windows Phone 8. Můžete také vytvořit přenosné formatters, které lze sdílet mezi klientem a serverem.

### <a name="improved-testability"></a>Vylepšená testovatelnost

Webové rozhraní API 2 usnadňuje testování částí řadičů rozhraní API. Stačí vytvořit instanci řadiče rozhraní API pomocí zprávy požadavku a konfigurace a potom zavolat metodu akce, kterou chcete otestovat. Je také snadné zesměšňovat **UrlHelper** třídy, pro metody akce, které provádějí generování propojení.

### <a name="ihttpactionresult"></a>IhttpActionResult

Nyní můžete implementovat IHttpActionResult zapouzdřit výsledek metody akce webového rozhraní API. IHttpActionResult vrácený z metody akce webového rozhraní API je proveden ASP.NET zaběhu webového rozhraní API k vytvoření výsledné zprávy odpovědi. IHttpActionResult lze vrátit z libovolné akce webového rozhraní API pro zjednodušení testování částí implementace webového rozhraní API. Pro pohodlí je po vybalení z krabice k dispozici řada implementací IHttpActionResult včetně výsledků pro vrácení konkrétních stavových kódů, formátovaného obsahu nebo odpovědí vyjednaných obsahem.

### <a name="httprequestcontext"></a>HttpRequestContext

Nový **HttpRequestContext** sleduje jakýkoli stav, který je vázán na požadavek, ale není okamžitě k dispozici z požadavku. Můžete například použít **HttpRequestContext** k získání dat trasy, jistiny přidružené k požadavku, klientského certifikátu, **UrlHelper** a kořenové virtuální cesty. Můžete snadno vytvořit **HttpRequestContext** pro účely testování částí.

Vzhledem k tomu, že objekt zabezpečení pro požadavek je tok s požadavkem namísto spoléhání se na **Thread.CurrentPrincipal**, jistiny je nyní k dispozici po celou dobu životnosti požadavku, zatímco je v kanálu webového rozhraní API.

### <a name="cors"></a>CORS

Díky dalšímu skvělému příspěvku brocka Allena nyní ASP.NET plně podporuje Sdílení žádostí o cross origin (CORS).

Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu. [CORS](http://www.w3.org/TR/cors/) je standard W3C, který umožňuje serveru uvolnit zásady stejného původu. Pomocí CORS server může explicitně povolit některé požadavky napříč původy při odmítnutí jiných.

Webové rozhraní API 2 nyní podporuje CORS, včetně automatického zpracování požadavků kontroly před výstupem. Další informace naleznete [v tématu Povolení požadavků na příčný původ v ASP.NET webovérozhraní API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).

### <a name="authentication-filters"></a>Filtry ověřování

Filtry ověřování jsou nový druh filtru v ASP.NET webovérozhraní API, které běží před filtry autorizace v kanálu webového rozhraní API ASP.NET a umožňují zadat logiku ověřování pro každou akci, na řadič nebo globálně pro všechny řadiče. Ověřování filtruje pověření procesu v požadavku a poskytují odpovídající objekt zabezpečení. Filtry ověřování mohou také přidávat výzvy ověřování v reakci na neoprávněné požadavky.

### <a name="filter-overrides"></a>Přepsání filtru

Nyní můžete přepsat, které filtry platí pro danou metodu akce nebo řadič, zadáním přepsání filtru. Přepsání filtrů určuje sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo řadič). To umožňuje přidat globální filtry, ale potom vyloučit některé z konkrétních akcí nebo řadičů.

### <a name="owin-integration"></a>Integrace OWIN

ASP.NET Web API nyní plně podporuje OWIN a lze jej spustit na libovolném hostiteli schopném OWIN. Součástí je také **filtr HostAuthenticationFilter,** který poskytuje integraci se systémem ověřování OWIN.

S integrací OWIN můžete samoobslužné webové rozhraní API ve vlastním procesu spolu s dalšími middleware OWIN, jako je SignalR. Další informace naleznete [v tématu Použití rozhraní OWIN k vlastnímu hostiteli ASP.NET webovérozhraní API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

Následující části popisují funkce signalr 2.0.

- [Postaveno na OWIN](#builtonowin)
- [MapHubs a MapConnection jsou nyní MapSignalR](#MapSignalR)
- [Podpora mezi doménami](#crossdomain)
- [Podpora iOS a Android přes MonoTouch a MonoDroid](#mobile)
- [Přenosný klient .NET](#portable)
- [Nový balíček samohostitele](#selfhost)
- [Zpětně kompatibilní podpora serveru](#backwardcompat)
- [Byla odebrána podpora serveru pro rozhraní .NET 4.0](#remove40)
- [Odeslání zprávy seznamu klientů a skupin](#messagelist)
- [Odeslání zprávy konkrétnímu uživateli](#sendtouser)
- [Lepší podpora zpracování chyb](#errorhandling)
- [Snadnější testování částí hubů](#unittesting)
- [Zpracování chyb javascriptu](#javascripterror)

Příklad upgradu existujícího projektu 1.x na SignalR 2.0 naleznete v [tématu Upgrade signalr 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>Postaveno na OWIN

SignalR 2.0 je kompletně postaven na [OWIN (Otevřené webové rozhraní pro .NET)](http://owin.org/). Tato změna umožňuje proces nastavení signalr mnohem konzistentnější mezi webhostované a samostatně hostované aplikace SignalR, ale také vyžaduje řadu změn rozhraní API.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs a MapConnection jsou nyní MapSignalR

Z důvodu kompatibility se standardy OWIN `MapSignalR`byly tyto metody přejmenovány na . `MapSignalR`volána bez parametrů bude mapovat `MapHubs` všechny rozbočovače (stejně jako ve verzi 1.x); chcete-li mapovat jednotlivé objekty **PersistentConnection,** zadejte typ připojení jako parametr typu a rozšíření adresy URL pro připojení jako první argument.

Metoda `MapSignalR` je volána ve třídě spuštění Owin. Visual Studio 2013 obsahuje novou šablonu pro spouštěcí třídu Owin; Chcete-li použít tuto šablonu, postupujte takto:

1. Klikněte pravým tlačítkem myši na projekt
2. Vybrat **přidat**, **novou položku...**
3. Vyberte **třídu Owin Startup**. Pojmenujte novou třídu **Startup.cs**.

Ve **webové aplikaci** je pak do `MapSignalR` Owinova spouštěcího procesu přidána třída spuštění Owin pomocí položky v uzlu nastavení aplikace souboru Web.Config, jak je znázorněno níže.

V **samoobslužné aplikaci**je třída Startup předána jako parametr typu `WebApp.Start` metody.

**Mapování rozbočovačů a připojení v SignalR 1.x (z globálního souboru aplikace ve webové aplikaci):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**Mapování rozbočovačů a připojení v SignalR 2.0 (ze souboru třídy Owin Startup):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

V **samoobslužné aplikaci**je třída Startup předána jako parametr typu pro metodu, `WebApp.Start` jak je znázorněno níže.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Podpora mezi doménami

V SignalR 1.x byly požadavky mezi doménami řízeny jedním příznakem EnableCrossDomain. Tento příznak řídil požadavky JSONP i CORS. Pro větší flexibilitu byla veškerá podpora CORS odebrána ze serverové součásti SignalR (javascriptoví klienti stále používají CORS normálně, pokud je zjištěno, že prohlížeč podporuje) a pro podporu těchto scénářů byl zpřístupněn nový middleware OWIN.

V SignalR 2.0, Pokud JSONP je požadováno na straně klienta (pro podporu požadavků mezi doménami `HubConfiguration` ve `true`starších prohlížečích), bude nutné povolit explicitně nastavením `EnableJSONP` na objekt , jak je znázorněno níže. JSONP je ve výchozím nastavení zakázán, protože je méně bezpečný než CORS.

Chcete-li přidat nový middleware CORS v SignalR 2.0, přidejte knihovnu `Microsoft.Owin.Cors` do projektu a zavolejte `UseCors` před middleware SignalR, jak je znázorněno v části níže.

**Přidání programu Microsoft.Owin.Cors do projektu**: Chcete-li nainstalovat tuto knihovnu, spusťte v konzole Správce balíčků následující příkaz:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Tento příkaz přidá verzi balíčku 2.0.0 do projektu.

**Volání UseCors**

Následující fragmenty kódu ukazují, jak implementovat připojení mezi doménami v signalr 1.x a 2.0.

**Implementace požadavků mezi doménami v SignalR 1.x (z globálního souboru aplikace)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**Implementace požadavků mezi doménami v signalr 2.0 (ze souboru kódu Jazyka C#)**

Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu SignalR 2.0. Tato ukázka `Map` `RunSignalR` kódu `MapSignalR`používá a místo , tak, aby middleware CORS běží pouze pro požadavky SignalR, které `MapSignalR`vyžadují podporu CORS (spíše než pro všechny provozy na cestě určené v .) `Map` lze také použít pro jakýkoli jiný middleware, který je třeba spustit pro konkrétní předponu URL, spíše než pro celou aplikaci.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>Podpora iOS a Android přes MonoTouch a MonoDroid

Byla přidána podpora pro klienty iOS a Android pomocí komponent MonoTouch a MonoDroid z [knihovny Xamarin](https://xamarin.com/). Další informace o jejich použití naleznete v tématu [Použití součástí Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln). Tyto součásti budou k dispozici v [obchodě Xamarin,](https://store.xamarin.com/) jakmile bude k dispozici verze SignalR RTW.

<a id="portable"></a>### Přenosný klient .NET

Pro lepší usnadnění vývoje napříč platformami byli klienti Silverlight, WinRT a Windows Phone nahrazeni jediným přenosným klientem .NET, který podporuje následující platformy:

- NET 4,5
- Silverlight 5
- WinRT (.NET pro aplikace pro Windows Store)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Nový balíček samohostitele

Nyní je balíček NuGet, který usnadňuje zahájení s vlastním hostitelem SignalR (aplikace SignalR, které jsou hostovány v procesu nebo jiné aplikaci, spíše než hostované na webovém serveru). Chcete-li upgradovat projekt vlastního hostitele vytvořený pomocí signalr 1.x, odeberte balíček Microsoft.AspNet.SignalR.Owin a přidejte balíček Microsoft.AspNet.SignalR.SelfHost. Další informace o tom, jak začít s balíčkem s vlastním hostitelem, naleznete [v tématu Výuka: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Zpětně kompatibilní podpora serveru

V předchozích verzích SignalR, verze balíčku SignalR používané v klientovi a server musí být identické. Za účelem podpory aplikací s tlustou klientskou službou, které by bylo obtížné aktualizovat, aplikace SignalR 2.0 nyní podporuje použití novější verze serveru se starším klientem. **Poznámka: SignalR 2.0 nepodporuje servery postavené se staršími verzemi s novějšími klienty.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>Byla odebrána podpora serveru pro rozhraní .NET 4.0

SignalR 2.0 snížil podporu pro interoperabilitu serveru s rozhraním .NET 4.0. .NET 4.5 musí být použit se servery SignalR 2.0. Stále existuje klient .NET 4.0 pro SignalR 2.0.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>Odeslání zprávy seznamu klientů a skupin

V SignalR 2.0 je možné odeslat zprávu pomocí seznamu ID klienta a skupiny. Následující fragmenty kódu ukazují, jak to provést.

**Odeslání zprávy seznamu klientů a skupin pomocí programu PersistentConnection**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Odeslání zprávy seznamu klientů a skupin pomocí hubů**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Odeslání zprávy konkrétnímu uživateli

Tato funkce umožňuje uživatelům určit, co userId je založena na IRequest prostřednictvím nového rozhraní IUserIdProvider:

**Rozhraní IUserIdProvider**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Ve výchozím nastavení bude existovat implementace, která používá IPrincipal.Identity.Name uživatele jako uživatelské jméno.

V rozbočovačích budete moci odesílat zprávy těmto uživatelům prostřednictvím nového rozhraní API:

**Použití rozhraní Clients.User API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Lepší podpora zpracování chyb

Uživatelé nyní mohou vyvolat **HubException** z libovolného vyvolání centra. Konstruktor **HubException** může trvat zprávu řetězce a objekt další data chyb. SignalR bude automaticky serializovat výjimku a odeslat klientovi, kde bude použit k odmítnutí nebo selhání vyvolání metody rozbočovače.

Zobrazit **podrobné hub výjimky** nastavení nemá žádný vliv na **HubException** odesílázpět klientovi nebo ne; je vždy odeslána.

**Kód na straně serveru demonstrující odesílání hubexception klientovi**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**Kód klienta JavaScriptu demonstrující odpověď na hubexception odeslaný ze serveru**

[!code-html[Main](release-notes/samples/sample16.html)]

**Kód klienta .NET demonstrující odpověď na hubexception odeslaný ze serveru**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Snadnější testování částí hubů

SignalR 2.0 obsahuje `IHubCallerConnectionContext` rozhraní volané na rozbočovače, které usnadňuje vytváření falešných vyvolání na straně klienta. Následující fragmenty kódu ukazují použití tohoto rozhraní s oblíbenými testovacími postroji [xUnit.net](https://github.com/xunit/xunit) a [moq](https://code.google.com/p/moq/).

**Jednotkové testování SignalR s xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Testování částí SignalR s moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>Zpracování chyb javascriptu

V SignalR 2.0 všechny chyby JavaScript zpracování zpětná volání vrátit javascriptové chybové objekty namísto nezpracovaných řetězců. To umožňuje SignalR toku bohatší informace o obslužné rutiny chyb. Můžete získat vnitřní výjimku `source` z vlastnosti chyby.

**Kód klienta JavaScriptu, který zpracovává výjimku Start.Fail**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>Nový systém členství v ASP.NET

ASP.NET Identity je nový systém členství pro ASP.NET aplikace. ASP.NET Identity usnadňuje integraci dat profilu specifického pro uživatele s daty aplikací. ASP.NET identity také umožňuje zvolit model trvalosti pro profily uživatelů ve vaší aplikaci. Data můžete uložit do databáze serveru SQL Server nebo do jiného úložiště dat, včetně úložišť dat NoSQL, jako jsou tabulky úložiště Azure. Další informace naleznete [v tématu Jednotlivé uživatelské účty](creating-web-projects-in-visual-studio.md#indauth) v **tématu vytváření ASP.NET webových projektů v sadě Visual Studio 2013**.

### <a name="claims-based-authentication"></a>Ověřování na základě deklarací

ASP.NET nyní podporuje ověřování na základě deklarací identity, kde je identita uživatele reprezentována jako sada deklarací od důvěryhodného vystavittele. Uživatele lze ověřovat pomocí uživatelského jména a hesla uchovávaných v databázi aplikací nebo pomocí poskytovatelů sociální identity (například Účty Microsoft, Facebook, Google, Twitter) nebo pomocí účtů organizace prostřednictvím služby Azure Active Directory nebo Služby ADF (ADFS).

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Integrace se službou Azure Active Directory a službou Windows Server Active Directory

Nyní můžete vytvořit ASP.NET projekty, které používají Azure Active Directory nebo Windows Server Active Directory (AD) pro ověřování. Další informace naleznete v [tématu Organizační účty](creating-web-projects-in-visual-studio.md#orgauth) v **tématu Vytváření ASP.NET webových projektů v sadě Visual Studio 2013**.

### <a name="owin-integration"></a>Integrace OWIN

ASP.NET ověřování je nyní založeno na middlewaru OWIN, který lze použít na libovolném hostiteli založeném na OWIN. Další informace o OWIN naleznete v následující části [Součásti Microsoft OWIN.](#TOC7)

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Součásti Microsoft OWIN

[Otevřené webové rozhraní pro rozhraní .NET](http://owin.org/) (OWIN) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odděluje webové aplikace od serveru, takže webové aplikace host-agnostik. Můžete například hostovat webovou aplikaci založenou na OWIN ve službě IIS nebo ji sami hostovat ve vlastním procesu.

Změny zavedené v součástech Microsoft OWIN (označované také jako projekt Katana) zahrnují nové serverové a hostitelské součásti, nové pomocné knihovny a middleware a nový ověřovací middleware.

Další informace o OWIN a Kataně najdete [v tématu Co je nového v OWIN a Kataně](../../../aspnet/overview/owin-and-katana/index.md).

**Poznámka: [Aplikace OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) nelze spustit v klasickém režimu iis. musí být provozovány v integrovaném režimu.**

**Poznámka: [Aplikace OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) musí být spuštěny v plné důvěře.**

### <a name="new-servers-and-hosts"></a>Nové servery a hostitelé

V této verzi byly přidány nové součásti, které umožňují scénáře vlastního hostitele. Mezi tyto součásti patří následující balíčky NuGet:

- **Microsoft.Owin.Host.HttpListener**. Poskytuje server OWIN, který používá **HttpListener** naslouchat požadavkům HTTP a nasměrovat je do kanálu OWIN.
- **Microsoft.Owin.Hosting** Poskytuje knihovnu pro vývojáře, kteří chtějí vlastní hostování kanálu OWIN ve vlastním procesu, jako je například konzolová aplikace nebo služba systému Windows.
- **OwinHost**. Poskytuje samostatný spustitelný soubor, `Microsoft.Owin.Hosting` který zabalí a umožňuje vlastní hostování kanálu OWIN bez nutnosti psát vlastní hostitelskou aplikaci.

Kromě toho `Microsoft.Owin.Host.SystemWeb` balíček nyní umožňuje middleware poskytovat rady **serveru SystemWeb,** označující, že middleware by měla být volána během určité ASP.NET fáze kanálu. Tato funkce je užitečná zejména pro ověřování middleware, který by měl být spuštěn v rané fázi ASP.NET kanálu.

### <a name="helper-libraries-and-middleware"></a>Pomocné knihovny a middleware

I když můžete psát komponenty OWIN pouze pomocí definice funkce a `Microsoft.Owin` typu ze specifikace OWIN, nový balíček poskytuje uživatelsky přívětivější sadu abstrakcí. Tento balíček kombinuje několik dřívějších balíčků `Owin.Extensions` `Owin.Types`(např. ,) do jednoho, dobře strukturovaného objektového modelu, který pak mohou snadno používat jiné komponenty OWIN. Ve skutečnosti většina součástí Microsoft OWIN nyní používá tento balíček.

> [!NOTE]
> [Aplikace OWIN](http://www.owin.org) nelze spustit v klasickém režimu iis. musí být provozovány v integrovaném režimu.

> [!NOTE]
> [Aplikace OWIN](http://www.owin.org) musí být spuštěny v plné důvěryhodnosti.

Tato verze také obsahuje balíček Microsoft.Owin.Diagnostics, který obsahuje middleware k ověření spuštěné aplikace OWIN, plus middleware chybové stránky, které pomáhají vyšetřovat chyby.

### <a name="authentication-components"></a>Součásti ověřování

K dispozici jsou následující součásti ověřování.

- **Adresář Microsoft.Owin.Security.ActiveDirectory**. Umožňuje ověřování pomocí místních nebo cloudových adresářových služeb.
- **Microsoft.Owin.Security.Cookies** Umožňuje ověřování pomocí souborů cookie. Tento balíček `Microsoft.Owin.Security.Forms`byl dříve pojmenován .
- **Microsoft.Owin.Security.Facebook** Umožňuje ověřování pomocí služby OAuth založené na Facebooku.
- **Microsoft.Owin.Security.Google** Umožňuje ověřování pomocí služby Založené na OpenID společnosti Google.
- **Microsoft.Owin.Security.Jwt** Umožňuje ověřování pomocí tokenů JWT.
- **Microsoft.Owin.Security.MicrosoftAccount** Umožňuje ověřování pomocí účtů Microsoft.
- **Microsoft.Owin.Security.OAuth**. Poskytuje autorizační server OAuth a middleware pro ověřování tokenů nosiče.
- **Microsoft.Owin.Security.Twitter** Umožňuje ověřování pomocí služby OAuth založené na Twitteru.

Tato verze obsahuje `Microsoft.Owin.Cors` také balíček, který obsahuje middleware pro zpracování požadavků HTTP napříč původem.

> [!NOTE]
> Podpora podepisování JWT byla odebrána v konečné verzi Sady Visual Studio 2013.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Seznam nových funkcí a další chod v rámci entity 6 naleznete v [tématu Entity Framework Version History](https://msdn.com/data/jj574253).

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Břitva 3

ASP.NET Razor 3 obsahuje následující nové funkce:

- Podpora pro úpravy tabulátoru. Dříve příkaz **Formát dokumentu,** automatické odsazení a automatické formátování v sadě Visual Studio nefungovaly správně při použití možnosti **Zachovat karty.** Tato změna opravuje Visual Studio formátování pro razor kód pro formátování karty.
- Podpora pravidel přepisování adres URL při generování odkazů.
- Odstranění transparentního atributu zabezpečení.
  > [!NOTE]
  > Jedná se o narušující změnu a razor 3 je nekompatibilní s MVC4 a starší, zatímco Razor 2 je nekompatibilní s MVC5 nebo sestavení kompilované proti MVC5.

Problémy s razorem 3 opravené v sadě Visual Studio 2013 z předběžných verzí naleznete [zde](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET pozastavení aplikace

ASP.NET App Suspend je hra měnící funkce v rozhraní .NET Framework 4.5.1, která radikálně mění uživatelské prostředí a ekonomický model pro hostování velkého počtu ASP.NET lokalit na jednom počítači. Další informace naleznete [v tématu ASP.NET App Suspend – responzivní sdílený web hosting .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a nejnovější změny

Tato část popisuje známé problémy a narušující změny v ASP.NET a webových nástrojích pro Visual Studio 2013.

### <a name="nuget"></a>NuGet

- [Nový balíček obnovení nefunguje na Mono při použití souboru SLN](https://nuget.codeplex.com/workitem/3596) – bude opravena v nadcházející nuget.exe download a [NuGet.CommandLine balíček](http://www.nuget.org/packages/NuGet.CommandLine/) aktualizace.
- [Obnovení nového balíčku nefunguje s projekty Wix](https://nuget.codeplex.com/workitem/3598) – bude opraveno v nadcházejícím stahování nuget.exe a aktualizaci [balíčku NuGet.CommandLine.](http://www.nuget.org/packages/NuGet.CommandLine/)
- [Automatické obnovení balíčků nefunguje pro projekty ve složce řešení](https://nuget.codeplex.com/workitem/3625) – bude opravena v NuGet 2.8.

### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`se nevrátí `IQueryable<T>` vždy, jak jsme `$select` přidali podporu pro a `$expand`.

    Naše dřívější `ODataQueryOptions<T>` ukázky pro vždy `ApplyTo` obsazení `IQueryable<T>`vrácená hodnota z . To fungovalo dříve, protože možnosti`$filter` `$orderby`dotazu, které jsme podporovali dříve ( , , `$skip`, `$top`) nemění tvar dotazu. Nyní, když `$select` `$expand` podporujeme a `ApplyTo` návratová `IQueryable<T>` hodnota z nebude vždy.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Pokud používáte ukázkový kód z předchozích, bude pokračovat `$select` v `$expand`práci, pokud klient neodesílá a . Pokud však chcete `$select` podporovat `$expand` a budete muset změnit tento kód na toto.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request.Url nebo RequestContext.Url má hodnotu null během dávkového požadavku.**

    Ve scénáři dávkování je **urlhelper** null při přístupu z **Request.Url** nebo **RequestContext.Url**.

    Tento problém je nyní sledován zde: [BatchRequestContext.Url je null pro dávkování požadavku](http://aspnetwebstack.codeplex.com/workitem/1301).

    Řešení tohoto problému je vytvořit novou instanci **UrlHelper**, jako v následujícím příkladu:

    **Vytvoření nové instance urlhelperu**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. Při použití MVC5 a OrgAuth, pokud máte zobrazení, která antiforgerToken ověření, můžete narazit na následující chybu při zaúčtování dat do zobrazení:

    **Chyba**:

    *Chyba serveru v aplikaci/.*

    <em>Nárok typu "<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>"<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>nebo " nebyl v poskytnuté deklaraci identity claimidentity. Chcete-li povolit podporu tokenů proti padělání s ověřováním na základě deklarací identity, ověřte, zda nakonfigurovaný poskytovatel deklarací identit y poskytuje obě tyto deklarace identity v instancích ClaimsIdentity, které generuje. Pokud nakonfigurovaný zprostředkovatel deklarací používá jako jedinečný identifikátor jiný typ deklarace identity, lze jej nakonfigurovat nastavením statické vlastnosti AntiForgeryConfig.UniqueClaimTypeIdentifier.</em>

    **Řešení**:

    Přidejte do global.asax následující řádek, abyste to opravili:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Tato oprava bude opravena pro další verzi.
2. Po upgradu aplikace MVC4 na MVC5 sestavte řešení a spusťte ho. Měla by se zobrazit následující chyba:

    [A] System.Web.WebPages.Razor.Configuration.HostSection nelze přetypovat na [B]System.Web.WebPages.Razor.Configuration.HostSection. Typ A pochází z 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' v kontextu 'Default' v\_umístění 'C:\windows\Microsoft.Net\assembly\GAC MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'. Typ B pochází z 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' v kontextu "Výchozí" v umístění C:\Windows\Microsoft.NET\Framework\v4.0.30319\Dočasné ASP.NET Soubory\root\6 d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.

    Chcete-li opravit výše uvedenou chybu, otevřete v projektu *všechny* soubory Web.config (včetně těch ve složce Zobrazení) a postupujte takto:

   1. Aktualizujte všechny výskyty verze "4.0.0.0" "System.Web.Mvc" na "5.0.0.0".
   2. Aktualizujte všechny výskyty verze &quot;"2.0.0.0" "System.Web.Helpers", System.Web.WebPages&quot; a &quot;System.Web.WebPages.Razor&quot; na "3.0.0.0"

      Například po provedené výše uvedené změny vazby sestavení by měl vypadat takto:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      Informace o inovaci projektů MVC 4 na MVC 5 naleznete [v tématu Jak upgradovat ASP.NET mvc 4 a projekt webového rozhraní API pro ASP.NET MVC 5 a Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).
3. Při použití ověření na straně klienta s jQuery Nenápadné ověření, ověřovací zpráva je někdy nesprávné pro vstupní prvek HTML s type ='number'. Chyba ověření pro požadovanou hodnotu ("Pole stáří je povinné") se zobrazí, když je zadáno neplatné číslo namísto správné zprávy, že je vyžadováno platné číslo.

    Tento problém se běžně vyskytuje s kódem scaffolded pro model s vlastností celé číslo v zobrazení vytvořit a upravit.

    Chcete-li tento problém vyřešit, změňte pomocníka editoru z:

    `@Html.EditorFor(person => person.Age)`

    Do:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 již nepodporuje částečnou důvěryhodnost. Projekty, které odkazují na binární soubory MVC nebo WebAPI, by měly odebrat atribut [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) a atribut [AllowPartiallyTrustedCallers.](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) Odebrání těchto atributů eliminuje chyby kompilátoru, jako je například následující.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Všimněte si, že jako vedlejší účinek tohoto nelze použít 4.0 a 5.0 sestavení ve stejné aplikaci. Je třeba aktualizovat všechny z nich 5.0.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Šablona SPA s autorizací facebooku může způsobit nestabilitu v aplikaci IE, zatímco web je hostován v intranetové zóně

Šablona SPA poskytuje externí přihlášení pomocí Facebooku. Pokud je projekt vytvořený pomocí šablony spuštěn místně, přihlašování může způsobit selhání aplikace IE.

Řešení:

1. Host webové stránky v internetové zóně; Nebo

2. Otestujte scénář v jiném prohlížeči než IE.

### <a name="web-forms-scaffolding"></a>Lešení webových formulářů

Webové formuláře lešení byla odebrána z VS2013 a bude k dispozici v budoucí aktualizaci sady Visual Studio. Generování uživatelského přihrádky však můžete v rámci projektu webových formulářů stále používat přidáním závislostí MVC a generováním generování generování pro mvc. Projekt bude obsahovat kombinaci webových formulářů a mvc.

Chcete-li přidat mvc do projektu webových formulářů, přidejte novou položku scaffolded a vyberte **položku Závislosti MVC 5**. Vyberte možnost Minimální nebo Úplná v závislosti na tom, zda potřebujete všechny soubory obsahu, například skripty. Potom přidejte šálací kód pro MVC, který vytvoří zobrazení a řadič v projektu.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC a webové api lešení - HTTP 404, nebyla nalezena chyba

Pokud dojde k chybě při přidávání šástavlna položky do projektu, je možné, že projekt bude ponechán v nekonzistentním stavu. Některé provedené změny se šaše budou vráceny zpět, ale jiné změny, jako jsou například nainstalované balíčky NuGet, nebudou vráceny zpět. Pokud jsou změny konfigurace směrování vráceny zpět, uživatelé obdrží chybu HTTP 404 při navigaci na položky sklopné kódy.

Alternativní řešení:

- Chcete-li opravit tuto chybu pro MVC, přidejte novou položku scaffolded a vyberte mvc 5 závislosti (minimální nebo úplné). Tento proces přidá všechny požadované změny do projektu.
- Oprava této chyby pro webové rozhraní API:

  1. Přidejte třídu WebApiConfig do projektu.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. Konfigurace webapiconfig.register v\_metodě Start aplikace v Global.asax takto:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
