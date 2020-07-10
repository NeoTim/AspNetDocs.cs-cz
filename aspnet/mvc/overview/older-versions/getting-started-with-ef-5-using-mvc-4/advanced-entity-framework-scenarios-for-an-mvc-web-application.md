---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: Pokročilé scénáře Entity Framework pro webovou aplikaci MVC (10 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163453"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>Pokročilé scénáře Entity Framework pro webovou aplikaci MVC (10 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste implementovali úložiště a pracovní jednotky vzorů. Tento kurz se zabývá následujícími tématy:

- Provádění nezpracovaných dotazů SQL.
- Provádění dotazů bez sledování.
- Zkoumání dotazů odeslaných do databáze.
- Práce se třídami proxy serveru.
- Zakáže se automatické zjišťování změn.
- Zakáže se ověřování při ukládání změn.
- [Chyby a obejít](#errors)

U většiny těchto témat budete pracovat se stránkami, které jste již vytvořili. Pokud chcete hromadné aktualizace použít nezpracovaných SQL, vytvoří se nová stránka, která aktualizuje počet kreditů všech kurzů v databázi:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

A pokud chcete použít dotaz bez sledování, přidejte novou logiku ověřování na stránku pro úpravy oddělení:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>Provádění nezpracovaných dotazů SQL

Rozhraní API pro Entity Framework Code First obsahuje metody, které umožňují předat příkazy SQL přímo do databáze. Máte tyto možnosti:

- Použijte `DbSet.SqlQuery` metodu pro dotazy, které vracejí typy entit. Vrácené objekty musí být typu očekávaného `DbSet` objektem a automaticky sledovány pomocí kontextu databáze, pokud nevypnete sledování. (Další informace o metodě naleznete v následující části `AsNoTracking` .)
- Použijte `Database.SqlQuery` metodu pro dotazy, které vracejí typy, které nejsou entitami. Vrácená data nejsou sledována kontextem databáze, a to i v případě, že použijete tuto metodu k načtení typů entit.
- Pro příkazy, které nejsou typu Query, použijte [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) .

Jednou z výhod používání Entity Framework je, že se vyhnete tomu, že váš kód je příliš úzce k určité metodě ukládání dat. Provede to tím, že vygeneruje dotazy a příkazy SQL za vás, což vám taky zabrání v jejich psaní. Existují však výjimečné scénáře, pokud potřebujete spustit konkrétní dotazy SQL, které jste vytvořili ručně, a tyto metody umožňují zpracovávat takové výjimky.

Jak je vždy true při provádění příkazů SQL ve webové aplikaci, je nutné podniknout preventivní opatření k ochraně vašeho webu před útoky prostřednictvím injektáže SQL. Jedním ze způsobů, jak to provést, je použít parametrizované dotazy, aby se zajistilo, že řetězce odeslané webovou stránkou nejde interpretovat jako příkazy SQL. V tomto kurzu použijete parametrizované dotazy při integraci vstupu uživatele do dotazu.

### <a name="calling-a-query-that-returns-entities"></a>Volání dotazu, který vrací entity

Předpokládejme, že chcete, `GenericRepository` aby třída poskytovala další filtrování a flexibilitu řazení bez nutnosti vytvořit odvozenou třídu s dalšími metodami. Jedním ze způsobů, jak toho dosáhnout, je přidat metodu, která přijímá dotaz SQL. V kontroleru pak můžete určit jakýkoli druh filtrování nebo řazení, jako je například `Where` klauzule, která závisí na spojeních nebo poddotazu. V této části se dozvíte, jak implementovat takovou metodu.

Vytvořte `GetWithRawSql` metodu přidáním následujícího kódu do *GenericRepository.cs*:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

V *CourseController.cs*zavolejte novou metodu z `Details` metody, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

V tomto případě jste mohli použít `GetByID` metodu, ale používáte `GetWithRawSql` metodu k ověření, že `GetWithRawSQL` metoda funguje.

Spusťte stránku podrobností, abyste ověřili, že výběrový dotaz funguje (vyberte kartu **kurz** a pak **Podrobnosti** o jednom kurzu).

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Volání dotazu, který vrací jiné typy objektů

Dříve jste vytvořili tabulku statistik studentů pro stránku o produktu, která ukázala počet studentů pro každé datum registrace. Kód, který je v *HomeController.cs* , používá LINQ:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

Předpokládejme, že chcete napsat kód, který načte tato data přímo v SQL místo použití LINQ. K tomu je nutné spustit dotaz, který vrací něco jiného než objekty entity, což znamená, že je nutné použít `Database.SqlQuery` metodu.

V *HomeController.cs*nahraďte příkaz LINQ v `About` metodě následujícím kódem:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Spusťte stránku o produktu. Zobrazuje stejná data jako předtím.

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>Volání aktualizačního dotazu

Předpokládejme, že správci služby contoso University chtějí v databázi provádět hromadné změny, jako je třeba Změna počtu kreditů pro každý kurz. Pokud má univerzita velký počet kurzů, je třeba je neefektivně načíst jako entity a jednotlivě je měnit. V této části implementujete webovou stránku, která uživateli umožní zadat faktor, podle kterého se má změnit počet kreditů pro všechny kurzy, a provedete změnu provedením `UPDATE` příkazu SQL. Webová stránka bude vypadat jako na následujícím obrázku:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

V předchozím kurzu jste použili obecné úložiště ke čtení a aktualizaci `Course` entit v `Course` řadiči. Pro tuto operaci hromadné aktualizace je potřeba vytvořit novou metodu úložiště, která není v obecném úložišti. K tomu vytvoříte vyhrazenou `CourseRepository` třídu, která je odvozena od `GenericRepository` třídy.

Ve složce *dal* vytvořte *CourseRepository.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

V *UnitOfWork.cs*změňte `Course` Typ úložiště z na. `GenericRepository<Course>``CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

Do *CourseController.cs*přidejte `UpdateCourseCredits` metodu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

Tato metoda bude použita pro i `HttpGet` `HttpPost` . Když je `HttpGet` `UpdateCourseCredits` metoda spuštěna, `multiplier` proměnná bude null a zobrazení zobrazí prázdné textové pole a tlačítko Odeslat, jak je znázorněno na předchozím obrázku.

Po kliknutí na tlačítko **aktualizovat** a `HttpPost` spuštění metody `multiplier` bude v textovém poli zadána hodnota. Kód pak zavolá metodu úložiště `UpdateCourseCredits` , která vrátí počet ovlivněných řádků a tato hodnota je uložena v `ViewBag` objektu. Když zobrazení obdrží počet ovlivněných řádků v `ViewBag` objektu, zobrazí toto číslo místo textového pole a tlačítka Odeslat, jak je znázorněno na následujícím obrázku:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

Vytvořte zobrazení ve složce *Views\Course* na stránce aktualizovat kredity kurzu:

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

V *Views\Course\UpdateCourseCredits.cshtml*nahraďte kód šablony následujícím kódem:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

Spusťte `UpdateCourseCredits` metodu tak, že vyberete kartu **kurzy** a pak na konec adresy URL v adresním řádku prohlížeče přidáte "/UpdateCourseCredits" (například: `http://localhost:50205/Course/UpdateCourseCredits` ). Do textového pole zadejte číslo:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

Klikněte na **Aktualizovat**. Zobrazí se počet ovlivněných řádků:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

Kliknutím na **zpět na seznam** zobrazíte seznam kurzů s revidovaným počtem kreditů.

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

Další informace o nezpracovaných dotazech SQL najdete v tématu [nezpracované dotazy SQL](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) na blogu týmu Entity Framework.

## <a name="no-tracking-queries"></a>Žádné dotazy pro sledování

Když kontext databáze načte řádky databáze a vytvoří objekty entity, které je reprezentují, ve výchozím nastavení udržuje přehled o tom, zda jsou entity v paměti synchronizovány s obsahem databáze. Data v paměti fungují jako mezipaměť a používají se při aktualizaci entity. Toto ukládání do mezipaměti je často zbytečné v rámci webové aplikace, protože instance kontextu jsou obvykle krátkodobé – neuvolňuje (nové je vytvořeno a odstraněno pro každý požadavek) a kontext, který čte entitu, je obvykle uvolněn předtím, než se entita znovu použije.

Můžete určit, zda kontext sleduje objekty entit pro dotaz pomocí `AsNoTracking` metody. Mezi obvyklé scénáře, které byste mohli chtít udělat, patří následující:

- Dotaz načte takový velký objem dat, který vypne sledování, může výrazně zvýšit výkon.
- Chcete připojit entitu, abyste ji mohli aktualizovat, ale dříve jste načetli stejnou entitu pro jiný účel. Vzhledem k tomu, že entita je již sledována kontextem databáze, nelze připojit entitu, kterou chcete změnit. Jedním ze způsobů, jak zabránit tomuto chování, je použití `AsNoTracking` Možnosti s dřívějším dotazem.

V této části budete implementovat obchodní logiku, která ilustruje druhý z těchto scénářů. Konkrétně vynutili obchodní pravidlo, které říká, že instruktor nemůže být správcem více oddělení.

V *DepartmentController.cs*přidejte novou metodu, kterou můžete volat z metod a, aby se `Edit` `Create` zajistilo, že žádný ze dvou oddělení nemá stejného správce:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

Přidejte kód do `try` bloku `HttpPost` `Edit` metody pro volání této nové metody, pokud nedošlo k chybám ověření. `try`Blok teď vypadá jako v následujícím příkladu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

Spusťte stránku pro úpravy oddělení a pokuste se změnit správce oddělení na instruktora, který je již správcem jiného oddělení. Zobrazí se očekávaná chybová zpráva:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Nyní spusťte znovu stránku Upravit oddělení a tentokrát změňte množství **rozpočtu** . Když kliknete na **Uložit**, zobrazí se chybová stránka:

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

Chybová zpráva výjimky je "", k nimž `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` došlo z důvodu následující posloupnosti událostí:

- `Edit`Metoda volá `ValidateOneAdministratorAssignmentPerInstructor` metodu, která načte všechna oddělení, která mají Jan Abercrombie jako správce. To způsobuje, že se v anglickém oddělení přečte. Vzhledem k tomu, že se jedná o upravované oddělení, není hlášena žádná chyba. Výsledkem této operace čtení však je, že entita pro angličtinu, která byla načtena z databáze, je nyní sledována kontextem databáze.
- `Edit`Metoda se pokusí nastavit `Modified` příznak pro entitu v rámci anglického oddělení vytvořenou pořadačem modelu MVC, ale to se nepovede, protože kontext už sleduje entitu pro anglické oddělení.

Jedním z řešení tohoto problému je zachovat kontext ze sledování entit oddělení v paměti načtených ověřovacím dotazem. K tomu nehrozí žádná nevýhoda, protože tuto entitu neaktualizujete ani ji nebudete moct znovu číst způsobem, který by byl z paměti v mezipaměti.

V *DepartmentController.cs*v `ValidateOneAdministratorAssignmentPerInstructor` metodě určete bez sledování, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

Opakujte pokus o úpravu částky **rozpočtu** oddělení. Tentokrát je operace úspěšná a lokalita se vrátí podle očekávání na stránku rejstřík oddělení, kde zobrazuje revidovanou hodnotu rozpočtu.

## <a name="examining-queries-sent-to-the-database"></a>Zkoumání dotazů odeslaných do databáze

Někdy je užitečné, abyste si mohli prohlédnout skutečné dotazy SQL, které se odesílají do databáze. Chcete-li to provést, můžete prostudovat proměnnou dotazu v ladicím programu nebo volat `ToString` metodu dotazu. Pokud to chcete vyzkoušet, podívejte se na jednoduchý dotaz a podívejte se na to, co se děje, když přidáte možnosti, jako je Eager načítání, filtrování a řazení.

V části *Controllers/CourseController*nahraďte `Index` metodu následujícím kódem:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

Nyní nastavte zarážku v *GenericRepository.cs* na `return query.ToList();` a `return orderBy(query).ToList();` příkazy `Get` metody. Spusťte projekt v režimu ladění a vyberte stránku index kurzu. Když kód dosáhne zarážky, prověřte `query` proměnnou. Zobrazí se dotaz, který se odešle do SQL Server. Jedná se o jednoduchý `Select` příkaz:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

Dotazy mohou být příliš dlouhé pro zobrazení v ladicích oknech v aplikaci Visual Studio. Chcete-li zobrazit celý dotaz, můžete zkopírovat hodnotu proměnné a vložit ji do textového editoru:

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

Nyní přidáte rozevírací seznam na stránku indexu kurzu, aby uživatelé mohli filtrovat konkrétní oddělení. Kurzy seřadíte podle názvu a zadáte Eager načítání pro `Department` navigační vlastnost. V *CourseController.cs*nahraďte `Index` metodu následujícím kódem:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

Metoda přijímá vybranou hodnotu rozevíracího seznamu v `SelectedDepartment` parametru. Pokud není nic vybráno, bude mít tento parametr hodnotu null.

`SelectList`Do zobrazení rozevíracího seznamu se předává kolekce obsahující všechna oddělení. Parametry předané `SelectList` konstruktoru určují název pole hodnoty, název textového pole a vybranou položku.

Pro `Get` metodu `Course` úložiště kód určuje výraz filtru, pořadí řazení a Eager načítání pro `Department` navigační vlastnost. Výraz filtru vždy vrátí hodnotu `true` , pokud není nic vybráno v rozevíracím seznamu (tj `SelectedDepartment` . je null).

V *Views\Course\Index.cshtml*bezprostředně před počáteční `table` značkou přidejte následující kód k vytvoření rozevíracího seznamu a tlačítko Odeslat:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

I když se zarážky ve třídě pořád nastavují `GenericRepository` , spusťte stránku index kurzu. Pokračujte v první dvou případech, kdy kód narazí na zarážku, aby se stránka zobrazila v prohlížeči. V rozevíracím seznamu vyberte oddělení a klikněte na **Filtr**:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

Tentokrát bude první zarážka pro dotaz oddělení v rozevíracím seznamu. Přeskočí tuto proměnnou a zobrazí `query` se, když kód příště dosáhne zarážky, aby se zobrazila informace o tom, jaký `Course` dotaz teď vypadá jako. Uvidíte něco podobného jako následující:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

Vidíte, že dotaz je nyní `JOIN` dotazem, který načítá `Department` data společně s `Course` daty a obsahuje `WHERE` klauzuli.

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>Práce s třídami proxy

Když Entity Framework vytvoří instance entit (například při spuštění dotazu), často je vytvoří jako instance dynamicky generovaného odvozeného typu, který funguje jako proxy pro entitu. Tento proxy Přepisuje některé virtuální vlastnosti entity, aby mohl vkládat háky pro provádění akcí automaticky při získání k vlastnosti. Například tento mechanismus slouží k podpoře opožděného načítání vztahů.

Ve většině případů nemusíte znát použití proxy serverů, ale existují výjimky:

- V některých případech můžete chtít zabránit Entity Framework v vytváření instancí proxy serveru. Například serializace instancí, které nejsou proxy, může být efektivnější než serializace instancí proxy serveru.
- Při vytváření instance třídy entity pomocí `new` operátoru nezískáte instanci proxy. To znamená, že nezískáte funkce, jako je opožděné načítání a automatické sledování změn. Obvykle je to v pořádku. obecně nepotřebujete opožděné načítání, protože vytváříte novou entitu, která není v databázi, a obecně nepotřebujete sledování změn, pokud entitu výslovně označíte jako `Added` . Pokud však potřebujete opožděné načítání a potřebujete sledování změn, můžete vytvořit nové instance entit s proxy objekty pomocí `Create` metody `DbSet` třídy.
- Je možné, že budete chtít z typu proxy získat skutečný typ entity. Pomocí `GetObjectType` metody `ObjectContext` třídy můžete získat skutečný typ entity instance typu proxy serveru.

Další informace najdete v tématu [práce se proxy](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) na blogu Entity Framework týmu.

## <a name="disabling-automatic-detection-of-changes"></a>Zákaz automatického zjišťování změn

Entity Framework určuje, jak se entita změnila (takže se aktualizace musí odeslat do databáze) porovnáním aktuálních hodnot entity s původními hodnotami. Původní hodnoty se uloží při dotazování nebo připojení entity. Některé z metod, které způsobují automatickou detekci změn, jsou následující:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Pokud sledujete velký počet entit a v rámci smyčky několikrát voláte jednu z těchto metod, můžete dosáhnout výrazného zlepšení výkonu tím, že se pomocí vlastnosti [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) dočasně vypne funkce automatického zjišťování změn. Další informace najdete v tématu [automatické zjišťování změn](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).

## <a name="disabling-validation-when-saving-changes"></a>Zakázání ověřování při ukládání změn

Když zavoláte `SaveChanges` metodu, ve výchozím nastavení Entity Framework před aktualizací databáze ověřuje data ve všech vlastnostech všech změněných entit. Pokud jste aktualizovali velký počet entit a již jste ověřili data, je tato práce nepotřebná a je možné, že proces uložení změn trvá méně času tím, že se dočasně vypne ověřování. Můžete to udělat pomocí vlastnosti [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) . Další informace najdete v tématu [ověření](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).

## <a name="summary"></a>Shrnutí

Tím se dokončí Tato série kurzů na používání Entity Framework v aplikaci ASP.NET MVC. Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

Další informace o tom, jak nasadit webovou aplikaci po sestavení, naleznete v tématu [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx) v knihovně MSDN.

Informace o dalších tématech souvisejících s MVC, jako je ověřování a autorizace, najdete v tématu [Doporučené prostředky MVC](../../getting-started/recommended-resources-for-mvc.md).

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>Poděkování

- Dykstra napsal původní verzi tohoto kurzu a je vedoucím programovacím autorem týmu obsahu pro webové platformy a nástroje Microsoftu.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) spoluvytvořil tento kurz a většinu práce aktualizovala pro EF 5 a MVC 4. Rick je hlavní programovací zapisovač pro zaměření Microsoftu na Azure a MVC.
- [Rowan Miller](http://www.romiller.com) a další členové týmu Entity Framework pomáhat s revizemi kódu a pomohli ladit mnoho problémů s migracemi, které vznikly během aktualizace kurzu pro EF 5.

## <a name="vb"></a>VB

V době, kdy byl kurz původně vytvořen, jsme poskytovali verzi dokončeného projektu stažení v jazyce C# i VB. V této aktualizaci poskytujeme projekt ke stažení v jazyce C# pro každou kapitolu, aby bylo snazší začít kdekoli v řadě, ale kvůli časovým omezením a dalším prioritám, které jsme v jazyce VB nevytvořili. Pokud sestavíte projekt VB pomocí těchto kurzů a chcete ho sdílet s ostatními, dejte nám prosím informace.

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>Chyby a alternativní řešení

### <a name="cannot-createshadow-copy"></a>Nelze vytvořit/stínovou kopii

Chybová zpráva:

*Nelze vytvořit nebo stínovou kopii DotNetOpenAuth. OpenId, pokud tento soubor již existuje.*

Řešení:

Počkejte několik sekund a aktualizujte stránku.

### <a name="update-database-not-recognized"></a>Aktualizace – databáze nebyla rozpoznána.

Chybová zpráva:

*Termín "aktualizace databáze" nebyl rozpoznán jako název rutiny, funkce, souboru skriptu nebo spustitelného programu. Zkontrolujte pravopis názvu, nebo pokud byla vložena cesta, ověřte, zda je cesta správná, a akci opakujte.* (Z *`Update-Database`* příkazu v PMC.)

Řešení:

Ukončete aplikaci Visual Studio. Znovu otevřete projekt a zkuste to znovu.

### <a name="validation-failed"></a>Neúspěšné ověření

Chybová zpráva:

*Nepodařilo se ověřit jednu nebo více entit. Další podrobnosti najdete ve vlastnosti ' EntityValidationErrors '.* (Z *`Update-Database`* příkazu v PMC.)

Řešení:

Jednou z příčin tohoto problému jsou chyby ověření při `Seed` spuštění metody. Tipy k ladění metody naleznete v tématu [osazení a ladění Entity Framework (EF) databáze](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` .

### <a name="http-50019-error"></a>Chyba HTTP 500,19

Chybová zpráva:

*Chyba protokolu HTTP 500,19 – vnitřní chyba serveru: k požadované stránce nelze přistupovat, protože související konfigurační data stránky jsou neplatná.*

Řešení:

Jedním ze způsobů, jak získat tuto chybu, je použití více kopií řešení, přičemž každý z nich používá stejné číslo portu. Tento problém obvykle můžete vyřešit ukončením všech instancí aplikace Visual Studio a následným restartováním projektu, na kterém pracujete. Pokud to nepomůže, zkuste změnit číslo portu. Klikněte pravým tlačítkem na soubor projektu a pak klikněte na vlastnosti. Vyberte kartu **Web** a potom změňte číslo portu v textovém poli **Adresa URL projektu** .

### <a name="error-locating-sql-server-instance"></a>Při hledání instance SQL Server došlo k chybě.

Chybová zpráva:

*Při navazování připojení k SQL Server došlo k chybě související se sítí nebo instanci. Server nebyl nalezen nebo k němu nelze získat přístup. Ověřte, zda je název instance správný a zda je SQL Server nakonfigurovaná tak, aby povolovala vzdálená připojení. (poskytovatel: síťová rozhraní SQL, chyba: 26 – Chyba při hledání zadaného serveru nebo instance)*

Řešení:

Ověřte připojovací řetězec. Pokud jste databázi odstranili ručně, změňte název databáze v řetězci konstrukce.

> [!div class="step-by-step"]
> [Předchozí](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
>  [Další](building-the-ef5-mvc4-chapter-downloads.md)
