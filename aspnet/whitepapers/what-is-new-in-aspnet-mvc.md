---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: Co je nového v ASP.NET MVC 2 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje nové funkce a vylepšení, které přináší ASP.NET MVC 2. Tento dokument je také k dispozici ke stažení.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045036"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>Novinky v ASP.NET MVC 2

> Tento dokument popisuje nové funkce a vylepšení, které přináší ASP.NET MVC 2. Tento dokument je také k dispozici ke [stažení](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf) .

[Ukázek](#_TOC1)   
[Upgrade projektu ASP.NET MVC 1,0 na ASP.NET MVC 2](#_TOC2)   
[Nové funkce](#_TOC3)   
[Pomocník s šablonami](#_TOC3_1)   
[Místa](#_TOC3_2)   
[Podpora pro asynchronní řadiče](#_TOC3_3)   
[Podpora DefaultValueAttribute – v parametrech Action-Method](#_TOC3_4)   
[Podpora pro svázání binárních dat s pojivy modelu](#_TOC3_5)   
[Třídy ModelMetadata a ModelMetadataProvider](#_TOC3_6)   
[Podpora atributů pro dataanotace](#_TOC3_7)   
[Poskytovatelé validátoru modelu](#_TOC3_8)   
[Ověřování na straně klienta](#_TOC3_9)   
[Nové fragmenty kódu pro Visual Studio 2010](#_TOC3_10)   
[Filtr akcí nového RequireHttpsAttribute](#_TOC3_11)   
[Přepsání příkazu metody HTTP](#_TOC3_12)   
[Nová třída HiddenInputAttribute pro pomocníky s šablonami](#_TOC3_13)   
[Pomocná metoda HTML. ovládací souhrnu ověření může zobrazit chyby na úrovni modelu.](#_TOC3_14)   
[Šablony T4 v aplikaci Visual Studio generují kód, který je specifický pro cílovou verzi rozhraní .NET Framework](#_TOC3_15)[API vylepšení](#_TOC4) .  
[Průlomové změny](#_TOC5)  
[Disclaimer](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  Ukázek

ASP.NET MVC 2 staví na ASP.NET MVC 1,0 a zavádí velkou sadu vylepšení a funkcí, které se zaměřují na zvýšení produktivity. Tato verze je kompatibilní s ASP.NET MVC 1,0, takže nadále platí všechny vaše znalosti, dovednosti, kód a rozšíření pro ASP.NET MVC 1,0.

Další informace o ASP.NET MVC najdete v následujících zdrojích informací:

- [Dokumentace k ASP.NET MVC na webu MSDN](https://go.microsoft.com/fwlink/?LinkId=159758)
- [Web ASP.NET MVC](https://asp.net/mvc/)
- [Fóra ASP.NET MVC](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  Upgrade projektu ASP.NET MVC 1,0 na ASP.NET MVC 2

ASP.NET MVC 2 se dá nainstalovat souběžně s ASP.NET MVC 1,0 na stejném serveru, který vývojářům aplikací nabízí flexibilitu při rozhodování o upgradu aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2. Informace o tom, jak upgradovat, najdete v dokumentu [Upgrade aplikace ASP.NET mvc 1,0 na ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).

## <a name="new-features"></a><a id="_TOC3"></a>  Nové funkce

Tato část popisuje funkce, které byly představeny ve verzi MVC 2.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  Pomocník s šablonami

Pomocníky s šablonou umožňují automaticky přidružit prvky HTML pro úpravy a zobrazení s datovými typy. Například pokud se data typu System. DateTime zobrazí v zobrazení, prvek uživatelského rozhraní pro výběr data lze automaticky vygenerovat. To se podobá tomu, jak šablony polí fungují v ASP.NET dynamická data. Další informace najdete v tématu [použití pomocníků se šablonami k zobrazení dat](https://go.microsoft.com/fwlink/?LinkId=159062) na webu MSDN.

### <a name="areas"></a><a id="_TOC3_2"></a>  Místa

Oblasti umožňují organizovat velký projekt do několika menších částí, aby bylo možné spravovat složitost velké webové aplikace. Každý oddíl ("Area") obvykle představuje samostatný oddíl velkého webu a používá se k seskupení souvisejících sad řadičů a zobrazení. Další informace najdete v tématu [Návod: uspořádání aplikace MVC ASP.NET podle oblastí](https://go.microsoft.com/fwlink/?LinkId=158978) na webu MSDN.

Chcete-li vytvořit novou oblast, v Průzkumník řešení klikněte pravým tlačítkem myši na projekt, klikněte na položku Přidat a poté klikněte na možnost oblast. Tím se zobrazí dialogové okno s výzvou k zadání názvu oblasti. Až zadáte název oblasti, Visual Studio přidá novou oblast do projektu.

Následující obrázek ukazuje příklad rozložení projektu se dvěma oblastmi, správci a blogy.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

Když vytvoříte oblast, Visual Studio přidá třídu, která je odvozena z AreaRegistration do každé oblasti. Tato třída je vyžadována, aby se mohla zaregistrovat oblast a její trasy, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

Výchozí šablona projektu pro ASP.NET MVC 2 obsahuje volání metody RegisterAllAreas v kódu pro soubor Global. asax. Tato metoda registruje každou oblast v projektu tím, že hledá všechny typy, které jsou odvozeny z třídy AreaRegistration, vytvoří instanci instance typu a pak zavolá metodu RegisterArea na instanci. Následující příklad ukazuje, jak je to hotové.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Pokud neurčíte obor názvů v metodě RegisterArea voláním kontextu. Namespaces. Add – metoda, ve výchozím nastavení se používá obor názvů třídy registrace.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  Podpora pro asynchronní řadiče

ASP.NET MVC 2 teď umožňuje řadičům zpracovávat požadavky asynchronně. To může vést k nárůstu výkonu tím, že umožňuje serverům, které často volají operace blokujících operací (například síťové požadavky), volat neblokující protějšky. Další informace najdete v tématu [použití asynchronního řadiče v ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) na webu MSDN.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  Podpora DefaultValueAttribute – v parametrech Action-Method

Třída System. ComponentModel. DefaultValueAttribute – umožňuje zadat výchozí hodnotu parametru argumentu metody Action. Předpokládejme například, že je definována následující výchozí trasa:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

Také předpokládá, že je definována následující metoda kontroleru a akce:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Kterákoli z následujících požadavků URL vyvolá metodu zobrazení akce, která je definována v předchozím příkladu.

- /Article/View/123
- /Article/View/123? Page = 1 (efektivně stejné jako u předchozí žádosti)
- /Article/View/123? stránka = 2

Bez atributu DefaultValueAttribute – nebude první adresa URL z předchozího seznamu fungovat, protože argument stránky je typ hodnoty, která není null, jejíž hodnota nebyla zadána.

Pokud je kód napsán v Visual Basic 2010 nebo Visual C# 2010, můžete místo atributu DefaultValueAttribute – použít volitelné parametry, jak je znázorněno v následujícím příkladu:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  Podpora pro svázání binárních dat s pojivy modelu

Existují dvě nová přetížení HTML. skryté pomocné rutiny, které zakódují binární hodnoty jako řetězce kódované jako Base-64:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Typickým použitím je vložení časového razítka pro objekt v zobrazení. Například vaše aplikace může obsahovat následující objekt produktu:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Formulář pro úpravy může vykreslit vlastnost časového razítka ve formuláři, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Tento kód vykresluje skrytý element input s hodnotou časového razítka jako řetězec kódovaný jako základní-64, který se podobá následujícímu příkladu:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Tento formulář může být odeslán do metody akce, která má argument typu produkt, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

V metodě Action je vlastnost TimeStamp správně naplněná, protože odeslaný řetězec kódovaný od základního 64 je převeden na bajtové pole.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  Třídy ModelMetadata a ModelMetadataProvider

Třída ModelMetadataProvider poskytuje abstrakci pro získání metadat pro model v rámci zobrazení. MVC 2 obsahuje výchozího zprostředkovatele, který zpřístupňuje metadata, která jsou zveřejněna pomocí atributů v oboru názvů System. ComponentModel. DataAnnotations. Je možné vytvořit zprostředkovatele metadat, kteří poskytují metadata z jiných úložišť dat, jako jsou databáze nebo soubory XML.

Třída ViewDataDictionary zpřístupňuje objekt ModelMetadata, který obsahuje metadata extrahovaná z modelu třídou ModelMetadataProvider. To umožní pomocníkům v šablonách spotřebovat tato metadata a odpovídajícím způsobem upravit jejich výstup.

Další informace najdete v dokumentaci ke třídám [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) a [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) .

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  Podpora atributů pro dataanotace

ASP.NET MVC 2 podporuje použití ověřovacích atributů RangeAttribute, RequiredAttribute, StringLengthAttribute a RegexAttribute (definované v oboru názvů System. ComponentModel. DataAnnotations) při vytváření vazby k modelu za účelem zajištění ověření vstupu.

Další informace naleznete v tématu [How to: Validate data modelu pomocí atributů DataAnnotations](https://go.microsoft.com/fwlink/?LinkId=159063) na webu MSDN. Vzorový projekt, který znázorňuje použití těchto atributů, je k dispozici ke stažení v [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  Poskytovatelé validátoru modelu

Třída zprostředkovatele ověřování modelu představuje abstrakci, která pro model poskytuje logiku ověřování. ASP.NET MVC obsahuje výchozího zprostředkovatele na základě atributů ověřování, které jsou obsaženy v oboru názvů System. ComponentModel. DataAnnotations. Můžete také vytvořit vlastní poskytovatele ověřování, který definuje vlastní ověřovací pravidla a vlastní mapování ověřovacích pravidel k modelu. Další informace najdete v dokumentaci ke třídě [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) .

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  Ověřování na straně klienta

Třída poskytovatele validátoru modelu zveřejňuje metadata ověřování v prohlížeči ve formě dat serializovaných ve formátu JSON, která lze spotřebovat pomocí knihovny ověřování na straně klienta. ASP.NET MVC 2 zahrnuje knihovnu ověřování klienta a adaptér, který podporuje atributy ověřování oboru názvů DataAnnotations, které jste si poznamenali dříve. Třída Provider také umožňuje používat jiné knihovny ověřování klienta zápisem adaptéru, který zpracovává data JSON a volá do alternativní knihovny.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  Nové fragmenty kódu pro Visual Studio 2010

Sada fragmentů kódu HTML pro ASP.NET MVC 2 je nainstalována společně se sadou Visual Studio 2010. Chcete-li zobrazit seznam těchto fragmentů kódu, v nabídce Nástroje vyberte Správce fragmentů kódů. V části jazyk vyberte HTML a pro umístění vyberte ASP.NET MVC 2. Další informace o tom, jak používat fragmenty kódu, naleznete v dokumentaci k sadě Visual Studio.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  Filtr akcí nového RequireHttpsAttribute

ASP.NET MVC 2 obsahuje novou třídu RequireHttpsAttribute, kterou lze použít na metody a řadiče akcí. Ve výchozím nastavení filtr přesměruje požadavek bez SSL (HTTP) na ekvivalent SSL (HTTPS) s povoleným protokolem SSL.

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  Přepsání příkazu metody HTTP

Při vytváření webu pomocí stylu architektury REST se k určení akce, která má provést pro prostředek, používá příkaz HTTP. REST vyžaduje, aby aplikace podporovaly celou škálu běžných příkazů HTTP, včetně GET, PUT, POST a DELETE.

ASP.NET MVC 2 obsahuje nové atributy, které se dají použít na metody akcí a tuto zkomprimovanou syntaxi funkce. Tyto atributy umožňují ASP.NET MVC vybrat metodu akce založenou na příkazu HTTP. V následujícím příkladu požadavek POST vyvolá metodu First Action a požadavek PUT zavolá druhou metodu Action.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

V dřívějších verzích ASP.NET MVC tyto metody vyžadují podrobnou syntaxi, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Vzhledem k tomu, že prohlížeče podporují pouze příkazy GET a POST HTTP, není možné vystavit akci, která vyžaduje jinou operaci. Proto není možné nativně podporovat všechny požadavky RESTful.

ASP.NET MVC 2 však zavádí novou pomocnou metodu HttpMethodOverride HTML, aby podporovala žádosti RESTful během operace POST. Tato metoda vykresluje skrytý vstupní prvek, který způsobí, že formulář bude efektivně emulovat jakoukoli metodu HTTP. Například pomocí pomocné metody HttpMethodOverride HTML můžete mít odeslání formuláře jako požadavek PUT nebo DELETE. Chování HttpMethodOverride má vliv na následující atributy:

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

Skrytý vstupní element má svůj název X-HTTP-Method-override a jeho hodnotu nastavenou na příkaz HTTP, který se emuluje. Hodnotu přepsání lze také zadat v hlavičce HTTP nebo v hodnotě řetězce dotazu jako dvojici název-hodnota.

Přepsání lze použít pouze v případě, že skutečný požadavek je požadavek POST. Hodnota přepsání bude ignorována u požadavků, které používají jakýkoli jiný příkaz HTTP.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  Nová třída HiddenInputAttribute pro pomocníky s šablonami

Nový atribut HiddenInputAttribute lze použít pro vlastnost modelu, aby označoval, zda má být při zobrazení modelu v šabloně editoru vykreslen skrytý element input. (Atribut nastaví implicitní hodnotu UIHint HiddenInput). Vlastnost DisplayValue atributu umožňuje určit, zda se má hodnota zobrazovat v editoru a v režimech zobrazení. Pokud je DisplayValue nastaveno na hodnotu false, nezobrazí se nic, ani kód HTML, který obvykle obklopuje pole. Výchozí hodnota pro DisplayValue je true.

V následujících scénářích můžete použít atribut HiddenInputAttribute:

- Když zobrazení umožňuje uživatelům upravit ID objektu a je nezbytné k zobrazení hodnoty a k poskytnutí skrytého vstupního prvku, který obsahuje staré ID, aby jej bylo možné předat zpět do kontroleru.
- Když zobrazení umožní uživatelům upravit binární vlastnost, která by neměla být nikdy zobrazená, jako je například vlastnost timestamp. V takovém případě se nezobrazí hodnota a okolní kód HTML (například popisek a hodnota).

Následující příklad ukazuje, jak použít třídu HiddenInputAttribute.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Pokud je atribut nastaven na hodnotu true (nebo není zadán žádný parametr), dojde k následujícímu:

- V šablonách zobrazení se popisek vykreslí a hodnota se zobrazí uživateli.
- V šablonách editoru je popisek vykreslen a hodnota je vykreslena ve skrytém elementu Input.

Pokud je atribut nastaven na hodnotu false, dojde k následujícímu:

- V šablonách zobrazení není pro toto pole vykreslena žádná data.
- V šablonách editoru není vykreslen žádný popisek a hodnota je vykreslena ve skrytém vstupním elementu.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  Pomocná metoda HTML. ovládací souhrnu ověření může zobrazit chyby na úrovni modelu.

Namísto zobrazování všech chyb ověřování obsahuje pomocná metoda HTML. ovládací souhrnu ověření novou možnost zobrazení pouze chyb na úrovni modelu. To umožňuje zobrazení chyb na úrovni modelu v souhrnu ověření a chyby specifické pro pole, které se mají zobrazit vedle jednotlivých polí.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  Šablony T4 v aplikaci Visual Studio generují kód, který je specifický pro cílovou verzi .NET Framework

K dispozici je nová vlastnost pro soubory T4 z hostitele ASP.NET MVC T4, který určuje verzi .NET Framework, kterou používá aplikace. To umožňuje šablonám T4 generovat kód a značky, které jsou specifické pro verzi .NET Framework. V aplikaci Visual Studio 2008 je hodnota vždy .NET 3,5. V aplikaci Visual Studio 2010 je hodnota buď .NET 3,5 nebo .NET 4.

## <a name="api-improvements"></a><a id="_TOC4"></a>  Vylepšení rozhraní API

Tato část popisuje změny stávajících typů a členů ASP.NET MVC.

- Do třídy Controller se přidala chráněná virtuální metoda CreateActionInvoker. Tato metoda je vyvolána vlastností ActionInvoker kontroleru a umožňuje opožděné vytváření instancí původce, pokud už není nastavená původce.
- Do třídy AuthorizeAttribute se přidala chráněná virtuální metoda HandleUnauthorizedRequest. To umožňuje filtrům odvozeným od AuthorizeAttribute řídit chování při neúspěchu autorizace.
- Do třídy ValueProviderDictionary se přidala metoda Add (řetězcový klíč, hodnota objektu). To umožňuje použít syntaxi inicializátoru slovníku pro ValueProviderDictionary, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- Do \_ třídy Sys. Mvc. AjaxContext se přidala metoda get Object. Toto je metoda JavaScriptu, která je podobná metodě Get \_ data, ale pokud je typ obsahu odpovědi Application/JSON, \_ vrátí objekt get objekt JSON.
- Do třídy AuthorizationContext se přidala vlastnost ActionDescriptor.
- Byl přidán UrlParameter. volitelný token, který lze použít k řešení problémů při vytváření vazby k modelu, který obsahuje vlastnost ID, pokud vlastnost chybí v příspěvku formuláře. Další podrobnosti najdete v tématu věnovaném [parametrům ASP.NET MVC 2 volitelné adresy URL](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) na blogu Filip Haack.

## <a name="breaking-changes"></a><a id="_TOC5"></a>  Průlomové změny

Následující změny můžou způsobit chyby v existujících aplikacích ASP.NET MVC 1,0.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>Změna chování při ověřování vlastností pro třídy, které implementují IDataErrorInfo

Pro objekty modelu, které používají IDataErrorInfo k ověřování, jsou všechny vlastnosti ověřeny bez ohledu na to, zda byla nastavena nová hodnota. V ASP.NET MVC 1,0 byly ověřeny pouze vlastnosti, u kterých byly nastaveny nové hodnoty. V ASP.NET MVC 2 je vlastnost Error třídy IDataErrorInfo volána pouze v případě, že byly všechny validátory vlastností úspěšné.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>Skript mapování skriptů služby IIS již není v instalačním programu k dispozici.

Skript mapování skriptů služby IIS je skript příkazového řádku, který se používá ke konfiguraci mapování skriptů pro IIS 6 a pro IIS 7 v klasickém režimu. Skript mapování skriptu není nutný, pokud používáte vývojový server sady Visual Studio nebo používáte službu IIS 7 v integrovaném režimu. Skripty jsou k dispozici jako samostatné nepodporované stažení v [Webstacku ASP.NET](https://github.com/aspnet/AspNetWebStack).

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>V termínech MVC již není k dispozici kód HTML. dosadit pomocná metoda.

Z důvodu změn v chování vykreslování modulů zobrazení MVC nefunguje metoda HTML. dosadit pomocná metoda a byla odebrána.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>Rozhraní IValueProvider nahrazuje všechna použití rozhraní IDictionary.

Všechny argumenty vlastnosti nebo metody, které přijaly rozhraní IDictionary v MVC 1,0, teď akceptují IValueProvider. Tato změna ovlivní pouze aplikace, které zahrnují vlastní zprostředkovatele hodnot nebo vlastní pořadače modelů. Mezi příklady vlastností a metod, které jsou ovlivněné touto změnou, patří následující:

- Vlastnost ValueProvider tříd ControllerBase a ModelBindingContext
- Metody TryUpdateModel třídy Controller

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Do souboru Web. CSS byly přidány nové třídy CSS.

Soubor Web. CSS v šablonách projektů ASP.NET MVC byl aktualizován tak, aby zahrnoval nové styly používané funkcemi ověřování a pomocníky s šablonami.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Pomocník nyní vrací objekt MvcHtmlString

Aby bylo možné využít novou syntaxi výrazu kódování HTML v ASP.NET 4, návratový typ pro pomocníky HTML je nyní MvcHtmlString namísto řetězce. Pokud používáte ASP.NET MVC 2 a nové pomocníky na ASP.NET 3,5, nebudete moci využít syntaxi kódování HTML; Nová syntaxe je k dispozici pouze v případě, že spustíte ASP.NET MVC 2 na ASP.NET 4.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult nyní reaguje pouze na požadavky HTTP POST.

Aby bylo možné zmírnit útoky napadení JSON, které mají potenciál pro zpřístupnění informací, třída JsonResult nyní reaguje pouze na požadavky HTTP POST. AJAX GET volá metody akcí, které vracejí objekt JsonResult, by měly být změněny na místo toho použít POST. V případě potřeby můžete toto chování přepsat nastavením nové vlastnosti JsonRequestBehavior třídy JsonResult. Další informace o potenciálním zneužití najdete v blogovém příspěvku o [zneužití JSON](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) na blogu Filip Haack.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>Nastavení modelu a vlastností typ modelu v ModelBindingContext jsou zastaralá.

Do třídy ModelBindingContext byla přidána nová nastavitelná vlastnost ModelMetadata. Nová vlastnost zapouzdřuje model i vlastnosti typ modelu. I když jsou vlastnosti modelu a typ modelu zastaralé pro zpětnou kompatibilitu, metoda getter vlastnosti stále funguje; k získání hodnoty deleguje vlastnost ModelMetadata.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Změny ve třídě DefaultControllerFactory, které vlastní továrny kontrolérů, které jsou z něj odvozeny

Třída DefaultControllerFactory byla opravena odebráním vlastnosti Třída requestContext. Namísto této vlastnosti je instance kontextu požadavku předána chráněným virtuálním metodám GetControllerInstance a GetControllerType. Tato změna má vliv na vlastní továrny kontrolérů, které jsou odvozeny z DefaultControllerFactory.

Vlastní továrny kontrolérů se často používají k zajištění vkládání závislostí pro aplikace ASP.NET MVC. Chcete-li aktualizovat vlastní továrny kontrolérů tak, aby podporovaly ASP.NET MVC 2, změňte signaturu nebo signatury metody tak, aby odpovídaly novým podpisům, a místo vlastnosti použijte parametr kontextu požadavku.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Oblast" je teď rezervovaný klíč hodnoty trasy.

Řetězec "oblast" v hodnotách tras má nyní zvláštní význam v ASP.NET MVC, stejně jako "Controller" a "Action". Jedním z nich je, že pokud jsou pomocníky jazyka HTML dodávány se slovníkem hodnot směrování, který obsahuje "oblast", v řetězci dotazu již nebude "oblast" připojovat.

Pokud používáte funkci oblasti, ujistěte se, že v rámci adresy URL trasy nepoužíváte aplikaci {Area}.

## <a name="disclaimer"></a><a id="_TOC6"></a>  Právní omezení

Toto je předběžný dokument a může být podstatně měněn před konečným komerčním vydáním softwaru popsaného v tomto dokumentu.

The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication. Vzhledem k tomu, že Microsoft musí reagovat na měnící se podmínky na trhu, neměl by být interpretován jako závazek společnosti Microsoft a společnost Microsoft nemůže zaručit přesnost všech informací, které jsou uvedeny po datu publikování.

Tento dokument White Paper slouží pouze k informativním účelům. SPOLEČNOST MICROSOFT NEPOSKYTUJE ŽÁDNÉ ZÁRUKY, AŤ UŽ VÝSLOVNĚ UVEDENÉ, PŘEDPOKLÁDANÉ NEBO STATUTÁRNÍ, JAKO INFORMACE V TOMTO DOKUMENTU.

Dodržování všech platných zákonů o autorských právech je zodpovědností uživatele. Bez omezení práv v rámci autorského práva nesmí být žádná část tohoto dokumentu reprodukována, ukládána do systému pro načítání nebo postoupena v jakémkoli tvaru nebo jakýmkoli způsobem (elektronickými, mechanicky, fotokopírováním, záznamem nebo jiným) nebo jakýmkoli účelem bez výslovného písemného svolení společnosti Microsoft Corporation.

Společnost Microsoft může mít patenty, patentové aplikace, ochranné známky, autorská práva nebo jiná práva duševního vlastnictví, která zahrnují předmět v tomto dokumentu. S výjimkou výslovně uvedených v písemné licenční smlouvě od společnosti Microsoft vám poskytnutí tohoto dokumentu neposkytuje žádnou licenci na tyto patenty, ochranné známky, autorská práva ani jiné duševní vlastnictví.

Pokud není uvedeno jinak, jsou ukázkové společnosti, organizace, produkty, názvy domén, e-mailové adresy, loga, osoby, místa a události uvedené v ukázkách smyšlené a bez jakýchkoli souvislostí se skutečnou společností, organizací, produktem, názvem domény, e-mailovou adresou, logem, osobou, místem nebo událostí by se měl odvodit.

© 2010 Microsoft Corporation. All rights reserved.

Microsoft a Windows jsou buď registrované ochranné známky, nebo ochranné známky společnosti Microsoft Corporation v USA a dalších zemích.

The names of actual companies and products mentioned herein may be the trademarks of their respective owners.
