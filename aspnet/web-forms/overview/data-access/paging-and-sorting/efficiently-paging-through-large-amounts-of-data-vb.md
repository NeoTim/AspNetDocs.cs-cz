---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: Efektivní stránkování prostřednictvím velkých objemů dat (VB) | Microsoft Docs
author: rick-anderson
description: Výchozí možnost stránkování ovládacího prvku pro prezentaci dat není vhodná při práci s velkými objemy dat, protože jeho základní ovládací prvek zdroje dat získává...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d1c49e076e1c78e584f91fe2357a98da321f4260
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045101"
---
# <a name="efficiently-paging-through-large-amounts-of-data-vb"></a>Účinné stránkování velkých objemů dat (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe) nebo [Stáhnout PDF](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> Výchozí možnost stránkování ovládacího prvku pro prezentaci dat je nevhodná při práci s velkými objemy dat, protože jeho podkladový ovládací prvek zdroje dat načte všechny záznamy, i když se zobrazí pouze podmnožina dat. V takovém případě je nutné změnit vlastní stránkování.

## <a name="introduction"></a>Úvod

Jak jsme probrali v předchozím kurzu, můžete stránkování implementovat jedním ze dvou způsobů:

- **Výchozí stránkování** lze implementovat pouhým zaškrtnutím možnosti Povolit stránkování v inteligentní značce datová webová ovládání s. Při zobrazení stránky dat však prvek ObjectDataSource načte *všechny* záznamy, i když na stránce se zobrazí pouze podmnožina těchto záznamů.
- **Vlastní stránkování** vylepšuje výkon výchozích stránkování tím, že načítá pouze záznamy z databáze, které je třeba zobrazit pro konkrétní stránku dat požadovanou uživatelem. vlastní stránkování ale zahrnuje trochu větší úsilí při implementaci než výchozí stránkování.

Z důvodu snadné implementace stačí zaškrtnout políčko a znovu provést. výchozí stránkování je atraktivní možnost. Přístup k Naive při načítání všech záznamů je ale díky tomu implausible volba při stránkování přes dostatečně velké objemy dat nebo pro weby s mnoha souběžnými uživateli. V takovém případě je nutné změnit vlastní stránkování, aby poskytovala reagující systém.

Výzvou k vlastnímu stránkování je schopnost zapisovat dotaz, který vrací přesně sadu záznamů potřebných pro konkrétní stránku dat. Naštěstí Microsoft SQL Server 2005 poskytuje nové klíčové slovo pro výsledky řazení, které nám umožňuje napsat dotaz, který může efektivně načíst správnou podmnožinu záznamů. V tomto kurzu se dozvíte, jak používat toto nové klíčové slovo SQL Server 2005 k implementaci vlastního stránkování v ovládacím prvku GridView. I když je uživatelské rozhraní pro vlastní stránkování stejné jako výchozí stránkování, krokování z jedné stránky na další s použitím vlastního stránkování může být několik objednávek rychleji než výchozí stránkování.

> [!NOTE]
> Přesný nárůst výkonu vystavený vlastním stránkováním závisí na celkovém počtu záznamů, které jsou stránkovaná, a zatížení na databázovém serveru. Na konci tohoto kurzu se podíváme na některé hrubé metriky, které prezentují výhody ve výkonu získané prostřednictvím vlastního stránkování.

## <a name="step-1-understanding-the-custom-paging-process"></a>Krok 1: Princip procesu vlastního stránkování

Při stránkování přes data jsou přesné záznamy zobrazené na stránce závislé na požadované stránce dat a na počtu zobrazených záznamů na stránce. Představte si například, že jsme chtěli stránku procházet 81 produktů a zobrazit 10 produktů na stránku. Při prohlížení první stránky chceme, aby byly produkty od 1 do 10. Při prohlížení druhé stránky, které vám d zajímá produkty 11 až 20 atd.

Existují tři proměnné, které určují, jaké záznamy je potřeba načíst a jak se mají vykreslovat rozhraní stránkování:

- **Začátek indexu řádku** index prvního řádku na stránce dat, která se má zobrazit; Tento index lze vypočítat vynásobením indexu stránky záznamy, které se mají zobrazit na stránce a přidáním jednoho. Například při stránkování prostřednictvím záznamů 10 pro první stránku (jejíž index stránky je 0) je index řádku začátek 0 \* 10 + 1 nebo 1; pro druhou stránku (jejíž index stránky je 1), index řádku začátku je 1 \* 10 + 1 nebo 11.
- **Maximální počet řádků** , které se mají zobrazit na jednu stránku (maximální počet záznamů) Tato proměnná se označuje jako maximální počet řádků, od poslední stránky může být méně záznamů vráceno, než je velikost stránky. Například když stránkování přes 81 Products 10 záznamů na stránku, bude mít devátá a poslední stránka pouze jeden záznam. Žádná stránka, ale zobrazí více záznamů, než je hodnota maximální počet řádků.
- **Celkový** počet záznamů, celkový počet záznamů, které jsou stránkované. I když tato proměnná není potřebná k určení záznamů, které se mají načíst pro danou stránku, nadiktujte rozhraní stránkování. Pokud se například stránkují 81 Products, rozhraní stránkování ví, že v uživatelském rozhraní stránkování zobrazí devět čísel stránek.

