---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045166"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Přístup k datům modelu z kontroleru

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

V této části vytvoříte novou `MoviesController` třídu a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení.

Než začnete pokračovat k dalšímu kroku, **sestavte aplikaci** . Pokud nevytvoříte aplikaci, zobrazí se chyba při přidávání kontroleru.

V Průzkumník řešení klikněte pravým tlačítkem na složku *Controllers* a pak klikněte na **Přidat**a pak na **kontroler**.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

V dialogovém okně **Přidat vygenerované uživatelské rozhraní** klikněte na **kontroler MVC 5 se zobrazeními, pomocí Entity Framework**a pak klikněte na **Přidat**.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Vyberte **video (MvcMovie. Models)** pro třídu modelu.
- Jako třídu kontextu dat vyberte **MovieDBContext (MvcMovie. Models)** .
- Jako název kontroleru zadejte **MoviesController**.

  Následující obrázek ukazuje dokončený dialog.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

Klikněte na **Přidat**. (Pokud se zobrazí chyba, pravděpodobně jste před zahájením přidávání kontroleru aplikaci nesestavili.) Visual Studio vytvoří následující soubory a složky:

- Soubor *MoviesController.cs* ve složce *Controllers* .
- Složka *Views\Movies*
- *Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .

Aplikace Visual Studio automaticky vytvořila metody a zobrazení akcí [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (vytváření, čtení, aktualizace a odstraňování) (automatické vytváření metod a zobrazení operace CRUD se říká generování uživatelského rozhraní). Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.

Spusťte aplikaci a klikněte na filmový odkaz **MVC** (nebo přejděte k `Movies` řadiči pomocí připojení */Movies* k adrese URL v adresním řádku prohlížeče). Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *App \_ Start\RouteConfig.cs* ), požadavek prohlížeče `http://localhost:xxxxx/Movies` se směruje na výchozí `Index` metodu akce `Movies` kontroleru. Jinými slovy, požadavek prohlížeče `http://localhost:xxxxx/Movies` je efektivně stejný jako požadavek prohlížeče `http://localhost:xxxxx/Movies/Index` . Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Vytvoření filmu

Vyberte odkaz **vytvořit nový** . Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> V poli Price možná nebudete moct zadat desetinné nebo čárkové tečky. Aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku ( &quot; , &quot; ) pro desetinné čárky a formáty kalendářních dat mimo USA, je nutné zahrnout *globalize.js* a konkrétní *jazykové verze/globalize.cultures.js* souboru (z [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) a JavaScriptu pro použití `Globalize.parseFloat` . Ukážeme si, jak to udělat v dalším kurzu. Prozatím stačí zadat celá čísla, třeba 10.

Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi. Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Vytvořte ještě několik dalších záznamů filmů. Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.

## <a name="examining-the-generated-code"></a>Prověřování generovaného kódu

Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou `Index` metodu. Část kontroleru filmů s `Index` metodou je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Požadavek na `Movies` kontroler vrátí všechny položky v `Movies` tabulce a poté předá výsledky `Index` zobrazení. Následující řádek z `MoviesController` třídy vytvoří instanci kontextu databáze videa, jak je popsáno výše. Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Modely silného typu a @model klíčové slovo

Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí `ViewBag` objektu. `ViewBag`Je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace zobrazení.

MVC také poskytuje možnost předat objekty *silného* typu do šablony zobrazení. Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) v editoru sady Visual Studio. Mechanizmus pro generování uživatelského rozhraní v aplikaci Visual Studio používal tento přístup (to znamená předání modelu *silného* typu) spolu s `MoviesController` třídou a zobrazení šablon při vytváření metod a zobrazení.

V souboru *Controllers\MoviesController.cs* prověřte vygenerovanou `Details` metodu. `Details`Metoda je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`Parametr je obecně předán jako data směrování, například `http://localhost:1234/movies/details/1` Nastaví kontroler na filmový kontroler, akci na `details` a na `id` 1. ID můžete předat také řetězci dotazu následujícím způsobem:

`http://localhost:1234/movies/details?id=1`

Pokud `Movie` je nalezen, instance `Movie` modelu je předána do `Details` zobrazení:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

Projděte si obsah souboru *Views\Movies\Details.cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Zahrnutím `@model` příkazu v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává. Když jste vytvořili kontroler filmů, Visual Studio automaticky zahrne následující `@model` příkaz na začátek souboru *Details. cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Tato `@model` Direktiva umožňuje přístup k videu, který kontroler předává do zobrazení pomocí `Model` objektu se silným typem. Například v šabloně *Details. cshtml* kód předá každé pole videa `DisplayNameFor` [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) pomocníkům HTML pomocí objektu silného typu `Model` . `Create`Šablony a `Edit` metody a zobrazení také předají objekt filmového modelu.

Prohlédněte si šablonu zobrazení *index. cshtml* a `Index` metodu v souboru *MoviesController.cs* . Všimněte si, jak kód vytvoří [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) objekt při volání `View` pomocné metody v `Index` metodě Action. Kód pak předá tento `Movies` seznam z `Index` metody Action do zobrazení:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

Když jste vytvořili kontroler filmů, Visual Studio automaticky obsahuje následující `@model` příkaz v horní části souboru *index. cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Tato `@model` Direktiva umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí `Model` silně typovaného objektu. Například v šabloně *index. cshtml* kód projde pomocí příkazu v rámci `foreach` objektu silného typu `Model` :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

Vzhledem k tomu `Model` , že objekt je silného typu (jako `IEnumerable<Movie>` objekt), každý `item` objekt ve smyčce je zadán jako `Movie` . Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>Práce s verzí SQL Server LocalDB

Entity Framework Code First zjistila, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil. Můžete ověřit, jestli je vytvořený, tak, že vyhledáte složku * \_ data aplikací* . Pokud nevidíte soubor *filmy. mdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku * \_ data aplikací* .

![](accessing-your-models-data-from-a-controller/_static/image9.png)

Dvojím kliknutím na *filmy. mdf* otevřete **Průzkumníka serveru**a potom rozbalte složku **Tables (tabulky** ) a zobrazte tabulku filmů. Poznamenejte si klíčovou ikonu vedle pole ID. Ve výchozím nastavení vlastnost EF vytvoří primární klíč s názvem ID. Další informace o EF a MVC najdete v Dykstra skvělého kurzu na [MVC a EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Kliknutím pravým tlačítkem myši na `Movies` tabulku a výběrem **Zobrazit tabulku data** zobrazíte data, která jste vytvořili.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Klikněte pravým tlačítkem na `Movies` tabulku a vyberte možnost **Otevřít definici tabulky** . zobrazí se struktura tabulky, kterou Entity Framework Code First vytvořili.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Všimněte si, jak se schéma `Movies` tabulky mapuje na `Movie` třídu, kterou jste vytvořili dříve. Entity Framework Code First automaticky vytvořil toto schéma na základě vaší `Movie` třídy.

Až skončíte, připojení zavřete kliknutím pravým tlačítkem na *MovieDBContext* a výběrem možnosti **Zavřít připojení**. (Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Teď máte databázi a stránky k zobrazení, úpravám, aktualizaci a odstraňování dat. V dalším kurzu probereme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní Hledat filmy v této databázi. Další informace o použití Entity Framework s MVC najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Předchozí](creating-a-connection-string.md) 
>  [Další](examining-the-edit-methods-and-edit-view.md)
