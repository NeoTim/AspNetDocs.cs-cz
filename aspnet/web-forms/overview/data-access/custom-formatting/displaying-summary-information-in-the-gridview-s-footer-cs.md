---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: Zobrazení souhrnných informací v zápatí prvku GridView (C#) | Dokumentace Microsoftu
author: rick-anderson
description: Zobrazí souhrnné informace v dolní části sestavy v souhrnu řádku se často. Ovládací prvek GridView může obsahovat řádek zápatí, do jehož buněk můžeme žádosti o přijetí změn...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 0bc3127974341a65fb5f38ac0a974782099fffce
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59385914"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>Zobrazení souhrnných informací v zápatí prvku GridView (C#)

podle [Scott Meisnerová](https://twitter.com/ScottOnWriting)

[Stáhněte si ukázkovou aplikaci](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) nebo [stahovat PDF](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> Zobrazí souhrnné informace v dolní části sestavy v souhrnu řádku se často. Řádek zápatí, do jehož buněk můžete programově vložíme agregovaná data, která může zahrnovat ovládacím prvku GridView. V tomto kurzu uvidíme, jak zobrazit agregovaná data, která v tomto řádku zápatí.


## <a name="introduction"></a>Úvod

Kromě toho každá ceny produktů, jednotky v zásobách, jednotky v objednávce a minimální počet, může uživatel také mohla zajímat souhrnné informace, jako je například průměrná cena, celkový počet jednotek v zásobách a tak dále. Zobrazí souhrnné informace v dolní části sestavy v souhrnu řádku se často. Řádek zápatí, do jehož buněk můžete programově vložíme agregovaná data, která může zahrnovat ovládacím prvku GridView.

Tento úkol představuje nám s tři problémy:

1. Konfigurace k zobrazení jeho řádku zápatí prvku GridView.
2. Určení souhrnná data; To znamená jak můžeme následujícím způsobem vypočítat průměrná cena nebo celkový počet jednotek v zásobách?
3. Vkládání souhrnných dat do odpovídající buňky řádku zápatí

V tomto kurzu uvidíme, jak vyřešit tyto problémy. Konkrétně vytvoříme stránku, která obsahuje seznam kategorií v rozevíracím seznamu s vybranou kategorii produkty portále GridView. GridView bude obsahovat zápatí řádek, který ukazuje průměrnou cenu a celkový počet jednotek v zásobách a na pořadí produktů v dané kategorii.


[![Zobrazí se souhrnné informace v řádku zápatí prvku GridView.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**Obrázek 1**: Zobrazí se souhrnné informace v řádku zápatí prvku GridView ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))


Tento kurz s jeho kategorie produktů záznamů master/detail rozhraní staví na koncepty uvedenými v předchozím [filtrování záznamů Master/Detail s DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) kurzu. Pokud už máte ještě prostřednictvím starší kurz, proveďte tak před spuštěním tohoto objektu.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>Krok 1: Přidání kategorie DropDownList a produkty GridView

Než si týkající se přidávání souhrnné informace pro zápatí prvku GridView, nejprve jednoduše Vytvořme záznamů master/detail sestavy. Když jsme dokončili tento první krok, podíváme se na tom, jak zahrnout souhrnná data.

Začněte otevřením `SummaryDataInFooter.aspx` stránku `CustomFormatting` složky. Přidejte ovládací prvek DropDownList a nastavte jeho `ID` k `Categories`. V dalším kroku klikněte na odkaz zvolit zdroj dat z inteligentních značek DropDownList a optimalizované pro přidání nového prvku ObjectDataSource s názvem `CategoriesDataSource` , která vyvolává `CategoriesBLL` třídy `GetCategories()` metody.


[![Přidat nový prvek ObjectDataSource s názvem CategoriesDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**Obrázek 2**: Přidat nový prvek ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))


[![Mít ObjectDataSource vyvolat metodu GetCategories() CategoriesBLL třídy](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**Obrázek 3**: Mít ObjectDataSource vyvolat `CategoriesBLL` třídy `GetCategories()` – metoda ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))


Po dokončení konfigurace ObjectDataSource, Průvodce vrátí nám konfigurace zdroje dat DropDownList by se mělo zobrazit průvodce, ze které potřebujeme zadat jakou hodnotu pole data a která z nich by měl odpovídat hodnotě DropDownList.`ListItem` s. Máte `CategoryName` pole zobrazit a použít `CategoryID` jako hodnotu.


[![Použít CategoryName a CategoryID pole jako Text a hodnoty pro položky ListItems, v uvedeném pořadí](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**Obrázek 4**: Použití `CategoryName` a `CategoryID` polí jako `Text` a `Value` pro `ListItem` s, respektive ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))


V tuto chvíli máme, aby DropDownList (`Categories`), který obsahuje seznam kategorií v systému. Teď potřebujeme přidat prvku GridView, který obsahuje seznam těchto produktů, které patří do vybrané kategorie. Před tím, než, i když, věnujte chvíli zaškrtněte políčko Povolit vlastnost AutoPostBack v inteligentních značek DropDownList. Jak je popsáno v *filtrování záznamů Master/Detail s DropDownList* výukový program, tak, že nastavíte DropDownList `AutoPostBack` vlastnost `true` stránky bude účtován zpět pokaždé, když se změní hodnota DropDownList. To způsobí, že GridView se aktualizuje, zobrazuje tyto produkty pro nově vybranou kategorii. Pokud `AutoPostBack` je nastavena na `false` (výchozí), změna kategorii nebude vyvolávají zpětné odeslání a proto nebude aktualizovat uvedené produkty.


[![Zaškrtněte políčko Povolit vlastnost AutoPostBack v inteligentních značek DropDownList](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**Obrázek 5**: Zaškrtněte políčko Povolit vlastnost AutoPostBack v inteligentních značek DropDownList ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png))


Přidání ovládacího prvku GridView na stránku mohla zobrazit produkty pro vybrané kategorie. Nastavte prvku GridView `ID` k `ProductsInCategory` a jeho vazbu na nového prvku ObjectDataSource s názvem `ProductsInCategoryDataSource`.


[![Přidat nový prvek ObjectDataSource s názvem ProductsInCategoryDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**Obrázek 6**: Přidat nový prvek ObjectDataSource s názvem `ProductsInCategoryDataSource` ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))


Nakonfigurujte prvku ObjectDataSource tak, aby vyvolá `ProductsBLL` třídy `GetProductsByCategoryID(categoryID)` metody.


[![Mít ObjectDataSource Invoke GetProductsByCategoryID(categoryID) – metoda](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**Obrázek 7**: Mít ObjectDataSource vyvolat `GetProductsByCategoryID(categoryID)` – metoda ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))


Protože `GetProductsByCategoryID(categoryID)` metoda přijímá vstupní parametr v posledním kroku průvodce můžeme určit příčiny hodnotu parametru. Chcete-li zobrazit tyto produkty z vybrané kategorie, mít parametr získaných z `Categories` DropDownList.


[![Získání ID kategorie hodnota parametru z DropDownList vybrané kategorie](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**Obrázek 8**: Získejte *`categoryID`* hodnoty parametru z vybrané kategorie DropDownList ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))


Po dokončení Průvodce prvku GridView, bude mít vlastnost BoundField pro jednotlivé vlastnosti produktu. Pojďme vyčištění tyto BoundFields takže jen `ProductName`, `UnitPrice`, `UnitsInStock`, a `UnitsOnOrder` BoundFields jsou zobrazeny. Nebojte se přidat žádné nastavení na úrovni pole zbývající BoundFields (například formátování `UnitPrice` jako měna). Po provedení těchto změn, deklarativní prvku GridView by měl vypadat nějak takto:


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

V tuto chvíli máme plně funkční sestavu záznamů master/detail, který zobrazuje název, cena za jednotku, jednotek v zásobách a jednotky v pořadí pro tyto produkty, které patří do vybrané kategorie.


[![Získání ID kategorie hodnota parametru z DropDownList vybrané kategorie](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**Obrázek 9**: Získejte *`categoryID`* hodnoty parametru z vybrané kategorie DropDownList ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))


## <a name="step-2-displaying-a-footer-in-the-gridview"></a>Krok 2: Zobrazování zápatí prvku GridView.

Ovládací prvek GridView mohl zobrazit řádek záhlaví a zápatí. Tyto řádky jsou zobrazeny v závislosti na hodnoty `ShowHeader` a `ShowFooter` vlastnosti, v uvedeném pořadí, s `ShowHeader` jako výchozí se použije `true` a `ShowFooter` k `false`. Chcete-li zahrnout zápatí prvku GridView jednoduše nastavte jeho `ShowFooter` vlastnost `true`.


[![Nastavit aplikaci prvku GridView ShowFooter vlastnost na hodnotu true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**Obrázek 10**: Nastavte prvku GridView `ShowFooter` vlastnost `true` ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))


Zápatí řádek má buňky pro každé pole definované v prvku GridView.; tyto buňky jsou však ve výchozím nastavení prázdné. Chcete-li zobrazit náš postup v prohlížeči chvíli trvat. S `ShowFooter` nyní nastavenou na `true`, obsahuje na řádek prázdný zápatí prvku GridView.


[![GridView nyní obsahuje řádek zápatí](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**Obrázek 11**: Teď obsahuje řádek zápatí prvku GridView ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))


Řádek zápatí v obrázek 11 nebude odlišit, je na něm bílé pozadí. Vytvoříme `FooterStyle` třídy šablony stylů CSS v `Styles.css` , který určuje tmavě červená na pozadí a potom nakonfigurujte `GridView.skin` soubor vzhledu v `DataWebControls` motiv k přiřazení této třídy šablony stylů CSS do prvku GridView `FooterStyle`společnosti `CssClass` vlastnost. Pokud je potřeba osvěžit skinů v šablonách a motivů, vraťte se do [zobrazení dat se prvku ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) kurzu.

Začněte přidáním následující třídu šablony stylů CSS do `Styles.css`:


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

`FooterStyle` Třídu šablony stylů CSS je podobné jako u styl, který `HeaderStyle` třídy, i když `HeaderStyle`na barvu pozadí je subtlety tmavší a jeho textu se zobrazí tučným písmem. Kromě toho text v zápatí jsou zarovnána doprava, že je na střed textu záhlaví.

Dále zápatí prvku GridView každý přidružit tuto třídu šablony stylů CSS, otevřete `GridView.skin` ve `DataWebControls` motivu a nastavte `FooterStyle`společnosti `CssClass` vlastnost. Po přidání tohoto souboru značek by měl vypadat jako:


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

Podle níže ukazuje snímek obrazovky, díky této změně v zápatí je uvedené informace jasně vyniknout.


[![Teď má barvu pozadí načervenalé řádek zápatí prvku GridView.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**Obrázek 12**: Teď má načervenalé barva pozadí řádku zápatí prvku GridView ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))


## <a name="step-3-computing-the-summary-data"></a>Krok 3: Výpočetní souhrnná Data

Zobrazit zápatí prvku GridView je další výzvy směřující nám jak compute souhrnná data. Existují dva způsoby, jak vypočítat toto agregované informace:

1. Pomocí dotazu SQL jsme setkat se k databázi pro výpočet souhrnná data pro určitou kategorii Další dotaz. Zahrnuje celou řadu agregační funkce spolu s SQL `GROUP BY` klauzule zadejte požadovaná data, přes který by měl shrnout data. Následující dotaz SQL by vrácení potřebné informace:  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    Samozřejmě není vhodné k vydávání tento dotaz přímo z `SummaryDataInFooter.aspx` stránky, ale spíše vytvořením metody v `ProductsTableAdapter` a `ProductsBLL`.
2. COMPUTE tyto informace, jak ho přidáte do prvku GridView. jak je popsáno v [vlastní formátování založené na Data](custom-formatting-based-upon-data-cs.md) kurzu, prvku GridView `RowDataBound` obslužné rutiny události spustí jednou pro každý řádek se přidávají do ovládacího prvku GridView, po jeho byla datové vazby. Vytvořením obslužnou rutinu události pro tuto událost, abychom průběžný součet hodnoty chceme agregovat. Za poslední řádek dat byla svázána se GridView máme součty a informace potřebné k výpočtu průměru.

Můžu druhým přístupem obvykle používají postoupí ho uloží do databáze a úsilí potřebné k implementaci funkcionality souhrnu v vrstvy přístupu k datům a vrstvu obchodní logiky, ale bude stačit kterýkoliv přístup. Pro účely tohoto kurzu můžeme použít druhou možnost a mějte přehled o průběžný součet míry pomocí `RowDataBound` obslužné rutiny události.

Vytvoření `RowDataBound` obslužnou rutinu události pro prvek GridView výběrem prvku GridView v návrháři, kliknutím na ikonu blesku v okně Vlastnosti a dvojitým kliknutím `RowDataBound` událostí. Tím se vytvoří novou obslužnou rutinu události s názvem `ProductsInCategory_RowDataBound` v `SummaryDataInFooter.aspx` použití modelu code-behind třídy stránky.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

Aby zůstalo zachované průběžný celkový musíme definovat proměnné mimo rozsah obslužné rutiny události. Vytvořte následující čtyři proměnné na úrovni stránky:

- `_totalUnitPrice`, typu `decimal`
- `_totalNonNullUnitPriceCount`, typu `int`
- `_totalUnitsInStock`, typu `int`
- `_totalUnitsOnOrder`, typu `int`

Dále napište kód pro pro každý řádek dat došlo k v těchto tří proměnných `RowDataBound` obslužné rutiny události.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` Obslužná rutina události začíná tím, že zajišťuje, že jsme pracujete s DataRow. Po vytvoření je, který se `Northwind.ProductsRow` instance, který byl právě spojen `GridViewRow` objektu v `e.Row` je uložen v proměnné `product`. Dál se spuštěné celkový počet proměnných jsou zvětšeny podle hodnoty, které odpovídají aktuální produkt (za předpokladu, že neobsahují databázi `NULL` hodnota). Budeme udržovat přehled o obou spouštění `UnitPrice` celkového počtu případů a počet jinou hodnotu než`NULL` `UnitPrice` záznamy, protože průměrná cena je podíl těchto dvou čísel.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>Krok 4: Zobrazení souhrnných dat v zápatí

Se souhrnnými daty sečteny posledním krokem je zobrazit v řádku zápatí prvku GridView. Tento úkol, lze provést prostřednictvím kódu programu přes `RowDataBound` obslužné rutiny události. Vzpomeňte si, že `RowDataBound` vyvolá obslužnou rutinu události pro *každý* řádek, který je vázán na včetně řádku zápatí prvku GridView. Proto jsme můžete rozšířit naše obslužnou rutinu události pro zobrazení dat v řádku zápatí pomocí následujícího kódu:


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

Protože řádku zápatí se přidá do prvku GridView. Po přidání všechny řádky dat, můžeme být jistí, že jsme připraveni zobrazit souhrnná data v zápatí, které se dokončily průběžný součet míry výpočty v čase. Poslední krok, pak se k nastavení těchto hodnot v buňkách zápatí.

Chcete-li zobrazit text v buňce konkrétní zápatí, použijte `e.Row.Cells[index].Text = value`, kde `Cells` indexování začínají na 0. Následující kód vypočítá průměrnou cenu (celková cena vydělí počtem produkty) a zobrazí ho společně s celkový počet jednotek na skladě a jednotek na pořadí do buňky odpovídající zápatí prvku GridView.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

Obrázek 13 zobrazuje sestavu po přidání tohoto kódu. Poznámka: Jak `ToString("c")` způsobí, že průměrná cena souhrnné informace bude naformátovaný jako měnu.


[![Teď má barvu pozadí načervenalé řádek zápatí prvku GridView.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**Obrázek 13**: Teď má načervenalé barva pozadí řádku zápatí prvku GridView ([kliknutím ji zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))


## <a name="summary"></a>Souhrn

Zobrazení souhrnných dat je běžné požadavky sestav a ovládací prvek GridView usnadňuje zahrnout tyto informace v zápatí řádku. Zobrazí se řádek zápatí při prvku GridView `ShowFooter` je nastavena na `true` a může mít textu v buňkách nastavují programově pomocí `RowDataBound` obslužné rutiny události. Výpočetní souhrnná data můžete buď provést znovu dotazování na databázi nebo pomocí kódu v třídě modelu code-behind stránky ASP.NET prostřednictvím kódu programu vypočítat souhrnná data.

V tomto kurzu končí naše zkoumání vlastní formátování s ovládacími prvky GridView DetailsView a FormView. V našem dalším kurzu zahajuje naše průzkum vložení, aktualizace a odstranění dat pomocí tyto stejné ovládací prvky.

Všechno nejlepší programování!

## <a name="about-the-author"></a>O autorovi

[Scott Meisnerová](http://www.4guysfromrolla.com/ScottMitchell.shtml), Autor sedm ASP/ASP.NET knih a Zakladatel [4GuysFromRolla.com](http://www.4guysfromrolla.com), má práce s Microsoft webových technologiích od roku 1998. Scott funguje jako nezávislý konzultant, trainer a zapisovače. Jeho nejnovější knihy [ *Edice nakladatelství Sams naučit sami ASP.NET 2.0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Může být dosáhl v [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím jeho blogu, který lze nalézt v [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](using-the-formview-s-templates-cs.md)
> [další](custom-formatting-based-upon-data-vb.md)