S výchozím stránkováním je index řádku zahájení vypočítán jako součin indexu stránky a velikosti stránky plus jedna, zatímco maximální počet řádků je pouze velikost stránky. Vzhledem k tomu, že výchozí stránkování načítá všechny záznamy z databáze při vykreslování libovolné stránky dat, je známý index pro každý řádek, čímž se při přechodu na řádek indexu počátečního řádku jedná o triviální úlohu. Celkový počet záznamů je navíc k dispozici okamžitě, protože je jednoduše počet záznamů v objektu DataTable (nebo jakýkoli objekt, který se používá k uchování výsledků databáze).

Když je zadaný index počátečního řádku a maximální počet řádků, musí implementace vlastního stránkování vracet jenom přesnou podmnožinu záznamů počínaje indexem počátečního řádku a až po dobu až po maximum řádků. Vlastní stránkování nabízí dva problémy:

- Musíme být schopni efektivně přidružit index řádku ke každému řádku v celých datech, která jsou stránkovaná, aby bylo možné začít vracet záznamy na zadaném indexu počátečního řádku.
- Musíme zadat celkový počet záznamů, které se stránkují.

V následujících dvou krocích prověříme skript SQL, který je potřeba k tomu, aby reagoval na tyto dva problémy. Kromě skriptu SQL budeme také muset implementovat metody do DAL a knihoven BLL.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>Krok 2: vrácení celkového počtu záznamů, které jsou stránkované prostřednictvím

