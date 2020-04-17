---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Použití řadičů a zobrazení k implementaci hlavního použití a podrobného uznaného použití | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 4 ukazuje, jak přidat řadič do aplikace, která využívá náš model poskytnout uživatelům výpis dat / podrobnosti navigace zkušenosti ...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541309"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Použití kontrolerů a zobrazení k implementaci uživatelského rozhraní seznamu a podrobností

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 4 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 4 ukazuje, jak přidat řadič do aplikace, která využívá náš model poskytnout uživatelům výpis dat nebo podrobnosti navigační prostředí pro večeře na našem webu NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner Krok 4: Řadiče a zobrazení

S tradičními webovými rámci (klasické ASP, PHP, ASP.NET webové formuláře atd.) jsou příchozí adresy URL obvykle mapovány na soubory na disku. Například: žádost o adresu URL jako "/Products.aspx" nebo "/Products.php" může být zpracována souborem "Products.aspx" nebo "Products.php".

Webové architektury MVC mapují adresy URL na kód serveru mírně odlišným způsobem. Místo mapování příchozích adres URL na soubory místo toho mapují adresy URL na metody ve třídách. Tyto třídy se nazývají "Řadiče" a jsou zodpovědné za zpracování příchozích požadavků HTTP, zpracování vstupu uživatele, načítání a ukládání dat a určení odpovědi k odeslání zpět klientovi (zobrazení HTML, stažení souboru, přesměrování na jinou adresu URL atd.).

Nyní, když jsme vytvořili základní model pro naši aplikaci NerdDinner, bude naším dalším krokem přidání řadiče do aplikace, která využívá k tomu, aby uživatelům poskytla možnost navigace v seznamu dat / podrobnostech pro večeře na našich stránkách.

### <a name="adding-a-dinnerscontroller-controller"></a>Přidání řadiče DinnersController

Začneme kliknutím pravým tlačítkem myši na složku "Řadiče" v rámci našeho webového projektu a poté vybereme příkaz nabídky **&gt;Přidat řadič** (tento příkaz můžete také provést zadáním Ctrl-M, Ctrl-C):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Tím se zobrazí dialogové okno "Přidat řadič":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

Pojmenujeme nový řadič "DinnersController" a klikneme na tlačítko "Přidat". Visual Studio pak přidá DinnersController.cs soubor do našeho adresáře \Controllers:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Také otevře nové DinnersController třídy v rámci editoru kódu.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Přidání metod akce Index() a Details() do třídy DinnersController

Chceme umožnit návštěvníkům, kteří používají naši aplikaci, aby si prohlédli seznam nadcházejících večeří a umožnili jim kliknout na libovolnou večeři v seznamu a zobrazit konkrétní podrobnosti o něm. Uděláme to tak, že z naší aplikace zveřejníme následující adresy URL:

| **Adresa URL** | **Účel** |
| --- | --- |
| */Večeře/* | Zobrazení html seznamu nadcházejících večeří |
| */Večeře/Podrobnosti/[id]* | Zobrazit podrobnosti o konkrétní večeři označené "id" parametr vložený do adresy URL – který bude odpovídat DinnerID večeře v databázi. Například: /Dinners/Details/2 zobrazí stránku HTML s podrobnostmi o večeři, jejíž hodnota DinnerID je 2. |

Budeme publikovat počáteční implementace těchto adres URL přidáním dvou veřejných "akčních metod" do naší třídy DinnersController, jako je níže:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Poté spustíme aplikaci NerdDinner a použijeme náš prohlížeč k jejich vyvolání. Zadáním adresy URL *"/Dinners/"* způsobíte spuštění metody *Index()* a odešle te zpět následující odpověď:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

Zadáním adresy URL *"/Dinners/Details/2"* se spustí naše metoda *Details()* a odešlete zpět následující odpověď:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

Možná se divíte - jak ASP.NET MVC vědět vytvořit naši třídu DinnersController a vyvolat tyto metody? Chcete-li pochopit, že pojďme se rychle podívat na to, jak směrování funguje.

### <a name="understanding-aspnet-mvc-routing"></a>Principy směrování MVC ASP.NET

