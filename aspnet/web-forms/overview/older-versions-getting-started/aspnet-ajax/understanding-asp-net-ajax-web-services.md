---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: Porozumění webovým službám ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Webové služby jsou nedílnou součástí rozhraní .NET Framework, které poskytuje řešení pro různé platformy pro výměnu dat mezi distribuovanými systémy. Přestože Web...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2020
ms.locfileid: "86162777"
---
# <a name="understanding-aspnet-ajax-web-services"></a>Principy webových služeb technologie ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Webové služby jsou nedílnou součástí rozhraní .NET Framework, které poskytuje řešení pro různé platformy pro výměnu dat mezi distribuovanými systémy. I když se webové služby používají obvykle k tomu, aby pro posílání a přijímání dat používaly různé operační systémy, objektové modely a programovací jazyky, můžou se také použít k dynamickému vkládání dat na stránku ASP.NET AJAX nebo posílání dat ze stránky do back-endového systému. Vše lze provést bez nutnosti provádět operace zpětného odeslání.

## <a name="calling-web-services-with-aspnet-ajax"></a>Volání webových služeb pomocí ASP.NET AJAX

Dan Wahlin

Webové služby jsou nedílnou součástí rozhraní .NET Framework, které poskytuje řešení pro různé platformy pro výměnu dat mezi distribuovanými systémy. I když se webové služby používají obvykle k tomu, aby pro posílání a přijímání dat používaly různé operační systémy, objektové modely a programovací jazyky, můžou se také použít k dynamickému vkládání dat na stránku ASP.NET AJAX nebo posílání dat ze stránky do back-endového systému. Vše lze provést bez nutnosti provádět operace zpětného odeslání.

I když ovládací prvek UpdatePanel ASP.NET AJAX poskytuje jednoduchý způsob, jak AJAX povolit jakoukoli stránku ASP.NET, mohou nastat situace, kdy potřebujete dynamicky přistupovat k datům na serveru bez použití prvku UpdatePanel. V tomto článku se dozvíte, jak toho dosáhnout vytvořením a použitím webových služeb v rámci stránek ASP.NET AJAX.

Tento článek se zaměřuje na funkce, které jsou dostupné v základních rozšířeních ASP.NET AJAX, a také na ovládacím prvku s povolenými webovými službami v sadě ASP.NET AJAX Toolkit s názvem AutoCompleteExtender. Mezi zahrnutá témata patří definování webových služeb s podporou jazyka AJAX, vytváření proxy serverů klientů a volání webových služeb pomocí JavaScriptu. Také se dozvíte, jak lze volání webové služby provést přímo na ASP.NET metody stránky.

## <a name="web-services-configuration"></a>Konfigurace webových služeb

Když je v aplikaci Visual Studio 2008 vytvořen nový projekt webu, web.config soubor obsahuje řadu nových dodatků, které mohou být pro uživatele předchozích verzí sady Visual Studio neobeznámeny. Některé z těchto změn mapují prefix "ASP" na ASP.NET AJAX Controls, aby bylo možné je použít na stránkách, zatímco jiné definují požadované HttpHandlers a httpModules. Výpis 1 zobrazuje změny `<httpHandlers>` elementu v web.config, které ovlivňují volání webové služby. Výchozí hodnota HttpHandlers použitá pro zpracování volání. asmx je odebrána a nahrazena třídou ScriptHandlerFactory umístěnou v sestavení System.Web.Extensions.dll. System.Web.Extensions.dll obsahuje všechny základní funkce, které používá ASP.NET AJAX.

**Výpis 1. Konfigurace obslužných rutin webové služby ASP.NET AJAX**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

Tato náhrada HttpHandlers je provedena, aby bylo možné provést volání JavaScript Object Notation (JSON) ze stránek AJAX ASP.NET do webových služeb .NET pomocí proxy webové služby jazyka JavaScript. ASP.NET AJAX odesílá zprávy JSON webovým službám na rozdíl od standardních volání protokolu SOAP (Simple Object Access Protocol), která jsou obvykle přidružena k webovým službám. Výsledkem je menší zpráva žádosti a odpovědi. Umožňuje taky efektivnější zpracování dat na straně klienta, protože knihovna JavaScript ASP.NET AJAX je optimalizovaná pro práci s objekty JSON. Výpis 2 a výpis 3 zobrazí příklady požadavků webové služby a zpráv odpovědí serializovaných do formátu JSON. Zpráva požadavku uvedená v seznamu 2 předá parametr země s hodnotou "Belgie", zatímco zpráva s odpovědí v seznamu 3 předá pole zákaznických objektů a jejich přidružených vlastností.

