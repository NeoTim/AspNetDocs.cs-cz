---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Implementace efektivního stránkování dat | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 8 ukazuje, jak přidat podporu stránkování na naši adresu URL / Dinners, takže místo zobrazení 1000s večeří najednou zobrazíme pouze 10 nadcházejících večeří na...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541322"
---
# <a name="implement-efficient-data-paging"></a>Implementace efektivního stránkování dat

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 8 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malou, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 8 ukazuje, jak přidat podporu stránkování do naší adresy URL /Dinners, takže místo zobrazení 1000s večeří najednou zobrazíme pouze 10 nadcházejících večeří najednou - a umožníme koncovým uživatelům stránku zpět a vpřed přes celý seznam přátelským způsobem SEO.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner Krok 8: Paging podpora

Pokud naše stránky budou úspěšné, budou mít tisíce nadcházejících večeří. Musíme se ujistit, že naše uživatelské ho ui škály pro zpracování všech těchto večeří a umožňuje uživatelům procházet. Chcete-li to povolit, přidáme podporu stránkování do naší adresy URL */Dinners* tak, abychom místo zobrazení 1000s večeří najednou zobrazili pouze 10 nadcházejících večeří najednou - a umožnili koncovým uživatelům stránkovat zpět a vpřed celý seznam přátelským způsobem.

### <a name="index-action-method-recap"></a>Index() Rekapitulace metody akce

Metoda akce Index() v rámci naší třídy DinnersController v současné době vypadá takto:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

Když je požadavek na adresu URL */Dinners,* načte seznam všech nadcházejících večeří a pak vykreslí seznam všech z nich ven:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>Principy IQueryable&lt;T&gt;

*IQueryable&lt;&gt; T* je rozhraní, které bylo zavedeno s LINQ jako součást rozhraní .NET 3.5. Umožňuje výkonné scénáře "odložené spuštění", které můžeme využít k implementaci podpory stránkování.

V našem DinnerRepository vracíme&lt;IQueryable&gt; Dinner sekvence z naší FindUpcomingDinners() metoda:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

IQueryable&lt;Dinner&gt; objektvrácené naše FindUpcomingDinners() metoda zapouzdřuje dotaz načíst Dinner objekty z naší databáze pomocí LINQ do SQL. Důležité je, že nebude provádět dotaz proti databázi, dokud se nepokusíme o přístup/ iterát přes data v dotazu, nebo dokud jsme volání ToList() metoda na něm. Kód volá naše FindUpcomingDinners() metoda můžete volitelně zvolit přidat další "zřetězené" operace/filtry na IQueryable&lt;Dinner&gt; objektu před spuštěním dotazu. LINQ na SQL je pak dostatečně chytrý, aby spustit kombinovaný dotaz proti databázi při požadavku na data.

Chcete-li implementovat stránkovací logiku, můžeme aktualizovat naši metodu akce Index() společnosti DinnersController tak, aby&lt;&gt; na vrácenou posloupnost IQueryable Dinner aponovala další operátory "Skip" a "Take" před voláním ToList() na něm:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

Výše uvedený kód přeskočí přes prvních 10 nadcházející večeře v databázi a potom vrátí zpět 20 večeří. LINQ to SQL je dostatečně chytrý na to, aby vytvořil optimalizovaný dotaz SQL, který provádí tuto logiku přeskakování v databázi SQL – a ne na webovém serveru. To znamená, že i v případě, že máme miliony nadcházející večeře v databázi, pouze 10 chceme budou načteny jako součást tohoto požadavku (takže je efektivní a škálovatelné).

### <a name="adding-a-page-value-to-the-url"></a>Přidání hodnoty "stránky" do adresy URL

Namísto pevného kódování určitého rozsahu stránek chceme, aby naše adresy URL obsahovaly parametr "page", který označuje, který rozsah večeří uživatel požaduje.

#### <a name="using-a-querystring-value"></a>Použití hodnoty Querystring

Níže uvedený kód ukazuje, jak můžeme aktualizovat naši metodu akce Index() pro podporu parametru řetězce dotazu a povolit adresy URL jako */Dinners?page=2*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

