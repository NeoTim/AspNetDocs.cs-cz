---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: Přidání modelu (C#) | Dokumentace Microsoftu
author: Rick-Anderson
description: 'Poznámka: Najít aktualizovanou verzi tohoto kurzu je k dispozici tady, která používá ASP.NET MVC 5 a Visual Studio 2013. Je bezpečnější, sledovat a ukázka mnohem jednodušší...'
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: f35e1fec7b3b2a1fc53cf8beb3781a2e2f6c8740
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068707"
---
<a name="adding-a-model-c"></a>Přidání modelu (C#)
====================
Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))

> V tomto kurzu se seznámíte se základy vytváření ASP.NET MVC webovou aplikaci pomocí Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze sady Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Kliknutím na následující odkaz můžete nainstalovat všechny z nich: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternativně můžete nainstalovat jednotlivě požadavky pomocí následujících odkazů:
> 
> - [Visual Studio Web Developer Express SP1 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Tools Update](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime a nástroje)
> 
> Pokud používáte Visual Studio 2010 namísto Visual Web Developer 2010, nainstalujte příslušné požadované součásti po kliknutí na následující odkaz: [Visual Studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt aplikace Visual Web Developer se zdrojovým kódem jazyka C# je k dispozici v tomto tématu. [Stáhněte si verzi C#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost jazyka Visual Basic, přejděte [verze jazyka Visual Basic](../vb/adding-a-model.md) tohoto kurzu.


## <a name="adding-a-model"></a>Přidání modelu

V této části přidáte některé třídy pro správu filmy v databázi. Tyto třídy bude "model" část aplikace ASP.NET MVC.

Přístup k datům technologie rozhraní .NET Framework označované jako Entity Framework budete používat k definování a pracovat s tyto třídy modelu. Entity Framework (často označované jako EF) podporuje vývoj paradigma volá *Code First*. Kód nejprve umožňuje vytvořit objekty modelu napsáním jednoduché třídy. (Tyto jsou také známé jako POCO tříd, z "prostý staré objekty CLR.") Potom můžete mít databázi vytvořené v reálném čase ze třídy, která umožňuje pracovní postupy s velmi čistá a rychlý vývoj.

## <a name="adding-model-classes"></a>Přidání třídy modelu

V **Průzkumníka řešení**, klikněte pravým tlačítkem myši *modely* složky, vyberte **přidat**a pak vyberte **třídy**.

![](adding-a-model/_static/image1.png)

Název *třídy* "Video".

[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)

Následujících pět vlastnosti, které chcete přidat `Movie` třídy:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Použijeme `Movie` pro reprezentaci filmy v databázi. Každá instance `Movie` objektu bude odpovídat řádek do tabulky databáze a každou vlastnost `Movie` třídy bude mapovat na sloupec v tabulce.

Ve stejném souboru přidejte následující `MovieDBContext` třídy:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` Třída reprezentuje kontext databáze filmů Entity Framework, která zpracovává načítání, ukládání a aktualizaci `Movie` třídy instancí v databázi. `MovieDBContext` Je odvozen od `DbContext` základní třída poskytované rozhraním Entity Framework. Další informace o `DbContext` a `DbSet`, naleznete v tématu [vylepšení produktivity pro Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).

Pokud chcete mít možnost odkazovat `DbContext` a `DbSet`, budete muset přidat následující `using` příkazu v horní části souboru:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Kompletní *Movie.cs* souboru je uveden níže.

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>Vytvoření připojovacího řetězce a práce s SQL serverem Compact

`MovieDBContext` Třídy, které jste vytvořili zpracovává úlohu s připojením k databázi a mapování `Movie` objekty se záznamy v databázi. Jednu otázku, kterou můžete pokládat, je, jak určit databázi, kterou se připojí k. Můžete to udělat tak, že přidáte informace o připojení v *Web.config* souboru aplikace.

Otevřete kořenový adresář aplikace *Web.config* souboru. (Ne *Web.config* ve *zobrazení* složky.) Na následujícím obrázku zobrazit obojí *Web.config* soubory; otevřít *Web.config* soubor v kruhu červeně.

![](adding-a-model/_static/image4.png)

### 

Přidejte následující připojovací řetězec do `<connectionStrings>` prvek *Web.config* souboru.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

Následující příklad ukazuje část *Web.config* soubor se přidat nový připojovací řetězec:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

Malé množství kódu a XML je všechno, co potřebujete k zápisu představují a ukládat data o filmech v databázi.

V dalším kroku vytvoříte novou `MoviesController` třídu, která vám pomůže se zobrazí data o filmech a umožní uživatelům vytvářet nové video výpisy.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md)
> [další](accessing-your-models-data-from-a-controller.md)
