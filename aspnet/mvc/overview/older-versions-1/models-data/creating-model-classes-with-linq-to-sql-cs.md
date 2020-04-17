---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: Vytváření tříd modelu s LINQ na SQL (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelu pro ASP.NET aplikace MVC. V tomto kurzu se naučíte, jak vytvořit model c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: eac6fec3a4cfd833b810378d946874a246d9a2c3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542726"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>Vytvoření tříd modelu pomocí LINQ to SQL (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelu pro ASP.NET aplikace MVC. V tomto kurzu se dozvíte, jak vytvářet třídy modelu a provádět přístup k databázi s využitím microsoft linq na SQL.

Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelu pro ASP.NET aplikace MVC. V tomto kurzu se dozvíte, jak vytvářet třídy modelů a provádět přístup k databázi s využitím služeb Microsoft LINQ na SQL

V tomto kurzu vytvoříme základní databázovou aplikaci Movie. Začneme tím, že vytvoříme databázovou aplikaci Movie nejrychlejším a nejjednodušším možným způsobem. Veškerý přístup k našim datům provádíme přímo z akcí našeho správce.

Dále se dozvíte, jak používat vzor úložiště. Použití vzoru úložiště vyžaduje trochu více práce. Výhodou přijetí tohoto vzoru je však to, že umožňuje vytvářet aplikace, které jsou adaptabilní na změnu a lze je snadno otestovat.

## <a name="what-is-a-model-class"></a>Co je modelová třída?

Model MVC obsahuje veškerou aplikační logiku, která není obsažena v zobrazení MVC nebo mvc řadiči. Zejména model MVC obsahuje všechny vaše obchodní aplikace a logiku přístupu k datům.

K implementaci logiky přístupu k datům můžete použít celou řadu různých technologií. Můžete například vytvořit třídy přístupu k datům pomocí microsoft entity framework, NHibernate, Subsonic nebo ADO.NET třídy.

V tomto kurzu používám LINQ na SQL k dotazování a aktualizaci databáze. LINQ to SQL poskytuje velmi snadný způsob interakce s databází serveru Microsoft SQL Server. Je však důležité si uvědomit, že ASP.NET MVC framework není vázána na LINQ sql v žádném případě. ASP.NET MVC je kompatibilní s jakoukoli technologií přístupu k datům.

## <a name="create-a-movie-database"></a>Vytvoření filmové databáze

V tomto kurzu – aby bylo možné ilustrovat, jak můžete vytvářet třídy modelu -- vytvoříme jednoduchou databázovou aplikaci Movie. Prvním krokem je vytvoření nové databáze. Klepněte pravým\_tlačítkem myši na složku Data aplikace v okně Průzkumník řešení a vyberte možnost nabídky **Přidat, Novou položku**. Vyberte šablonu **databáze serveru SQL Server,** pojmenujte ji MoviesDB.mdf a klikněte na tlačítko **Přidat** (viz obrázek 1).

[![Přidání nové databáze serveru SQL Server](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Obrázek 01**: Přidání nové databáze serveru SQL Server[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image3.png)

Po vytvoření nové databáze můžete databázi otevřít poklepáním na soubor MoviesDB.mdf ve složce Data aplikace.\_ Poklepáním na soubor MoviesDB.mdf se otevře okno Průzkumník serveru (viz obrázek 2).

Okno Průzkumníkserveru se při použití aplikace Visual Web Developer nazývá okno Průzkumník databáze.

[![Použití okna Průzkumníka serveru](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Obrázek 02**: Použití okna Průzkumníkserveru[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image6.png)

Musíme do naší databáze přidat jednu tabulku, která reprezentuje naše filmy. Klepněte pravým tlačítkem myši na složku Tabulky a vyberte možnost nabídky **Přidat novou tabulku**. Výběrem této možnosti nabídky se otevře Návrhář tabulek (viz obrázek 3).

[![Použití okna Průzkumníka serveru](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Obrázek 03**: Návrhář tabulky[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image9.png)

Do tabulky databáze musíme přidat následující sloupce:

| **Název sloupce** | **Typ dat** | **Povolit hodnoty Null** |
| --- | --- | --- |
| ID | Int | False |
| Nadpis | Nvarchar(200) | False |
| Ředitel | Nvarchar(50) | False |

Musíte udělat dvě zvláštní věci do sloupce Id. Nejprve je třeba označit sloupec Id jako sloupec primárního klíče tak, že vyberete sloupec v Návrháři tabulek a kliknete na ikonu klíče. LINQ to SQL vyžaduje zadání sloupců primárního klíče při provádění vložení nebo aktualizace proti databázi.

Dále je třeba označit sloupec ID jako sloupec Identity přiřazením hodnoty Ano **vlastnosti Je identita** (viz obrázek 3). Sloupec Identita je sloupec, kterému je automaticky přiřazeno nové číslo při každém přidání nového řádku dat do tabulky.

## <a name="create-linq-to-sql-classes"></a>Vytvořit třídy LINQ na SQL

Náš model MVC bude obsahovat třídy LINQ to SQL, které představují databázovou tabulku tblMovie. Nejjednodušší způsob, jak vytvořit tyto třídy LINQ na SQL, je kliknout pravým tlačítkem myši na složku Modely, vybrat **možnost Přidat, Nová položka**, vybrat šablonu LINQ do tříd SQL, dát třídám název Movie.dbml a kliknout na tlačítko **Přidat** (viz obrázek 4).

[![Vytváření tříd LINQ na SQL](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Obrázek 04**: Vytvoření tříd LINQ na SQL[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image12.png)

Ihned po vytvoření movie LINQ na SQL třídy, objekt relační návrhář se zobrazí. Databázové tabulky můžete přetáhnout z okna Průzkumníka serveru do návrháře relačních objektů a vytvořit tak LINQ na třídy SQL, které představují konkrétní databázové tabulky. Musíme přidat databázovou tabulku tblMovie do objektu Relační designer (viz obrázek 5).

[![Použití relačního návrháře objektu](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Obrázek 05**: Použití návrháře relačních objektů[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image15.png)

Ve výchozím nastavení vytvoří návrhář relační objekttřídy třídy se stejným názvem jako databázová tabulka, kterou přetáhnete do návrháře. Nechceme však volat do naší `tblMovie`třídy . Proto klepněte na název třídy v návrháři a změňte název třídy na Film.

Nakonec nezapomeňte kliknout na tlačítko **Uložit** (obrázek diskety) pro uložení LINQ do tříd SQL. V opačném případě linq na SQL třídy nebudou generovány objektrelační návrháře.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Použití LINQ na SQL v akci řadiče

Nyní, když máme naše LINQ na SQL třídy, můžeme použít tyto třídy k načtení dat z databáze. V této části se dozvíte, jak používat linq na SQL třídy přímo v rámci akce kontroleru. Zobrazíme seznam filmů z tabulky databáze tblMovies v zobrazení MVC.

Nejprve je třeba upravit HomeController třídy. Tuto třídu najdete ve složce Řadiče vaší aplikace. Upravte třídu tak, aby vypadala jako třída v seznamu 1.

**Výpis 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

Akce `Index()` v výpisu 1 používá linq na `MovieDataContext`SQL DataContext `MoviesDB` třídy () představují databázi. Třída `MoveDataContext` byla generována Visual Studio Objekt Relační designer.

Dotaz LINQ se provádí proti DataContext načíst všechny `tblMovies` filmy z tabulky databáze. Seznam filmů je přiřazen k místní `movies`proměnné s názvem . Nakonec je seznam filmů předán zobrazení prostřednictvím dat zobrazení.

Aby bylo možné zobrazit filmy, dále je třeba upravit zobrazení indexu. Zobrazení rejstříku najdete `Views\Home\` ve složce. Aktualizujte zobrazení rejstříku tak, aby vypadalo jako zobrazení v seznamu 2.

**Výpis 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Všimněte si, že `<%@ import namespace %>` upravené zobrazení indexu obsahuje direktivu v horní části zobrazení. Tato směrnice dováží `MvcApplication1.Models namespace`. Potřebujeme tento obor názvů, abychom `model` mohli pracovat s `Movie` třídami – zejména s třídou – v zobrazení.

Zobrazení v výpisu `foreach` 2 obsahuje smyčku, která itetuje přes všechny položky reprezentované vlastností. `ViewData.Model` Hodnota vlastnosti `Title` je zobrazena `movie`pro každou .

Všimněte si, `ViewData.Model` že hodnota vlastnosti je přetypována do . `IEnumerable` To je nezbytné pro prosmykat obsah `ViewData.Model`. Další možností je vytvořit silný typ `view`. Když vytvoříte silně typovaný `view`, přetypovat `ViewData.Model` vlastnost na určitý typ v zobrazení kód na pozadí třídy.

Pokud spustíte aplikaci po `HomeController` úpravě třídy a zobrazení indexu, zobrazí se prázdná stránka. Zobrazí se prázdná stránka, protože v databázové `tblMovies` tabulce nejsou žádné filmové záznamy.

Chcete-li přidat záznamy `tblMovies` do databázové tabulky, klepněte pravým tlačítkem `tblMovies` myši na databázovou tabulku v okně Průzkumník serveru (okno Průzkumník databáze v aplikaci Visual Web Developer) a vyberte možnost nabídky Zobrazit data tabulky. Záznamy můžete `movie` vložit pomocí mřížky, která se zobrazí (viz obrázek 6).

[![Vkládání filmů](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Obrázek 06**: Vkládání[filmů(Kliknutím zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image18.png)

Po přidání některých databázových záznamů do `tblMovies` tabulky a spuštění aplikace se zobrazí stránka na obrázku 7. Všechny záznamy filmové databáze jsou zobrazeny v seznamu s odrážkami.

[![Zobrazení filmů v zobrazení Rejstřík](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Obrázek 07**: Zobrazení filmů v zobrazení rejstříku(Kliknutím[zobrazíte obrázek v plné velikosti)](creating-model-classes-with-linq-to-sql-cs/_static/image21.png)

## <a name="using-the-repository-pattern"></a>Použití vzoru úložiště

V předchozí části jsme použili LINQ na SQL třídy přímo v rámci akce kontroleru. Použili `MovieDataContext` jsme třídu `Index()` přímo z akce řadiče. Není nic špatného na tom, že v případě jednoduché aplikace. Práce přímo s LINQ na SQL ve třídě řadiče však vytváří problémy, když potřebujete vytvořit složitější aplikaci.

Použití LINQ sql v rámci třídy řadiče ztěžuje přepínání technologií přístupu k datům v budoucnu. Můžete se například rozhodnout přejít z používání microsoft linq na SQL na using Microsoft Entity Framework jako technologie přístupu k datům. V takovém případě budete muset přepsat každý řadič, který přistupuje k databázi v rámci vaší aplikace.

Použití LINQ sql v rámci třídy řadiče také ztěžuje sestavení testů částí pro vaši aplikaci. Za normálních okolností nechcete pracovat s databází při provádění testů částí. Chcete použít testy částí k testování aplikační logiky a nikoli databázového serveru.

Chcete-li vytvořit aplikaci MVC, která je více přizpůsobitelná budoucím změnám a kterou lze snadněji testovat, měli byste zvážit použití vzoru úložiště. Při použití vzoru úložiště vytvoříte samostatnou třídu úložiště, která obsahuje všechny logiky přístupu k databázi.

Při vytváření třídy úložiště vytvoříte rozhraní, které představuje všechny metody používané třídou úložiště. V rámci řadiče, napíšete kód proti rozhraní namísto úložiště. Tímto způsobem můžete implementovat úložiště pomocí různých technologií přístupu k datům v budoucnu.

Rozhraní v listing u `IMovieRepository` 3 je pojmenováno `ListAll()`a představuje jednu metodu s názvem .

**Výpis 3 –`Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

Třída úložiště v listingu 4 `IMovieRepository` implementuje rozhraní. Všimněte si, že `ListAll()` obsahuje metodu s názvem, která odpovídá metodě vyžadované `IMovieRepository` rozhraní.

**Výpis 4 –`Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Nakonec třída `MoviesController` v výpisu 5 používá vzor úložiště. Již používá linq na SQL třídy přímo.

**Výpis 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Všimněte `MoviesController` si, že třída v výpisu 5 má dva konstruktory. První konstruktor, konstruktor bez parametrů, je volána při spuštění aplikace. Tento konstruktor vytvoří instanci `MovieRepository` třídy a předá ji druhému konstruktoru.

Druhý konstruktor má jeden parametr: `IMovieRepository` parametr. Tento konstruktor jednoduše přiřadí hodnotu parametru poli `_repository`na úrovni třídy s názvem .

Třída `MoviesController` využívá návrhový vzor softwaru nazvaný vzor vkládání závislostí. Zejména používá něco, co nazývá vkládání závislostí konstruktoru. Můžete si přečíst více o tomto vzoru čtením následujícího článku Martin Fowler:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Všimněte si, že `MoviesController` všechny kód ve třídě (s výjimkou první `IMovieRepository` konstruktor) spolupracuje `MovieRepository` s rozhraním namísto skutečné třídy. Kód spolupracuje s abstraktní rozhraní namísto konkrétní implementace rozhraní.

Pokud chcete upravit technologii přístupu k datům používanou `IMovieRepository` aplikací, můžete jednoduše implementovat rozhraní s třídou, která používá technologii alternativního přístupu k databázi. Můžete například vytvořit `EntityFrameworkMovieRepository` třídu `SubSonicMovieRepository` nebo třídu. Vzhledem k tomu, že třída kontroleru je naprogramována proti rozhraní, můžete předat novou implementaci `IMovieRepository` do třídy kontroleru a třída bude pokračovat v práci.

Kromě toho, pokud chcete `MoviesController` otestovat třídu, pak můžete předat falešné `HomeController`video úložiště třídy na . Můžete implementovat `IMovieRepository` třídu s třídou, která není ve skutečnosti přístup `IMovieRepository` k databázi, ale obsahuje všechny požadované metody rozhraní. Tímto způsobem můžete jednotkový test třídy `MoviesController` bez skutečné databáze.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo ukázat, jak můžete vytvořit třídy modelu MVC s využitím microsoft linq na SQL. Zkoumali jsme dvě strategie pro zobrazení databázových dat v ASP.NET aplikaci MVC. Nejprve jsme vytvořili linq na SQL třídy a používá třídy přímo v rámci akce kontroleru. Použití tříd LINQ to SQL v rámci řadiče umožňuje rychlé a snadné zobrazení databázových dat v aplikaci MVC.

Dále jsme prozkoumali o něco obtížnější, ale rozhodně ctnostnější cestu pro zobrazení dat databáze. Využili jsme vzor úložiště a umístili všechny naše logiky přístupu k databázi do samostatné třídy úložiště. V našem řadiči jsme napsali všechny naše kód proti rozhraní namísto konkrétní třídy. Výhodou vzoru úložiště je, že nám umožňuje v budoucnu snadno měnit technologie přístupu k databázi a umožňuje nám snadno testovat naše třídy kontrolerů.

> [!div class="step-by-step"]
> [Předchozí](creating-model-classes-with-the-entity-framework-cs.md)
> [další](displaying-a-table-of-database-data-cs.md)
