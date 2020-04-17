---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: Zobrazení tabulky databázových dat (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto tutoriálu předvádím dvě metody zobrazení sady databázových záznamů. I zobrazit dvě metody formátování sadu databázových záznamů v HTML ta ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541894"
---
# <a name="displaying-a-table-of-database-data-vb"></a>Zobrazení tabulky databázových dat (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> V tomto tutoriálu předvádím dvě metody zobrazení sady databázových záznamů. Zobrazil(a) jsem dvě metody formátování sady databázových záznamů v tabulce HTML. Nejprve vám ukážu, jak můžete naformátovat databázové záznamy přímo v rámci zobrazení. Dále jsem ukázat, jak můžete využít částečné při formátování databázových záznamů.

Cílem tohoto kurzu je vysvětlit, jak můžete zobrazit tabulku HTML databázových dat v ASP.NET aplikace MVC. Nejprve se dozvíte, jak pomocí nástrojů generování uživatelského a uživatelského zařízení zahrnuté v sadě Visual Studio generovat zobrazení, které automaticky zobrazuje sadu záznamů. Dále se dozvíte, jak použít částečné jako šablonu při formátování záznamů databáze.

## <a name="create-the-model-classes"></a>Vytvoření tříd modelu

Zobrazíme sadu záznamů z tabulky databáze Filmy. Databázová tabulka Filmy obsahuje následující sloupce:

<a id="0.4_table01"></a>

| **Název sloupce** | **Typ dat** | **Povolit hodnoty Null** |
| --- | --- | --- |
| ID | Int | False |
| Nadpis | Nvarchar(200) | False |
| Ředitel | NVarchar(50) | False |
| Datum zveřejnění | DateTime | False |

Aby bylo možné reprezentovat tabulky Filmy v naší ASP.NET aplikace MVC, musíme vytvořit třídu modelu. V tomto kurzu používáme Microsoft Entity Framework k vytvoření našich tříd modelu.

> [!NOTE] 
> 
> V tomto kurzu používáme Microsoft Entity Framework. Je však důležité si uvědomit, že můžete použít celou řadu různých technologií pro interakci s databází z ASP.NET aplikace MVC, včetně LINQ na SQL, NHibernate nebo ADO.NET.

Průvodce datovým modelem entity spusťte následujícím způsobem:

1. Klepněte pravým tlačítkem myši na složku Modely v okně Průzkumník řešení a vyberte možnost nabídky **Přidat, Novou položku**.
2. Vyberte kategorii **Data** a vyberte šablonu **ADO.NET datového modelu entity.**
3. Dejte svému datovému modelu název *MoviesDBModel.edmx* a klikněte na tlačítko **Přidat.**

Po klepnutí na tlačítko Přidat se zobrazí Průvodce datovým modelem entity (viz obrázek 1). Průvodce dokončujte následujícím postupem:

1. V kroku **Zvolit obsah modelu** vyberte volbu Generovat z **databáze.**
2. V kroku **Zvolit datové připojení** použijte datové připojení *MoviesDB.mdf* a název *MoviesDBEntities* pro nastavení připojení. Klikněte na tlačítko **Další.**
3. V kroku **Zvolit databázové objekty** rozbalte uzel Tabulky a vyberte tabulku Filmy. Zadejte *modely* oboru názvů a klepněte na tlačítko **Dokončit.**

[![Vytváření tříd LINQ na SQL](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**Obrázek 01**: Vytvoření tříd LINQ na SQL[(Klepnutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image2.png)

Po dokončení Průvodce datovým modelem entity se otevře Návrhář modelu dat entity. Návrhář by měl zobrazit entitu Filmy (viz obrázek 2).

[![Návrhář datového modelu entity](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**Obrázek 02**: Návrhář datového modelu entity[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image4.png)

Než budeme pokračovat, musíme udělat jednu změnu. Průvodce daty entit generuje třídu modelu s názvem *Filmy,* která představuje databázovou tabulku Filmy. Vzhledem k tomu, že budeme používat Filmy třídy představují konkrétní film, musíme upravit název třídy *být film* místo *filmy* (jednotné číslo spíše než množné číslo).

Poklepejte na název třídy na povrchu návrháře a změňte název třídy z Filmy na Film. Po provedení této změny vygenerujte třídu Movie klepnutím na tlačítko **Uložit** (ikona diskety).

## <a name="create-the-movies-controller"></a>Vytvoření ovladače pro filmy

Teď, když máme způsob, jak reprezentovat naše databázové záznamy, můžeme vytvořit řadič, který vrací sbírku filmů. V okně Průzkumník řešení sady Visual Studio klepněte pravým tlačítkem myši na složku Řadiče a vyberte možnost nabídky **Přidat, Řadič** (viz obrázek 3).

[![Nabídka Přidat ovladač](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**Obrázek 03**: Nabídka Přidat ovladač[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image6.png)

Po zobrazení dialogového okna **Přidat řadič** zadejte název řadiče MovieController (viz obrázek 4). Kliknutím na tlačítko **Přidat** přidejte nový ovladač.

[![Dialogové okno Přidat řadič](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**Obrázek 04**: Dialogové okno Přidat ovladač([Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image8.png)

Musíme upravit akci Index() vystavenou řadičem filmu tak, aby vrátil sadu databázových záznamů. Upravte řadič tak, aby vypadal jako řadič v výpisu 1.

**Výpis 1 – Řadiče\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

V výpisu 1, MoviesDBEntities třída se používá k reprezentaci databáze MoviesDB. Entity *výrazu. MovieSet.ToList()* vrátí sadu všech filmů z tabulky databáze Filmy.

## <a name="create-the-view"></a>Vytvoření zobrazení

Nejjednodušší způsob, jak zobrazit sadu databázových záznamů v tabulce HTML, je využít možnosti uživatelského prostředí poskytovaného sadou Visual Studio.

Vytvořte si aplikaci výběrem možnosti nabídky **Sestavení, Sestavení řešení**. Před otevřením dialogového okna **Přidat zobrazení** je nutné vytvořit aplikaci, jinak se vaše třídy dat v dialogovém okně nezobrazí.

Klikněte pravým tlačítkem myši na akci Index() a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 5).

[![Přidání zobrazení](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**Obrázek 05**: Přidání zobrazení[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image10.png)

V dialogovém okně **Přidat zobrazení** zaškrtněte políčko Vytvořit **zobrazení silného typu**. Vyberte třídu Film jako **třídu dat zobrazení**. Jako obsah **zobrazení** vyberte *Seznam* (viz obrázek 6). Výběrem těchto možností se vygeneruje zobrazení silného typu, které zobrazí seznam filmů.

[![Dialogové okno Přidat zobrazení](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**Obrázek 06**: Dialogové okno Přidat zobrazení([Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image12.png)

Po klepnutí na tlačítko **Přidat** se automaticky vygeneruje zobrazení v seznamu 2. Toto zobrazení obsahuje kód potřebný k iterátu prostřednictvím kolekce filmů a zobrazení jednotlivých vlastností filmu.

**Výpis 2 – Zobrazení\Film\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

Aplikaci můžete spustit výběrem možnosti nabídky **Ladění, Spustit ladění** (nebo stisknutím klávesy F5). Spuštění aplikace spustí aplikaci Internet Explorer. Pokud přejdete na adresu URL /Movie, zobrazí se stránka na obrázku 7.

[![Tabulka filmů](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**Obrázek 07**: Tabulka[filmů(Klikněte pro zobrazení obrázku v plné velikosti)](displaying-a-table-of-database-data-vb/_static/image14.png)

Pokud se vám nelíbí nic o vzhledu mřížky databázových záznamů na obrázku 7, pak můžete jednoduše upravit zobrazení indexu. Můžete například změnit hlavičku *DateReleased* na *Datum vydání* úpravou zobrazení rejstříku.

## <a name="create-a-template-with-a-partial"></a>Vytvoření šablony s částečným

Když se zobrazení příliš zkomplikuje, je vhodné začít rozdělit zobrazení na částečné. Použití částečných částek usnadňuje pochopení a údržbu zobrazení. Vytvoříme částečný, který můžeme použít jako šablonu pro formátování každého z záznamů filmové databáze.

Chcete-li vytvořit částečné, postupujte takto:

1. Klepněte pravým tlačítkem myši na složku Zobrazení\Film a vyberte možnost nabídky **Přidat zobrazení**.
2. Zaškrtněte políčko *Vytvořit částečné zobrazení (.ascx).*
3. Pojmenujte částečnou *movietemplate*.
4. Zaškrtněte políčko **Vytvořit zobrazení silného typu**.
5. Jako *třídu dat zobrazení*vyberte Vyvěšení .
6. Jako obsah *zobrazení*vyberte Možnost Prázdné .
7. Kliknutím na tlačítko **Přidat** přidáte částečné část projektu.

Po dokončení těchto kroků upravte šablonu MovieTemplate tak, aby vypadala jako Výpis 3.

**Výpis 3 – Zobrazení\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

Částečné v výpisu 3 obsahuje šablonu pro jeden řádek záznamů.

Upravené zobrazení indexu v seznamu 4 používá částečné movietemplate.

**Výpis 4 – Zobrazení\Film\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

Zobrazení v seznamu 4 obsahuje pro každou smyčku, která itetuje přes všechny filmy. Pro každý film se k formátování filmu používá šablona MovieTemplate. MovieTemplate je vykreslen voláním RenderPartial() pomocné metody.

Upravené zobrazení indexu vykreslí stejnou tabulku HTML databázových záznamů. Pohled byl však značně zjednodušen.

RenderPartial() Metoda se liší od většiny jiných pomocných metod, protože nevrátí řetězec. Proto je nutné volat RenderPartial() &lt;metoda pomocí % Html.RenderPartial() %&gt; místo &lt;%= Html.RenderPartial() %&gt;.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo vysvětlit, jak lze zobrazit sadu databázových záznamů v tabulce HTML. Nejprve jste se naučili, jak vrátit sadu záznamů databáze z akce kontroleru s využitím rozhraní Microsoft Entity Framework. Dále jste se naučili používat generování uživatelského přilnavého zařízení sady Visual Studio ke generování zobrazení, které automaticky zobrazuje kolekci položek. Nakonec jste se naučili, jak zjednodušit zobrazení využitím částečné. Naučili jste se používat částečné jako šablonu, takže můžete formátovat každý záznam databáze.

> [!div class="step-by-step"]
> [Předchozí](creating-model-classes-with-linq-to-sql-vb.md)
> [další](performing-simple-validation-vb.md)
