---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET přístup k datům – doporučené zdroje | Dokumenty společnosti Microsoft
author: rick-anderson
description: Toto téma obsahuje odkazy na materiály dokumentace o tom, jak získat přístup k datům v ASP.NET webových aplikací, především pomocí entity framework a SQL Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676165"
---
# <a name="aspnet-data-access---recommended-resources"></a>Přístup k datům ASP.NET – doporučené zdroje informací

> Toto téma obsahuje odkazy na materiály dokumentace o tom, jak získat přístup k datům v ASP.NET webových aplikací, především pomocí entity framework a SQL Server.
> 
> Pokud víte, skvělý blog post, [stackoverflow](http://stackoverflow.com) vlákno, nebo jakýkoli jiný odkaz, který by byl užitečný, [pošlete nám e-mail](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) s odkazem.
> 
> Naposledy aktualizováno 4/3/2014

Téma obsahuje následující části:

- [Začínáme s přístupem k datům v ASP.NET](#gettingstarted)
- [Použití entity frameworku](#ef)

    - [Nejprve použít kód entity frameworku](#cf)
    - [Použití migrace prvního kódu entity](#efcfmigrations)
    - [Použití databáze entity framework první nebo model první (EF Designer)](#efdbf)
    - [Načítání souvisejících dat v rámci entity (opožděné načítání, eager loading a explicitní načítání)](#efrelateddata)
    - [Optimalizace výkonnosti rámce entity](#optimizingef)
    - [Zpracování souběžnosti v aplikaci entity frameworku](#efconcurrency)
    - [Knihy o entity rámce](#efbooks)
    - [Další prostředky entity frameworku](#otherefresources)
- [Datová vazba v aplikacích ASP.NET webových formulářů](#wfdatabinding)

    - [Použití vazby modelu webových formulářů](#wfmodelbinding)
    - [Použití ovládacích prvků zdroje dat webových formulářů](#wfdsc)
    - [Použití ovládacích prvků vázaných na data webových formulářů a výrazů datových vazeb](#wfdbc)
- [Práce s databázemi serveru SQL Server](#sqlserver)

    - [Práce s místními databázemi SQL Server Express](#sslocaldb)
    - [Práce s databázemi SQL Server Express](#sse)
    - [Práce s databází Sql Windows Azure](#ssdb)
    - [Výběr mezi SQL Serverem a databází Windows Azure SQL Database](#ssdbchoosing)
- [Práce se systémy pro správu databází NoSQL](#nosql)
- [Použití dotazů LINQ v ASP.NET aplikacích](#linq)
- [Použití dynamického datového lešení](#dd)
- [Zabezpečení přístupu k datům](#securing)
- [Optimalizace výkonu přístupu k datům](#optimizingdataaccess)
- [Nasazení databáze](#deploying)
- [Přístup k datům prostřednictvím webové služby](#webservice)
- [Další zdroje informací](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Začínáme s přístupem k datům v ASP.NET

- [Možnosti úložiště dat (vytváření reálných cloudových aplikací s Windows Azure).](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) Kapitola e-knihy o vývoji pro cloud. Zavádí NoSQL databáze jako alternativu, že mnoho vývojářů obeznámených s relační databáze mají tendenci přehlížet. Představuje pokyny, o čem přemýšlet při výběru relační nebo NoSQL, nebo výběru konkrétní platformy.
- [ASP.NET možnosti přístupu k datům](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Úvod k možnostem přístupu k datům pro relační databáze pro ASP.NET a pokyny, jak zvolit platformy a metody přístupu, které jsou vhodné pro váš scénář.
- [Relační databáze](http://en.wikipedia.org/wiki/Relational_database). Wikipedie). Pokud jste nepracovali s relačními databázemi, podívejte se na tuto stránku, kde najdete úvod do terminologie a konceptů relačních databází. Pro úvod do SQL Server zejména naleznete [práce s databázemi SQL Server](#sqlserver) dále v tomto tématu.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Použití entity frameworku

- [přístupy k rozvoji rámce entit](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Pokyny, jak zvolit přístup k vývoji entity framework databáze první, model první nebo kód první.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Nejprve použít kód entity frameworku

Následující kurzy nabízejí ukázkové aplikace ke stažení:

- [Začínáme s EF 6 pomocí MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Zahrnuje širokou škálu scénářů entity framework code first, včetně migrace a funkce EF 6, jako je odolnost proti připojení, zachycení příkazů a asynchronní. Toto je aktualizovaná verze [řady EF 5 / MVC 4](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Předchozí série obsahuje kurz o úložiště a jednotky práce vzory, které nejsou zahrnuty v nové řady.
- [Úvod do ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). Zahrnuje užší rozsah scénáře Entity Framework Code First, ale provádí komplexnější úlohu při zavádění funkcí MVC.
- [Vazba modelu a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Používá kód jako první v aplikaci webových formulářů.
- [Začínáme s ASP.NET 4.5 Web Forms](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Úvod do webových formulářů s určitým pokrytím code first. Používá vazbu modelu.
- [Hudební obchod MVC](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Používá Code First v aplikaci MVC 3 elektronického obchodování, která také implementuje členství a autorizaci. Zde používaný systém mvc verze a ASP.NET členství (ověřování a autorizace) jsou zastaralé; Další aktuální informace o členství v ASP.NET [https://asp.net/identity](https://asp.net/identity)naleznete v tématu .

Další zdroje:

- [Entity Framework - Kód nejprve existující databáze](https://msdn.microsoft.com/data/jj200620). Msdn. Video a návod, který ukazuje, jak používat kód jako první s existující databází.
- [Centrum pro vývojáře dat – entity framework](https://msdn.microsoft.com/data/ef). Msdn. Průvodce dokumentací entity framework, která byla vytvořena a udržována týmem entity frameworku, najdete v článku Začínáme odkaz [Začínáme.](https://msdn.microsoft.com/data/ee712907)

Viz také [knihy o entity framework](#efbooks) a další prostředky entity framework [dále](#otherefresources) v tomto tématu.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Použití migrace prvního kódu entity

Většina kurzů Code First uvedených výše pokrývá migrace. Viz také následující zdroje.

- [ASP.NET nasazení webu pomocí sady Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Dvoudílné série kurzů, které ukazují, jak pomocí migrace Code First k nasazení databáze.
- [Nasazení zabezpečené aplikace ASP.NET MVC 5 s členstvím, OAuth a databází SQL na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Microsoft Azure). Jak používat migrace k nasazení členství a dat aplikací do Azure.
- [Přehled nasazení webu pro sady Visual Studio a ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). Vysvětlení, jak je migrace code first integrovaná do funkcí webového nasazení sady Visual Studio, najdete v části **Konfigurace nasazení databáze v sadě Visual Studio.**
- [Centrum pro vývojáře dat – migrace prvního kódu](https://msdn.microsoft.com/data/jj591621) (MSDN). Dokumentace týmu entity framework migrace.
- [Migrace Screencast Series](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF). Tři videa na pokročilá témata v code first migrace.
- [První migrace kódu s ASP.NET webech webových stránek](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Mikesdotnetting blog). Ukazuje, jak používat migrace Code First s webem ASP.NET web vložením datového kontextu do projektu knihovny tříd sady Visual Studio.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Použití databáze entity framework první nebo model první (EF Designer)

- [Začínáme s entity Framework 6 databáze nejprve pomocí MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Spusťte skript v Průzkumníkovi serveru k vytvoření databáze a potom pomocí návrháře entity framework uvytvořit datový model. Ukazuje, jak vytvořit jednoduché webové stránky CRUD a pro další funkce zpracování dat můžete sledovat jeden z kurzů Code First, protože všechny pracovní postupy EF používají stejné rozhraní DBContext API.

Následující prostředky jsou starší. Jsou užitečné, pokud chcete použít verzi 4.0 entity frameworku a chcete použít ovládací prvek zdroje dat pro datové vazby v aplikaci webových formulářů.

- [Začínáme s rámcem entity 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Ukazuje, jak používat **entityDataSource** ovládací prvek.
- [Pokračování entity framework](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(Ukazuje, jak používat **Objekt ObjektDataSource** ovládacího prvku. Obsahuje kurz o zpracování souběžnosti, kurz na výkon EF a kurz na to, co je nového v EF 4.0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Zpracování souvisejících dat v rámci entity (opožděné načítání, eager loading a explicitní načítání)

- [Čtení souvisejících dat s entity frameworkem v ASP.NET mvc aplikaci](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Kód první, MVC ukázková aplikace. Zobrazené metody platí také pro vazbu modelu webových formulářů a pracovní postup Database First.
- [Centrum pro vývojáře dat – načítání souvisejících entit](https://msdn.microsoft.com/data/jj574232) (MSDN). Dokumentace týmu entity framework o načítání souvisejících dat.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Optimalizace výkonnosti entity frameworku

- [Scénáře rozšířeného rámce entit pro ASP.NET aplikaci](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Ukazuje, jak spustit vlastní příkazy SQL nebo volat vlastní uložené procedury, jak zakázat zjišťování změn a jak zakázat ověřování při ukládání změn.
- [Důležité informace o výkonu pro entity Framework 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Důležité informace o výkonu (entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Maximalizace výkonu pomocí entity frameworku ve ASP.NET webové aplikaci](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md). Platí pro entity Framework 4.0.
- Viz také [Optimalizace přístupu k ASP.NET datdále](#optimizingdataaccess) v tomto tématu.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Zpracování souběžnosti v aplikaci entity frameworku

- [Zpracování souběžnosti s entity framework u ASP.NET aplikace MVC](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, DbContext API, pomocí ukázkové aplikace MVC.
- [Centrum pro vývojáře dat – optimistické vzory souběžnosti](https://msdn.microsoft.com/data/jj592904) (MSDN). Dokumentace souběžnosti týmu entity framework.
- [Zpracování souběžnosti s entity framework u ASP.NET webové aplikace](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Platí pro entity Framework 4.0. Nejprve databáze, ObjectContext API, pomocí ukázkové aplikace webových formulářů.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Knihy o entity rámce

- [Rámec programovacíentity: DbContext](http://shop.oreilly.com/product/0636920022237.do) od Julie Lermana a Rowana Millera.
- [Rámec programovacíentity: Code First](http://shop.oreilly.com/product/0636920022220.do) od Julie Lermanové a Rowana Millera.

Obě tyto knihy jsou aktuální s aktuálními doporučenými technikami. Poskytují komplexnější, ale snadno sledovat úvod do entity rámce, než cokoli, co je k dispozici na internetu. Další kniha, [Programování Entity Framework](http://shop.oreilly.com/product/9780596807252.do) Julie Lerman, je větší a komplexnější, ale je starší a mnoho technik, které pokrývá již nejsou doporučený způsob, jak používat entity rámce. Viz také seznam knih doporučený týmem Entity Framework v [Centru pro vývojáře dat – knihy](https://msdn.microsoft.com/data/aa937716) na webu MSDN.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Jiné zdroje rámce entity

- [Entity Framework (ADO.NET) týmový blog](https://blogs.msdn.com/b/adonet/). Jeden z nejlepších zdrojů pro nejaktuálnější informace a oznámení o nových vylepšeních. Další blogy související s EF najdete v tématu Blogroll at [Get Started with Entity Framework](https://msdn.microsoft.com/data/ee712907).
- [Časopis MSDN](https://msdn.microsoft.com/magazine/default.aspx). Podívejte se na sloupec **Datové body,** který se často týká témat souvisejících s rozhraním entity.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Datová vazba v aplikacích ASP.NET webových formulářů

- [ASP.NET možnosti přístupu k datům webových formulářů](https://msdn.microsoft.com/library/jj822927.aspx) (MSDN).<a id="wfmodelbinding"></a>

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Použití vazby modelu webových formulářů

- [Vazba modelu a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Série kurzů pomocí kódu EF jako první.
- [Webových formulářů Model Vazba Část 1: Výběr dat](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie blog). V těchto starších příspěvcích blogu byla vlastnost, která je aktuálně pojmenována ItemType, pojmenována ModelType, ale jinak jsou informace, které obsahují, platné.
- [Web Forms Model Binding Part 2: Filtrování dat](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (blog Scotta Guthrieho).
- [Web Forms Model Binding Část 3: Aktualizace a ověření](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie blog).
- [ASP.NET 4.5 Vazba modelu webových formulářů](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (video).
- [Model binding part 1 - Výběr dat](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (video).
- [Model Binding Part 2 - Filtrování](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (video).
- [Začínáme s ASP.NET 4.5 webových formulářů - Zobrazení datových položek a podrobností](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Použití ovládacích prvků zdroje dat webových formulářů

- [Ovládací prvky webového serveru zdroje dat](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- [Oznámení vydání zprostředkovatele dynamických dat a entityDataSource ovládacího prvku pro entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (Microsoft Web Development blog).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Použití ovládacích prvků vázaných na data webových formulářů a výrazů datových vazeb

- [Vazba modelu a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Série kurzů, která používá ef kód jako první.
- [Začínáme s ASP.NET 4.5 webových formulářů - Zobrazení datových položek a podrobností](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Silně zadali ovládací prvky dat](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie blog).
- [Ovládací prvky dat silného typu](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [ASP.NET 4.5 Ovládací prvky silných zadaných dat (video) webových formulářů.](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)
- [Ovládací prvky webového serveru vázaného na data](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Přehled výrazů datové vazby](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Tato stránka se vztahuje pouze **eval** a **bind**; nebyla aktualizována tak, aby **zahrnovala položky** a **BindItem**.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Práce s databázemi serveru SQL Server

- [Funkce databáze serveru SQL Server](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Obecný úvod do široké škály témat serveru SQL Server naleznete položky pod tento jeden v toc.
- [SQL Server Editions](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Souhrn dostupných edicí serveru SQL Server s odkazy na další informace o jednotlivých verzích.)
- [Připojovací řetězce serveru SQL Server pro ASP.NET webových aplikací](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Použití sql server compact pro ASP.NET webových aplikací](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: Ukázky databázových produktů](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Ukázka adventureworks databází.
- [Instalace ukázkových databází](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Kromě zde uvedených metod můžete také stáhnout jeden z ukázkových souborů\_MDF do složky Data aplikace webového projektu, převést databázi na LocalDB a vytvořit připojovací řetězec LocalDB. Informace o tom, jak to provést, naleznete v [tématu How to: Upgrade na LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

Viz také následující části o práci s SQL Server Express a LocalDB a výběru mezi SQL Server a SQL Database.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Práce s místními databázemi SQL Server Express

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). Oficiální MSDN úvod do LocalDB.
- [Připojovací řetězce serveru SQL Server pro ASP.NET webových aplikací](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Postup: Upgrade na LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Jak migrovat soubor MDF ze starší verze sql server express u LocalDB. Tento proces musíte také projít, pokud si stáhnete jednu z [ukázkových databází serveru SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=117483).
- [Představujeme LocalDB, vylepšený SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express blog). Má více pozadí o tom, proč LocalDB byl vytvořen, než je součástí MSDN.
- [LocalDB: Kde je moje databáze?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express blog). Informace o tom, kde jsou vytvořeny soubory databáze LocalDB.
- [Použití LocalDB s úplnou službou IIS, část 1: Profil uživatele](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express blog). LocalDB není určen pro práci se správou IIS. Tato série blogových příspěvků vysvětluje problémy a některá řešení.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Práce s databázemi SQL Server Express

- [Připojovací řetězce serveru SQL Server pro ASP.NET webových aplikací](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Pokud používáte nastavení připojovacího řetězce AttachDBFileName s SQL Server Express, podívejte se zejména na část Instanci uživatele na této stránce.
- [Jak převzít vlastnictví místníSQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express blog). Běžným problémem je, že nelze pracovat s databázemi SQL Server Express, protože nejste správcem instance SQL Server Express. Ve výchozím nastavení je správcem pouze osoba, která nainstalovala sql server Express. Tento blog vysvětluje, jak se vytvořit správce SQL Server Express, pokud jste správce v počítači.
- [Může ASP.NET webová aplikace používat databázi SQL Server Express v produkčním prostředí?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Práce s databází Sql Windows Azure

- [Nasazení zabezpečené ASP.NET aplikace MVC s členstvím, OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (web Microsoft Azure).
- [DATABÁZE SQL](https://docs.microsoft.com/azure/sql-database/) (web Microsoft Azure). Začínáme s kurzy a návody.
- [Databáze SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). Uzel nejvyšší úrovně obsahu pro databázi SQL v msdn.
- [Index článků Wiki webu TechNet na webu TechNet v databázi Windows Azure SQL](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (web Microsoft TechNet).
- [Přechodný blok aplikace pro zpracování poruch](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Rámec, který umožňuje zpracovávat přechodné síťové chyby a chyby připojení, které jsou výsledkem omezení. K dispozici v balíčku NuGet: [Enterprise Library 5.0 - Přechodný blok aplikace pro zpracování chyb](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [Začínáme s sql database a entity framework](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Školicí sada Windows Azure](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft Download Center). Zahrnuje praktická cvičení pro databázi SQL.
- [Fórum komunity databáze SQL Windows Azure](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Přechod na windows azure sql databáze](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Jedna kapitola komplexního komplexního scénáře začátku do konce týmem Microsoft Patterns and Practices. Popisuje, proč můžete chtít migrovat a jak migrovat z SQL Server do databáze SQL.
- [Migrace databází SQL Serveru do databáze Sql Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN) Windows Azure.
- [Průvodce migrací databáze SQL](http://sqlazuremw.codeplex.com/). Nástroj s otevřeným zdrojovým kódem pro migraci databází do a z databáze SQL.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Výběr mezi SQL Serverem a databází Windows Azure SQL Database

- [Porovnejte SQL Server s databází SQL Windows Azure](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (web Microsoft TechNet).
- [Migrace dat do databáze SQL Windows Azure: Nástroje a techniky](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Zahrnuje oddíly, které porovnávají SQL Server s databází SQL a poskytují pokyny, kdy se má z serveru SQL Server do databáze SQL migrovat.
- [Průvodce doručováním databází Windows Azure SQL](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (web Microsoft TechNet).
- [Omezení funkcí serveru SQL Server (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Úložiště tabulek Windows Azure a databáze SQL Windows Azure – porovnání a porovnání](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Pro aplikaci, kterou nasadíte do Windows Azure, může být úložiště tabulek Windows Azure alternativou k databázi Windows Azure SQL Database. Toto téma vám pomůže rozhodnout mezi těmito alternativami.
- [Databáze SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Pokyny a omezení (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Práce se systémy pro správu databází NoSQL

- [Datové služby Windows Azure](https://www.windowsazure.com/develop/net/data/) (web Microsoft Azure). Podívejte se na [průvodce funkcí Table Service](https://docs.microsoft.com/azure/) a část Big **Data** na stránce.
- [ASP.NET vícevrstvé aplikace pomocí tabulek úložiště, fronty a objekty BLOB](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (web Microsoft Azure). Kurz na konci s ukázkovou aplikací ke stažení, která používá tabulky NoSQL úložiště Windows Azure.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Použití dotazů LINQ v ASP.NET aplikacích

- [ASP.NET možnosti přístupu k datům](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Obsahuje úvod do LINQ.
- [LINQ Školení Videa](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagner blog).
- [ASP.NET fórum vlákno s odkazy na dynamické linq zdroje](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Použití dynamického datového lešení

- [Šablony projektů dynamických dat](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Pokyny k použití projektů dynamických dat.
- [ASP.NET dynamických dat](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Zabezpečení přístupu k datům

- [Zabezpečení přístupu k datům v ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Aspekty zabezpečení (entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Postup: Zabezpečené připojovací řetězce při použití ovládacích prvků zdroje dat](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Optimalizace výkonu přístupu k datům

- [ASP.NET přehled výkonu](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET ukládání do mezipaměti](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787) (MSDN). V horní části této stránky je upozornění "Vyřazený obsah", ale většina informací je stále relevantní a neexistuje žádný srovnatelný aktualizovaný zdroj.
- [Zlepšení výkonu serveru SQL Server](https://msdn.microsoft.com/library/ff647793) (MSDN). Stejný komentář jako předchozí odkaz.

Viz také [optimalizace výkonu entity framework](#optimizingef) dříve v tomto tématu.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Nasazení databáze

- [ASP.NET nasazení webu – doporučené prostředky](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Přístup k datům prostřednictvím webové služby

- [Přístup k datům prostřednictvím webové služby](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). Pokyny k použití webového rozhraní API versus WCF.
- [Začínáme s ASP.NET webapi](../web-api/index.md).
- [datové služby WCF](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Další zdroje

- [nejčastější dotazy k přístupu k datům](https://msdn.microsoft.com/library/jj653753.aspx) ASP.NET (MSDN).
- [ASP.NET webových formulářů – data](../web-forms/overview/data-access/index.md). Většina z těchto výukových programů jsou poměrně staré; Nejprve si přečtěte [ASP.NET možnosti přístupu k datům](https://msdn.microsoft.com/library/ms178359.aspx) a [možnosti úložiště dat (vytváření cloudových aplikací reálného světa s Windows Azure),](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) abyste se nedostali příliš daleko k metodě přístupu k datům, která není pro váš scénář vhodná.
- [ASP.NET mapa obsahu MVC](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [ASP.NET kurzy webových stránek – data](../web-pages/overview/data/index.md).
- [Přístup k datům v sadě Visual Studio](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Obsahuje seznam odkazů podobných této mapě obsahu, ale se zaměřením na Visual Studio, nikoli na ASP.NET.
