---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Vytvoření modelu s ověřením obchodních pravidel | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 3 ukazuje, jak vytvořit model, který můžeme použít k dotazu a aktualizaci databáze pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541634"
---
# <a name="build-a-model-with-business-rule-validations"></a>Vytvoření modelu s ověřením obchodních pravidel

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 3 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 3 ukazuje, jak vytvořit model, který můžeme použít k dotazu a aktualizaci databáze pro naši aplikaci NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner Krok 3: Stavební model

V rámci model-view-controller termín "model" odkazuje na objekty, které představují data aplikace, stejně jako odpovídající logiku domény, která integruje ověření a obchodní pravidla s ním. Model je v mnoha ohledech "srdce" aplikace založené na MVC, a jak uvidíme později zásadně řídí chování to.

Rozhraní ASP.NET MVC podporuje použití jakékoli technologie přístupu k datům a vývojáři si mohou vybrat z různých bohatých možností dat .NET implementovat své modely, včetně: LINQ entity, LINQ na SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM nebo jen raw ADO.NET DataReaders nebo DataSets.

Pro naši aplikaci NerdDinner budeme používat LINQ na SQL vytvořit jednoduchý model, který odpovídá poměrně úzce naše databáze design a přidává některé vlastní ověřování logiky a obchodní pravidla. Poté implementujeme třídu úložiště, která pomáhá abstrahovat implementaci trvalosti dat od zbytku aplikace a umožňuje nám snadno ji testovat.

### <a name="linq-to-sql"></a>Technologie LINQ to SQL

LINQ to SQL je ORM (objekt relační mapovač), který je dodáván jako součást .NET 3.5.

LINQ to SQL poskytuje snadný způsob mapování databázových tabulek na třídy .NET, proti které můžeme kódovat. Pro naši aplikaci NerdDinner ji použijeme k mapování tabulek Dinners a RSVP v rámci naší databáze na třídy Dinner a RSVP. Sloupce tabulky Večeře a RSVP bude odpovídat vlastnosti na večeři a RSVP třídy. Každý Dinner a RSVP objekt bude představovat samostatný řádek v rámci večeří nebo RSVP tabulky v databázi.

LINQ to SQL nám umožňuje vyhnout se nutnosti ručně vytvářet příkazy SQL k načtení a aktualizaci objektů Dinner a RSVP s daty databáze. Místo toho budeme definovat večeři a RSVP třídy, jak se mapovat do/z databáze a vztahy mezi nimi. LINQ na SQL se pak postará o generování příslušné logiky spuštění SQL pro použití za běhu při interakci a jejich použití.

Můžeme použít podporu jazyka LINQ v rámci VB a C# k zápisu expresivní dotazy, které načítají Dinner a RSVP objekty z databáze. Tím se minimalizuje množství datového kódu, který potřebujeme napsat, a umožňuje nám vytvářet opravdu čisté aplikace.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Přidání LINQ do tříd SQL do našeho projektu

Začneme kliknutím pravým tlačítkem myši na složku "Modely" v rámci našeho projektu a vybereme příkaz Nabídky **Přidat&gt;novou položku:**

![](build-a-model-with-business-rule-validations/_static/image1.png)

Tím se zobrazí dialogové okno Přidat novou položku. Budeme filtrovat podle kategorie "Data" a vyberte šablonu "LINQ to SQL Classes" v ní:

![](build-a-model-with-business-rule-validations/_static/image2.png)

Pojmenujeme položku "NerdDinner" a klikneme na tlačítko "Přidat". Visual Studio přidá soubor NerdDinner.dbml pod naším adresářem \Models a potom otevře návrhář relační objektu LINQ na SQL:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Vytváření tříd datového modelu pomocí LINQ na SQL

LINQ to SQL nám umožňuje rychle vytvářet třídy datového modelu z existujícího schématu databáze. Pokud to chcete provést, otevřeme databázi NerdDinner v Průzkumníkovi serveru a vybereme tabulky, které v ní chceme modelovat:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Potom můžeme přetáhnout tabulky na povrch ulinq návrháře SQL. Když to uděláme LINQ to SQL automaticky vytvoří večeři a RSVP třídy pomocí schématu tabulek (s vlastnostmi třídy, které mapují na sloupce tabulky databáze):

