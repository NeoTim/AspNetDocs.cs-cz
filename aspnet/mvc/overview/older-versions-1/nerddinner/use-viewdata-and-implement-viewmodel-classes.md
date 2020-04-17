---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: Použití tříd ViewData a Implementovat viewmodel | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 6 ukazuje, jak povolit podporu pro scénáře úprav bohatší formuláře a také popisuje dva přístupy, které lze použít k předávání dat z řadičů do zobrazení:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541101"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>Použití slovníku ViewData a implementace tříd ViewModel

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 6 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 6 ukazuje, jak povolit podporu pro scénáře úprav bohatší formulář a také popisuje dva přístupy, které lze použít k předání dat z řadičů do zobrazení: ViewData a ViewModel.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner Krok 6: ViewData a ViewModel

Probrali jsme řadu scénářů formulářových sloupů a diskutovali jsme o tom, jak implementovat podporu pro vytváření, aktualizaci a odstraňování (CRUD). Nyní budeme mít naše DinnersController implementace dále a povolit podporu pro bohatší scénáře úprav formulářů. Přitom budeme diskutovat o dva přístupy, které lze použít k předání dat z řadičů do zobrazení: ViewData a ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Předávání dat z řadičů do šablon zobrazení

Jednou z určujících charakteristik vzoru MVC je přísné "oddělení obav", které pomáhá prosazovat mezi různými součástmi aplikace. Modely, řadiče a zobrazení každý mají dobře definované role a odpovědnosti a komunikují mezi sebou dobře definovanými způsoby. To pomáhá podporovat testovatelnost a opětovné použití kódu.

Když Controller třída rozhodne vykreslit odpověď HTML zpět klientovi, je zodpovědný za explicitní předání do šablony zobrazení všechna data potřebná k vykreslení odpovědi. Zobrazit šablony by nikdy nemělprovádět žádné načítání dat nebo aplikační logiku – a místo toho by se měly omezit na pouze vykreslovací kód, který je řízen mimo model/data, která je mu předána řadičem.

Právě teď data modelu předávaná naší třídou DinnersController do našich šablon zobrazení je jednoduchá a přímočará – seznam objektů Dinner v případě Index(), a jeden objekt Dinner v případě Details(), Edit(), Create() a Delete(). Jak jsme se přidat další možnosti uživatelského práva do naší aplikace, jsme často bude muset předat více než jen tato data k vykreslení HTML odpovědi v rámci našich šablon zobrazení. Například můžeme chtít změnit pole "Země" v rámci našeho upravit a vytvořit zobrazení z bytí HTML textového pole na rozevírací seznam. Místo pevného kódu rozevíracího seznamu názvů zemí v šabloně zobrazení jej můžeme chtít vygenerovat ze seznamu podporovaných zemí, které naplníme dynamicky. Budeme potřebovat způsob, jak předat objekt Dinner *a* seznam podporovaných zemí z našeho řadiče do našich šablon zobrazení.

Podívejme se na dva způsoby, jak toho dosáhnout.

### <a name="using-the-viewdata-dictionary"></a>Použití slovníku ViewData

Základní třída řadiče zpřístupňuje vlastnost slovníku "ViewData", kterou lze použít k předání dalších datových položek z řadičů do zobrazení.

Například pro podporu scénáře, kde chceme změnit textové pole "Země" v našem zobrazení úprav z textového pole HTML na rozevírací seznam, můžeme aktualizovat naši metodu akce Edit() tak, aby předala (kromě objektu Dinner) objekt SelectList, který lze použít jako model rozevíracího seznamu zemí.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

Konstruktor výše selectlist přijímá seznam okresů k naplnění rozevíracího seznamu s, stejně jako aktuálně vybranou hodnotu.

Poté můžeme aktualizovat naši šablonu zobrazení Edit.aspx tak, aby používala pomocnou metodu Html.DropDownList() namísto pomocné metody Html.TextBox(), kterou jsme použili dříve:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

Html.DropDownList() pomocná metoda výše trvá dva parametry. První je název prvku formuláře HTML pro výstup. Druhým je model "SelectList", který jsme předali prostřednictvím slovníku ViewData. Používáme c# "as" klíčové slovo přetypovat typ ve slovníku jako SelectList.

A teď, když spustíme naši aplikaci a přístup */ Večeře / Edit / 1* URL v našem prohlížeči uvidíme, že naše upravit UI byla aktualizována zobrazit rozevírací seznam zemí namísto textového pole:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

Vzhledem k tomu, že také vykreslujeme šablonu upravit zobrazení z metody HTTP-POST Edit (ve scénářích, kdy dojde k chybám), chceme se ujistit, že tuto metodu aktualizujeme také tak, abychom přidali SelectList do ViewData, když je šablona zobrazení vykreslena v chybových scénářích:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

A teď náš scénář úprav DinnersController podporuje DropDownList.

### <a name="using-a-viewmodel-pattern"></a>Použití vzoru ViewModel

