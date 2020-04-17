---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Ovládací prvky vázané na data | Dokumenty společnosti Microsoft
author: rick-anderson
description: Většina ASP.NET aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data byly klíčovou součástí interakce w...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 941e2ed15b3da28991e7b06cbab570eb1b5b8899
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543077"
---
# <a name="data-bound-controls"></a>Ovládací prvky svázané s daty

podle [společnosti Microsoft](https://github.com/microsoft)

> Většina ASP.NET aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data byly klíčovou součástí interakce s daty v dynamických webových aplikacích. ASP.NET 2.0 zavádí některá podstatná vylepšení ovládacích prvků vázaných na data, včetně nové třídy BaseDataBoundControl a deklarativní syntaxe.

Většina ASP.NET aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data byly klíčovou součástí interakce s daty v dynamických webových aplikacích. ASP.NET 2.0 zavádí některá podstatná vylepšení ovládacích prvků vázaných na data, včetně nové třídy BaseDataBoundControl a deklarativní syntaxe.

BaseDataBoundControl funguje jako základní třída pro třídu DataBoundControl a třídu HierarchicalDataBoundControl. V tomto modulu budeme diskutovat o následující třídy, které jsou odvozeny z DataBoundControl:

- Adrotator
- Ovládací prvky seznamu
- GridView
- Formview
- Detailsview

Budeme také diskutovat o následující třídy, které jsou odvozeny z HierarchicalDataBoundControl třídy:

- TreeView
- Nabídka
- Sitemappath

## <a name="databoundcontrol-class"></a>Třída DataBoundControl

Třída DataBoundControl je abstraktní třída (označená MustInherit v VB) používaná k interakci s daty tabulkového nebo listového stylu. Následující ovládací prvky jsou některé z ovládacích prvků, které jsou odvozeny z DataBoundControl.

## <a name="adrotator"></a>Adrotator

Ovládací prvek AdRotator umožňuje zobrazit grafický nápis na webové stránce, která je propojena s konkrétní adresou URL. Zobrazená grafika je otočena pomocí vlastností ovládacího prvku. Četnost zobrazování konkrétní reklamy na stránce lze konfigurovat pomocí **služby Zobrazení** a reklamy lze filtrovat pomocí filtrování klíčových slov.

Ovládací prvky AdRotator používají pro data soubor XML nebo tabulku v databázi. Následující atributy se používají v souborech XML ke konfiguraci ovládacího prvku AdRotator.

### <a name="imageurl"></a>Imageurl
Adresa URL obrázku, který se má zobrazit pro reklamu.

### <a name="navigateurl"></a>Navigateurl
Adresa URL, na kterou by měl uživatel při kliknutí na reklamu převzít. Tato adresa by měla být kódována jako adresa URL.

### <a name="alternatetext"></a>Alternatetext
Alternativní text, který je zobrazen v popisku a přečten programy pro čtení z obrazovky. Zobrazí se také v případě, že obrázek určený imageurl není k dispozici.

### <a name="keyword"></a>Klíčové slovo
Definuje klíčové slovo, které lze použít při použití filtrování klíčových slov. Pokud je zadáno, zobrazí se pouze reklamy s klíčovým slovem odpovídajícím filtru klíčových slov.

### <a name="impressions"></a>Dojmy
Váhové číslo, které určuje, jak často se určitá avisla konkrétní reklama pravděpodobně zobrazí. Je to vzhledem k dojmu jiných reklam ve stejném souboru. Maximální hodnota kolektivních zobrazení pro všechny reklamy v souboru XML je 2 048 000 000 1.

### <a name="height"></a>Vlastnost Height
Výška reklamy v pixelech.

### <a name="width"></a>impulzu
Šířka reklamy v pixelech.

> [!NOTE]
> Atributy Výška a Šířka přepíší výšku a šířku samotného ovládacího prvku AdRotator.

Typický soubor XML může vypadat takto:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

Ve výše uvedeném příkladu je pravděpodobnost, že se ad pro contoso zobrazí dvakrát častěji než u reklamy na web ASP.NET, protože hodnota atributu Zobrazení je.

Chcete-li zobrazit reklamy z výše uvedeného souboru XML, přidejte na stránku ovládací prvek AdRotator a nastavte vlastnost **AdvertisementFile** tak, aby ukazovala na soubor XML, jak je znázorněno níže:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

Pokud se rozhodnete použít databázovou tabulku jako zdroj dat pro ovládací prvek AdRotator, budete muset nejprve nastavit databázi pomocí následujícího schématu:

| **Název sloupce** | **Datový typ** | **Popis** |
| --- | --- | --- |
| ID | int | Primární klíč. Tento sloupec může mít libovolný název. |
| Imageurl | nvarchar(*délka*) | Relativní nebo absolutní adresa URL obrázku, který se má pro reklamu zobrazit. |
| Navigateurl | nvarchar(*délka*) | Cílová adresa URL reklamy. Pokud hodnotu nezadáte, není to hypertextový odkaz. |
| Alternatetext | nvarchar(*délka*) | Text zobrazený v případě, že obrázek nelze najít. V některých prohlížečích je text zobrazen jako popis. Alternativní text se také používá pro usnadnění přístupu, takže uživatelé, kteří nevidí grafiku, mohou slyšet její popis číst nahlas. |
| Klíčové slovo | nvarchar(*délka*) | Kategorie reklamy, na kterou může stránka filtrovat. |
| Dojmy | int(4) | Číslo, které označuje pravděpodobnost, jak často se bude reklama zobrazovat. Čím větší číslo, tím častěji se bude zobrazovat. Celkový počet všech hodnot zobrazení v souboru XML nesmí překročit 2 048 000 000 – 1. |
| impulzu | int(4) | Šířka obrazu v obrazových bodech. |
| Vlastnost Height | int(4) | Výška obrazu v obrazových bodech. |

V případech, kdy již máte databázi s jiným schématem, můžete použít **vlastnosti AlternateTextField**, **ImageUrlField**a **NavigateUrlField** k mapování atributů AdRotator na existující databázi. Chcete-li zobrazit data z databáze v ovládacím prvku AdRotator, přidejte na stránku ovládací prvek zdroje dat, nakonfigurujte připojovací řetězec pro ovládací prvek zdroje dat tak, aby ukazoval na databázi, a nastavte vlastnost **DataSourceID** ovládacího prvku AdRotator na ID ovládacího prvku zdroje dat. V případech, kdy je třeba nakonfigurovat reklamy AdRotator programově, použijte událost AdCreated. Událost AdCreated má dva parametry; jeden objekt a druhý instance AdCreatedEventArgs. AdCreatedEventArgs je odkaz na vytvářenou reklamu.

Následující fragment kódu nastaví imageUrl, NavigateUrl a AlternateText pro ad programově:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Ovládací prvky seznamu

Ovládací prvky seznamu zahrnují list, dropdownlist, checkboxlist, radiobuttonlist a bulletedlist. Každý z těchto ovládacích prvků může být data vázána na zdroj dat. Jako zobrazovaný text používají jedno pole ve zdroji dat a volitelně mohou použít druhé pole jako hodnotu položky. Položky lze také přidat staticky v době návrhu a můžete kombinovat statické položky a dynamické položky přidané ze zdroje dat.

Chcete-li svázat data ovládacího prvku seznamu, přidejte na stránku ovládací prvek zdroje dat. Zadejte příkaz SELECT pro ovládací prvek zdroje dat a nastavte vlastnost DataSourceID ovládacího prvku seznamu na ID ovládacího prvku zdroje dat. Pomocí vlastností **DataTextField** a **DataValueField** definujte zobrazovaný text a hodnotu ovládacího prvku. Kromě toho můžete použít **Vlastnost DataTextFormatString** k řízení vzhledu zobrazovaného textu následujícím způsobem:

| **Expression** | **Popis** |
| --- | --- |
| Cena:{0:C} | Pro číselná/desetinná data. Zobrazí literál "Cena:" následovaný čísly ve formátu měny. Formát měny závisí na nastavení jazykové verze zadané v atributu jazykové verze na **stránce Page** nebo v souboru Web.config. |
| {0:D4} | Pro celá data. Nelze použít s desetinnými čísly. Celá čísla jsou zobrazena v poli s nulovým předu, které je široké čtyři znaky. |
| {0:N2}% | Pro číselná data. Zobrazí číslo s přesností dvou desetinných míst následované literálem %. |
| {0:000.0} | Pro číselná/desetinná data. Čísla jsou zaokrouhlena na jedno desetinné místo. Čísla menší než tři číslice jsou s nulovým polstrovaným. |
| {0:D} | Pro data data a čas. Zobrazuje formát dlouhého data ("Čtvrtek, srpen 06, 1996"). Formát data závisí na nastavení jazykové verze stránky nebo souboru Web.config. |
| {0:d} | Pro data data a čas. Zobrazuje krátký formát data ("12/31/99"). |
| {0:yy-MM-dd} | Pro data data a čas. Zobrazuje datum v číselném formátu měsíce -měsíc (96-08-06) |

## <a name="gridview"></a>GridView

Ovládací prvek GridView umožňuje zobrazení a úpravy tabulkových dat pomocí deklarativního přístupu a je následníkem ovládacího prvku DataGrid. Následující funkce jsou k dispozici v gridview ovládacího prvku.

- Vazba na ovládací prvky zdroje dat, jako je například SqlDataSource.
- Integrované možnosti řazení.
- Integrované možnosti aktualizace a odstranění.
- Integrované možnosti stránkování.
- Vestavěné možnosti výběru řádků.
- Programový přístup k objektovému modelu GridView k dynamickému nastavení vlastností, zpracování událostí a tak dále.
- Více klíčových polí.
- Více datových polí pro sloupce hypertextového odkazu.
- Přizpůsobitelný vzhled prostřednictvím motivů a stylů.

**Sloupcová pole**

Každý sloupec v ovládacím prvku GridView je reprezentován objektem DataControlField. Ve výchozím nastavení je vlastnost AutoGenerateColumns nastavena na **hodnotu true**, která vytvoří objekt AutoGeneratedField pro každé pole ve zdroji dat. Každé pole je pak vykresleno jako sloupec v ovládacím prvku GridView v pořadí, ve které se každé pole zobrazí ve zdroji dat. Můžete také ručně určit, která sloupcová pole se zobrazí v ovládacím prvku **GridView** nastavením vlastnosti **AutoGenerateColumns** na **false** a definováním vlastní kolekce sloupcových polí. Chování sloupců v ovládacím prvku určují různé typy sloupců.

V následující tabulce jsou uvedeny různé typy sloupcových polí, které lze použít.

| **Typ pole sloupce** | **Popis** |
| --- | --- |
| Boundfield | Zobrazí hodnotu pole ve zdroji dat. Toto je výchozí typ sloupce ovládacího prvku GridView. |
| Buttonfield | Zobrazí příkazové tlačítko pro každou položku v ovládacím prvku GridView. To umožňuje vytvořit sloupec vlastních ovládacích prvků tlačítek, například tlačítko Přidat nebo Odebrat. |
| Checkboxfield | Zobrazí zaškrtávací políčko pro každou položku v ovládacím prvku GridView. Tento typ sloupcového pole se běžně používá k zobrazení polí s logickou hodnotou. |
| Commandfield | Zobrazí předdefinovaná příkazová tlačítka pro provádění operací výběru, úprav nebo odstranění. |
| Hyperlinkfield | Zobrazí hodnotu pole ve zdroji dat jako hypertextový odkaz. Tento typ sloupcového pole umožňuje svázat druhé pole s adresou URL hypertextového odkazu. |
| Imagefield | Zobrazí obrázek pro každou položku v ovládacím prvku GridView. |
| Templatefield | Zobrazí uživatelem definovaný obsah pro každou položku v ovládacím prvku GridView podle zadané šablony. Tento typ sloupcového pole umožňuje vytvořit vlastní sloupcové pole. |

Chcete-li deklarativně definovat kolekci sloupcových polí, nejprve přidejte otevírací a uzavírací ** &lt;značky Columns&gt; ** mezi otevírací a uzavírací značky ovládacího prvku GridView. Dále uveďte sloupcová pole, která chcete zahrnout mezi otevírací a uzavírací ** &lt;značky Sloupce.&gt; ** Zadané sloupce jsou přidány do kolekce Sloupce v uvedeném pořadí. Kolekce **Columns** ukládá všechna sloupcová pole v ovládacím prvku a umožňuje programově spravovat sloupcová pole v ovládacím prvku GridView.

Explicitně deklarovaná sloupcová pole mohou být zobrazena v kombinaci s automaticky generovanými sloupcovými poli. Při použití obou jsou explicitně deklarovaná sloupcová pole vykreslena jako první následovaná automaticky generovanými sloupcovými poli.

## <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek GridView může být vázán na ovládací prvek zdroje dat (například **SqlDataSource**, **ObjectDataSource**a tak dále), stejně jako jakýkoli zdroj dat, který implementuje rozhraní System.Collections.IEnumerable (například System.Data.DataView, System.Collections.ArrayList nebo System.Collections.Hashtable). Pomocí jedné z následujících metod svázat Ovládací prvek GridView na příslušný typ zdroje dat:

- Chcete-li vytvořit vazbu na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku GridView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek GridView se automaticky váže na zadaný ovládací prvek zdroje dat a může využít možnosti ovládacího prvku zdroje dat k provádění funkcí řazení, aktualizace, odstranění a stránkování. Toto je upřednostňovaná metoda pro vazbu na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní System.Collections.IEnumerable, programově nastavte vlastnost DataSource ovládacího prvku GridView na zdroj dat a pak zavolejte metodu DataBind. Při použití této metody ovládací prvek GridView neposkytuje integrované řazení, aktualizace, odstranění a stránkování funkce. Tuto funkci je třeba zadat sami.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek GridView poskytuje mnoho předdefinovaných funkcí, které umožňují uživateli řadit, aktualizovat, odstraňovat, vybírat a stránkovat mezi položkami v ovládacím prvku. Když je ovládací prvek GridView svázaný s ovládacím prvkem zdroje dat, ovládací prvek GridView může využít možnosti ovládacího prvku zdroje dat a poskytnout funkce automatického řazení, aktualizace a odstranění.

> [!NOTE]
> Ovládací prvek GridView může poskytovat podporu pro řazení, aktualizaci a odstranění s jinými typy zdrojů dat; však budete muset poskytnout odpovídající obslužnou rutinu události s implementací pro tyto operace.

Řazení umožňuje uživateli seřadit položky v ovládacím prvku GridView s ohledem na konkrétní sloupec kliknutím na záhlaví sloupce. Chcete-li povolit řazení, nastavte vlastnost AllowSorting na **hodnotu true**.

Funkce automatických aktualizací, odstranění a výběru jsou povoleny po klepnutí na tlačítko ve sloupcovém poli **ButtonField** nebo **TemplateField** s názvem příkazu "Upravit", "Odstranit" a "Vybrat". Ovládací prvek GridView může automaticky přidat **sloupcové** pole CommandField s tlačítkem Upravit, Odstranit nebo Vybrat, pokud je vlastnost AutoGenerateEditButton, AutoGenerateDeleteButton nebo AutoGenerateSelectButton nastavena na **hodnotu true**.

> [!NOTE]
> Vkládání záznamů do zdroje dat není přímo podporováno ovládacím prvkem GridView. Je však možné vložit záznamy pomocí GridView ovládacího prvku ve spojení s Ovládací prvek DetailsView nebo FormView.

Namísto zobrazení všech záznamů ve zdroji dat současně gridview ovládací prvek může automaticky rozdělit záznamy do stránek. Chcete-li povolit stránkování, nastavte vlastnost AllowPaging na **hodnotu true**.

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Vzhled ovládacího prvku GridView můžete přizpůsobit nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Stylu** | **Popis** |
| --- | --- |
| Alternatingrowstyle | Nastavení stylu pro řádky střídavých dat v ovládacím prvku GridView. Pokud je tato vlastnost nastavena, řádky dat se zobrazí střídavě mezi rowstyle nastavení a **alternatingRowStyle** nastavení. |
| Editrowstyle | Nastavení stylu pro řádek upravovaný v ovládacím prvku GridView. |
| Emptydatarowstyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku GridView, pokud zdroj dat neobsahuje žádné záznamy. |
| Footerstyle | Nastavení stylu pro řádek zápatí ovládacího prvku GridView. |
| Headerstyle | Nastavení stylu pro řádek záhlaví ovládacího prvku GridView. |
| Pagerstyle | Nastavení stylu pro řádek operátoru ovládacího prvku GridView. |
| Rowstyle | Nastavení stylu pro řádky dat v ovládacím prvku GridView. Když **alternatingRowStyle** vlastnost je také nastavena, řádky dat jsou zobrazeny střídavě mezi **RowStyle** nastavení a **AlternatingRowStyle** nastavení. |
| SelectedRowStyle | Nastavení stylu pro vybraný řádek v ovládacím prvku GridView. |

Můžete také zobrazit nebo skrýt různé části ovládacího prvku. V následující tabulce jsou uvedeny vlastnosti, které řídí, které části jsou zobrazeny nebo skryty.

| **Vlastnost** | **Popis** |
| --- | --- |
| Zobrazit | Zobrazí nebo skryje oddíl zápatí ovládacího prvku GridView. |
| Showheader | Zobrazí nebo skryje část záhlaví ovládacího prvku GridView. |

### <a name="events"></a>Události

Ovládací prvek GridView poskytuje několik událostí, které můžete programovat proti. To umožňuje spustit vlastní rutiny vždy, když dojde k události. V následující tabulce jsou uvedeny události podporované ovládacím prvkem GridView.

| **Událost** | **Popis** |
| --- | --- |
| Pageindexchanged | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale po gridview ovládacíprvek zpracovává stránkovací operace. Tato událost se běžně používá, když potřebujete provést úkol poté, co uživatel přejde na jinou stránku v ovládacím prvku. |
| Změna indexu stránky | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale před gridview ovládací prvek zpracovává stránkování operace. Tato událost se často používá ke zrušení operace stránkování. |
| Rowcancelingedit | Vyvolá se při klepnutí na tlačítko Storno řádku, ale před ukončením režimu úprav ovládacího prvku GridView. Tato událost se často používá k zastavení operace zrušení. |
| Rowcommand | Vyvolá se při klepnutí na tlačítko v ovládacím prvku GridView. Tato událost se často používá k provedení úkolu při klepnutí na tlačítko v ovládacím prvku. |
| RowCreated | Vyvolá se při vytvoření nového řádku v ovládacím prvku GridView. Tato událost se často používá k úpravě obsahu řádku při vytvoření řádku. |
| RowDataBound | Vyvolá se, když je řádek dat vázán na data v ovládacím prvku GridView. Tato událost se často používá k úpravě obsahu řádku, když je řádek vázán na data. |
| Rowdeleted | Vyvolá se při klepnutí na tlačítko Odstranit v řádku, ale po ovládacím prvku GridView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| Rowdeleting | Vyvolá se při klepnutí na tlačítko Odstranit v řádku, ale před tím, než ovládací prvek GridView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| Rowediting | Vyvolá se, když klepnete na tlačítko Upravit řádku, ale před vstupem ovládacího prvku GridView do režimu úprav. Tato událost se často používá ke zrušení operace úprav. |
| Rowupdated | Vyvolá se při klepnutí na tlačítko Aktualizovat řádku, ale po GridView ovládací prvek aktualizuje řádek. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| Rowupdating | Vyvolá se při klepnutí na tlačítko Aktualizovat řádku, ale před GridView ovládací prvek aktualizuje řádek. Tato událost se často používá ke zrušení operace aktualizace. |
| Selectedindexchanged | Vyvolá se při klepnutí na tlačítko Vybrat řádku, ale po gridview ovládacího prvku zpracovává operaci výběru. Tato událost se často používá k provedení úkolu po výběru řádku v ovládacím prvku. |
| Selectedindexchanging | Vyvolá se při klepnutí na tlačítko Vybrat řádku, ale před gridview ovládacíprvek zpracovává operaci výběru. Tato událost se často používá ke zrušení operace výběru. |
| Seřazeny | Vyvolá se při klepnutí na hypertextový odkaz na řazení sloupce, ale po gridview ovládacího prvku zpracovává operaci řazení. Tato událost se běžně používá k provedení úkolu poté, co uživatel klepne na hypertextový odkaz pro řazení sloupce. |
| Řazení | Vyvolá se při klepnutí na hypertextový odkaz na řazení sloupce, ale před gridview ovládacíprvek zpracovává operaci řazení. Tato událost se často používá ke zrušení operace řazení nebo k provedení vlastní rutiny řazení. |

## <a name="formview"></a>Formview

Ovládací prvek FormView se používá k zobrazení jednoho záznamu ze zdroje dat. Je podobný ovládacímu prvku DetailsView, s tím rozdílem, že zobrazuje uživatelem definované šablony namísto řádkových polí. Vytváření vlastních šablon poskytuje větší flexibilitu při řízení způsobu zobrazení dat. Ovládací prvek FormView podporuje následující funkce:

- Vazba na ovládací prvky zdroje dat, jako je například SqlDataSource a ObjectDataSource.
- Integrované možnosti vkládání.
- Integrované možnosti aktualizace a odstranění.
- Integrované možnosti stránkování.
- Programový přístup k objektovému modelu FormView k dynamickému nastavení vlastností, zpracování událostí a tak dále.
- Přizpůsobitelný vzhled prostřednictvím uživatelem definovaných šablon, motivů a stylů.

## <a name="templates"></a>Šablony

Aby ovládací prvek FormView zobrazoval obsah, je třeba vytvořit šablony pro různé části ovládacího prvku. Většina šablon je nepovinná; je však nutné vytvořit šablonu pro režim, ve kterém je ovládací prvek nakonfigurován. Například ovládací prvek FormView, který podporuje vkládání záznamů, musí mít definovánu šablonu položky vložení. V následující tabulce jsou uvedeny různé šablony, které můžete vytvořit.

| **Typ šablony** | **Popis** |
| --- | --- |
| Edititemtemplate | Definuje obsah pro řádek dat, když je ovládací prvek FormView v režimu úprav. Tato šablona obvykle obsahuje vstupní ovládací prvky a příkazová tlačítka, pomocí kterých může uživatel upravovat existující záznam. |
| Emptydatatemplate | Definuje obsah prázdného řádku dat zobrazeného, když je ovládací prvek FormView svázán se zdrojem dat, který neobsahuje žádné záznamy. Tato šablona obvykle obsahuje obsah, který uživatele upozorní, že zdroj dat neobsahuje žádné záznamy. |
| Footertemplate | Definuje obsah pro řádek zápatí. Tato šablona obvykle obsahuje další obsah, který chcete zobrazit v řádku zápatí. Jako alternativu můžete jednoduše určit text, který se má zobrazit v řádku zápatí, nastavením vlastnosti FooterText. |
| Headertemplate | Definuje obsah pro řádek záhlaví. Tato šablona obvykle obsahuje jakýkoli další obsah, který chcete zobrazit v řádku záhlaví. Jako alternativu můžete jednoduše určit text, který se má zobrazit v řádku záhlaví, nastavením vlastnosti HeaderText. |
| Itemtemplate | Definuje obsah pro řádek dat, když je ovládací prvek FormView v režimu jen pro čtení. Tato šablona obvykle obsahuje obsah pro zobrazení hodnot existujícího záznamu. |
| Insertitemtemplate | Definuje obsah pro řádek dat, když je ovládací prvek FormView v režimu vložení. Tato šablona obvykle obsahuje vstupní ovládací prvky a příkazová tlačítka, pomocí kterých může uživatel přidat nový záznam. |
| Pagertemplate | Definuje obsah řádku operátoru zobrazeného při povolení funkce stránkování (pokud je vlastnost AllowPaging nastavena na **hodnotu true**). Tato šablona obvykle obsahuje ovládací prvky, pomocí kterých může uživatel přejít na jiný záznam. |

Vstupní ovládací prvky v šabloně upravit položku a vložit šablonu položky mohou být vázány na pole zdroje dat pomocí výrazu obousměrné vazby. To umožňuje Ovládací prvek FormView automaticky extrahovat hodnoty vstupního ovládacího prvku pro operaci aktualizace nebo vložení. Obousměrné výrazy vazeb také umožňují, aby vstupní ovládací prvky v šabloně upravit položku automaticky zobrazovaly původní hodnoty polí.

### <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek FormView může být vázán na ovládací prvek zdroje dat (například **SqlDataSource**, AccessDataSource, **ObjectDataSource** a tak dále) nebo na libovolný zdroj dat, který implementuje rozhraní System.Collections.IEnumerable (například System.Data.DataView, System.Collections.ArrayList a System.Collections.Hashtable). Pomocí jedné z následujících metod svázat Ovládací prvek FormView na příslušný typ zdroje dat:

- Chcete-li vytvořit vazbu na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku FormView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek FormView se automaticky váže na zadaný ovládací prvek zdroje dat a může využít možnosti ovládacího prvku zdroje dat k provádění funkcí vkládání, aktualizace, odstranění a stránkování. Toto je upřednostňovaná metoda pro vazbu na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní **System.Collections.IEnumerable,** programově nastavte vlastnost DataSource ovládacího prvku FormView na zdroj dat a pak zavolejte metodu DataBind. Při použití této metody ovládací prvek FormView neposkytuje integrované vkládání, aktualizace, odstranění a stránkování funkce. Tuto funkci je třeba zadat pomocí příslušné události.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek FormView poskytuje mnoho předdefinovaných funkcí, které umožňují uživateli aktualizovat, odstranit, vložit a stránkovat prostřednictvím položek v ovládacím prvku. Pokud je ovládací prvek FormView svázán s ovládacím prvkem zdroje dat, ovládací prvek FormView může využít možnosti ovládacího prvku zdroje dat a poskytnout automatické aktualizace, odstranění, vložení a stránkování funkce. Ovládací prvek FormView může poskytovat podporu pro operace aktualizace, odstranění, vložení a stránkování s jinými typy zdrojů dat; však je nutné poskytnout odpovídající obslužnou rutinu události s implementací pro tyto operace.

Vzhledem k tomu, že ovládací prvek FormView používá šablony, neposkytuje způsob, jak automaticky generovat příkazová tlačítka k provádění operací aktualizace, odstranění nebo vložení. Tato příkazová tlačítka je nutné ručně zahrnout do příslušné šablony. Ovládací prvek FormView rozpozná určitá tlačítka, která mají vlastnosti **CommandName** nastavené na určité hodnoty. V následující tabulce jsou uvedena příkazová tlačítka, která ovládací prvek FormView rozpozná.

| **Tlačítko** | **Hodnota Commandname** | **Popis** |
| --- | --- | --- |
| Zrušit | "Zrušit" | Používá se při aktualizaci nebo vložení operací ke zrušení operace a k zahození hodnot zadaných uživatelem. Ovládací prvek FormView se pak vrátí do režimu určeného vlastností DefaultMode. |
| Odstranit | "Odstranit" | Používá se při odstraňování operací k odstranění zobrazeného záznamu ze zdroje dat. Vyvolá ItemDeleting a ItemDeleted události. |
| Upravit | "Upravit" | Používá se při aktualizaci operací, aby ovládací prvek FormView v režimu úprav. Obsah zadaný ve vlastnosti **EditItemTemplate** se zobrazí pro řádek dat. |
| Vložit | "Vložit" | Používá se při vkládání operací k pokusu o vložení nového záznamu do zdroje dat pomocí hodnot poskytnutých uživatelem. Vyvolá iteminserting a ItemInserted události. |
| Nová | "Nový" | Používá se při vkládání operací pro vložení ovládacího prvku FormView do režimu vložení. Obsah zadaný ve vlastnosti **InsertItemTemplate** se zobrazí pro řádek dat. |
| stránka | "Stránka" | Používá se v operacích stránkování představující tlačítko v řádku operátoru, který provádí stránkování. Chcete-li určit operaci stránkování, nastavte vlastnost **CommandArgument** tlačítka na "Další", "Předchozí", "První", "Poslední" nebo index stránky, na kterou chcete přejít. Vyvolá události PageIndexChanging a PageIndexChanged. |
| Aktualizace | "Aktualizace" | Používá se při aktualizaci operací k pokusu o aktualizaci zobrazeného záznamu ve zdroji dat s hodnotami poskytnutými uživatelem. Vyvolá itemUpdating a ItemUpdated události. |

Na rozdíl od tlačítka Odstranit (které okamžitě odstraní zobrazený záznam) po klepnutí na tlačítko Upravit nebo Nový přejde ovládací prvek FormView do režimu úprav nebo vložení. V režimu úprav se pro aktuální datovou položku zobrazí obsah obsažený ve vlastnosti **EditItemTemplate.** Šablona upravit položku je obvykle definována tak, že tlačítko Upravit je nahrazeno tlačítkem Aktualizovat a Storno. Vstupní ovládací prvky, které jsou vhodné pro datový typ pole (například TextBox nebo Ovládací prvek CheckBox) jsou také obvykle zobrazeny s hodnotou pole, kterou může uživatel upravit. Kliknutím na tlačítko Aktualizovat aktualizujete záznam ve zdroji dat a klepnutím na tlačítko Storno se všechny změny přerušíte.

Podobně obsah obsažený ve vlastnosti **InsertItemTemplate** se zobrazí pro datovou položku, když je ovládací prvek v režimu vložení. Šablona vložit položku je obvykle definována tak, že tlačítko Nový je nahrazeno tlačítkem Vložit a Storno a uživateli se zobrazí prázdné vstupní ovládací prvky pro zadání hodnot nového záznamu. Klepnutím na tlačítko Vložit vložíte záznam do zdroje dat, zatímco klepnutím na tlačítko Storno přenecháte všechny změny.

Ovládací prvek FormView poskytuje funkci stránkování, která umožňuje uživateli přejít na jiné záznamy ve zdroji dat. Pokud je povoleno, řádek operátoru se zobrazí v ovládacím prvku FormView, který obsahuje ovládací prvky navigace stránky. Chcete-li povolit stránkování, nastavte vlastnost **AllowPaging** na **hodnotu true**. Řádek operátoru můžete přizpůsobit nastavením vlastností objektů obsažených ve vlastnostech PagerStyle a PagerSettings. Namísto použití vestavěného uživatelského uživatelského nastavení řádku operátoru můžete vytvořit vlastní uživatelské tlačítko pomocí vlastnosti **PagerTemplate.**

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Vzhled ovládacího prvku FormView můžete přizpůsobit nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Stylu** | **Popis** |
| --- | --- |
| Editrowstyle | Nastavení stylu pro řádek dat, když je ovládací prvek FormView v režimu úprav. |
| Emptydatarowstyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku FormView, pokud zdroj dat neobsahuje žádné záznamy. |
| Footerstyle | Nastavení stylu pro řádek zápatí ovládacího prvku FormView. |
| Headerstyle | Nastavení stylu pro řádek záhlaví ovládacího prvku FormView. |
| Insertrowstyle | Nastavení stylu pro řádek dat, když je ovládací prvek FormView v režimu vložení. |
| Pagerstyle | Nastavení stylu pro řádek operátoru zobrazené v ovládacím prvku FormView, když je povolena funkce stránkování. |
| Rowstyle | Nastavení stylu pro řádek dat, když je ovládací prvek FormView v režimu jen pro čtení. |

## <a name="events"></a>Události

Ovládací prvek FormView poskytuje několik událostí, které můžete programovat proti. To umožňuje spustit vlastní rutiny vždy, když dojde k události. V následující tabulce jsou uvedeny události podporované ovládacím prvkem FormView.

| **Událost** | **Popis** |
| --- | --- |
| Itemcommand | Vyvolá se při klepnutí na tlačítko v ovládacím prvku FormView. Tato událost se často používá k provedení úkolu při klepnutí na tlačítko v ovládacím prvku. |
| Itemcreated | Vyvolá se po vytvoření všech objektů FormViewRow v ovládacím prvku FormView. Tato událost se často používá k úpravě hodnot záznamu před jeho zobrazením. |
| Itemdeleted | Vyvolá se při klepnutí na tlačítko Delete (tlačítko s vlastností **CommandName** nastavenou na "Odstranit"), ale poté, co ovládací prvek FormView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| Itemdeleting | Vyvolá se při klepnutí na tlačítko Delete, ale před ovládacím prvkem FormView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| Iteminserted | Vyvolá se při klepnutí na tlačítko Insert (tlačítko s vlastností **CommandName** nastavenou na možnost Vložit), ale poté, co ovládací prvek FormView vloží záznam. Tato událost se často používá ke kontrole výsledků operace vložení. |
| Iteminserting | Vyvolá se při klepnutí na tlačítko Vložit, ale před formview ovládací prvek vloží záznam. Tato událost se často používá ke zrušení operace vložení. |
| Itemupdated | Vyvolá se při klepnutí na tlačítko Aktualizovat (tlačítko s vlastností **CommandName** nastavenou na možnost Aktualizovat), ale po aktualizaci ovládacího prvku FormView řádek. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| Itemupdating | Vyvolá se při klepnutí na tlačítko Aktualizovat, ale před ovládacím prvkem FormView aktualizuje záznam. Tato událost se často používá ke zrušení operace aktualizace. |
| Modechanged | Vyvolá se po změně režimů ovládacího prvku FormView (pro úpravy, vložení nebo režim jen pro čtení). Tato událost se často používá k provedení úlohy při formview ovládací prvek změní režimy. |
| Modechanging | Vyvolá se před změnou režimu ovládacího prvku FormView (pro úpravy, vložení nebo režim jen pro čtení). Tato událost se často používá ke zrušení změny režimu. |
| Pageindexchanged | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale po formview ovládací prvek zpracovává stránkování operace. Tato událost se běžně používá, když potřebujete provést úkol poté, co uživatel přejde na jiný záznam v ovládacím prvku. |
| Změna indexu stránky | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale před formview ovládací prvek zpracovává stránkování operace. Tato událost se často používá ke zrušení operace stránkování. |

## <a name="detailsview"></a>Detailsview

Ovládací prvek DetailsView se používá k zobrazení jednoho záznamu ze zdroje dat v tabulce, kde je každé pole záznamu zobrazeno v řádku tabulky. Lze jej použít v kombinaci s ovládacím prvkem GridView pro scénáře hlavních podrobností. Ovládací prvek DetailsView podporuje následující funkce:

- Vazba na ovládací prvky zdroje dat, jako je například SqlDataSource.
- Integrované možnosti vkládání.
- Integrované možnosti aktualizace a odstranění.
- Integrované možnosti stránkování.
- Programový přístup k objektovému modelu DetailsView k dynamickému nastavení vlastností, zpracování událostí a tak dále.
- Přizpůsobitelný vzhled prostřednictvím motivů a stylů.

## <a name="row-fields"></a>Řádková pole

Každý řádek dat v ovládacím prvku DetailsView je vytvořen deklarováním ovládacího prvku pole. Různé typy řádkových polí určují chování řádků v ovládacím prvku. Ovládací prvky pole jsou odvozeny z pole DataControlField. V následující tabulce jsou uvedeny různé typy řádkových polí, které lze použít.

| **Typ pole sloupce** | **Popis** |
| --- | --- |
| Boundfield | Zobrazí hodnotu pole ve zdroji dat jako text. |
| Buttonfield | Zobrazí příkazové tlačítko v ovládacím prvku DetailsView. To umožňuje zobrazit řádek s vlastním ovládacím prvkem tlačítka, například tlačítko Přidat nebo Odebrat. |
| Checkboxfield | Zobrazí zaškrtávací políčko v ovládacím prvku DetailsView. Tento typ řádkového pole se běžně používá k zobrazení polí s logickou hodnotou. |
| Commandfield | Zobrazí vestavěná příkazová tlačítka pro provádění operací úprav, vkládání nebo odstraňování v ovládacím prvku DetailsView. |
| Hyperlinkfield | Zobrazí hodnotu pole ve zdroji dat jako hypertextový odkaz. Tento typ řádkového pole umožňuje svázat druhé pole s adresou URL hypertextového odkazu. |
| Imagefield | Zobrazí obrázek v ovládacím prvku DetailsView. |
| Templatefield | Zobrazí uživatelem definovaný obsah pro řádek v ovládacím prvku DetailsView podle zadané šablony. Tento typ řádkového pole umožňuje vytvořit vlastní řádkové pole. |

Ve výchozím nastavení je vlastnost AutoGenerateRows nastavena na **hodnotu true**, která automaticky generuje objekt vázaného řádkového pole pro každé pole vypovatelného typu ve zdroji dat. Platné vazby typy jsou String, DateTime, Decimal, Guid a sada primitivních typů. Každé pole je pak zobrazeno v řádku jako text v pořadí, ve kterém se každé pole zobrazí ve zdroji dat.

Automatické generování řádků poskytuje rychlý a snadný způsob zobrazení všech polí v záznamu. Chcete-li však použít rozšířené možnosti ovládacího prvku DetailsView, je nutné explicitně deklarovat řádková pole, která mají být zahrnuta do ovládacího prvku DetailsView. Chcete-li deklarovat řádková pole, nastavte nejprve vlastnost **AutoGenerateRows** na **hodnotu false**. Dále přidejte otevírací ** &lt;&gt; ** a uzavírací značky Polí mezi otevírací a uzavírací značky ovládacího prvku DetailsView. Nakonec uveďte řádková pole, která chcete zahrnout ** &lt;&gt; ** mezi otevírací a uzavírací značky Polí. Zadaná řádková pole jsou přidána do kolekce Pole v uvedeném pořadí. Fields **Fields** Kolekce umožňuje programově spravovat řádková pole v ovládacím prvku DetailsView.

> [!NOTE]
> Automaticky generovaná řádková pole nebudou přidána do kolekce Pole.

## <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek DetailsView může být vázán na ovládací prvek zdroje dat, například **SqlDataSource** nebo AccessDataSource, nebo na jakýkoli zdroj dat, který implementuje rozhraní System.Collections.IEnumerable, například System.Data.DataView, System.Collections.ArrayList a System.Collections.Hashtable.

Pomocí jedné z následujících metod svázat Ovládací prvek DetailsView na příslušný typ zdroje dat:

- Chcete-li vytvořit vazbu na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku DetailsView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek DetailsView se automaticky váže na zadaný ovládací prvek zdroje dat. Toto je upřednostňovaná metoda pro vazbu na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní **System.Collections.IEnumerable,** programově nastavte vlastnost DataSource ovládacího prvku DetailsView na zdroj dat a pak zavolejte metodu DataBind.

## <a name="security"></a>Zabezpečení

Tento ovládací prvek lze použít k zobrazení vstupu uživatele, který může obsahovat škodlivý klientský skript. Před zobrazením v aplikaci zkontrolujte všechny informace odeslané z klienta pro spustitelný skript, příkazy SQL nebo jiný kód. ASP.NET poskytuje funkci ověření vstupního požadavku pro blokování skriptu a HTML v uživatelském vstupu.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek DetailsView poskytuje integrované funkce, které umožňují uživateli aktualizovat, odstranit, vložit a stránkovat prostřednictvím položek v ovládacím prvku. Když detailsview ovládací prvek je vázán na ovládací prvek zdroje dat, ovládací prvek DetailsView můžete využít možnosti ovládacího prvku zdroje dat a poskytují automatické aktualizace, odstranění, vkládání a stránkování funkce.

Ovládací prvek DetailsView může poskytnout podporu pro operace aktualizace, odstranění, vložení a stránkování s jinými typy zdrojů dat; je však nutné zadat implementaci pro tyto operace v příslušné obslužné rutině události.

Ovládací prvek DetailsView může automaticky přidat řádkové pole **CommandField** s tlačítkem Upravit, Odstranit nebo Nový nastavením vlastností AutoGenerateEditButton, AutoGenerateDeleteButton nebo AutoGenerateInsertButton na **hodnotu true**. Na rozdíl od tlačítka Odstranit (které okamžitě odstraní vybraný záznam), po klepnutí na tlačítko Upravit nebo Nový přejde ovládací prvek DetailsView do režimu úprav nebo vložení. V režimu úprav je tlačítko Upravit nahrazeno tlačítkem Aktualizovat a Storno. Vstupní ovládací prvky, které jsou vhodné pro datový typ pole (například TextBox nebo Ovládací prvek CheckBox), jsou zobrazeny s hodnotou pole, kterou může uživatel upravit. Kliknutím na tlačítko Aktualizovat aktualizujete záznam ve zdroji dat a klepnutím na tlačítko Storno se všechny změny přerušíte. Podobně v režimu vložení je tlačítko Nový nahrazeno tlačítkem Vložit a Storno a uživateli se zobrazí prázdné vstupní ovládací prvky pro zadání hodnot nového záznamu.

Ovládací prvek DetailsView poskytuje funkci stránkování, která umožňuje uživateli přejít na jiné záznamy ve zdroji dat. Pokud je tato možnost povolena, ovládací prvky navigace na stránce se zobrazí v řádku operátoru. Chcete-li povolit stránkování, nastavte vlastnost AllowPaging na **hodnotu true**. Řádek operátoru lze přizpůsobit pomocí vlastností PagerStyle a PagerSettings.

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Vzhled ovládacího prvku DetailsView můžete přizpůsobit nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Stylu** | **Popis** |
| --- | --- |
| Alternatingrowstyle | Nastavení stylu pro řádky střídavých dat v ovládacím prvku DetailsView. Pokud je tato vlastnost nastavena, řádky dat se zobrazí střídavě mezi rowstyle nastavení a **alternatingRowStyle** nastavení. |
| CommandRowStyle | Nastavení stylu pro řádek obsahující vestavěná příkazová tlačítka v ovládacím prvku DetailsView. |
| Editrowstyle | Nastavení stylu pro řádky dat, když je ovládací prvek DetailsView v režimu úprav. |
| Emptydatarowstyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku DetailsView, pokud zdroj dat neobsahuje žádné záznamy. |
| Footerstyle | Nastavení stylu pro řádek zápatí ovládacího prvku DetailsView. |
| Headerstyle | Nastavení stylu pro řádek záhlaví ovládacího prvku DetailsView. |
| Insertrowstyle | Nastavení stylu pro řádky dat, když je ovládací prvek DetailsView v režimu vložení. |
| Pagerstyle | Nastavení stylu pro řádek operátoru ovládacího prvku DetailsView. |
| Rowstyle | Nastavení stylu pro řádky dat v ovládacím prvku DetailsView. Když **alternatingRowStyle** vlastnost je také nastavena, řádky dat jsou zobrazeny střídavě mezi **RowStyle** nastavení a **AlternatingRowStyle** nastavení. |
| Styl záhlaví pole | Nastavení stylu pro sloupec záhlaví ovládacího prvku DetailsView. |

## <a name="events"></a>Události

Ovládací prvek DetailsView poskytuje několik událostí, které můžete programovat proti. To umožňuje spustit vlastní rutiny vždy, když dojde k události. V následující tabulce jsou uvedeny události podporované ovládacím prvkem DetailsView. Ovládací prvek DetailsView také dědí tyto události ze svých základních tříd: DataBinding, DataBound, Disposed, Init, Load, PreRender a Render.

| **Událost** | **Popis** |
| --- | --- |
| Itemcommand | Vyvolá se při klepnutí na tlačítko v ovládacím prvku DetailsView. |
| Itemcreated | Vyvolá se po vytvoření všech objektů DetailsViewRow v ovládacím prvku DetailsView. Tato událost se často používá k úpravě hodnot záznamu před jeho zobrazením. |
| Itemdeleted | Vyvolá se při klepnutí na tlačítko Odstranit, ale po ovládacím prvku DetailsView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| Itemdeleting | Vyvolá se při klepnutí na tlačítko Odstranit, ale před ovládacím prvkem DetailsView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| Iteminserted | Vyvolá se při klepnutí na tlačítko Vložit, ale poté, co ovládací prvek DetailsView vloží záznam. Tato událost se často používá ke kontrole výsledků operace vložení. |
| Iteminserting | Vyvolá se při klepnutí na tlačítko Vložit, ale před položkou DetailView vloží záznam. Tato událost se často používá ke zrušení operace vložení. |
| Itemupdated | Vyvolá se při klepnutí na tlačítko Aktualizovat, ale po podrobnostiZobrazit ovládací prvek aktualizuje řádek. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| Itemupdating | Vyvolá se při klepnutí na tlačítko Aktualizovat, ale před ovládacím prvkem DetailsView aktualizuje záznam. Tato událost se často používá ke zrušení operace aktualizace. |
| Modechanged | Vyvolá se po změně režimů ovládacího prvku DetailsView (režim úpravy, vložení nebo jen pro čtení). Tato událost se často používá k provedení úlohy při detailsview ovládací prvek změní režimy. |
| Modechanging | Vyvolá se před změnou režimu ovládacího prvku DetailsView (režim úpravy, vložení nebo jen pro čtení). Tato událost se často používá ke zrušení změny režimu. |
| Pageindexchanged | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale po ovládacím prvku DetailsView zpracovává operaci stránkování. Tato událost se běžně používá, když potřebujete provést úkol poté, co uživatel přejde na jiný záznam v ovládacím prvku. |
| Změna indexu stránky | Vyvolá se při klepnutí na jedno z tlačítek operátoru, ale před ovládacím prvkem DetailsView zpracovává operaci stránkování. Tato událost se často používá ke zrušení operace stránkování. |

## <a name="the-menu-control"></a>Ovládací prvek Nabídky

Ovládací prvek Menu v ASP.NET 2.0 je navržen tak, aby byl plně vybavený navigační systém. Může být snadno vázán na hierarchické zdroje dat, jako je například SiteMapDataSource.

A Menu controls structure can be defined declarativně nebo dynamicky a se skládá z jednoho kořenového uzlu a libovolný počet poduzlů. Následující kód deklarativně definuje nabídku pro ovládací prvek Menu.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

Ve výše uvedeném příkladu je uzel Home.aspx kořenovým uzlem. Všechny ostatní uzly jsou vnořeny do kořenového uzlu na různých úrovních.

Existují dva typy nabídek, které ovládací prvek Nabídky lze vykreslit; statické nabídky a dynamické nabídky. Statické nabídky se skládají z položek nabídky, které jsou vždy viditelné. Dynamické nabídky se skládají z položek nabídky, které jsou viditelné pouze v případě, že na ně uživatel najedete myší. Zákazníci mohou často zaměnit statické nabídky s nabídkami definovanými deklarativně a dynamické nabídky s nabídkami, které jsou databound za běhu. Ve skutečnosti dynamické a statické nabídky nesouvisí s metodou plnění. Termíny *statické* a *dynamické* odkazují pouze na to, zda je nabídka staticky zobrazena ve výchozím nastavení nebo je zobrazena pouze v případě, že uživatel provede nějakou akci.

Vlastnost **StaticDisplayLevels** se používá ke konfiguraci, kolik úrovní nabídky jsou statické a proto se ve výchozím nastavení zobrazí. Ve výše uvedeném příkladu by nastavení vlastnosti **StaticDisplayLevels** na hodnotu 2 způsobilo, že nabídka bude staticky zobrazovat uzel Domů, uzel Hudba a uzel Filmy. Všechny ostatní uzly by se dynamicky zobrazí, když uživatel najede nad nadřazený uzel.

Vlastnost **MaximumDynamicDisplayLevels** konfiguruje maximální počet dynamických úrovní, které je nabídka schopna zobrazit. Všechny dynamické nabídky na vyšší úrovni, než je hodnota určená vlastností **MaximumDynamicDisplayLevels,** jsou zahozeny.

> [!NOTE]
> Je téměř jisté, že může dojít k situacím, kdy nabídky nezobrazí vykreslovat z důvodu MaximumDynamicDisplayLevels vlastnost. V těchto případech se ujistěte, že vlastnost je nastavena dostatečně, aby bylo možné zobrazit nabídky zákazníků.

## <a name="data-binding-the-menu-control"></a>Datová vazba ovládacího prvku nabídky

Ovládací prvek Nabídka může být vázán na libovolný hierarchický zdroj dat, například Například SiteMapDataSource nebo XMLDataSource. SiteMapDataSource je nejčastěji používaná metoda pro datovou vazbu na ovládací prvek Menu, protože se živí souborem Web.sitemap a jeho schéma poskytuje známé rozhraní API ovládacímu prvku Menu. Níže uvedený výpis ukazuje jednoduchý soubor Web.sitemap.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Všimněte si, že existuje pouze jeden kořenový prvek siteMapNode, v tomto případě Home element. Pro každý siteMapNode lze nakonfigurovat několik atributů. Nejčastěji používané atributy jsou:

- **adresa URL** Určuje adresu URL, která se má zobrazit, když uživatel klepne na položku nabídky. Pokud tento atribut není k dispozici, uzel bude jednoduše účtovat zpět po kliknutí.
- **název** Určuje text, který se zobrazí v položce nabídky.
- **popis** Používá se jako dokumentace pro uzel. Zobrazí se také jako tip nástroje, když je myš najetá nad uzla.
- **soubor siteMapFile** Umožňuje vnořené mapy webu. Tento atribut musí ukazovat na dobře vytvořený soubor ASP.NET sitemap.
- **role** Umožňuje, aby vzhled uzlu bylo řízeno ASP.NET oříznutízabezpečení.

Všimněte si, že zatímco tyto atributy jsou všechny volitelné, chování nabídky nemusí být co se očekává, pokud nejsou zadány. Pokud je například zadán atribut *url,* ale atribut *popisu* nikoli, uzel nebude viditelný a nebude existovat žádný způsob, jak přejít na zadanou adresu URL.

## <a name="controlling-a-menus-operation"></a>Ovládání operace nabídky

Existuje několik vlastností, které ovlivňují činnost ovládacího prvku ASP.NET Menu; **Vlastnost Orientace,** **vlastnost DisappearAfter,** vlastnost **StaticItemFormatString** a vlastnost **StaticPopoutImageUrl** jsou jen některé z nich.

- **Orientace** může být nastavena na *vodorovnou* nebo *svislou* a určuje, zda jsou statické položky nabídky rozloženy vodorovně v řadě nebo svisle a skládané na sebe. Tato vlastnost nemá vliv na dynamické nabídky.
- Vlastnost **DisappearAfter** konfiguruje, jak dlouho by měla být dynamická nabídka viditelná i po přesunutí myši. Hodnota je zadána v milisekundách a výchozí hodnota 500. Nastavení této vlastnosti na hodnotu -1 způsobí, že nabídka nikdy automaticky nezmizí. V takovém případě nabídka zmizí pouze tehdy, když uživatel klepne mimo nabídku.
- Vlastnost **StaticItemFormatString** usnadňuje udržování konzistentního verbiage v systému nabídek. Při zadávání této *{0}* vlastnosti, by měly být zadány na místo popisu, který se zobrazí ve zdroji dat. Například chcete-li mít položku nabídky z cvičení 1 říci Navštivte naše produkty {0} page, atd., byste zadat Navštivte naši stránku pro StaticItemFormatString. Za běhu ASP.NET nahradí jakýkoli {0} výskyt správným popisem položky nabídky.
- Vlastnost **StaticPopoutImageUrl** určuje bitovou kopii, která se používá k označení, že konkrétní uzel nabídky má podřízené uzly, ke kterým lze získat přístup najetím na něj. Dynamické nabídky budou nadále používat výchozí obrázek.

## <a name="templated-menu-controls"></a>Ovládací prvky nabídky s šablonami

Ovládací prvek Nabídka je ovládací prvek šablony a umožňuje dvě různé ItemTemplates; StaticItemTemplate a DynamicItemTemplate. Pomocí těchto šablon můžete do nabídek snadno přidat serverové ovládací prvky nebo uživatelské ovládací prvky.

Pokud chcete upravit šablony ve Visual Studiu .NET, klikněte v nabídce na tlačítko Inteligentní značka a zvolte Upravit šablony. Potom můžete zvolit mezi úpravou StaticItemTemplate nebo DynamicItemTemplate.

Všechny ovládací prvky přidané do staticitemtemplate se zobrazí ve statické nabídce při načtení stránky. Všechny ovládací prvky přidané do šablony DynamicItemTemplate se zobrazí ve všech rozbalovacích nabídkách.

## <a name="menu-events"></a>Události nabídky

Ovládací prvek Nabídky má dvě události, které jsou jedinečné; událost **MenuItemClicked** a **MenuItemDatabound.**

Událost MenuItemClicked je vyvolána po klepnutí na položku nabídky. Událost MenuItemDatabound je vyvolána, když je položka nabídky vázána na data. **MenuEventArgs,** který je předán obslužné rutině události poskytuje přístup k položce nabídky prostřednictvím Item vlastnost.

## <a name="controlling-a-menus-appearance"></a>Ovládání vzhledu nabídek

Vzhled ovládacího prvku nabídky můžete také ovlivnit pomocí jednoho nebo více z mnoha stylů dostupných pro formátování nabídek. Mezi ně patří **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**a **DynamicHoverStyle**. Tyto vlastnosti jsou konfigurovány pomocí standardního řetězce stylu HTML. Například následující bude mít vliv na styl pro dynamické nabídky.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Pokud používáte některý ze stylů Hover, budete &lt;muset&gt; přidat prvek head na stránku s prvkem *runat* nastaveným na *server*.

Ovládací prvky nabídky také podporují použití motivů ASP.NET 2.0.

## <a name="the-treeview-control"></a>Ovládací prvek TreeView

Ovládací prvek TreeView zobrazuje data ve stromové struktuře. Stejně jako u ovládacího prvku Menu mohou být snadno vázána data vázána na libovolný hierarchický zdroj dat, jako je například SiteMapDataSource.

První otázka, kterou zákazníci pravděpodobně položí na ovládací prvek TreeView v ASP.NET 2.0, je, zda souvisí s ovládacím prvkem TreeView IE WebControl, který byl k dispozici pro ASP.NET 1.x. Není. Ovládací prvek ASP.NET 2.0 TreeView byl napsán od základu a nabízí významné zlepšení oproti IE TreeView WebControl, který byl dříve k dispozici.

Nebudu zacházet do podrobností o tom, jak svázat TreeView ovládací prvek na mapě webu, jak se provádí přesně stejným způsobem jako ovládací prvek Menu. TreeView ovládací prvek má některé odlišné rozdíly ve způsobu, jakým funguje.

Ve výchozím nastavení treeview ovládací prvek se zobrazí plně rozbalen. Chcete-li změnit úroveň rozšíření při počátečním zatížení, upravte vlastnost **ExpandDepth** ovládacího prvku. To je zvláště důležité v případech, kdy TreeView je databound na rozbalení konkrétní uzly.

## <a name="databinding-the-treeview-control"></a>Datová vazba ovládacího prvku TreeView

Na rozdíl od ovládacího prvku Menu TreeView půjčuje dobře pro zpracování velkého množství dat. Proto kromě datové vazby na SiteMapDataSource nebo XMLDataSource, TreeView je často data vázána na DataSet nebo jiné relační data. V případech, kdy TreeView ovládací prvek je vázán na velké množství dat, je nejlepší vázat pouze na data, která je skutečně viditelné v ovládacím prvku. Potom můžete vytvořit vazbu dat na další data jako TreeView uzly jsou rozbaleny.

V těchto případech **PopulateOnDemand** vlastnost TreeView by měla být nastavena na *hodnotu true*. Potom budete muset poskytnout implementaci pro **TreeNodePopulate** metoda.

## <a name="data-binding-without-postback"></a>Datová vazba bez zpětného příspěvku

Všimněte si, že když poprvé rozbalíte uzel v předchozím příkladu, stránka se odešle zpět a aktualizuje. To není problém v tomto příkladu, ale můžete si představit, že může být v produkčním prostředí s velkým množstvím dat. Lepší scénář by byl ten, ve kterém TreeView by stále dynamicky naplnit své uzly, ale bez post zpět na server.

Nastavením **PopulateNodesFromClient** a **PopulateOnDemand** vlastnosti true, ovládací prvek ASP.NET TreeView dynamicky naplní uzly bez post zpět. Při rozbalení nadřazeného uzlu je z klienta proveden požadavek XMLHttp a je aktivována událost OnTreeNodePopulate. Server odpoví datovým ostrovem XML, který se pak používá k vytvoření datové vazby podřízených uzlů.

ASP.NET dynamicky vytvoří klientský kód, který implementuje tuto funkci. &lt;Značky&gt; skriptů, které obsahují skript, jsou generovány odkazem na soubor AXD. Například níže uvedený výpis zobrazuje odkazy skriptů pro kód skriptu, který generuje požadavek XMLHttp.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Pokud prohledáte výše uvedený soubor AXD v prohlížeči a otevřete jej, zobrazí se kód, který implementuje požadavek XMLHttp. Tato metoda zabraňuje zákazníkům v úpravě souboru skriptu.

## <a name="controlling-the-operation-of-the-treeview-control"></a>Řízení provozu ovládacího prvku TreeView

TreeView ovládací prvek má několik vlastností, které ovlivňují provoz ovládacího prvku. Nejviditelnější vlastnosti jsou **ShowCheckBoxes**, **ShowExpandCollapse**a **ShowLines**.

Vlastnost **ShowCheckBoxes** ovlivňuje, zda uzly při vykreslení zobrazí zaškrtávací políčko. Platné hodnoty pro tuto vlastnost jsou **None**, **Root**, **Parent**, **Leaf**a **All**. Tyto vliv TreeView ovládacíprvek takto:

| **Hodnota vlastnosti** | **Účinek** |
| --- | --- |
| Žádná | Zaškrtávací políčka se nezobrazují na žádném uzlu. Toto je výchozí nastavení. |
| Kořenová složka | Zaškrtávací políčko se zobrazí pouze v kořenovém uzlu. |
| Nadřazený | Zaškrtávací políčko se zobrazí pouze na uzlech, které mají podřízené uzly. Tyto podřízené uzly mohou být nadřazené uzly nebo listové uzly. |
| List | Zaškrtávací políčko se zobrazí pouze na uzlech, které nemají žádné podřízené uzly. |
| Všechny | Zaškrtávací políčko se zobrazí na všech uzlech. |

Při použití zaškrtávacích políček **CheckedNodes** vlastnost vrátí kolekci TreeView uzly, které jsou kontrolovány na postback.

Vlastnost **ShowExpandCollapse** řídí vzhled rozbaleného/sbalitého obrazu vedle kořenových a nadřazených uzlů. Pokud je tato vlastnost nastavena na **hodnotu false**, uzly TreeView jsou vykresleny jako hypertextové odkazy a jsou rozbaleny/sbaleny kliknutím na odkaz.

Vlastnost **ShowLines** určuje, zda jsou zobrazeny čáry spojující nadřazené uzly s podřízenými uzly. Pokud **false** (výchozí), jsou zobrazeny žádné řádky. Pokud **true**, TreeView ovládací prvek bude používat řádky obrazy ve složce určené **Vlastnost LineImagesFolder.**

Chcete-li přizpůsobit vzhled řádků TreeView, sada Visual Studio .NET 2005 obsahuje nástroj návrháře čar. K tomuto nástroji se dostanete pomocí tlačítka Inteligentní značka v ovládacím prvku TreeView, jak je uvedeno níže.

![](data-bound-controls/_static/image1.jpg)

**Obrázek 1**

Když vyberete možnost **Přizpůsobit obrazce řádků,** spustí se nástroj Návrhář linek, který vám umožní konfigurovat vzhled řádků TreeView.

## <a name="treeview-events"></a>Události TreeView

Ovládací prvek TreeView má následující jedinečné události:

- SelectedNodeChanged Vyvolá se, když je uzel vybrán na základě vlastnosti **SelectAction.**
- TreeNodeCheckChanged Nastane při změně stavu uzly.
- TreeNodeExpanded dojde při rozbalení uzlu na základě **SelectAction** vlastnost.
- TreeNodeCollapsed dojde při sbalení uzlu.
- TreeNodeDataBound Vyvolá, když je uzel vázán na data.
- TreeNodePopulate Nastane, když je naplněn uzel.

**Vlastnost SelectAction** umožňuje nakonfigurovat, která událost je aktivována, když je vybrán uzel. Vlastnost SelectAction poskytuje následující akce:

- TreeNodeSelectAction.Expand zvyšuje TreeNodeExpanded, když je vybrán uzel.
- TreeNodeSelectAction.None vyvolá žádnou událost, když je uzel vybrán.
- TreeNodeSelectAction.Select Vyvolá událost SelectedNodeChanged, když je uzel vybrán.
- TreeNodeSelectAction.SelectExpand vyvolá událost SelectedNodeChanged i událost TreeNodeExpanded, když je uzel vybrán.

## <a name="controlling-appearance-with-styles"></a>Ovládání vzhledu pomocí stylů

TreeView ovládací prvek poskytuje mnoho vlastností pro řízení vzhledu ovládacího prvku se styly. K dispozici jsou následující vlastnosti.

| **Název vlastnosti** | **Ovládací prvky** |
| --- | --- |
| HoverNodeStyle | Řídí styl uzlů, když je nad nimi najetá myš. |
| Styl listového uzlu | Řídí styl listových uzlů. |
| Nodestyle | Řídí styl pro všechny uzly. Konkrétní styly uzlů (například LeafNodeStyle) tento styl přepsat. |
| ParentNodeStyle | Řídí styl pro všechny nadřazené uzly. |
| Rootnodestyle | Řídí styl kořenového uzlu. |
| Styl SelectedNode | Řídí styl vybraného uzlu. |

Každá z těchto vlastností je jen pro čtení. Každý však vrátí **treenodestyle** objekt a vlastnosti tohoto objektu lze upravit pomocí formátu *vlastnosti podvlastnost.* Chcete-li například nastavit vlastnost **ForeColor** v stylu **SelectedNodeStyle**, použijte následující syntaxi:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Všimněte si, že výše uvedená značka není uzavřena. Je to proto, že při použití zde uvedené deklarativní syntaxe byste zahrnuli také uzly TreeViews do kódu HTML.

Vlastnosti stylu lze také zadat v kódu pomocí formátu *property.subproperty.* Chcete-li například nastavit vlastnost **ForeColor** v kódu **RootNodeStyle,** použijte následující syntaxi:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Úplný seznam různých vlastností stylu naleznete v dokumentaci msdn na TreeNodeStyle objektu.

## <a name="the-sitemappath-control"></a>Ovládací prvek Mapa stránek

Ovládací prvek SiteMapPath poskytuje ovládací prvek navigace strouhanky pro vývojáře ASP.NET. Stejně jako ostatní navigační ovládací prvky mohou být snadno vázána na hierarchické zdroje dat, jako je Například SiteMapDataSource nebo XmlDataSource.

Ovládací prvek SiteMapPath se skládá z objektů SiteMapNodeItem. Existují tři typy uzlů; Kořenový uzel, nadřazené uzly a aktuální uzel. Kořenový uzel je uzel v horní části hierarchické struktury. Aktuální uzel představuje aktuální stránku. Všechny ostatní uzly jsou nadřazené uzly.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>Řízení provozu ovládacího prvku SiteMapPath

Vlastnosti, které řídí provoz ovládacího prvku SiteMapPath, jsou následující:

| **Vlastnost** | **Popis nemovitosti** |
| --- | --- |
| Zobrazené nadřazené úrovně | Určuje, kolik nadřazených uzlů se zobrazí. Výchozí hodnota je -1, která neukládá žádné omezení počtu zobrazených nadřazených uzlů. |
| Směr cesty | Určuje směr cesty SiteMapPath. Platné hodnoty jsou RootToCurrent (výchozí) a CurrentToRoot. |
| Pathseparator | Řetězec, který řídí znak, který odděluje uzly v ovládacím prvku SiteMapPath. Výchozí hodnota je :. |
| RenderCurrentNodeAsLink | Logická hodnota, která určuje, zda je aktuální uzel vykreslen jako odkaz. Výchozí hodnota je False. |
| Skiplinktext | Pomáhá s usnadněním přístupu při prohlížení stránky programy pro čtení z obrazovky. Tato vlastnost umožňuje programy pro čtení z obrazovky přeskočit ovládací prvek SiteMapPath. Chcete-li tuto funkci zakázat, nastavte vlastnost string.Empty. |

## <a name="templated-sitemappath-controls"></a>Předkládaná ovládací prvky Cesty

SiteMapControl je ovládací prvek šablony a jako takový můžete definovat různé šablony pro použití při zobrazení ovládacího prvku. Chcete-li upravit šablony v ovládacím prvku SiteMapPath, klepněte na tlačítko Inteligentní značka v ovládacím prvku a z nabídky zvolte Upravit šablony. Zobrazí se nabídka SiteMapTasks, jak je znázorněno níže, kde si můžete vybrat mezi různými dostupnými šablonami.

![](data-bound-controls/_static/image2.jpg)

**Obrázek 2**

Šablona **NodeTemplate** odkazuje na libovolný uzel v sitemappathu. Pokud je uzel kořenový uzel nebo aktuální uzel a je nakonfigurován **rootNodeTemplate** nebo **CurrentNodeTemplate,** je přepsána nodetemplate.

## <a name="sitemappath-events"></a>Události aplikace SiteMapPath

Ovládací prvek SiteMapPath má dvě události, které nejsou odvozeny z Control třídy; událost **ItemCreated** a **ItemDataBound.** Událost ItemCreated je vyvolána při vytvoření položky SiteMapPath. ItemDataBound je aktivována, když je metoda DataBind volána během datové vazby uzlu SiteMapPath. Objekt **SiteMapNodeItemEventArgs** poskytuje přístup ke konkrétní sitemapnodeitem prostřednictvím vlastnosti Item.

## <a name="controlling-appearance-with-styles"></a>Ovládání vzhledu pomocí stylů

Pro formátování ovládacího prvku SiteMapPath jsou k dispozici následující styly.

| **Název vlastnosti** | **Ovládací prvky** |
| --- | --- |
| Currentnodestyle | Řídí styl textu pro aktuální uzel. |
| Rootnodestyle | Řídí styl textu kořenového uzlu. |
| Nodestyle | Řídí styl textu pro všechny uzly za předpokladu, že neplatí CurrentNodeStyle nebo RootNodeStyle. |

Vlastnost NodeStyle je přepsána buď CurrentNodeStyle nebo RootNodeStyle. Každá z těchto vlastností je jen pro čtení a vrátí **Objekt Style.** Chcete-li ovlivnit vzhled uzlu pomocí jedné z těchto vlastností, budete muset nastavit vlastnosti Objektstyle, který je vrácen. Například níže uvedený kód změní vlastnost forecolor aktuálního uzlu.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

Vlastnost lze také programově použít takto:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Pokud je použita šablona, styl nebude použit.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Lab 1: Konfigurace ovládacího prvku nabídky ASP.NET

1. Vytvořte nový web.
2. Přidejte soubor mapy webu tak, že vyberete Soubor, Nový, Soubor a vyberete Mapu webu ze seznamu šablon souborů.
3. Otevřete mapu webu (web.sitemap ve výchozím nastavení) a upravte ji tak, aby vypadala jako níže uvedený výpis. Stránky, na které odkazujete v souboru mapy webu, ve skutečnosti neexistují, ale to nebude problém pro toto cvičení.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Otevřete výchozí webový formulář v návrhovém zobrazení.
5. V části Navigace v panelu nástrojů přidejte na stránku nový ovládací prvek Nabídka.
6. V části Data v panelu nástrojů přidejte nový SiteMapDataSource. SiteMapDataSource bude automaticky používat soubor Web.sitemap na vašem webu. (Soubor Web.sitemap *musí* být v kořenové složce webu.)
7. Klepněte na ovládací prvek Nabídka a potom klepnutím na tlačítko Inteligentní značka zobrazte dialogové okno Úlohy nabídky.
8. V rozevíracím okně Zvolit zdroj dat vyberte SiteMapDataSource1.
9. Klepněte na odkaz Automatický formát a zvolte formát nabídky.
10. V podokně Vlastnosti nastavte vlastnost **StaticDisplayLevels** na 2. Ovládací prvek Nabídky by nyní měl zobrazit uzel Domů, Produkty a Služby v návrháři.
11. Projděte si stránku v prohlížeči a použijte nabídku. (Protože stránky, které jste přidali na mapu webu, ve skutečnosti neexistují, zobrazí se při pokusu o jejich procházení chyba.)

Experimentujte se změnou StaticDisplayLevels a MaximumDynamicDisplayLevels vlastnosti a uvidíte, jak ovlivňují způsob vykreslení nabídky.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Lab 2: Dynamicky vazby TreeView ovládacího prvku

Toto cvičení předpokládá, že máte SQL Server spuštěn místně a že databáze Northwind je k dispozici na instanci serveru SQL Server. Pokud tyto podmínky nejsou splněny, změňte připojovací řetězec v ukázce. Všimněte si, že může být také nutné zadat ověřování serveru SQL Server namísto důvěryhodného připojení.

1. Vytvořte nový web.
2. Přepněte do zobrazení kód pro Default.aspx a nahraďte veškerý kód kódem uvedeným níže. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Uložte stránku jako treeview.aspx.
4. Prohlédněte si stránku.
5. Při prvním zobrazení stránky zobrazte zdroj stránky v prohlížeči. Všimněte si, že klientovi byly odeslány pouze viditelné uzly.
6. Klikněte na znaménko plus vedle libovolného uzlu.
7. Znovu zobrazit zdroj na stránce. Všimněte si, že nově zobrazené uzly jsou nyní k dispozici.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Lab 3: Podrobnosti zobrazení a úpravy dat pomocí GridView a DetailsView

1. Vytvořte nový web.
2. Přidejte na web nový soubor web.config.
3. Přidejte připojovací řetězec do souboru web.config, jak je znázorněno níže: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > Možná budete muset změnit připojovací řetězec na základě vašeho prostředí.
4. Uložte a zavřete soubor web.config.
5. Otevřete soubor Default.aspx a přidejte nový ovládací prvek SqlDataSource.
6. Změňte ID ovládacího prvku SqlDataSource na **Produkty**.
7. V nabídce **Úlohy SqlDataSource** klepněte na **tlačítko Konfigurovat zdroj dat**.
8. V rozevíracím souboru připojení vyberte **Možnost Northwind** a klikněte na Další.
9. V rozevíracím seznamu **Název** vyberte **Produkty** a zaškrtněte **políčka ProductID**, **ProductName**, **UnitPrice**a **UnitsInStock,** jak je znázorněno níže. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. Klikněte na **Další**.
11. Klikněte na **Finish** (Dokončit).
12. Přepněte do zobrazení zdroje a zkontrolujte kód, který byl vygenerován. Všimněte si **příkazů SelectCommand**, **DeleteCommand**, **InsertCommand**a **UpdateCommand,** které byly přidány do ovládacího prvku SqlDataSource. Všimněte si také parametry, které byly přidány.
13. Přepněte do návrhového zobrazení a přidejte na stránku nový ovládací prvek GridView.
14. V rozevíracím souboru **Zvolit zdroj dat** vyberte **Produkty.**
15. Zaškrtněte **políčko Povolit stránkování** a **Povolit výběr,** jak je znázorněno níže. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. Klikněte na odkaz **Upravit sloupce** a zkontrolujte, zda jsou zaškrtnuta **políčka Automatické generování.**
17. Klikněte na tlačítko **OK**.
18. Když je vybraný ovládací prvek GridView, klepněte na tlačítko vedle vlastnosti **DataKeyNames** v podokně Vlastnosti.
19. V seznamu **Dostupná datová pole** vyberte **&gt;** **ProductID** a kliknutím na tlačítko ho přidejte.
20. Klikněte na tlačítko OK.
21. Přidejte na stránku nový ovládací prvek SqlDataSource.
22. Změňte ID ovládacího prvku SqlDataSource na **Podrobnosti**.
23. Z nabídky Úlohy SqlDataSource zvolte **Konfigurovat zdroj dat**.
24. Z rozevíracího souboru zvolte **Northwind** a klepněte na **tlačítko Další**.
25. V rozevíracím seznamu <strong>Název</strong> <strong> \<vyberte <strong>Produkty</strong> a zaškrtněte políčko /strong>* v seznamu <strong>Sloupce.</strong>
26. Klepněte na tlačítko **KDE.**
27. V rozevíracím souboru **Sloupec** vyberte **ProductID.**
28. V **=** yberte v rozevíracím souboru Operátor.
29. V rozevíracím souboru **Zdroj** vyberte **Ovládacíprvek.**
30. V rozevíracím souboru **ID ovládacího prvku** vyberte **GridView1.**
31. Kliknutím na tlačítko **Přidat** přidejte klauzuli WHERE.
32. Klikněte na tlačítko **OK**.
33. Klepněte na tlačítko **Upřesnit** a zaškrtněte políčko **Generovat příkazy INSERT, UPDATE a DELETE.**
34. Klikněte na tlačítko **OK**.
35. Klepněte na tlačítko **Další** a klepněte na **tlačítko Dokončit**.
36. Přidejte ovládací prvek DetailsView na stránku.
37. V rozevíracím souboru **Zvolit zdroj dat** zvolte **Podrobnosti**.
38. Zaškrtněte políčko **Povolit úpravy,** jak je znázorněno níže. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Uložte stránku a procházejte soubor Default.aspx.
40. Kliknutím na odkaz **Vybrat** vedle různých záznamů automaticky zobrazíte aktualizaci Zobrazení podrobností.
41. Klikněte na odkaz **Upravit** v ovládacím prvku DetailsView.
42. Proveďte změnu záznamu a klepněte na tlačítko **Aktualizovat**.