![](build-a-model-with-business-rule-validations/_static/image5.png)

Ve výchozím nastavení linq na SQL návrháře automaticky "pluralizes" názvy tabulek a sloupců při vytváření tříd na základě schématu databáze. Například: tabulka "Večeře" v našem příkladu výše vyústila ve třídě "Dinner". Tato třída pojmenování pomáhá, aby naše modely konzistentní s .NET konvence pojmenování a obvykle zjistíte, že s návrhářem opravit to pohodlné (zejména při přidávání velké množství tabulek). Pokud se vám nelíbí název třídy nebo vlastnosti, které návrhář generuje, můžete jej vždy přepsat a změnit na libovolný název, který chcete. Můžete to provést buď úpravou názvu entity nebo vlastnosti v rámci návrháře nebo úpravou prostřednictvím mřížky vlastností.

Ve výchozím nastavení linq na SQL návrháře také kontroluje primární klíč nebo cizí klíč vztahy tabulek a na základě nich automaticky vytvoří výchozí "přidružení vztahů" mezi různými třídami modelu, které vytvoří. Například když jsme přetáhli tabulky Dinners a RSVP do návrháře LINQ na SQL, přidružení vztahů 1:N mezi nimi bylo odvozeno na základě skutečnosti, že tabulka RSVP měla cizí klíč k tabulce Večeře (to je označeno šipkou v návrháři):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Výše uvedené přidružení způsobí LINQ sql přidat silně zadaný "Dinner" vlastnost třídy RSVP, které vývojáři mohou použít pro přístup k večeři spojené s daným RSVP. To také způsobí, že Dinner třídy mít "RSVPs" vlastnost kolekce, která umožňuje vývojářům načíst a aktualizovat RSVP objekty spojené s konkrétní Dinner.

Níže můžete vidět příklad intellisense v rámci sady Visual Studio, když vytvoříme nový objekt RSVP a přidáme ho do kolekce rsvps večeři. Všimněte si, jak LINQ sql automaticky přidána kolekce "RSVPs" na Dinner objektu:

![](build-a-model-with-business-rule-validations/_static/image7.png)

Přidáním rsvp objektu večeři rsvps kolekce říkáme LINQ sql přidružit vztah cizího klíče mezi večeři a rsvp řádek v naší databázi:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Pokud se vám nelíbí, jak návrhář modeloval nebo pojmenoval přidružení tabulky, můžete ho přepsat. Stačí kliknout na asociační šipku v rámci návrháře a získat přístup k jeho vlastnostem prostřednictvím mřížky vlastností, abyste ji přejmenovali, odstranili nebo upravili. Pro naši aplikaci NerdDinner však výchozí pravidla přidružení fungují dobře pro třídy datového modelu, které vytváříme, a můžeme použít výchozí chování.

### <a name="nerddinnerdatacontext-class"></a>Třída NerdDinnerDataContext

Visual Studio automaticky vytvoří třídy .NET, které představují modely a relace databáze definované pomocí návrháře LINQ na SQL. Třída LINQ to SQL DataContext je také generována pro každý soubor návrháře LINQ do SQL přidané do řešení. Protože jsme pojmenovali naši položku třídy LINQ na SQL "NerdDinner", vytvořená třída DataContext se bude nazývat "NerdDinnerDataContext". Tato třída NerdDinnerDataContext je primární způsob, jak budeme pracovat s databází.

Naše Třída NerdDinnerDataContext zveřejňuje dvě vlastnosti - "Večeře" a "RSVPs" - které představují dvě tabulky, které jsme modelovali v rámci databáze. Můžeme použít C# k zápisu linq dotazy proti tyto vlastnosti dotaz a načíst Večeři a RSVP objekty z databáze.

