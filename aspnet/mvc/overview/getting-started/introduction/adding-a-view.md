---
title: Přidání zobrazení do aplikace MVC
author: Rick-Anderson
description: Přidání zobrazení do aplikace MVC
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045010"
---
# <a name="adding-a-view"></a>Přidání zobrazení

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

V této části se chystáte upravit `HelloWorldController` třídu, aby používala soubory šablon zobrazení k čistě zapouzdření procesu generování odpovědí HTML na klienta. 

Vytvoříte soubor šablony zobrazení pomocí [zobrazovacího modulu Razor](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md). Šablony zobrazení založené na Razor mají příponu *. cshtml* a poskytují elegantní způsob, jak vytvořit výstup HTML pomocí C#. Razor minimalizuje počet znaků a klávesových úhozů, které jsou požadovány při psaní šablony zobrazení, a umožňuje rychlý a rychlejší pracovní postup kódování.

V současné době `Index` metoda vrací řetězec se zprávou, která je pevně zakódována ve třídě Controller. Změňte `Index` metodu pro volání metody [zobrazení](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) Controllers, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

`Index`Výše uvedená metoda používá šablonu zobrazení k vygenerování odpovědi HTML do prohlížeče. Metody kontroleru (známé také jako [metody akcí](http://rachelappel.com/asp.net-mvc-actionresults-explained)), jako je `Index` výše uvedená metoda, obecně vracejí [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (nebo třídu odvozenou z [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), nikoli primitivní typy jako řetězec.

Klikněte pravým tlačítkem na složku *Views\HelloWorld* a pak klikněte na **Přidat**a potom na **stránku zobrazení MVC 5 s rozložením (Razor)**.
  
![](adding-a-view/_static/image1.png)   
  
V dialogovém okně **Zadejte název pro položku** zadejte *index*a pak klikněte na **OK**.  
  
![](adding-a-view/_static/image2.png)  
  
V dialogu **Vybrat rozložení stránky** přijměte výchozí nastavení ** \_ layout. cshtml** a klikněte na tlačítko **OK**.  
  
![](adding-a-view/_static/image3.png)  
  
V dialogovém okně výše se v levém podokně vybere složka *Views\Shared* . Pokud máte vlastní soubor rozložení v jiné složce, můžete ho vybrat. Později v tomto kurzu budeme mluvit o souboru rozložení.

Vytvoří se soubor *MvcMovie\Views\HelloWorld\Index.cshtml* .

![](adding-a-view/_static/image4.png)

Přidejte následující zvýrazněný kód.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

Klikněte pravým tlačítkem na soubor *index. cshtml* a vyberte **Zobrazit v prohlížeči**.

![PI](adding-a-view/_static/image5.png)

Můžete také kliknout pravým tlačítkem na soubor *index. cshtml* a vybrat **Zobrazit v okně Kontrola stránky.** Další informace najdete v [kurzu inspektora stránky](../../views/using-page-inspector-in-aspnet-mvc.md) .

Případně spusťte aplikaci a přejděte k `HelloWorld` řadiči ( `http://localhost:xxxx/HelloWorld` ). `Index`Metoda v řadiči neudělala spoustu práce. jednoduše spustil příkaz `return View()` , který určuje, že metoda má použít soubor šablony zobrazení k vykreslení odpovědi do prohlížeče. Vzhledem k tomu, že jste explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení *index. cshtml* ve složce *\Views\HelloWorld* . Následující obrázek ukazuje řetězec &quot; Hello z naší šablony zobrazení! &quot; pevně zakódovaný v zobrazení.

![](adding-a-view/_static/image6.png)

Vypadá poměrně dobrý. Všimněte si ale, že v záhlaví prohlížeče se zobrazuje "index – moje aplikace ASP.NET" a velký odkaz v horní části stránky říká "název aplikace". V závislosti na tom, jak malé okno prohlížeče nastavíte, možná budete muset kliknout na tři pruhy v pravém horním rohu, abyste viděli odkazy na **domovskou stránku**, **informace o** **kontaktech**, **registraci** a **přihlášení** .

## <a name="changing-views-and-layout-pages"></a>Změna zobrazení a stránek rozložení

Nejdříve je třeba změnit &quot; odkaz na název aplikace &quot; v horní části stránky. Tento text je společný pro každou stránku. V projektu se v současnosti implementuje jenom v jednom místě, i když se objeví na každé stránce aplikace. Přejít do složky */views/Shared* v **Průzkumník řešení** a otevřete soubor * \_ layout. cshtml* . Tento soubor se nazývá *Stránka rozložení* a je ve sdílené složce, kterou používají všechny ostatní stránky.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Šablony rozložení umožňují určit rozložení kontejneru HTML webu na jednom místě a pak ho použít na více stránek na webu. Najděte `@RenderBody()` řádek. `RenderBody` je zástupný symbol, ve kterém se zobrazí všechny stránky specifické pro zobrazení, &quot; zabalené na &quot; stránce rozložení. Pokud například vyberete odkaz **o** , zobrazení *Views\Home\About.cshtml* se vykreslí uvnitř `RenderBody` metody.

Změňte obsah elementu title. Změňte [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) v šabloně rozložení z &quot; názvu aplikace &quot; na &quot; video MVC &quot; a kontroler z `Home` na `Movies` . Úplný soubor rozložení je zobrazený níže:

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

Spusťte aplikaci a Všimněte si, že nyní říká &quot; film MVC &quot; . Klikněte na odkaz **informace** a uvidíte, jak tato stránka zobrazuje &quot; film MVC &quot; . Tuto změnu jsme dokázali udělat v šabloně rozložení a všechny stránky na webu odrážejí nový název.

![](adding-a-view/_static/image8.png)

Při prvním vytvoření souboru *Views\HelloWorld\Index.cshtml* obsahuje následující kód:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Výše uvedený kód Razor explicitně nastavuje stránku rozložení. Prověřte *zobrazení \\ _ViewStart souboru. cshtml* , obsahuje přesně stejný kód Razor. *[Zobrazení \\ _ViewStart souboru. cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* definuje společné rozložení, které budou používat všechna zobrazení, takže můžete odkomentovat nebo odebrat tento kód ze souboru *Views\HelloWorld\Index.cshtml* .

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

Vlastnost můžete použít `Layout` k nastavení jiného zobrazení rozložení nebo k jeho nastavení na, `null` takže nebude použit žádný soubor rozložení.

Teď změníme název zobrazení indexu.

Otevřete *MvcMovie\Views\HelloWorld\Index.cshtml*. Existují dvě místa pro provedení změny: nejprve text zobrazený v názvu prohlížeče a potom v sekundární hlavičce ( `<h2>` element). Mírně se mírně liší, abyste viděli, který bit kódu se změní v rámci aplikace.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

Chcete-li určit, který název HTML se má zobrazit, kód výše nastaví `Title` vlastnost `ViewBag` objektu (která je v šabloně zobrazení *index. cshtml* ). Všimněte si, že šablona rozložení ( *Views\Shared \\ _Layout. cshtml* ) používá tuto hodnotu v `<title>` prvku jako součást `<head>` oddílu HTML, kterou jsme předtím změnili.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

Pomocí tohoto `ViewBag` přístupu můžete snadno předat další parametry mezi šablonou zobrazení a vaším souborem rozložení.

Aplikaci spusťte. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. (Pokud nevidíte změny v prohlížeči, můžete zobrazit obsah uložený v mezipaměti. Stisknutím kombinace kláves CTRL + F5 v prohlížeči vynutíte načtení odpovědi ze serveru.) Název prohlížeče se vytvoří se sadou, kterou `ViewBag.Title` jsme nastavili v šabloně zobrazení *index. cshtml* a &quot; aplikaci další film &quot; přidanou v souboru rozložení.

Všimněte si také, jak byl obsah v šabloně zobrazení *index. cshtml* sloučen se šablonou zobrazení * \_ . cshtml* a byla odeslána jedna odpověď HTML do prohlížeče. Šablony rozložení umožňují snadno provádět změny, které se vztahují na všechny stránky aplikace.

![](adding-a-view/_static/image9.png)

Naším malým množstvím &quot; dat &quot; (v tomto případě &quot; Hello z naší šablony zobrazení! &quot; zpráva) je pevně zakódováno, i když. Aplikace MVC má &quot; v &quot; (zobrazení) a současně máte &quot; C &quot; (Controller), ale ne &quot; M &quot; (model). Za chvíli vám ukážeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-data-from-the-controller-to-the-view"></a>Předávání dat z kontroleru do zobrazení

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o předávání informací z kontroleru do zobrazení. Třídy kontroleru jsou vyvolány v reakci na příchozí požadavek adresy URL. Třída kontroleru je místo, kde píšete kód, který zpracovává příchozí požadavky prohlížeče, načítá data z databáze a nakonec rozhoduje o tom, jaký typ reakce se má poslat zpátky do prohlížeče. Šablony zobrazení se pak dají použít z kontroleru k vygenerování a formátování odpovědi HTML do prohlížeče.

Řadiče jsou zodpovědné za poskytnutí jakýchkoli dat nebo objektů, aby mohla šablona zobrazení vykreslovat odpověď do prohlížeče. Osvědčeným postupem: **Šablona zobrazení by nikdy neměla provádět obchodní logiku ani pracovat s databází přímo**. Místo toho by šablona zobrazení měla fungovat jenom s daty, která mu poskytl kontroler. Udržování tohoto &quot; oddělení obav &quot; pomáhá udržet vyčištění kódu, testovatelné a udržovatelnější.

V současné době `Welcome` Metoda Action ve `HelloWorldController` třídě přebírá `name` a `numTimes` parametr a následně výstup hodnot přímo do prohlížeče. Místo toho, aby kontroler tuto odpověď vygeneroval jako řetězec, změňte místo toho kontroler tak, aby používal šablonu zobrazení. Šablona zobrazení vygeneruje dynamickou odpověď, což znamená, že před vygenerováním odpovědi musíte předat příslušné bity dat z kontroleru do zobrazení. To můžete provést tak, že řadič umístí dynamická data (parametry), která šablona zobrazení potřebuje, do `ViewBag` objektu, ke kterému může přistupovat šablona zobrazení.

Vraťte se do souboru *HelloWorldController.cs* a změňte `Welcome` metodu tak, aby se do objektu přidala `Message` `NumTimes` hodnota a `ViewBag` . `ViewBag` je dynamický objekt, což znamená, že můžete do něj umístit cokoli, co chcete. `ViewBag` objekt nemá žádné definované vlastnosti, dokud do něj nevložíte nějaký text. [Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry ( `name` a `numTimes` ) z řetězce dotazu v adresním řádku na parametry v metodě. Úplný soubor *HelloWorldController.cs* vypadá takto:

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

Objekt nyní `ViewBag` obsahuje data, která budou automaticky předána do zobrazení. Dále potřebujete šablonu zobrazení Vítejte! V nabídce **sestavení** vyberte **Sestavit řešení** (nebo CTRL + SHIFT + B) a ujistěte se, že je projekt kompilován. Klikněte pravým tlačítkem na složku *Views\HelloWorld* a pak klikněte na **Přidat**a potom na **stránku zobrazení MVC 5 s rozložením (Razor)**.
  
![](adding-a-view/_static/image10.png)   
  
V dialogovém okně **Zadejte název pro položku** zadejte *Welcome*a pak klikněte na **OK**.   
  
V dialogu **Vybrat rozložení stránky** přijměte výchozí nastavení ** \_ layout. cshtml** a klikněte na tlačítko **OK**.  
  
![](adding-a-view/_static/image11.png)   

Vytvoří se soubor *MvcMovie\Views\HelloWorld\Welcome.cshtml* .

Nahraďte značku v souboru *Welcome. cshtml* . Vytvoříte smyčku, která říká &quot; Hello tolikrát, &quot; kolikrát by měl uživatel vyjadřovat. Úplný soubor *Welcome. cshtml* je uveden níže.

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

Spusťte aplikaci a přejděte na následující adresu URL:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Nyní se data z adresy URL předávají do kontroleru pomocí [pořadače modelů](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx). Kontroler zabalí data do `ViewBag` objektu a předá tento objekt zobrazení. Zobrazení pak zobrazí data jako HTML pro uživatele.

![](adding-a-view/_static/image12.png)

V ukázce výše jsme pomocí `ViewBag` objektu předávali data z kontroleru do zobrazení. Později v tomto kurzu použijeme model zobrazení k předání dat z kontroleru do zobrazení. Přístup k modelu zobrazení pro předávání dat je obecně mnohem upřednostňovaný nad přístupem k balíčku zobrazení. Další informace najdete v [zobrazeních dynamického typu](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) položky blogu. 

Dobře, to bylo druh &quot; M &quot; pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-controller.md) 
>  [Další](adding-a-model.md)