ASP.NET MVC obsahuje výkonný modul směrování adres URL, který poskytuje velkou flexibilitu při řízení, jak jsou adresy URL mapovány na třídy řadiče. To nám umožňuje zcela přizpůsobit, jak ASP.NET MVC vybere, které třídy řadiče vytvořit, která metoda vyvolat na to, stejně jako konfigurovat různé způsoby, které proměnné mohou být automaticky analyzovány z URL / Querystring a předány metodě jako parametr argumenty. Poskytuje flexibilitu zcela optimalizovat stránky pro SEO (optimalizace pro vyhledávače), stejně jako publikovat všechny URL struktury chceme od aplikace.

Ve výchozím nastavení jsou nové ASP.NET projekty MVC dodávány s předkonfigurovanou sadou již registrovaných pravidel směrování adres URL. To nám umožňuje snadno začít s aplikací, aniž bybylo nutné explicitně konfigurovat cokoli. Výchozí registrace pravidel směrování lze nalézt v rámci třídy "Aplikace" našich projektů - které můžeme otevřít poklepáním na soubor "Global.asax" v kořenovém adresáři našeho projektu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

Výchozí ASP.NET pravidla směrování MVC jsou registrovány v rámci metody "RegisterRoutes" této třídy:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"Trasy. MapRoute()" volání metody výše registruje výchozí pravidlo směrování, které mapuje příchozí adresy URL na třídy řadiče pomocí formátu URL: "/{controller}/{action}/{id}" – kde "controller" je název třídy řadiče k vytvoření instance, "akce" je název veřejné metody, kterou chcete vyvolat, a "id" je volitelný parametr vložený do adresy URL, který lze předat jako argument metodě. Třetí parametr předaný volání metody "MapRoute()" je sada výchozích hodnot, které se mají použít pro hodnoty kontroleru/akce/id v případě, že nejsou v adrese URL (Controller = "Home", Action="Index", Id="").

Níže je tabulka, která ukazuje, jak jsou mapovány různé adresy URL pomocí výchozího pravidla postupu<em>"/{controllers}/{action}/{id}":</em>