**Výpis 2. Zpráva žádosti webové služby serializovaná do formátu JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]název operace je definován jako součást adresy URL webové služby. Kromě toho se zprávy požadavku neodesílají vždy prostřednictvím formátu JSON. Webové služby mohou využívat atribut ScriptMethod s parametrem UseHttpGet nastaveným na hodnotu true, což způsobí, že parametry budou předány prostřednictvím parametrů řetězce dotazu.*

**Výpis 3. Zpráva odpovědi webové služby serializovaná na JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

V další části se dozvíte, jak vytvořit webové služby, které umožňují zpracovávat zprávy s požadavky JSON a reagovat jak na jednoduché, tak i komplexní typy.

## <a name="creating-ajax-enabled-web-services"></a>Vytváření webových služeb s podporou jazyka AJAX

Rozhraní ASP.NET AJAX poskytuje několik různých způsobů, jak volat webové služby. Můžete použít ovládací prvek AutoCompleteExtender (dostupný v ASP.NET toolkitu AJAX) nebo v JavaScriptu. Nicméně před voláním služby, kterou máte v AJAX, povolte ji tak, aby ji mohl volat kód klientského skriptu.

Bez ohledu na to, jestli nejste u webových služeb ASP.NET, můžete jednoduše vytvořit služby a povolit služby AJAX. Rozhraní .NET Framework podporuje vytváření webových služeb ASP.NET od počáteční verze v 2002 a rozšíření ASP.NET AJAX poskytují další funkce AJAX, které jsou založeny na výchozí sadě funkcí rozhraní .NET Framework. Visual Studio .NET 2008 Beta 2 obsahuje integrovanou podporu pro vytváření souborů webové služby. asmx a automaticky odvozuje přidružený kód vedle tříd z třídy System. Web. Services. WebService. Při přidávání metod do třídy je nutné použít atribut WebMethod, aby bylo možné je volat příjemci webové služby.

Výpis 4 ukazuje příklad použití atributu WebMethod na metodu s názvem GetCustomersByCountry ().

**Výpis 4. Použití atributu WebMethod ve webové službě**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

Metoda GetCustomersByCountry () přijímá parametr země a vrací pole zákaznického objektu. Hodnota země předaná metodě je předána třídě obchodní vrstvy, která zase volá třídu datové vrstvy, aby načetla data z databáze, vyplní vlastnosti objektu zákazníka daty a vrátí pole.

## <a name="using-the-scriptservice-attribute"></a>Použití atributu ScriptService

Při přidání atributu WebMethod umožníte volání metody GetCustomersByCountry () klientům, kteří odesílají standardní zprávy protokolu SOAP do webové služby, nedovolují volání JSON z aplikací ASP.NET AJAX z okna. Aby bylo možné provést volání JSON, je nutné použít atribut rozšíření ASP.NET AJAX `ScriptService` pro třídu webové služby. Díky tomu může webová služba odesílat zprávy odpovědi formátované pomocí JSON a umožňuje skriptu na straně klienta volat službu posíláním zpráv JSON.

Výpis 5 ukazuje příklad použití atributu ScriptService na třídu webové služby s názvem CustomersService.

**Výpis 5. Použití atributu ScriptService pro AJAX – povolení webové služby**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

Atribut ScriptService funguje jako značka, která označuje, že je možné ji volat z kódu skriptu AJAX. Ve skutečnosti nezpracovává žádné úlohy serializace JSON nebo deserializace, ke kterým dochází na pozadí. ScriptHandlerFactory (nakonfigurovaný v web.config) a další související třídy jsou hromadné zpracování JSON.

## <a name="using-the-scriptmethod-attribute"></a>Použití atributu ScriptMethod

