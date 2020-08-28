---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Zkoumání metod Edit a zobrazení pro úpravy | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045205"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Zkoumání metod Edit a zobrazení pro úpravy

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

V této části proberete vygenerované `Edit` metody a zobrazení akcí pro kontroler videí. Ale nejdřív potrváme krátkému odklonování, aby bylo datum vydání lépe podrobnější. Otevřete soubor *Models\Movie.cs* a přidejte zvýrazněné řádky zobrazené níže:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

Můžete také nastavit jazykovou verzi, která bude specifická jako tato:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

V dalším kurzu budeme pokrývat tato [Anotace](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) . Atribut [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) určuje, co se má zobrazit pro název pole (v tomto případě "Datum vydání" místo "ReleaseDate"). Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) určuje typ dat, v tomto případě je to datum, takže se nezobrazí informace o čase uložené v poli. Atribut [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) je potřeba pro chybu v prohlížeči Chrome, která vykresluje formáty data nesprávně.

Spusťte aplikaci a přejděte k `Movies` řadiči. Podržte ukazatel myši na odkaz pro **Úpravy** a zobrazte tak adresu URL, na kterou odkazuje.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Odkaz **Edit** byl vygenerován `Html.ActionLink` metodou v zobrazení *Views\Movies\Index.cshtml* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`Objekt je pomocník, který je vystaven pomocí vlastnosti základní třídy [System. Web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) . `ActionLink`Metoda pomocné rutiny usnadňuje dynamické generování hypertextových odkazů HTML, které odkazují na metody akcí na řadičích. Prvním argumentem `ActionLink` metody je text odkazu, který se má vykreslit (například `<a>Edit Me</a>` ). Druhý argument je název metody akce, která se má vyvolat (v tomto případě `Edit` Akce). Konečný argument je [anonymní objekt](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , který generuje data trasy (v tomto případě ID 4).

Vygenerovaný odkaz uvedený na předchozím obrázku je `http://localhost:1234/Movies/Edit/4` . Výchozí trasa (vytvořená v *App \_ Start\RouteConfig.cs*) přebírá vzor adresy URL `{controller}/{action}/{id}` . Proto ASP.NET převede `http://localhost:1234/Movies/Edit/4` požadavek na `Edit` metodu akce `Movies` kontroleru s parametrem, který se `ID` rovná 4. Projděte si následující kód ze souboru *App \_ Start\RouteConfig.cs* . Metoda [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) se používá ke směrování požadavků HTTP na správnou metodu kontroleru a akce a zadání volitelného parametru ID. Metoda [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) je také používána [HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) , například `ActionLink` k vygenerování adres URL za daný kontroler, akce a veškerá data trasy.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

Můžete také předat parametry metody akce pomocí řetězce dotazu. Například adresa URL `http://localhost:1234/Movies/Edit?ID=3` také předá parametr `ID` 3 `Edit` metodě Action `Movies` kontroleru.

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

Otevřete `Movies` kontroler. Následující dvě `Edit` metody akce jsou uvedeny níže.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

