---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: Filtrování seznamu a podrobností na dvou stránkách (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 0e30d47a565c3b6cb9f647d54d47c10a418762f4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044971"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>Filtrování hlavních záznamů / podrobností na dvou stránkách (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) nebo [Stáhnout PDF](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat odkaz Zobrazit produkty, který po kliknutí umožní uživateli samostatnou stránku se seznamem těchto produktů pro vybraného dodavatele.

## <a name="introduction"></a>Úvod

V předchozích dvou kurzech jsme viděli, jak zobrazit hlavní a podrobné sestavy na jediné webové stránce pomocí DropDownList k zobrazení "hlavních" záznamů a ovládacího prvku [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) nebo [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) pro zobrazení podrobností. Dalším běžným vzorem, který se používá pro sestavy Master/Details, je mít hlavní záznamy na jedné webové stránce a podrobnosti zobrazené na jiném. Web fóra, jako [jsou fóra ASP.NET](https://forums.asp.net/), je skvělým příkladem tohoto vzoru v praxi. Fóra ASP.NET se skládají z nejrůznějších fór Začínáme, webových formulářů, ovládacích prvků prezentace dat a tak dále. Každé fórum se skládá z mnoha vláken a každé vlákno se skládá z řady příspěvků. Na domovské stránce fóra ASP.NET jsou fóra uvedená v seznamu. Kliknutím na fórum se zobrazí `ShowForum.aspx` Stránka s přehledem vláken pro toto fórum. Podobně kliknutím na vlákno přejdete na `ShowPost.aspx` , které zobrazuje příspěvky pro vlákno, na které jste klikli.

V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat odkaz Zobrazit produkty, který po kliknutí umožní uživateli samostatnou stránku se seznamem těchto produktů pro vybraného dodavatele.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>Krok 1: přidání `SupplierListMaster.aspx` a vložení `ProductsForSupplierDetails.aspx` stránek do `Filtering` složky

Při definování rozložení stránky v třetím kurzu jsme přidali řadu "počátečních" stránek do `BasicReporting` `Filtering` složek, a `CustomFormatting` . V tuto chvíli jsme ale nepřidali úvodní stránku pro tento kurz, proto si chvíli počkejte, než do složky přidáte dvě nové stránky `Filtering` : `SupplierListMaster.aspx` a `ProductsForSupplierDetails.aspx` . `SupplierListMaster.aspx` Zobrazí seznam "hlavních" záznamů (dodavatelé) a současně `ProductsForSupplierDetails.aspx` zobrazí produkty pro vybraného dodavatele.

Při vytváření těchto dvou nových stránek je jisté, že je přiřadíte k `Site.master` hlavní stránce.

![Přidejte stránky SupplierListMaster. aspx a ProductsForSupplierDetails. aspx do složky filtrování.](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**Obrázek 1**: přidání `SupplierListMaster.aspx` stránek a `ProductsForSupplierDetails.aspx` do `Filtering` složky

Při přidávání nových stránek do projektu Nezapomeňte také aktualizovat soubor mapy webu, `Web.sitemap` a odpovídajícím způsobem. Pro účely tohoto kurzu jednoduše přidejte `SupplierListMaster.aspx` stránku na mapu webu pomocí následujícího obsahu XML jako podřízeného elementu filtrovat sestavy `<siteMapNode>` :

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> Proces aktualizace souboru mapy lokality můžete automatizovat při přidávání nových stránek ASP.NET pomocí [makra K mapě webu](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)aplikace Visual Studio [. Scott Allen](http://odetocode.com/Blogs/scott/).

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>Krok 2: zobrazení seznamu dodavatelů v`SupplierListMaster.aspx`

S `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` vytvořenými stránkami a je dalším krokem vytvoření prvku GridView pro dodavatele v `SupplierListMaster.aspx` . Přidejte prvek GridView na stránku a vytvořte jeho vazby s novým prvkem ObjectDataSource. Tento prvek ObjectDataSource by měl použít `SuppliersBLL` `GetSuppliers()` metodu třídy pro vrácení všech dodavatelů.

[![Vyberte třídu SuppliersBLL](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**Obrázek 2**: vyberte `SuppliersBLL` třídu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image4.png)).

[![Konfigurace prvku ObjectDataSource pro použití metody getsupplierss ()](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro použití `GetSuppliers()` metody ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image7.png))

Musíme zahrnout odkaz s názvem zobrazení produktů v každém řádku GridView, který po kliknutí převezme uživatele, aby `ProductsForSupplierDetails.aspx` přesměroval hodnotu vybraného řádku `SupplierID` pomocí řetězce dotazu. Pokud uživatel například klikne na odkaz Zobrazit produkty pro dodavatele Brna Traders (který má `SupplierID` hodnotu 4), mělo by být odesláno `ProductsForSupplierDetails.aspx?SupplierID=4` .

K tomuto účelu přidejte [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) do prvku GridView, který přidá hypertextový odkaz na každý řádek prvku GridView. Začněte kliknutím na odkaz Upravit sloupce z inteligentní značky GridView. Dále vyberte HyperLinkField ze seznamu v levém horním rohu a kliknutím na tlačítko Přidat zahrňte HyperLinkField do seznamu polí prvku GridView.

[![Přidat HyperLinkField do prvku GridView.](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**Obrázek 4**: Přidání prvku HyperLinkField do prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image10.png))

HyperLinkField je možné nakonfigurovat tak, aby používala stejný text nebo hodnoty URL jako odkaz v jednotlivých řádcích prvku GridView nebo tyto hodnoty mohou být základem datových hodnot vázaných na konkrétní řádek. Chcete-li určit statickou hodnotu ve všech řádcích, použijte `Text` vlastnosti HyperLinkField nebo `NavigateUrl` . Vzhledem k tomu, že chceme, aby byl text odkazu stejný pro všechny řádky, nastavte `Text` vlastnost HyperLinkField na hodnotu Zobrazit produkty.

[![Nastavte vlastnost text HyperLinkField na Zobrazit produkty.](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**Obrázek 5**: nastavte `Text` vlastnost HyperLinkField na hodnotu Zobrazit produkty ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image13.png)).

Chcete-li nastavit hodnoty textu nebo adresy URL na základě podkladových dat vázaných na řádek prvku GridView, určete datová pole, která mají být z vlastností nebo zadány z hodnot text nebo URL `DataTextField` `DataNavigateUrlFields` . `DataTextField` dá se nastavit jenom na jedno datové pole. `DataNavigateUrlFields`Nicméně lze nastavit na seznam datových polí oddělených čárkami. Často je potřeba založit text nebo adresu URL na kombinaci hodnoty datového pole aktuálního řádku a některých statických značek. V tomto kurzu například chceme mít adresu URL odkazů na HyperLinkField `ProductsForSupplierDetails.aspx?SupplierID=supplierID` , kde *`supplierID`* je každá hodnota Row's prvku GridView `SupplierID` . Všimněte si, že v tomto umístění potřebujeme jak statické, tak datově řízené hodnoty: `ProductsForSupplierDetails.aspx?SupplierID=` část adresy URL odkazu je statická, zatímco *`supplierID`* část je řízená daty jako její hodnota je vlastní hodnota každého řádku `SupplierID` .

Chcete-li označit kombinaci statických a dat řízených hodnot, použijte `DataTextFormatString` `DataNavigateUrlFormatString` vlastnosti a. V těchto vlastnostech zadejte statické značky podle potřeby a pak použijte značku, `{0}` kde má být hodnota pole zadaná ve `DataTextField` `DataNavigateUrlFields` vlastnostech nebo. Pokud `DataNavigateUrlFields` má vlastnost použít více polí, `{0}` kde má být první hodnota pole vložena, `{1}` pro druhé pole hodnota a tak dále.

V našem kurzu musíme `DataNavigateUrlFields` vlastnost nastavit na `SupplierID` , protože to je datové pole, jehož hodnota potřebujeme přizpůsobit pro jednotlivé řádky a `DataNavigateUrlFormatString` vlastnost na `ProductsForSupplierDetails.aspx?SupplierID={0}` .

[![Nakonfigurujte HyperLinkField tak, aby zahrnoval správnou adresu URL odkazu na základě ČísloDodavatele.](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**Obrázek 6**: Nakonfigurujte HyperLinkField tak, aby zahrnoval správnou adresu URL odkazu na základě `SupplierID` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-vb/_static/image16.png)

Po přidání HyperLinkField Nebojte se přizpůsobit a změnit pořadí polí prvku GridView. Následující kód ukazuje prvek GridView po provedení některých menších úprav na úrovni pole.

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

Chvíli si zobrazte `SupplierListMaster.aspx` stránku v prohlížeči. Jak ukazuje obrázek 7, stránka aktuálně obsahuje seznam všech dodavatelů včetně odkazu zobrazit produkty. Kliknutím na odkaz Zobrazit produkty přejdete do `ProductsForSupplierDetails.aspx` řetězce dotazu, který se nachází podél dodavatele `SupplierID` .

[![Každý řádek dodavatele obsahuje odkaz Zobrazit produkty.](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**Obrázek 7**: každý řádek dodavatele obsahuje odkaz na zobrazení produktů ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image19.png)).

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>Krok 3: výpis produktů dodavatele v`ProductsForSupplierDetails.aspx`

V tomto okamžiku `SupplierListMaster.aspx` stránka posílá uživatele do `ProductsForSupplierDetails.aspx` řetězce dotazu, který předá vybraný dodavatel `SupplierID` . Posledním krokem tohoto kurzu je zobrazení produktů v prvku GridView, jejichž výsledkem je `ProductsForSupplierDetails.aspx` `SupplierID` , že se rovná `SupplierID` předanému pomocí řetězce dotazu. Chcete-li dosáhnout tohoto začátku přidáním prvku GridView do `ProductsForSupplierDetails.aspx` stránky, pomocí nového ovládacího prvku ObjectDataSource s názvem `ProductsBySupplierDataSource` , který vyvolá `GetProductsBySupplierID(supplierID)` metodu z `ProductsBLL` třídy.

[![Přidat nový prvek ObjectDataSource s názvem ProductsBySupplierDataSource](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**Obrázek 8**: Přidání nového prvku ObjectDataSource pojmenovaného `ProductsBySupplierDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image22.png))

[![Vyberte třídu ProductsBLL](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**Obrázek 9**: vyberte `ProductsBLL` třídu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image25.png)).

[![Má ObjectDataSource vyvolat metodu GetProductsBySupplierID (KódDodavatele)](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**Obrázek 10**: prvek ObjectDataSource vyvolá `GetProductsBySupplierID(supplierID)` metodu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image28.png)).

Poslední krok průvodce konfigurací zdroje dat vás vyzve k zadání zdroje `GetProductsBySupplierID(supplierID)` *`supplierID`* parametru metody. Chcete-li použít hodnotu QueryString, nastavte zdroj parametru na hodnotu QueryString a zadejte název hodnoty řetězce dotazu, který chcete použít v textovém poli vlastnost QueryStringField ( `SupplierID` ).

[![Naplnit hodnotu parametru ČísloDodavatele z hodnoty QueryString řetězce KódDodavatele](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**Obrázek 11**: naplňte *`supplierID`* hodnotu parametru z `SupplierID` hodnoty QueryString ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image31.png)).

A je to! Obrázek 12 `ProductsForSupplierDetails.aspx` : po navštívení se stránka zobrazí kliknutím na odkaz Tokio Traders z `SupplierListMaster.aspx` .

[![Zobrazí se produkty dodávané obchodníci z Brna.](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**Obrázek 12**: zobrazí se produkty dodávané pomocí Brna Traders ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-vb/_static/image34.png)

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Zobrazení informací o dodavateli v`ProductsForSupplierDetails.aspx`

Jak ukazuje obrázek 12, `ProductsForSupplierDetails.aspx` Stránka jednoduše zobrazuje seznam produktů, které jsou zadány `SupplierID` ve formátu QueryString. Někdo odeslaný přímo na tuto stránku ale neví, že na obrázku 12 se zobrazuje produkty z Brna Traders. Aby bylo možné tento problém vyřešit, můžeme na této stránce zobrazit také informace o dodavateli.

Začněte přidáním třídy FormView nad ovládací prvek prvků pro produkty. Vytvořte nový ovládací prvek ObjectDataSource s názvem `SuppliersDataSource` , který vyvolá `SuppliersBLL` metodu třídy `GetSupplierBySupplierID(supplierID)` .

[![Vyberte třídu SuppliersBLL](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**Obrázek 13**: vyberte `SuppliersBLL` třídu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image37.png)).

[![Má ObjectDataSource vyvolat metodu GetSupplierBySupplierID (KódDodavatele)](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**Obrázek 14**: Chcete-li, aby prvek ObjectDataSource vyvolal `GetSupplierBySupplierID(supplierID)` metodu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image40.png))

Stejně jako u `ProductsBySupplierDataSource` *`supplierID`* parametru má parametr přiřazenou hodnotu `SupplierID` hodnoty QueryString.

[![Naplnit hodnotu parametru ČísloDodavatele z hodnoty QueryString řetězce KódDodavatele](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**Obrázek 15**: naplňte *`supplierID`* hodnotu parametru z `SupplierID` hodnoty QueryString ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image43.png)).

Při vázání třídy FormView na prvek ObjectDataSource v zobrazení Návrh aplikace Visual Studio automaticky vytvoří `ItemTemplate` webové ovládací prvky FormView, a `InsertItemTemplate` `EditItemTemplate` s popiskem a TextBox pro každé z datových polí vrácených prvkem ObjectDataSource. Vzhledem k tomu, že chceme pouze zobrazit informace o dodavatelích, je třeba odebrat `InsertItemTemplate` a `EditItemTemplate` . Dále upravte hodnotu ItemTemplate tak, aby zobrazila název společnosti dodavatele v `<h3>` prvku a adresu, město, zemi a telefonní číslo pod názvem společnosti. Alternativně můžete ručně nastavit `DataSourceID` a vytvořit kód třídy FormView `ItemTemplate` , stejně jako v kurzu[zobrazení dat pomocí prvku ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md).

Po úpravách deklarativních značek třídy FormView by měl vypadat nějak takto:

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

Obrázek 16 ukazuje snímek obrazovky `ProductsForSupplierDetails.aspx` stránky po zahrnutí informací o dodavateli.

[![Seznam produktů obsahuje souhrnné informace o dodavateli.](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**Obrázek 16**: seznam produktů obsahuje souhrnné informace o dodavateli ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image46.png)).

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Použití konečných vylepšení `ProductsForSupplierDetails.aspx` uživatelského rozhraní

Chcete-li zlepšit uživatelské prostředí pro tuto sestavu, je nutné provést několik dalších přidání na `ProductsForSupplierDetails.aspx` stránku. V současné době může uživatel přejít ze `ProductsForSupplierDetails.aspx` stránky zpátky na seznam dodavatelů kliknutím na tlačítko zpět v prohlížeči. Pojďme na `ProductsForSupplierDetails.aspx` stránku, která odkazuje zpátky, přidat ovládací prvek hypertextový odkaz, který uživateli umožní vrátit se `SupplierListMaster.aspx` k hlavnímu seznamu.

[![Přidání ovládacího prvku hypertextový odkaz, který uživateli převezme zpátky do SupplierListMaster. aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**Obrázek 17**: Přidání ovládacího prvku hypertextový odkaz, který uživateli převezme zpátky `SupplierListMaster.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-vb/_static/image49.png))

Pokud uživatel klikne na odkaz Zobrazit produkty pro dodavatele, který nemá žádné produkty, `ProductsBySupplierDataSource` prvek ObjectDataSource v `ProductsForSupplierDetails.aspx` nevrátí žádné výsledky. Ovládací prvek GridView vázaný na prvek ObjectDataSource nevytiskne žádný kód, který je v prohlížeči uživatele v prázdné oblasti na stránce. Aby bylo zřejmé, že se k tomuto dodavateli nevztahují žádné produkty, můžeme nastavit vlastnost prvku GridView `EmptyDataText` na zprávu, kterou chcete zobrazit, pokud taková situace nastane. Tato vlastnost jsem nastavila na hodnotu neexistují žádné produkty poskytované tímto dodavatelem.

Ve výchozím nastavení poskytují všichni dodavatelé v databázi Northwind alespoň jeden produkt. V tomto kurzu jsme ale ručně upravili `Products` tabulku tak, že dodavatel Escargots Nouveaux už není přidružený k žádným produktům. Po provedení této změny se na obrázku 18 zobrazí stránka s podrobnostmi pro Escargots Nouveaux.

[![Uživatelům se dozvíte, že dodavatel neposkytuje žádné produkty.](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**Obrázek 18**: uživatelům se dozvíte, že dodavatel neposkytuje žádné produkty ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-vb/_static/image52.png)

## <a name="summary"></a>Souhrn

I když se v sestavách a podrobností můžou zobrazovat hlavní a podrobné záznamy na jedné stránce, na mnoha webech, které jsou oddělené na dvou webových stránkách. V tomto kurzu jsme se podívali na to, jak implementovat takovou sestavu hlavní/podrobnosti, která má dodavatele uvedené v prvku GridView v hlavní webové stránce a v přidružených produktech uvedených na stránce podrobností. Každý řádek dodavatele na hlavní webové stránce obsahoval odkaz na stránku s podrobnostmi, která byla předána do hodnoty daného řádku `SupplierID` . Tyto odkazy na konkrétní řádek lze snadno přidat pomocí HyperLinkField prvku GridView.

Na stránce podrobností načítající tyto produkty pro zadaného dodavatele bylo provedeno vyvoláním `ProductsBLL` `GetProductsBySupplierID(supplierID)` metody třídy. *`supplierID`* Hodnota parametru byla určena deklarativně pomocí řetězce dotazu jako zdroje parametru. Zjistili jsme také, jak zobrazit podrobnosti o dodavatelích na stránce podrobností pomocí FormView.

Náš [Další kurz](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) je konečným řešením pro hlavní a podrobné sestavy. Podíváme se na to, jak zobrazit seznam produktů v prvku GridView, kde každý řádek obsahuje tlačítko pro výběr. Po kliknutí na tlačítko vybrat se zobrazí podrobnosti o tomto produktu v ovládacím prvku DetailsView na stejné stránce.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na adrese [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, umístěte mi čáru na [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-with-two-dropdownlists-vb.md) 
>  [Další](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
