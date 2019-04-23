---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: Přidání a reakce na tlačítek do ovládacího prvku GridView (C#) | Dokumentace Microsoftu
author: rick-anderson
description: V tomto kurzu podíváme na tom, jak přidat vlastní tlačítka na šablonu a k polím ovládacího prvku GridView nebo prvku DetailsView. Konkrétně jsme budete pří...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: a8cc1d98c0574145b0b74b64d53772bd50517067
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59404192"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>Přidání tlačítek do ovládacího prvku GridView a reakce na ně (C#)

podle [Scott Meisnerová](https://twitter.com/ScottOnWriting)

[Stáhněte si ukázkovou aplikaci](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe) nebo [stahovat PDF](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> V tomto kurzu podíváme na tom, jak přidat vlastní tlačítka na šablonu a k polím ovládacího prvku GridView nebo prvku DetailsView. Zejména vytvoříme rozhraní, které má FormView, umožňující uživateli stránkovat dodavatelů.


## <a name="introduction"></a>Úvod

Přestože mnoho scénáře vytváření sestav zahrnují přístup jen pro čtení k datům sestav, není, sestavy, které zahrnují možnost provádět akce na základě dat zobrazí. Obvykle to týká, přidání ovládacího prvku tlačítko, odkazem (LinkButton) nebo webové ImageButton s každý záznam zobrazí v sestavě, po kliknutí na vyvolá zpětné volání a vyvolá nějaký kód na straně serveru. Úpravy a odstranění dat na základě záznamu podle je Nejběžnějším příkladem. Ve skutečnosti, jak jsme viděli, počínaje [Přehled vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) kurz, úpravy a odstranění je běžné, že ovládací prvky GridView, DetailsView a FormView může podporovat tyto funkce bez třeba pro napsat jediný řádek kódu.

Kromě toho pro úpravy a odstraňování tlačítek, ovládacího prvku GridView, DetailsView a FormView ovládacích prvků může také zahrnovat tlačítka, LinkButtons nebo ImageButtons, po kliknutí na provést nějakou vlastní logiku na straně serveru. V tomto kurzu podíváme na tom, jak přidat vlastní tlačítka na šablonu a k polím ovládacího prvku GridView nebo prvku DetailsView. Zejména vytvoříme rozhraní, které má FormView, umožňující uživateli stránkovat dodavatelů. Pro daného dodavatele FormView zobrazí informace o dodavateli spolu s ovládací prvek tlačítko Web, který if kliknuto, označí všechny jejich související produkty jako ukončena. Kromě toho GridView uvádí tyto produkty vybrané dodavatelem, opatřeného každý řádek obsahující zvýšení ceny a slevy cena tlačítka, která, pokud kliknutí, zvýšit nebo snížit produktu `UnitPrice` % 10 (viz obrázek 1).


[![FormView i GridView obsahovat tlačítka, která provést vlastní akce](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**Obrázek 1**: FormView i GridView obsahovat tlačítka, že provedení vlastní akce ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png))


## <a name="step-1-adding-the-button-tutorial-web-pages"></a>Krok 1: Přidání tlačítka kurz webových stránek

Předtím, než se podíváme na tom, jak přidat vlastní tlačítka, věnujte chvíli vytvářet stránky technologie ASP.NET v našem projektu webu, který budeme potřebovat pro účely tohoto kurzu první. Začněte přidáním novou složku s názvem `CustomButtons`. Dále přidejte následující dvě stránky ASP.NET do této složky, nezapomeňte přiřadit každou stránku s `Site.master` hlavní stránky:

- `Default.aspx`
- `CustomButtons.aspx`


![Přidání stránky technologie ASP.NET pro vlastní tlačítka související kurzy](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**Obrázek 2**: Přidání stránky technologie ASP.NET pro vlastní tlačítka související kurzy


V jiných složkách, jako jsou `Default.aspx` v `CustomButtons` složky zobrazí seznam kurzů v příslušném oddílu. Vzpomeňte si, že `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek tuto funkci poskytuje. Proto přidat tento uživatelský ovládací prvek `Default.aspx` jeho přetažením z Průzkumníka řešení do zobrazení návrhu.


[![Přidat na stránku Default.aspx SectionLevelTutorialListing.ascx uživatelského ovládacího prvku](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**Obrázek 3**: Přidat `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek `Default.aspx` ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png))


A konečně, přidejte na stránkách jako položky `Web.sitemap` souboru. Konkrétně, přidejte následující kód za stránkování a řazení `<siteMapNode>`:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`, věnujte chvíli zobrazit kurzy web prostřednictvím prohlížeče. V nabídce na levé straně teď obsahuje položky pro úpravy, vložení a odstranění kurzy.


![Mapa webu nyní obsahuje položku pro tento kurz vlastních tlačítek](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**Obrázek 4**: Mapa webu nyní obsahuje položku pro tento kurz vlastních tlačítek


## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>Krok 2: Přidání třídy FormView, který obsahuje seznam dodavatelů

Můžeme začít s tímto kurzem přidáním FormView, který obsahuje seznam dodavatelů. Jak je popsáno v úvodu tohoto FormView umožní uživateli procházení dodavatelů, produkty poskytnuté dodavatelem v GridView zobrazující. Kromě toho tato FormView bude obsahovat tlačítko, po kliknutí na označí všechny produkty dodavatele jak ukončena. Předtím, než jsme si problém s přidání vlastního tlačítka na třídě FormView, nejdřív právě vytvoříme FormView tak, aby zobrazil informace o dodavateli.

Začněte otevřením `CustomButtons.aspx` stránku `CustomButtons` složky. Přidat na stránku FormView jeho přetažením z panelu nástrojů do návrháře a nastavte jeho `ID` vlastnost `Suppliers`. Z ovládacího prvku FormView inteligentních značek, rozhodnout vytvořit nového prvku ObjectDataSource s názvem `SuppliersDataSource`.


[![Vytvoření nového prvku ObjectDataSource s názvem SuppliersDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**Obrázek 5**: Vytvoření nového prvku ObjectDataSource s názvem `SuppliersDataSource` ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png))


Nakonfigurujte tento nový prvek ObjectDataSource, tak, aby se dotázal z `SuppliersBLL` třídy `GetSuppliers()` – metoda (viz obrázek 6). Protože tato FormView neposkytuje rozhraní pro aktualizaci dodavatele informace, vyberte možnost (žádná) z rozevíracího seznamu na kartě aktualizace.


[![Konfigurace zdroje dat pomocí třídy SuppliersBLL s GetSuppliers() – metoda](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**Obrázek 6**: Konfigurace zdroje dat pro použití `SuppliersBLL` třídy `GetSuppliers()` – metoda ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png))


Po dokončení konfigurace ObjectDataSource, Visual Studio vygeneruje `InsertItemTemplate`, `EditItemTemplate`, a `ItemTemplate` pro FormView. Odeberte `InsertItemTemplate` a `EditItemTemplate` a upravovat `ItemTemplate` tak, aby zobrazil pouze dodavatele společnosti jméno a telefonní číslo. Nakonec zapnutí podpory stránkování pro FormView zaškrtnutím políčka Povolit stránkování z jeho inteligentní značky (nebo nastavením jeho `AllowPaging` vlastnost `True`). Po provedení těchto změn na stránce deklarativní by měl vypadat nějak takto:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

Obrázek 7 znázorňuje stránce CustomButtons.aspx při zobrazit pomocí prohlížeče.


[![Pole CompanyName a Phone od aktuálně vybraného dodavatele obsahuje seznam FormView](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**Obrázek 7**: Uvádí FormView `CompanyName` a `Phone` pole od dodavatele aktuálně vybrané ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png))


## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>Krok 3: Přidání prvku GridView, která zobrazuje seznam produktů, vybrané dodavatele

Předtím, než jsme do ovládacího prvku FormView šablony přidat tlačítko Ukončit všechny produkty, nejprve přidáme GridView ve třídě FormView, který obsahuje seznam produktů poskytovaných vybrané dodavatelem. Chcete-li GridView dosáhnout, přidat na stránku, nastavte jeho `ID` vlastnost `SuppliersProducts`, a přidejte nový prvek ObjectDataSource s názvem `SuppliersProductsDataSource`.


[![Vytvoření nového prvku ObjectDataSource s názvem SuppliersProductsDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**Obrázek 8**: Vytvoření nového prvku ObjectDataSource s názvem `SuppliersProductsDataSource` ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png))


Konfigurace tohoto prvku ObjectDataSource pomocí třídy ProductsBLL `GetProductsBySupplierID(supplierID)` – metoda (viz obrázek 9). Zatímco ceny produktu upraví umožní tohoto ovládacího prvku GridView, nebude použití předdefinované úpravy nebo odstranění funkce z prvku GridView. Proto jsme rozevíracího seznamu na (žádný) nastavit ObjectDataSource uživatele UPDATE, INSERT a odstranit záložky.


[![Konfigurace zdroje dat pomocí třídy ProductsBLL s GetProductsBySupplierID(supplierID) – metoda](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**Obrázek 9**: Konfigurace zdroje dat pro použití `ProductsBLL` třídy `GetProductsBySupplierID(supplierID)` – metoda ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))


Vzhledem k tomu, `GetProductsBySupplierID(supplierID)` metoda přijímá jako vstupní parametr, Průvodce ObjectDataSource vyzve nám zdroje hodnota tohoto parametru. A zajistěte tak předání `SupplierID` hodnotu FormView, nastavte parametr zdroj rozevíracího seznamu na ovládací prvek a rozevírací seznam ControlID na `Suppliers` (ID třídy FormView vytvořili v kroku 2).


[![Označení pole supplierID parametr musí pocházet z ovládacího prvku FormView dodavatelů](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**Obrázek 10**: Označuje, že *`supplierID`* parametr by měl pocházet z `Suppliers` ovládacího prvku FormView ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png))


Po dokončení Průvodce prvek ObjectDataSource, bude prvku GridView obsahovat vlastnost BoundField nebo třídě CheckBoxField pro každé pole data produktu. Pojďme to trim dolů zobrazíte jenom `ProductName` a `UnitPrice` BoundFields spolu s `Discontinued` třídě CheckBoxField; navíc umožňuje formát `UnitPrice` Vlastnost BoundField tak, aby jeho textu je formátován jako měnu. Vaše GridView a `SuppliersProductsDataSource` ObjectDataSource deklarativní by měla vypadat podobně jako následující kód:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

V tomto okamžiku v našem kurzu zobrazí hlavních/podrobných sestav, umožňuje uživateli vybrat jiného dodavatele z FormView v horní části a zobrazit produkty poskytovaných dodavateli prostřednictvím GridView v dolní části. Při výběru Tokio Traders dodavatel z FormView obrázku 11 můžete vidět snímek obrazovky na této stránce.


[![Produkty s vybraný poskytovatel se zobrazují v prvku GridView.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**Obrázek 11**: Dodavatel vybrané produkty jsou zobrazeny v prvku GridView ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png))


## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>Krok 4: Vytvoření vrstvy DAL a metody BLL ukončit všechny produkty pro dodavatele

Předtím, než jsme FormView přidáte tlačítko, po kliknutí na ze všech produktů dodavatele, musíme nejprve přidat metodu k DAL a BLL, který provádí tuto akci. Zejména, bude mít tato metoda `DiscontinueAllProductsForSupplier(supplierID)`. Při kliknutí na tlačítko ovládacího prvku FormView jsme budete vyvolat tuto metodu v vrstvy obchodní logiky předáním hodnoty ve vybrané dodavatele `SupplierID`; BLL pak zavolá na odpovídající metody vrstvy přístupu k datům, které budou vydávat `UPDATE` – příkaz k databázi, která ze zadaného dodavatele produkty.

Jak jsme udělali v našich kurzů pro předchozí, použijeme zdola nahoru přístup, od vytvoření metodu DAL, pak metoda knihoven BLL a nakonec implementace funkcí na stránce technologie ASP.NET. Otevřít `Northwind.xsd` typované datové sady v `App_Code/DAL` složky a přidat nový způsob `ProductsTableAdapter` (klikněte pravým tlačítkem na `ProductsTableAdapter` a zvolte Přidat dotaz). Tím se otevře Průvodce konfigurací dotazu TableAdapter, který nám vás provede procesem přidávání nové metody. Začněte tak, že tato metoda naše DAL pomocí ad-hoc příkazu SQL.


[![Vytvořit metodu DAL pomocí Ad-Hoc příkazu SQL](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**Obrázek 12**: Vytvoření vrstvy DAL metoda použití příkazu SQL Ad-Hoc ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png))


V dalším kroku průvodce vyzve nám, jaký typ dotazu vytvořte. Protože `DiscontinueAllProductsForSupplier(supplierID)` metoda bude nutné provést aktualizaci `Products` databázové tabulky, nastavení `Discontinued` pole na hodnotu 1 pro všechny produkty poskytnuté zadaný *`supplierID`*, potřebujeme vytvořit dotaz, který aktualizuje data.


[![Zvolte typ dotazu aktualizace](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**Obrázek 13**: Zvolte typ dotazu aktualizace ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png))


Na další obrazovce průvodce jsou existující TableAdapter `UPDATE` příkazu, který aktualizuje všech polí definovaných v `Products` objektu DataTable. Text dotazu nahraďte následující příkaz:

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

Po zadání tohoto dotazu a kliknutí na tlačítko Další, na poslední obrazovce průvodce požádá o novou metodu název použití `DiscontinueAllProductsForSupplier`. Dokončete průvodce kliknutím na tlačítko Dokončit. Po návratu do návrháře datových sad, měli byste vidět nové metody v `ProductsTableAdapter` s názvem `DiscontinueAllProductsForSupplier(@SupplierID)`.


[![Název nové DiscontinueAllProductsForSupplier DAL – metoda](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**Obrázek 14**: Pojmenujte novou metodu DAL `DiscontinueAllProductsForSupplier` ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))


S `DiscontinueAllProductsForSupplier(supplierID)` metoda vytvořené v vrstvy přístupu k datům, naše dalším krokem je vytvoření `DiscontinueAllProductsForSupplier(supplierID)` metoda ve vrstvy obchodní logiky. Chcete-li to provést, otevřete `ProductsBLL` třídy soubor a přidejte následující:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

Tato metoda provede jednoduché volání dolů na `DiscontinueAllProductsForSupplier(supplierID)` metoda ve DAL předávání podél zadaných *`supplierID`* hodnotu parametru. Kdyby existovalo všechny obchodní pravidla, která povoluje jenom dodavatele produkty ukončena za určitých okolností, by měl být tato pravidla zde prováděn BLL.

> [!NOTE]
> Na rozdíl od `UpdateProduct` přetížení v `ProductsBLL` třídy, `DiscontinueAllProductsForSupplier(supplierID)` nezahrnuje podpis metody `DataObjectMethodAttribute` atribut (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`). To vylučuje `DiscontinueAllProductsForSupplier(supplierID)` metodu z Průvodce konfigurací zdroje dat prvku ObjectDataSource rozevíracího seznamu na kartě aktualizace. Můžu odebrat vynechána tento atribut, protože jsme vám volat `DiscontinueAllProductsForSupplier(supplierID)` metody přímo z obslužné rutiny události na naší stránce ASP.NET.


## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>Krok 5: Přidání ukončit všechny produkty tlačítko třídě FormView

S `DiscontinueAllProductsForSupplier(supplierID)` metodou v knihoven BLL a DAL dokončení v posledním kroku pro přidání možnost ukončit všechny produkty pro vybrané dodavatele je přidání ovládacího prvku tlačítko ovládacího prvku FormView `ItemTemplate`. Přidejte tlačítko, níže dodavatele telefonní číslo, text tlačítka, ukončí všechny produkty a `ID` hodnotou vlastnosti `DiscontinueAllProductsForSupplier`. Přidáte tento ovládací prvek tlačítko Web prostřednictvím návrháře kliknutím na odkaz Upravit šablony v inteligentní značky ovládacího prvku FormView (viz obrázek 15), nebo přímo prostřednictvím deklarativní syntaxe.


[![Přidat ukončit všechny produkty webového ovládacího prvku tlačítka FormView s ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**Obrázek 15**: Přidání ukončit všechny produkty tlačítko webový ovládací prvek do ovládacího prvku FormView `ItemTemplate` ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png))


Po kliknutí na tlačítko tak, že uživatel navštívit stránku postback vyplývá a ovládacího prvku FormView na [ `ItemCommand` události](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) aktivována. K provedení vlastního kódu v reakci na toto tlačítko klepnutí, můžeme vytvořit obslužnou rutinu události pro tuto událost. Informace o tom, ale, že `ItemCommand` událost se aktivuje vždy, když *jakékoli* dojde ke kliknutí na ovládací prvek tlačítko, odkazem (LinkButton) nebo webové ImageButton ve třídě FormView. To znamená, že když uživatel přesune z jedné stránky na jiné ve třídě FormView `ItemCommand` dojde k aktivaci události; stejnou věc, když uživatel klikne na tlačítko Nový, úpravy, nebo odstraňte ve třídě FormView, který podporuje vkládání, aktualizace nebo odstranění.

Vzhledem k tomu, `ItemCommand` aktivuje se bez ohledu na to, co je kliknutí na tlačítko v případě, že obslužná rutina potřebujeme způsob, jak určit, pokud došlo ke kliknutí na tlačítko Ukončit všechny produkty, nebo pokud se jednalo o některé jiné tlačítko. K tomu můžeme můžete nastavit ovládací prvek tlačítko webového `CommandName` vlastnost nějakou identifikační hodnotu. Při klepnutí na tlačítko, to `CommandName` předanou do `ItemCommand` obslužná rutina události, umožňuje nám zjistit, zda tlačítko Ukončit všechny produkty kliknutí na tlačítko. Ukončit všechny produkty tlačítka nastavte `CommandName` vlastnost DiscontinueProducts.

K zajištění, že uživatel chce přestat vybrané dodavatele produkty nakonec použijeme dialogové okno potvrzení na straně klienta. Jak jsme viděli v [přidání Client-Side potvrzení při odstraňování](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md) výukový program, můžete to provést pomocí verze jazyka JavaScript. Konkrétně pro vlastnost ovládacího prvku tlačítko webového OnClientClick `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

Po provedení těchto změn, ovládacího prvku FormView deklarativní syntaxe by měl vypadat nějak takto:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

Dále vytvořte obslužnou rutinu události pro ovládacího prvku FormView `ItemCommand` událostí. V této obslužné rutiny události je třeba nejprve určit, zda došlo ke kliknutí na tlačítko Ukončit všechny produkty. Pokud tedy chcete vytvořit instanci `ProductsBLL` třídy a vyvolání jeho `DiscontinueAllProductsForSupplier(supplierID)` metodu `SupplierID` o vybrané třídě FormView:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

Všimněte si, že `SupplierID` aktuální vybrané dodavatele ve třídě FormView lze přistupovat pomocí ovládacího prvku FormView [ `SelectedValue` vlastnost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx). `SelectedValue` Vlastnost vrací hodnotu pro tento záznam se zobrazí ve třídě FormView klíče první data. Ovládacího prvku FormView [ `DataKeyNames` vlastnost](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx), což znamená data pole, ze kterých hodnoty klíče data jsou z, byl automaticky nastaven na `SupplierID` pomocí sady Visual Studio při vytváření vazby ObjectDataSource ke třídě FormView zpět v kroku 2.

S `ItemCommand` obslužná rutina události vytvoří, využít k otestování stránky. Přejděte do Cooperativa de Quesos "Las Cabras" supplier (je pátý dodavatele ve třídě FormView pro mě). Tento poskytovatel poskytuje dva produkty, Queso Cabrales a Queso Manchego La Pastora, které jsou *není* ukončena.

Představte si, že Cooperativa de Quesos "Las Cabras" náramků RFID nevyvíjí obchodní činnost, a proto jeho produktů jsou ukončena. Klikněte na tlačítko ukončí všechny produkty tlačítko. Zobrazí se dialogové okno potvrzení na straně klienta (viz obrázek 16).


[![Cooperativa de Quesos Las Cabras poskytuje dva aktivní produkty](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**Obrázek 16**: Cooperativa de Quesos Las Cabras poskytuje dva aktivní produkty ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png))


Pokud klepnete na tlačítko OK v dialogovém okně Potvrdit na straně klienta, bude pokračovat odeslání formuláře, ve kterém způsobí zpětné odeslání ovládacího prvku FormView `ItemCommand` událost se aktivuje. Obslužná rutina události, které jsme vytvořili pak spustí, volání `DiscontinueAllProductsForSupplier(supplierID)` metoda a ukončení Queso Cabrales i Queso Manchego La Pastora produktů.

Pokud jste zakázali stav zobrazení v prvku GridView, prvku GridView je právě znovu připojeno k základnímu úložišti dat. při každém postbacku a proto bude okamžitě aktualizovat tak, aby odrážely, že tyto dva produkty jsou nyní ukončena (viz obrázek 17). Pokud však ještě zakázaný stav zobrazení v prvku GridView, musíte ručně po provedení této změny znovu připojit data, která mají prvku GridView. K tomu stačí provést volání do prvku GridView `DataBind()` metoda ihned po volání `DiscontinueAllProductsForSupplier(supplierID)` metody.


[![Po kliknutí na tlačítko Ukončit všechny produkty, Dodavatel s produkty jsou odpovídajícím způsobem aktualizuje](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**Obrázek 17**: Po kliknutí na tlačítko Ukončit všechny produkty, dodavatele produkty jsou odpovídajícím způsobem aktualizuje ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png))


## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>Krok 6: Vytváření přetížení UpdateProduct v vrstvy obchodní logiky pro úpravu ceny produktu

Stejně jako se ukončí všechny produkty tlačítko ve třídě FormView, chcete-li přidat tlačítka pro zvýšení a snížení ceny pro produkt v prvku GridView musíme nejprve přidat vhodné metody vrstvy přístupu k datům a vrstvu obchodní logiky. Vzhledem k tomu, že už máme metodu, která aktualizuje řádek jednoho produktu v DAL, můžete tyto funkce zajišťuje tak, že vytvoříte nová přetížení pro `UpdateProduct` metodu BLL.

Naše minulosti `UpdateProduct` přetížení trvalo v kombinaci polí produktů jako skalární vstupní hodnoty a potom aktualizují pouze pole pro daný produkt. Pro toto přetížení budeme se trochu liší od tento standard a místo toho předat v rámci produktu `ProductID` a procento, podle kterého chcete upravit `UnitPrice` (na rozdíl od předávání na novém upravit `UnitPrice` samotné). Tento přístup se zjednodušit kód, který potřebujeme k zápisu do třídy modelu code-behind stránky technologie ASP.NET, protože nemusíme zabývat určující aktuální produkt `UnitPrice`.

`UpdateProduct` Přetížení pro tento kurz je uveden níže:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

Toto přetížení načte informace o daný produkt prostřednictvím DAL `GetProductByProductID(productID)` metody. Poté zkontroluje, zda produktu `UnitPrice` je přiřazena databázi `NULL` hodnotu. Pokud se jedná, cena je ponechán beze změny. Pokud však není non -`NULL` `UnitPrice` hodnotu metodu aktualizace produktu `UnitPrice` pomocí zadaného procenta (`unitPriceAdjustmentPercent`).

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>Krok 7: Přidání zvýšení a snížení tlačítka do prvku GridView.

Ovládacího prvku GridView (a DetailsView) jsou oba obsahují celou kolekci polí. Kromě BoundFields, CheckBoxFields a vlastností TemplateField technologie ASP.NET obsahuje ButtonField, ve kterém, jak již název napovídá, vykreslí jako tlačítko, odkazem (LinkButton) nebo ImageButton sloupec pro každý řádek. Podobný třídě FormView kliknutím *jakékoli* tlačítko v rámci ovládacího prvku GridView tlačítka stránkování, úpravy nebo odstranění tlačítka, tlačítka řazení a tak dále vyvolá zpětné volání a vyvolá prvku GridView [ `RowCommand` události](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx).

Má ButtonField `CommandName` vlastnost, která se přiřadí zadanou hodnotu na všech svých tlačítek `CommandName` vlastnosti. Třeba v třídě FormView `CommandName` hodnotu používají `RowCommand` obslužné rutiny události k určení, které tlačítko došlo ke kliknutí na.

Přidejme dvě nové ButtonFields do prvku GridView, jednu s text tlačítka Price + 10 % a další s textem cena -10 %. Chcete-li přidat tyto ButtonFields, klikněte na odkaz Upravit sloupce v prvku GridView inteligentní značky, vyberte typ ButtonField pole ze seznamu v levém horním rohu a klikněte na tlačítko Přidat.


![Přidání dvou ButtonFields do prvku GridView.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**Obrázek 18**: Přidání dvou ButtonFields do prvku GridView.


Přesuňte dvě ButtonFields tak, aby se zobrazí jako první dvě pole ovládacího prvku GridView. Dále nastavte `Text` vlastnosti těchto dvou ButtonFields k určení ceny + 10 % a cena -10 % a `CommandName` vlastností IncreasePrice a DecreasePrice, v uvedeném pořadí. Ve výchozím nastavení ButtonField zobrazí jeho sloupec tlačítka jako LinkButtons. To lze změnit, ale prostřednictvím ButtonField [ `ButtonType` vlastnost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx). Dopřejeme si tyto dvě ButtonFields se vykresluje jako tlačítek regulární; Proto nastavte `ButtonType` vlastnost `Button`. Obrázek 19 zobrazuje pole dialogové okno po provedení těchto změn; Následující je deklarativní značkovací prvku GridView.


![Konfigurace textu ButtonFields, CommandName a má vlastnost ButtonType vlastnosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**Obrázek 19**: Konfigurace ButtonFields `Text`, `CommandName`, a `ButtonType` vlastnosti


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

Pomocí těchto ButtonFields vytvořili, posledním krokem je vytvoření obslužné rutiny události pro prvku GridView `RowCommand` událostí. Tato obslužná rutina události, je-li aktivováno, protože buď cena + 10 % nebo % tlačítka cena -10 bylo kliknuto, je potřeba určit `ProductID` pro řádek, jehož tlačítko došlo ke kliknutí na a pak vyvolejte `ProductsBLL` třídy `UpdateProduct` metoda předávání do příslušné `UnitPrice` procentuální úprava spolu s `ProductID`. Následující kód provede tyto úlohy:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

Aby bylo možné zjistit `ProductID` řádku jejichž cena + 10 % nebo % tlačítko cena -10 došlo ke kliknutí na, budeme potřebovat poradit prvku GridView `DataKeys` kolekce. Tato kolekce obsahuje hodnoty polí podle `DataKeyNames` vlastnost pro každý řádek prvku GridView. Od prvku GridView `DataKeyNames` vlastnost nastavila na ProductID pomocí sady Visual Studio při vytváření vazby ObjectDataSource k prvku GridView, `DataKeys(rowIndex).Value` poskytuje `ProductID` pro zadaný rozbočovač *rowIndex*.

ButtonField automaticky předá *rowIndex* řádku došlo ke kliknutí na tlačítko, jejichž prostřednictvím `e.CommandArgument` parametru. Proto k určení `ProductID` řádku jejichž cena + 10 % nebo % tlačítko cena -10 došlo ke kliknutí na, používáme: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`.

Jako s tlačítko Ukončit všechny produkty, pokud jste zakázali stav zobrazení prvku GridView, prvku GridView je právě znovu připojeno k základnímu úložišti dat. při každém postbacku a proto bude okamžitě aktualizovat tak, aby odrážely, ke které dochází od kliknutí na změnu ceny Některé z tlačítek. Pokud však ještě zakázaný stav zobrazení v prvku GridView, musíte ručně po provedení této změny znovu připojit data, která mají prvku GridView. K tomu stačí provést volání do prvku GridView `DataBind()` metoda ihned po volání `UpdateProduct` metody.

Obrázek 20 zobrazuje stránku při prohlížení produktů poskytovaných Grandma Kelly věci odvál čas. Obrázek 21 ukazuje výsledky po Price + 10 % bylo stisknuto tlačítko dvakrát pro Grandma's Boysenberry Spread a tlačítko cena -10 % jednou pro úpravu Cranberry Northwoods.


[![GridView zahrnuje cena + 10 % a cena -10 % tlačítka](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**Obrázek 20**: Cena zahrnuje GridView + 10 % a cena -10 % tlačítka ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png))


[![Ceny produktu první a třetí se aktualizovaly přes Price + 10 % a cena -10 % tlačítka](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**Obrázek 21**: Ceny platné pro první a třetí produktu se aktualizovaly přes Price + 10 % a cena -10 % tlačítka ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png))


> [!NOTE]
> Ovládacího prvku GridView (a DetailsView) může mít také tlačítka, LinkButtons nebo ImageButtons přidán do jejich vlastností TemplateField. Jak se vlastnost BoundField, bude tato tlačítka, po kliknutí na zahájit zpětné volání, zvýšení prvku GridView `RowCommand` událostí. Při přidání tlačítek v TemplateField, ale na tlačítko `CommandArgument` nejsou nastaveny automaticky na index řádku, který je při použití ButtonFields. Pokud je potřeba určit index řádku tlačítka, které bylo kliknuto v rámci `RowCommand` obslužná rutina události, bude nutné ručně nastavit na tlačítko `CommandArgument` vlastnost v jeho deklarativní syntaxe v rámci TemplateField, pomocí kódu, jako jsou:  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`.


## <a name="summary"></a>Souhrn

Všechny prvky GridView, DetailsView a FormView můžou zahrnovat tlačítka, LinkButtons nebo ImageButtons. Tlačítka, po kliknutí na vyvolávají zpětné odeslání a zvýšit `ItemCommand` události v ovládacích prvcích FormView a DetailsView a `RowCommand` události v prvku GridView. Tyto webové ovládací prvky dat mít integrovanou funkci pro zpracování běžných akce související s příkazu, jako je například odstranění nebo úprava záznamů. Ale můžeme také použití tlačítka, které při kliknutí na, reagovat pomocí provádí vlastní vlastní kód.

K tomu potřebujeme vytvořit obslužná rutina události `ItemCommand` nebo `RowCommand` událostí. V této obslužné rutiny události jsme příchozí zprávy nejprve zkontrolujte `CommandName` hodnotu k určení, které tlačítko došlo ke kliknutí na a poté přijmout vhodná opatření vlastní. V tomto kurzu jsme viděli, jak pomocí tlačítka a ButtonFields ukončit všechny produkty pro zadaný dodavatele nebo zvýšení nebo snížení ceny konkrétního produktu 10 %.

Všechno nejlepší programování!

## <a name="about-the-author"></a>O autorovi

[Scott Meisnerová](http://www.4guysfromrolla.com/ScottMitchell.shtml), Autor sedm ASP/ASP.NET knih a Zakladatel [4GuysFromRolla.com](http://www.4guysfromrolla.com), má práce s Microsoft webových technologiích od roku 1998. Scott funguje jako nezávislý konzultant, trainer a zapisovače. Jeho nejnovější knihy [ *Edice nakladatelství Sams naučit sami ASP.NET 2.0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Může být dosáhl v [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím jeho blogu, který lze nalézt v [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Next](adding-and-responding-to-buttons-to-a-gridview-vb.md)