Metoda akce Index() výše má parametr s názvem "stránka". Parametr je deklarován jako celé číslo s možnou hodnotou null (to znamená, co int? To znamená, že adresa URL */Dinners?page=2* způsobí, že hodnota "2" bude předána jako hodnota parametru. *Adresa /Dinners* URL (bez hodnoty řetězce dotazu) způsobí předání hodnoty null.

Vynásobíme hodnotu stránky velikostí stránky (v tomto případě 10 řádků), abychom zjistili, kolik večeří má přeskočit. Používáme [c# null "coalescing" operátor (??),](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) který je užitečný při práci s nullable typy. Výše uvedený kód přiřadí stránce hodnotu 0, pokud je parametr stránky nulový.

#### <a name="using-embedded-url-values"></a>Použití vložených hodnot url

Alternativou k použití querystring hodnotu by bylo vložit parametr stránky v rámci samotné adresy URL. Příklad: */Dinners/Page/2* nebo */Dinners/2*. ASP.NET MVC obsahuje výkonný modul pro směrování adres URL, který usnadňuje podporu scénářů, jako je tento.

Můžeme zaregistrovat vlastní pravidla směrování, která mapují libovolnou příchozí adresu URL nebo formát ADRESY URL na libovolnou třídu nebo metodu akce řadiče, kterou chceme. Vše, co potřebujeme udělat, je otevřít soubor Global.asax v rámci našeho projektu:

![](implement-efficient-data-paging/_static/image2.png)

A pak zaregistrujte nové pravidlo mapování pomocí MapRoute() pomocné metody, jako je první volání tras. MapRoute() níže:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Výše registrujeme nové pravidlo směrování s názvem "Nadcházející večeře". Uvádíme, že má formát URL "Dinners/Page/{page}" – kde {page} je hodnota parametru vložená do adresy URL. Třetí parametr metody MapRoute() označuje, že bychom měli mapovat adresy URL, které odpovídají tomuto formátu, na metodu akce Index() ve třídě DinnersController.

Můžeme použít přesně stejný Index() kód jsme měli před s naší mačká scénář Querystring – s výjimkou nyní naše "page" parametr bude pocházet z URL a ne querystring:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

A teď, když spustíme aplikaci a zadejte */ Večeře* uvidíme prvních 10 nadcházejícívečeře:

![](implement-efficient-data-paging/_static/image3.png)

A když zadáme */Dinners/Page/1,* uvidíme další stránku večeří:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Přidání uživatelského uživatelského uživatelského panelu navigace na stránce

Posledním krokem k dokončení našeho stránkování scénář bude implementovat "další" a "předchozí" navigační uživatelské okno v rámci naší šablony zobrazení, aby uživatelé snadno přeskočit data večeři.

Chcete-li implementovat správně, budeme potřebovat znát celkový počet večeří v databázi, stejně jako kolik stránek dat to překládá. Poté budeme muset vypočítat, zda je aktuálně požadovaná hodnota "stránka" na začátku nebo na konci dat, a odpovídajícím způsobem zobrazit nebo skrýt předchozí a "další" uI. Tuto logiku můžeme implementovat v rámci naší metody akce Index(). Alternativně můžeme přidat pomocnou třídu do našeho projektu, který zapouzdřuje tuto logiku více re-použitelným způsobem.

Níže je jednoduchá "PaginatedList" pomocná třída,&lt;která&gt; je odvozena z list T třídy kolekce zabudované do rozhraní .NET Framework. Implementuje opakovaně použitelnou třídu kolekce, která může být použita k stránkování libovolné sekvence dat IQueryable. V naší aplikaci NerdDinner budeme mít to&lt;&gt; pracovat přes IQueryable Dinner výsledky, ale&lt;&gt; to by&lt;mohlo&gt; stejně snadno použít proti IQueryable produktu nebo IQueryable zákazník výsledky v jiných scénářích aplikace:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

Všimněte si, jak vypočítá a potom zpřístupňuje vlastnosti jako "PageIndex", "PageSize", "TotalCount" a "TotalPages". Také pak zpřístupní dvě pomocné vlastnosti "HasPreviousPage" a "HasNextPage", které označují, zda je stránka dat v kolekci na začátku nebo na konci původní sekvence. Výše uvedený kód způsobí spuštění dvou dotazů SQL – první načíst počet celkový počet Dinner objekty (to nevrátí objekty – spíše provede příkaz "SELECT COUNT", který vrátí celé číslo) a druhý načíst pouze řádky dat, které potřebujeme z naší databáze pro aktuální stránku dat.

Můžeme pak aktualizovat naše DinnersController.Index() pomocná metoda k&lt;vytvoření&gt; Večeři PaginatedList z našeho DinnerRepository.FindUpcomingDinners() výsledek a předat ji do našeho zobrazení šablony:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Potom můžeme aktualizovat šablonu zobrazení \Views\Dinners\Index.aspx,&lt;která se dědí z aplikace&lt;ViewPage&gt; &gt; NerdDinner.Helpers.PaginatedList Dinner místo aplikace&lt;ViewPage IEnumerable&lt;Dinner&gt;&gt;, a potom přidat následující kód na konec naší šablony zobrazení, aby se zobrazilo nebo skrylo další a předchozí navigační uživatelské tlačítko:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Všimněte si, jak používáme Html.RouteLink() pomocnou metodu pro generování našich hypertextových odkazů. Tato metoda je podobná metodě pomocné položky Html.ActionLink(), kterou jsme použili dříve. Rozdíl je v tom, že generujeme adresu URL pomocí pravidla směrování "UpcomingDinners", které nastavujeme v našem souboru Global.asax. Tím zajistíme, že budeme generovat adresy URL do naší metody akce Index(), které mají formát: */Dinners/Page/{page}* – kde hodnota {page} je proměnná, kterou poskytujeme výše na základě aktuálního PageIndex.

A teď, když spustíme naši aplikaci znovu uvidíme 10 večeří najednou v našem prohlížeči:

![](implement-efficient-data-paging/_static/image5.png)

&lt; &lt; Máme &lt; také &gt; &gt; &gt; navigační uživatelské tlačítko v dolní části stránky, které nám umožňuje přeskočit dopředu a dozadu přes naše data pomocí vyhledávacího stroje přístupné adresy URL:

![](implement-efficient-data-paging/_static/image6.png)

| **Boční téma: Pochopení důsledků IQueryable&lt;T&gt;** |
| --- |
| IQueryable&lt;&gt; T je velmi výkonná funkce, která umožňuje řadu zajímavých scénářů odložené spuštění (jako je stránkování a dotazy založené na složení). Stejně jako u všech výkonných funkcí, chcete být opatrní s tím, jak ji používat, a ujistěte se, že není zneužívána. Je důležité si uvědomit, že&lt;vrácení&gt; iQueryable T výsledek z vašeho úložiště umožňuje volání kódu připojit na zřetězené operátor metody k němu, a tak se podílet na konečné spuštění dotazu. Pokud nechcete poskytnout volající kód této schopnosti, pak&lt;byste&gt; měli vrátit&lt;zpět&gt; IList T nebo IEnumerable T výsledky - které obsahují výsledky dotazu, který již byl proveden. Pro scénáře stránkování by to vyžadovalo, abyste do volané metody úložiště posunuli logiku stránkování skutečných dat. V tomto scénáři můžeme aktualizovat naše FindUpcomingDinners() finder metoda mít podpis, který buď vrátil&lt; &gt; PaginatedList: PaginatedList Dinner FindComingDinners (int&lt;pageIndex, int pageSize) { } Nebo vrátit zpět IList Dinner&gt;, a použít "totalCount" z param vrátit celkový počet Dinners: IList&lt;Dinner&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) { } |

### <a name="next-step"></a>Další krok

Podívejme se nyní na to, jak můžeme do naší aplikace přidat podporu ověřování a autorizace.

> [!div class="step-by-step"]
> [Předchozí](re-use-ui-using-master-pages-and-partials.md)
> [další](secure-applications-using-authentication-and-authorization.md)
