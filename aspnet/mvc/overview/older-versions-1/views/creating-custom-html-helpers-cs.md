---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Vytváření vlastních pomocníků HTML (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC. Využitím HTML Pomocník ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542557"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="86a81-104">Vytvoření vlastních pomocných rutin HTML (C#)</span><span class="sxs-lookup"><span data-stu-id="86a81-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="86a81-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86a81-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="86a81-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="86a81-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="86a81-107">Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC.</span><span class="sxs-lookup"><span data-stu-id="86a81-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="86a81-108">Využitím nápovědy HTML můžete snížit množství únavného psaní značek HTML, které je nutné provést, abyste vytvořili standardní stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="86a81-109">Cílem tohoto kurzu je ukázat, jak můžete vytvořit vlastní html pomocníky, které můžete použít v zobrazení MVC.</span><span class="sxs-lookup"><span data-stu-id="86a81-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="86a81-110">Využitím nápovědy HTML můžete snížit množství únavného psaní značek HTML, které je nutné provést, abyste vytvořili standardní stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="86a81-111">V první části tohoto kurzu, jsem popsat některé ze stávajících HTML pomocníků součástí ASP.NET MVC framework.</span><span class="sxs-lookup"><span data-stu-id="86a81-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="86a81-112">Dále jsem popsat dvě metody vytváření vlastních HTML pomocníků: I vysvětlit, jak vytvořit vlastní HTML pomocníky vytvořením statické metody a vytvořením metody rozšíření.</span><span class="sxs-lookup"><span data-stu-id="86a81-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="86a81-113">Principy pomocníků HTML</span><span class="sxs-lookup"><span data-stu-id="86a81-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="86a81-114">Pomocník HTML je pouze metoda, která vrací řetězec.</span><span class="sxs-lookup"><span data-stu-id="86a81-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="86a81-115">Řetězec může představovat libovolný typ obsahu, který chcete.</span><span class="sxs-lookup"><span data-stu-id="86a81-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="86a81-116">Můžete například použít pomocné soubory HTML k `<input>` vykreslení standardních značek HTML, jako jsou HTML a `<img>` tagy.</span><span class="sxs-lookup"><span data-stu-id="86a81-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="86a81-117">Pomocí pomocníků HTML můžete také vykreslit složitější obsah, například proužka tabulátoru nebo tabulka HTML s daty databáze.</span><span class="sxs-lookup"><span data-stu-id="86a81-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="86a81-118">Rozhraní ASP.NET MVC obsahuje následující sadu standardních pomocníků HTML (nejedná se o úplný seznam):</span><span class="sxs-lookup"><span data-stu-id="86a81-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="86a81-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="86a81-119">Html.ActionLink()</span></span>
- <span data-ttu-id="86a81-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="86a81-120">Html.BeginForm()</span></span>
- <span data-ttu-id="86a81-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="86a81-121">Html.CheckBox()</span></span>
- <span data-ttu-id="86a81-122">Html.DropdownList()</span><span class="sxs-lookup"><span data-stu-id="86a81-122">Html.DropDownList()</span></span>
- <span data-ttu-id="86a81-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="86a81-123">Html.EndForm()</span></span>
- <span data-ttu-id="86a81-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="86a81-124">Html.Hidden()</span></span>
- <span data-ttu-id="86a81-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="86a81-125">Html.ListBox()</span></span>
- <span data-ttu-id="86a81-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="86a81-126">Html.Password()</span></span>
- <span data-ttu-id="86a81-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="86a81-127">Html.RadioButton()</span></span>
- <span data-ttu-id="86a81-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="86a81-128">Html.TextArea()</span></span>
- <span data-ttu-id="86a81-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="86a81-129">Html.TextBox()</span></span>

<span data-ttu-id="86a81-130">Zvažte například formulář v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="86a81-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="86a81-131">Tento formulář je vykreslen pomocí dvou standardních pomocníků HTML (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="86a81-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="86a81-132">Tento formulář `Html.BeginForm()` používá `Html.TextBox()` metody a Helper k vykreslení jednoduchého formuláře HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="86a81-133">[![Stránka vykreslená pomocí pomocných modulů HTML](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="86a81-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="86a81-134">**Obrázek 01**: Stránka vykreslená pomocí pomocných zařízení HTML[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-custom-html-helpers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="86a81-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="86a81-135">**Výpis 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="86a81-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="86a81-136">Metoda Html.BeginForm() Helper se používá k vytvoření `<form>` otevíracích a uzavíracích značek HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="86a81-137">Všimněte `Html.BeginForm()` si, že metoda je volána v rámci using prohlášení.</span><span class="sxs-lookup"><span data-stu-id="86a81-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="86a81-138">Příkaz using zajišťuje, `<form>` že značka se zavře na konci bloku using.</span><span class="sxs-lookup"><span data-stu-id="86a81-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="86a81-139">Pokud dáváte přednost, namísto vytvoření using block, můžete volat Html.EndForm() Helper metoda zavřít `<form>` značku.</span><span class="sxs-lookup"><span data-stu-id="86a81-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="86a81-140">Použijte podle toho, jaký přístup `<form>` k vytvoření otevírací a uzavírací značky, která se vám bude jevit jako nejintuitivnější.</span><span class="sxs-lookup"><span data-stu-id="86a81-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="86a81-141">Pomocné `Html.TextBox()` metody se používají v výpisu 1 k vykreslení značek HTML. `<input>`</span><span class="sxs-lookup"><span data-stu-id="86a81-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="86a81-142">Pokud vyberete zdroj zobrazení ve vašem prohlížeči, pak se zobrazí zdroj HTML v výpisu 2.</span><span class="sxs-lookup"><span data-stu-id="86a81-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="86a81-143">Všimněte si, že zdroj obsahuje standardní značky HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86a81-144">všimněte `Html.TextBox()`si, že pomocník -HTML je vykreslen pomocí `<%= %>` značek namísto `<% %>` značek.</span><span class="sxs-lookup"><span data-stu-id="86a81-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="86a81-145">Pokud nezahrnete znaménko rovná se, nic se do prohlížeče nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="86a81-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="86a81-146">Rozhraní ASP.NET MVC obsahuje malou sadu pomocníků.</span><span class="sxs-lookup"><span data-stu-id="86a81-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="86a81-147">S největší pravděpodobností budete muset rozšířit architekturu MVC o vlastní pomocné moduly HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="86a81-148">Ve zbývající části tohoto kurzu se naučíte dvě metody vytváření vlastních pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="86a81-149">**Výpis 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="86a81-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="86a81-150">Vytváření pomocníků HTML pomocí statických metod</span><span class="sxs-lookup"><span data-stu-id="86a81-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="86a81-151">Nejjednodušší způsob, jak vytvořit nový pomocník HTML, je vytvořit statickou metodu, která vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="86a81-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="86a81-152">Představte si například, že se rozhodnete vytvořit nový pomocník `<label>` HTML, který vykreslí značku HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="86a81-153">Třídu v výpisu 2 můžete `<label>` použít k vykreslení .</span><span class="sxs-lookup"><span data-stu-id="86a81-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="86a81-154">**Výpis 2 –`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="86a81-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="86a81-155">Na třídě v seznamu 2 není nic zvláštního.</span><span class="sxs-lookup"><span data-stu-id="86a81-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="86a81-156">Metoda `Label()` jednoduše vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="86a81-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="86a81-157">Upravené zobrazení indexu v seznamu `LabelHelper` 3 `<label>` používá k vykreslení značek HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="86a81-158">Všimněte si, `<%@ imports %>` že zobrazení obsahuje `Application1.Helpers` direktivu, která importuje obor názvů.</span><span class="sxs-lookup"><span data-stu-id="86a81-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="86a81-159">**Výpis 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="86a81-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="86a81-160">Vytváření pomocníků HTML pomocí rozšiřujících metod</span><span class="sxs-lookup"><span data-stu-id="86a81-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="86a81-161">Pokud chcete vytvořit HTML pomocníky, které fungují stejně jako standardní HTML pomocníky obsažené v ASP.NET mvc framework pak je třeba vytvořit metody rozšíření.</span><span class="sxs-lookup"><span data-stu-id="86a81-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="86a81-162">Rozšiřující metody umožňují přidat nové metody do existující třídy.</span><span class="sxs-lookup"><span data-stu-id="86a81-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="86a81-163">Při vytváření metody HTML Helper přidáte nové metody do třídy HtmlHelper reprezentované vlastností Html zobrazení.</span><span class="sxs-lookup"><span data-stu-id="86a81-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="86a81-164">Třída v listingu 3 přidá `HtmlHelper` metodu `Label()`rozšíření do třídy s názvem .</span><span class="sxs-lookup"><span data-stu-id="86a81-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="86a81-165">Existuje několik věcí, které byste si měli všimnout o této třídě.</span><span class="sxs-lookup"><span data-stu-id="86a81-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="86a81-166">Nejprve si všimněte, že třída je statickou třídou.</span><span class="sxs-lookup"><span data-stu-id="86a81-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="86a81-167">Je nutné definovat metodu rozšíření se statickou třídou.</span><span class="sxs-lookup"><span data-stu-id="86a81-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="86a81-168">Za druhé, všimněte si, že první `Label()` parametr `this`metody předchází klíčové slovo .</span><span class="sxs-lookup"><span data-stu-id="86a81-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="86a81-169">První parametr metody rozšíření označuje třídu, kterou rozšiřuje metoda rozšíření.</span><span class="sxs-lookup"><span data-stu-id="86a81-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="86a81-170">**Výpis 3 –`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="86a81-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="86a81-171">Po vytvoření metody rozšíření a sestavení aplikace úspěšně, metoda rozšíření se zobrazí v aplikaci Visual Studio Intellisense stejně jako všechny ostatní metody třídy (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="86a81-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="86a81-172">Jediným rozdílem je, že metody rozšíření se zobrazí se speciálním symbolem vedle nich (ikona šipky dolů).</span><span class="sxs-lookup"><span data-stu-id="86a81-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="86a81-173">[![Použití metody rozšíření Html.Label()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="86a81-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="86a81-174">**Obrázek 02**: Použití metody rozšíření Html.Label()[(Klepnutím zobrazíte obrázek v plné velikosti)](creating-custom-html-helpers-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="86a81-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="86a81-175">Upravené zobrazení indexu v seznamu 4 používá metodu rozšíření Html.Label() k vykreslení všech jeho `<label>` značek.</span><span class="sxs-lookup"><span data-stu-id="86a81-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="86a81-176">**Výpis 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="86a81-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="86a81-177">Souhrn</span><span class="sxs-lookup"><span data-stu-id="86a81-177">Summary</span></span>

<span data-ttu-id="86a81-178">V tomto kurzu jste se naučili dvě metody vytváření vlastních pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="86a81-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="86a81-179">Nejprve jste se naučili, jak vytvořit vlastní `Label()` nápovědu HTML vytvořením statické metody, která vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="86a81-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="86a81-180">Dále jste se dozvěděli, `Label()` jak vytvořit vlastní metodu nápovědy HTML vytvořením metody rozšíření ve `HtmlHelper` třídě.</span><span class="sxs-lookup"><span data-stu-id="86a81-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="86a81-181">V tomto tutoriálu jsem se zaměřil na budování velmi jednoduché metody HTML Helper.</span><span class="sxs-lookup"><span data-stu-id="86a81-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="86a81-182">Uvědomte si, že pomocník HTML může být tak složitý, jak chcete.</span><span class="sxs-lookup"><span data-stu-id="86a81-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="86a81-183">Můžete vytvářet pomocné soubory HTML, které vykreslují bohatý obsah, jako jsou stromová zobrazení, nabídky nebo tabulky databázových dat.</span><span class="sxs-lookup"><span data-stu-id="86a81-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86a81-184">[Předchozí](asp-net-mvc-views-overview-cs.md)
> [další](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="86a81-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
