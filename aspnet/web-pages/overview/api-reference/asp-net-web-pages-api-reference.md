---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Webové stránky (Břitva) API Stručný přehled | Dokumenty společnosti Microsoft
author: Rick-Anderson
description: Tato stránka obsahuje seznam se stručnými příklady nejčastěji používaných objektů, vlastností a metod programování ASP.NET webových stránek se syntaxí Razor.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676242"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET stručný přehled api webových stránek (Razor)

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

> Tato stránka obsahuje seznam se stručnými příklady nejčastěji používaných objektů, vlastností a metod programování ASP.NET webových stránek se syntaxí Razor.
> 
> Popisy označené "(v2)" byly zavedeny v ASP.NET webových stránek verze 2.
> 
> Referenční dokumentace rozhraní API naleznete v [ASP.NET referenční dokumentaci k webovým stránkám](https://go.microsoft.com/fwlink/?LinkId=208659) v síti MSDN.
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> 
> - webové stránky ASP.NET (Břitva) 3
>   
> 
> Tento kurz funguje také s ASP.NET webových stránek 2 a ASP.NET webových stránek 1.0 (s výjimkou funkcí označených v2).

Tato stránka obsahuje referenční informace pro následující:

- [Třídy](#Classes)
- [Data](#Data)
- [Pomocníci](#Helpers)
- [Ověřování](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Třídy

### `AppState[key], AppState[index],App`

Obsahuje data, která mohou být sdílena libovolné stránky v aplikaci. Dynamickou `App` vlastnost můžete použít pro přístup ke stejným datům, jako v následujícím příkladu:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Převede hodnotu řetězce na logickou hodnotu (true/false). Vrátí hodnotu false nebo zadanou hodnotu, pokud řetězec nepředstavuje hodnotu true/false.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Převede hodnotu řetězce na datum a čas. Vrátí `DateTime.MinValue` nebo zadanou hodnotu, pokud řetězec nepředstavuje datum a čas.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Převede hodnotu řetězce na desítkovou hodnotu. Vrátí hodnotu 0,0 nebo zadanou hodnotu, pokud řetězec nepředstavuje desítkovou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Převede hodnotu řetězce na float. Vrátí hodnotu 0,0 nebo zadanou hodnotu, pokud řetězec nepředstavuje desítkovou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Převede hodnotu řetězce na celé číslo. Vrátí hodnotu 0 nebo zadanou hodnotu, pokud řetězec nepředstavuje celé číslo.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Vytvoří adresu URL kompatibilní s prohlížečem z místní cesty k souboru s volitelnými dalšími částmi cesty.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Vykreslí *hodnotu* jako značky HTML namísto vykreslování jako výstup kódovaný HTML.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Vrátí hodnotu true, pokud lze hodnotu převést z řetězce na zadaný typ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Vrátí hodnotu true, pokud objekt nebo proměnná nemá žádnou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Vrátí hodnotu true, pokud je požadavek požadavek POST. (Počáteční požadavky jsou obvykle GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Určuje cestu stránky rozložení, která se má použít na tuto stránku.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Obsahuje data sdílená mezi stránkou, stránkami rozložení a částečnými stránkami v aktuálním požadavku. Dynamickou `Page` vlastnost můžete použít pro přístup ke stejným datům, jako v následujícím příkladu:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Rozložení stránky) Vykreslí obsah stránky obsahu, která není v žádné pojmenované části.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Vykreslí stránku obsahu pomocí zadané cesty a volitelných dodatečných dat. Hodnoty dalších parametrů můžete získat `PageData` z pozice (příklad 1) nebo klávesy (příklad 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Rozložení stránky) Vykreslí oddíl obsahu, který má název. Nastavte *požadováno,* aby false, aby se oddíl volitelné.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Získá nebo nastaví hodnotu souboru cookie HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Získá soubory, které byly odeslány v aktuální požadavek.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Získá data, která byla zaúčtována ve formuláři (jako řetězce). `Request[key]`kontroluje jak `Request.Form` sbírky, tak `Request.QueryString` sbírky.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Získá data, která byla zadána v řetězci dotazu URL. `Request[key]`kontroluje jak `Request.Form` sbírky, tak `Request.QueryString` sbírky.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Selektivně zakáže ověření požadavku pro prvek formuláře, hodnotu řetězce dotazu, soubor cookie nebo hodnotu záhlaví. Ověření požadavku je ve výchozím nastavení povoleno a zabraňuje uživatelům v zveřejňování značek nebo jiného potenciálně nebezpečného obsahu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Přidá k odpovědi hlavičku serveru HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Uloží výstup stránky do mezipaměti po určitou dobu. Volitelně nastavte *posuvné* obnovit časový limit na každé stránce přístup a *varyByParams* do mezipaměti různé verze stránky pro každý jiný řetězec dotazu v požadavku na stránku.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Přesměruje požadavek prohlížeče na nové umístění.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Nastaví stavový kód HTTP odeslaný do prohlížeče.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Zapíše obsah *dat* do odpovědi s volitelným typem MIME.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Zapíše obsah souboru na odpověď.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Rozložení stránky) Definuje oddíl obsahu, který má název.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Dekóduje řetězec, který je kódován html.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Zakóduje řetězec pro vykreslování ve značkách HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Vrátí fyzickou cestu serveru pro zadanou virtuální cestu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Dekóduje text z adresy URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Zakóduje text, který chcete vložit do adresy URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Získá nebo nastaví hodnotu, která existuje, dokud uživatel zavře prohlížeč.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Zobrazí řetězcovou reprezentaci hodnoty objektu.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Získá další data z adresy URL (například */MyPage/ExtraData*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Změní heslo pro zadaného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Potvrdí účet pomocí tokenu potvrzení účtu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Vytvoří nový uživatelský účet se zadaným uživatelským jménem a heslem. Chcete-li vyžadovat potvrzovací token, předavte hodnotu true pro *requireConfirmationToken.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Získá identifikátor celé číslo pro aktuálně přihlášeného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Získá název aktuálně přihlášeného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Generuje token pro obnovení hesla, který lze odeslat e-mailem uživateli, aby uživatel mohl heslo resetovat.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Vrátí ID uživatele z uživatelského jména.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Vrátí hodnotu true, pokud je přihlášen aktuální uživatel.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Vrátí hodnotu true, pokud byl uživatel potvrzen (například prostřednictvím potvrzovacího e-mailu).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Vrátí hodnotu true, pokud se jméno aktuálního uživatele shoduje se zadaným uživatelským jménem.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Přihlásí uživatele nastavením ověřovacího tokenu v souboru cookie.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Zaznamená uživatele odebráním souboru cookie ověřovacího tokenu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Pokud uživatel není ověřen, nastaví stav HTTP na 401 (Neautorizováno).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Pokud aktuální uživatel není členem jedné ze zadaných rolí, nastaví stav HTTP na 401 (Neautorizováno).

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Pokud aktuální uživatel není uživatelem určeným *uživatelským jménem*, nastaví stav HTTP na 401 (Neautorizováno).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Pokud je token pro obnovení hesla platný, změní heslo uživatele na nové heslo.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Data

### `Database.Execute(SQLstatement [,parameters]`

Provede *SQLstatement* (s volitelnými parametry), například INSERT, DELETE nebo UPDATE a vrátí počet ovlivněných záznamů.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Vrátí sloupec identity z naposledy vloženého řádku.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Otevře zadaný databázový soubor nebo databázi určenou pomocí pojmenovaného připojovacího řetězce ze souboru *Web.config.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Otevře databázi pomocí připojovacího řetězce. (To kontrastuje `Database.Open`s , který používá název připojovacího řetězce.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Dotazuje databázi pomocí *SQLstatement* (volitelně předávání parametrů) a vrátí výsledky jako kolekce.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Provede *SQLstatement* (s volitelnými parametry) a vrátí jeden záznam.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Provede *SQLstatement* (s volitelnými parametry) a vrátí jednu hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Pomocníci

### `Analytics.GetGoogleHtml(webPropertyId)`

Vykreslí javascriptový kód Google Analytics pro zadané ID.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Vykreslí kód JavaScript statcounter analytics pro zadaný projekt.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Vykreslí kód JavaScriptu Yahoo Analytics pro zadaný účet.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Předává vyhledávání Bingovi. Chcete-li určit web, který chcete vyhledat, a `Bing.SiteUrl` název `Bing.SiteTitle` vyhledávacího pole, můžete nastavit vlastnosti a. Obvykle tyto vlastnosti * \_* nastavíte na stránce AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Inicializuje graf.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Přidá do grafu legendu.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Přidá do grafu řadu hodnot.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Vrátí hodnotu hash pro zadaná data. Výchozí algoritmus `sha256`je .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Umožňuje uživatelům Facebooku navázat spojení se stránkami.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Vykreslí uI pro nahrávání souborů.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Vykreslí zadanou značku hráče Xbox.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Vykreslí obrázek Gravatar pro zadanou e-mailovou adresu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Převede datový objekt na řetězec ve formátu Zápis objektu JavaScriptu (JSON).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Převede vstupní řetězec kódovaný jsonem na datový objekt, který můžete iterate přes nebo vložit do databáze.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Vykreslí odkazy na sociální sítě pomocí zadaného názvu a volitelné adresy URL.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Přidruží chybovou zprávu k poli formuláře. Použijte `ModelState` pomocníka pro přístup k tomuto členu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Přidruží chybovou zprávu k formuláři. Použijte `ModelState` pomocníka pro přístup k tomuto členu.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Vrátí hodnotu true, pokud nejsou k dispozici žádné chyby ověření. Použijte `ModelState` pomocníka pro přístup k tomuto členu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Vykreslí vlastnosti a hodnoty objektu a všechny podřízené objekty.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Vykreslí ověřovací test reCAPTCHA.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Nastaví veřejné a soukromé klíče pro službu reCAPTCHA. Obvykle tyto vlastnosti * \_* nastavíte na stránce AppStart.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Vrátí výsledek testu reCAPTCHA.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Vykreslí informace o stavu ASP.NET webových stránek.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Vykreslí datový proud Twitter pro zadaného uživatele.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Vykreslí datový proud Twitteru pro zadaný hledaný text.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Vykreslí přehrávač videa Flash pro zadaný soubor s volitelnou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Vykreslí program Windows Media pro zadaný soubor s volitelnou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Vykreslí přehrávač Silverlight pro zadaný soubor *XAP* s požadovanou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Vrátí objekt určený *klíčem*nebo hodnotou null, pokud objekt nebyl nalezen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Odebere objekt určený *klíčem* z mezipaměti.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Vloží *hodnotu* do mezipaměti pod názvem určeným *klíčem*.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Vytvoří nový `WebGrid` objekt pomocí dat z dotazu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Vykreslí značky pro zobrazení dat v tabulce HTML.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Vykreslí operátor pro `WebGrid` objekt.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Načte obraz ze zadané cesty.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Přidá zadaný obrázek jako vodoznak.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Přidá do obrazu zadaný text.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Překlopí obraz vodorovně nebo svisle.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Načte obrázek, když je obrázek během nahrávání souboru zaúčtován na stránku.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Změní velikost obrázku.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Otočí obraz doleva nebo doprava.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Uloží obraz do zadané cesty.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Nastaví heslo pro server SMTP. Tuto vlastnost obvykle nastavíte na * \_stránce AppStart.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Odešle e-mailovou zprávu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Nastaví název serveru SMTP. Tuto vlastnost obvykle nastavíte na * \_stránce AppStart.*

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Nastaví uživatelské jméno serveru SMTP. Za normálních okolností * \_* byste měli tuto vlastnost nastavit na stránce AppStart.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Ověřování

### `Html.ValidationMessage(field)`

(v2) Vykreslí chybovou zprávu ověření pro zadané pole.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) Zobrazí seznam všech chyb ověření.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) Zaregistruje vstupní prvek uživatele pro zadaný typ ověření.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) Dynamicky vykresluje atributy třídy CSS pro ověření na straně klienta, takže můžete formátovat chybové zprávy ověření. (Vyžaduje, abyste odkazovali na příslušné knihovny klientských skriptů a definovali třídy CSS.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) Umožňuje ověření na straně klienta pro vstupní pole uživatele. (Vyžaduje odkaz na příslušné knihovny klientských skriptů.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) Vrátí hodnotu true, pokud všechny vstupní prvky uživatele, které jsou registrovány pro ověření, obsahují platné hodnoty.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) Určuje, že uživatelé musí zadat hodnotu pro vstupní prvek uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) Určuje, že uživatelé musí zadat hodnoty pro každý vstupní element uživatele. Tato metoda neumožňuje zadat vlastní chybovou zprávu.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

(v2) Určuje ověřovací test při použití `Validation.Add` metody.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