| **Adresa URL** | **Třída řadiče** | **Metoda akce** | **Předané parametry** |
| --- | --- | --- | --- |
| */Večeře/Podrobnosti/2* | DinnersController | Podrobnosti (id) | id=2 |
| */Večeře/Úpravy/5* | DinnersController | Upravit(id) | id=5 |
| */Večeře/Vytvořit* | DinnersController | Vytvořit() | – |
| */Večeře* | DinnersController | Index() | – |
| */Domů* | Domácí kontrolka | Index() | – |
| */* | Domácí kontrolka | Index() | – |

Poslední tři řádky zobrazují výchozí hodnoty (Controller = Home, Action = Index, Id = "") používané. Vzhledem k tomu, že metoda "Index" je registrována jako výchozí název akce, pokud není zadán, adresy URL "/Dinners" a "/Home" způsobí, že metoda akce Index() bude vyvolána ve třídách kontroleru. Vzhledem k tomu, že "Home" řadič je registrován jako výchozí řadič, pokud není zadán, "/" URL způsobí HomeController, které mají být vytvořeny a Index() metoda akce na něm být vyvolána.

Pokud se vám nelíbí tyto výchozí url směrování pravidla, dobrou zprávou je, že jsou snadno změnit - stačí upravit v rámci RegisterRoutes metoda výše. Pro naši aplikaci NerdDinner však nezměníme žádné výchozí pravidla směrování adres URL - místo toho je použijeme tak, jak jsou.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Použití DinnerRepository z našeho DinnersController

Nyní nahradíme naši aktuální implementaci metod akce Index() a Details() dinnersController implementacemi, které používají náš model.

Použijeme DinnerRepository třídy jsme vytvořili dříve implementovat chování. Začneme přidáním příkazu "using", který odkazuje na obor názvů "NerdDinner.Models" a pak deklarujeme instanci našeho DinnerRepository jako pole v naší třídě DinnerController.

Dále v této kapitole představíme koncept "vkládání závislostí" a zobrazíme další způsob, jak naši správci získat odkaz na DinnerRepository, který umožňuje lepší testování částí – ale právě teď budeme jen vytvořit instanci našedinnerRepository inline jako níže.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Nyní jsme připraveni generovat odpověď HTML zpět pomocí našich objektů načteného datového modelu.

### <a name="using-views-with-our-controller"></a>Použití zobrazení s naším ovladačem

I když je možné napsat kód v rámci našich akčních metod sestavit HTML a pak použít *Response.Write()* pomocné metody k odeslání zpět klientovi, tento přístup se stává poměrně těžkopádný rychle. Mnohem lepší přístup je pro nás provádět pouze aplikační a datovou logiku uvnitř našich metod akce DinnersController a pak předat data potřebná k vykreslení odpovědi HTML na samostatnou šablonu "view", která je zodpovědná za odchozí reprezentaci HTML. Jak uvidíme za chvíli, šablona "view" je textový soubor, který obvykle obsahuje kombinaci značek HTML a vloženého vykreslovacího kódu.

Oddělení logiky řadiče od našeho zobrazení vykreslování přináší několik velkých výhod. Zejména pomáhá vynutit jasné "oddělení obav" mezi kódaplikace a ui formátování / vykreslovací kód. To usnadňuje logiku aplikace testování částí v izolaci od logiky vykreslování ui. Usnadňuje pozdější úpravy šablon vykreslování uživatelského počítače bez nutnosti provádět změny kódu aplikace. A to může usnadnit vývojářům a návrhářům spolupracovat na projektech.

Můžeme aktualizovat naše DinnersController třídy označující, že chceme použít šablonu zobrazení odeslat zpět odpověď uživatelského jazyka HTML změnou podpisy metody našich dvou metod akce z mít návratový typ "void" místo toho mít návratový typ "ActionResult". Potom můžeme volat *View()* pomocné metody na controller základní třídy vrátit zpět "ViewResult" objekt, jako je níže:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

Podpis *View()* pomocné metody, kterou používáme výše vypadá níže:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

První parametr pomocné metody *View()* je název souboru šablony zobrazení, který chceme použít k vykreslení odpovědi HTML. Druhý parametr je objekt modelu, který obsahuje data, která šablona zobrazení potřebuje k vykreslení odpovědi HTML.

V rámci naší Metody akce Index() voláme *metodu View()* pomocné a označujeme, že chceme vykreslit seznam HTML večeří pomocí šablony zobrazení "Index". Předáváme šablonu zobrazení posloupnost objektů Dinner, ze které chcete vygenerovat seznam z:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

V rámci naší Metody akce Details() se pokusíme načíst objekt Dinner pomocí id uvedeného v adrese URL. Pokud je nalezen platný Dinner voláme *View()* pomocná metoda, označující, že chceme použít "Podrobnosti" zobrazit šablonu k vykreslení načtený Objekt. Pokud je požadována neplatná večeře, vykreslíme užitečnou chybovou zprávu, která označuje, že večeře neexistuje pomocí šablony zobrazení "NotFound" (a přetížené verze metodu *View(),* která pouze přebírá název šablony):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Nyní implementujeme šablony zobrazení "NotFound", "Details" a "Index".

### <a name="implementing-the-notfound-view-template"></a>Implementace šablony zobrazení "Nenalezeno"

Začneme implementací šablony zobrazení "NotFound" – která zobrazuje popisnou chybovou zprávu, že požadovanou večeři nelze najít.

Vytvoříme novou šablonu zobrazení umístěním našeho textového kurzoru v rámci metody akce kontroleru a pak klikněte pravým tlačítkem myši a zvolte příkaz nabídky "Přidat zobrazení" (tento příkaz můžeme také spustit zadáním Ctrl-M, Ctrl-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Tím se zobrazí dialogové okno "Přidat zobrazení" jako níže. Ve výchozím nastavení dialogové okno předem vyplní název zobrazení, které má být vyhotoveno názvu metody akce, ve které byl kurzor při spuštění dialogového okna (v tomto případě "Podrobnosti"). Protože chceme nejprve implementovat šablonu "NotFound", přepíšeme tento název zobrazení a nastavíme ji tak, aby byla "Nenalezeno":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

Když klikneme na tlačítko "Přidat", Visual Studio pro nás vytvoří novou šablonu zobrazení NotFound.aspx v adresáři \Views\Dinners (který také vytvoří, pokud adresář ještě neexistuje):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Také otevře naši novou šablonu zobrazení "NotFound.aspx" v editoru kódu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

Zobrazit šablony ve výchozím nastavení mají dvě "oblasti obsahu", kde můžeme přidat obsah a kód. První nám umožňuje přizpůsobit "název" stránky HTML odeslané zpět. Druhý nám umožňuje přizpůsobit "hlavní obsah" stránky HTML odeslané zpět.

Chcete-li implementovat naši šablonu zobrazení "NotFound", přidáme základní obsah:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Můžeme to pak vyzkoušet v prohlížeči. Chcete-li to provést, vyžádejte adresu URL *"/Dinners/Details/9999".* To bude odkazovat na večeři, která v současné době neexistuje v databázi a způsobí, že naše DinnersController.Details() metoda akce k vykreslení naší šablony zobrazení "NotFound":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Jedna věc, kterou si všimnete na obrazovce-shot výše je, že naše základní zobrazení šablony zdědil spoustu HTML, který obklopuje hlavní obsah na obrazovce. Je to proto, že naše šablona zobrazení používá šablonu "vzorové stránky", která nám umožňuje použít konzistentní rozložení ve všech zobrazeních na webu. Budeme diskutovat o tom, jak stránky předlohy fungují více v pozdější části tohoto kurzu.

### <a name="implementing-the-details-view-template"></a>Implementace šablony zobrazení Podrobnosti

Nyní implementujeme šablonu zobrazení "Podrobnosti" – která bude generovat HTML pro jeden model večeři.

Uděláme to tak, že umístíme kurzor textu do metody akce Podrobnosti a pak klikněte pravým tlačítkem myši a zvolte příkaz nabídky "Přidat zobrazení" (nebo stiskněte kombinaci kláves Ctrl-M, Ctrl-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Tím se zobrazí dialogové okno "Přidat zobrazení". Zachováme výchozí název zobrazení ("Podrobnosti"). V dialogovém okně také vybereme políčko Vytvořit zobrazení silného typu a vyberte (pomocí rozevíracího okna se seznamem) název typu modelu, který předáváme z řadiče do zobrazení. Pro toto zobrazení jsme předávání Dinner objektu (plně kvalifikovaný název pro tento typ je: "NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

Na rozdíl od předchozí šablony, kde jsme se rozhodli vytvořit "Prázdné zobrazení", tentokrát se rozhodneme automaticky "scaffold" zobrazení pomocí šablony "Podrobnosti". Můžeme to označit změnou rozevíracího okna "Zobrazit obsah" ve výše uvedeném dialogu.

"Lešení" vygeneruje počáteční implementaci naší šablony zobrazení podrobností na základě objektu Dinner, který mu předáváme. To nám poskytuje snadný způsob, jak rychle začít s implementací šablony zobrazení.

Po kliknutí na tlačítko "Přidat" visual studio vytvoří nový soubor šablony zobrazení "Details.aspx" pro nás v našem adresáři "\Views\Dinners":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Také otevře naši novou šablonu zobrazení "Details.aspx" v editoru kódu. Bude obsahovat počáteční implementaci uživatelského a uživatelského prohlášení zobrazení podrobností na základě modelu Dinner. Modul lešení používá .NET reflexe podívat na veřejné vlastnosti vystavené na třídu předána a přidá příslušný obsah na základě každého typu najde:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

Můžeme požádat o adresu URL *"/Dinners/Details/1",* abychom zjistili, jak tato implementace "details" lešení vypadá v prohlížeči. Pomocí této adresy URL se zobrazí jedna z večeří, které jsme ručně přidali do naší databáze při prvním vytvoření:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

To nás rychle zprovozní a poskytne nám počáteční implementaci našeho zobrazení Details.aspx. Pak můžeme jít a vyladit ji přizpůsobit ui k naší spokojenosti.

Když se podíváme na šablonu Details.aspx podrobněji, zjistíme, že obsahuje statický kód HTML i vložený kód vykreslování. &lt;%&gt; kódnugety spustit kód při zobrazení šablony &lt;vykreslí a %=&gt; kód nuggets spustit kód obsažený v nich a pak vykreslit výsledek výstupní hod šablony.

Můžeme napsat kód v rámci našeho zobrazení, který přistupuje k objektu modelu "Dinner", který byl předán z našeho řadiče pomocí vlastnosti "Model" silného typu. Visual Studio nám poskytuje úplný kód-intellisense při přístupu k této vlastnosti "Model" v editoru:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Udělejme nějaké vylepšení tak, aby zdroj pro naši konečnou šablonu zobrazení Podrobnosti vypadal níže:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

Když jsme se přístup *"/ Večeře / Podrobnosti / 1"* URL znovu to bude nyní vykreslovat jako níže:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>Implementace šablony zobrazení "Index"

Nyní implementujeme šablonu zobrazení "Index" – která vygeneruje seznam nadcházejících večeří. Chcete-li to provést, umístíme kurzor textu do metody akce Index a pak klikněte pravým tlačítkem myši a zvolte příkaz nabídky "Přidat zobrazení" (nebo stiskněte kombinaci kláves Ctrl-M, Ctrl-V).

V dialogovém okně "Přidat zobrazení" zachováme šablonu zobrazení s názvem "Index" a zaškrtneme políčko Vytvořit zobrazení silného typu. Tentokrát se rozhodneme automaticky generovat šablonu zobrazení "Seznam" a vybereme "NerdDinner.Models.Dinner" jako typ modelu předaný zobrazení (což, protože jsme uvedli, že vytváříme generování uživatelského okna "Seznam", způsobí, že dialogové okno Přidat zobrazení předpokládá, že předáváme posloupnost objektů Večeři z našeho řadiče do zobrazení):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

Po kliknutí na tlačítko "Přidat" visual studio vytvoří nový soubor šablony zobrazení "Index.aspx" pro nás v rámci našeho adresáře "\Views\Dinners". Bude "lešení" počáteční implementace v něm, který poskytuje html tabulka seznam dinners přejdeme do zobrazení.

Když spustíme aplikaci a přístup *k "/ Večeře /"* URL bude vykreslovat náš seznam večeří, jako je to:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

Tabulka řešení výše nám dává mřížky-jako rozložení našich dat večeře - což není úplně to, co chceme pro naše spotřebitele čelí večeři výpis. Můžeme aktualizovat šablonu zobrazení Index.aspx a upravit ji tak, &lt;aby&gt; vyňala méně sloupců dat, a použít prvek ul k jejich vykreslení namísto tabulky pomocí následujícího kódu:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Používáme klíčové slovo "var" v rámci výše uvedeného foreach prohlášení, jak jsme smyčky přes každou večeři v našem modelu. Ti, kteří nejsou obeznámeni s C# 3.0 může myslet, že pomocí "var" znamená, že objekt večeři je pozdě vázána. Místo toho znamená, že kompilátor používá odvození typu proti vlastnosti silně zadaný "Model"&lt;(která je typu "IEnumerable Dinner")&gt;a kompilaci místní proměnné "dinner" jako typu Dinner – což znamená, že získáme plnou intellisense a kompilaci v rámci bloků kódu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Když jsme hit refresh na */ Večeře* URL v našem prohlížeči naše aktualizované zobrazení nyní vypadá níže:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

