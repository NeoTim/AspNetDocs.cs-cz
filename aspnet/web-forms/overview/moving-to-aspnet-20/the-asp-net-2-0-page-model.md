---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: Model stránky ASP.NET 2.0 | Dokumenty společnosti Microsoft
author: rick-anderson
description: V ASP.NET 1.x měli vývojáři na výběr mezi modelem vřádkového kódu a modelem kódu na pozadí kódu. Code-behind by mohla být implementována buď s použitím Src attr ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542856"
---
# <a name="the-aspnet-20-page-model"></a>Model stránky ASP.NET 2.0

podle [společnosti Microsoft](https://github.com/microsoft)

> V ASP.NET 1.x měli vývojáři na výběr mezi modelem vřádkového kódu a modelem kódu na pozadí kódu. Code-behind může být implementována pomocí atributu Src @Page nebo CodeBehind atribut směrnice. V ASP.NET 2.0 mají vývojáři stále na výběr mezi vázacím kódem a kódem na pozadí, ale došlo k významným vylepšením modelu s kódem na pozadí.

V ASP.NET 1.x měli vývojáři na výběr mezi modelem vřádkového kódu a modelem kódu na pozadí kódu. Code-behind může být implementována pomocí atributu Src @Page nebo CodeBehind atribut směrnice. V ASP.NET 2.0 mají vývojáři stále na výběr mezi vázacím kódem a kódem na pozadí, ale došlo k významným vylepšením modelu s kódem na pozadí.

## <a name="improvements-in-the-code-behind-model"></a>Vylepšení modelu code-behind

Chcete-li plně pochopit změny v modelu s kódem na pozadí v ASP.NET 2.0, jeho nejlepší rychle zkontrolovat model, jak existoval v ASP.NET 1.x.

## <a name="the-code-behind-model-in-aspnet-1x"></a>Code-Behind Model v ASP.NET 1.x

V ASP.NET 1.x se model s kódem na pozadí skládal ze souboru ASPX (webový formulář) a souboru s kódem na pozadí obsahujícího programovací kód. Tyto dva soubory byly @Page připojeny pomocí směrnice v souboru ASPX. Každý ovládací prvek na stránce ASPX měl odpovídající deklaraci v souboru s kódem na pozadí jako proměnnou instance. Soubor s kódem na pozadí také obsahoval kód pro vazbu událostí a generovaný kód nezbytný pro návrháře sady Visual Studio. Tento model fungoval poměrně dobře, ale protože každý prvek ASP.NET na stránce ASPX vyžadoval odpovídající kód v souboru s kódem na pozadí, neexistovalo žádné skutečné oddělení kódu a obsahu. Například pokud návrhář přidal nový serverový ovládací prvek do souboru ASPX mimo IDE sady Visual Studio, aplikace by se přerušila z důvodu absence deklarace tohoto ovládacího prvku v souboru s kódem na pozadí.

## <a name="the-code-behind-model-in-aspnet-20"></a>Code-Behind Model v ASP.NET 2.0

ASP.NET 2.0 výrazně zlepšuje na tomto modelu. V ASP.NET 2.0 je kód na pozadí implementován pomocí nových *částečných tříd uvedených* v ASP.NET 2.0. Třída s kódem na pozadí v ASP.NET 2.0 je definována jako částečná třída, což znamená, že obsahuje pouze část definice třídy. Zbývající část definice třídy je dynamicky generována ASP.NET 2.0 pomocí stránky ASPX za běhu nebo při předkompilaci webu. Propojení mezi souborem s kódem na pozadí a stránkou ASPX je stále vytvořeno pomocí direktivy @ Page. Místo atributu CodeBehind nebo Src však ASP.NET 2.0 nyní používá atribut CodeFile. Atribut Inherits se také používá k určení názvu třídy stránky.

Typická direktiva @ Page může vypadat takto:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

Typická definice třídy v souboru s kódem 2.0 ASP.NET může vypadat takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# a Visual Basic jsou pouze spravované jazyky, které aktuálně podporují částečné třídy. Proto vývojáři pomocí J# nebude moci používat model s kódem na pozadí v ASP.NET 2.0.

Nový model vylepšuje model s kódem na pozadí, protože vývojáři budou mít nyní soubory kódu, které obsahují pouze kód, který vytvořili. Poskytuje také skutečné oddělení kódu a obsahu, protože v souboru s kódem na pozadí nejsou žádné deklarace proměnných instance.

> [!NOTE]
> Vzhledem k tomu, že částečná třída pro stránku ASPX je místo, kde dochází k vazbě událostí, mohou vývojáři jazyka Visual Basic realizovat mírné zvýšení výkonu pomocí klíčového slova Handles v kódu na pozadí pro svázání událostí. C# nemá žádné ekvivalentní klíčové slovo.

## <a name="new--page-directive-attributes"></a>Nové @ Atributy směrnice stránky

ASP.NET 2.0 přidá mnoho nových atributů @ Page směrnice. Následující atributy jsou nové v ASP.NET 2.0.

## <a name="async"></a>Async

Atribut Async umožňuje nakonfigurovat stránku tak, aby byla spuštěna asynchronně. No pokrytí asynchronní stránky později v tomto modulu.

## <a name="asynctimeout"></a>AsyncTimeout

Zadaný časový čas pro asynchronní stránky. Výchozí hodnota je 45 sekund.

## <a name="codefile"></a>Codefile

Atribut CodeFile je náhradou atributu CodeBehind v sadě Visual Studio 2002/2003.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

Atribut CodeFileBaseClass se používá v případech, kdy chcete, aby více stránek bylo odvozeno z jedné základní třídy. Z důvodu implementace částečné třídy v ASP.NET, bez tohoto atributu, základní třída, která používá sdílené společné pole odkazovat na ovládací prvky deklarované na stránce ASPX nebude fungovat správně, protože modul kompilace ASP.NETs automaticky vytvoří nové členy na základě ovládacích prvků na stránce. Proto pokud chcete společnou základní třídu pro dvě nebo více stránek v ASP.NET, budete muset definovat určit základní třídu v attribute CodeFileBaseClass a potom odvodit každou třídu stránek z této základní třídy. Atribut CodeFile je také vyžadován při použití tohoto atributu.

## <a name="compilationmode"></a>Compilationmode

Tento atribut umožňuje nastavit vlastnost CompilationMode stránky ASPX. Vlastnost CompilationMode je výčet obsahující hodnoty **Always**, **Auto**a **Never**. Výchozí hodnota je **Vždy**. Nastavení **Automaticky** zabrání ASP.NET dynamicky kompilovat stránku, pokud je to možné. Vyloučení stránek z dynamické kompilace zvyšuje výkon. Pokud však stránka, která je vyloučena, obsahuje tento kód, který musí být zkompilován, bude při procházení stránky vyvolána chyba.

## <a name="enableeventvalidation"></a>EnableEventValidation

Tento atribut určuje, zda jsou ověřeny události postback a callback. Pokud je tato možnost povolena, jsou kontrolovány argumenty pro události zpětného volání nebo zpětného volání, aby bylo zajištěno, že pocházejí ze serverového ovládacího prvku, který je původně vykresloval.

## <a name="enabletheming"></a>Enabletheming

Tento atribut určuje, zda jsou na stránce použity ASP.NET motivy. Výchozí hodnota je **false**. ASP.NET témata jsou zahrnuta v [modulu 10](profiles-themes-and-web-parts.md).

## <a name="linepragmas"></a>LinePragmas

Tento atribut určuje, zda má být během kompilace přidán řádek pragmas. Line pragmas jsou možnosti používané ladicími programy k označení konkrétních částí kódu.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Tento atribut určuje, zda je JavaScript vložen do stránky, aby se zachovala pozice posouvání mezi postbacky. Tento atribut je ve výchozím nastavení **false.**

Pokud je tento atribut **pravdivý**&gt; , přidá ASP.NET blok skriptu &lt;na postback, který vypadá takto:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Všimněte si, že src pro tento blok skriptu je WebResource.axd. Tento prostředek není fyzická cesta. Je-li tento skript požadován, ASP.NET dynamicky vytvoří skript.

### <a name="masterpagefile"></a>Masterpagefile

Tento atribut určuje soubor stránky předlohy pro aktuální stránku. Cesta může být relativní nebo absolutní. Vzorové stránky jsou zahrnuty v [modulu 4](master-pages.md).

## <a name="stylesheettheme"></a>Stylesheettheme

Tento atribut umožňuje přepsat vlastnosti vzhledu uživatelského rozhraní definované ASP.NET motivem 2.0. Témata jsou popsána v [modulu 10](profiles-themes-and-web-parts.md).

## <a name="theme"></a>Motiv

Určuje motiv stránky. Pokud pro atribut StyleSheetTheme není zadána hodnota, atribut Motiv přepíše všechny styly použité na ovládací prvky na stránce.

## <a name="title"></a>Nadpis

Nastaví název stránky. Zde zadaná hodnota &lt;se&gt; zobrazí v názvu prvku vykreslené stránky.

### <a name="viewstateencryptionmode"></a>Režim šifrování stavu Zobrazení

Nastaví hodnotu výčtu ViewStateEncryptionMode. Dostupné hodnoty jsou **Always**, **Auto**a **Never**. Výchozí hodnota je **Auto**. Pokud je tento atribut nastaven na hodnotu **Auto**, viewstate je šifrována je ovládací prvek požaduje voláním **RegisterRequiresViewStateEncryption** metoda.

## <a name="setting-public-property-values-via-the--page-directive"></a>Nastavení hodnot veřejného vlastnictví prostřednictvím direktivy @ Page

Další novou funkcí @ Page směrnice v ASP.NET 2.0 je možnost nastavit počáteční hodnotu veřejné vlastnosti základní třídy. Předpokládejme například, že máte veřejnou vlastnost s názvem **SomeText** ve vaší základní třídě a chcete, aby byla inicializována na **Hello** při načtení stránky. Toho lze dosáhnout jednoduše nastavením hodnoty ve směrnici @ Page takto:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

**SomeText** atribut @ Page směrnice nastaví počáteční hodnotu SomeText vlastnost v základní třídě *Hello!*. Video níže je návod nastavení počáteční hodnoty veřejné vlastnosti v základní třídě pomocí @ Page směrnice.

![](the-asp-net-2-0-page-model/_static/image1.png)

[Otevřít video na celou obrazovku](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Nové veřejné vlastnosti třídy Page

Následující veřejné vlastnosti jsou nové v ASP.NET 2.0.

## <a name="apprelativetemplatesourcedirectory"></a>Apprelativetemplatesourcedirectory

Vrátí cestu relativní k aplikaci na stránku nebo ovládací prvek. Například pro stránku http://app/folder/page.aspxumístěnou na , vlastnost vrátí ~/folder/.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

Vrátí relativní cestu virtuálního adresáře ke stránce nebo ovládacímu prvku. Například pro stránku http://app/folder/page.aspxumístěnou na stránce , vlastnost vrátí ~/folder/page.aspx.

## <a name="asynctimeout"></a>AsyncTimeout

Získá nebo nastaví časový čas použitý pro zpracování asynchronní stránky. (Asynchronní stránky budou zahrnuty dále v tomto modulu.)

## <a name="clientquerystring"></a>Řetězec klientských dotazů

Vlastnost jen pro čtení, která vrací část řetězce dotazu požadované adresy URL. Tato hodnota je kódována adresou URL. K dekódování můžete použít metodu UrlDecode třídy HttpServerUtility.

## <a name="clientscript"></a>Klientský jazyk

Tato vlastnost vrátí objekt ClientScriptManager, který lze použít ke správě emisí ASP.NETs skriptu na straně klienta. (Třída ClientScriptManager je popsána dále v tomto modulu.)

## <a name="enableeventvalidation"></a>EnableEventValidation

Tato vlastnost určuje, zda je povoleno ověření události pro události postback a callback. Pokud je povoleno, argumenty pro události postback nebo callback jsou ověřeny, aby bylo zajištěno, že pocházejí z ovládacího prvku serveru, který je původně vykreslil.

## <a name="enabletheming"></a>Enabletheming

Tato vlastnost získá nebo nastaví logickou hodnotu, která určuje, zda se na stránku vztahuje ASP.NET motiv 2.0.

## <a name="form"></a>Formulář

Tato vlastnost vrátí formulář HTML na stránce ASPX jako objekt HtmlForm.

## <a name="header"></a>Hlavička

Tato vlastnost vrátí odkaz na objekt HtmlHead, který obsahuje záhlaví stránky. Můžete použít vrácený objekt HtmlHead k získání / nastavení šablon stylů, meta tagů atd.

## <a name="idseparator"></a>IdSekretor

Tato vlastnost jen pro čtení získá znak, který se používá k oddělení identifikátorů ovládacího prvku při ASP.NET vytváří jedinečné ID pro ovládací prvky na stránce. Není určen k použití přímo z vašeho kódu.

## <a name="isasync"></a>Isasync

Tato vlastnost umožňuje asynchronní stránky. Asynchronní stránky jsou popsány dále v tomto modulu.

## <a name="iscallback"></a>IsCallback

Tato vlastnost jen pro čtení vrátí **true,** pokud je stránka výsledkem zpětného volání. Zpětné volání jsou popsány později v tomto modulu.

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

Tato vlastnost jen pro čtení vrátí **true,** pokud je stránka součástí postback u několika stránek. Cross-page postbacks jsou zahrnuty dále v tomto modulu.

## <a name="items"></a>Items

Vrátí odkaz na instanci IDictionary, která obsahuje všechny objekty uložené v kontextu stránek. Můžete přidat položky tohoto objektu IDictionary a budou k dispozici po celou dobu životnosti kontextu.

## <a name="maintainscrollpositiononpostback"></a>Udržovat ScrollpositiononPostback

Tato vlastnost určuje, zda ASP.NET vydává JavaScript, který udržuje pozici posouvání stránek v prohlížeči po postbacku. (Podrobnosti o této vlastnosti byly popsány dříve v tomto modulu.)

## <a name="master"></a>Hlavní

Tato vlastnost jen pro čtení vrátí odkaz na instanci MasterPage pro stránku, na kterou byla použita stránka předlohy.

## <a name="masterpagefile"></a>Masterpagefile

Získá nebo nastaví název souboru stránky předlohy pro stránku. Tuto vlastnost lze nastavit pouze v Metodě PreInit.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

Tato vlastnost získá nebo nastaví maximální délku pro stav stránek v bajtech. Pokud je vlastnost nastavena na kladné číslo, stav zobrazení stránek bude rozdělen do více skrytých polí, aby nepřekročil zadaný počet bajtů. Pokud je vlastnost záporné číslo, stav zobrazení nebude rozdělen na bloky.

## <a name="pageadapter"></a>Pageadapter

Vrátí odkaz na objekt PageAdapter, který upravuje stránku pro žádající prohlížeč.

## <a name="previouspage"></a>Previouspage

Vrátí odkaz na předchozí stránku v případě Server.Transfer nebo cross-page postback.

## <a name="skinid"></a>Skinid

Určuje vzhled ASP.NET 2.0, který se má na stránku aplikovat.

## <a name="stylesheettheme"></a>Stylesheettheme

Tato vlastnost získá nebo nastaví šablonu stylů, která je použita na stránku.

## <a name="templatecontrol"></a>Templatecontrol

Vrátí odkaz na ovládací prvek obsahující pro stránku.

## <a name="theme"></a>Motiv

Získá nebo nastaví název ASP.NET motivu 2.0 použitého na stránce. Tato hodnota musí být nastavena před metodou PreInit.

## <a name="title"></a>Nadpis

Tato vlastnost získá nebo nastaví název stránky, jak bylo získáno z hlavičky stránky.

## <a name="viewstateencryptionmode"></a>Režim šifrování stavu Zobrazení

Získá nebo nastaví ViewStateEncryptionMode stránky. Podívejte se na podrobnou diskusi o této vlastnosti dříve v tomto modulu.

## <a name="new-protected-properties-of-the-page-class"></a>Nové chráněné vlastnosti třídy Page

Následují nové chráněné vlastnosti Page třídy v ASP.NET 2.0.

## <a name="adapter"></a>Adaptér

Vrátí odkaz na ControlAdapter, který vykreslí stránku na zařízení, které o to požádalo.

## <a name="asyncmode"></a>Asynchronizační režim

Tato vlastnost označuje, zda je stránka zpracována asynchronně. Je určen pro použití za běhu a není přímo v kódu.

## <a name="clientidseparator"></a>Oddělovač Klienti

Tato vlastnost vrátí znak používaný jako oddělovač při vytváření jedinečných ID klienta pro ovládací prvky. Je určen pro použití za běhu a není přímo v kódu.

## <a name="pagestatepersister"></a>Pagestatepersister

Tato vlastnost vrátí PageStatePersister objekt pro stránku. Tato vlastnost je primárně používán vývojáři ovládacího prvku ASP.NET.

## <a name="uniquefilepathsuffix"></a>Jedinečná přípona FilePathSuffix

Tato vlastnost vrátí jedinečnou příponu, která je připojena k cestě k souboru pro ukládání prohlížečů do mezipaměti. Výchozí hodnota \_ \_je ufps= a šestimístné číslo.

## <a name="new-public-methods-for-the-page-class"></a>Nové veřejné metody pro třídu Page

Následující veřejné metody jsou nové Page třídy v ASP.NET 2.0.

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

Tato metoda registruje delegáty obslužné rutiny události pro spuštění asynchronní stránky. Asynchronní stránky jsou popsány dále v tomto modulu.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

Aplikuje vlastnosti v šabloně stylů stránek na stránku.

## <a name="executeregisteredasynctasks"></a>SpustitpříkazAsynchronizační úkoly

Tato metoda se jedná o asynchronní úlohu.

### <a name="getvalidators"></a>GetValidátory

Vrátí kolekci validátorů pro zadanou skupinu ověření nebo výchozí ověřovací skupinu, pokud není zadánžádný.

## <a name="registerasynctask"></a>RegisterAsyncTask

Tato metoda registruje novou asynchronní úlohu. Asynchronní stránky jsou popsány dále v tomto modulu.

## <a name="registerrequirescontrolstate"></a>Registerrequirescontrolstate

Tato metoda ASP.NET říká, že stav ovládacího prvku stránky musí být trvalé.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

Tato metoda ASP.NET říká, že stav zobrazení stránek vyžaduje šifrování.

## <a name="resolveclienturl"></a>Adresa Klienta Přeložit

Vrátí relativní adresu URL, kterou lze použít pro požadavky klientů na obrázky atd.

## <a name="setfocus"></a>SetFocus

Tato metoda nastaví fokus na ovládací prvek, který je určen při počátečním načtení stránky.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState UnregisterRequiresControlState UnregisterRequiresControlState Unregister

Tato metoda zruší registraci ovládacího prvku, který je předán k němu jako již nevyžaduje trvalost stavu ovládacího prvku.

## <a name="changes-to-the-page-lifecycle"></a>Změny životního cyklu stránky

Životní cyklus stránky v ASP.NET 2.0 se dramaticky nezměnil, ale existují některé nové metody, které byste měli vědět. Životní cyklus stránky ASP.NET 2.0 je popsán níže.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (Novinka v ASP.NET 2.0)

Událost PreInit je nejranější fází životního cyklu, ke kterému má vývojář přístup. Přidání této události umožňuje programově měnit motivy ASP.NET 2.0, vzorové stránky, vlastnosti přístupu pro ASP.NET 2.0 profil atd. Pokud jste ve stavu postback, jeho důležité si uvědomit, že Viewstate dosud nebyla použita na ovládací prvky v tomto okamžiku životního cyklu. Proto pokud vývojář změní vlastnost ovládacího prvku v této fázi, bude pravděpodobně přepsána později v životním cyklu stránek.

## <a name="init"></a>Init

Událost Init se nezměnila z ASP.NET 1.x. Toto je místo, kde byste chtěli číst nebo inicializovat vlastnosti ovládacích prvků na stránce. V této fázi jsou na stránku již použity stránky předlohy, motivy atd.

## <a name="initcomplete-new-in-20"></a>InitComplete (Novinka v 2.0)

Událost InitComplete je volána na konci fáze inicializace stránek. V tomto okamžiku životního cyklu můžete získat přístup k ovládacím prvkům na stránce, ale jejich stav ještě nebyl naplněn.

## <a name="preload-new-in-20"></a>Předpětí (novinka v 2.0)

Tato událost je volána po použití všech dat\_postback a těsně před načtení stránky.

## <a name="load"></a>Načtení

Událost Load se nezměnila z ASP.NET 1.x.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (Novinka v 2.0)

Událost LoadComplete je poslední událostí ve fázi načítání stránek. V této fázi byla na stránce použita všechna data postback a viewstate.

## <a name="prerender"></a>Prerender

Pokud chcete, aby byl stav zobrazení správně udržován pro ovládací prvky, které jsou přidány na stránku dynamicky, je událost PreRender poslední příležitostí k jejich přidání.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (Novinka v 2.0)

Ve fázi PreRenderComplete byly na stránku přidány všechny ovládací prvky a stránka je připravena k vykreslení. Událost PreRenderComplete je poslední událost vyzdvižená před uložením stavu zobrazení stránek.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (Novinka v 2.0)

SaveStateComplete událost je volána okamžitě po uložení všech stav zobrazení stránky a stav ovládacího prvku. Toto je poslední událost před stránkou je skutečně vykreslen do prohlížeče.

## <a name="render"></a>Vykreslování

Metoda Render se od ASP.NET 1.x nezměnila. Toto je místo, kde je inicializován HtmlTextWriter a stránka je vykreslen a prohlížeč.

## <a name="cross-page-postback-in-aspnet-20"></a>Cross-Page Postback v ASP.NET 2.0

V ASP.NET 1.x, postbacks byly povinny psát na stejné stránce. Cross-page postbacks nebyly povoleny. ASP.NET 2.0 přidává možnost zaúčtovat zpět na jinou stránku prostřednictvím rozhraní IButtonControl. Jakýkoli ovládací prvek, který implementuje nové rozhraní IButtonControl (Button, LinkButton a ImageButton kromě vlastních ovládacích prvků třetích stran) může využít této nové funkce pomocí atributu PostBackUrl. Následující kód zobrazuje button ovládací prvek, který příspěvky zpět na druhou stránku.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Když je stránka zaúčtována zpět, stránka, která iniciuje postback, je přístupná prostřednictvím vlastnosti PreviousPage na druhé stránce. Tato funkce je implementována\_prostřednictvím nové funkce WebForm DoPostBackWithOptions na straně klienta, která ASP.NET 2.0 vykreslí na stránku, když ovládací prvek odešle zpět na jinou stránku. Tato funkce JavaScriptu je poskytována novou obslužnou rutinou WebResource.axd, která vyzařuje skript klientovi.

Video níže je návod cross-page postback.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Otevřít video na celou obrazovku](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Další podrobnosti o cross-Page Postbacks

### <a name="viewstate"></a>Viewstate

Možná jste se již ptali sami sebe o tom, co se stane se stavem zobrazení z první stránky ve scénáři postback u několika stránek. Koneckonců, jakýkoli ovládací prvek, který neimplementuje IPostBackDataHandler bude přetrvávat jeho stav prostřednictvím viewstate, tak mít přístup k vlastnostem tohoto ovládacího prvku na druhé stránce cross-page postback, musíte mít přístup ke stavu zobrazení pro stránku. ASP.NET 2.0 se postará o tento scénář pomocí nového skrytého pole na druhé stránce s názvem \_ \_PREVIOUSPAGE. Pole \_ \_formuláře PREVIOUSPAGE obsahuje stav zobrazení pro první stránku, takže můžete mít přístup k vlastnostem všech ovládacích prvků na druhé stránce.

### <a name="circumventing-findcontrol"></a>Obcházení FindControl

V návodu k videu cross-page postback, Použil jsem FindControl metoda získat odkaz na textbox ovládacíprvek na první stránce. Tato metoda funguje dobře pro tento účel, ale FindControl je nákladné a vyžaduje psaní dalšího kódu. Naštěstí ASP.NET 2.0 poskytuje alternativu k FindControl pro tento účel, který bude fungovat v mnoha scénářích. Direktiva PreviousPageType umožňuje mít silný odkaz na předchozí stránku pomocí atributu TypeName nebo VirtualPath. Atribut TypeName umožňuje určit typ předchozí stránky, zatímco atribut VirtualPath umožňuje odkazovat na předchozí stránku pomocí virtuální cesty. Po nastavení PředchozíPageType směrnice, potom je nutné vystavit ovládací prvky, atd., ke kterému chcete povolit přístup pomocí veřejných vlastností.

## <a name="lab-1-cross-page-postback"></a>Laboratoř 1 Cross-Page Postback

V tomto testovacím prostředí vytvoříte aplikaci, která používá novou funkci zpětného odeslání mezi stránkami ASP.NET 2.0.

1. Otevřete visual studio 2005 a vytvořte nový ASP.NET webu.
2. Přidejte nový webový formulář s názvem page2.aspx.
3. Otevřete soubor Default.aspx v návrhovém zobrazení a přidejte ovládací prvek Button a ovládací prvek TextBox. 

    1. Pojmenujte ovládací prvek Button iD **submitbutton** a ovládací prvek TextBox iD **uživatelského jména**.
    2. Nastavte vlastnost PostBackUrl tlačítka na page2.aspx.
4. Otevřete stránku page2.aspx ve zdrojovém zobrazení.
5. Přidejte direktivu @ PreviousPageType, jak je znázorněno níže:
6. Přidejte následující kód\_do kódu page2.aspx: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Sestavte projekt kliknutím na Sestavení v nabídce Sestavení.
8. Přidejte následující kód na pozadí kódu pro Default.aspx: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Změňte\_načtení stránky na stránce page2.aspx na následující: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Sestavte projekt.
11. Spusťte projekt.
12. Zadejte své jméno do textového pole a klepněte na tlačítko.
13. Jaký je výsledek?

## <a name="asynchronous-pages-in-aspnet-20"></a>Asynchronní stránky v ASP.NET 2.0

Mnoho konfliktproblémy v ASP.NET jsou způsobeny latencí externích volání (například webové služby nebo volání databáze), vplatnosti souboru latence atd. Pokud je požadavek podán proti ASP.NET aplikaci, ASP.NET používá jeden ze svých pracovních podprocesů k obslužit tento požadavek. Tento požadavek vlastní toto vlákno, dokud není požadavek dokončen a odpověď byla odeslána. ASP.NET 2.0 se snaží vyřešit problémy s latencí s těmito typy problémů přidáním schopnosti spouštět stránky asynchronně. To znamená, že pracovní podproces můžete spustit požadavek a potom předat další spuštění do jiného vlákna, a tím se vrátí do fondu dostupných vláken rychle. Po dokončení vi, volání databáze atd.

Prvním krokem při provádění stránky asynchronně je nastavení atributu **Async** směrnice stránky takto:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Tento atribut ASP.NET sděluje implementaci ihttpasyncHandler pro stránku.

Dalším krokem je volání addOnPreRenderCompleteAsync metoda v bodě v životním cyklu stránky před PreRender. (Tato metoda se obvykle\_nazývá v zatížení stránky.) Metoda AddOnPreRenderCompleteAsync má dva parametry; a BeginEventHandler a EndEventHandler. BeginEventHandler vrátí IAsyncResult, který je pak předán jako parametr EndEventHandler.

Video níže je návod asynchronní stránky požadavku.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Otevřít video na celou obrazovku](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Asynchronní stránka se nevykresluje do prohlížeče, dokud endEventHandler nedokončí. Není pochyb o tom, ale že někteří vývojáři budou myslet asynchronní požadavky jako podobné asynchronní zpětná volání. Je důležité si uvědomit, že nejsou. Výhodou pro asynchronní požadavky je, že první pracovní podproces může být vrácena do fondu vláken pro servis nových požadavků, čímž se sníží tvrzení z důvodu vi vázané, atd.

## <a name="script-callbacks-in-aspnet-20"></a>Script Callbacks v ASP.NET 2.0

Weboví vývojáři vždy hledali způsoby, jak zabránit blikání spojené s zpětným voláním. V ASP.NET 1.x, SmartNavigation byla nejběžnější metoda, jak se vyhnout blikání, ale SmartNavigation způsobil problémy pro některé vývojáře z důvodu složitosti jeho implementace na straně klienta. ASP.NET 2.0 řeší tento problém pomocí zpětných volání skriptů. Zpětná volání skriptů využívají protokol XMLHttp k požadavkům na webový server prostřednictvím jazyka JavaScript. Požadavek XMLHttp vrátí data XML, se kterými lze manipulovat prostřednictvím objektu DOM prohlížeče. Nový obslužný zdroj WebResource.axd skryje uživateli kód XMLHttp.

Existuje několik kroků, které jsou nezbytné pro konfiguraci zpětného volání skriptu v ASP.NET 2.0.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>Krok 1 : Implementace rozhraní ICallbackEventHandler

Aby ASP.NET rozpoznat vaši stránku jako účast na zpětném volání skriptu, musíte implementovat rozhraní ICallbackEventHandler. Můžete to udělat v souboru s kódem na pozadí, například takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Můžete to také provést pomocí @ Implements směrnice, jako je takto:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

Obvykle byste použít @ Implements směrnice při použití vřádík ASP.NET kódu.

## <a name="step-2--call-getcallbackeventreference"></a>Krok 2: Volání GetCallbackEventReference

Jak již bylo zmíněno dříve, volání XMLHttp je zapouzdřeno v obslužné rutině WebResource.axd. Po vykreslení stránky přidá ASP.NET volání do\_webform docallback, což je klientský skript poskytovaný webresource.axd. Funkce WebForm\_DoCallback nahrazuje \_ \_funkci doPostBack pro zpětné volání. Nezapomeňte, \_ \_že doPostBack programově odešle formulář na stránce. Ve scénáři zpětného volání chcete zabránit postback, takže \_ \_doPostBack nebude stačit.

> [!NOTE]
> \_\_doPostBack je stále vykreslen na stránku ve scénáři zpětného volání klientského skriptu. Však se nepoužívá pro zpětné volání.

Argumenty pro funkci\_WebForm DoCallback na straně klienta jsou poskytovány prostřednictvím funkce GetCallbackEventReference na straně serveru, která by se normálně nazývala v zatížení stránky.\_ Typické volání GetCallbackEventReference může vypadat takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> V tomto případě cm je instancí ClientScriptManager. Třída ClientScriptManager bude zahrnuta později v tomto modulu.

Existuje několik přetížených verzí GetCallbackEventReference. V tomto případě jsou argumenty následující:

`this`

Odkaz na ovládací prvek, kde je volána GetCallbackEventReference. V tomto případě je to samotná stránka.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

Řetězec argument, který bude předán z kódu na straně klienta na straně serveru události. V tomto případě im předávání hodnoty rozevírací seznam s názvem ddlCompany.

`ShowCompanyName`

Název funkce na straně klienta, která přijme vrácenou hodnotu (jako řetězec) z události zpětného volání na straně serveru. Tato funkce bude volána pouze v případě, že je zpětné volání na straně serveru úspěšné. Proto z důvodu robustnosti se obecně doporučuje použít přetíženou verzi GetCallbackEventReference, která přebírá další řetězec argument určující název funkce na straně klienta spustit v případě chyby.

`null`

Řetězec představující funkci na straně klienta, kterou inicioval před zpětnou voláním na server. V tomto případě neexistuje žádný takový skript, takže argument je null.

`true`

Logická hodnota určující, zda má být zpětné volání provedeno asynchronně.

Volání WebForm\_DoCallback na straně klienta předá tyto argumenty. Proto při této stránce je vykreslen na straně klienta, tento kód bude vypadat takto:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

Všimněte si, že podpis funkce na straně klienta je trochu jiný. Funkce na straně klienta předá 5 řetězců a logická hodnota. Další řetězec (který je null ve výše uvedeném příkladu) obsahuje funkci na straně klienta, která bude zpracovávat všechny chyby z zpětného volání na straně serveru.

## <a name="step-3--hook-the-client-side-control-event"></a>Krok 3: Zavěste událost řízení na straně klienta

Všimněte si, že vrácená hodnota Výše uvedeného příkazu GetCallbackEventReference byla přiřazena proměnné řetězce. Tento řetězec se používá k připojení události na straně klienta pro ovládací prvek, který iniciuje zpětné volání. V tomto příkladu je zpětné volání iniciováno rozevírací seznam na stránce, takže chci připojit *událost OnChange.*

Chcete-li připojit událost na straně klienta, jednoduše přidejte obslužnou rutinu do značky na straně klienta následujícím způsobem:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

Připomeňme, že *cbRef* je vrácená hodnota z volání GetCallbackEventReference. Obsahuje volání WebForm\_DoCallback, který byl zobrazen výše.

## <a name="step-4--register-the-client-side-script"></a>Krok 4 : Registrace skriptu na straně klienta

Připomeňme, že volání GetCallbackEventReference zadalo, že skript na straně klienta s názvem **ShowCompanyName** bude spuštěn, když bude zpětné volání na straně serveru úspěšné. Tento skript je třeba přidat na stránku pomocí instance ClientScriptManager. (Třída ClientScriptManager bude popsána později v tomto modulu.) Děláte to takto:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>Krok 5 : Volání metod rozhraní ICallbackEventHandler

ICallbackEventHandler obsahuje dvě metody, které je třeba implementovat ve vašem kódu. Jsou **To RaiseCallbackEvent** a **GetCallbackEvent**.

**RaiseCallbackEvent** trvá řetězec jako argument a vrátí nic. Argument řetězce je předán z volání na\_straně klienta webform DoCallback. V tomto případě je tato hodnota *atributem hodnoty* rozevíracího souboru s názvem ddlCompany. Kód na straně serveru by měl být umístěn do metody RaiseCallbackEvent. Například pokud zpětné volání provádí WebRequest proti externí prostředek, tento kód by měl být umístěn v RaiseCallbackEvent.

**GetCallbackEvent** je zodpovědný za zpracování vrácení zpětného volání klientovi. Trvá žádné argumenty a vrátí řetězec. Řetězec, který vrátí, bude předán jako argument funkci na straně klienta, v tomto případě *ShowCompanyName*.

Po dokončení výše uvedených kroků jste připraveni provést zpětné volání skriptu v ASP.NET 2.0.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Otevřít video na celou obrazovku](the-asp-net-2-0-page-model/_static/callback1.wmv)

Zpětná volání skriptů v ASP.NET jsou podporována v libovolném prohlížeči, který podporuje volání XMLHttp. To zahrnuje všechny moderní prohlížeče, které se dnes používají. Aplikace Internet Explorer používá objekt XMLHttp ActiveX, zatímco jiné moderní prohlížeče (včetně nadcházejícíverze IE 7) používají vnitřní objekt XMLHttp. Chcete-li programově určit, zda prohlížeč podporuje zpětná volání, můžete použít **vlastnost Request.Browser.SupportCallback.** Tato vlastnost vrátí **true,** pokud žádající klient podporuje zpětná volání skriptu.

## <a name="working-with-client-script-in-aspnet-20"></a>Práce s klientským skriptem v ASP.NET 2.0

Klientské skripty v ASP.NET 2.0 jsou spravovány pomocí třídy ClientScriptManager. Třída ClientScriptManager sleduje klientské skripty pomocí typu a názvu. Tím zabráníte programovému vložení stejného skriptu na stránku více než jednou.

> [!NOTE]
> Po úspěšném zaregistrování skriptu na stránce bude jakýkoli následný pokus o registraci stejného skriptu jednoduše za následek, že skript nebude zaregistrován podruhé. Nejsou přidány žádné duplicitní skripty a nedojde k žádné výjimce. Chcete-li se vyhnout zbytečným výpočtům, existují metody, které můžete použít k určení, zda je skript již registrován, takže se jej nepokoušíte zaregistrovat více než jednou.

Metody ClientScriptManager by měly být známé všem současným vývojářům ASP.NET:

## <a name="registerclientscriptblock"></a>Registerclientscriptblock

Tato metoda přidá skript na horní část vykreslené stránky. To je užitečné pro přidání funkcí, které budou explicitně volány na straně klienta.

Existují dvě přetížené verze této metody. Tři ze čtyř argumentů jsou mezi nimi běžné. Jsou to tyto:

`type (string)`

Argument ***typu*** identifikuje typ skriptu. Obecně je vhodné použít typ stránky (toto. GetType()) pro typ.

`key (string)`

***Klíčovým*** argumentem je uživatelem definovaný klíč pro skript. To by mělo být jedinečné pro každý skript. Pokud se pokusíte přidat skript se stejným klíčem a typem již přidaného skriptu, nebude přidán.

`script (string)`

Argument ***skriptu*** je řetězec obsahující skutečný skript, který má být přidejte. Doporučujeme použít StringBuilder k vytvoření skriptu a potom použít Metodu ToString() na StringBuilder přiřadit argument ***skriptu.***

Pokud použijete přetížený RegisterClientScriptBlock, který trvá pouze tři argumenty, &lt;musíte&gt;do skriptu zahrnout elementy skriptu (&lt;skript&gt; a /script).

Můžete použít přetížení RegisterClientScriptBlock, který trvá čtvrtý argument. Čtvrtým argumentem je logická hodnota, která určuje, zda ASP.NET má přidat prvky skriptu za vás. Pokud je tento argument **pravdivý**, skript by neměl obsahovat prvky skriptu explicitně.

Pomocí metody IsClientScriptBlockRegistered určete, zda již byl skript zaregistrován. To vám umožní vyhnout se pokusu o opětovnou registraci skriptu, který již byl zaregistrován.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (Novinka v 2.0)

Značka RegisterClientScriptInclude vytvoří blok skriptu, který odkazuje na externí soubor skriptu. Má dvě přetížení. Jeden má klíč a URL. Druhý přidá třetí argument určující typ.

Například následující kód generuje blok skriptu, který odkazuje na soubor jsfunctions.js v kořenovém adresáři složky skriptů aplikace:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Tento kód vytváří následující kód na vykreslené stránce:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> Blok skriptu je vykreslen v dolní části stránky.

Pomocí metody IsClientScriptIncludeRegistered určete, zda již byl skript zaregistrován. To vám umožní vyhnout se pokusu o opětovné registraci skriptu.

## <a name="registerstartupscript"></a>Registerstartupscript

Metoda RegisterStartupScript přebírá stejné argumenty jako metoda RegisterClientScriptBlock. Skript registrovaný pomocí RegisterStartupScript se spustí po načtení stránky, ale před událostí na straně klienta OnLoad. V 1.X byly skripty registrované na RegisterStartupScript &lt;umístěny těsně před uzavírací značkou /form,&gt; zatímco &lt;&gt; skripty registrované u RegisterClientScriptBlock byly umístěny bezprostředně za počáteční značku formuláře. V ASP.NET 2.0 jsou obě umístěny bezprostředně před uzavírací &lt;/form&gt; tag.

> [!NOTE]
> Pokud zaregistrujete funkci s RegisterStartupScript, tato funkce se nespustí, dokud ji explicitně nezavoláte v kódu na straně klienta.

Pomocí metody IsStartupScriptRegistered určete, zda již byl skript zaregistrován, a vyhněte se pokusu o opětovnou registraci skriptu.

## <a name="other-clientscriptmanager-methods"></a>Jiné metody ClientScriptManager

Zde jsou některé z dalších užitečných metod třídy ClientScriptManager.

|  <strong>GetCallbackEventReference</strong>   |                                                 Viz zpětná volání skriptu dříve v tomto modulu.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                Získá referenční javascript (javascript:&lt;volání),&gt;který lze použít k odeslání zpět z události na straně klienta.                 |
|  <strong>Getpostbackeventreference</strong>   |                                   Získá řetězec, který lze použít k zahájení post zpět z klienta.                                    |
|      <strong>GetWebResourceUrl</strong>       | Vrátí adresu URL prostředku, který je vložen do sestavení. Musí být použit ve spojení s <strong>RegisterClientScriptResource</strong>. |
| <strong>Registerclientscriptresource</strong> |     Zaregistruje webový prostředek se stránkou. Jedná se o prostředky vložené do sestavení a zpracované novou obslužnou rutinou WebResource.axd.      |
|     <strong>RegisterHiddenField</strong>      |                                                 Zaregistruje skryté pole formuláře se stránkou.                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  Registruje kód na straně klienta, který se spustí při odeslání formuláře HTML.                                   |