Atribut ScriptService je jediný atribut ASP.NET AJAX, který musí být definován ve webové službě .NET, aby jej bylo možné používat na stránkách ASP.NET AJAX. Nicméně jiný atribut s názvem ScriptMethod lze také použít přímo na webové metody v rámci služby. ScriptMethod definuje tři vlastnosti `UseHttpGet` , včetně, `ResponseFormat` a `XmlSerializeString` . Změna hodnot těchto vlastností může být užitečná v případech, kdy je třeba změnit typ požadavku akceptovaného webovou metodou, pokud webová metoda potřebuje vracet nezpracovaná data XML ve formě `XmlDocument` `XmlElement` objektu nebo nebo když data vrácená ze služby by měla být vždy serializována jako XML namísto JSON.

Vlastnost UseHttpGet lze použít, pokud webová metoda by měla přijímat požadavky GET na rozdíl od požadavků POST. Žádosti se odesílají pomocí adresy URL se vstupními parametry webové metody, které jsou převedené na parametry QueryString. Vlastnost UseHttpGet je nastavena na hodnotu false a měla by být nastavena pouze na to, `true` kdy jsou operace známé jako bezpečné a když nejsou citlivá data předávána webové službě. Výpis 6 ukazuje příklad použití atributu ScriptMethod s vlastností UseHttpGet.

**Výpis 6. Pomocí atributu ScriptMethod s vlastností UseHttpGet.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

Příklad záhlaví odeslaných při volání webové metody HttpGetEcho, která je uvedena v seznamu 6, se zobrazí jako další:

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

Kromě povolení, aby webové metody přijímaly požadavky HTTP GET, lze atribut ScriptMethod použít také v případě, že je nutné vrátit odpovědi XML ze služby spíše než pomocí formátu JSON. Webová služba může například načíst informační kanál RSS ze vzdáleného webu a vrátit jej jako objekt XmlDocument nebo XmlElement. Zpracování dat XML může následně probíhat na klientovi.

Výpis 7 ukazuje příklad použití vlastnosti ResponseFormat k určení, že by měla být vrácena data XML z webové metody.

**Výpis 7. Pomocí atributu ScriptMethod s vlastností ResponseFormat.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

Vlastnost ResponseFormat lze také použít společně s vlastností XmlSerializeString. Vlastnost XmlSerializeString má výchozí hodnotu false, což znamená, že všechny návratové typy s výjimkou řetězců vrácených z webové metody jsou serializovány jako XML, pokud `ResponseFormat` je vlastnost nastavena na `ResponseFormat.Xml` . `XmlSerializeString`Je-li nastavena na hodnotu `true` , všechny typy vrácené z webové metody jsou serializovány jako XML včetně typů řetězců. Pokud má vlastnost ResponseFormat hodnotu `ResponseFormat.Json` vlastnosti XmlSerializeString, bude ignorována.

Výpis 8 ukazuje příklad použití vlastnosti XmlSerializeString k vynucení řetězců, které mají být serializovány jako XML.

**Výpis 8. Použití atributu ScriptMethod s vlastností XmlSerializeString**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

Hodnota vrácená voláním webové metody GetXmlString zobrazené v seznamu 8 je uvedena dále:

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

I když výchozí formát JSON minimalizuje celkovou velikost zpráv požadavků a odpovědí a je snadněji využíván klienty ASP.NET AJAX v různých prohlížečích, lze vlastnosti ResponseFormat a XmlSerializeString využít, když klientské aplikace, jako je například aplikace Internet Explorer 5 nebo vyšší, očekávají vrácení dat XML z webové metody.

## <a name="working-with-complex-types"></a>Práce se složitými typy

Výpis 5 ukázal příklad vrácení komplexního typu s názvem zákazník z webové služby. Třída Customer definuje několik různých jednoduchých typů interně jako vlastnosti jako FirstName a LastName. Komplexní typy používané jako vstupní parametr nebo návratový typ u webové metody s podporou jazyka AJAX jsou automaticky serializovány do formátu JSON před odesláním na straně klienta. Vnořené komplexní typy (které jsou definovány interně v rámci jiného typu) však nebudou klientovi k dispozici jako samostatné objekty ve výchozím nastavení.

