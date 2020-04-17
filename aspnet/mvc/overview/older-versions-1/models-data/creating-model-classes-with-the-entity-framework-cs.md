---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Vytváření modelových tříd pomocí entity Framework (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto kurzu se dozvíte, jak používat ASP.NET MVC s Microsoft Entity Framework. Dozvíte se, jak pomocí Průvodce entitou vytvořit ADO.NET entity Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542661"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Vytvoření tříd modelu v sadě Entity Framework (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> V tomto kurzu se dozvíte, jak používat ASP.NET MVC s Microsoft Entity Framework. Dozvíte se, jak pomocí Průvodce entitami vytvořit ADO.NET datového modelu entity. V průběhu tohoto kurzu vytvoříme webovou aplikaci, která ukazuje, jak vybrat, vložit, aktualizovat a odstranit data databáze pomocí entity frameworku.

Cílem tohoto kurzu je vysvětlit, jak můžete vytvořit třídy přístupu k datům pomocí microsoft entity framework při vytváření ASP.NET aplikace MVC. Tento kurz nepředpokládá žádné předchozí znalosti rozhraní Microsoft Entity Framework. Na konci tohoto kurzu pochopíte, jak pomocí entity Framework vybrat, vložit, aktualizovat a odstranit záznamy databáze.

Microsoft Entity Framework je nástroj pro relační mapování objektů (O/RM), který umožňuje automaticky generovat vrstvu přístupu k datům z databáze. Entity Framework umožňuje vyhnout se únavné práci vytváření tříd přístupu k datům ručně.

Abychom ilustrovali, jak můžete použít microsoft entity framework s ASP.NET MVC, vytvoříme jednoduchou ukázkovou aplikaci. Vytvoříme aplikaci Movie Database, která vám umožní zobrazit a upravit záznamy filmové databáze.

Tento kurz předpokládá, že máte Visual Studio 2008 nebo Visual Web Developer 2008 s aktualizací Service Pack 1. K použití entity Frameworku potřebujete aktualizaci Service Pack 1. Aktualizaci Visual Studio 2008 Service Pack 1 nebo Visual Web Developer s aktualizací Service Pack 1 si můžete stáhnout z následující adresy:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> Neexistuje žádné základní spojení mezi ASP.NET MVC a Microsoft Entity Framework. Existuje několik alternativ k entity framework, který můžete použít s ASP.NET MVC. Můžete například vytvořit třídy modelu MVC pomocí jiných nástrojů O/RM, jako je Microsoft LINQ na SQL, NHibernate nebo SubSonic.

## <a name="creating-the-movie-sample-database"></a>Vytvoření ukázkové databáze filmu

Aplikace Movie Database používá databázovou tabulku s názvem Filmy, která obsahuje následující sloupce:

| Název sloupce | Typ dat | Povolit nulls? | Je primární klíč? |
| --- | --- | --- | --- |
| ID | int | False | True |
| Nadpis | nvarchar(100) | False | False |
| Ředitel | nvarchar(100) | False | False |

Tuto tabulku můžete přidat do projektu ASP.NET MVC následujícím postupem:

1. Klikněte pravým\_tlačítkem myši na složku Data aplikace v okně Průzkumník řešení a vyberte možnost nabídky **Přidat, nová položka.**
2. V dialogovém okně **Přidat novou položku** vyberte **databázi serveru SQL Server**, pojmenujte databázi název MoviesDB.mdf a klepněte na tlačítko **Přidat.**
3. Poklepáním na soubor MoviesDB.mdf otevřete okno Průzkumník serveru/Průzkumník databáze.
4. Rozbalte databázové připojení MoviesDB.mdf, klepněte pravým tlačítkem myši na složku Tabulky a vyberte možnost nabídky **Přidat novou tabulku**.
5. V Návrháři tabulek přidejte sloupce Id, Title a Director.
6. Kliknutím na tlačítko **Uložit** (obsahuje ikonu diskety) uložte novou tabulku s názvem Filmy.

Po vytvoření databázové tabulky Filmy byste měli do tabulky přidat několik ukázkových dat. Klepněte pravým tlačítkem myši na tabulku Filmy a vyberte možnost nabídky **Zobrazit data tabulky**. Do mřížky, která se zobrazí, můžete zadat falešná data o filmu.

## <a name="creating-the-adonet-entity-data-model"></a>Vytvoření datového modelu entity ADO.NET

Chcete-li použít entity Framework, musíte vytvořit datový model entity. Můžete využít *Průvodce modelem datového modelu entity* sady Visual Studio k automatickému generování datového modelu entity z databáze.

Postupujte následovně:

1. Klepněte pravým tlačítkem myši na složku Modely v okně Průzkumník řešení a vyberte možnost nabídky **Přidat, novou položku**.
2. V dialogovém okně **Přidat novou položku** vyberte kategorii Data (viz obrázek 1).
3. Vyberte šablonu **ADO.NET datového modelu entity,** přiřazujte datovému modelu entity název MoviesDBModel.edmx a klepněte na tlačítko **Přidat.** Kliknutím na tlačítko **Přidat** se spustí Průvodce datovým modelem.
4. V kroku **Zvolit obsah modelu** zvolte **volbu Generovat z databáze** a klepněte na tlačítko **Další** (viz obrázek 2).
5. V kroku **Zvolit datové připojení** vyberte databázové připojení MoviesDB.mdf, zadejte název nastavení připojení entit MoviesDBEntities a klepněte na tlačítko **Další** (viz obrázek 3).
6. V kroku **Zvolit databázové objekty** vyberte databázovou tabulku Film a klepněte na tlačítko **Dokončit** (viz obrázek 4).

Po dokončení těchto kroků se otevře návrhář ADO.NET entity data modelu (Návrhář entit).

**Obrázek 1 – Vytvoření nového datového modelu entity**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**Obrázek 2 – Zvolte krok obsahu modelu**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**Obrázek 3 – Vyberte si datové připojení**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**Obrázek 4 – Výběr databázových objektů**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>Úprava datového modelu ADO.NET entity

Po vytvoření datového modelu entity můžete model upravit využitím návrháře entit (viz obrázek 5). Návrhář entit můžete kdykoli otevřít poklepáním na soubor MoviesDBModel.edmx obsažený ve složce Modely v okně Průzkumník řešení.

**Obrázek 5 – návrhář ADO.NET entity modelu dat**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

Pomocí Návrháře entit můžete například změnit názvy tříd, které generuje Průvodce daty modelu entity. Průvodce vytvořil novou třídu přístupu k datům s názvem Filmy. Jinými slovy, Průvodce dal třídě stejný název jako tabulka databáze. Vzhledem k tomu, že tuto třídu použijeme k reprezentaci konkrétní instance filmu, měli bychom třídu přejmenovat z filmy na film.

Pokud chcete třídu entity přejmenovat, můžete poklepat na název třídy v Návrháři entit a zadat nový název (viz obrázek 6). Případně můžete změnit název entity v okně Vlastnosti po výběru entity v Návrháři entit.

**Obrázek 6 – Změna názvu entity**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

Nezapomeňte datový model entity uložit po provedení změny kliknutím na tlačítko Uložit (ikona diskety). Na pozadí návrhářentgeneruje sadu c# tříd. Tyto třídy můžete zobrazit otevřením souboru MoviesDBModel.Designer.cs z okna Průzkumníka řešení.

Neupravujte kód v souboru Designer.cs, protože změny budou přepsány při příštím použití Návrháře entit. Pokud chcete rozšířit funkce tříd entit definovaných v souboru Designer.cs pak můžete vytvořit *částečné třídy* v samostatných souborech.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Výběr záznamů databáze pomocí entity frameworku

Začněme vytvářet aplikaci Movie Database vytvořením stránky, která zobrazuje seznam filmových záznamů. Domácí kontroler v výpisu 1 zpřístupňuje akci s názvem Index(). Akce Index() vrátí všechny filmové záznamy z tabulky databáze Film s využitím entity frameworku.

**Výpis 1 – Řadiče\HomeController.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

Všimněte si, že řadič v výpisu 1 obsahuje konstruktor. Konstruktor inicializuje pole na úrovni \_třídy s názvem db. Pole \_db představuje databázové entity generované rozhraním Microsoft Entity Framework. Pole \_db je instancí třídy MoviesDBEntities, která byla generována Návrhářem entit.

Chcete-li použít třídu MoviesDBEntities v řadiči Home, musíte importovat obor názvů MovieEntityApp.Models (*MVCProjectName*. modely).

Pole \_db se používá v rámci akce Index() k načtení záznamů z databázové tabulky Filmy. Výraz \_db. MovieSet představuje všechny záznamy z tabulky databáze Filmy. Metoda ToList() se používá k převodu sady filmů na obecnou&lt;&gt;kolekci objektů Movie (List Movie ).

Filmové záznamy jsou načteny pomocí LINQ entity. Akce Index() v výpisu 1 používá *syntaxi metody* LINQ k načtení sady databázových záznamů. Pokud chcete, můžete místo toho použít *syntaxi dotazu* LINQ. Následující dva příkazy udělat totéž:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

Použijte podle toho, která syntaxe LINQ – syntaxe metody nebo syntaxe dotazu – která je pro vás nejintuitivnější. Neexistuje žádný rozdíl ve výkonu mezi těmito dvěma přístupy - jediný rozdíl je styl.

Zobrazení v seznamu 2 se používá k zobrazení filmových záznamů.

**Výpis 2 – Zobrazení\Domů\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

Zobrazení v seznamu 2 obsahuje **foreach** smyčky, která iterates prostřednictvím každého záznamu filmu a zobrazí hodnoty názvu filmu a režie vlastnosti. Všimněte si, že se vedle každého záznamu zobrazí odkaz Upravit a odstranit. V dolní části zobrazení se navíc zobrazí odkaz Přidat film (viz obrázek 7).

**Obrázek 7 – Zobrazení indexu**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

Zobrazení Rejstřík je *zadané zobrazení*. Zobrazení rejstříku &lt;obsahuje direktivu %@ Page %&gt; s atributem *Inherits,* který přetypuje&lt;vlastnost Model na kolekci objektů typu Velký typ (Vyvěšený film).

## <a name="inserting-database-records-with-the-entity-framework"></a>Vkládání databázových záznamů pomocí entity frameworku

Pomocí entity frameworku můžete usnadnit vkládání nových záznamů do databázové tabulky. Výpis 3 obsahuje dvě nové akce přidané do třídy Domácí kontrolor, které můžete použít k vložení nových záznamů do tabulky Databáze filmu.

**Výpis 3 – Controllers\HomeController.cs (Přidat metody)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

První add() akce jednoduše vrátí zobrazení. Zobrazení obsahuje formulář pro přidání nového záznamu filmové databáze (viz obrázek 8). Při odeslání formuláře je vyvolána druhá akce Add().

Všimněte si, že druhá akce Add() je dekorována atributem AcceptVerbs. Tuto akci lze vyvolat pouze při provádění operace HTTP POST. Jinými slovy, tuto akci lze vyvolat pouze při zaúčtování formuláře HTML.

Druhá akce Add() vytvoří novou instanci třídy Entity Framework Movie pomocí metody ASP.NET MVC TryUpdateModel(). Metoda TryUpdateModel() přebírá pole v kolekci formulářů předaná metodě Add() a přiřazuje hodnoty těchto polí formuláře HTML třídě Movie.

Při použití entity framework, musíte zadat "bílý seznam" vlastností při použití TryUpdateModel nebo UpdateModel metody aktualizovat vlastnosti třídy entity.

V dalším kroku add() akce provede některé jednoduché ověření formuláře. Akce ověří, zda vlastnosti Title i Director mají hodnoty. Pokud dojde k chybě ověření, je do stavu ModelState přidána chybová zpráva ověření.

Pokud nejsou žádné chyby ověření pak nový záznam filmu je přidán do tabulky databáze Filmy pomocí entity frameworku. Nový záznam je přidán do databáze s následujícími dvěma řádky kódu:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

První řádek kódu přidá novou entitu Movie do sady filmů sledovaných rozhraním Entity Framework. Druhý řádek kódu ukládá všechny změny, které byly provedeny ve filmech sledovaných zpět do podkladové databáze.

**Obrázek 8 – Zobrazení sčítání**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Aktualizace záznamů databáze pomocí entity Framework

Můžete postupovat téměř stejným způsobem upravit záznam databáze s entity framework jako přístup, který jsme právě následovali vložit nový záznam databáze. Výpis 4 obsahuje dvě nové akce řadiče s názvem Edit(). První akce Edit() vrátí formulář HTML pro úpravy záznamu vydědění. Druhá akce Edit() se pokusí aktualizovat databázi.

**Výpis 4 – Controllers\HomeController.cs (Metody úprav)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

Druhá akce Edit() začíná načtením záznamu filmu z databáze, která odpovídá ID upravovaného filmu. Následující příkaz LINQ entity uchopí první záznam databáze, který odpovídá konkrétnímu ID:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

Dále tryUpdateModel() metoda se používá k přiřazení hodnoty polí formuláře HTML vlastnosti entity filmu. Všimněte si, že je zadán bílý seznam k určení přesné vlastnosti aktualizovat.

Dále se provádí některé jednoduché ověření k ověření, že název filmu a ředitel vlastnosti mají hodnoty. Pokud některá vlastnost chybí hodnota, pak je přidána chybová zpráva ověření modelstate a ModelState.IsValid vrátí hodnotu false.

Nakonec pokud neexistují žádné chyby ověření, podkladová tabulka databáze Filmy je aktualizována všemi změnami voláním metody SaveChanges().

Při úpravách záznamů databáze je třeba předat ID upravovaného záznamu akci kontroleru, která provádí aktualizaci databáze. V opačném případě akce kontroleru nebude vědět, který záznam aktualizovat v podkladové databázi. Zobrazení Upravit obsažené v seznamu 5 obsahuje skryté pole formuláře, které představuje ID upravovaného záznamu databáze.

**Výpis 5 – Zobrazení\Domů\Upravit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Odstranění databázových záznamů pomocí entity Frameworku

Operace konečné databáze, které musíme řešit v tomto kurzu, je odstranění záznamů databáze. Pomocí akce kontroléru v seznamu 6 můžete odstranit určitý záznam databáze.

**Výpis 6 -- \Controllers\HomeController.cs (Akce Odstranit)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Akce Delete() nejprve načte entitu Film, která odpovídá ID předané akci. Dále je film odstraněn z databáze voláním metody DeleteObject() následované metodou SaveChanges(). Nakonec je uživatel přesměrován zpět do zobrazení index.

## <a name="summary"></a>Souhrn

Účelem tohoto kurzu bylo ukázat, jak můžete vytvářet webové aplikace řízené databází využitím ASP.NET MVC a Microsoft Entity Framework. Zjistili jste, jak vytvořit aplikaci, která umožňuje vybrat, vložit, aktualizovat a odstranit databázové záznamy.

Nejprve jsme probrali, jak můžete použít Průvodce datovým modelem entity ke generování datového modelu entity z aplikace Visual Studio. Dále se dozvíte, jak pomocí LINQ entity načíst sadu databázových záznamů z tabulky databáze. Nakonec jsme použili entity framework vložit, aktualizovat a odstranit záznamy databáze.

> [!div class="step-by-step"]
> [Další](creating-model-classes-with-linq-to-sql-cs.md)