To vypadá lépe - ale není úplně tam ještě. Naším posledním krokem je umožnit koncovým uživatelům kliknout na jednotlivé večeře v seznamu a zobrazit podrobnosti o nich. Budeme implementovat tím, že vykresluje prvky hypertextového odkazu HTML, které odkazují na podrobnosti akce metody na naše DinnersController.

Tyto hypertextové odkazy můžeme vygenerovat v rámci zobrazení indexu jedním ze dvou způsobů. Prvním z nich je &lt;ručně&gt; vytvořit HTML prvky, &lt;jako&gt; je &lt;níže, kde jsme vložit % % bloky v rámci elementu&gt; HTML:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Alternativní přístup, který můžeme použít, je využít vestavěnou pomocnou metodu "Html.ActionLink()" v rámci &lt;ASP.NET&gt; MVC, která podporuje programové vytváření html prvku, který odkazuje na jinou metodu akce na řadiči:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Prvním parametrem pomocné metody Html.ActionLink() je text odkazu, který se má zobrazit (v tomto případě název večeře), druhým parametrem je název akce Controller, na který chceme vygenerovat odkaz (v tomto případě metoda Details) a třetí parametr je sada parametrů, které mají být odeslány do akce (implementována jako anonymní typ s názvem/hodnotami vlastnosti). V tomto případě zadáváme parametr "id" večeře, na kterou chceme vytvořit odkaz, a protože výchozí pravidlo směrování adresy URL v ASP.NET MVC je "{Controller}/{Action}/{id}" metoda pomocné položky Html.ActionLink() vygeneruje následující výstup:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Pro naše zobrazení Index.aspx budeme používat Html.ActionLink() pomocné metody přístupu a mají každou večeři v seznamu odkaz na příslušné podrobnosti URL:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