V případech, kdy se na stránce klienta musí použít vnořený komplexní typ používaný webovou službou, lze do webové služby přidat atribut ASP.NET AJAX GenerateScriptType. Například třída CustomerDetails zobrazená v seznamu 9 obsahuje vlastnosti adresa a pohlaví, které ***reprezentují vnořené komplexní typy.***

**Výpis 9. Zde uvedená třída CustomerDetails obsahuje dva vnořené komplexní typy.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

Objekty adresy a pohlaví definované v rámci třídy CustomerDetails zobrazené v seznamu 9 nebudou automaticky dostupné pro použití na straně klienta prostřednictvím JavaScriptu, protože jsou vnořené typy (adresa je třída a pohlaví je výčet). V situacích, kdy musí být vnořený typ použitý v rámci webové služby dostupný na straně klienta, lze použít atribut GenerateScriptType uvedený výše (viz výpis 10). Tento atribut lze přidat několikrát v případech, kdy je ze služby vrácena jiná vnořená komplexní typ. Dá se použít přímo na třídu webové služby nebo nad konkrétní webové metody.

**Výpis 10. Pomocí atributu GenerateScriptService definujte vnořené typy, které by měly být k dispozici klientovi.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

Použitím `GenerateScriptType` atributu pro webovou službu budou automaticky zpřístupněny typy adresa a pohlaví pro použití kódem javascriptu ASP.NET AJAX na straně klienta. Příkladem JavaScriptu, který se automaticky vygeneroval a pošle klientovi přidáním atributu GenerateScriptType ve webové službě, se zobrazí v seznamu 11. Později v článku se dozvíte, jak používat vnořené komplexní typy.

**Výpis 11. Vnořené komplexní typy zpřístupněné stránce ASP.NET AJAX.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

Teď, když jste viděli, jak vytvořit webové služby a zpřístupnit je pro ASP.NET stránky AJAX, si se podíváme na to, jak vytvořit a používat JavaScriptové proxy, aby se data mohla načíst nebo odeslat webovým službám.

## <a name="creating-javascript-proxies"></a>Vytváření proxy serverů JavaScript

Volání standardní webové služby (.NET nebo jiné platformy) obvykle zahrnuje vytvoření proxy objektu, který vás chrání před složitou složitostí odesílání požadavků SOAP a zpráv odpovědí. Pomocí volání webové služby ASP.NET AJAX lze vytvořit a použít proxy servery JavaScriptu pro snadné volání služeb bez obav o serializaci a deserializaci zpráv JSON. Proxy servery JavaScriptu lze automaticky generovat pomocí ovládacího prvku ASP.NET AJAX ScriptManager.

Vytvoření proxy serveru JavaScriptu, který může volat webové služby, se docílí pomocí vlastnosti služeb ovládacího prvku ScriptManager. Tato vlastnost umožňuje definovat jednu nebo více služeb, které může stránka ASP.NET AJAX volat asynchronně, aby odesílala nebo přijímala data, aniž by bylo nutné provádět operace zpětného odeslání. Službu definujete pomocí `ServiceReference` ovládacího prvku ASP.NET AJAX a přiřazujete adresu URL webové služby vlastnosti ovládacího prvku `Path` . Výpis 12 ukazuje příklad odkazování na službu s názvem CustomersService. asmx.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**Výpis 12. Definování webové služby použité na stránce ASP.NET AJAX.**

Přidání odkazu na CustomersService. asmx prostřednictvím ovládacího prvku ScriptManager způsobí, že se proxy server JavaScriptu dynamicky vygeneruje a odkazuje na stránku. Proxy je vložený pomocí &lt; &gt; značky Script a dynamicky načtený voláním souboru CustomersService. asmx a připojením/js na konec. Následující příklad ukazuje, jak je JavaScriptový proxy server vložený na stránce, když je ladění v web.config zakázané:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]Pokud chcete vidět skutečný javascriptový kód, který je vygenerován, můžete zadat adresu URL požadované webové služby .NET do pole Adresa v aplikaci Internet Explorer a připojit/js k konci.*

Pokud je ladění povoleno v web.config ladicí verze JavaScriptového proxy serveru bude vložena na stránku, jak je uvedeno dále:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