Následující kód ukazuje, jak vytvořit konkretizovat Objekt NerdDinnerDataContext a provést dotaz LINQ proti němu získat posloupnost Dinners, ke kterým dojde v budoucnu. Visual Studio poskytuje plnou intellisense při psaní dotazu LINQ a objekty vrácené z něj jsou silně typované a také podporují intellisense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Kromě toho, že nám umožňuje dotaz na dinner a RSVP objekty, NerdDinnerDataContext také automaticky sleduje všechny změny, které následně provedeme na večeři a RSVP objekty načteme přes něj. Tuto funkci můžeme použít ke snadnému uložení změn zpět do databáze - aniž bychom museli psát jakýkoli explicitní kód aktualizace SQL.

Například níže uvedený kód ukazuje, jak pomocí dotazu LINQ načíst jeden objekt Dinner z databáze, aktualizovat dvě vlastnosti Dinner a potom uložit změny zpět do databáze:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Objekt NerdDinnerDataContext ve výše uvedeném kódu automaticky sledoval změny vlastností provedené v objektu Dinner, který jsme z něj načetli. Když jsme volali "SubmitChanges()" metoda, provede příslušný příkaz SQL "UPDATE" do databáze zachovat aktualizované hodnoty zpět.

### <a name="creating-a-dinnerrepository-class"></a>Vytvoření třídy DinnerRepository

Pro malé aplikace je někdy v pořádku mít řadiče pracovat přímo proti LINQ na SQL DataContext třídy a vložit LINQ dotazy v rámci řadiče. Jako aplikace získat větší, i když tento přístup se stává těžkopádné udržovat a testovat. To může také vést k nám duplikovat stejné linq dotazy na více místech.

Jeden přístup, který může usnadnit údržbu a testování aplikací, je použití vzoru "úložiště". Třída úložiště pomáhá zapouzdřit logiku dotazování a trvalosti dat a abstrahovat podrobnosti implementace trvalosti dat z aplikace. Kromě čištění kódu aplikace může použití vzoru úložiště usnadnit změnu implementace úložiště dat v budoucnu a může pomoci usnadnit testování částí aplikace bez nutnosti skutečné databáze.

Pro naši aplikaci NerdDinner definujeme třídu DinnerRepository s níže uvedeným podpisem:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Poznámka: Dále v této kapitole budeme extrahovat rozhraní IDinnerRepository z této třídy a povolit vkládání závislostí s ním na našich řadičů. Za prvé, i když začneme jednoduché a jen pracovat přímo s DinnerRepository třídy.*

Chcete-li implementovat tuto třídu, klikneme pravým tlačítkem myši na složku "Modely" a zvolíme příkaz nabídky **Přidat&gt;novou položku.** V dialogovém okně "Přidat novou položku" vybereme šablonu "Třída" a pojmenujeme soubor "DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

Můžeme pak implementovat naše DinnerRepository třídy pomocí kódu níže:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Načítání, aktualizace, vkládání a odstranění pomocí třídy DinnerRepository

Teď, když jsme vytvořili naši třídu DinnerRepository, podívejme se na několik příkladů kódu, které ukazují běžné úkoly, které s ním můžeme dělat:

#### <a name="querying-examples"></a>Dotazování příklady

Níže uvedený kód načte jednu večeři pomocí DinnerID hodnotu:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Níže uvedený kód načte všechny nadcházející večeře a smyčky nad nimi:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Příklady vložení a aktualizace

Níže uvedený kód ukazuje přidání dvou nových večeří. Dodatky/úpravy úložiště nejsou potvrzeny do databáze, dokud "Save()" metoda je volána na něj. LINQ to SQL automaticky zalomí všechny změny v databázové transakci – takže buď dojde ke všem změnám, nebo k žádné z nich nedojde, když naše úložiště uloží:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Níže uvedený kód načte existující Dinner objektu a upraví dvě vlastnosti na něm. Změny jsou potvrzeny zpět do databáze při "Save()" metoda je volána na našem úložišti:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Níže uvedený kód načte večeři a přidá k němu odpověď. Je to pomocí rsvps kolekce na Dinner objektu, který LINQ na SQL vytvořil pro nás (protože je vztah primárního klíče/cizího klíče mezi těmito dvěma v databázi). Tato změna je zachována zpět do databáze jako nový řádek tabulky RSVP při volání metody "Save()" v úložišti:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Odstranit příklad

