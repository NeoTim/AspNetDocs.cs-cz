---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: Použití závislostí mezipaměti SQL (C#) | Microsoft Docs
author: rick-anderson
description: Nejjednodušší strategie ukládání do mezipaměti je povolení vypršení platnosti dat uložených v mezipaměti po uplynutí určité doby. Tento jednoduchý přístup ale znamená, že data uložená v mezipaměti maintai...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 6a039cdfb1da294744b92648386468f69193ae6b
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045257"
---
# <a name="using-sql-cache-dependencies-c"></a>Použití závislostí mezipaměti SQL (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip) nebo [stažení PDF](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> Nejjednodušší strategie ukládání do mezipaměti je povolení vypršení platnosti dat uložených v mezipaměti po uplynutí určité doby. Tento jednoduchý přístup ale znamená, že data uložená v mezipaměti neudržují žádné spojení s podkladovým zdrojem dat. výsledkem jsou zastaralá data, která se uchovávají příliš dlouho nebo aktuální data, jejichž platnost vypršela příliš brzo. Lepším přístupem je použití třídy SqlCacheDependency, aby data zůstala ukládána do mezipaměti, dokud se jejich podkladová data nezměnila v databázi SQL. V tomto kurzu se dozvíte, jak.

## <a name="introduction"></a>Úvod

Techniky ukládání do mezipaměti, které jsou zkoumány v [ukládání dat do mezipaměti, pomocí ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) a [data do mezipaměti v](caching-data-in-the-architecture-cs.md) kurzech architektury používaly časový limit pro vyřazení dat z mezipaměti po uplynutí určité doby. Tento přístup představuje nejjednodušší způsob, jak vyrovnávat zvýšení výkonu při ukládání do mezipaměti proti neaktuálnosti dat. Když vyberete vypršení časového limitu *x* sekund, vývojář stránky se postará o výhody související s výkonem při ukládání do mezipaměti jenom po dobu *x* sekund, ale můžou klidně zabývat, že jeho data nikdy nebudou zastaralá déle než *x* sekund. U statických dat se samozřejmě dá *x* rozšířit až na životnost webové aplikace, jak byla prověřena v kurzu při [spuštění aplikace v datech ukládání do mezipaměti](caching-data-at-application-startup-cs.md) .

Při ukládání dat do mezipaměti se často vybrala doba vypršení platnosti na základě času, ale často je to nedostatečné řešení. V ideálním případě by data databáze zůstala uložená v mezipaměti, dokud se v databázi nezmění podkladová data. mezipaměť by pak měla být vyřazená. Tento přístup maximalizuje výhody výkonu ukládání do mezipaměti a minimalizuje dobu trvání zastaralých dat. Aby bylo možné využít tyto výhody, je třeba mít na paměti nějaký systém, který ví, že byla změněna podkladová data databáze a vyloučí odpovídající položky z mezipaměti. Před ASP.NET 2,0 byly pro implementaci tohoto systému zodpovědné vývojáři stránek.

ASP.NET 2,0 poskytuje [ `SqlCacheDependency` třídu](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) a potřebnou infrastrukturu k určení, kdy došlo ke změně v databázi, aby bylo možné vyřadit odpovídající položky v mezipaměti. Existují dva způsoby, jak určit, kdy se podkladová data změnila: oznámení a dotazování. Po prozkoumání rozdílů mezi oznámením a dotazování vytvoříme infrastrukturu potřebnou k podpoře cyklického dotazování a pak prozkoumat způsob použití `SqlCacheDependency` třídy v deklarativních a programově scénářích.

## <a name="understanding-notification-and-polling"></a>Principy oznámení a cyklického dotazování

Existují dva postupy, které lze použít k určení, kdy byla data v databázi upravena: oznámení a dotazování. V případě oznámení databáze automaticky upozorní modul runtime ASP.NET, když se od posledního spuštění dotazu změnily výsledky konkrétního dotazu, v jakém okamžiku jsou položky uložené v mezipaměti přidružené k dotazu vyřazeny. V případě cyklického dotazování databázový server uchovává informace o tom, kdy byly určité tabulky Poslední aktualizace. Modul runtime ASP.NET se pravidelně dotazuje databáze a kontroluje, které tabulky se od jejich zadání do mezipaměti změnily. V tabulkách, jejichž data byla změněna, jsou vyřazeny přidružené položky mezipaměti.

Možnost oznámení vyžaduje méně nastavení než cyklické dotazování a je podrobnější, protože sleduje změny na úrovni dotazu, nikoli na úrovni tabulky. Oznámení jsou bohužel dostupná jenom v plných edicích Microsoft SQL Server 2005 (tj. edice, které nejsou verze Express). Možnost dotazování se ale dá použít pro všechny verze Microsoft SQL Server od 7,0 do 2005. Vzhledem k tomu, že tyto kurzy používají Express Edition SQL Server 2005, zaměřte se na nastavení a použití možnosti cyklického dotazování. Další zdroje informací o možnostech oznámení SQL Server 2005 s najdete v části Další materiály pro čtení na konci tohoto kurzu.

Při cyklickém dotazování musí být databáze nakonfigurovaná tak, aby zahrnovala tabulku s názvem `AspNet_SqlCacheTablesForChangeNotification` , která má tři sloupce – `tableName` , `notificationCreated` a `changeId` . Tato tabulka obsahuje řádek pro každou tabulku obsahující data, která může být potřeba použít ve funkci závislosti mezipaměti SQL ve webové aplikaci. `tableName`Sloupec určuje název tabulky, zatímco se `notificationCreated` zobrazuje datum a čas přidání řádku do tabulky. `changeId`Sloupec je typu `int` a má počáteční hodnotu 0. Jeho hodnota se zvyšuje s každou úpravou tabulky.

Kromě `AspNet_SqlCacheTablesForChangeNotification` tabulky musí databáze také obsahovat triggery na každou tabulku, která se může objevit v závislosti mezipaměti SQL. Tyto triggery se spustí pokaždé, když se řádek vloží, aktualizuje nebo odstraní a zvýší `changeId` hodnotu tabulky v `AspNet_SqlCacheTablesForChangeNotification` .

Modul runtime ASP.NET sleduje aktuální `changeId` tabulku při ukládání dat do mezipaměti pomocí `SqlCacheDependency` objektu. Databáze je pravidelně kontrolována a všechny `SqlCacheDependency` objekty `changeId` , jejichž hodnota se liší od hodnoty v databázi, jsou vyřazeny, protože odlišná `changeId` hodnota označuje, že došlo ke změně tabulky, protože data byla uložena do mezipaměti.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>Krok 1: prozkoumání `aspnet_regsql.exe` programu příkazového řádku

V rámci přístupu pro cyklické dotazování musí být databáze nastavena tak, aby obsahovala výše popsanou infrastrukturu: předdefinovaná tabulka ( `AspNet_SqlCacheTablesForChangeNotification` ), několik uložených procedur a triggery na všech tabulkách, které lze použít v závislostech mezipaměti SQL ve webové aplikaci. Tyto tabulky, uložené procedury a triggery lze vytvořit pomocí programu příkazového řádku `aspnet_regsql.exe` , který najdete ve `$WINDOWS$\Microsoft.NET\Framework\version` složce. Chcete-li vytvořit `AspNet_SqlCacheTablesForChangeNotification` tabulku a přidružené uložené procedury, spusťte z příkazového řádku následující příkaz:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> Chcete-li provést tyto příkazy, je nutné, aby zadané přihlášení databáze bylo v [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) rolích a. Chcete-li ověřit T-SQL odeslaný do databáze pomocí `aspnet_regsql.exe` programu příkazového řádku, přečtěte si [Tento záznam blogu](http://scottonwriting.net/sowblog/posts/10709.aspx).

Pokud například chcete přidat infrastrukturu pro dotazování do databáze Microsoft SQL Server s názvem `pubs` na databázovém serveru s názvem `ScottsServer` pomocí ověřování systému Windows, přejděte do příslušného adresáře a z příkazového řádku zadejte:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

Po přidání infrastruktury na úrovni databáze musíme přidat triggery do tabulek, které se použijí v závislostech mezipaměti SQL. Použijte `aspnet_regsql.exe` znovu program příkazového řádku, ale zadejte název tabulky pomocí `-t` přepínače a místo použití `-ed` přepínače `-et` , například:

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

Chcete-li přidat triggery `authors` do `titles` tabulek a v `pubs` databázi na `ScottsServer` , použijte:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

V tomto kurzu přidejte triggery do `Products` tabulek, `Categories` a `Suppliers` . V kroku 3 se podíváme na konkrétní syntaxi příkazového řádku.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>Krok 2: odkazování na databázi edice Microsoft SQL Server 2005 Express v`App_Data`

`aspnet_regsql.exe`Program příkazového řádku vyžaduje název databáze a serveru, aby bylo možné přidat nezbytnou infrastrukturu cyklického dotazování. Ale jaký je název databáze a serveru pro databázi Microsoft SQL Server 2005 Express, která se nachází ve `App_Data` složce? Místo toho, abyste zjistili, jak jsou názvy databází a serverů, jsem zjistili, že nejjednodušší přístup je připojit databázi k `localhost\SQLExpress` instanci databáze a přejmenovat data pomocí [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Pokud máte na svém počítači nainstalovanou plnou verzi SQL Server 2005, je možné, že už máte v počítači nainstalovanou SQL Server Management Studio. Pokud máte jenom edici Express, můžete si stáhnout bezplatnou [edici Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Začněte zavřením sady Visual Studio. Pak otevřete SQL Server Management Studio a vyberte připojení k `localhost\SQLExpress` serveru pomocí ověřování systému Windows.

![Připojit k serveru localhost\SQLExpress](using-sql-cache-dependencies-cs/_static/image1.gif)

**Obrázek 1**: připojení k `localhost\SQLExpress` serveru

Po připojení k serveru Management Studio zobrazí server a bude mít podsložky pro databáze, zabezpečení a tak dále. Klikněte pravým tlačítkem na složku databáze a vyberte možnost připojit. Tím zobrazíte dialogové okno připojit databáze (viz obrázek 2). Klikněte na tlačítko Přidat a vyberte `NORTHWND.MDF` složku databáze ve složce webových aplikací s `App_Data` .

[![Připojte NORTHWND. Databáze MDF ze složky App_Data](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**Obrázek 2**: připojení `NORTHWND.MDF` databáze ze `App_Data` složky ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image2.png))

Tím se databáze přidá do složky databáze. Název databáze může být úplná cesta k databázovému souboru nebo úplná cesta s [identifikátorem GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier). Chcete-li se vyhnout nutnosti zadávat při použití \_ nástroje příkazového řádku aspnetregsql.exe, přejmenujte databázi na výstižnější název tak, že kliknete pravým tlačítkem na databázi, která je právě připojená a zvolíte možnost Přejmenovat. Přejmenoval (a) jsem databázi na datakurzy.

![Přejmenování připojené databáze na výstižnější název](using-sql-cache-dependencies-cs/_static/image3.gif)

**Obrázek 3**: přejmenování připojené databáze na výstižnější název

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>Krok 3: Přidání infrastruktury cyklického dotazování do databáze Northwind

Teď, když jsme připojili `NORTHWND.MDF` databázi ze `App_Data` složky, budeme připraveni přidat infrastrukturu cyklického dotazování. Za předpokladu, že jste přejmenovali databázi na datatutorial, spusťte následující čtyři příkazy:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

Po spuštění těchto čtyř příkazů klikněte pravým tlačítkem myši na název databáze v Management Studio, přejděte do podnabídky úkoly a vyberte možnost Odpojit. Pak zavřete Management Studio a znovu otevřete Visual Studio.

Po opětovném otevření sady Visual Studio přejděte k databázi prostřednictvím Průzkumník serveru. Poznamenejte si novou tabulku ( `AspNet_SqlCacheTablesForChangeNotification` ), nové uložené procedury a triggery v `Products` `Categories` tabulkách, a `Suppliers` .

![Databáze teď obsahuje nezbytnou infrastrukturu dotazování.](using-sql-cache-dependencies-cs/_static/image4.gif)

**Obrázek 4**: databáze teď obsahuje nezbytnou infrastrukturu dotazování.

## <a name="step-4-configuring-the-polling-service"></a>Krok 4: Konfigurace služby cyklického dotazování

Po vytvoření potřebných tabulek, triggerů a uložených procedur v databázi je posledním krokem konfigurace služby cyklického dotazování, která se provádí pomocí `Web.config` Určení databází, které se mají použít, a frekvence dotazování v milisekundách. Následující kód se dotazuje databáze Northwind každou sekundu.

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

`name`Hodnota v `<add>` elementu (NorthwindDB) spojuje uživatelsky čitelný název s konkrétní databází. Při práci se závislostmi mezipaměti SQL budeme muset odkazovat na zde definovaný název databáze a také na tabulku, na které jsou data uložená v mezipaměti založena. Podíváme se, jak pomocí `SqlCacheDependency` třídy programově přidružit závislosti mezipaměti SQL k datům uložených v mezipaměti v kroku 6.

Po navázání závislosti mezipaměti SQL se systém cyklického dotazování připojí k databázím definovaným v `<databases>` prvcích každých `pollTime` milisekund a spustí `AspNet_SqlCachePollingStoredProcedure` uloženou proceduru. Tato uložená procedura, která se přidala zpátky v kroku 3 pomocí `aspnet_regsql.exe` nástroje příkazového řádku – vrátí `tableName` `changeId` hodnoty a pro každý záznam v `AspNet_SqlCacheTablesForChangeNotification` . Zastaralé závislosti mezipaměti SQL jsou vyřazeny z mezipaměti.

Toto `pollTime` Nastavení přináší kompromisy mezi výkonem a zastaralosti dat. Malá `pollTime` hodnota zvyšuje počet požadavků na databázi, ale rychleji vyloučí zastaralá data z mezipaměti. Větší `pollTime` hodnota snižuje počet požadavků databáze, ale zvyšuje zpoždění mezi tím, kdy se data back-endu mění a jsou vyřazeny související položky mezipaměti. Naštěstí požadavek databáze zpracovává jednoduchou uloženou proceduru, která vrací pouze několik řádků z jednoduché, zjednodušené tabulky. Ale Experimentujte s různými `pollTime` hodnotami a Najděte ideální rovnováhu mezi přístupem k databázi a neaktuálností dat pro vaši aplikaci. Nejmenší `pollTime` povolená hodnota je 500.

> [!NOTE]
> Výše uvedený příklad poskytuje jednu `pollTime` hodnotu v `<sqlCacheDependency>` prvku, ale lze volitelně zadat `pollTime` hodnotu v `<add>` elementu. To je užitečné v případě, že máte zadáno více databází a chcete přizpůsobit četnost dotazování na databázi.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>Krok 5: deklarativní práce se závislostmi mezipaměti SQL

V krocích 1 až 4 jsme se podívali na to, jak nastavit potřebnou databázovou infrastrukturu a nakonfigurovat systém cyklického dotazování. Tato infrastruktura teď umožňuje přidávat do mezipaměti dat položky s přidruženou závislostí mezipaměti SQL pomocí programových nebo deklarativních technik. V tomto kroku se podíváme, jak deklarativně pracovat se závislostmi mezipaměti SQL. V kroku 6 se podíváme na programový přístup.

[Data ukládání do mezipaměti s](caching-data-with-the-objectdatasource-cs.md) kurzem ObjectDataSource prozkoumaly deklarativní možnosti ukládání do mezipaměti prvku ObjectDataSource. Pouhým nastavením `EnableCaching` vlastnosti na `true` a `CacheDuration` vlastnost na určitý časový interval bude prvek ObjectDataSource automaticky ukládat data vrácená z podkladového objektu na zadaný interval. Prvek ObjectDataSource může také používat jednu nebo více závislostí mezipaměti SQL.

Chcete-li demonstrovat použití závislostí mezipaměti SQL deklarativně, otevřete `SqlCacheDependencies.aspx` stránku ve `Caching` složce a přetáhněte prvek GridView z panelu nástrojů do návrháře. Nastavte prvek GridView s `ID` na `ProductsDeclarative` a, z jeho inteligentní značky, vyberte možnost svázání s novým prvkem ObjectDataSource s názvem `ProductsDataSourceDeclarative` .

[![Vytvořit nový prvek ObjectDataSource s názvem ProductsDataSourceDeclarative](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**Obrázek 5**: vytvoření nového prvku ObjectDataSource s názvem `ProductsDataSourceDeclarative` ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image4.png))

Nakonfigurujte prvek ObjectDataSource tak, aby používal `ProductsBLL` třídu a nastavte rozevírací seznam na kartě vybrat na `GetProducts()` . Na kartě aktualizace vyberte `UpdateProduct` přetížení se třemi vstupními parametry – `productName` , `unitPrice` a `productID` . Na kartách vložit a odstranit nastavte rozevírací seznamy na (žádné).

[![Použití přetížení UpdateProduct se třemi vstupními parametry](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**Obrázek 6**: použití přetížení UpdateProduct se třemi vstupními parametry ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image6.png)).

[![Pro karty INSERT a DELETE nastavte rozevírací seznam na (žádný).](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**Obrázek 7**: Nastavení rozevíracího seznamu na (žádné) pro karty Vložit a odstranit ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image8.png))

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio v prvku GridView pro každé z datových polí BoundFields a CheckBoxFields. Odeberte všechna pole, ale, `ProductName` `CategoryName` a `UnitPrice` naformátujte tato pole podle potřeby. Z inteligentní značky GridView s zaškrtněte políčka Povolit stránkování, Povolit řazení a povolit úpravy. Sada Visual Studio nastaví vlastnost ObjectDataSource s `OldValuesParameterFormatString` na `original_{0}` . Aby funkce Edit prvku GridView s fungovala správně, buď odeberte tuto vlastnost zcela z deklarativní syntaxe nebo ji nastavte zpět na výchozí hodnotu `{0}` .

Nakonec přidejte webový ovládací prvek Popisek nad prvek GridView a nastavte jeho `ID` vlastnost na `ODSEvents` `EnableViewState` hodnotu `false` . Po provedení těchto změn by deklarativní označení stránky mělo vypadat podobně jako následující. Všimněte si, že jsem vytvořil řadu možností přizpůsobení pro pole GridView, která nejsou nutná k předvedení funkce závislosti mezipaměti SQL.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

Dále vytvořte obslužnou rutinu události pro událost ObjectDataSource s `Selecting` a přidejte následující kód:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

Odvolání události ObjectDataSource s `Selecting` aktivované pouze při načítání dat z jeho podkladového objektu. Pokud prvek ObjectDataSource přistupuje k datům z vlastní mezipaměti, tato událost není aktivována.

Nyní navštivte tuto stránku v prohlížeči. Vzhledem k tomu, že jsme zatím naimplementovali jakékoli ukládání do mezipaměti, pokaždé, když na stránce, seřadíte nebo upravíte mřížku, by se stránka měla zobrazit text, vybrala se událost vyvolaná na obrázku 8.

[![Událost výběru ObjectDataSource s se aktivuje při každém stránkování, úpravě nebo řazení prvku GridView.](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**Obrázek 8**: událost ObjectDataSource s je `Selecting` aktivována při každém stránkování, úpravě nebo řazení prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti).](using-sql-cache-dependencies-cs/_static/image10.png)

Jak jsme viděli v [datech ukládání do mezipaměti s](caching-data-with-the-objectdatasource-cs.md) kurzem ObjectDataSource, nastavení `EnableCaching` vlastnosti pro `true` způsobí, že prvek ObjectDataSource uloží data do mezipaměti po dobu určenou `CacheDuration` vlastností. Prvek ObjectDataSource má také [ `SqlCacheDependency` vlastnost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx), která přidá jednu nebo více závislostí mezipaměti SQL k datům uloženým v mezipaměti pomocí vzoru:

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

Kde *DatabaseName* je název databáze, jak je uvedeno v `name` atributu `<add>` elementu v `Web.config` a *TableName* je název tabulky databáze. Například pro vytvoření prvku ObjectDataSource, který ukládá data do mezipaměti neomezeně na základě závislosti mezipaměti SQL proti tabulce Northwind s `Products` , nastavte vlastnost ObjectDataSource s `EnableCaching` na `true` a její `SqlCacheDependency` vlastnost na NorthwindDB: Products.

> [!NOTE]
> Můžete použít závislost mezipaměti SQL *a* vypršení platnosti na základě času nastavením `EnableCaching` na `true` `CacheDuration` časový interval a `SqlCacheDependency` na název databáze a tabulky (y). Prvek ObjectDataSource vyřadí svá data v případě vypršení platnosti založené na čase nebo v případě, že systém dotazování obsahuje poznámku, že se změnila podkladová data databáze, podle toho, co se stane jako první.

Prvek GridView v `SqlCacheDependencies.aspx` zobrazuje data ze dvou tabulek – `Products` a `Categories` (produkt s `CategoryName` je načten prostřednictvím `JOIN` `Categories` ). Proto chceme zadat dvě závislosti mezipaměti SQL: NorthwindDB: Products; NorthwindDB: Categories.

[![Konfigurace prvku ObjectDataSource pro podporu ukládání do mezipaměti s využitím závislostí mezipaměti SQL pro produkty a kategorie](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**Obrázek 9**: Konfigurace prvku ObjectDataSource tak, aby podporoval ukládání do mezipaměti pomocí závislostí mezipaměti SQL `Products` a `Categories` ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image12.png))

Po nakonfigurování prvku ObjectDataSource tak, aby podporoval ukládání do mezipaměti, je nutné znovu navštívit stránku v prohlížeči. Znovu, text ' výběr vyvolání události by se měl zobrazit na první stránce, ale měl by přijít o stránkování, řazení nebo kliknutí na tlačítka pro úpravy nebo zrušení. Důvodem je, že po načtení dat do mezipaměti ObjectDataSource s, zůstane tam, dokud nedojde ke `Products` `Categories` změně tabulek nebo nebo dokud nebudou data aktualizována prostřednictvím prvku GridView.

Po stránkování přes mřížku a zaznamenání chybějícího textu, který vyvolal událost, otevřete nové okno prohlížeče a přejděte k základnímu kurzu v části úpravy, vložení a odstranění ( `~/EditInsertDelete/Basics.aspx` ). Aktualizujte název nebo cenu produktu. Poté z okna do prvního okna prohlížeče zobrazte jinou stránku dat, seřaďte mřížku nebo klikněte na tlačítko Upravit řádek. Tentokrát by se měla znovu zobrazit možnost vybrat událost, která se má znovu zobrazit, protože se změnila podkladová data databáze (viz obrázek 10). Pokud se text nezobrazí, chvíli počkejte a zkuste to znovu. Mějte na paměti, že služba cyklického dotazování kontroluje změny v `Products` tabulce každých `pollTime` milisekund, takže dojde ke zpoždění mezi tím, kdy se podkladová data aktualizují a když jsou data uložená v mezipaměti vyřazení.

[![Úprava tabulky Products vyřadí data produktu uložená v mezipaměti.](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**Obrázek 10**: Změna tabulky Products vyřadí data produktu uložená v mezipaměti ([kliknutím zobrazíte obrázek v plné velikosti).](using-sql-cache-dependencies-cs/_static/image14.png)

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>Krok 6: práce s třídou prostřednictvím kódu programu `SqlCacheDependency`

[Data o ukládání do mezipaměti v kurzu architektury](caching-data-in-the-architecture-cs.md) vyhledaly výhody použití samostatné vrstvy ukládání do mezipaměti v architektuře, a to na rozdíl od těsného propojení mezipaměti s prvkem ObjectDataSource. V tomto kurzu jsme vytvořili `ProductsCL` třídu, která ukazuje, jak programově pracovat s datovou mezipamětí. Chcete-li využít závislosti mezipaměti SQL ve vrstvě ukládání do mezipaměti, použijte `SqlCacheDependency` třídu.

V systému cyklického dotazování `SqlCacheDependency` musí být objekt přidružen ke konkrétní dvojici databáze a tabulky. Následující kód například vytvoří `SqlCacheDependency` objekt založený na tabulce Northwind Database s `Products` :

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

Dva vstupní parametry `SqlCacheDependency` konstruktoru s jsou názvy databáze a tabulky, v uvedeném pořadí. Podobně jako u vlastnosti ObjectDataSource s `SqlCacheDependency` je použitý název databáze stejný jako hodnota zadaná v `name` atributu `<add>` elementu v `Web.config` . Název tabulky je skutečný název tabulky databáze.

Chcete-li přidružit k `SqlCacheDependency` položce, která je přidána do mezipaměti dat, použijte jedno z `Insert` přetížení metod, které přijímá závislost. Následující kód přidá *hodnotu* do mezipaměti dat pro neomezenou dobu trvání, ale přidruží ji k `SqlCacheDependency` `Products` tabulce. V krátkém případě *hodnota* zůstane v mezipaměti, dokud není vyřazena z důvodu omezení paměti nebo protože systém cyklického dotazování zjistil, že se `Products` tabulka od okamžiku, kdy byla uložena do mezipaměti, nezměnila.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

Třída pro ukládání do mezipaměti v mezipaměti v tuto `ProductsCL` chvíli ukládá data z `Products` tabulky pomocí vypršení platnosti po 60 sekundách. Tuto třídu nechte aktualizovat tak, aby místo toho používala závislosti mezipaměti SQL. `ProductsCL` `AddCacheItem` Metoda třídy, která je zodpovědná za přidání dat do mezipaměti, v současné době obsahuje následující kód:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

Aktualizujte tento kód, aby `SqlCacheDependency` místo `MasterCacheKeyArray` závislosti mezipaměti používal objekt:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

Chcete-li otestovat tuto funkci, přidejte prvek GridView na stránku pod existující `ProductsDeclarative` prvek GridView. Nastavte tento nový prvek GridView `ID` pro na `ProductsProgrammatic` a, prostřednictvím inteligentní značky, navažte jej na nový prvek ObjectDataSource s názvem `ProductsDataSourceProgrammatic` . Nakonfigurujte prvek ObjectDataSource, aby používal `ProductsCL` třídu, a nastavení rozevíracích seznamů na kartách vybrat a aktualizovat na `GetProducts` a v `UpdateProduct` uvedeném pořadí.

[![Konfigurace prvku ObjectDataSource pro použití třídy ProductsCL](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**Obrázek 11**: Konfigurace prvku ObjectDataSource pro použití `ProductsCL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](using-sql-cache-dependencies-cs/_static/image16.png))

[![V rozevíracím seznamu vybrat kartu vyberte metodu GetProducts.](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**Obrázek 12**: vyberte `GetProducts` metodu z rozevíracího seznamu vybrat kartu ([kliknutím zobrazíte obrázek v plné velikosti).](using-sql-cache-dependencies-cs/_static/image18.png)

[![Z rozevíracího seznamu karta aktualizace vyberte metodu UpdateProduct.](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**Obrázek 13**: v rozevíracím seznamu karta aktualizace vyberte metodu UpdateProduct ([kliknutím zobrazíte obrázek v plné velikosti).](using-sql-cache-dependencies-cs/_static/image20.png)

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio v prvku GridView pro každé z datových polí BoundFields a CheckBoxFields. Podobně jako u prvního prvku GridView, který je přidán na tuto stránku, odeberte všechna pole, ale, `ProductName` `CategoryName` a `UnitPrice` naformátujte tato pole podle potřeby. Z inteligentní značky GridView s zaškrtněte políčka Povolit stránkování, Povolit řazení a povolit úpravy. Stejně jako u prvku `ProductsDataSourceDeclarative` ObjectDataSource, sada Visual Studio nastaví `ProductsDataSourceProgrammatic` vlastnost ObjectDataSource s `OldValuesParameterFormatString` na `original_{0}` . Aby funkce Edit prvku GridView s fungovala správně, nastavte tuto vlastnost zpět na `{0}` (nebo odeberte přiřazení vlastností z deklarativní syntaxe úplně).

Po dokončení těchto úloh by výsledné deklarativní označení prvku GridView a ObjectDataSource mělo vypadat takto:

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

Chcete-li otestovat závislost mezipaměti SQL ve vrstvě ukládání do mezipaměti, nastavte zarážku v `ProductCL` metodě třídy s `AddCacheItem` a pak spusťte ladění. Při první návštěvě `SqlCacheDependencies.aspx` by se měla zarážka narazit, protože data se požadují poprvé a umístí do mezipaměti. Dále přejděte na jinou stránku v prvku GridView nebo seřaďte jeden ze sloupců. Výsledkem je, že GridView spustí dotaz na data, ale data by se měla v mezipaměti najít, protože `Products` Databázová tabulka nebyla upravena. Pokud se data v mezipaměti opakovaně nenacházejí, ujistěte se, že je v počítači k dispozici dostatek paměti, a zkuste to znovu.

Po stránkování přes několik stránek prvku GridView otevřete druhé okno prohlížeče a přejděte k základnímu kurzu v části úpravy, vložení a odstranění ( `~/EditInsertDelete/Basics.aspx` ). Aktualizujte záznam z tabulky Products a potom v prvním okně prohlížeče zobrazte novou stránku nebo klikněte na některou z hlaviček řazení.

V tomto scénáři se zobrazí jedna z následujících dvou věcí: buď se zarážka objeví, což značí, že data uložená v mezipaměti byla vyřazena z důvodu změny v databázi. nebo, zarážka se neobjeví, což znamená, že `SqlCacheDependencies.aspx` se teď zobrazují zastaralá data. Pokud zarážka není dosaženo, je pravděpodobně způsobena tím, že služba cyklického dotazování ještě nebyla od změny dat aktivována. Mějte na paměti, že služba cyklického dotazování kontroluje změny v `Products` tabulce každých `pollTime` milisekund, takže dojde ke zpoždění mezi tím, kdy se podkladová data aktualizují a když jsou data uložená v mezipaměti vyřazení.

> [!NOTE]
> Tato prodleva se pravděpodobněji objevuje při úpravě jednoho z produktů prostřednictvím prvku GridView v `SqlCacheDependencies.aspx` . V [datech ukládání do mezipaměti v kurzu architektury](caching-data-in-the-architecture-cs.md) jsme přidali `MasterCacheKeyArray` závislost mezipaměti, aby bylo zajištěno, že data, která jsou upravována `ProductsCL` metodou třídy s, `UpdateProduct` byla z mezipaměti vyřazena. Tuto závislost mezipaměti jsme však nahradili při změně `AddCacheItem` metody dříve v tomto kroku, a proto `ProductsCL` bude třída dál zobrazovat data uložená v mezipaměti, dokud systém cyklického dotazování nepoznámku na změnu v `Products` tabulce. Ukážeme, jak `MasterCacheKeyArray` v kroku 7 znovu zavést závislost mezipaměti.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>Krok 7: přidružení více závislostí k položce v mezipaměti

Zajistěte, aby se `MasterCacheKeyArray` závislost mezipaměti zajistila, že se *všechna* data související s produktem vyloučí z mezipaměti, když se aktualizuje nějaká jedna položka, která je v ní spojená. Metoda například ukládá do `GetProductsByCategoryID(categoryID)` mezipaměti `ProductsDataTables` instance pro každou jedinečnou hodnotu *KódKategorie* . Pokud je jeden z těchto objektů vyřazený, `MasterCacheKeyArray` závislost mezipaměti zajistí, že ostatní budou také odebrány. Bez této závislosti mezipaměti platí, že při změně dat uložených v mezipaměti existuje možnost, že jiná data produktu v mezipaměti mohou být zastaralá. V důsledku toho je důležité, abyste zachovali `MasterCacheKeyArray` závislost mezipaměti při použití závislostí mezipaměti SQL. Metoda cache s daty ale `Insert` povoluje jenom jeden objekt závislosti.

Navíc při práci se závislostmi mezipaměti SQL může být nutné přidružit více tabulek databáze jako závislosti. Například `ProductsDataTable` mezipaměť ve `ProductsCL` třídě obsahuje názvy kategorií a dodavatelů pro každý produkt, ale `AddCacheItem` Metoda používá pouze závislost na `Products` . Pokud uživatel v této situaci aktualizuje název kategorie nebo dodavatele, data produktu uložená v mezipaměti zůstanou v mezipaměti a budou zastaralá. Proto chceme, aby data produktu uložená v mezipaměti byla závislá nejen na `Products` tabulce, ale také i v `Categories` tabulkách a `Suppliers` .

[ `AggregateCacheDependency` Třída](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) poskytuje způsob pro přidružení více závislostí k položce mezipaměti. Začněte vytvořením `AggregateCacheDependency` instance. Dále přidejte sadu závislostí pomocí `AggregateCacheDependency` `Add` metody s. Při vkládání položky do mezipaměti dat potom předejte `AggregateCacheDependency` instanci. Dojde *any* -li ke `AggregateCacheDependency` změně jakékoli závislosti instance, bude položka v mezipaměti vyřazena.

Následující příklad ukazuje aktualizovaný kód pro `ProductsCL` metodu třídy s `AddCacheItem` . Metoda vytvoří `MasterCacheKeyArray` závislost mezipaměti spolu s `SqlCacheDependency` objekty pro `Products` tabulky, a `Categories` `Suppliers` . Všechny jsou sloučeny do jednoho `AggregateCacheDependency` objektu s názvem `aggregateDependencies` , který je poté předán do `Insert` metody.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

Otestujte tento nový kód. Nyní změny v `Products` tabulkách, `Categories` nebo `Suppliers` způsobují vyřazení dat uložených v mezipaměti. Kromě toho `ProductsCL` `UpdateProduct` Metoda třídy, která je volána při úpravách produktu prostřednictvím prvku GridView, vyřadí `MasterCacheKeyArray` závislost mezipaměti, která způsobí `ProductsDataTable` vyřazení mezipaměti a data, která budou znovu načtena při další žádosti.

> [!NOTE]
> Závislosti mezipaměti SQL lze také použít s [ukládání výstupu do mezipaměti](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx). Ukázku této funkce naleznete v tématu: [použití ukládání výstupu ASP.NET do mezipaměti s SQL Server](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx).

## <a name="summary"></a>Souhrn

Při ukládání dat do mezipaměti budou data v mezipaměti v ideálním případě uložena v mezipaměti, dokud je neupravíte v databázi. V případě ASP.NET 2,0 lze vytvořit závislosti mezipaměti SQL a použít je v deklarativních i programových scénářích. Jedním z problémů s tímto přístupem je zjišťování, kdy byla data změněna. Úplné verze Microsoft SQL Server 2005 poskytují možnosti oznámení, které mohou aplikaci upozornit, když se změní výsledek dotazu. Pro Express edici SQL Server 2005 a starších verzí SQL Server se místo toho musí použít systém cyklického dotazování. Naštěstí nastavení nezbytné infrastruktury cyklického dotazování je poměrně jasné.

Šťastné programování!

## <a name="further-reading"></a>Další materiály

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Používání oznámení dotazů v Microsoft SQL Server 2005](https://msdn.microsoft.com/library/ms175110.aspx)
- [Vytvoření oznámení dotazu](https://msdn.microsoft.com/library/ms188669.aspx)
- [Ukládání do mezipaměti v ASP.NET s `SqlCacheDependency` třídou](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [Nástroj pro registraci SQL Server ASP.NET ( `aspnet_regsql.exe` )](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [Přehled `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na adrese [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Marko Range, Teresa Murphy a Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, umístěte mi čáru na [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](caching-data-at-application-startup-cs.md) 
>  [Další](caching-data-with-the-objectdatasource-vb.md)