JavaScriptový proxy vytvořený pomocí ovládacího prvku ScriptManager může být také vložen přímo na stránku namísto odkazování pomocí &lt; &gt; atributu SRC značky skriptu. To lze provést nastavením vlastnosti InlineScript ovládacího prvku ServiceReference na hodnotu true (výchozí hodnota je false). To může být užitečné, když se proxy server nesdílí mezi několika stránkami a pokud chcete snížit počet síťových volání provedených na serveru. Pokud je InlineScript nastavené na hodnotu true, nebude prohlížeč ukládat do mezipaměti skript, takže výchozí hodnota false se doporučuje v případech, kdy se proxy používá na více stránkách aplikace ASP.NET AJAX. Příklad použití vlastnosti InlineScript se zobrazí jako další:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>Používání proxy serverů JavaScript

Jakmile je webová služba odkazována stránkou ASP.NET AJAX pomocí ovládacího prvku ScriptManager, je možné provést volání webové služby a vrácená data lze zpracovat pomocí funkcí zpětného volání. Webová služba je volána odkazem na svůj obor názvů (pokud existuje), názvem třídy a názvem webové metody. Všechny parametry předané webové službě lze definovat společně s funkcí zpětného volání, která zpracovává vrácená data.

Příklad použití proxy serveru JavaScriptu k volání webové metody s názvem GetCustomersByCountry () je uveden v seznamu 13. Funkce GetCustomersByCountry () se volá, když koncový uživatel klikne na tlačítko na stránce.

**Výpis 13. Volání webové služby s JavaScriptovým proxy serverem.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

Toto volání odkazuje na obor názvů InterfaceTraining, webovou metodu CustomersService třídy a GetCustomersByCountry, která je definována ve službě. Předá hodnotu země získanou z textového pole a také funkce zpětného volání s názvem OnWSRequestComplete, které by měly být vyvolány při vrácení volání asynchronní webové služby. OnWSRequestComplete zpracovává pole zákaznických objektů vrácených službou a převede je na tabulku, která se zobrazí na stránce. Výstup vygenerovaný z volání je znázorněn na obrázku 1.

[![Vázání dat získaných vytvořením asynchronního volání AJAX webové službě.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**Obrázek 1**: vazba dat získaná vytvořením asynchronního volání AJAX do webové služby.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-web-services/_static/image3.png))

Proxy servery JavaScript mohou také volat jednosměrná volání webových služeb v případech, kdy by měla být volána Webová metoda, ale proxy server by neměl čekat na odpověď. Například můžete chtít zavolat webovou službu, která spustí proces, jako je například pracovní tok, ale nečeká na návratovou hodnotu ze služby. V případech, kdy je třeba provést jednosměrné volání ke službě, může být funkce zpětného volání zobrazená v seznamu 13 jednoduše vynechána. Vzhledem k tomu, že není definována žádná funkce zpětného volání, nebude objekt proxy čekat, než webová služba vrátí data.

## <a name="handling-errors"></a>Zpracování chyb

Asynchronní zpětné volání webové služby může narazit na různé typy chyb, jako je síť, která je mimo provoz, Webová služba není k dispozici nebo se vrátí výjimka. Naštěstí proxy objekty JavaScriptu generované nástrojem ScriptManager umožňují definovat více zpětných volání, aby bylo možné zpracovávat chyby a chyby kromě zpětného volání, které se zobrazilo dříve. Funkce zpětného volání chyby může být definována hned po standardní funkci zpětného volání ve volání webové metody, jak je znázorněno v seznamu 14.

**Výpis 14. Definování funkce zpětného volání chyb a zobrazování chyb.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

Všechny chyby, ke kterým dojde při volání webové služby, spustí funkci zpětného volání OnWSRequestFailed (), která přijímá objekt představující chybu jako parametr. Objekt Error zpřístupňuje několik různých funkcí, které určují příčinu chyby, a také to, jestli vypršel časový limit volání. Výpis 14 ukazuje příklad použití různých chybových funkcí a obrázek 2 ukazuje příklad výstupu generovaného funkcemi.

[![Výstup generovaný při volání funkcí ASP.NET AJAX.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**Obrázek 2**: výstup generovaný při volání funkcí ASP.NET AJAX  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-web-services/_static/image6.png))

