---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 Autorizační server | Dokumenty společnosti Microsoft
author: hongyes
description: Tento výukový program vás provede tím, jak implementovat Autorizační server OAuth 2.0 pomocí middlewaru OWIN OAuth. Jedná se o pokročilý výukový program, který pouze outlin ...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540389"
---
<a name="owin-oauth-20-authorization-server"></a>Autorizační server OWIN OAuth 2.0
====================
podle [Hongye Sun](https://github.com/hongyes) a [Praburaj Thiagarajan](https://github.com/Praburaj)

> Tento výukový program vás provede tím, jak implementovat Autorizační server OAuth 2.0 pomocí middlewaru OWIN OAuth. Toto je pokročilý kurz, který pouze popisuje kroky k vytvoření Autorizačního serveru OWin OAuth 2.0. Toto není krok za krokem tutorial. [Stáhněte si ukázkový kód](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).
>
> > [!NOTE]
> > Tento přehled by neměl být určen k vytvoření zabezpečené produkční aplikace. Tento kurz je určen pouze přehled o tom, jak implementovat OAuth 2.0 Autorizační server pomocí MiddleWare OWIN OAuth.
>
>
> ## <a name="software-versions"></a>Verze softwaru
>
> | **Zobrazeno v tutoriálu** | **Pracuje také s** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [Visual Studio 2013 Express pro stolní počítače](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 s nejnovější aktualizací by mělo fungovat, ale kurz nebyl testován s ním a některé nabídky výběry a dialogová okna se liší. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>Otázky a komentáře
>
> Pokud máte otázky, které přímo nesouvisejí s tutoriálem, můžete je zveřejnit v [projektu Katana na GitHubu](https://github.com/aspnet/AspNetKatana/). Dotazy a komentáře týkající se samotného výukového programu naleznete v části komentáře v dolní části stránky.


Architektura [OAuth 2.0](http://tools.ietf.org/html/rfc6749) umožňuje aplikaci jiného výrobce získat omezený přístup ke službě HTTP. Namísto použití pověření vlastníka prostředku pro přístup k chráněnému prostředku získá klient přístupový token (což je řetězec označující určitý obor, životnost a další atributy přístupu). Přístupové tokeny jsou vydávány klientům třetích stran autorizačním serverem se souhlasem vlastníka prostředku.

Tento výukový program se bude týkat:

- Jak vytvořit autorizační server pro podporu čtyř typů autorizačních oprávnění a tokenů aktualizace:
    - Udělení autorizačního kódu
    - Implicitní grant
    - Grant pověření vlastníka prostředku
    - Udělení pověření klienta
- Vytvoření serveru prostředků, který je chráněn přístupovým tokenem.
- Vytváření klientů OAuth 2.0.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Požadavky

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) nebo visual [studio express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)zdarma , jak je uvedeno v **softwarových verzích** v horní části stránky.
- Znalost OWIN. Viz [Začínáme s katana projektu](https://msdn.microsoft.com/magazine/dn451439.aspx) a [co je nového v OWIN a Katana](index.md).
- Znalost terminologie [OAuth,](http://tools.ietf.org/html/rfc6749) včetně [rolí](http://tools.ietf.org/html/rfc6749#section-1.1), [toku protokolu](http://tools.ietf.org/html/rfc6749#section-1.2)a [udělení autorizace](http://tools.ietf.org/html/rfc6749#section-1.3). [OAuth 2.0 úvod](http://tools.ietf.org/html/rfc6749#section-1) poskytuje dobrý úvod.

## <a name="create-an-authorization-server"></a>Vytvoření autorizačního serveru

V tomto kurzu budeme zhruba načrtnout, jak používat [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) a ASP.NET MVC k vytvoření autorizačního serveru. Doufáme, že brzy poskytneme ke stažení pro dokončený vzorek, protože tento výukový program nezahrnuje každý krok. Nejprve vytvořte prázdnou webovou aplikaci s názvem *AuthorizationServer* a nainstalujte následující balíčky:

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- Microsoft.Owin.Security.Google (Nebo jakýkoli jiný balíček pro přihlášení k sociálním sítím, například Microsoft.Owin.Security.Facebook)

Přidejte [třídu OWIN Startup](owin-startup-class-detection.md) pod kořenovou složku projektu s názvem *Startup*.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

Vytvořte složku *Start aplikace.\_* Vyberte složku *Start\_aplikace* a pomocí shift+alt+a přidejte staženou verzi souboru *AuthorizationServer\Start_App\Startup.Auth.cs.\_*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

Výše uvedený kód umožňuje aplikace / externí přihlášení cookies a ověřování Google, které jsou používány autorizační server sám pro správu účtů.

Metoda `UseOAuthAuthorizationServer` rozšíření je nastavení autorizačního serveru. Možnosti nastavení jsou:

- `AuthorizeEndpointPath`: Cesta požadavku, kde klientské aplikace přesměrují uživatelského agenta za účelem získání souhlasu uživatelů s vydáním tokenu nebo kódu. Musí začínat například úvodním`/Authorize`lomítkem " ".
- `TokenEndpointPath`: Klientské aplikace cesty požadavku přímo komunikují k získání přístupového tokenu. Musí začínat úvodním lomítkem, například "/Token". Pokud je klientovi vydán [tajný klíč klienta\_](http://tools.ietf.org/html/rfc6749#appendix-A.2), musí být k dispozici do tohoto koncového bodu.
- `ApplicationCanDisplayErrors`: Nastavte `true` na pokud webová aplikace chce generovat vlastní chybovou stránku pro chyby ověření klienta v `/Authorize` koncovém bodě. To je potřeba pouze v případech, kdy prohlížeč není přesměrován zpět `client_id` do `redirect_uri` klientské aplikace, například pokud nebo jsou nesprávné. Koncový `/Authorize` bod by měl očekávat, že "oauth. Chyba", "oauth. ErrorDescription", a "oauth. ErrorUri" vlastnosti jsou přidány do prostředí OWIN.

    > [!NOTE]
    > Pokud není true, autorizační server vrátí výchozí chybovou stránku s podrobnostmi o chybě.
- `AllowInsecureHttp`: True povolit autorizovat a token požadavky dorazit na adresy `redirect_uri` HTTP URI a umožnit příchozí autorizovat parametry požadavku mít http uri adresy.

    > [!WARNING]
    > Zabezpečení - To to je pouze pro vývoj.
- `Provider`: Objekt poskytnutý aplikací ke zpracování událostí vyvolaných middlewarem autorizačního serveru. Aplikace může plně implementovat rozhraní nebo může `OAuthAuthorizationServerProvider` vytvořit instanci a přiřadit delegáty nezbytné pro toky OAuth, které tento server podporuje.
- `AuthorizationCodeProvider`: Vytvoří jednopoužití autorizační kód pro návrat do klientské aplikace. Pro server OAuth, aby byl zabezpečený, **musí** aplikace poskytnout instanci, `AuthorizationCodeProvider` pro kterou je token vytvořený `OnCreate/OnCreateAsync` událostí považován za platný pouze pro jedno volání . `OnReceive/OnReceiveAsync`
- `RefreshTokenProvider`: Vytvoří obnovovací token, který může být použit k vytvoření nového přístupového tokenu v případě potřeby. Pokud není k dispozici autorizační server nevrátí `/Token` obnovovací tokeny z koncového bodu.

## <a name="account-management"></a>Správa účtů

OAuth se nestará o to, kde a jak spravujete informace o svém uživatelském účtu. Je to [ASP.NET identita,](../../../identity/index.md) která je za to zodpovědná. V tomto tutoriálu zjednodušíme kód pro správu účtu a jen se ujistíme, že se uživatel může přihlásit pomocí middleware souborů Cookie OWIN. Zde je zjednodušený ukázkový kód pro `AccountController`:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`slouží k ověření klienta s registrovanou adresou URL přesměrování. `ValidateClientAuthentication`zkontroluje záhlaví základního schématu a tělo formuláře, aby získal pověření klienta.

Přihlašovací stránka je uvedena níže:

![](owin-oauth-20-authorization-server/_static/image1.png)

Projděte si sekci IETF OAuth 2 [Authorization Code Grant.](http://tools.ietf.org/html/rfc6749#section-4.1)

**Zprostředkovatel** (v tabulce níže) je [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx). Zprostředkovatel, který je `OAuthAuthorizationServerProvider`typu , který obsahuje všechny události serveru OAuth.

| Kroky toku z oddílu Udělení autorizačního kódu | Ukázkové stažení provádí tyto kroky pomocí: |
| --- | --- |
|  |  |
| (A) Klient iniciuje tok přesměrováním uživatelského agenta vlastníka prostředku na koncový bod autorizace. Klient obsahuje identifikátor klienta, požadovaný obor, místní stav a identifikátor URI přesměrování, ke kterému autorizační server odešle uživatelského agenta zpět, jakmile je udělen (nebo odepřen přístup). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Autorizační server ověří vlastníka prostředku (prostřednictvím uživatelského agenta) a zjistí, zda vlastník prostředku udělí nebo zamítne žádost o přístup klienta. | **Pokud uživatel udělí přístup&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCode.CreateAsync |
|  |  |
| (C) Za předpokladu, že vlastník prostředku udělí přístup, autorizační server přesměruje uživatelského agenta zpět na klienta pomocí dříve poskytnutého identifikátoru URI přesměrování (v požadavku nebo při registraci klienta). ... |  |
|  |  |
| (D) Klient požaduje přístupový token z koncového bodu tokenu autorizačního serveru zahrnutím autorizačního kódu přijatého v předchozím kroku. Při provádění požadavku se klient ověřuje pomocí autorizačního serveru. Klient obsahuje identifikátor URI přesměrování použitý k získání autorizačního kódu pro ověření. | Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

Ukázková implementace `AuthorizationCodeProvider.CreateAsync` `ReceiveAsync` a řízení vytvoření a ověření autorizačního kódu je uvedena níže.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

Výše uvedený kód používá souběžný slovník v paměti k uložení kódu a lístku identity a obnovení identity po přijetí kódu. V reálné aplikaci by byl nahrazen trvalým úložištěm dat. Koncový bod autorizace je pro vlastníka prostředku udělit přístup ke klientovi. Obvykle potřebuje uživatelské rozhraní, aby uživatel mohl kliknout na tlačítko a potvrdit udělení. OWIN OAuth middleware umožňuje kód aplikace pro zpracování autorizačního koncového bodu. V naší ukázkové aplikaci používáme `OAuthController` řadič MVC volaný k jeho zpracování. Zde je ukázka implementace:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

Akce `Authorize` nejprve zkontroluje, zda se uživatel přihlásil k autorizačnímu serveru. Pokud tomu tak není, ověřovací middleware vyzve volajícího k ověření pomocí souboru cookie "Aplikace" a přesměruje na přihlašovací stránku. (Viz zvýrazněný kód výše.) Pokud se uživatel přihlásil, vykreslí zobrazení Autorizovat, jak je znázorněno níže:

![](owin-oauth-20-authorization-server/_static/image2.png)

Pokud je **vybráno** tlačítko `Authorize` Grant, akce vytvoří novou identitu "Nosič" a přihlásit se s ním. Spustí autorizační server pro generování nosné tokena a odeslat jej zpět klientovi s datovou částí JSON.

### <a name="implicit-grant"></a>Implicitní grant

Naleznete v části [Implicitní grant](http://tools.ietf.org/html/rfc6749#section-4.2) IETF OAuth 2.

 [Implicitní grantový](http://tools.ietf.org/html/rfc6749#section-4.2) tok znázorněný na obrázku 4 je tok a mapování, které následuje middleware OWin OAuth.

| Kroky toku z části Implicitní grant | Ukázkové stažení provádí tyto kroky pomocí: |
| --- | --- |
|  |  |
| (A) Klient iniciuje tok přesměrováním uživatelského agenta vlastníka prostředku na koncový bod autorizace. Klient obsahuje identifikátor klienta, požadovaný obor, místní stav a identifikátor URI přesměrování, ke kterému autorizační server odešle uživatelského agenta zpět, jakmile je udělen (nebo odepřen přístup). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Autorizační server ověří vlastníka prostředku (prostřednictvím uživatelského agenta) a zjistí, zda vlastník prostředku udělí nebo zamítne žádost o přístup klienta. | **Pokud uživatel udělí přístup&gt; &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCode.CreateAsync |
|  |  |
| (C) Za předpokladu, že vlastník prostředku udělí přístup, autorizační server přesměruje uživatelského agenta zpět na klienta pomocí dříve poskytnutého identifikátoru URI přesměrování (v požadavku nebo při registraci klienta). ... |  |
|  |  |
| (D) Klient požaduje přístupový token z koncového bodu tokenu autorizačního serveru zahrnutím autorizačního kódu přijatého v předchozím kroku. Při provádění požadavku se klient ověřuje pomocí autorizačního serveru. Klient obsahuje identifikátor URI přesměrování použitý k získání autorizačního kódu pro ověření. |  |

Vzhledem k tomu, že`OAuthController.Authorize` jsme již implementovali koncový bod autorizace (akce) pro udělení autorizačního kódu, automaticky také umožňuje implicitní tok. Poznámka: `Provider.ValidateClientRedirectUri` Slouží k ověření ID klienta s jeho adresou URL přesměrování, která chrání implicitní tok grantu před odesláním přístupového tokenu klientům se zlými úmysly ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).

### <a name="resource-owner-password-credentials-grant"></a>Grant pověření vlastníka prostředku

Naleznete v části IETF OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) nyní.

 Tok pověření hesla [vlastníka prostředku grantový](http://tools.ietf.org/html/rfc6749#section-4.3) tok znázorněný na obrázku 5 je tok a mapování, které následuje middleware OWIN OAuth.

| Kroky toku z oddílu Grant pověření vlastníka vlastníka prostředku | Ukázkové stažení provádí tyto kroky pomocí: |
| --- | --- |
|  |  |
| (A) Vlastník prostředku poskytuje klientovi své uživatelské jméno a heslo. |  |
|  |  |
| (B) Klient požaduje přístupový token z koncového bodu tokenu autorizačního serveru zahrnutím pověření přijatých od vlastníka prostředku. Při provádění požadavku se klient ověřuje pomocí autorizačního serveru. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) Autorizační server ověří klienta a ověří pověření vlastníka prostředku a pokud je platný, vydá přístupový token. |  |

Zde je ukázková `Provider.GrantResourceOwnerCredentials`implementace pro :

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> Výše uvedený kód je určen k vysvětlení této části kurzu a neměl by být používán v zabezpečených nebo produkčních aplikacích. Nekontroluje pověření vlastníků prostředků. Předpokládá, že každé pověření je platné a vytvoří pro něj novou identitu. Nová identita bude použita ke generování přístupového tokenu a obnovovacího tokenu. Nahraďte kód vlastním zabezpečeným kódem pro správu účtu.


### <a name="client-credentials-grant"></a>Udělení pověření klienta

Naleznete v části IETF OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) nyní.

 Tok [grantu pověření klienta](http://tools.ietf.org/html/rfc6749#section-4.4) znázorněný na obrázku 6 je tok a mapování, které následuje middleware OAuth OWIN.

| Kroky toku z oddílu Grant pověření klienta | Ukázkové stažení provádí tyto kroky pomocí: |
| --- | --- |
|  |  |
| (A) Klient se ověří pomocí autorizačního serveru a požaduje přístupový token z koncového bodu tokenu. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) Autorizační server ověřuje klienta a pokud je platný, vydá přístupový token. |  |

Zde je ukázková `Provider.GrantClientCredentials`implementace pro :

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> Výše uvedený kód je určen k vysvětlení této části kurzu a neměl by být používán v zabezpečených nebo produkčních aplikacích. Nahraďte kód vlastním zabezpečeným kódem pro správu klienta.


### <a name="refresh-token"></a>Aktualizovat token

Podívejte se na část IETF OAuth 2 [Refresh Token.](http://tools.ietf.org/html/rfc6749#section-1.5)

 [Tok tokenu aktualizace](http://tools.ietf.org/html/rfc6749#section-1.5) znázorněný na obrázku 2 je tok a mapování, které následuje middleware OWin OAuth.

| Kroky toku z oddílu Grant pověření klienta | Ukázkové stažení provádí tyto kroky pomocí: |
| --- | --- |
|  |  |
| (G) Klient požaduje nový přístupový token ověřením pomocí autorizačního serveru a předložením obnovovacího tokenu. Požadavky na ověření klienta jsou založeny na typu klienta a na zásadách autorizačního serveru. | Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshProviderProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (H) Autorizační server ověří klienta a ověří obnovovací token a pokud je platný, vydá nový přístupový token (a volitelně nový obnovovací token). |  |

Zde je ukázková `Provider.GrantRefreshToken`implementace pro :

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>Vytvoření serveru prostředků chráněného přístupovým tokenem

Vytvořte prázdný projekt webové aplikace a nainstalujte do projektu následující balíčky:

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

Vytvořte spouštěcí třídu a nakonfigurujte ověřování a webové rozhraní API. Viz *AuthorizationServer\ResourceServer\Startup.cs* v ukázkovém stažení.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

V ukázkovém stažení naleznete informace *o serveru\_AuthorizationServer\ResourceServer\Spuštění aplikace\Startup.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

Viz *AuthorizationServer\ResourceServer\Start_App\Startup.WebApi.cs\_* v ukázkovém stažení.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`metoda umožňuje CORS pro všechny domény.
- `UseOAuthBearerAuthentication`metoda umožňuje OAuth nosné token ověřování middleware, který bude přijímat a ověřovat nosný token z autorizační hlavičky v požadavku.
- `Config.SuppressDefaultHostAuthenticaiton`potlačí výchozí objekt zabezpečení ověřený hostitele z aplikace, proto budou všechny požadavky anonymní po tomto volání.
- `HostAuthenticationFilter`umožňuje ověřování pouze pro zadaný typ ověřování. V tomto případě je typ ověřování nosiče.

Aby bylo možné demonstrovat ověřenou identitu, vytvoříme ApiController pro výstup aktuálního uživatele deklarací.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

Pokud autorizační server a server prostředků nejsou ve stejném počítači, middleware OAuth použije různé klíče počítače k šifrování a dešifrování přístupového tokenu nosiče. Abybylo možné sdílet stejný soukromý klíč mezi oběma `machinekey` projekty, přidáme stejné nastavení v obou souborech *web.config.*

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>Vytvořit klienty OAuth 2.0

 Ke zjednodušení klientského kódu používáme balíček [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet.

### <a name="authorization-code-grant-client"></a>Klient udělení autorizačního kódu

 Tento klient je aplikace MVC. Spustí tok udělení autorizačního kódu získat přístupový token z back-endu. Má jednu stránku, jak je znázorněno níže:

![](owin-oauth-20-authorization-server/_static/image3.png)

- Tlačítko **Autorizovat** přesměruje prohlížeč na autorizační server a upozorní vlastníka prostředku, aby tomuto klientovi udělil přístup.
- Tlačítko **Aktualizovat** získá nový přístupový token a obnovovací token pomocí aktuálního obnovovacího tokenu.
- Tlačítko **Rozhraní ACCESS Protected Resource API** zavolá server prostředků, aby získalo data deklarací identity aktuálního uživatele a zobrazilo je na stránce.

Zde je ukázkový `HomeController` kód klienta.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`ve výchozím nastavení vyžaduje ssl. Vzhledem k tomu, že naše demo používá HTTP, musíte přidat následující nastavení do konfiguračního souboru:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> Zabezpečení – Nikdy nezakažte ssl v produkční aplikaci. Vaše přihlašovací údaje jsou nyní odesílány ve prostém textu přes drát. Výše uvedený kód je určen pouze pro místní ukázkové ladění a průzkum.


### <a name="implicit-grant-client"></a>Implicitní klient grantu

Tento klient používá JavaScript k:

1. Otevřete nové okno a přesměrujte na autorizační koncový bod autorizačního serveru.
2. Získejte přístupový token z fragmentů adresy URL, když se přesměruje zpět.

Následující obrázek ukazuje tento proces:

![](owin-oauth-20-authorization-server/_static/image4.png)

Klient by měl mít dvě stránky: jednu pro domovskou stránku a druhou pro zpětné volání. Zde je ukázkový kód JavaScriptu nalezený v souboru *Index.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

Zde je kód zpracování zpětného volání v souboru *SignIn.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> Osvědčeným postupem je přesunout JavaScript do externího souboru a nevložit jej pomocí značky Razor. Aby byl tento vzorek jednoduchý, byly kombinovány.


### <a name="resource-owner-password-credentials-grant-client"></a>Klient a klient hesla vlastníka prostředku

Používáme konzolovou aplikaci k demo tohoto klienta. Zde je kód:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>Klientpověření udělit klienta

Podobně jako u grantu přihlašovacích údajů vlastníka prostředku je zde kód aplikace konzoly:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