Níže uvedený kód načte existující Dinner objektu a označí jej odstranit. Když "Save()" metoda je volána v úložišti bude potvrdit delete zpět do databáze:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Integrace logiky ověřování a obchodních pravidel s třídami modelu

Integrace logiky ověřování a obchodních pravidel je klíčovou součástí každé aplikace, která pracuje s daty.

#### <a name="schema-validation"></a>Ověření schématu

Když jsou definovány třídy modelu pomocí návrháře LINQ na SQL, datové typy vlastností ve třídách datového modelu odpovídají datovým typům databázové tabulky. Například: Pokud je sloupec "EventDate" v tabulce Dinners "datetime", třída datového modelu vytvořená linq na SQL bude typu "DateTime" (což je vestavěný datový typ .NET). To znamená, že se zobrazí chyby kompilace, pokud se pokusíte přiřadit celé číslo nebo logickou hodnotu k němu z kódu a automaticky vyvolá chybu, pokud se pokusíte implicitně převést neplatný typ řetězce na něj za běhu.

LINQ na SQL bude také automaticky zpracovává úniku hodnoty SQL pro vás při použití řetězců - což pomáhá chránit před útoky injektáže SQL při jeho použití.

#### <a name="validation-and-business-rule-logic"></a>Logika ověření a obchodních pravidel

Ověření schématu je užitečné jako první krok, ale je zřídka dostačující. Většina scénářů reálného světa vyžaduje možnost zadat bohatší ověřovací logiku, která může span více vlastností, spustit kód a často mít povědomí o stavu modelu (například: je to vytváří /aktualizován/odstraněn, nebo v rámci stavu specificképro doménu, jako je "archivován"). Existuje celá řada různých vzorů a rámců, které lze použít k definování a použití ověřovacích pravidel pro třídy modelu a existuje několik rozhraní založených na rozhraní .NET, které lze použít k tomu, aby vám pomohly. Můžete použít skoro některý z nich v rámci ASP.NET aplikací MVC.

Pro účely naší aplikace NerdDinner použijeme relativně jednoduchý a přímočarý vzor, kde zveřejňujeme isvalid vlastnost a GetRuleViolations() metoda na naše Dinner model objektu. IsValid Vlastnost vrátí true nebo false v závislosti na tom, zda jsou platná ověřovací a obchodní pravidla. Metoda GetRuleViolations() vrátí seznam všech chyb pravidel.

Budeme implementovat IsValid a GetRuleViolations() pro náš model Večeři přidáním "částečné třídy" do našeho projektu. Částečné třídy lze přidat metody/vlastnosti/události do tříd udržovaných návrhářem VS (jako dinner třídy generované LINQ do SQL designer) a pomoci vyhnout se nástroj probírat s naším kódem. Do našeho projektu můžeme přidat novou částečnou třídu kliknutím pravým tlačítkem myši na složku \Models a poté vybrat příkaz nabídky "Přidat novou položku". Poté můžeme zvolit šablonu "Třída" v dialogovém okně "Přidat novou položku" a pojmenovat ji Dinner.cs.

![](build-a-model-with-business-rule-validations/_static/image11.png)

Kliknutím na tlačítko "Přidat" přidáte do našeho projektu soubor Dinner.cs a otevřete jej v rámci ide. Potom můžeme implementovat základní rámec pro vynucení pravidla/ověření pomocí níže uvedeného kódu:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Několik poznámek k výše uvedenému kódu:

- Dinner Třída je předchází "částečné" klíčové slovo – což znamená, že kód obsažený v něm bude kombinovat s třídou generované nebo spravované LINQ do SQL návrháře a kompilovány do jedné třídy.
- Třída RuleViolation je pomocná třída, kterou přidáme do projektu, který nám umožňuje poskytnout další podrobnosti o porušení pravidel.
- Dinner.GetRuleViolations() metoda způsobí, že naše ověření a obchodní pravidla, která mají být vyhodnocena (budeme implementovat v nejbližší době). Potom vrátí zpět posloupnost RuleViolation objekty, které poskytují další podrobnosti o všechny chyby pravidla.
- Vlastnost Dinner.IsValid poskytuje pohodlné pomocné vlastnost, která označuje, zda Dinner objekt má všechny aktivní RuleViolations. Může být proaktivně kontrolována vývojářpomocí Dinner objektu kdykoliv (a nevyvolá výjimku).
- Dinner.OnValidate() částečná metoda je zavěšení, které poskytuje LINQ na SQL, který nám umožňuje být upozorněni kdykoli Dinner objekt uchovává v databázi. Naše OnValidate() implementace výše zajišťuje, že večeři nemá žádné RuleViolations před uložením. Pokud je v neplatném stavu vyvolá výjimku, která způsobí LINQ sql přerušit transakci.

Tento přístup poskytuje jednoduchý rámec, do kterého můžeme integrovat ověřovací a obchodní pravidla. Pro tuto chvíli přidáme níže uvedená pravidla do naší metody GetRuleViolations() :

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Používáme funkci "yield return" jazyka C# k vrácení posloupnosti všech porušení pravidel. Prvních šest kontrol pravidel výše jednoduše vynutit, že vlastnosti řetězce na naší večeři nemůže být null nebo prázdné. Poslední pravidlo je trochu zajímavější, a volá PhoneValidator.IsValidNumber() pomocná metoda, kterou můžeme přidat do našeho projektu ověřit, že formát čísla ContactPhone odpovídá večeři země.

Můžeme použít . NET podporuje regulární výraz pro implementaci podpory tohoto telefonického ověření. Níže je jednoduchá implementace PhoneValidator, kterou můžeme přidat do našeho projektu, který nám umožňuje přidat kontroly vzoru Regex specifické pro zemi:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Zpracování ověření a porušení obchodní logiky

Teď, když jsme přidali výše uvedený kód ověření a obchodnípravidla, kdykoli se pokusíme vytvořit nebo aktualizovat večeři, naše pravidla logiky ověření budou vyhodnocena a vynucena.

Vývojáři mohou psát kód jako níže proaktivně určit, pokud Dinner objekt je platný a načíst seznam všech porušení v něm bez vyvolání jakékoli výjimky:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Pokud se pokusíme uložit Dinner v neplatném stavu, bude vyvolána výjimka při volání Save() metoda na DinnerRepository. K tomu dochází, protože LINQ sql automaticky volá naše Dinner.OnValidate() částečná metoda před uložením Dinner změny a jsme přidali kód Dinner.OnValidate() vyvolat výjimku, pokud existují porušení pravidel v Dinner. Můžeme zachytit tuto výjimku a reaktivně načíst seznam porušení opravit:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Vzhledem k tomu, že naše ověřovací a obchodní pravidla jsou implementována v rámci vrstvy modelu a ne v rámci vrstvy ui, budou použity a použity ve všech scénářích v rámci naší aplikace. Můžeme později změnit nebo přidat obchodní pravidla a mít veškerý kód, který pracuje s našimi objekty Večeři ctít je.

S flexibilitou změnit obchodní pravidla na jednom místě, aniž by tyto změny zvlnění v celé aplikaci a logiky rozhraní, je známkou dobře napsané aplikace a výhoda, která rozhraní MVC pomáhá podporovat.

### <a name="next-step"></a>Další krok

Nyní máme model, který můžeme použít k dotazování a aktualizaci naší databáze.

Nyní přidáme do projektu některé řadiče a zobrazení, které můžeme použít k vytvoření prostředí uživatelského prostředí HTML kolem něj.

> [!div class="step-by-step"]
> [Předchozí](create-a-database.md)
> [další](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