## <a name="handling-xml-data-returned-from-a-web-service"></a>Zpracování dat XML vrácených z webové služby

Dříve jste viděli, jak může webová metoda vracet nezpracovaná data XML pomocí atributu ScriptMethod spolu s vlastností ResponseFormat. Pokud je ResponseFormat nastaveno na ResponseFormat.Xml, data vrácená z webové služby jsou serializována jako XML místo JSON. To může být užitečné, pokud data XML musí být předána přímo klientovi ke zpracování pomocí JavaScriptu nebo XSLT. V současné době Internet Explorer 5 nebo vyšší poskytuje nejlepší objektový model na straně klienta pro analýzu a filtrování dat XML z důvodu integrované podpory MSXML.

Načítání dat XML z webové služby se neliší od načtení jiných datových typů. Začněte vyvoláním proxy JavaScriptu pro volání příslušné funkce a definování funkce zpětného volání. Jakmile volání vrátí, můžete zpracovat data ve funkci zpětného volání.

Výpis 15 ukazuje příklad volání webové metody s názvem GetRssFeed (), která vrací objekt XmlElement. GetRssFeed () přijímá jeden parametr představující adresu URL informačního kanálu RSS, který se má načíst.

**Výpis 15. Práce s daty XML vrácenými z webové služby.**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

Tento příklad předá adresu URL informačního kanálu RSS a zpracovává vrácená data XML ve funkci OnWSRequestComplete (). OnWSRequestComplete () nejprve zkontroluje, zda je prohlížeč Internet Explorer, aby bylo možné zjistit, zda je analyzátor MSXML k dispozici. Pokud je, použije se k vyhledání všech &lt; &gt; značek položek v informačním kanálu RSS příkaz XPath. Každá položka se pak prochází pomocí a &lt; &gt; &lt; &gt; jsou umístěné a zpracovávané přidružené značky title a Link pro zobrazení dat jednotlivých položek. Obrázek 3 ukazuje příklad výstupu generovaného z ASP.NET volání AJAX prostřednictvím proxy JavaScriptu na webovou metodu GetRssFeed ().

## <a name="handling-complex-types"></a>Zpracování komplexních typů

Komplexní typy přijaté nebo vrácené webovou službou se automaticky zveřejňují prostřednictvím proxy JavaScriptu. Vnořené komplexní typy však nejsou přímo přístupné na straně klienta, pokud atribut GenerateScriptType se na službu nepoužívá, jak je popsáno výše. Proč byste chtěli použít vnořený komplexní typ na straně klienta?

Pro zodpovězení této otázky Předpokládejme, že stránka ASP.NET AJAX zobrazuje zákaznická data a umožňuje koncovým uživatelům aktualizovat adresu zákazníka. Pokud webová služba Určuje, že typ adresy (komplexní typ definovaný v rámci třídy CustomerDetails) může být odeslán klientovi, pak může být proces aktualizace rozdělen na samostatné funkce pro lepší opakované použití kódu.

[![Výstup vytvoření z volání webové služby, která vrací data RSS.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**Obrázek 3**: vytváření výstupu z volání webové služby, která vrací data RSS.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-web-services/_static/image9.png))

Výpis 16 ukazuje příklad kódu na straně klienta, který vyvolá objekt adresy definovaný v oboru názvů modelu, vyplní aktualizované údaje a přiřadí je vlastnosti Adresa objektu CustomerDetails. Objekt CustomerDetails se pak předává webové službě ke zpracování.

**Výpis 16. Použití vnořených komplexních typů**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>Vytváření a používání metod stránky

Webové služby poskytují skvělý způsob, jak vystavit opakované služby pro celou řadu klientů, včetně stránek ASP.NET AJAX. Mohou však nastat případy, kdy stránka potřebuje načíst data, která nikdy nebudou použita nebo sdílena jinými stránkami. V takovém případě může být soubor. asmx, který umožňuje stránku přístup k datům, vypadat jako přehnaně důkladné, protože služba je používána pouze jednou stránkou.

