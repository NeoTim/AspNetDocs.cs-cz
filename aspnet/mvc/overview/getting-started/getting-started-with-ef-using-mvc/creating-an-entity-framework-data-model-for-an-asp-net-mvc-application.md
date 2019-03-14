---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 'Kurz: Začínáme s Entity Framework 6 Code First pomocí MVC 5 | Dokumentace Microsoftu'
description: V této sérii kurzů se dozvíte, jak sestavit aplikaci ASP.NET MVC 5, která pro přístup k datům používá Entity Framework 6.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076051"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>Kurz: Začínáme s Entity Framework 6 Code First pomocí MVC 5

> [!NOTE]
> Pro nový vývoj doporučujeme [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) přes zobrazení a kontrolery ASP.NET MVC. Pro řadu kurzů podobné následujícímu pomocí Razor Pages, naleznete v tématu [kurzu: Začínáme se stránkami Razor v ASP.NET Core](/aspnet/core/tutorials/razor-pages/razor-pages-start). Nové kurzu:
> * Je usnadňuje její sledování.
> * Poskytuje další EF Core osvědčené postupy.
> * Používá účinnější dotazy.
> * Je více aktuální pomocí nejnovější rozhraní API.
> * Zahrnuje další funkce.
> * Je upřednostňovaný způsob pro nový vývoj aplikací.

V této sérii kurzů se dozvíte, jak sestavit aplikaci ASP.NET MVC 5, která pro přístup k datům používá Entity Framework 6. Tento kurz používá Code First pracovního postupu. Informace o tom, jak si vybrat mezi Code First, Database First a první Model, najdete v části [vytvořit model](/ef/ef6/modeling/).

