---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: Zobrazení dat v grafu s ASP.NET webových stránek (břitva) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tato kapitola vysvětluje, jak zobrazit data v grafu. V předchozích kapitolách jste se naučili zobrazovat data ručně a v mřížce. Tato kapitola vysvětluje...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542882"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>Zobrazení dat v grafu s ASP.NET webových stránek (Břitva)

podle [společnosti Microsoft](https://github.com/microsoft)

> Tento článek vysvětluje, jak pomocí grafu zobrazit data na webu ASP.NET webových stránek (Razor) pomocí pomocníka. `Chart`
> 
> **Co se naučíte:**
> 
> - Jak zobrazit data v grafu.
> - Jak styl grafy pomocí vestavěných motivů.
> - Jak uložit grafy a jak je uložit do mezipaměti pro lepší výkon.
> 
> Jedná se o ASP.NET programovací funkce zavedené v článku:
> 
> - Pomocník. `Chart`
> 
> > [!NOTE]
> > Informace v tomto článku platí pro ASP.NET webových stránek 1.0 a webových stránek 2.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Pomocník grafu

Chcete-li zobrazit data v grafické podobě, `Chart` můžete použít pomocnou pomoc. Pomocník `Chart` může vykreslit obrázek, který zobrazuje data v různých typech grafů. Podporuje mnoho možností formátování a popisování. Pomocník `Chart` může vykreslit více než 30 typů grafů, včetně všech typů grafů, které můžete znát z aplikace Microsoft Excel nebo jiných nástrojů &#8212; plošných grafů, pruhových grafů, sloupcových grafů, spojnicových grafů a výsečových grafů, spolu s více specializovanými grafy, jako jsou burzovní grafy.

| Popis **plošného grafu:** ![Obrázek typu plošného grafu](7-displaying-data-in-a-chart/_static/image1.jpg) | Popis **pruhového grafu:** ![Obrázek typu pruhového grafu](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| Popis **sloupcového grafu:** ![Obrázek typu sloupcového grafu](7-displaying-data-in-a-chart/_static/image3.jpg) | Popis **spojnicového grafu:** ![Obrázek typu spojnicového grafu](7-displaying-data-in-a-chart/_static/image4.jpg) |
| Popis **výsečového grafu:** ![Obrázek typu výsečového grafu](7-displaying-data-in-a-chart/_static/image5.jpg) | **Popis burzovního grafu:** ![Obrázek typu burzovního grafu](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Prvky grafu

Grafy zobrazují data a další prvky, jako jsou legendy, osy, řady a tak dále. Následující obrázek znázorňuje mnoho prvků grafu, které `Chart` lze přizpůsobit při použití pomocníka. Tento článek ukazuje, jak nastavit některé (ne všechny) z těchto prvků.

![Popis: Obrázek znázorňující prvky grafu](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Vytvoření grafu z dat

Data zobrazená v grafu mohou podoby z pole, z výsledků vrácených z databáze nebo z dat v souboru XML.

### <a name="using-an-array"></a>Použití pole

Jak je vysvětleno v [úvodu k programování webových stránek ASP.NET pomocí syntaxe holicího strojku](https://go.microsoft.com/fwlink/?LinkId=202890), pole umožňuje uložit kolekci podobných položek do jedné proměnné. Pole můžete použít k obsahovat data, která chcete zahrnout do grafu.

Tento postup ukazuje, jak můžete vytvořit graf z dat v polích pomocí výchozího typu grafu. Ukazuje také, jak zobrazit graf na stránce.

1. Vytvořte nový soubor s názvem *ChartArrayBasic.cshtml*.
2. Nahraďte existující obsah následujícím: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Kód nejprve vytvoří nový graf a nastaví jeho šířku a výšku. Název grafu zadáte pomocí `AddTitle` metody. Chcete-li přidat data, použijte metodu. `AddSeries` V tomto `name`příkladu použijete , `xValue`a `yValues` `AddSeries` parametry metody. Parametr `name` se zobrazí v legendě grafu. Parametr `xValue` obsahuje pole dat, která jsou zobrazena podél vodorovné osy grafu. Parametr `yValues` obsahuje pole dat, které se používá k vykreslení svislých bodů grafu.

    Metoda `Write` ve skutečnosti vykreslí graf. V tomto případě, protože jste nezadali `Chart` typ grafu, pomocník vykreslí svůj výchozí graf, což je sloupcový graf.
3. Spusťte stránku v prohlížeči. Prohlížeč zobrazí graf. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Použití databázového dotazu pro data grafu

Pokud jsou informace, které chcete vytvořit, v databázi, můžete spustit databázový dotaz a potom k vytvoření grafu použít data z výsledků. Tento postup ukazuje, jak číst a zobrazovat data z databáze vytvořené v článku [Úvod do práce s databází v ASP.NET webech webových stránek](https://go.microsoft.com/fwlink/?LinkId=202893).

1. Pokud složka ještě neexistuje, přidejte do kořenového adresáře webu složku *\_Složky Složena Dat* aplikace.
2. Do složky *Data\_aplikace* přidejte databázový soubor s názvem *SmallBakery.sdf,* který je popsán v části Úvod do práce s databází v ASP.NET [webech webových stránek](https://go.microsoft.com/fwlink/?LinkId=202893).
3. Vytvořte nový soubor s názvem *ChartDataQuery.cshtml*.
4. Nahraďte existující obsah následujícím:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Kód nejprve otevře databázi SmallBakery a přiřadí ji proměnné s názvem `db`. Tato proměnná `Database` představuje objekt, který lze použít ke čtení z databáze a zápisu do databáze. Dále kód spustí dotaz SQL získat název a cenu každého produktu. Kód vytvoří nový graf a předá mu databázový dotaz `DataBindTable` voláním metody grafu. Tato metoda má dva `dataSource` parametry: parametr je pro data `xField` z dotazu a parametr umožňuje nastavit, který sloupec dat se používá pro osu x grafu.

    Jako alternativu k `DataBindTable` použití metody můžete `AddSeries` použít `Chart` metodu pomocníka. Metoda `AddSeries` umožňuje nastavit `xValue` parametry `yValues` a. Například místo použití `DataBindTable` metody, jako je tento:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Můžete použít `AddSeries` metodu, jako je tato:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Oba vykreslují stejné výsledky. Metoda `AddSeries` je flexibilnější, protože můžete zadat typ grafu `DataBindTable` a data explicitněji, ale metoda je jednodušší použít, pokud nepotřebujete další flexibilitu.
5. Spusťte stránku v prohlížeči. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>Použití dat XML

Třetí možností pro vytváření grafů je použití souboru XML jako dat pro graf. To vyžaduje, aby soubor XML měl také soubor schématu *(.xsd* file), který popisuje strukturu XML. Tento postup ukazuje, jak číst data ze souboru XML.

1. Ve složce *Data aplikace\_* vytvořte nový soubor XML s názvem *data.xml*.
2. Nahraďte existující xml následujícím, což jsou některá data XML o zaměstnancích fiktivní společnosti. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. Ve složce *Data aplikace\_* vytvořte nový soubor XML s názvem *data.xsd*. (Všimněte si, že prodloužení tentokrát je *.xsd*.)
4. Nahraďte existující xml následujícím: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartDataXML.cshtml*.
6. Nahraďte existující obsah následujícím: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Kód nejprve `DataSet` vytvoří objekt. Tento objekt slouží ke správě dat, která jsou čtena ze souboru XML, a k jejich uspořádání podle informací v souboru schématu. (Všimněte si, že horní `using SystemData`část kódu obsahuje příkaz . To je nutné, aby bylo možné `DataSet` pracovat s objektem. Další informace naleznete [ &quot;&quot; v tématu Using Statements and Fully Qualified Names](#SB_UsingStatements) dále v tomto článku.)

    Dále kód vytvoří `DataView` objekt založený na datové sadě. Zobrazení dat poskytuje objekt, který graf může vázat na &#8212;, který je čtení a vykreslení. Graf se váže k datům `AddSeries` pomocí metody, jak jste viděli dříve při mapování `xValue` `yValues` dat pole, s `DataView` tím rozdílem, že tentokrát a parametry jsou nastaveny na objekt.

    Tento příklad také ukazuje, jak zadat konkrétní typ grafu. Při přidání dat do `AddSeries` metody `chartType` je parametr také nastaven na zobrazení výsečového grafu.
7. Spusťte stránku v prohlížeči. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" prohlášení a plně kvalifikované názvy
> 
> Rozhraní .NET Framework, který ASP.NET webové stránky se syntaxí Razor, se skládá z mnoha tisíc komponent (tříd). Aby bylo možné pracovat se všemi těmito třídami, jsou uspořádány do *oborů názvů*, které jsou poněkud podobné knihovnám. Obor `System.Web` názvů například obsahuje třídy, které podporují `System.Xml` komunikaci mezi prohlížečem a serverem, obor `System.Data` názvů obsahuje třídy, které se používají k vytváření a čtení souborů XML, a obor názvů obsahuje třídy, které umožňují pracovat s daty.
> 
> Chcete-li získat přístup k dané třídě v rozhraní .NET Framework, kód potřebuje znát nejen název třídy, ale také obor názvů, ve kterém se třída nachází. Například pro `Chart` použití pomocníka, kód potřebuje najít `System.Web.Helpers.Chart` třídu, která kombinuje`System.Web.Helpers`obor názvů (`Chart`) s názvem třídy ( ). To se označuje jako *plně kvalifikovaný* název třídy &#8212; jeho úplné, jednoznačné umístění v rámci vastness rozhraní .NET Framework. V kódu by to vypadalo takto:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Je však těžkopádné (a náchylné k chybám) muset použít tyto dlouhé, plně kvalifikované názvy pokaždé, když chcete odkazovat na třídu nebo pomocníka. Proto, aby bylo snazší používat názvy tříd, můžete *importovat* obory názvů, které vás zajímají, což je obvykle jen hrstka z mnoha oborů názvů v rozhraní .NET Framework. Pokud jste importovali obor názvů, můžete místo plně`Chart`kvalifikovaného názvu ( (`System.Web.Helpers.Chart`použít pouze název třídy ( ). Když váš kód spustí a narazí na název třídy, může hledat pouze v oborech názvů, které jste importovali, a najít tuto třídu.
> 
> Při použití ASP.NET webových stránek s syntaxí Razor k vytvoření webových stránek, `WebPage` obvykle používáte stejnou sadu tříd pokaždé, včetně třídy, různých pomocníků a tak dále. Chcete-li ušetřit práci při importu příslušných oborů názvů při každém vytvoření webu, je ASP.NET nakonfigurovántak, aby automaticky importoval sadu základních oborů názvů pro každý web. To je důvod, proč jste se dosud nemuseli zabývat obory názvů nebo importem; všechny třídy, se kterými jste pracovali, jsou v oborech názvů, které jsou již importovány za vás.
> 
> Někdy však potřebujete pracovat s třídou, která není v oboru názvů, který je automaticky importován za vás. V takovém případě můžete buď použít plně kvalifikovaný název této třídy, nebo můžete ručně importovat obor názvů, který obsahuje třídu. Chcete-li importovat obor `using` názvů,`import` použijte příkaz (v jazyce Visual Basic), jak jste viděli v příkladu dříve v článku.
> 
> Například `DataSet` třída je v `System.Data` oboru názvů. Obor `System.Data` názvů není automaticky k dispozici pro ASP.NET stránek Razor. Proto pro práci `DataSet` s třídou pomocí plně kvalifikovaný název, můžete použít kód, jako je tento:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> Pokud máte použít `DataSet` třídu opakovaně, můžete importovat obor názvů, jako je tento, a pak použít pouze název třídy v kódu:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Můžete přidat `using` příkazy pro všechny ostatní obory názvů rozhraní .NET Framework, na které chcete odkazovat. Nicméně, jak již bylo uvedeno, nebudete muset dělat to často, protože většina tříd, které budete pracovat s jsou v oborech názvů, které jsou importovány automaticky ASP.NET pro použití v *.cshtml* a *.vbhtml* stránky.

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Zobrazení grafů uvnitř webové stránky

V příkladech, které jste dosud viděli, vytvoříte graf a pak se graf vykreslí přímo do prohlížeče jako grafiku. V mnoha případech však chcete zobrazit graf jako součást stránky, a to nejen sám v prohlížeči. K tomu vyžaduje dvoustupňový proces. Prvním krokem je vytvoření stránky, která generuje graf, jak jste již viděli.

Druhým krokem je zobrazení výsledného obrázku na jiné stránce. Chcete-li zobrazit obraz, `<img>` použijte element HTML stejným způsobem jako libovolný obrázek. Namísto odkazování na soubor *JPG* nebo *PNG* však `<img>` prvek odkazuje na soubor `Chart` *.cshtml,* který obsahuje pomocníka, který vytváří graf. Při spuštění stránky zobrazení `<img>` prvek získá výstup `Chart` pomocníka a vykreslí graf.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. Vytvořte soubor s názvem *ShowChart.cshtml*.
2. Nahraďte existující obsah následujícím: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Kód používá `<img>` prvek k zobrazení grafu, který jste vytvořili dříve v souboru *ChartArrayBasic.cshtml.*
3. Spusťte webovou stránku v prohlížeči. Soubor *ShowChart.cshtml* zobrazí obrázek grafu na základě kódu obsaženého v souboru *ChartArrayBasic.cshtml.*

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Stylování grafu

Pomocník `Chart` podporuje velký počet možností, které umožňují přizpůsobit vzhled grafu. Můžete nastavit barvy, písma, ohraničení a tak dále. Snadný způsob, jak přizpůsobit vzhled grafu, je použít *motiv*. Motivy jsou kolekce informací, které určují, jak vykreslit graf pomocí písem, barev, popisků, palet, ohraničení a efektů. (Všimněte si, že styl grafu neoznačuje typ grafu.)

V následující tabulce jsou uvedeny předdefinované motivy.

| Motiv | Popis |
| --- | --- |
| `Vanilla` | Zobrazí červené sloupce na bílém pozadí. |
| `Blue` | Zobrazí modré sloupce na modrém pozadí přechodu. |
| `Green` | Zobrazí modré sloupce na zeleném pozadí přechodu. |
| `Yellow` | Zobrazí oranžové sloupce na žlutém pozadí přechodu. |
| `Vanilla3D` | Zobrazí 3D červené sloupce na bílém pozadí. |

Můžete určit motiv, který se má použít při vytváření nového grafu.

1. Vytvořte nový soubor s názvem *ChartStyleGreen.cshtml*.
2. Nahraďte existující obsah na stránce následujícími:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Tento kód je stejný jako předchozí příklad, který používá `theme` databázi pro `Chart` data, ale přidá parametr při vytváření objektu. Následující ukazuje změněný kód:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Spusťte stránku v prohlížeči. Zobrazí se stejná data jako předtím, ale graf vypadá leštěněji: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Uložení grafu

Při použití `Chart` pomocníka, jak jste viděli zatím v tomto článku, pomocník znovu vytvoří graf od začátku pokaždé, když je vyvolána. V případě potřeby kód grafu také znovu napíše databázi nebo přečte soubor XML, aby získal data. V některých případech to může být složitá operace, například pokud je databáze, na kterou se dotazujete, velká nebo pokud soubor XML obsahuje velké množství dat. I v případě, že graf neobsahuje velké množství dat, proces dynamického vytváření obrázku zabírá prostředky serveru a pokud mnoho lidí požaduje stránku nebo stránky, které graf zobrazují, může to mít vliv na výkon vašeho webu.

Chcete-li snížit potenciální dopad vytvoření grafu na výkon, můžete vytvořit graf při prvním využití a poté jej uložit. Když je graf potřeba znovu, spíše než jeho regenerace, stačí načíst uloženou verzi a vykreslit ji.

Graf můžete uložit následujícími způsoby:

- Ukládat graf do mezipaměti v paměti počítače (na serveru).
- Uložte graf jako soubor obrázku.
- Uložte graf jako soubor XML. Tato možnost umožňuje upravit graf před uložením.

### <a name="caching-a-chart"></a>Ukládání grafu do mezipaměti

Po vytvoření grafu jej můžete uložit do mezipaměti. Ukládání grafu do mezipaměti znamená, že není nutné jej znovu vytvořit, pokud je třeba jej znovu zobrazit. Když uložíte graf do mezipaměti, dáte mu klíč, který musí být jedinečný pro tento graf.

Grafy uložené do mezipaměti mohou být odebrány, pokud má server nedostatek paměti. Kromě toho je mezipaměť vymazána, pokud se aplikace z nějakého důvodu restartuje. Standardní mač proto pracuje s grafem uloženým v mezipaměti, aby se vždy nejprve zkontrolovalo, zda je k dispozici v mezipaměti, a pokud ne, pak jej vytvořte nebo znovu vytvořte.

1. V kořenovém adresáři webu vytvořte soubor s názvem *ShowCachedChart.cshtml*.
2. Nahraďte existující obsah následujícím: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    Značka `<img>` obsahuje `src` atribut, který odkazuje na soubor *ChartSaveToCache.cshtml* a předá klíč stránce jako řetězec dotazu. Klíč obsahuje hodnotu &quot;myChartKey&quot;. Soubor *ChartSaveToCache.cshtml* obsahuje `Chart` pomocníka, který vytváří graf. Tuto stránku vytvoříte za chvíli.

    Na konci stránky je odkaz na stránku s názvem *ClearCache.cshtml*. To je stránka, kterou také brzy vytvoříte. Potřebujete *ClearCache.cshtml* pouze k testování ukládání do mezipaměti pro tento příklad - to není odkaz nebo stránky, které byste normálně zahrnout při práci s grafy v mezipaměti.
3. V kořenovém adresáři vašeho webu vytvořte nový soubor s názvem *ChartSaveToCache.cshtml*.
4. Nahraďte existující obsah následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Kód nejprve zkontroluje, zda něco bylo předáno jako hodnota klíče v řetězci dotazu. Pokud ano, kód se pokusí číst graf z `GetFromCache` mezipaměti voláním metody a předáním klíče. Pokud se ukáže, že v mezipaměti pod tímto klíčem není nic (což by se stalo při prvním požadavku grafu), kód vytvoří graf obvyklým způsobem. Po dokončení grafu kód uloží do mezipaměti voláním `SaveToCache`. Tato metoda vyžaduje klíč (takže graf lze požadovat později) a množství času, který by měl být uložen v mezipaměti. (Přesný čas, kdy byste do mezipaměti grafu by záviset na tom, jak často jste si mysleli, že data, která představuje může změnit.) Metoda `SaveToCache` také vyžaduje `slidingExpiration` parametr &#8212; pokud je nastavena na hodnotu true, čítač časového období se resetuje při každém přístupu k grafu. V tomto případě to ve skutečnosti znamená, že platnost položky mezipaměti grafu vyprší 2 minuty po posledním přístupu uživatele k grafu. (Alternativou k posuvné vypršení platnosti je absolutní vypršení platnosti, což znamená, že položka mezipaměti vyprší přesně 2 minuty po jeho uvedení do mezipaměti, bez ohledu na to, jak často byla zpřístupněna.)

    Nakonec kód používá `WriteFromCache` metodu k načtení a vykreslení grafu z mezipaměti. Všimněte si, že `if` tato metoda je mimo blok, který kontroluje mezipaměť, protože získá graf z mezipaměti, zda graf byl tam začít nebo musel být generována a uložena v mezipaměti.

    Všimněte si, že `AddTitle` v příkladu metoda obsahuje časové razítko. (Přidá aktuální datum a `DateTime.Now` čas &#8212; &#8212; do názvu.)
5. Vytvořte novou stránku s názvem *ClearCache.cshtml* a nahraďte její obsah následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Tato stránka `WebCache` používá pomocníka k odebrání grafu, který je uložen v mezipaměti *chartsavetocache.cshtml*. Jak již bylo uvedeno dříve, nemusíte normálně mít stránku, jako je tato. Vytváříte ji zde jen proto, abyste usnadnili testování ukládání do mezipaměti.
6. Spusťte webovou stránku *ShowCachedChart.cshtml* v prohlížeči. Stránka zobrazí obrázek grafu na základě kódu obsaženého v souboru *ChartSaveToCache.cshtml.* Poznamenejte si, co je v názvu grafu uvedeno časové razítko. 

    ![Popis: Obrázek základního grafu s časovým razítkem v názvu grafu](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Zavřete prohlížeč.
8. Spusťte *znovu soubor ShowCachedChart.cshtml.* Všimněte si, že časové razítko je stejné jako dříve, což znamená, že graf nebyl obnoven, ale místo toho byl přečten z mezipaměti.
9. V *souboru ShowCachedChart.cshtml*klepněte na odkaz **Vymazat mezipaměť.** Tím přejdete na *ClearCache.cshtml*, který hlásí, že mezipaměť byla vymazána.
10. Klepněte na odkaz **Return to ShowCachedChart.cshtml** nebo znovu spusťte *showCachedChart.cshtml* z WebMatrix. Všimněte si, že tentokrát se časové razítko změnilo, protože mezipaměť byla vymazána. Proto kód musel znovu vygenerovat graf a vrátit jej zpět do mezipaměti.

### <a name="saving-a-chart-as-an-image-file"></a>Uložení grafu jako obrazového souboru

Graf můžete také uložit jako soubor obrázku (například jako soubor *JPG)* na serveru. Soubor obrázku pak můžete použít stejně jako libovolný obrázek. Výhodou je, že soubor je uložen, nikoli uložen do dočasné mezipaměti. Nový obrázek grafu můžete uložit v různých časech (například každou hodinu) a pak uchovávat trvalý záznam o změnách, ke kterým dochází v průběhu času. Všimněte si, že je třeba se ujistit, že vaše webová aplikace má oprávnění k uložení souboru do složky na serveru, kam chcete umístit soubor obrázku.

1. V kořenovém adresáři webu vytvořte složku s názvem * \_ChartFiles,* pokud ještě neexistuje.
2. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartSave.cshtml*.
3. Nahraďte existující obsah následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Kód nejprve zkontroluje, zda soubor *JPG* existuje `File.Exists` voláním metody. Pokud soubor neexistuje, kód vytvoří nový `Chart` z pole. Tentokrát kód volá metodu `Save` a `path` předá parametr určit cestu k souboru a název souboru, kam chcete uložit graf. V textu stránky `<img>` element používá cestu k zobrazení souboru *JPG.*
4. Spusťte soubor *ChartSave.cshtml.*
5. Vraťte se na WebMatrix. Všimněte si, že soubor obrázku s názvem *chart01.jpg* byl uložen ve * \_* složce ChartFiles.

### <a name="saving-a-chart-as-an-xml-file"></a>Uložení grafu jako souboru XML

Nakonec můžete graf uložit jako soubor XML na server. Výhodou použití této metody při ukládání grafu do mezipaměti nebo ukládání grafu do souboru je, že můžete upravit xml před zobrazením grafu, pokud chcete. Aplikace musí mít oprávnění ke čtení a zápisu pro složku na serveru, kam chcete umístit soubor obrázku.

1. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartSaveXml.cshtml*.
2. Nahraďte existující obsah následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Tento kód je podobný kódu, který jste viděli dříve pro ukládání grafu do mezipaměti, s tím rozdílem, že používá soubor XML. Kód nejprve zkontroluje, zda soubor XML `File.Exists` existuje voláním metody. Pokud soubor existuje, kód vytvoří `Chart` nový objekt a předá `themePath` název souboru jako parametr. Tím se vytvoří graf na základě toho, co je v souboru XML. Pokud soubor XML ještě neexistuje, vytvoří kód graf jako obvykle `SaveXml` a pak zavolá jeho uložení. Graf je vykreslen pomocí `Write` metody, jak jste viděli dříve.

    Stejně jako u stránky, která ukázala ukládání do mezipaměti, tento kód obsahuje časové razítko v názvu grafu.
3. Vytvořte novou stránku s názvem *ChartDisplayXMLChart.cshtml* a přidejte k ní následující značky: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. Spusťte stránku *ChartDisplayXMLChart.cshtml.* Zobrazí se graf. Poznamenejte si časové razítko v názvu grafu.
5. Zavřete prohlížeč.
6. V aplikaci WebMatrix klepněte pravým **Refresh**tlačítkem * \_* myši na složku ChartFiles, klepněte na příkaz Aktualizovat a otevřete ji. Soubor *XMLChart.xml* v této složce `Chart` byl vytvořen pomocníkem. 

    ![Popis: Složka _ChartFiles zobrazující soubor XMLChart.xml vytvořený pomocníkem v grafu.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. Spusťte stránku *ChartDisplayXMLChart.cshtml* znovu. Graf zobrazuje stejné časové razítko jako při prvním spuštění stránky. Je to proto, že graf je generován z XML, který jste uložili dříve.
8. V aplikaci WebMatrix otevřete složku * \_ChartFiles* a odstraňte soubor *XMLChart.xml.*
9. Znovu spusťte stránku *ChartDisplayXMLChart.cshtml.* Tentokrát je časové razítko aktualizováno, protože `Chart` pomocník musel znovu vytvořit soubor XML. Pokud chcete, zkontrolujte složku * \_ChartFiles* a všimněte si, že soubor XML je zpět.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další zdroje

- [Úvod do práce s databází v ASP.NET webech webových stránek](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Použití ukládání do mezipaměti v ASP.NET webech webových stránek ke zvýšení výkonu](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Třída grafu](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (odkaz ASP.NET webových stránek rozhraní API na msdn)