ASP.NET AJAX poskytuje další mechanismus pro volání na základě webové služby bez vytváření samostatných souborů. asmx. To se provádí pomocí techniky, která je označována jako "metody stránky". Metody stránky jsou statické metody (sdílené v VB.NET) vložené přímo do stránky nebo souboru s kódem vedle kódu, který má atribut WebMethod použit pro ně. Použitím atributu WebMethod lze volat pomocí speciálního objektu jazyka JavaScript s názvem PageMethods, který se dynamicky vytvoří za běhu. Objekt PageMethods funguje jako proxy, který vás chrání před procesem serializace/deserializace JSON. Všimněte si, že aby bylo možné použít objekt PageMethods, musíte nastavit vlastnost EnablePageMethods ovládacího prvku ScriptManager na hodnotu true.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

Výpis 17 ukazuje příklad definování dvou metod stránky ve třídě ASP.NET (vedle kódu). Tyto metody načítají data z třídy obchodní vrstvy, která se nachází ve \_ složce s kódem aplikace na webu.

**Výpis 17. Definování metod stránky.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

Když ScriptManager zjistí přítomnost webových metod na stránce, vygeneruje dynamický odkaz na objekt PageMethods zmíněný výše. Volání webové metody je provedeno odkazem na třídu PageMethods následovanou názvem metody a všemi potřebnými daty parametrů, které by měly být předány. Výpis 18 ukazuje příklady volání dvou výše uvedených metod stránky.

**Výpis 18. Volání metod stránky s objektem JavaScript PageMethods**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

Použití objektu PageMethods je velmi podobné použití JavaScriptového objektu JavaScript. Nejprve zadáte všechna data parametrů, která by měla být předána metodě stránky a poté definovat funkci zpětného volání, která by měla být volána, když se vrátí asynchronní volání. Lze také zadat zpětné volání při selhání (pro příklad selhání zpracování se podívejte na výpis 14).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender a ASP.NET Toolkit AJAX