A teď, když jsme narazili na */ Večeře* URL náš seznam večeří vypadá níže:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Když klikneme na některou z večeří v seznamu, přejdeme k podrobnostem o něm:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Pojmenování založené na konventu a adresářová struktura \Views

ASP.NET aplikace MVC ve výchozím nastavení používají při řešení šablon zobrazení strukturu pojmenování adresářů založenou na konvencích. To umožňuje vývojářům vyhnout se nutnosti plně kvalifikovat cestu umístění při odkazování na zobrazení z třídy Controller. Ve výchozím nastavení ASP.NET mvc bude hledat soubor\[šablony zobrazení\* v adresáři *\Views ControllerName] pod aplikací.

Například jsme pracovali na DinnersController třídy – který explicitně odkazuje na tři šablony zobrazení: "Index", "Podrobnosti" a "NotFound". ASP.NET mvc bude ve výchozím nastavení hledat tato zobrazení v adresáři *\Views\Dinners* pod kořenovým adresářem aplikace:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Všimněte si, jak jsou aktuálně tři třídy kontroleru v rámci projektu (DinnersController, HomeController a AccountController – poslední dva byly přidány ve výchozím nastavení při vytváření projektu) a existují tři podadresáře (jeden pro každý řadič) v rámci \Views adresáře.

