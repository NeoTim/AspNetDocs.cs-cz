---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Ovládací prvky zdrojů dat | Dokumenty společnosti Microsoft
author: rick-anderson
description: Ovládací prvek DataGrid v ASP.NET 1.x znamenal velké zlepšení v přístupu k datům ve webových aplikacích. Nebylo to však tak uživatelsky přívětivé, jak by to mohlo být....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540217"
---
# <a name="data-source-controls"></a>Ovládací prvky zdroje dat

podle [společnosti Microsoft](https://github.com/microsoft)

> Ovládací prvek DataGrid v ASP.NET 1.x znamenal velké zlepšení v přístupu k datům ve webových aplikacích. Nicméně, to nebylo tak uživatelsky přívětivé, jak by to mohlo být. Stále vyžaduje značné množství kódu získat mnoho užitečných funkcí z něj. Takový je model ve všech snahách o přístup k datům v 1.x.

Ovládací prvek DataGrid v ASP.NET 1.x znamenal velké zlepšení v přístupu k datům ve webových aplikacích. Nicméně, to nebylo tak uživatelsky přívětivé, jak by to mohlo být. Stále vyžaduje značné množství kódu získat mnoho užitečných funkcí z něj. Takový je model ve všech snahách o přístup k datům v 1.x.

ASP.NET 2.0 řeší to v části s ovládacími prvky zdroje dat. Ovládací prvky zdroje dat v ASP.NET 2.0 poskytují vývojářům deklarativní model pro načítání dat, zobrazení dat a úpravy dat. Účelem ovládacích prvků zdroje dat je poskytnout konzistentní reprezentaci dat ovládacích prvkůvázaných pro data bez ohledu na zdroj těchto dat. Jádrem ovládacích prvků zdroje dat v ASP.NET 2.0 je třída abstract DataSourceControl. Třída DataSourceControl poskytuje základní implementaci rozhraní IDataSource a rozhraní IListSource, které umožňuje přiřadit ovládací prvek zdroje dat jako data ovládacího prvku vázaného na data (prostřednictvím nové vlastnosti DataSourceId popsané později) a vystavit data v něm jako seznam. Každý seznam dat z ovládacího prvku zdroje dat je vystaven jako objekt DataSourceView. Přístup k instancím DataSourceView poskytuje rozhraní IDataSource. Například GetViewNames metoda vrátí ICollection, který umožňuje výčet DataSourceViews přidružené k určitému ovládacímu prvku zdroje dat a GetView metoda umožňuje přístup k konkrétní Instance DataSourceView podle názvu.

Ovládací prvky zdroje dat nemají žádné uživatelské rozhraní. Jsou implementovány jako serverové ovládací prvky tak, aby mohly podporovat deklarativní syntaxi a tak, aby měly přístup ke stavu stránky v případě potřeby. Ovládací prvky zdroje dat nevykreslují žádné značky HTML klientovi.

> [!NOTE]
> Jak uvidíte později, existují také výhody ukládání do mezipaměti získané pomocí ovládacích prvků zdroje dat.

## <a name="storing-connection-strings"></a>Ukládání připojovacích řetězců

Než se podíváme na to, jak konfigurovat ovládací prvky zdroje dat, měli bychom pokrýt nové funkce v ASP.NET 2.0 týkající se připojovacích řetězců. ASP.NET 2.0 zavádí nový oddíl v konfiguračním souboru, který umožňuje snadno ukládat připojovací řetězce, které lze číst dynamicky za běhu. ConnectionStrings &lt;&gt; sekce usnadňuje ukládání připojovacích řetězců.

Níže uvedený úryvek přidá nový připojovací řetězec.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> Stejně jako &lt;v&gt; části &lt;appSettings&gt; se oddíl connectionStrings zobrazí mimo oddíl &lt;system.web&gt; v konfiguračním souboru.

Chcete-li použít tento připojovací řetězec, můžete při nastavování atributu ConnectionString serverového ovládacího prvku použít následující syntaxi.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

ConnectionStrings &lt;&gt; části lze také zašifrovat tak, aby citlivé informace nejsou vystaveny. Tato schopnost bude pokryta pozdějším modulem.

## <a name="caching-data-sources"></a>Ukládání zdrojů dat do mezipaměti

Každý DataSourceControl poskytuje čtyři vlastnosti pro konfiguraci ukládání do mezipaměti; EnableCaching, CacheDuration, CacheExpirationPolicy a CacheKeyDependency.

## <a name="enablecaching"></a>Enablecaching

EnableCaching je logická vlastnost, která určuje, zda je pro ovládací prvek zdroje dat povolena ukládání do mezipaměti.

## <a name="cacheduration-property"></a>Vlastnost CacheDuration

Vlastnost CacheDuration nastaví počet sekund, po které zůstane mezipaměť platná. Nastavení této vlastnosti na **hodnotu 0** způsobí, že mezipaměť zůstane platná, dokud nebude explicitně zrušena.

## <a name="cacheexpirationpolicy-property"></a>Vlastnost CacheExpirationPolicy

Vlastnost CacheExpirationPolicy lze nastavit na **hodnotu Absolutní** nebo **Posuvné**. Nastavení na Hodnotu Absolutní znamená, že maximální doba, po kterou budou data uložena do mezipaměti, je počet sekund určený vlastností CacheDuration. Nastavením na Sliding, doba vypršení platnosti se resetuje při provádění každé operace.

## <a name="cachekeydependency-property"></a>Vlastnost CacheKeyDependency

Pokud je pro vlastnost CacheKeyDependency zadána hodnota řetězce, ASP.NET na staví novou závislost mezipaměti na základě tohoto řetězce. To umožňuje explicitně zneplatnit mezipaměť jednoduše změnou nebo odebráním CacheKeyDependency.

**Důležité:** Pokud je povoleno zosobnění a přístup ke zdroji dat nebo obsahu dat je založen na identitě klienta, doporučujeme zakázat ukládání do mezipaměti nastavením EnableCaching na False. Pokud ukládání do mezipaměti je povolena v tomto scénáři a uživatel jiný než uživatel, který původně požádal o data vydá požadavek, autorizace ke zdroji dat není vynucena. Data budou jednoduše obsluhována z mezipaměti.

## <a name="the-sqldatasource-control"></a>Ovládací prvek SqlDataSource

Ovládací prvek SqlDataSource umožňuje vývojáři přístup k datům uloženým v libovolné relační databázi, která podporuje ADO.NET. Může použít poskytovatele System.Data.SqlClient pro přístup k databázi serveru SQL Server, zprostředkovateli System.Data.OleDb, poskytovateli System.Data.Odbc nebo poskytovateli System.Data.OracleClient pro přístup k oracle. Proto SqlDataSource se jistě používá pouze pro přístup k datům v databázi serveru SQL Server.

Chcete-li použít SqlDataSource, jednoduše zadat hodnotu pro ConnectionString vlastnost a zadat příkaz SQL nebo uloženou proceduru. Ovládací prvek SqlDataSource se postará o práci s základní ADO.NET architekturou. Otevře připojení, dotazuje zdroj dat nebo provede uloženou proceduru, vrátí data a pak zavře připojení za vás.

> [!NOTE]
> Vzhledem k tomu, že třída DataSourceControl automaticky zavře připojení za vás, měla by snížit počet volání zákazníků generovaných nevracením připojení databáze.

Fragment kódu níže váže ovládací prvek DropDownList na ovládací prvek SqlDataSource pomocí připojovacího řetězce, který je uložen v konfiguračním souboru, jak je znázorněno výše.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Jak je znázorněno výše, vlastnost DataSourceMode zdroje SqlDataSource určuje režim pro zdroj dat. Ve výše uvedeném příkladu je Mode DataSourceMode nastaven na DataReader. V takovém případě SqlDataSource vrátí objekt IDataReader pomocí kurzor u dálný a jen pro čtení. Zadaný typ objektu, který je vrácen, je řízen poskytovatelem, který se používá. V tomto případě používám zprostředkovatele System.Data.SqlClient, &lt;jak je&gt; uvedeno v části connectionStrings souboru web.config. Proto objekt, který je vrácen a bude typu SqlDataReader. Zadáním dataSourceMode hodnotu DataSet data mohou být uloženy v DataSet na serveru. Tento režim umožňuje přidávat funkce, jako je třídění, stránkování atd. Kdybych byl data-vazba SqlDataSource na GridView ovládacíprvek, tak bych si zvolili režim DataSet. V případě DropDownList však režim DataReader je správná volba.

> [!NOTE]
> Při ukládání do mezipaměti SqlDataSource nebo AccessDataSource, DataSourceMode vlastnost musí být nastavena na DataSet. Výjimka nastane, pokud povolíte ukládání do mezipaměti s DataSourceMode DataReader.

## <a name="sqldatasource-properties"></a>Vlastnosti zdroje SqlDataSource

Následují některé vlastnosti ovládacího prvku SqlDataSource.

### <a name="cancelselectonnullparameter"></a>Parametr CancelSelectOnNullParametr

Logická hodnota, která určuje, zda je příkaz select zrušen, pokud je jeden z parametrů null. True ve výchozím nastavení.

### <a name="conflictdetection"></a>Conflictdetection

V situaci, kdy více uživatelů může aktualizovat zdroj dat současně, vlastnost ConflictDetection určuje chování ovládacího prvku SqlDataSource. Tato vlastnost vyhodnotí jednu z hodnot ConflictOptions výčtu. Tyto hodnoty jsou **CompareAllValues** a **OverwriteChanges**. Pokud je nastavena na PřepsatZměny, poslední osoba, která má zapisovat data do zdroje dat, přepíše všechny předchozí změny. Však pokud ConflictDetection vlastnost je nastavena na CompareAllValues, parametry získat vytvořeny pro sloupce vrácené SelectCommand a parametry jsou také vytvořeny pro uložení původní hodnoty v každém z těchto sloupců umožňuje SqlDataSource určit, zda hodnoty se změnily od SelectCommand byl proveden.

### <a name="deletecommand"></a>Deletecommand

Nastaví nebo získá řetězec SQL použitý při odstranění řádků z databáze. Může se jedná o dotaz SQL nebo název uložené procedury.

### <a name="deletecommandtype"></a>DeleteCommandType

Nastaví nebo získá typ příkazu delete, dotaz SQL (Text) nebo uloženou proceduru (StoredProcedure).

### <a name="deleteparameters"></a>Deleteparameters

Vrátí parametry, které používá DeleteCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

### <a name="oldvaluesparameterformatstring"></a>Oldvaluesparameterformatstring

Tato vlastnost se používá k určení formátu původní parametry hodnoty v případech, kdy ConflictDetection vlastnost je nastavena na CompareAllValues. Výchozí hodnota {0} je, což znamená, že parametry původní hodnoty budou mít stejný název jako původní parametr. Jinými slovy, pokud je název pole EmployeeID, @EmployeeIDpůvodní parametr hodnoty by byl .

### <a name="selectcommand"></a>Selectcommand

Nastaví nebo získá řetězec SQL, který se používá k načtení dat z databáze. Může se jedná o dotaz SQL nebo název uložené procedury.

### <a name="selectcommandtype"></a>SelectCommandType

Nastaví nebo získá typ příkazu select, buď dotaz SQL (Text) nebo uloženou proceduru (StoredProcedure).

### <a name="selectparameters"></a>Selectparameters

Vrátí parametry, které používá SelectCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

### <a name="sortparametername"></a>Sortparametername

Získá nebo nastaví název parametru uložené procedury, který se používá při řazení dat načtených ovládacím prvkem zdroje dat. Platnost platí pouze v případě, že selectcommandtype je nastavena na StoredProcedure.

### <a name="sqlcachedependency"></a>Sqlcachedependency

Řetězec oddělený středníkem určující databáze a tabulky používané v závislosti mezipaměti serveru SQL Server. (Závislosti mezipaměti SQL budou popsány v pozdějším modulu.)

### <a name="updatecommand"></a>Updatecommand

Nastaví nebo získá řetězec SQL, který se používá při aktualizaci dat v databázi. Může se jedná o dotaz SQL nebo název uložené procedury.

### <a name="updatecommandtype"></a>UpdateCommandType

Nastaví nebo získá typ příkazu aktualizace, dotaz SQL (Text) nebo uloženou proceduru (StoredProcedure).

### <a name="updateparameters"></a>Updateparameters

Vrátí parametry, které používá příkaz UpdateCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

## <a name="the-accessdatasource-control"></a>Ovládací prvek AccessDataSource

Ovládací prvek AccessDataSource je odvozen od třídy SqlDataSource a používá se k vazbě dat na databázi aplikace Microsoft Access. Vlastnost ConnectionString pro ovládací prvek AccessDataSource je vlastnost jen pro čtení. Místo použití vlastnosti ConnectionString se vlastnost DataFile používá k zobrazení bodu na databázi aplikace Access, jak je znázorněno níže.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource vždy nastaví Název providerzákladního Zdroje SqlDataSource na System.Data.OleDb a připojí se k databázi pomocí zprostředkovatele Microsoft.Jet.OLEDB.4.0 OLE DB. Ovládací prvek AccessDataSource nelze použít k připojení k databázi aplikace Access chráněné heslem. Pokud máte připojení k databázi chráněné heslem, měli byste použít ovládací prvek SqlDataSource.

> [!NOTE]
> Databáze aplikace Access uložené na webu by\_měly být umístěny v adresáři Data aplikace. ASP.NET neumožňuje procházení souborů v tomto adresáři. Při používání databází aplikace Access budete muset udělit přístupovému účtu pro čtení a zápis do adresáře Dat aplikace.\_

## <a name="the-xmldatasource-control"></a>Ovládací prvek XmlDataSource

Zdroj XmlDataSource se používá k vazby dat XML s ovládacími prvky vázanými na data. Můžete vytvořit vazbu na soubor XML pomocí vlastnosti DataFile nebo můžete svázat s řetězcem XML pomocí vlastnosti Data. XmlDataSource zveřejňuje atributy XML jako vypoovací pole. V případech, kdy je třeba vytvořit vazbu na hodnoty, které nejsou reprezentovány jako atributy, budete muset použít transformaci XSL. Výrazy XPath můžete také použít k filtrování dat XML.

Zvažte následující soubor XML:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

Všimněte si, že XmlDataSource používá Vlastnost XPath osoby nebo &lt;&gt; *osoby,* aby se filtrovat pouze na osoby uzly. DropDownList pak data váže na LastName atribut pomocí DataTextField vlastnost.

Zatímco ovládací prvek XmlDataSource se používá především k vazbě dat na data XML jen pro čtení, je možné upravit datový soubor XML. Všimněte si, že v takových případech automatické vkládání, aktualizace a odstranění informací v souboru XML se neprovádí automaticky, jak to dělá s jinými ovládacími prvky zdroje dat. Místo toho budete muset napsat kód pro ruční úpravu dat pomocí následujících metod ovládacího prvku XmlDataSource.

### <a name="getxmldocument"></a>GetXmlDocument

Načte objekt XmlDocument obsahující kód XML načtený zdrojem XmlDataSource.

### <a name="save"></a>Uložit

Uloží dokument XmlDocument v paměti zpět do zdroje dat.

Je důležité si uvědomit, že Save metoda bude fungovat pouze v případě, že jsou splněny následující dvě podmínky:

1. XmlDataSource používá vlastnost DataFile k vazbě na soubor XML namísto vlastnosti Data, aby se svázal s daty XML v paměti.
2. Žádná transformace je zadána prostřednictvím Transform nebo TransformFile vlastnost.

Všimněte si také, že Save metoda může přinést neočekávané výsledky při volání více uživatelů současně.

## <a name="the-objectdatasource-control"></a>Ovládací prvek ObjectDataSource

Ovládací prvky zdroje dat, které jsme do tohoto okamžiku zakryli, jsou vynikající volbou pro dvouvrstvé aplikace, kde ovládací prvek zdroje dat komunikuje přímo do úložiště dat. Mnoho aplikací v reálném světě jsou však vícevrstvé aplikace, kde může být nutné komunikovat s obchodní objekt, který zase komunikuje s datovou vrstvou. V těchto situacích ObjectDataSource vyplní účet pěkně. Objekt ObjectDataSource funguje ve spojení se zdrojovým objektem. Ovládací prvek ObjectDataSource vytvoří instanci zdrojového objektu, zavolá zadanou metodu a nabude instance objektu v rámci oboru jednoho požadavku, pokud má objekt metody instance namísto statických metod (Sdíleno v jazyce Visual Basic). Proto musí být objekt bezstavové. To znamená, že objekt by měl získat a uvolnit všechny požadované prostředky v rámci rozsahu jednoho požadavku. Způsob vytvoření zdrojového objektu můžete řídit zpracováním události ObjectCreating ovládacího prvku ObjectDataSource. Můžete vytvořit instanci zdrojového objektu a potom nastavit vlastnost ObjectInstance třídy ObjectDataSourceEventArgs na tuto instanci. Ovládací prvek ObjectDataSource použije instanci, která je vytvořena v události ObjectCreating, namísto vytvoření instance samostatně.

Pokud zdrojový objekt pro ovládací prvek ObjectDataSource zveřejňuje veřejné statické metody (Shared in Visual Basic), které lze volat k načtení a úpravám dat, ovládací prvek ObjectDataSource bude tyto metody volat přímo. Pokud ovládací prvek ObjectDataSource musí vytvořit instanci zdrojového objektu, aby bylo možné volat metodu, musí objekt obsahovat veřejný konstruktor, který nepřijímá žádné parametry. Ovládací prvek ObjectDataSource zavolá tento konstruktor, když vytvoří novou instanci zdrojového objektu.

Pokud zdrojový objekt neobsahuje veřejný konstruktor bez parametrů, můžete vytvořit instanci zdrojového objektu, který bude použit ovládacím prvkem ObjectDataSource v události ObjectCreating.

## <a name="specifying-object-methods"></a>Určení metod objektů

Zdrojový objekt pro ovládací prvek ObjectDataSource může obsahovat libovolný počet metod, které se používají k výběru, vložení, aktualizaci nebo odstranění dat. Tyto metody jsou volány ovládacím prvkem ObjectDataSource na základě názvu metody, jak je identifikováno pomocí vlastností SelectMethod, InsertMethod, UpdateMethod nebo DeleteMethod ovládacího prvku ObjectDataSource. Zdrojový objekt může také obsahovat volitelnou metodu SelectCount, která je identifikována ovládacím prvkem ObjectDataSource pomocí vlastnosti SelectCountMethod, která vrací počet celkového počtu objektů ve zdroji dat. Ovládací prvek ObjectDataSource zavolá metodu SelectCount poté, co byla volána metoda Select, aby načetla celkový počet záznamů ve zdroji dat pro použití při stránkování.

## <a name="lab-using-data-source-controls"></a>Testovací prostředí pomocí ovládacích prvků zdroje dat

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Cvičení 1 – zobrazení dat pomocí ovládacího prvku SqlDataSource

Následující cvičení používá ovládací prvek SqlDataSource pro připojení k databázi Northwind. Předpokládá, že máte přístup k databázi Northwind na instanci serveru SQL Server 2000.

1. Vytvořte nový ASP.NET web.
2. Přidejte nový soubor web.config.

    1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a klikněte na Přidat novou položku.
    2. Ze seznamu šablon zvolte Webový konfigurační soubor a klikněte na Přidat.
3. Upravte &lt;oddíl&gt; connectionStrings takto: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Přepněte do zobrazení kód a přidejte atribut ConnectionString a atribut SelectCommand do ovládacího &lt;prvku asp:SqlDataSource&gt; následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. V návrhovém zobrazení přidejte nový ovládací prvek GridView.
6. V rozevíracím seznamu Zvolit zdroj dat v nabídce Úlohy GridView zvolte SqlDataSource1.
7. Klikněte pravým tlačítkem na Default.aspx a z nabídky zvolte Zobrazit v prohlížeči. Po zobrazení výzvy k uložení klepněte na tlačítko Ano.
8. GridView zobrazí data z tabulky Produkty.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Cvičení 2 – úpravy dat pomocí ovládacího prvku SqlDataSource

Následující cvičení ukazuje, jak data vázat ovládací prvek DropDownList pomocí deklarativní syntaxe a umožňuje upravit data prezentovaná v ovládacím prvku DropDownList.

1. V návrhovém zobrazení odstraňte ovládací prvek GridView z default.aspx. 

    **Důležité:** Ponechte ovládací prvek SqlDataSource na stránce.
2. Přidejte ovládací prvek DropDownList do souboru Default.aspx.
3. Přepněte do zobrazení zdroje.
4. Přidejte atribut DataSourceId, DataTextField a DataValueField do ovládacího &lt;prvku asp:DropDownList&gt; následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Uložit Default.aspx a zobrazit v prohlížeči. Všimněte si, že DropDownList obsahuje všechny produkty z databáze Northwind.
6. Zavřete prohlížeč.
7. Ve zdrojovém zobrazení default.aspx přidejte nový ovládací prvek TextBox pod ovládací prvek DropDownList. Změňte vlastnost ID textového pole na txtProductName.
8. Pod ovládacím prvkem TextBox přidejte nový ovládací prvek Button. Změňte vlastnost ID tlačítka na btnUpdate a vlastnost Text na **Aktualizovat název produktu**.
9. Ve zdrojovém zobrazení default.aspx přidejte vlastnost UpdateCommand a dva nové parametry UpdateParameters do značky SqlDataSource následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Všimněte si, že jsou přidány dva parametry aktualizace (ProductName a ProductID) v tomto kódu. Tyto parametry jsou mapovány na vlastnost Text textového pole txtProductName a vlastnost SelectedValue dropdownlistu ddlProducts.
10. Přepněte do návrhového zobrazení a poklepáním na ovládací prvek Button přidejte obslužnou rutinu události.
11. Do kódu btnUpdate\_Click přidejte následující kód: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Klikněte pravým tlačítkem myši na soubor Default.aspx a zvolte jeho zobrazení v prohlížeči. Po zobrazení výzvy k uložení všech změn klepněte na tlačítko Ano.
13. ASP.NET 2.0 částečné třídy umožňují kompilaci za běhu. Není nutné vytvářet aplikaci, aby se změny kódu projevily.
14. Vyberte produkt z dropdownlistu.
15. Do textového pole zadejte nový název vybraného produktu a klepněte na tlačítko Aktualizovat.
16. Název produktu je aktualizován v databázi.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Cvičení 3 pomocí ovládacího prvku ObjectDataSource

Toto cvičení ukáže, jak používat ovládací prvek ObjectDataSource a zdrojový objekt pro interakci s databází Northwind.

1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a klikněte na Přidat novou položku.
2. V seznamu šablon vyberte Webový formulář. Změňte název na object.aspx a klikněte na Přidat.
3. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a klikněte na Přidat novou položku.
4. V seznamu šablon vyberte Třída. Změňte název třídy, aby NorthwindData.cs a klikněte na Přidat.
5. Po zobrazení výzvy k přidání třídy do složky Kód aplikace\_klikněte na Ano.
6. Do souboru NorthwindData.cs přidejte následující kód: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Přidejte následující kód do zdrojového zobrazení object.aspx: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Uložte všechny soubory a procházejte objekt object.aspx.
9. Pracujte s rozhraním zobrazením podrobností, úpravami zaměstnanců, přidáním zaměstnanců a odstraněním zaměstnanců.