ASP.NET AJAX Toolkit (dostupný z [http://ajax.asp.net](http://ajax.asp.net) ) nabízí několik ovládacích prvků, které lze použít pro přístup k webovým službám. Konkrétně sada nástrojů obsahuje užitečný ovládací prvek s názvem `AutoCompleteExtender` , který lze použít k volání webových služeb a zobrazení dat na stránkách bez nutnosti psaní jakéhokoli kódu JavaScriptu.

Ovládací prvek AutoCompleteExtender se dá použít k rozšiřování existujících funkcí textového pole a snadnějšímu vyhledávání dat, která hledají uživatelé. Při zadávání do textového pole lze ovládací prvek použít k dotazování webové služby a k dynamickému zobrazení výsledků pod textovým polem. Obrázek 4 ukazuje příklad použití ovládacího prvku AutoCompleteExtender k zobrazení ID zákazníků pro aplikaci podpory. Vzhledem k tomu, že uživatel zadá různé znaky do textového pole, budou na základě jeho vstupu zobrazeny různé položky. Uživatelé pak mohou vybrat požadované ID zákazníka.

Použití AutoCompleteExtender v rámci stránky ASP.NET AJAX vyžaduje, aby bylo sestavení AjaxControlToolkit.dll přidáno do složky Bin webu. Po přidání sestavení sady Toolkit je vhodné na něj odkazovat v web.config tak, aby ovládací prvky, které obsahuje, byly k dispozici pro všechny stránky v aplikaci. To lze provést přidáním následující značky v rámci &lt; značky ovládacích prvků web.config &gt; :

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

V případech, kdy je třeba použít pouze ovládací prvek na konkrétní stránce, můžete na něj odkazovat přidáním direktivy Reference do horní části stránky, jak je uvedeno dále, nikoli aktualizací web.config:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![Použití ovládacího prvku AutoCompleteExtender](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**Obrázek 4**: použití ovládacího prvku AutoCompleteExtender  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-web-services/_static/image12.png))

Po nakonfigurování webu pro použití nástroje ASP.NET AJAX Toolkit lze přidat ovládací prvek AutoCompleteExtender do stránky podobně jako byste přidali běžný ovládací prvek ASP.NET serveru. Výpis 19 ukazuje příklad použití ovládacího prvku pro volání webové služby.

**Výpis 19. Pomocí ovládacího prvku ASP.NET AJAX Toolkit AutoCompleteExtender.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender má několik různých vlastností, včetně standardního ID a vlastností runat nalezených na serverových ovládacích prvcích. Kromě toho vám umožňuje definovat, kolik znaků typ koncového uživatele před dotazováním webové služby na data. Vlastnost MinimumPrefixLength uvedená v seznamu 19 způsobí, že se služba zavolá pokaždé, když se do textového pole zadá znak. Tuto hodnotu budete muset pečlivě nastavit, protože pokaždé, když uživatel zadá znak, který bude volat webová služba, vyhledá hodnoty, které odpovídají znakům v textovém poli. Webová služba, která se má volat, stejně jako cílová webová metoda je definována pomocí vlastností ServicePath a ServiceMethod v uvedeném pořadí. Nakonec vlastnost vlastnost TargetControlID prvku určuje, které textové pole má připojovat ovládací prvek AutoCompleteExtender.

Volaná webová služba musí mít atribut ScriptService použit jak je popsáno výše a cílová webová metoda musí přijmout dva parametry s názvem prefixText a Count. Parametr prefixText představuje znaky zadané koncovým uživatelem a parametr Count představuje počet položek, které se mají vrátit (výchozí hodnota je 10). Výpis 20 ukazuje příklad webové metody getkódzákazníkas volané ovládacím prvkem AutoCompleteExtender, který je uveden výše v seznamu 19. Metoda web volá metodu obchodní vrstvy, která zase volá metodu datové vrstvy, která zpracovává filtrování dat a vrací odpovídající výsledky. Kód pro metodu datové vrstvy je zobrazen v seznamu 21.

**Výpis 20. Filtrování dat odeslaných z ovládacího prvku AutoCompleteExtender.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**Výpis 21. Filtrování výsledků na základě vstupu koncového uživatele.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>Závěr

ASP.NET AJAX poskytuje skvělou podporu pro volání webových služeb, aniž by bylo potřeba psát spoustu vlastních kódů JavaScriptu pro zpracování žádostí a zpráv odpovědí. V tomto článku jste se naučili, jak AJAX povolit webové služby .NET, aby mohly zpracovávat zprávy JSON a jak definovat proxy JavaScripty pomocí ovládacího prvku ScriptManager. Viděli jste také, jak můžou být proxy servery jazyka JavaScript použity pro volání webových služeb, zpracování jednoduchých a složitých typů a řešení chyb. Nakonec jste viděli, jak lze metody stránky použít ke zjednodušení procesu vytváření a provádění volání webové služby a způsobu, jakým může ovládací prvek AutoCompleteExtender poskytnout uživatelům při psaní lepší informace pro koncové uživatele. I když je ovládací prvek UpdatePanel dostupný v ASP.NET AJAX v důsledku jednoduchosti kontrolou volby pro mnoho programátorů AJAX, je důležité vědět, jak volat webové služby prostřednictvím proxy serverů JavaScriptu může být užitečné v mnoha aplikacích.

## <a name="bio"></a>Životopis

Dan Wahlin (Microsoft nejvíc Professional for ASP.NET and XML Web Services) je instruktor pro vývoj a architekturu pro vývoj rozhraní .NET na úrovni technického školení ( [http://www.interfacett.com](http://www.interfacett.com) ). Daň ze sady XML for ASP.NET Developers web ([www.XMLforASP.NET](http://www.XMLforASP.NET)) se nachází v kanceláři mluvčího v INETA a mluví na několika konferencích. Specialista na spolupracovníka Windows DNA (Wrox), ASP.NET: tipy, kurzy a Code (Sams), ASP.NET 1,1 řešení Insider, Professional ASP.NET 2,0 AJAX (Wrox), ASP.NET 2,0 MVP Hackatony a vytvořil XML pro vývojáře ASP.NET (Sams). Když není psaní kódu, článků nebo knih, Dan, požívá psaní a zaznamenávání hudby a hraní Golfů a basketbalový s jeho manželkou a dětem.

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) blogu nebo jeho blogu na adrese [ScottCate.com](http://ScottCate.com) .

> [!div class="step-by-step"]
> [Předchozí](understanding-asp-net-ajax-localization.md) 
>  [Další](understanding-asp-net-ajax-debugging-capabilities.md)