Zobrazení odkazovaná z řadičů domů a účtů automaticky vyřeší jejich šablony zobrazení z příslušných *\Zobrazení\Domů* a *\Zobrazení\Adresáře účtů.* Podadresář *\Views\Shared* umožňuje ukládat šablony zobrazení, které jsou znovu použity ve více řadičích v rámci aplikace. Při ASP.NET mvc pokusí vyřešit šablonu zobrazení, bude nejprve zkontrolovat v *adresáři \Views\[Controller]* konkrétní, a pokud nemůže najít šablonu zobrazení tam bude vypadat v *\Views\Shared* adresáře.

Pokud jde o pojmenování jednotlivých šablon zobrazení, doporučujeme, aby šablona zobrazení sdílela stejný název jako metoda akce, která způsobila její vykreslení. Například nad naší metodou akce "Index" používá zobrazení "Index" k vykreslení výsledku zobrazení a metoda akce "Podrobnosti" používá zobrazení "Podrobnosti" k vykreslení výsledků. Díky tomu je snadné rychle zjistit, která šablona je přidružena ke každé akci.

Vývojáři nemusí explicitně zadat název šablony zobrazení, pokud má šablona zobrazení stejný název jako metoda akce vyvolaná na řadiči. Místo toho můžeme pouze předat objekt modelu metodě "View()" (bez zadání názvu zobrazení) a ASP.NET MVC automaticky odvodí, že chceme použít šablonu zobrazení *\Views\[ControllerName]\[ActionName]* na disku k jeho vykreslení.

To nám umožňuje trochu vyčistit kód ovladače a vyhnout se duplikaci názvu dvakrát v našem kódu:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

Výše uvedený kód je vše, co je potřeba k provedení pěkné večeře výpis / podrobnosti zkušenosti pro stránky.

#### <a name="next-step"></a>Další krok

Nyní máme pěkný zážitek z prohlížení večeře postavený.

Nyní povolte podporu úprav datového formuláře CRUD (Vytvořit, Číst, Aktualizovat, Odstranit).

> [!div class="step-by-step"]
> [Předchozí](build-a-model-with-business-rule-validations.md)
> [další](provide-crud-create-read-update-delete-data-form-entry-support.md)
