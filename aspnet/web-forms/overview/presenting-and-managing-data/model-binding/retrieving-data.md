---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Načítání a zobrazování dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240748"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>Načítání a zobrazování dat s vazbami modelů a webovými formuláři

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> Vzor vazby modelu funguje s libovolnou technologií pro přístup k datům. V tomto kurzu použijete Entity Framework, ale můžete použít technologii pro přístup k datům, která je pro vás nejvhodnější. Z ovládacího prvku vázaného na data, jako je ovládací prvek GridView, ListView, DetailsView nebo FormView, určíte názvy metod, které se mají použít pro výběr, aktualizaci, odstranění a vytváření dat. V tomto kurzu zadáte hodnotu pro vlastnost SelectMethod. 
> 
> V rámci této metody poskytnete logiku pro načítání dat. V dalším kurzu nastavíte hodnoty pro UpdateMethod, DeleteMethod a určena metoda InsertMethod.
>
> Můžete [Stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v jazyce C# nebo Visual Basic. Kód ke stažení funguje v sadě Visual Studio 2012 a novějších. Používá šablonu sady Visual Studio 2012, která je mírně odlišná než šablona sady Visual Studio 2017 uvedená v tomto kurzu.
> 
> V kurzu spustíte aplikaci v aplikaci Visual Studio. Aplikaci můžete nasadit také pro poskytovatele hostingu a zpřístupnit ji přes Internet. Společnost Microsoft nabízí bezplatné webové hostování až pro 10 webů v  
> [bezplatný zkušební účet Azure](https://azure.microsoft.com/free/dotnet/). Informace o tom, jak nasadit webový projekt aplikace Visual Studio do Azure App Service Web Apps, naleznete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) Series. Tento kurz také ukazuje, jak použít Migrace Entity Framework Code First k nasazení databáze SQL Server do Azure SQL Database.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> - Microsoft Visual Studio 2017 nebo Microsoft Visual Studio Community 2017
>   
> Tento kurz také funguje se sadou Visual Studio 2012 a Visual Studio 2013, ale v uživatelském rozhraní a šabloně projektu jsou nějaké rozdíly.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu:

* Vytváření datových objektů, které odrážejí vysokou univerzita s studenty registrovanými v kurzech
* Vytváření tabulek databáze z objektů
* Naplnit databázi testovacími daty
* Zobrazení dat ve webovém formuláři

## <a name="create-the-project"></a>Vytvoření projektu

1. V aplikaci Visual Studio 2017 vytvořte projekt **webové aplikace ASP.NET (.NET Framework)** s názvem **ContosoUniversityModelBinding**.

   ![vytvořit projekt](retrieving-data/_static/image19.png)

2. Vyberte **OK**. Zobrazí se dialogové okno pro výběr šablony.

   ![vybrat webové formuláře](retrieving-data/_static/image3.png)

3. Vyberte šablonu **webových formulářů** . 

4. V případě potřeby změňte ověřování na **jednotlivé uživatelské účty**. 

5. Vyberte **OK** a vytvořte projekt.

## <a name="modify-site-appearance"></a>Upravit vzhled webu

   Udělejte několik změn pro přizpůsobení vzhledu webu. 
   
   1. Otevřete soubor Web. Master.
   
   2. Změňte název, aby se zobrazila **Společnost Contoso University** a ne **Moje aplikace ASP.NET**.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. Změňte text záhlaví z **názvu aplikace** na **Univerzita Contoso**.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. Změňte navigační záhlaví odkazy na příslušné lokality. 
   
      Odeberte odkazy na **informace o** a **kontaktu** a místo toho odkaz na stránku **Students** , kterou vytvoříte.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. Uložte Web. Master.

## <a name="add-a-web-form-to-display-student-data"></a>Přidat webový formulář pro zobrazení dat studenta

   1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte položku **Přidat** a **Nová položka**. 
   
   2. V dialogovém okně **Přidat novou položku** vyberte **webový formulář se šablonou stránky předlohy** a pojmenujte ho **students. aspx**.

      ![vytvořit stránku](retrieving-data/_static/image5.png)

   3. Vyberte možnost **Přidat**.
   
   4. Pro stránku předlohy webového formuláře vyberte **site. Master**.
   
   5. Vyberte **OK**.

## <a name="add-the-data-model"></a>Přidání datového modelu

Ve složce **modely** přidejte třídu s názvem **UniversityModels.cs**.

   1. Klikněte pravým tlačítkem na **modely**, vyberte **Přidat**a **Nová položka**. Zobrazí se dialogové okno **Přidat novou položku**.

   2. V levém navigačním panelu vyberte **kód**a pak **Třída**.

      ![vytvořit třídu modelu](retrieving-data/_static/image20.png)

   3. Pojmenujte třídu **UniversityModels.cs** a vyberte **Přidat**.

      V tomto souboru definujte `SchoolContext` `Student` třídy,, a `Enrollment` `Course` následujícím způsobem:

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext`Třída je odvozena z `DbContext` , která spravuje připojení k databázi a změny v datech.

      Ve `Student` třídě si všimněte atributů použitých pro `FirstName` `LastName` vlastnosti, a `Year` . Tento kurz používá tyto atributy pro ověřování dat. Chcete-li zjednodušit kód, jsou označeny pouze tyto vlastnosti s atributy ověřování dat. Ve skutečném projektu byste použili atributy ověřování pro všechny vlastnosti, které vyžadují ověření.

   4. Uložte UniversityModels.cs.

## <a name="set-up-the-database-based-on-classes"></a>Nastavení databáze na základě tříd

V tomto kurzu se používá [migrace Code First](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) k vytváření objektů a tabulek databáze. Tyto tabulky obsahují informace o studentech a jejich kurzech.

   1. Vyberte **nástroje**  >  **Správce balíčků NuGet**  >  **Konzola správce balíčků**.

   2. V **konzole správce balíčků**spusťte tento příkaz:  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      Pokud se příkaz úspěšně dokončí, zobrazí se zpráva oznamující, že migrace byla povolena.

      ![Povolit migrace](retrieving-data/_static/image8.png)

      Všimněte si, že byl vytvořen soubor s názvem *Configuration.cs* . `Configuration`Třída obsahuje `Seed` metodu, která může předem naplnit tabulky databáze daty testů.

## <a name="pre-populate-the-database"></a>Předem naplnit databázi

   1. Otevřete Configuration.cs.
   
   2. Do metody `Seed` přidejte následující kód. Přidejte také `using` příkaz pro `ContosoUniversityModelBinding. Models` obor názvů.

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. Uložte Configuration.cs.

   4. V konzole správce balíčků spusťte příkaz **Add-Migration Initial**.

   5. Spusťte příkaz **Update-Database**.

      Pokud při spuštění tohoto příkazu dojde k výjimce, `StudentID` hodnoty a se `CourseID` mohou lišit od `Seed` hodnot metody. Otevřete tyto databázové tabulky a vyhledejte existující hodnoty pro `StudentID` a `CourseID` . Přidejte tyto hodnoty do kódu pro osazení `Enrollments` tabulky.

## <a name="add-a-gridview-control"></a>Přidání ovládacího prvku GridView

S vyplněnými daty databáze jste nyní připraveni načíst tato data a zobrazit je. 

1. Otevřete studenty. aspx.

2. Vyhledejte `MainContent` zástupný symbol. V rámci tohoto zástupného symbolu přidejte ovládací prvek **GridView** , který obsahuje tento kód.

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   Co je potřeba vzít v vědomí:
   * Všimněte si hodnoty nastavené pro `SelectMethod` vlastnost v prvku GridView. Tato hodnota určuje metodu použitou k načtení dat GridView, které vytvoříte v následujícím kroku. 
   
   * `ItemType`Vlastnost je nastavena na `Student` třídu vytvořenou dříve. Toto nastavení umožňuje odkazovat na vlastnosti třídy v kódu. `Student`Třída má například kolekci s názvem `Enrollments` . Můžete použít `Item.Enrollments` k načtení této kolekce a pak použít [syntaxi LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) k načtení součtu zaregistrovaných kreditů každého studenta.
   
3. Uložte studenty. aspx.

## <a name="add-code-to-retrieve-data"></a>Přidat kód pro načtení dat

   V souboru s kódem na pozadí pro studenty. aspx přidejte metodu určenou pro `SelectMethod` hodnotu. 
   
   1. Otevřete Students.aspx.cs.
   
   2. Přidejte `using` příkazy pro `ContosoUniversityModelBinding. Models` `System.Data.Entity` obory názvů a.

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. Přidejte metodu, kterou jste zadali pro `SelectMethod` :

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include`Klauzule vylepšuje výkon dotazů, ale není vyžadována. Bez `Include` klauzule se data načítají pomocí [*opožděného načítání*](https://en.wikipedia.org/wiki/Lazy_loading), což zahrnuje odeslání samostatného dotazu do databáze pokaždé, když se načtou související data. S klauzulí se data načítají `Include` pomocí *Eager načítání*, což znamená, že jeden databázový dotaz načte všechna související data. Pokud se související data nepoužívají, načítání Eager je méně efektivní, protože se načítají další data. V tomto případě ale Eager načítání poskytuje nejlepší výkon, protože související data se zobrazují pro každý záznam.

      Další informace o požadavcích na výkon při načítání souvisejících dat naleznete v části **opožděné, Eager a explicitní načítání souvisejících dat** v tématu [čtení souvisejících dat pomocí Entity Framework v článku aplikace ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) .

      Ve výchozím nastavení jsou data řazena podle hodnot vlastnosti označené jako klíč. Můžete přidat `OrderBy` klauzuli a zadat jinou hodnotu řazení. V tomto příkladu `StudentID` je použita výchozí vlastnost pro řazení. V článku [řazení, stránkování a filtrování dat](sorting-paging-and-filtering-data.md) je povoleno, aby uživatel mohl vybrat sloupec pro řazení.
 
   4. Uložte Students.aspx.cs.

## <a name="run-your-application"></a>Spusťte aplikaci 

Spusťte webovou aplikaci (**F5**) a přejděte na stránku **Students** , kde se zobrazí následující:

   ![Zobrazit data](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>Automatické generování metod vazby modelu

Při práci prostřednictvím této série kurzů můžete jednoduše zkopírovat kód z kurzu do projektu. Ale jednou z nevýhod tohoto přístupu je, že se nemůžete seznámit s funkcí poskytovanými aplikací Visual Studio a automaticky vygenerovat kód pro metody vazby modelu. Při práci na vašich vlastních projektech vám automatické generování kódu může ušetřit čas a pomohou vám získat představu o tom, jak implementovat operaci. Tato část popisuje funkci automatického generování kódu. Tato část je pouze informativní a neobsahuje žádný kód, který je třeba implementovat do projektu. 

Při nastavování hodnoty `SelectMethod` vlastností, `UpdateMethod` , `InsertMethod` nebo `DeleteMethod` v kódu značky můžete vybrat možnost **vytvořit novou metodu** .

![Vytvoření metody](retrieving-data/_static/image18.png)

Visual Studio nevytvoří pouze metodu v kódu na pozadí se správným podpisem, ale také generuje implementační kód pro provedení operace. Pokud nejprve nastavíte `ItemType` vlastnost před použitím funkce Automatické generování kódu, vygenerovaný kód použije tento typ pro operace. Například při nastavování `UpdateMethod` vlastnosti se automaticky vygeneruje následující kód:

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

Tento kód znovu není nutné přidat do projektu. V dalším kurzu implementujete metody pro aktualizaci, odstranění a přidávání nových dat.

## <a name="summary"></a>Souhrn

V tomto kurzu jste vytvořili třídy datového modelu a z těchto tříd vygenerovali databázi. Vyplnili jste tabulky databáze testovacími daty. Použili jste vazbu modelu k načtení dat z databáze a následně jste zobrazili data v prvku GridView.

V dalším [kurzu](updating-deleting-and-creating-data.md) tohoto seriálu povolíte aktualizaci, odstraňování a vytváření dat.

> [!div class="step-by-step"]
> [Další](updating-deleting-and-creating-data.md)