Přístup slovníku ViewData má tu výhodu, že je poměrně rychlý a snadno implementovat. Někteří vývojáři však nemají rádi použití slovníků založených na řetězecích, protože překlepy mohou vést k chybám, které nebudou zachyceny v době kompilace. Netypový ViewData slovník také vyžaduje použití operátoru "as" nebo přetypování při použití jazyka silného typu, jako je C# v šabloně zobrazení.

Alternativní přístup, který bychom mohli použít, je jeden často označovány jako "ViewModel" vzor. Při použití tohoto vzoru vytvoříme třídy silného typu, které jsou optimalizovány pro naše konkrétní scénáře zobrazení a které zveřejňují vlastnosti dynamických hodnot nebo obsahu, které naše šablony zobrazení potřebují. Naše třídy kontroleru pak můžete naplnit a předat tyto třídy optimalizované pro zobrazení do naší šablony zobrazení použít. To umožňuje bezpečnost typů, kontrolu v době kompilace a editor intellisense v rámci šablony zobrazení.

Chcete-li například povolit scénáře úprav formuláře večeři, můžeme vytvořit třídu "DinnerFormViewModel", jako je níže, která zveřejňuje dvě vlastnosti silného typu: objekt Dinner a model SelectList potřebný k naplnění rozevíracího seznamu zemí:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Můžeme pak aktualizovat naše Edit() metoda akce k vytvoření DinnerFormViewModel pomocí Dinner objektu načteme z našeho úložiště a pak předat do našeho zobrazení šablony:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Šablonu zobrazení pak aktualizujeme tak, aby očekávala místo objektu "DinnerFormViewModel" místo objektu "Dinner" změnou atributu "inherits" v horní části stránky edit.aspx takto:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Jakmile to uděláme, intellisense vlastnosti "Model" v rámci naší šablony zobrazení budou aktualizovány tak, aby odrážely objektový model typu DinnerFormViewModel jsme předávání:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Poté můžeme aktualizovat náš kód zobrazení, abychom ho vyřešili. Všimněte si, jak nejsme měnit názvy vstupních prvků, které vytváříme (prvky formuláře bude stále s názvem "Název", "Země") – ale aktualizujeme HTML Helper metody načíst hodnoty pomocí DinnerFormViewModel třídy:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Budeme také aktualizovat naše Upravit post metoda použít DinnerFormViewModel třídy při vykreslování chyby:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Můžeme také aktualizovat naše Create() metody akce znovu použít přesně stejnou *třídu DinnerFormViewModel* povolit země DropDownList v rámci těchto také. Níže je implementace HTTP-GET:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

Níže je implementace metody HTTP-POST Create:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

A nyní obě naše obrazovky Pro úpravy a vytváření podporují rozevírací seznamy pro výběr země.

### <a name="custom-shaped-viewmodel-classes"></a>Třídy ViewModel ve tvaru vlastního tvaru

Ve výše uvedeném scénáři naše DinnerFormViewModel třídy přímo zpřístupňuje Dinner objekt modelu jako vlastnost, spolu s podpůrnou SelectList vlastnost modelu. Tento přístup funguje v pořádku pro scénáře, kde uživatelské okno HTML, které chceme vytvořit v rámci naší šablony zobrazení, odpovídá relativně úzce našim objektům modelu domény.

Pro scénáře, kde tomu tak není, je jednou z možností, kterou můžete použít, vytvoření třídy ViewModel ve tvaru vlastního tvaru, jejíž objektový model je optimalizován pro spotřebu podle zobrazení – a která může vypadat zcela odlišně od základního objektu modelu domény. Například může potenciálně vystavit názvy různých vlastností nebo agregační vlastnosti shromážděné z více objektů modelu.

Vlastní ve tvaru ViewModel třídy lze použít jak k předání dat z řadičů do zobrazení k vykreslení, stejně jako ke zpracování dat formuláře zaúčtované zpět do metody akce řadiče. V tomto pozdějším scénáři může být metoda akce aktualizovat objekt ViewModel s daty zaúčtovaných formulářem a potom pomocí instance ViewModel mapovat nebo načíst skutečný objekt modelu domény.

Vlastní ve tvaru ViewModel třídy může poskytnout velkou flexibilitu a jsou něco prozkoumat pokaždé, když najdete kód vykreslování v rámci šablony zobrazení nebo kód vysílání formuláře uvnitř metody akce začíná příliš komplikované. To je často známkou toho, že vaše modely domény neodpovídají čistě uživatelskému uživatelskému uživatelskému uživatelskému nastavení, které generujete, a že může pomoci zprostředkující třída ViewModel ve tvaru vlastního tvaru.

### <a name="next-step"></a>Další krok

Podívejme se teď na to, jak můžeme použít částečné a vzorové stránky k opětovnému použití a sdílení ui v celé naší aplikaci.

> [!div class="step-by-step"]
> [Předchozí](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [další](re-use-ui-using-master-pages-and-partials.md)