Tato série kurzů vysvětluje, jak vytvořit ukázková aplikace Contoso University. Ukázková aplikace je jednoduchá university webu. S ním můžete zobrazit a aktualizovat Všichni studenti, kurz a informace instruktorem. Tady jsou dvě obrazovky, kterou jste vytvořili:

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![Upravit studenta](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření webové aplikace MVC
> * Nastavit styl lokality
> * Nainstalujte rozhraní Entity Framework 6
> * Vytvoření datového modelu
> * Vytvořte kontext databáze
> * Inicializace databáze s testovací data
> * Nastavení EF 6 pro použití LocalDB
> * Vytvoření kontroleru a zobrazení
> * Zobrazení databáze

## <a name="prerequisites"></a>Požadavky

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>Vytvoření webové aplikace MVC

1. Otevřete Visual Studio a vytvořte C# webového projektu pomocí **webová aplikace ASP.NET (.NET Framework)** šablony. Pojmenujte projekt *ContosoUniversity* a vyberte **OK**.

   ![Dialogové okno Nový projekt v sadě Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. V **nová webová aplikace ASP.NET - ContosoUniversity**vyberte **MVC**.

   ![Webové aplikace dialogové okno Nový v sadě Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > Ve výchozím nastavení **ověřování** je možnost nastavená na **bez ověřování**. Pro účely tohoto kurzu webové aplikace nevyžaduje, aby uživatelům umožní přihlásit. Také nijak neomezuje přístup na základě, na který je přihlášen.

1. Vyberte **OK** pro vytvoření projektu.

## <a name="set-up-the-site-style"></a>Nastavit styl lokality

Několik jednoduchých změn se nastavit v nabídce webu, rozložení a domovské stránky.

1. Otevřít *Views\Shared\\_Layout.cshtml*a proveďte následující změny:

   - Změňte všechny výskyty "My ASP.NET Application" a "Název aplikace" na "University společnosti Contoso".
   - Přidání položek nabídky pro studenty, kurzy, vyučující a oddělení a odstraňte záznam kontaktu.

   Změny jsou vyznačené na následující fragment kódu:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. V *Views\Home\Index.cshtml*, nahraďte obsah souboru následující kód, který nahradí text o ASP.NET a MVC o této aplikaci:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. Stiskněte Ctrl + F5 ke spuštění webové stránky. Zobrazí domovská stránka s hlavní nabídky.

## <a name="install-entity-framework-6"></a>Nainstalujte rozhraní Entity Framework 6

1. Z **nástroje** nabídky, zvolte **Správce balíčků NuGet**a pak zvolte **konzoly Správce balíčků**.

2. V **Konzola správce balíčků** okno, zadejte následující příkaz:

   ```text
   Install-Package EntityFramework
   ```

Tento krok je jedním z několika kroků, obsahující tento kurz můžete provést ručně, ale že by byly provedeny automaticky funkcí generování uživatelského rozhraní technologie ASP.NET MVC. Provádíte je ručně, aby mohli zobrazit kroky potřebné k použití Entity Framework (EF). Později budete používat generování uživatelského rozhraní pro vytvoření kontroleru MVC a zobrazení. Alternativou je umožnit generování uživatelského rozhraní automaticky nainstalovat balíček EF NuGet, vytvořit třídy kontextu databáze a vytvořit připojovací řetězec. Jakmile budete připraveni to udělat tak, je vše, co musíte udělat Přeskočit tyto kroky a generování uživatelského rozhraní řadiče MVC po vytvoření tříd entit.

## <a name="create-the-data-model"></a>Vytvoření datového modelu

Dále vytvoříte tříd entit pro aplikaci Contoso University. Začnete s následující tři entity:

**Kurz** <-> **registrace** <-> **studenta**

| Entity | Relace |
| -------- | ------------ |
| Kurz k registraci | Jeden mnoho |
| Student k registraci | Jeden mnoho |

Existuje vztah jeden mnoho mezi `Student` a `Enrollment` entity, a existuje vztah jeden mnoho mezi `Course` a `Enrollment` entity. Jinými slovy student možné zaregistrovat libovolný počet kurzy a kurzu může mít libovolný počet studentů zaregistrovaná do něj.

V následujících částech vytvoříte třídu pro každou z těchto entit.

> [!NOTE]
> Pokud se pokusíte ke kompilaci projektu před dokončením vytvoření všech těchto tříd entit, získáte chyby kompilátoru.

### <a name="the-student-entity"></a>Entita studenta

- V *modely* složku, vytvořte soubor třídy s názvem *Student.cs* klepnutím pravým tlačítkem myši na složku v **Průzkumník řešení** a volba **přidat**  >  **Třídy**. Nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` Vlastnost se stane sloupec primárního klíče tabulky databáze, která odpovídá této třídy. Ve výchozím nastavení Entity Framework interpretuje vlastnost s názvem `ID` nebo *název třídy* `ID` jako primární klíč.

`Enrollments` Je vlastnost *navigační vlastnost*. Vlastnosti navigace podržte dalšími subjekty, které se vztahují k této entity. V takovém případě `Enrollments` vlastnost `Student` entita bude obsahovat všechny `Enrollment` entity, které se vztahují k, které `Student` entity. Jinými slovy Pokud daný `Student` řádků v databázi má dva související `Enrollment` řádky (hodnota řádky, které obsahují student získal primární klíč v jejich `StudentID` sloupec cizího klíče), který `Student` entity `Enrollments` navigační vlastnost bude obsahovat tyto dvě `Enrollment` entity.

Navigační vlastnosti se obvykle definují jako `virtual` tak, aby se můžete využít některé funkce Entity Framework, jako *opožděné načtení*. (Opožděné načtení budou vysvětlena dále v [čtení souvisejících dat](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) později v této sérii kurzů.)

Pokud vlastnost navigace může obsahovat více entit (jako v relace m: n nebo 1 n), jeho typ musí být seznam, ve kterém položky lze přidávat, odstranit a aktualizovat, například `ICollection`.

### <a name="the-enrollment-entity"></a>Registrace entity

- V *modely* složku, vytvořte *Enrollment.cs* a nahraďte existující kód následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` Bude mít vlastnost primárního klíče; tato entita používá *classname* `ID` vzorku místo `ID` samostatně jako jste viděli v `Student` entity. Obvykle by zvolte jeden model a použít ho v rámci datového modelu. Tady variantu ukazuje, které můžete použít buď vzor. V pozdějších kurzech, zobrazí se vám jak pomocí `ID` bez `classname` usnadňuje implementaci dědičnosti v datovém modelu.

`Grade` Vlastnost je [výčtu](/ef/ef6/modeling/code-first/data-types/enums). Otazník po `Grade` deklarace typu znamená, že `Grade` vlastnost [s možnou hodnotou Null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types). Se liší od nulovou na podnikové úrovni na podnikové úrovni, který má hodnotu null – hodnota null znamená známku vyjádřenou není znám nebo ještě nebyly přiřazeny.

`StudentID` Vlastnost je cizí klíč a odpovídající navigační vlastnost je `Student`. `Enrollment` Entita je přidružený nejméně k jednomu `Student` entity, tak vlastnost může obsahovat pouze jeden `Student` entity (na rozdíl od `Student.Enrollments` navigační vlastnost předchozímu příkladu, který může obsahovat více `Enrollment` entity).

`CourseID` Vlastnost je cizí klíč a odpovídající navigační vlastnost je `Course`. `Enrollment` Entita je přidružený nejméně k jednomu `Course` entity.

Nastavení interpretuje Entity Framework vlastnost jako vlastnost cizího klíče Pokud je název *&lt;název navigační vlastnosti&gt;&lt;vlastnost primárního klíče název&gt;* (například `StudentID`pro `Student` navigační vlastnost, protože `Student` je primární klíč entity `ID`). Vlastnosti cizího klíče může také být pojmenován stejně jednoduše *&lt;vlastnost primárního klíče název&gt;* (například `CourseID` od `Course` je primární klíč entity `CourseID`).

### <a name="the-course-entity"></a>Kurz entity

- V *modely* složku, vytvořte *Course.cs*, nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` Je navigační vlastnost. A `Course` entit může souviset s libovolným počtem `Enrollment` entity.

Budete říkáme více o <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> atribut v pozdějších kurzech této řady. V podstatě tento atribut umožňuje zadat primární klíč pro kurz namísto nutnosti databáze jeho vygenerování.

## <a name="create-the-database-context"></a>Vytvořte kontext databáze

Hlavní třída, která koordinuje funkce Entity Framework pro daný datový model je *kontext databáze* třídy. Vytvoření této třídy odvozené z [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) třídy. Ve svém kódu určit entit, které jsou součástí datového modelu. Můžete také přizpůsobit chování určité Entity Framework. V tomto projektu je s názvem třídy `SchoolContext`.

- K vytvoření složky v projektu ContosoUniversity, klikněte pravým tlačítkem na projekt v **Průzkumníka řešení** a klikněte na tlačítko **přidat**a potom klikněte na tlačítko **novou složku**. Název nové složky *DAL* (pro Data Access Layer). V této složce, vytvořte nový soubor třídy *SchoolContext.cs*a nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>Určení sady entit

Tento kód vytvoří [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) vlastností pro každou sadu entit. V terminologii Entity Framework *sadu entit* obvykle odpovídá tabulku databáze a *entity* odpovídající řádek v tabulce.

> [!NOTE]
>
> Můžete vynechat `DbSet<Enrollment>` a `DbSet<Course>` příkazy a bude fungovat stejně. Entity Framework bude zahrnovat je implicitně protože `Student` odkazy na entity `Enrollment` entity a `Enrollment` odkazy na entity `Course` entity.

### <a name="specify-the-connection-string"></a>Zadejte připojovací řetězec

Název připojovacího řetězce (které přidáte do souboru Web.config později) je předáno konstruktoru.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

Můžete také předat samotný připojovací řetězec ne název jednoho, který je uložen v souboru Web.config. Další informace o možnosti pro určení databáze, které se mají použít, najdete v části [připojovací řetězce a modely](/ef/ef6/fundamentals/configuring/connection-strings).

Pokud nechcete explicitně zadat připojovací řetězec nebo název jednoho, Entity Framework předpokládá, že název připojovacího řetězce je stejný jako název třídy. Výchozí název připojovacího řetězce v tomto příkladu by pak `SchoolContext`, stejně jako co zadáváte explicitně.

### <a name="specify-singular-table-names"></a>Zadejte názvy singulární tabulek

`modelBuilder.Conventions.Remove` Výroky [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) metoda zabraňuje se pluralized názvy tabulek. Pokud jste to neudělali, by se pojmenoval generované tabulky v databázi `Students`, `Courses`, a `Enrollments`. Místo toho budou názvy tabulek `Student`, `Course`, a `Enrollment`. Vývojáři Nesouhlasím o tom, jestli by měl názvy tabulek pluralized nebo ne. Tento kurz používá jednotný tvar, ale důležité je, že můžete vybrat libovolný formulář dáváte přednost zahrnutím nebo vynechání tento řádek kódu.

## <a name="initialize-db-with-test-data"></a>Inicializace databáze s testovací data

Entity Framework můžete automaticky vytvořit (nebo vyřadit a znovu vytvořit) databáze za vás při spuštění aplikace. Můžete určit, že to by mělo být provedeno pokaždé, když vaše aplikace spuštěná, nebo jenom v případě modelu je synchronizovaný s existující databází. Můžete je zapsat také `Seed` metody tohoto rozhraní Entity Framework automaticky volá po vytvoření databáze, aby bylo možné naplnit ho daty testu.

Výchozí chování je vytvořit databázi jenom v případě, že ho neexistuje (a vyvolání výjimky, pokud došlo ke změně modelu a databáze již existuje). V této části zadáte, že by měl být databázi vyřadit a znovu vytvořit při každé změně modelu. Vyřazení databáze způsobí ztrátu všechna vaše data. Toto je obvykle dobře během vývoje, protože `Seed` metody se spustí, jakmile se znovu vytvoří databázi a znovu vytvoříte testovací data. Ale v produkčním prostředí budete obvykle nechcete ztratit všechna vaše data pokaždé, když je třeba změnit schéma databáze. Později uvidíte, jak zpracovat změny modelu pomocí migrace Code First pro změnu schématu databáze místo vyřadit a znovu vytvořit databázi.

1. Ve složce DAL, vytvořte nový soubor třídy s názvem *SchoolInitializer.cs* a nahraďte kód šablony následujícím kódem, což způsobí, že databáze má být vytvořen v případě potřeby a načte testovací data do nové databáze.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` Metoda přijímá jako vstupní parametr objekt kontextu databáze, a kód v metodě používá tento objekt k přidání nové entity do databáze. Pro každý typ entity kód vytvoří kolekci nové entity, se přidají do příslušné `DbSet` vlastnost a uloží změny do databáze. Není nutné volat `SaveChanges` metoda po každé skupiny entit, jako se zde provádí, ale způsobem, který pomáhá při hledání příčiny problému, pokud dojde k výjimce, zatímco kód zapisuje do databáze.

2. Zjistit Entity Framework pomocí vaší inicializátor třídy, přidejte element, který má `entityFramework` v aplikaci prvku *Web.config* souboru (je v kořenové složce projektu), jak je znázorněno v následujícím příkladu:

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` Určuje kontext plně kvalifikovaný název třídy a sestavení probíhá, a `databaseinitializer type` Určuje plně kvalifikovaný název inicializátor třídy a je v sestavení. (Pokud nechcete, aby EF použití inicializátoru, můžete nastavit atribut na `context` element: `disableDatabaseInitialization="true"`.) Další informace najdete v tématu [nastavení konfiguračního souboru](/ef/ef6/fundamentals/configuring/config-file).

   Alternativa k nastavení inicializátoru *Web.config* souboru se to udělat v kódu tak, že přidáte `Database.SetInitializer` příkazu `Application_Start` metoda ve *Global.asax.cs* souboru. Další informace najdete v tématu [Principy inicializátory databáze v Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).

Aplikace je nyní nastavit tak, aby při přístupu k databázi v daném běhu aplikace poprvé, Entity Framework porovnává databáze do modelu (vaše `SchoolContext` a tříd entit). Pokud rozdíl aplikace zahodí a znovu vytvoří databázi.

> [!NOTE]
> Při nasazení aplikace do produkčního prostředí webového serveru, musíte odebrat nebo zakázat kód, který se zahodí a znovu vytvoří databázi. Můžete to udělat v pozdějších kurzech v této sérii.

## <a name="set-up-ef-6-to-use-localdb"></a>Nastavení EF 6 pro použití LocalDB

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) je Odlehčená verze databázového stroje systému SQL Server Express. Snadno nainstalujte a nakonfigurujte, spustí na vyžádání a běží v uživatelském režimu. LocalDB běží v ve speciálním režimu provádění SQL Server Express, která umožňuje pracovat s databází jako *.mdf* soubory. Můžete umístit soubory databáze LocalDB *aplikace\_Data* složce webového projektu, pokud chcete zkopírovat databázi s projektem. Funkce instance uživatele v SQL serveru Express také umožňuje pracovat s *.mdf* soubory, ale uživatelské instance funkce je zastaralá možnost; proto se doporučuje LocalDB pro práci s *.mdf* soubory. LocalDB je nainstalovaný ve výchozím nastavení se sadou Visual Studio.

Obvykle SQL Server Express se nepoužívá pro produkční webové aplikace. LocalDB zejména se nedoporučuje pro produkční použití s webovou aplikací vzhledem k tomu, že má nejsou určeny pro práci se službou IIS.

- V tomto kurzu budete pracovat s LocalDB. Otevřete aplikaci *Web.config* a přidejte `connectionStrings` předchozí element `appSettings` elementu, jak je znázorněno v následujícím příkladu. (Nezapomeňte aktualizovat *Web.config* soubor v kořenové složce projektu. K dispozici je také *Web.config* soubor *zobrazení* podsložky, která není nutné aktualizovat.)

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

Určuje připojovací řetězec, který jste přidali, Entity Framework použijete databázi LocalDB s názvem *ContosoUniversity1.mdf*. (Databáze ještě neexistuje ale EF ji vytvoří.) Pokud chcete vytvořit databázi v vaše *aplikace\_Data* složky, můžete přidat `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` na připojovací řetězec. Další informace o připojovacích řetězcích najdete v tématu [připojovací řetězce SQL serveru pro webové aplikace ASP.NET](/previous-versions/aspnet/jj653752(v=vs.110)).

Doopravdy nepotřebujete připojovacího řetězce v *Web.config* souboru. Pokud nezadáte připojovací řetězec, Entity Framework používá výchozí propojovací řetězec založené na třídě kontextu. Další informace najdete v tématu [Code First pro novou databázi](/ef/ef6/modeling/code-first/workflows/new-database).

## <a name="create-controller-and-views"></a>Vytvoření kontroleru a zobrazení

Teď vytvoříte webovou stránku zobrazit data. Proces žádosti o data automaticky aktivuje vytváření databáze. Zobrazí za přibližně tak, že vytvoříte nový kontroler. Ale předtím, než to uděláte, sestavte projekt a zpřístupnit třídy modelu a kontextu pro generování uživatelského rozhraní řadiče MVC.

1. Klikněte pravým tlačítkem na **řadiče** složky v **Průzkumníka řešení**vyberte **přidat**a potom klikněte na tlačítko **novou vygenerovanou položku**.
2. V **přidat vygenerované uživatelské rozhraní** dialogu **kontroler MVC 5 se zobrazeními, používá nástroj Entity Framework**a klikněte na tlačítko **přidat**.

     ![Přidat dialog vygenerované uživatelské rozhraní v sadě Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. V **přidat kontroler** dialogové okno, proveďte následující výběr a klikněte na tlačítko **přidat**:

   - Třída modelu: **Student (ContosoUniversity.Models)**. (Pokud se tato možnost v rozevíracím seznamu nezobrazí, sestavte projekt a zkuste to znovu.)
   - Třída kontextu dat: **SchoolContext (ContosoUniversity.DAL)**.
   - Název kontroleru: **StudentController** (ne StudentsController).
   - Ponechte výchozí hodnoty pro ostatní pole.

     Po kliknutí na **přidat**, vytvoří scaffolder *StudentController.cs* souboru a nastavte zobrazení (*.cshtml* soubory), které fungují s kontrolerem. V budoucnu při vytváření projektů, které využívají Entity Framework, můžete taky využít výhod některé další funkce scaffolder: vytvoření vaší první třídy modelu, nevytvářejte připojovací řetězec a pak **přidat kontroler** pole zadejte **nový kontext dat.** tak, že vyberete **+** vedle **třída kontextu dat**. Vytvoří scaffolder vaše `DbContext` třídy a připojení řetězec a také kontroler a zobrazení.
4. Visual Studio otevře *Controllers\StudentController.cs* souboru. Uvidíte, že proměnné třídy se vytvořil, který vytvoří instanci objektu kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` Metody akce získá seznam studenti z *studenty* načtením sadu entit `Students` vlastnost instance kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml* zobrazení seznamu v tabulce:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Stiskněte kombinaci kláves Ctrl + F5 ke spuštění projektu. (Pokud dojde k chybě "Nejde vytvořit stínovou kopii" zavřete prohlížeč a zkuste to znovu.)

     Klikněte na tlačítko **studenty** kartu pro zobrazení testovacích dat, který `Seed` metoda vložen. V závislosti na tom, jak úzké okno prohlížeče, je, uvidíte odkaz karta studenta nejvyšší adresního řádku nebo budete muset klikněte na tlačítko pravém horním rohu na odkaz.

     ![Tlačítko nabídky](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>Zobrazení databáze

Když jste spustili na stránce studenty a pokusu o přístup k databázi aplikace, zjistí EF, existuje se žádná databáze a jste jej vytvořili. EF pak jste spustili seed – metoda k naplnění databáze s daty.

Můžete použít buď **Průzkumníka serveru** nebo **Průzkumník objektů systému SQL Server** (SSOX) Chcete-li zobrazit databáze v sadě Visual Studio. Pro účely tohoto kurzu budete používat **Průzkumníka serveru**.

1. Zavřete prohlížeč.
2. V **Průzkumníka serveru**, rozbalte **datová připojení** (budete muset nejprve vyberte tlačítko pro aktualizaci), rozbalte **školním kontextu (ContosoUniversity)** a potom rozbalte  **Tabulky** zobrazíte tabulek v nové databázi.

3. Klikněte pravým tlačítkem na **Student** tabulky a klikněte na tlačítko **zobrazit Data tabulky** zobrazit sloupce, které byly vytvořeny a řádky, které byly vloženy do tabulky.

4. Zavřít **Průzkumníka serveru** připojení.

*ContosoUniversity1.mdf* a *.ldf* databázové soubory jsou v *% USERPROFILE %* složky.

Vzhledem k tomu, že používáte `DropCreateDatabaseIfModelChanges` inicializátor, může teď provedete změnu `Student` třídy, spusťte aplikaci znovu spustit a databáze bude automaticky znovu vytvořit tak, aby odpovídaly změny. Například, pokud chcete přidat `EmailAddress` vlastnost `Student` třídy, znovu spusťte stránce studenty a pak pohled na tabulku znovu, zobrazí se vám nový `EmailAddress` sloupce.

## <a name="conventions"></a>Konvence

Množství kódu, které jste měli pro zápis v pořadí pro Entity Framework umožnit vytvoření kompletní databáze je minimální z důvodu *konvence*, nebo předpokladů, které díky rozhraní Entity Framework. Některé z nich už bylo uvedeno nebo byly použity bez vašeho vědomí:

- Pluralized formy názvy tříd entit se používají jako názvy tabulek.
- Názvy vlastností entity se používají pro názvy sloupců.
- Vlastnosti entity, které jsou pojmenovány `ID` nebo *classname* `ID` jsou rozpoznány jako vlastnosti primárního klíče.
- Vlastnost je interpretován jako vlastnost cizího klíče, pokud je název *&lt;název navigační vlastnosti&gt;&lt;vlastnost primárního klíče název&gt;* (například `StudentID` pro `Student` navigační vlastnost, protože `Student` je primární klíč entity `ID`). Vlastnosti cizího klíče může také být pojmenován stejně jednoduše &lt;vlastnost primárního klíče název&gt; (například `EnrollmentID` od `Enrollment` je primární klíč entity `EnrollmentID`).

Už víte, že konvence lze přepsat. Například jste zadali, že by neměla být pluralized názvy tabulek a později uvidíte, jak lze explicitně označit vlastnost jako vlastnost cizího klíče.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Další informace o EF 6 najdete v těchto článcích:

* [Přístup k datům ASP.NET – doporučené zdroje informací](../../../../whitepapers/aspnet-data-access-content-map.md)

* [První konvence kódu](/ef/ef6/modeling/code-first/conventions/built-in)

* [Vytvoření složitějšího datového modelu](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření webové aplikace MVC
> * Nastavit styl lokality
> * Nainstalované Entity Framework 6
> * Vytvoření datového modelu
> * Vytvoří kontext databáze
> * Inicializované databáze se testovací data
> * Nastavení EF 6 pro použití LocalDB
> * Vytvořený kontroler a zobrazení
> * Zobrazení databáze

Přejděte k dalším článku se naučíte, jak zkontrolovat a upravit vytvořit, číst, aktualizovat, odstranění (CRUD) kódu v kontrolerů a zobrazení.
> [!div class="nextstepaction"]
> [Implementace základních funkcí CRUD](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)