---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: Ověřování v rozhraní IDataErrorInfo (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Stephen Walther se dozvíte, jak zobrazit chybové zprávy ověření na vlastních implementací rozhraní IDataErrorInfo v třídě modelu.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117561"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="04bc7-103">Ověřování v rozhraní IDataErrorInfo (C#)</span><span class="sxs-lookup"><span data-stu-id="04bc7-103">Validating with the IDataErrorInfo Interface (C#)</span></span>

<span data-ttu-id="04bc7-104">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="04bc7-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="04bc7-105">Stephen Walther se dozvíte, jak zobrazit chybové zprávy ověření na vlastních implementací rozhraní IDataErrorInfo v třídě modelu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="04bc7-106">Cílem tohoto kurzu je vysvětlit jedním z přístupů k provedení ověření v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="04bc7-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="04bc7-107">Zjistíte, jak zabránit odeslání formuláře HTML bez zadání hodnot požadovaných polí.</span><span class="sxs-lookup"><span data-stu-id="04bc7-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="04bc7-108">V tomto kurzu se dozvíte, jak provádět ověření pomocí rozhraní IErrorDataInfo.</span><span class="sxs-lookup"><span data-stu-id="04bc7-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="04bc7-109">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="04bc7-109">Assumptions</span></span>

<span data-ttu-id="04bc7-110">V tomto kurzu použiju MoviesDB databáze a tabulky databáze filmů.</span><span class="sxs-lookup"><span data-stu-id="04bc7-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="04bc7-111">Tato tabulka obsahuje následující sloupce:</span><span class="sxs-lookup"><span data-stu-id="04bc7-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>

| <span data-ttu-id="04bc7-112">**Název sloupce**</span><span class="sxs-lookup"><span data-stu-id="04bc7-112">**Column Name**</span></span> | <span data-ttu-id="04bc7-113">**Datový typ**</span><span class="sxs-lookup"><span data-stu-id="04bc7-113">**Data Type**</span></span> | <span data-ttu-id="04bc7-114">**Povolit hodnoty Null**</span><span class="sxs-lookup"><span data-stu-id="04bc7-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04bc7-115">ID</span><span class="sxs-lookup"><span data-stu-id="04bc7-115">Id</span></span> | <span data-ttu-id="04bc7-116">Int</span><span class="sxs-lookup"><span data-stu-id="04bc7-116">Int</span></span> | <span data-ttu-id="04bc7-117">False</span><span class="sxs-lookup"><span data-stu-id="04bc7-117">False</span></span> |
| <span data-ttu-id="04bc7-118">Název</span><span class="sxs-lookup"><span data-stu-id="04bc7-118">Title</span></span> | <span data-ttu-id="04bc7-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="04bc7-119">Nvarchar(100)</span></span> | <span data-ttu-id="04bc7-120">False</span><span class="sxs-lookup"><span data-stu-id="04bc7-120">False</span></span> |
| <span data-ttu-id="04bc7-121">Ředitel</span><span class="sxs-lookup"><span data-stu-id="04bc7-121">Director</span></span> | <span data-ttu-id="04bc7-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="04bc7-122">Nvarchar(100)</span></span> | <span data-ttu-id="04bc7-123">False</span><span class="sxs-lookup"><span data-stu-id="04bc7-123">False</span></span> |
| <span data-ttu-id="04bc7-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="04bc7-124">DateReleased</span></span> | <span data-ttu-id="04bc7-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="04bc7-125">DateTime</span></span> | <span data-ttu-id="04bc7-126">False</span><span class="sxs-lookup"><span data-stu-id="04bc7-126">False</span></span> |

<span data-ttu-id="04bc7-127">V tomto kurzu pomocí Microsoft Entity Framework vytvořit Moje databáze třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="04bc7-128">Třída film vygenerovaným rozhraním Entity Framework se zobrazí na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="04bc7-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="04bc7-129">[![Video entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="04bc7-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="04bc7-130">**Obrázek 01**: Movie entity ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="04bc7-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="04bc7-131">Další informace o použití rozhraní Entity Framework pro generování tříd modelu vaší databáze najdete v tématu Moje kurz s názvem vytváření tříd modelu s použitím rozhraní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="04bc7-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="04bc7-132">Třída Kontroleru</span><span class="sxs-lookup"><span data-stu-id="04bc7-132">The Controller Class</span></span>

<span data-ttu-id="04bc7-133">Používáme kontroler Home na filmy seznamu a vytvořit nové filmy.</span><span class="sxs-lookup"><span data-stu-id="04bc7-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="04bc7-134">Kód pro tuto třídu je obsažen v informacích 1.</span><span class="sxs-lookup"><span data-stu-id="04bc7-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="04bc7-135">**Výpis 1 - Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="04bc7-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="04bc7-136">Třída kontroleru Domovská stránka v informacích 1 obsahuje dvě Create() akce.</span><span class="sxs-lookup"><span data-stu-id="04bc7-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="04bc7-137">První akci zobrazí formulář HTML pro vytvoření nové video.</span><span class="sxs-lookup"><span data-stu-id="04bc7-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="04bc7-138">Druhou akci Create() provádí skutečné vložit tento nový film do databáze.</span><span class="sxs-lookup"><span data-stu-id="04bc7-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="04bc7-139">Druhou akci Create() je voláno, když se odešle formulář zobrazí první Create() akcí na server.</span><span class="sxs-lookup"><span data-stu-id="04bc7-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="04bc7-140">Všimněte si, že druhou akci Create() obsahuje následující řádky kódu:</span><span class="sxs-lookup"><span data-stu-id="04bc7-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="04bc7-141">Vlastnost IsValid vrátí hodnotu false, když dojde k chybě ověřování.</span><span class="sxs-lookup"><span data-stu-id="04bc7-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="04bc7-142">V takovém případě se zobrazí znovu vytvořit zobrazení, která obsahuje formulář HTML pro vytváření videa.</span><span class="sxs-lookup"><span data-stu-id="04bc7-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="04bc7-143">Vytvoření částečné třídy</span><span class="sxs-lookup"><span data-stu-id="04bc7-143">Creating a Partial Class</span></span>

<span data-ttu-id="04bc7-144">Třída Video je vygenerovaným rozhraním Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="04bc7-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="04bc7-145">Pokud rozbalte soubor MoviesDBModel.edmx v okně Průzkumník řešení a otevřete soubor MoviesDBModel.Designer.cs v editoru kódu vidíte kód pro třídu Movie (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="04bc7-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="04bc7-146">[![Kód pro entitu Movie](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="04bc7-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="04bc7-147">**Obrázek 02**: Kód pro entitu Movie ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="04bc7-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>

<span data-ttu-id="04bc7-148">Třída Video je částečnou třídu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-148">The Movie class is a partial class.</span></span> <span data-ttu-id="04bc7-149">To znamená, že můžeme přidat jiné částečné třídy se stejným názvem k rozšíření funkčnosti film třídy.</span><span class="sxs-lookup"><span data-stu-id="04bc7-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="04bc7-150">Přidáme náš logiku ověřování novou třídu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="04bc7-151">Přidáte třídu v informacích 2 do složky modely.</span><span class="sxs-lookup"><span data-stu-id="04bc7-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="04bc7-152">**Výpis 2 - Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="04bc7-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="04bc7-153">Všimněte si, že třída v informacích 2 zahrnuje *částečné* modifikátor.</span><span class="sxs-lookup"><span data-stu-id="04bc7-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="04bc7-154">Jakékoliv metody nebo vlastnosti, které přidáte do této třídy, se stanou součástí třídy film vygenerovaným rozhraním Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="04bc7-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="04bc7-155">Přidání OnChanging a OnChanged částečné metody</span><span class="sxs-lookup"><span data-stu-id="04bc7-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="04bc7-156">Když Entity Frameworku vygeneruje třídu entity, Entity Framework přidá částečné metody do třídy automaticky.</span><span class="sxs-lookup"><span data-stu-id="04bc7-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="04bc7-157">Entity Framework generuje OnChanging a OnChanged částečné metody, které odpovídají každá vlastnost třídy.</span><span class="sxs-lookup"><span data-stu-id="04bc7-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="04bc7-158">V případě třídy film Entity Framework vytvoří následující metody:</span><span class="sxs-lookup"><span data-stu-id="04bc7-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="04bc7-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="04bc7-159">OnIdChanging</span></span>
- <span data-ttu-id="04bc7-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="04bc7-160">OnIdChanged</span></span>
- <span data-ttu-id="04bc7-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="04bc7-161">OnTitleChanging</span></span>
- <span data-ttu-id="04bc7-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="04bc7-162">OnTitleChanged</span></span>
- <span data-ttu-id="04bc7-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="04bc7-163">OnDirectorChanging</span></span>
- <span data-ttu-id="04bc7-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="04bc7-164">OnDirectorChanged</span></span>
- <span data-ttu-id="04bc7-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="04bc7-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="04bc7-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="04bc7-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="04bc7-167">Před změnou odpovídající vlastnosti je volána metoda OnChanging vpravo.</span><span class="sxs-lookup"><span data-stu-id="04bc7-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="04bc7-168">Po změně vlastnosti je volána metoda OnChanged vpravo.</span><span class="sxs-lookup"><span data-stu-id="04bc7-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="04bc7-169">Můžete využít výhod těchto částečné metody třídy film přidat logiku ověřování.</span><span class="sxs-lookup"><span data-stu-id="04bc7-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="04bc7-170">Aktualizace třídy filmu v informacích 3 ověřuje, že nadpis a ředitel pro vlastnosti se přiřazují neprázdných hodnot.</span><span class="sxs-lookup"><span data-stu-id="04bc7-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="04bc7-171">Částečná metoda je metoda definovaná ve třídě, není nutná pro implementaci.</span><span class="sxs-lookup"><span data-stu-id="04bc7-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="04bc7-172">Pokud není implementovat částečnou metodu kompilátor odebere podpis metody a všechny volání metody tady nejsou žádné běhové náklady spojené s částečnou metodu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="04bc7-173">V editoru Visual Studio Code, můžete přidat částečná metoda zadáním klíčového slova *částečné* následovaný mezerami, chcete-li zobrazit seznam částečných zobrazení k implementaci.</span><span class="sxs-lookup"><span data-stu-id="04bc7-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="04bc7-174">**Výpis 3 - Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="04bc7-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="04bc7-175">Například pokud se pokusíte přiřadit vlastnosti název prázdný řetězec, chybovou zprávu přiřadí se mu na slovník s názvem \_chyby.</span><span class="sxs-lookup"><span data-stu-id="04bc7-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="04bc7-176">V tomto okamžiku nic ve skutečnosti se stane, když přiřadíte prázdný řetězec pro vlastnost názvu a chyba se přidá do soukromého \_pole chyby.</span><span class="sxs-lookup"><span data-stu-id="04bc7-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="04bc7-177">Musíme implementovat v rozhraní IDataErrorInfo umožní vystavit tyto chyby ověření do rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="04bc7-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="04bc7-178">Implementace rozhraní IDataErrorInfo</span><span class="sxs-lookup"><span data-stu-id="04bc7-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="04bc7-179">V rozhraní IDataErrorInfo byl součástí rozhraní .NET framework od první verze.</span><span class="sxs-lookup"><span data-stu-id="04bc7-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="04bc7-180">Toto rozhraní je velmi jednoduché rozhraní:</span><span class="sxs-lookup"><span data-stu-id="04bc7-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="04bc7-181">Pokud třída implementuje rozhraní IDataErrorInfo, rozhraní ASP.NET MVC bude používat toto rozhraní, při vytváření instance třídy.</span><span class="sxs-lookup"><span data-stu-id="04bc7-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="04bc7-182">Například kontroler Home Create() akce přijímá instanci třídy filmu:</span><span class="sxs-lookup"><span data-stu-id="04bc7-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="04bc7-183">Architektura ASP.NET MVC vytvoří instanci film předán Create() akce pomocí vazače modelu (DefaultModelBinder).</span><span class="sxs-lookup"><span data-stu-id="04bc7-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="04bc7-184">Vazač modelu zodpovídá za vytvoření instance objektu film navázáním pole formuláře HTML na instanci objektu video.</span><span class="sxs-lookup"><span data-stu-id="04bc7-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="04bc7-185">DefaultModelBinder zjišťuje, zda třída implementuje rozhraní IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="04bc7-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="04bc7-186">Pokud třída implementuje toto rozhraní vazače modelu vyvolá IDataErrorInfo.this indexeru pro každou vlastnost třídy.</span><span class="sxs-lookup"><span data-stu-id="04bc7-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="04bc7-187">Pokud indexeru vrátí chybovou zprávu přidá vazač modelu tato chybová zpráva pro modelování stav automaticky.</span><span class="sxs-lookup"><span data-stu-id="04bc7-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="04bc7-188">DefaultModelBinder také kontroluje IDataErrorInfo.Error vlastnost.</span><span class="sxs-lookup"><span data-stu-id="04bc7-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="04bc7-189">Tato vlastnost je určena k reprezentaci chyby ověřování podle jiné vlastnosti přidružené k třídě.</span><span class="sxs-lookup"><span data-stu-id="04bc7-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="04bc7-190">Můžete například chtít vynutit ověřovací pravidlo, které závisí na hodnotách více vlastností třídy Video.</span><span class="sxs-lookup"><span data-stu-id="04bc7-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="04bc7-191">V takovém případě by vrátit chybu ověření z vlastnosti chyby.</span><span class="sxs-lookup"><span data-stu-id="04bc7-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="04bc7-192">Aktualizované třídy filmu v informacích 4 implementuje rozhraní IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="04bc7-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="04bc7-193">**Část 4 – Models\Movie.cs (implementuje IDataErrorInfo)**</span><span class="sxs-lookup"><span data-stu-id="04bc7-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="04bc7-194">V informacích 4 kontroluje vlastnost indexeru \_předaný kolekce chyb, pokud obsahuje klíč, který odpovídá názvu vlastnosti indexeru.</span><span class="sxs-lookup"><span data-stu-id="04bc7-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="04bc7-195">Pokud se nezobrazí žádná chyba ověření přidružený k vlastnosti je vrácen prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="04bc7-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="04bc7-196">Není nutné upravovat kontroler Home žádným způsobem pomocí upravené třídy film.</span><span class="sxs-lookup"><span data-stu-id="04bc7-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="04bc7-197">Stránky zobrazené na obrázku 3 znázorňuje, co se stane, když je zadána žádná hodnota pro název nebo ředitel pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="04bc7-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="04bc7-198">[![Automatické vytváření metody akce](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="04bc7-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="04bc7-199">**Obrázek 03**: Formulář s chybějící hodnoty ([kliknutím ji zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="04bc7-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>

<span data-ttu-id="04bc7-200">Všimněte si, že hodnota DateReleased proběhne automaticky.</span><span class="sxs-lookup"><span data-stu-id="04bc7-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="04bc7-201">Protože vlastnost DateReleased nepřijímá hodnoty NULL, DefaultModelBinder Chyba ověřování pro tuto vlastnost automaticky při vygeneruje nemá hodnotu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="04bc7-202">Pokud chcete upravit chybové zprávy pro vlastnost DateReleased budete muset vytvořit vlastní vazač modelu.</span><span class="sxs-lookup"><span data-stu-id="04bc7-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="04bc7-203">Souhrn</span><span class="sxs-lookup"><span data-stu-id="04bc7-203">Summary</span></span>

<span data-ttu-id="04bc7-204">V tomto kurzu jste zjistili, jak používat rozhraní IDataErrorInfo ke generování chybových zpráv ověření.</span><span class="sxs-lookup"><span data-stu-id="04bc7-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="04bc7-205">Nejprve jsme vytvořili částečné třídy film, který rozšiřuje funkce částečné třídy film vygenerovaným rozhraním Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="04bc7-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="04bc7-206">Dále jsme přidali logiku ověřování k film třídy OnTitleChanging() OnDirectorChanging() částečné metody a.</span><span class="sxs-lookup"><span data-stu-id="04bc7-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="04bc7-207">Nakonec jsme implementovali v rozhraní IDataErrorInfo aby bylo možné zveřejnit tyto zprávy ověření na rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="04bc7-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04bc7-208">[Předchozí](performing-simple-validation-cs.md)
> [další](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="04bc7-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>