Všimněte si, že druhá `Edit` Metoda Action předchází `HttpPost` atribut. Tento atribut určuje, že přetížení `Edit` metody lze vyvolat pouze pro požadavky post. Můžete použít `HttpGet` atribut na první metodu Edit, ale to není nutné, protože je to výchozí. (Odkazujeme na metody akcí, které implicitně přiřazují `HttpGet` atribut jako `HttpGet` metody.) Atribut [BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) je dalším důležitým mechanismem zabezpečení, který brání v navýšení dat z více než po data do modelu. Do atributu BIND, který chcete změnit, byste měli zahrnout pouze vlastnosti. Můžete si přečíst informace o tom, jak přeposílat, tak i atribut BIND v [poznámce zabezpečení](https://go.microsoft.com/fwlink/?LinkId=317598). V jednoduchém modelu použitém v tomto kurzu budeme svázat všechna data v modelu. Atribut [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) se používá k tomu, aby se zabránilo padělání požadavku a bylo spárováno s `@Html.AntiForgeryToken()` v souboru pro úpravy (*Views\Movies\Edit.cshtml*), část je zobrazena níže:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` generuje skrytý formulář tokenu proti padělání, který se musí shodovat s `Edit` metodou `Movies` kontroleru. Další informace o padělání požadavků pro více lokalit (označované také jako XSRF nebo CSRF) najdete v tématu můj kurz [XSRF/CSRF prevence v MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).

`HttpGet` `Edit` Metoda přebírá parametr ID filmu, vyhledá film pomocí `Find` metody Entity Framework a vrátí vybraný film do zobrazení pro úpravy. Pokud se video nenajde, vrátí se [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) . Když systém generování uživatelského rozhraní vytvořil zobrazení pro úpravy, zkontroloval `Movie` třídu a vytvořil kód pro vykreslení `<label>` a `<input>` prvky pro každou vlastnost třídy. Následující příklad ukazuje zobrazení pro úpravy, které bylo vygenerováno systémem pro generování uživatelského rozhraní sady Visual Studio:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Všimněte si, jak šablona zobrazení obsahuje `@model MvcMovie.Models.Movie` příkaz v horní části souboru – určuje, že zobrazení očekává, že model pro šablonu zobrazení bude typu `Movie` .

Generovaný kód používá několik *pomocných metod* pro zjednodušení značek HTML. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Pomocník zobrazuje název pole ( &quot; title &quot; , &quot; ReleaseDate &quot; , &quot; Žánr &quot; nebo &quot; Price &quot; ). [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Pomoc vykreslí prvek HTML `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Pomocník zobrazuje všechny ověřovací zprávy přidružené k této vlastnosti.

Spusťte aplikaci a přejděte na adresu URL */Movies* . Klikněte na odkaz **Upravit** . V prohlížeči zobrazte zdroj stránky. KÓD HTML prvku formuláře je uveden níže.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>`Prvky jsou v elementu HTML, `<form>` jehož `action` atribut je nastaven na hodnotu post na adresu URL */Movies/Edit* . Data formuláře budou při kliknutí na tlačítko **Uložit** publikována na serveru. Druhý řádek ukazuje skrytý token [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) generovaný `@Html.AntiForgeryToken()` voláním.

## <a name="processing-the-post-request"></a>Zpracovává se žádost POST.

Následující výpis zobrazuje `HttpPost` verzi `Edit` metody Action.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Atribut [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) ověřuje token [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) generovaný `@Html.AntiForgeryToken()` voláním v zobrazení.

[Pořadač modelu ASP.NET MVC](https://msdn.microsoft.com/library/dd410405.aspx) přebírá hodnoty v zaúčtovaném formuláři a vytvoří `Movie` objekt, který se předává jako `movie` parametr. `ModelState.IsValid`Ověřuje, že data odeslaná ve formuláři lze použít k úpravě (úpravě nebo aktualizaci) `Movie` objektu. Pokud jsou data platná, data videa se uloží do `Movies` kolekce `db` ( `MovieDBContext` instance). Nová data videa se uloží do databáze voláním `SaveChanges` metody `MovieDBContext` . Po uložení dat kód přesměruje uživatele na `Index` metodu Action `MoviesController` třídy, která zobrazí kolekci filmů, včetně změn, které byly právě provedeny.

Jakmile ověřování na straně klienta určí, že hodnota pole není platná, zobrazí se chybová zpráva. Pokud je JavaScript zakázaný, ověřování na straně klienta je zakázané. Server ale zjistí, že odeslané hodnoty nejsou platné, a hodnoty formuláře se zobrazí znovu s chybovými zprávami.

Ověření se podrobněji prozkoumá v tomto kurzu.

U `Html.ValidationMessageFor` pomocníků v šabloně zobrazení *Edit. cshtml* se postará o zobrazení příslušných chybových zpráv.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

Všechny `HttpGet` metody následují podobně jako vzor. Získají filmový objekt (nebo seznam objektů, v případě `Index` ) a předávají model do zobrazení. `Create`Metoda předá prázdný objekt filmu do zobrazení pro vytváření. Všechny metody, které vytvářejí, upravují, odstraňují nebo jinak upravují data, jsou v `HttpPost` přetížení metody. Úprava dat v metodě HTTP GET je bezpečnostní riziko, jak je popsáno v příspěvku na blogu [ASP.NET #46 Tip – nepoužívejte odstranit propojení, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Úpravy dat v metodě GET také porušují osvědčené postupy HTTP a model [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) architektury, který určuje, že požadavky GET by neměly měnit stav aplikace. Jinými slovy, provádění operace GET by mělo být bezpečná operace, která nemá žádné vedlejší účinky a neupravuje vaše trvalá data.

## <a name="jquery-validation-for-non-english-locales"></a>ověření jQuery pro jiné než anglické národní prostředí

Pokud používáte počítač v češtině, můžete tuto část přeskočit a přejít k dalšímu kurzu. Verzi globalizace tohoto kurzu si můžete stáhnout [tady](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475). Kurz o tom, jak se na mezinárodní základě vychází, najdete v tématu [Nadeem 's ASP.NET MVC 5 – mezinárodní](http://afana.me/post/aspnet-mvc-internationalization.aspx).

> [!NOTE]
> aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku ( &quot; , &quot; ) pro desetinné čárky a formáty kalendářních dat mimo USA, je nutné zahrnout *globalize.js* a konkrétní *jazykové verze/globalize.cultures.js* souboru (z [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) a JavaScriptu pro použití `Globalize.parseFloat` . Z NuGet můžete získat ověřování jQuery bez angličtiny. (Neinstalujte globalizaci, pokud používáte anglické národní prostředí.)

1. V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Spravovat balíčky NuGet pro řešení**.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. V levém podokně vyberte <strong>Procházet *.</strong> * (Podívejte se na obrázek níže.)
3. Do vstupního pole zadejte * globalizace * *.

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) Vyberte `jQuery.Validation.Globalize` , vyberte `MvcMovie` a klikněte na **nainstalovat**. Soubor *Scripts\jquery.globalize\globalize.js* se přidá do vašeho projektu. Složka * Scripts\jquery.globalize\cultures \* bude obsahovat mnoho souborů JavaScriptu jazykové verze. Poznámka: instalace tohoto balíčku může trvat pět minut.

   Následující kód ukazuje úpravy souboru Views\Movies\Edit.cshtml:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Chcete-li se vyhnout opakování tohoto kódu v každém zobrazení pro úpravy, můžete ho přesunout do souboru rozložení. Pokud chcete optimalizovat stažení skriptu, přečtěte si téma moje výukové [sdružování a minifikace](../../performance/bundling-and-minification.md).

Další informace najdete v části [ASP.NET MVC 3 – mezinárodní](http://afana.me/post/aspnet-mvc-internationalization.aspx) využití a [ASP.NET MVC 3 – část 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).

Pokud se vám dočasná oprava nedaří ověřit ve svém národním prostředí, můžete vašemu počítači vynutit použití anglické angličtiny nebo můžete v prohlížeči zakázat JavaScript. Chcete-li vynutit, aby počítač používal anglickou angličtinu, můžete přidat prvek globalizace do kořenového souboru projektu *web.config* . Následující kód ukazuje prvek globalizace s jazykovou verzí nastavenou na USA angličtinu.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> V dalším kurzu implementujeme funkce vyhledávání.

> [!div class="step-by-step"]
> [Předchozí](accessing-your-models-data-from-a-controller.md) 
>  [Další](adding-search.md)