Než se podíváme, jak načíst přesnou podmnožinu záznamů pro stránku, která se zobrazuje, Podívejme se nejprve na to, jak vrátit celkový počet záznamů, které jsou stránkou. Tyto informace jsou potřebné k tomu, aby bylo možné správně nakonfigurovat stránkovací uživatelské rozhraní. Celkový počet záznamů vrácených konkrétním dotazem SQL lze získat pomocí [ `COUNT` agregační funkce](https://msdn.microsoft.com/library/ms175997.aspx). Například k určení celkového počtu záznamů v `Products` tabulce můžeme použít následující dotaz:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

Pojďme do našeho DAL přidat metodu, která tyto informace vrátí. Konkrétně vytvoříme metodu DAL s názvem `TotalNumberOfProducts()` , která provede `SELECT` příkaz uvedený výše.

Začněte otevřením `Northwind.xsd` souboru typované datové sady ve `App_Code/DAL` složce. Potom klikněte pravým tlačítkem myši na `ProductsTableAdapter` v návrháři a vyberte možnost Přidat dotaz. Jak jsme se seznámili v předchozích kurzech, to nám umožní přidat novou metodu na DAL, který při vyvolání spustí konkrétní příkaz SQL nebo uloženou proceduru. Podobně jako u našich TableAdapter metod v předchozích kurzech se tato možnost používá k použití ad-hoc SQL příkazu.

![Použití příkazu SQL ad hoc](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**Obrázek 1**: použití příkazu SQL ad hoc

Na další obrazovce můžeme zadat typ dotazu, který se má vytvořit. Vzhledem k tomu, že tento dotaz vrátí jednu, skalární hodnotu, zobrazí se v tabulce celkový počet záznamů v `Products` tabulce, `SELECT` která vrací hodnotu jednotlivě.

![Nakonfigurujte dotaz tak, aby používal příkaz SELECT, který vrací jedinou hodnotu.](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**Obrázek 2**: Nakonfigurujte dotaz tak, aby používal příkaz SELECT, který vrací jedinou hodnotu.

Po označení typu dotazu, který se má použít, je nutné zadat dotaz Next.

![Použít dotaz na výběr počtu (*) z produktů](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**Obrázek 3**: použití dotazu vybrat počet ( \* ) z produktu

Nakonec zadejte název metody. Jak je uvedeno výše, můžeme použít `TotalNumberOfProducts` .

![Pojmenujte metodu DAL TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**Obrázek 4**: pojmenování metody dal TotalNumberOfProducts

Po kliknutí na tlačítko Dokončit průvodce přidá `TotalNumberOfProducts` metodu do dal. Skalární návratové metody v DAL vrací typy s možnou hodnotou null pro případ, že je výsledek dotazu SQL `NULL` . Náš `COUNT` dotaz však vždycky vrátí nenulovou `NULL` hodnotu; bez ohledu na to, že metoda dal vrátí celé číslo s možnou hodnotou null.

Kromě metody DAL potřebujeme také metodu v knihoven BLL. Otevřete `ProductsBLL` soubor třídy a přidejte `TotalNumberOfProducts` metodu, která jednoduše zavolá metodu dal s `TotalNumberOfProducts` :

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

Metoda DAL s `TotalNumberOfProducts` vrací celé číslo s možnou hodnotou null, ale jsme vytvořili `ProductsBLL` metodu třídy s `TotalNumberOfProducts` , aby vracela standardní celé číslo. Proto potřebujeme, aby `ProductsBLL` Metoda třídy, `TotalNumberOfProducts` vrátila hodnotu v rámci celého čísla s možnou hodnotou null vráceného metodou dal s `TotalNumberOfProducts` . Volání `GetValueOrDefault()` funkce vrátí hodnotu celého čísla s možnou hodnotou null, pokud existuje. Pokud je však celé číslo s možnou hodnotou null, `null` vrátí výchozí celočíselnou hodnotu 0.

## <a name="step-3-returning-the-precise-subset-of-records"></a>Krok 3: vrácení přesné podmnožiny záznamů

Naším dalším úkolem je vytvořit metody v rámci DAL a knihoven BLL, které přijímají index počátečního řádku a maximální výše popsané proměnné řádků a vracejí příslušné záznamy. Než to uděláte, Podívejme se nejprve na potřebný skript SQL. K tomu čelíme, že musíme být schopni efektivně přiřadit index ke každému řádku v rámci celých výsledků, které jsou stránkovaná, aby bylo možné vracet pouze ty záznamy, které začínají indexem počátečního řádku (a až do maximálního počtu záznamů).

Nejedná se o výzvu, pokud je v tabulce databáze již sloupec, který slouží jako index řádku. Na první pohled si můžeme všimnout, že `Products` pole s tabulkami `ProductID` by poznamenalo, protože první produkt má `ProductID` 1, druhý a 2 atd. Odstraněním produktu se ale v sekvenci opustí mezeru, nullifying tento přístup.

K dispozici jsou dvě obecné techniky, pomocí kterých můžete efektivně přidružit index řádku k datům, která se stránkují, a tím umožnit načtení přesné podmnožiny záznamů:

- **Použití SQL Server 2005 s `ROW_NUMBER()` Klíčové** slovo new SQL Server 2005, `ROW_NUMBER()` klíčové slovo přidružuje hodnocení každému vrácenému záznamu na základě určitého řazení. Toto hodnocení lze použít jako index řádku pro každý řádek.
- **Použití proměnné tabulky a `SET ROWCOUNT` ** [ `SET ROWCOUNT` Příkaz](https://msdn.microsoft.com/library/ms188774.aspx) SQL Server s lze použít k určení, kolik celkových záznamů má dotaz zpracovat před ukončením; [proměnné tabulky](http://www.sqlteam.com/item.asp?ItemID=9454) jsou lokální proměnné T-SQL, které mohou uchovávat tabulková data, podobají [dočasné tabulky](http://www.sqlteam.com/item.asp?ItemID=2029). Tento přístup funguje stejně dobře Microsoft SQL Server 2005 i SQL Server 2000 (zatímco `ROW_NUMBER()` přístup funguje jenom s SQL Server 2005).  
  
  Nápad je vytvořit proměnnou tabulky, která má `IDENTITY` sloupec a sloupce pro primární klíče tabulky, jejichž data jsou stránkovaná. V dalším kroku se obsah tabulky, jejíž data se stránkuje, dohlíží do proměnné tabulky, takže se pro každý záznam v tabulce přidruží sekvenční index řádku (přes `IDENTITY` sloupec). Po naplnění proměnné tabulky `SELECT` může být proveden příkaz v proměnné tabulky, který je spojen s podkladovou tabulkou, a vyžádat si konkrétní záznamy. `SET ROWCOUNT`Příkaz se používá k inteligentnímu omezení počtu záznamů, které musí být v proměnné tabulky dumpingové.  
  
  Tento přístup s efektivitou je založený na požadovaném číslu stránky, protože `SET ROWCOUNT` je hodnotě přiřazena hodnota indexu počátečního řádku a maximální počet řádků. Při stránkování na stránky s nízkými čísly, například na prvních několika stránkách dat, tento přístup je velmi efektivní. Ale při načítání stránky poblíž konce vykazuje výchozí výkon stránkování jako.

Tento kurz implementuje vlastní stránkování pomocí `ROW_NUMBER()` klíčového slova. Další informace o použití proměnné tabulky a techniky najdete `SET ROWCOUNT` v článku [efektivnější způsob stránkování prostřednictvím rozsáhlých sad výsledků](http://www.4guysfromrolla.com/webtech/042606-1.shtml).

`ROW_NUMBER()`Klíčové slovo, které je přidružené k hodnocení pomocí konkrétního řazení, pomocí následující syntaxe:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` vrátí číselnou hodnotu, která určuje pořadí pro každý záznam s ohledem na označené řazení. Pokud například chcete zobrazit pořadí jednotlivých produktů seřazené od nejdražších po nejnižší, můžeme použít následující dotaz:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

Obrázek 5 ukazuje tento dotaz s výsledky při spuštění prostřednictvím okna dotazu v aplikaci Visual Studio. Všimněte si, že produkty jsou seřazené podle ceny a zároveň s cenovou známkou pro každý řádek.

![Cenové pořadí je zahrnuté pro každý vrácený záznam.](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**Obrázek 5**: cenová klasifikace je zahrnutá u každého vráceného záznamu.

> [!NOTE]
> `ROW_NUMBER()` je jenom jedna z mnoha nových funkcí hodnocení dostupných v SQL Server 2005. Podrobnější diskuzi o `ROW_NUMBER()` , spolu s dalšími funkcemi hodnocení, najdete v článku o [vracení výsledků seřazené podle Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml).

Při řazení výsledků podle zadaného `ORDER BY` sloupce v `OVER` klauzuli ( `UnitPrice` v předchozím příkladu) musí SQL Server seřadit výsledky. Jedná se o rychlou operaci, pokud se ve sloupcích nachází clusterovaný index, ve kterém jsou výsledky seřazeny, nebo v případě, že existuje pokrýváný index, ale může být levnější v jiném. Chcete-li zlepšit výkon pro dostatečně velké dotazy, zvažte přidání neclusterovaných indexů pro sloupec, podle kterého jsou výsledky seřazeny. Podrobnější informace najdete v tématu věnovaném [funkcím řazení a výkonu v SQL Server 2005](http://www.sql-server-performance.com/ak_ranking_functions.asp) .

Informace o řazení vrácené funkcí `ROW_NUMBER()` nelze v klauzuli použít přímo `WHERE` . Odvozenou tabulku však lze použít k vrácení `ROW_NUMBER()` výsledku, který lze poté zobrazit v `WHERE` klauzuli. Následující dotaz například používá odvozenou tabulku pro vrácení sloupců NázevVýrobku a UnitPrice společně s `ROW_NUMBER()` výsledkem a pak použije `WHERE` klauzuli, která vrátí pouze ty produkty, jejichž cenová klasifikace je mezi 11 a 20:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

Dalším rozšiřováním tohoto konceptu můžete využít tento přístup k načtení konkrétní stránky dat podle požadovaného indexu počátečního řádku a maximální hodnoty řádků:

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> Jak uvidíme později v tomto kurzu, *`StartRowIndex`* je zadaný prvek ObjectDataSource indexován od nuly, zatímco `ROW_NUMBER()` hodnota vrácená SQL Server 2005 je indexována od 1. Proto `WHERE` klauzule vrátí tyto záznamy, kde `PriceRank` je striktně větší než *`StartRowIndex`* a menší než nebo rovno *`StartRowIndex`*  +  *`MaximumRows`* .

Teď, když jsme probrali, jak `ROW_NUMBER()` se dá použít k načtení konkrétní stránky dat z indexu počátečního řádku a maximálního počtu řádků, teď je potřeba tuto logiku implementovat jako metody v dal a knihoven BLL.

Při vytváření tohoto dotazu musíte určit řazení, podle kterého budou výsledky seřazeny. v abecedním pořadí si můžeme produkty seřadit podle názvu. To znamená, že s implementací vlastního stránkování v tomto kurzu nebudeme moct vytvořit vlastní stránkovou sestavu, než dá se taky seřadit. V dalším kurzu ale uvidíte, jak se tyto funkce dají zadat.

V předchozí části jsme vytvořili metodu DAL jako příkaz SQL ad hoc. Analyzátor T-SQL v aplikaci Visual Studio, který využíval Průvodce TableAdapter, nefunguje jako syntaxe, kterou `OVER` funkce používá `ROW_NUMBER()` . Proto je nutné vytvořit tuto metodu DAL jako uloženou proceduru. V nabídce zobrazení vyberte Průzkumník serveru (nebo stiskněte kombinaci kláves CTRL + ALT + S) a rozbalte `NORTHWND.MDF` uzel. Chcete-li přidat novou uloženou proceduru, klikněte pravým tlačítkem na uzel uložené procedury a vyberte možnost Přidat novou uloženou proceduru (viz obrázek 6).

![Přidat novou uloženou proceduru pro stránkování prostřednictvím produktů](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**Obrázek 6**: Přidání nové uložené procedury pro stránkování prostřednictvím produktů

Tato uložená procedura by měla přijmout dva celočíselné vstupní parametry – `@startRowIndex` a `@maximumRows` použít `ROW_NUMBER()` funkci seřazenou podle `ProductName` pole a vracet pouze ty řádky, které jsou větší než zadané `@startRowIndex` a menší nebo rovny hodnotě `@startRowIndex`  +  `@maximumRow` s. Do nové uložené procedury zadejte následující skript a potom kliknutím na ikonu Uložit přidejte uloženou proceduru do databáze.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

Po vytvoření uložené procedury chvíli počkejte, než se otestuje. Klikněte pravým tlačítkem na `GetProductsPaged` název uložené procedury v Průzkumník serveru a vyberte možnost provést. Visual Studio vás pak vyzve k zadání vstupních parametrů `@startRowIndex` a `@maximumRow` s (viz obrázek 7). Zkuste použít jiné hodnoty a prověřte výsledky.

![Zadejte hodnotu @startRowIndex parametrů a. @maximumRows](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>Obrázek 7</strong>: zadejte hodnotu @startRowIndex parametrů a. @maximumRows

Po zvolení hodnot vstupních parametrů zobrazí okno výstup výsledky. Obrázek 8 ukazuje výsledky při průchodu 10 pro `@startRowIndex` `@maximumRows` parametry a.

[![Vrátí se záznamy, které by se zobrazily na druhé stránce dat.](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**Obrázek 8**: vrátí se záznamy, které by se zobrazily na druhé stránce dat ([kliknutím zobrazíte obrázek v plné velikosti).](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png)

Po vytvoření této uložené procedury jsme připraveni vytvořit `ProductsTableAdapter` metodu. Otevřete `Northwind.xsd` typovou datovou sadu, klikněte na ni pravým tlačítkem `ProductsTableAdapter` a vyberte možnost Přidat dotaz. Místo vytvoření dotazu pomocí příkazu SQL ad hoc ho vytvořte pomocí existující uložené procedury.

![Vytvoření metody DAL pomocí existující uložené procedury](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**Obrázek 9**: vytvoření metody dal pomocí existující uložené procedury

V dalším kroku se zobrazí výzva, abyste vybrali uloženou proceduru, která se má vyvolat. `GetProductsPaged`Z rozevíracího seznamu vyberte uloženou proceduru.

![Z rozevíracího seznamu vyberte uloženou proceduru GetProductsPaged.](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**Obrázek 10**: z rozevíracího seznamu vyberte uloženou proceduru GetProductsPaged.

Na další obrazovce se zobrazí dotaz, jaký typ dat je vrácen uloženou procedurou: tabulková data, jedna hodnota nebo žádná hodnota. Vzhledem k `GetProductsPaged` tomu, že úložná procedura může vracet více záznamů, naznačí, že vrátí tabulková data.

![Označení, že uložená procedura vrátí tabulková data](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**Obrázek 11**: označení, že uložená procedura vrátí tabulková data

Nakonec uveďte názvy metod, které chcete vytvořit. Stejně jako u našich předchozích kurzů, pokračujte a vytvořte metody pomocí naplnit objekt DataTable a vraťte DataTable. Pojmenujte první metodu `FillPaged` a druhou `GetProductsPaged` .

![Pojmenování metod FillPaged a GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**Obrázek 12**: pojmenování metod FillPaged a GetProductsPaged

Kromě vytvoření metody DAL pro vrácení konkrétní stránky produktů je také potřeba poskytnout tyto funkce v knihoven BLL. Podobně jako u metody DAL musí metoda knihoven BLL s GetProductsPaged přijmout dva celočíselné vstupy pro zadání indexu počátečního řádku a maximálního počtu řádků a musí vracet pouze ty záznamy, které spadají do zadaného rozsahu. Vytvořte takovou metodu knihoven BLL ve třídě ProductsBLL, která se pouze zavolá do metody GetProductsPaged DAL s, například:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

Můžete použít libovolný název pro vstupní parametry metody knihoven BLL, ale to, jak se vám bude brzy zobrazovat, zvolit, co je potřeba pro `startRowIndex` `maximumRows` použití této metody při konfiguraci prvku ObjectDataSource použít a uložit.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>Krok 4: Konfigurace prvku ObjectDataSource pro použití vlastního stránkování

Díky metodám knihoven BLL a DAL pro přístup k určité podmnožině záznamů je vše připraveno k vytvoření ovládacího prvku GridView, který provede stránky prostřednictvím svých podkladových záznamů pomocí vlastního stránkování. Začněte tím, že otevřete `EfficientPaging.aspx` stránku ve `PagingAndSorting` složce, přidáte na stránku prvek GridView a nakonfigurujete ji tak, aby používala nový ovládací prvek ObjectDataSource. V předchozích kurzech máme často nakonfigurovaný prvek ObjectDataSource, aby používal `ProductsBLL` metodu třídy s `GetProducts` . Tentokrát ale chceme použít `GetProductsPaged` metodu místo toho, protože `GetProducts` Metoda vrátí *všechny* produkty v databázi, zatímco `GetProductsPaged` vrátí pouze konkrétní podmnožinu záznamů.

![Konfigurace prvku ObjectDataSource pro použití metody ProductsBLL třídy s GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**Obrázek 13**: Konfigurace prvku ObjectDataSource pro použití metody ProductsBLL třídy s GetProductsPaged

Vzhledem k tomu, že jsme znovu vytvořili prvek GridView, který je jen pro čtení, chvíli počkejte, než nastavíte rozevírací seznam metoda na kartách vložení, aktualizace a odstranění na (žádné).

V dalším kroku průvodce ObjectDataSource vyzve pro zdroje `GetProductsPaged` metod s `startRowIndex` a `maximumRows` hodnot vstupních parametrů. Tyto vstupní parametry budou ve skutečnosti automaticky nastaveny pomocí prvku GridView, takže zdrojovou sadu jednoduše ponechte nastavenou na None a klikněte na tlačítko Dokončit.

![Ponechat zdroje vstupních parametrů jako žádné](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**Obrázek 14**: ponechte zdroje vstupních parametrů jako žádné.

Po dokončení průvodce ObjectDataSource bude prvek GridView obsahovat vlastnost BoundField nebo třídě CheckBoxField podporována pro každé pole dat produktu. Nebojte se přizpůsobit vzhled prvku GridView, jak je vidět. Zobrazuje se jenom BoundFields,,, `ProductName` `CategoryName` `SupplierName` `QuantityPerUnit` a `UnitPrice` . Také nakonfigurujete prvek GridView tak, aby podporoval stránkování, zaškrtnutím políčka Povolit stránkování v jeho inteligentní značce. Po těchto změnách by deklarativní označení GridView a ObjectDataSource mělo vypadat podobně jako následující:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

Pokud ale navštívíte stránku prostřednictvím prohlížeče, ovládací prvek GridView však není tam, kde má být nalezen.

![Prvek GridView není zobrazen](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**Obrázek 15**: prvek GridView není zobrazen.

Prvek GridView chybí, protože prvek ObjectDataSource aktuálně používá hodnotu 0 jako hodnoty pro oba `GetProductsPaged` `startRowIndex` `maximumRows` vstupní parametry a. Proto výsledný dotaz SQL nevrací žádné záznamy, takže prvek GridView není zobrazen.

Chcete-li tento problém napravit, musíme prvek ObjectDataSource nakonfigurovat tak, aby používal vlastní stránkování. To lze provést v následujících krocích:

1. **Nastavte vlastnost ObjectDataSource s `EnablePaging` na `true` ** this, která určuje prvek ObjectDataSource, který musí předat do `SelectMethod` dvou dalších parametrů: jeden pro určení indexu počátečního řádku ( [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) ) a jeden pro určení maximálního počtu řádků ( [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) ).
2. **Nastavte prvek ObjectDataSource s `StartRowIndexParameterName` a `MaximumRowsParameterName` vlastnosti odpovídajícím způsobem** `StartRowIndexParameterName` a vlastností, které `MaximumRowsParameterName` označují názvy vstupních parametrů předaných do `SelectMethod` pro účely vlastního stránkování. Ve výchozím nastavení jsou tyto názvy parametrů `startIndexRow` a `maximumRows` , což je důvod, proč při vytváření `GetProductsPaged` metody v knihoven BLL použili tyto hodnoty pro vstupní parametry. Pokud se rozhodnete použít jiné názvy parametrů pro metodu knihoven BLL, `GetProductsPaged` například `startIndex` a `maxRows` , například byste museli nastavit prvek ObjectDataSource s `StartRowIndexParameterName` a `MaximumRowsParameterName` vlastnosti odpovídajícím způsobem (například startIndex pro `StartRowIndexParameterName` a maxRows pro `MaximumRowsParameterName` ).
3. **Nastavte [ `SelectCountMethod` vlastnost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) ObjectDataSource s na název metody, která vrátí celkový počet záznamů, které jsou stránkou prostřednictvím ( `TotalNumberOfProducts` )** odvolání, že `ProductsBLL` `TotalNumberOfProducts` Metoda třídy vrátí celkový počet záznamů, které jsou stránkou, pomocí metody dal, která spouští `SELECT COUNT(*) FROM Products` dotaz. Tyto informace vyžaduje prvek ObjectDataSource, aby bylo možné správně vykreslit rozhraní stránkování.
4. **Odeberte `startRowIndex` elementy a `maximumRows` `<asp:Parameter>` z deklarativní značky ObjectDataSource** při konfiguraci prvku ObjectDataSource prostřednictvím průvodce. Visual Studio automaticky přidalo dva `<asp:Parameter>` prvky pro `GetProductsPaged` vstupní parametry metody. Nastavením `EnablePaging` na `true` tyto parametry budou předány automaticky; Pokud jsou také zobrazeny v deklarativní syntaxi, prvek ObjectDataSource se pokusí předat do metody *čtyři* parametry `GetProductsPaged` a dva parametry `TotalNumberOfProducts` metody. Pokud zapomenete odebrat tyto `<asp:Parameter>` prvky, zobrazí se při návštěvě stránky v prohlížeči chybová zpráva, například: *ObjectDataSource ' ObjectDataSource1 ' nemůže najít neobecnou metodu ' TotalNumberOfProducts ', která má parametry: StartRowIndex, MaximumRows*.

Po provedení těchto změn by deklarativní syntaxe ObjectDataSource s měla vypadat takto:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

Všimněte si, `EnablePaging` že `SelectCountMethod` vlastnosti a byly nastaveny a `<asp:Parameter>` prvky byly odebrány. Obrázek 16 ukazuje snímek obrazovky okno Vlastnosti poté, co byly provedeny tyto změny.

![Chcete-li použít vlastní stránkování, nakonfigurujte ovládací prvek ObjectDataSource](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**Obrázek 16**: použití vlastního stránkování, konfigurace ovládacího prvku ObjectDataSource

Po provedení těchto změn navštivte tuto stránku v prohlížeči. Měli byste vidět seznam 10 produktů seřazený podle abecedy. Chvíli počkejte, než budou data postupně procházet jednou stránkou. I když z pohledu koncového uživatele mezi výchozím stránkováním a vlastním stránkováním nedochází k žádnému vizuálnímu rozdílu, vlastní stránkování je efektivněji stránkou prostřednictvím velkých objemů dat, protože načítá pouze ty záznamy, které se musí zobrazit pro danou stránku.

[![Data seřazená podle názvu produktu jsou stránkovaná s použitím vlastního stránkování.](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**Obrázek 17**: data seřazená podle názvu produktu jsou stránkovaná pomocí vlastního stránkování ([kliknutím zobrazíte obrázek v plné velikosti).](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png)

> [!NOTE]
> U vlastního stránkování je hodnota počtu stránek vrácená ovládacím prvkem ObjectDataSource `SelectCountMethod` uložena ve stavu zobrazení prvku GridView. Další proměnné GridView `PageIndex` , `EditIndex` ,, `SelectedIndex` `DataKeys` kolekce a tak dále jsou uloženy ve *stavu ovládacího prvku*, který je trvalý bez ohledu na hodnotu vlastnosti prvku GridView `EnableViewState` . Vzhledem k tomu, `PageCount` že je hodnota trvalá napříč zpětnými odesláními pomocí stavu zobrazení, při použití rozhraní stránkování, které obsahuje odkaz pro přechod na poslední stránku, je nezbytné, aby byl stav zobrazení prvku GridView povolen. (Pokud rozhraní pro stránkování neobsahuje přímý odkaz na poslední stránku, můžete stav zobrazení zakázat.)

Kliknutím na odkaz na poslední stránku dojde k postbacku a ovládací prvek GridViewa vydá pokyn, aby aktualizoval svou `PageIndex` vlastnost. Pokud se klikne na odkaz na poslední stránku, ovládací prvek GridView přiřadí jeho `PageIndex` vlastnost k hodnotě, která je nižší než jeho `PageCount` vlastnost. Je-li stav zobrazení zakázán, `PageCount` hodnota je ztracena mezi zpětnými odesláními a `PageIndex` místo toho je přiřazena maximální celočíselná hodnota. V dalším kroku se prvek GridView pokusí určit počáteční index řádku vynásobením `PageSize` vlastností a `PageCount` . Výsledkem je, že `OverflowException` produkt překračuje maximální povolenou velikost celého čísla.

## <a name="implement-custom-paging-and-sorting"></a>Implementace vlastního stránkování a řazení

Naše aktuální implementace vlastního stránkování vyžaduje, aby se při vytváření uložené procedury určila objednávka, podle které jsou data stránkovaná `GetProductsPaged` . Nicméně jste si mohli všimnout, že inteligentní značka GridView s obsahuje kromě možnosti Povolit stránkování také zaškrtávací políčko Povolit řazení. Bohužel přidání podpory řazení do prvku GridView s naší aktuální implementací vlastního stránkování bude setříděno pouze záznamy na aktuálně zobrazené stránce dat. Pokud například nakonfigurujete prvek GridView tak, aby podporoval také stránkování a pak při zobrazení první stránky dat se v sestupném pořadí seřadí podle názvu produktu sestupně, obrátí se pořadí produktů na stránce 1. Jak ukazuje obrázek 18, například Carnarvon Tigers jako první produkt při řazení v obráceném abecedním pořadí, které ignoruje 71 dalších produktů, které jsou po Carnarvon Tigers, abecedně; pouze záznamy na první stránce jsou posuzovány v řazení.

[![Seřadí se jenom data zobrazená na aktuální stránce.](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**Obrázek 18**: seřazení pouze dat zobrazených na aktuální stránce ([kliknutím zobrazíte obrázek v plné velikosti](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))

Řazení se vztahuje pouze na aktuální stránku dat, protože k řazení dochází po načtení dat z `GetProductsPaged` metody knihoven BLL, a tato metoda vrátí pouze ty záznamy pro konkrétní stránku. Aby bylo řazení správně implementováno, je nutné předat do metody výraz řazení, aby `GetProductsPaged` bylo možné data seřadit odpovídajícím způsobem před vrácením konkrétní stránky dat. V našem dalším kurzu zjistíme, jak to provést.

## <a name="implementing-custom-paging-and-deleting"></a>Implementace vlastního stránkování a odstranění

Pokud povolíte odstraňování funkcí v prvku GridView, jehož data jsou stránkovaná pomocí vlastních technik stránkování, zjistíte, že při odstranění posledního záznamu z poslední stránky se v prvku GridView zmizí místo řádného snížení prvku GridView `PageIndex` . Pro reprodukování této chyby povolte odstranění pro kurz, který jsme právě vytvořili. Přejděte na poslední stránku (stránku 9), kde byste měli vidět jeden produkt, protože máme na sebe stránkování přes 81 produktů, 10 produktů najednou. Odstranit tento produkt

Po odstranění posledního produktu by prvek GridView *měl* automaticky přejít na osmá stránku a tato funkce se zobrazí s výchozím stránkováním. S vlastním stránkováním ale po odstranění tohoto posledního produktu na poslední stránce se v prvku GridView jednoduše z obrazovky úplně zmizí. Přesný důvod, *Proč* k tomu dochází, je trochu nad rámec tohoto kurzu; viz [odstranění posledního záznamu na poslední stránce z prvku GridView s vlastním stránkováním](http://scottonwriting.net/sowblog/posts/7326.aspx) pro podrobnosti nízké úrovně jako zdroj tohoto problému. V souhrnu je to kvůli následující sekvenci kroků, které jsou provedeny v prvku GridView při kliknutí na tlačítko Odstranit:

1. Odstranit záznam
2. Získejte příslušné záznamy, které se zobrazí pro zadané `PageIndex` a `PageSize`
3. Zkontrolujte, zda `PageIndex` nepřekračuje počet stránek dat ve zdroji dat; pokud má, automaticky sníží vlastnost GridView s. `PageIndex`
4. Vytvoření vazby příslušné stránky dat k prvku GridView pomocí záznamů získaných v kroku 2

Problém vychází z faktu, že v kroku 2, který se `PageIndex` používá, když se záznamy, které se mají zobrazit, je stále `PageIndex` Poslední stránkou, jejíž jediný záznam byl právě odstraněn. Proto v kroku 2 nejsou vráceny *žádné* záznamy, protože poslední stránka dat již neobsahuje žádné záznamy. V kroku 3 potom v ovládacím prvku GridView vzroste, že jeho `PageIndex` vlastnost je větší než celkový počet stránek ve zdroji dat (protože jsme na poslední stránce odstranili poslední záznam), a proto snižuje jeho `PageIndex` vlastnost. V kroku 4 se GridView pokusí vázat sebe na data získaná v kroku 2; v kroku 2 však nebyly vráceny žádné záznamy, takže výsledkem je prázdný prvek GridView. Při výchozím stránkování se tento problém nejedná o Surface t, protože v kroku 2 se ze zdroje dat načítají *všechny* záznamy.

K vyřešení tohoto problému máme dvě možnosti. První je vytvořit obslužnou rutinu události pro `RowDeleted` obslužnou rutinu události GridView s, která určuje, kolik záznamů bylo zobrazeno na stránce, která byla právě odstraněna. Pokud byl k dispozici pouze jeden záznam, musí být záznam právě odstraněn a musíme vysnížit prvky GridView `PageIndex` . Samozřejmě chceme aktualizovat pouze v případě, že `PageIndex` byla operace odstranění skutečně úspěšná, což lze určit tak, že zajistíte, že `e.Exception` vlastnost je `null` .

Tento přístup funguje, protože se aktualizuje `PageIndex` po kroku 1, ale před krokem 2. Proto se v kroku 2 vrátí vhodná sada záznamů. K tomu použijte kód podobný následujícímu:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

Alternativním řešením je vytvořit obslužnou rutinu události pro událost ObjectDataSource s `RowDeleted` a nastavit `AffectedRows` vlastnost na hodnotu 1. Po odstranění záznamu v kroku 1 (ale před opakovaným načtením dat v kroku 2) prvek GridView aktualizuje jeho `PageIndex` vlastnost, pokud jeden nebo více řádků ovlivnila operace. Vlastnost však není `AffectedRows` nastavena prvkem ObjectDataSource, a proto je tento krok vynechán. Jedním ze způsobů, jak tento krok provést, je ručně nastavit `AffectedRows` vlastnost, pokud se operace odstranění úspěšně dokončí. To lze provést pomocí kódu podobného následujícímu:

[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

Kód pro obě tyto obslužné rutiny události lze nalézt v třídě Code-na pozadí `EfficientPaging.aspx` příkladu.

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>Porovnání výkonu výchozích a vlastních stránkování

Vzhledem k tomu, že vlastní stránkování načítá pouze potřebné záznamy, zatímco výchozí stránkování vrátí *všechny* záznamy pro každou prohlíženou stránku, bude jasné, že vlastní stránkování je efektivnější než výchozí stránkování. Ale jenom to, jak mnohem efektivnější je vlastní stránkování? Jaký je způsob, jakým můžete obcházet nárůst výkonu přesunutím z výchozího stránkování do vlastního stránkování?

Neexistují však žádné místo, které by vyhovovaly všem odpovědím. Zvýšení výkonu závisí na několika faktorech, na nejvýraznějších dvou typech záznamů a na zatížení na databázovém serveru a na komunikačních kanálech mezi webovým serverem a databázovým serverem. U malých tabulek, které mají jen pár desítek záznamů, může být rozdíl výkonu zanedbatelný. V případě rozsáhlých tabulek, které mají tisíce až stovky tisíc řádků, je rozdíl mezi výkonem i čárkou.

Článek o svém [vlastním stránkování v ASP.NET 2,0 s SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)obsahuje některé testy výkonu, které jsem narazil na rozdíly mezi těmito dvěma technikami stránkování při procházení databázovými tabulkami pomocí záznamů 50 000. V těchto testech jsem zkoumal čas spustit dotaz na úrovni SQL Server (pomocí [SQL profileru](https://msdn.microsoft.com/library/ms173757.aspx)) a na stránce ASP.NET pomocí [funkcí trasování ASP.NET s](https://msdn.microsoft.com/library/y13fw6we.aspx). Pamatujte, že tyto testy byly spuštěny ve vývojovém poli s jedním aktivním uživatelem, a proto nejsou vědecky a Nenapodobují typický vzor zatížení webu. Bez ohledu na to, jaké výsledky ilustrují relativní rozdíly v době provádění výchozího a vlastního stránkování při práci s dostatečně velkým objemem dat.

|  | **Průměrná doba trvání (s)** | **Čtení** |
| --- | --- | --- |
| **Výchozí stránkovací Profiler SQL** | 1,411 | 383 |
| **Vlastní stránkování – Profiler SQL** | 0,002 | 29 |
| **Výchozí ASP.NET trasování stránkování** | 2,379 | *–* |
| **Vlastní ASP.NET trasování stránkování** | 0,029 | *–* |

Jak vidíte, načítají se konkrétní stránka dat, která vyžaduje 354 čtení v průměru a dokončených ve zlomcích času. Na stránce ASP.NET se vlastní stránka mohla vykreslit za blížící se 1/100<sup>tou</sup> dobu trvání při použití výchozího stránkování. V [tomto článku](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) najdete další informace o těchto výsledcích spolu s kódem a databází, kterou si můžete stáhnout pro reprodukování těchto testů ve vlastním prostředí.

## <a name="summary"></a>Souhrn

Výchozí stránkování je cinch k implementaci zaškrtnutím políčka Povolit stránkování v inteligentní značce webového ovládacího prvku dat, ale jednoduchost se dostane na náklady na výkon. S výchozím stránkováním, když uživatel požádá o jakoukoli stránku dat, vrátí se *všechny* záznamy, i když je možné zobrazit jenom malé zlomky. Pro boj proti této režii výkonu prvek ObjectDataSource nabízí alternativní stránkování možnosti stránkování.

I když se vlastní stránkování vylepšuje při potížích s výkonem výchozích stránkování načtením pouze těch záznamů, které je třeba zobrazit, je více zapojeno k implementaci vlastního stránkování. Nejprve je třeba zapsat dotaz, který bude správně (a efektivně) přistupovat ke konkrétní podmnožině požadovaných záznamů. To lze provést několika způsoby. ta, kterou jsme prozkoumali v tomto kurzu, je použití nové funkce SQL Server 2005 s `ROW_NUMBER()` k zařazení výsledků a vrácení pouze těch výsledků, jejichž řazení spadá do zadaného rozsahu. Kromě toho je potřeba přidat způsob, jak určit celkový počet záznamů, které se stránkují. Po vytvoření těchto metod DAL a knihoven BLL je také potřeba nakonfigurovat prvek ObjectDataSource tak, aby bylo možné určit, kolik celkových záznamů se stránkuje, a může správně předávat index řádků zahájení a maximální počet řádků pro knihoven BLL.

Při implementaci vlastního stránkování je potřeba provést několik kroků a není skoro tak jednoduché jako výchozí stránkování, vlastní stránkování je nutné při stránkování prostřednictvím dostatečně velkých objemů dat. Vzhledem k zobrazeným výsledkům může vlastní stránkování uvolnit sekundy od času vykreslování stránky ASP.NET a může vyšetřit zatížení databázového serveru o jeden mnohem více objednávek.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na adrese [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

> [!div class="step-by-step"]
> [Předchozí](paging-and-sorting-report-data-vb.md) 
>  [Další](sorting-custom-paged-data-vb.md)
