---
title: Pomocných rutin značek ve formulářích v ASP.NET Core
author: rick-anderson
description: Popisuje předdefinované pomocných rutin značek použít s formuláři.
ms.author: riande
ms.custom: mvc
ms.date: 1/11/2019
uid: mvc/views/working-with-forms
ms.openlocfilehash: cd15c641fbf702071bd57510a1d51737f6ab8e19
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068536"
---
# <a name="tag-helpers-in-forms-in-aspnet-core"></a><span data-ttu-id="cb55a-103">Pomocných rutin značek ve formulářích v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cb55a-103">Tag Helpers in forms in ASP.NET Core</span></span>

<span data-ttu-id="cb55a-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT), [Dave Paquette](https://twitter.com/Dave_Paquette), a [Jerrie Pelser](https://github.com/jerriep)</span><span class="sxs-lookup"><span data-stu-id="cb55a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Dave Paquette](https://twitter.com/Dave_Paquette), and [Jerrie Pelser](https://github.com/jerriep)</span></span>

<span data-ttu-id="cb55a-105">Tento dokument vysvětluje práce s formuláři a elementů HTML běžně používají na formuláři.</span><span class="sxs-lookup"><span data-stu-id="cb55a-105">This document demonstrates working with Forms and the HTML elements commonly used on a Form.</span></span> <span data-ttu-id="cb55a-106">Kód HTML [formuláře](https://www.w3.org/TR/html401/interact/forms.html) element poskytuje primární mechanismus webové aplikace využívají k odesílání dat zpět na server.</span><span class="sxs-lookup"><span data-stu-id="cb55a-106">The HTML [Form](https://www.w3.org/TR/html401/interact/forms.html) element provides the primary mechanism web apps use to post back data to the server.</span></span> <span data-ttu-id="cb55a-107">Většina tento dokument popisuje [pomocných rutin značek](tag-helpers/intro.md) a jak se vám může pomoci produktivně vytvářet robustní formuláře HTML.</span><span class="sxs-lookup"><span data-stu-id="cb55a-107">Most of this document describes [Tag Helpers](tag-helpers/intro.md) and how they can help you productively create robust HTML forms.</span></span> <span data-ttu-id="cb55a-108">Doporučujeme si přečíst [Úvod do pomocné rutiny značek](tag-helpers/intro.md) předtím, než čtete tento dokument.</span><span class="sxs-lookup"><span data-stu-id="cb55a-108">We recommend you read [Introduction to Tag Helpers](tag-helpers/intro.md) before you read this document.</span></span>

<span data-ttu-id="cb55a-109">V mnoha případech pomocných rutin HTML poskytnout alternativní způsob konkrétní pomocné rutiny značky, ale je důležité uvědomit si, že pomocné rutiny značek nemáte nahradit pomocné rutiny HTML a není k dispozici pomocné rutiny značky pro každý pomocné rutiny HTML.</span><span class="sxs-lookup"><span data-stu-id="cb55a-109">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers don't replace HTML Helpers and there's not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="cb55a-110">Pokud existuje alternativní pomocné rutiny HTML, je uvedený.</span><span class="sxs-lookup"><span data-stu-id="cb55a-110">When an HTML Helper alternative exists, it's mentioned.</span></span>

<a name="my-asp-route-param-ref-label"></a>

## <a name="the-form-tag-helper"></a><span data-ttu-id="cb55a-111">Pomocná rutina značky formuláře</span><span class="sxs-lookup"><span data-stu-id="cb55a-111">The Form Tag Helper</span></span>

<span data-ttu-id="cb55a-112">[Formuláře](https://www.w3.org/TR/html401/interact/forms.html) pomocné rutiny značky:</span><span class="sxs-lookup"><span data-stu-id="cb55a-112">The [Form](https://www.w3.org/TR/html401/interact/forms.html) Tag Helper:</span></span>

* <span data-ttu-id="cb55a-113">Generuje kód HTML [ \<formulář >](https://www.w3.org/TR/html401/interact/forms.html) `action` hodnota atributu pro akce řadiče MVC nebo pojmenovanou trasu</span><span class="sxs-lookup"><span data-stu-id="cb55a-113">Generates the HTML [\<FORM>](https://www.w3.org/TR/html401/interact/forms.html) `action` attribute value for a MVC controller action or named route</span></span>

* <span data-ttu-id="cb55a-114">Vytváří skrytý [tokenu pro ověření žádosti](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) paděláním požadavku mezi weby (při použití s `[ValidateAntiForgeryToken]` atributu v metodě akce HTTP Post)</span><span class="sxs-lookup"><span data-stu-id="cb55a-114">Generates a hidden [Request Verification Token](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) to prevent cross-site request forgery (when used with the `[ValidateAntiForgeryToken]` attribute in the HTTP Post action method)</span></span>

* <span data-ttu-id="cb55a-115">Poskytuje `asp-route-<Parameter Name>` atribut, ve kterém `<Parameter Name>` se přidá do hodnoty trasy.</span><span class="sxs-lookup"><span data-stu-id="cb55a-115">Provides the `asp-route-<Parameter Name>` attribute, where `<Parameter Name>` is added to the route values.</span></span> <span data-ttu-id="cb55a-116">`routeValues` Parametry `Html.BeginForm` a `Html.BeginRouteForm` poskytuje podobné funkce.</span><span class="sxs-lookup"><span data-stu-id="cb55a-116">The  `routeValues` parameters to `Html.BeginForm` and `Html.BeginRouteForm` provide similar functionality.</span></span>

* <span data-ttu-id="cb55a-117">Má alternativu pomocné rutiny HTML `Html.BeginForm` a `Html.BeginRouteForm`</span><span class="sxs-lookup"><span data-stu-id="cb55a-117">Has an HTML Helper alternative `Html.BeginForm` and `Html.BeginRouteForm`</span></span>

<span data-ttu-id="cb55a-118">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-118">Sample:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/RegisterFormOnly.cshtml)]

<span data-ttu-id="cb55a-119">Pomocná rutina formuláře značky výše uvedené vytvoří následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-119">The Form Tag Helper above generates the following HTML:</span></span>

```HTML
<form method="post" action="/Demo/Register">
    <!-- Input and Submit elements -->
    <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

<span data-ttu-id="cb55a-120">Generuje modul runtime pro MVC `action` hodnotu atributu z atributů pomocné rutiny značky formuláře `asp-controller` a `asp-action`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-120">The MVC runtime generates the `action` attribute value from the Form Tag Helper attributes `asp-controller` and `asp-action`.</span></span> <span data-ttu-id="cb55a-121">Pomocná rutina značky formuláře také vytváří skrytý [tokenu pro ověření žádosti](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) paděláním požadavku mezi weby (při použití s `[ValidateAntiForgeryToken]` atributu v metodě akce HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="cb55a-121">The Form Tag Helper also generates a hidden [Request Verification Token](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) to prevent cross-site request forgery (when used with the `[ValidateAntiForgeryToken]` attribute in the HTTP Post action method).</span></span> <span data-ttu-id="cb55a-122">Ochrana proti padělání žádosti více webů čistě formuláře HTML je obtížné, pomocné rutiny značky formuláře poskytuje tato služba za vás.</span><span class="sxs-lookup"><span data-stu-id="cb55a-122">Protecting a pure HTML Form from cross-site request forgery is difficult, the Form Tag Helper provides this service for you.</span></span>

### <a name="using-a-named-route"></a><span data-ttu-id="cb55a-123">Pomocí pojmenovanou trasu</span><span class="sxs-lookup"><span data-stu-id="cb55a-123">Using a named route</span></span>

<span data-ttu-id="cb55a-124">`asp-route` Pomocné rutiny značky atribut může také generovat značky HTML `action` atribut.</span><span class="sxs-lookup"><span data-stu-id="cb55a-124">The `asp-route` Tag Helper attribute can also generate markup for the HTML `action` attribute.</span></span> <span data-ttu-id="cb55a-125">Aplikaci se službou [trasy](../../fundamentals/routing.md) s názvem `register` použít následující kód pro registrační stránky:</span><span class="sxs-lookup"><span data-stu-id="cb55a-125">An app with a [route](../../fundamentals/routing.md)  named `register` could use the following markup for the registration page:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterRoute.cshtml)]

<span data-ttu-id="cb55a-126">Počet zobrazení v *zobrazení/účet* složky (vygeneruje, když vytvoříte novou webovou aplikaci s *jednotlivé uživatelské účty*) obsahují [asp. trasa returnurl](xref:mvc/views/working-with-forms) atribut:</span><span class="sxs-lookup"><span data-stu-id="cb55a-126">Many of the views in the *Views/Account* folder (generated when you create a new web app with *Individual User Accounts*) contain the [asp-route-returnurl](xref:mvc/views/working-with-forms) attribute:</span></span>

```cshtml
<form asp-controller="Account" asp-action="Login"
     asp-route-returnurl="@ViewData["ReturnUrl"]"
     method="post" class="form-horizontal" role="form">
```

>[!NOTE]
><span data-ttu-id="cb55a-127">Pomocí integrované šablony `returnUrl` se jenom vyplní automaticky při pokusu o přístup k autorizovaným prostředků, ale nejsou ověřeny nebo oprávnění.</span><span class="sxs-lookup"><span data-stu-id="cb55a-127">With the built in templates, `returnUrl` is only populated automatically when you try to access an authorized resource but are not authenticated or authorized.</span></span> <span data-ttu-id="cb55a-128">Při pokusu o neoprávněný přístup, middleware zabezpečení vás přesměruje na přihlašovací stránku s `returnUrl` nastavit.</span><span class="sxs-lookup"><span data-stu-id="cb55a-128">When you attempt an unauthorized access, the security middleware redirects you to the login page with the `returnUrl` set.</span></span>

## <a name="the-input-tag-helper"></a><span data-ttu-id="cb55a-129">Pomocná rutina vstupní značky</span><span class="sxs-lookup"><span data-stu-id="cb55a-129">The Input Tag Helper</span></span>

<span data-ttu-id="cb55a-130">Sváže vstupní pomocné rutiny značky HTML [ \<vstupní >](https://www.w3.org/wiki/HTML/Elements/input) element modelu výrazu v zobrazení syntaxe razor.</span><span class="sxs-lookup"><span data-stu-id="cb55a-130">The Input Tag Helper binds an HTML [\<input>](https://www.w3.org/wiki/HTML/Elements/input) element to a model expression in your razor view.</span></span>

<span data-ttu-id="cb55a-131">Syntaxe:</span><span class="sxs-lookup"><span data-stu-id="cb55a-131">Syntax:</span></span>

```HTML
<input asp-for="<Expression Name>" />
```

<span data-ttu-id="cb55a-132">Pomocná rutina vstupní značky:</span><span class="sxs-lookup"><span data-stu-id="cb55a-132">The Input Tag Helper:</span></span>

* <span data-ttu-id="cb55a-133">Generuje `id` a `name` atributy HTML pro název výraz zadaný v `asp-for` atribut.</span><span class="sxs-lookup"><span data-stu-id="cb55a-133">Generates the `id` and `name` HTML attributes for the expression name specified in the `asp-for` attribute.</span></span> <span data-ttu-id="cb55a-134">`asp-for="Property1.Property2"` je ekvivalentní `m => m.Property1.Property2`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-134">`asp-for="Property1.Property2"` is equivalent to `m => m.Property1.Property2`.</span></span> <span data-ttu-id="cb55a-135">Název výrazu se používá pro `asp-for` hodnotu atributu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-135">The name of the expression is what is used for the `asp-for` attribute value.</span></span> <span data-ttu-id="cb55a-136">Zobrazit [názvy výrazů](#expression-names) části Další informace.</span><span class="sxs-lookup"><span data-stu-id="cb55a-136">See the [Expression names](#expression-names) section for additional information.</span></span>

* <span data-ttu-id="cb55a-137">Nastaví kód HTML `type` atribut hodnotu podle typu modelu a [dat. Poznámka](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) atributy použité na vlastnost modelu</span><span class="sxs-lookup"><span data-stu-id="cb55a-137">Sets the HTML `type` attribute value based on the model type and  [data annotation](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes applied to the model property</span></span>

* <span data-ttu-id="cb55a-138">Nedojde k přepsání HTML `type` když je zadaná hodnota atributu</span><span class="sxs-lookup"><span data-stu-id="cb55a-138">Won't overwrite the HTML `type` attribute value when one is specified</span></span>

* <span data-ttu-id="cb55a-139">Generuje [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) atributy ověření ze [dat. Poznámka](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) atributy použité na vlastnosti modelu</span><span class="sxs-lookup"><span data-stu-id="cb55a-139">Generates [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5)  validation attributes from [data annotation](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes applied to model properties</span></span>

* <span data-ttu-id="cb55a-140">Obsahuje funkci pomocné rutiny HTML, které se překrývají s `Html.TextBoxFor` a `Html.EditorFor`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-140">Has an HTML Helper feature overlap with `Html.TextBoxFor` and `Html.EditorFor`.</span></span> <span data-ttu-id="cb55a-141">Zobrazit **alternativy pomocné rutiny HTML pro pomocné rutiny značky vstup** podrobné informace.</span><span class="sxs-lookup"><span data-stu-id="cb55a-141">See the **HTML Helper alternatives to Input Tag Helper** section for details.</span></span>

* <span data-ttu-id="cb55a-142">Poskytuje silné typování.</span><span class="sxs-lookup"><span data-stu-id="cb55a-142">Provides strong typing.</span></span> <span data-ttu-id="cb55a-143">Pokud název změny vlastností a vy nechcete aktualizovat pomocné rutiny značky získáte chybu podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="cb55a-143">If the name of the property changes and you don't update the Tag Helper you'll get an error similar to the following:</span></span>

```HTML
An error occurred during the compilation of a resource required to process
this request. Please review the following specific error details and modify
your source code appropriately.

Type expected
 'RegisterViewModel' does not contain a definition for 'Email' and no
 extension method 'Email' accepting a first argument of type 'RegisterViewModel'
 could be found (are you missing a using directive or an assembly reference?)
```

<span data-ttu-id="cb55a-144">`Input` Nastaví pomocné rutiny značky HTML `type` atribut založený na typ .NET.</span><span class="sxs-lookup"><span data-stu-id="cb55a-144">The `Input` Tag Helper sets the HTML `type` attribute based on the .NET type.</span></span> <span data-ttu-id="cb55a-145">Následující tabulka uvádí některé běžné typy .NET a generovaný typ HTML (ne každý typ formátu .NET je uvedena).</span><span class="sxs-lookup"><span data-stu-id="cb55a-145">The following table lists some common .NET types and generated HTML type (not every .NET type is listed).</span></span>

|<span data-ttu-id="cb55a-146">Typ formátu .NET</span><span class="sxs-lookup"><span data-stu-id="cb55a-146">.NET type</span></span>|<span data-ttu-id="cb55a-147">Typ vstupu</span><span class="sxs-lookup"><span data-stu-id="cb55a-147">Input Type</span></span>|
|---|---|
|<span data-ttu-id="cb55a-148">Bool</span><span class="sxs-lookup"><span data-stu-id="cb55a-148">Bool</span></span>|<span data-ttu-id="cb55a-149">type="checkbox"</span><span class="sxs-lookup"><span data-stu-id="cb55a-149">type="checkbox"</span></span>|
|<span data-ttu-id="cb55a-150">String</span><span class="sxs-lookup"><span data-stu-id="cb55a-150">String</span></span>|<span data-ttu-id="cb55a-151">type="text"</span><span class="sxs-lookup"><span data-stu-id="cb55a-151">type="text"</span></span>|
|<span data-ttu-id="cb55a-152">DateTime</span><span class="sxs-lookup"><span data-stu-id="cb55a-152">DateTime</span></span>|<span data-ttu-id="cb55a-153">type=["datetime-local"](https://developer.mozilla.org/docs/Web/HTML/Element/input/datetime-local)</span><span class="sxs-lookup"><span data-stu-id="cb55a-153">type=["datetime-local"](https://developer.mozilla.org/docs/Web/HTML/Element/input/datetime-local)</span></span>|
|<span data-ttu-id="cb55a-154">Byte</span><span class="sxs-lookup"><span data-stu-id="cb55a-154">Byte</span></span>|<span data-ttu-id="cb55a-155">typ = "cislo"</span><span class="sxs-lookup"><span data-stu-id="cb55a-155">type="number"</span></span>|
|<span data-ttu-id="cb55a-156">Int</span><span class="sxs-lookup"><span data-stu-id="cb55a-156">Int</span></span>|<span data-ttu-id="cb55a-157">typ = "cislo"</span><span class="sxs-lookup"><span data-stu-id="cb55a-157">type="number"</span></span>|
|<span data-ttu-id="cb55a-158">Jednoduché, Double</span><span class="sxs-lookup"><span data-stu-id="cb55a-158">Single, Double</span></span>|<span data-ttu-id="cb55a-159">typ = "cislo"</span><span class="sxs-lookup"><span data-stu-id="cb55a-159">type="number"</span></span>|


<span data-ttu-id="cb55a-160">V následující tabulce jsou uvedeny některé běžné [anotacemi dat](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) atributy, které pomocné rutiny vstupní značky se mapují na konkrétní typy vstupu (ne každý atribut ověření je uvedená):</span><span class="sxs-lookup"><span data-stu-id="cb55a-160">The following table shows some common [data annotations](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes that the input tag helper will map to specific input types (not every validation attribute is listed):</span></span>


|<span data-ttu-id="cb55a-161">Atribut</span><span class="sxs-lookup"><span data-stu-id="cb55a-161">Attribute</span></span>|<span data-ttu-id="cb55a-162">Typ vstupu</span><span class="sxs-lookup"><span data-stu-id="cb55a-162">Input Type</span></span>|
|---|---|
|<span data-ttu-id="cb55a-163">[EmailAddress]</span><span class="sxs-lookup"><span data-stu-id="cb55a-163">[EmailAddress]</span></span>|<span data-ttu-id="cb55a-164">type="email"</span><span class="sxs-lookup"><span data-stu-id="cb55a-164">type="email"</span></span>|
|<span data-ttu-id="cb55a-165">[Url]</span><span class="sxs-lookup"><span data-stu-id="cb55a-165">[Url]</span></span>|<span data-ttu-id="cb55a-166">type="url"</span><span class="sxs-lookup"><span data-stu-id="cb55a-166">type="url"</span></span>|
|<span data-ttu-id="cb55a-167">[HiddenInput]</span><span class="sxs-lookup"><span data-stu-id="cb55a-167">[HiddenInput]</span></span>|<span data-ttu-id="cb55a-168">typ = "skrytá"</span><span class="sxs-lookup"><span data-stu-id="cb55a-168">type="hidden"</span></span>|
|<span data-ttu-id="cb55a-169">[Phone]</span><span class="sxs-lookup"><span data-stu-id="cb55a-169">[Phone]</span></span>|<span data-ttu-id="cb55a-170">type="tel"</span><span class="sxs-lookup"><span data-stu-id="cb55a-170">type="tel"</span></span>|
|<span data-ttu-id="cb55a-171">[DataType(DataType.Password)]</span><span class="sxs-lookup"><span data-stu-id="cb55a-171">[DataType(DataType.Password)]</span></span>| <span data-ttu-id="cb55a-172">type="password"</span><span class="sxs-lookup"><span data-stu-id="cb55a-172">type="password"</span></span>|
|<span data-ttu-id="cb55a-173">[DataType(DataType.Date)]</span><span class="sxs-lookup"><span data-stu-id="cb55a-173">[DataType(DataType.Date)]</span></span>| <span data-ttu-id="cb55a-174">type="date"</span><span class="sxs-lookup"><span data-stu-id="cb55a-174">type="date"</span></span>|
|<span data-ttu-id="cb55a-175">[DataType(DataType.Time)]</span><span class="sxs-lookup"><span data-stu-id="cb55a-175">[DataType(DataType.Time)]</span></span>| <span data-ttu-id="cb55a-176">type="time"</span><span class="sxs-lookup"><span data-stu-id="cb55a-176">type="time"</span></span>|


<span data-ttu-id="cb55a-177">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-177">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/RegisterViewModel.cs)]

[!code-HTML[](working-with-forms/sample/final/Views/Demo/RegisterInput.cshtml)]

<span data-ttu-id="cb55a-178">Výše uvedený kód generuje následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-178">The code above generates the following HTML:</span></span>

```HTML
  <form method="post" action="/Demo/RegisterInput">
       Email:
       <input type="email" data-val="true"
              data-val-email="The Email Address field is not a valid email address."
              data-val-required="The Email Address field is required."
              id="Email" name="Email" value="" /> <br>
       Password:
       <input type="password" data-val="true"
              data-val-required="The Password field is required."
              id="Password" name="Password" /><br>
       <button type="submit">Register</button>
     <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
   </form>
```

<span data-ttu-id="cb55a-179">Datové poznámky u `Email` a `Password` vlastnosti generovat metadata v modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-179">The data annotations applied to the `Email` and `Password` properties generate metadata on the model.</span></span> <span data-ttu-id="cb55a-180">Pomocná rutina značky vstup využívá metadat modelu a vytváří [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-val-*` atributy (viz [ověření modelu](../models/validation.md)).</span><span class="sxs-lookup"><span data-stu-id="cb55a-180">The Input Tag Helper consumes the model metadata and produces [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-val-*` attributes (see [Model Validation](../models/validation.md)).</span></span> <span data-ttu-id="cb55a-181">Tyto atributy popisují validátory pro připojení k vstupních polí.</span><span class="sxs-lookup"><span data-stu-id="cb55a-181">These attributes describe the validators to attach to the input fields.</span></span> <span data-ttu-id="cb55a-182">To umožňuje nerušivý HTML5 a [jQuery](https://jquery.com/) ověření.</span><span class="sxs-lookup"><span data-stu-id="cb55a-182">This provides unobtrusive HTML5 and [jQuery](https://jquery.com/) validation.</span></span> <span data-ttu-id="cb55a-183">Nerušivý atributy mají formát `data-val-rule="Error Message"`, kde pravidlo je název ověřovacího pravidla (třeba `data-val-required`, `data-val-email`, `data-val-maxlength`atd.) Pokud chybová zpráva v atributu se zobrazí jako hodnota `data-val-rule` atribut.</span><span class="sxs-lookup"><span data-stu-id="cb55a-183">The unobtrusive attributes have the format `data-val-rule="Error Message"`, where rule is the name of the validation rule (such as `data-val-required`, `data-val-email`, `data-val-maxlength`, etc.) If an error message is provided in the attribute, it's displayed as the value for the `data-val-rule` attribute.</span></span> <span data-ttu-id="cb55a-184">Existují také atributy ve formátu `data-val-ruleName-argumentName="argumentValue"` , které poskytují další informace o pravidle, třeba `data-val-maxlength-max="1024"` .</span><span class="sxs-lookup"><span data-stu-id="cb55a-184">There are also attributes of the form `data-val-ruleName-argumentName="argumentValue"` that provide additional details about the rule, for example, `data-val-maxlength-max="1024"` .</span></span>

### <a name="html-helper-alternatives-to-input-tag-helper"></a><span data-ttu-id="cb55a-185">Alternativy pomocné rutiny HTML pro pomocné rutiny značky vstup</span><span class="sxs-lookup"><span data-stu-id="cb55a-185">HTML Helper alternatives to Input Tag Helper</span></span>

<span data-ttu-id="cb55a-186">`Html.TextBox`, `Html.TextBoxFor`, `Html.Editor` a `Html.EditorFor` překrývat funkcí pomocné rutiny značky vstup.</span><span class="sxs-lookup"><span data-stu-id="cb55a-186">`Html.TextBox`, `Html.TextBoxFor`, `Html.Editor` and `Html.EditorFor` have overlapping features with the Input Tag Helper.</span></span> <span data-ttu-id="cb55a-187">Pomocná rutina značky vstup automaticky nastaví `type` atribut; `Html.TextBox` a `Html.TextBoxFor` nebude.</span><span class="sxs-lookup"><span data-stu-id="cb55a-187">The Input Tag Helper will automatically set the `type` attribute; `Html.TextBox` and `Html.TextBoxFor` won't.</span></span> <span data-ttu-id="cb55a-188">`Html.Editor` a `Html.EditorFor` zpracování kolekce komplexních objektů a šablon; není pomocné rutiny značky vstup.</span><span class="sxs-lookup"><span data-stu-id="cb55a-188">`Html.Editor` and `Html.EditorFor` handle collections, complex objects and templates; the Input Tag Helper doesn't.</span></span> <span data-ttu-id="cb55a-189">Pomocná rutina značky vstup `Html.EditorFor` a `Html.TextBoxFor` jsou silného typu (používají výrazy lambda); `Html.TextBox` a `Html.Editor` nejsou (používají názvy výrazů).</span><span class="sxs-lookup"><span data-stu-id="cb55a-189">The Input Tag Helper, `Html.EditorFor`  and  `Html.TextBoxFor` are strongly typed (they use lambda expressions); `Html.TextBox` and `Html.Editor` are not (they use expression names).</span></span>

### <a name="htmlattributes"></a><span data-ttu-id="cb55a-190">HtmlAttributes</span><span class="sxs-lookup"><span data-stu-id="cb55a-190">HtmlAttributes</span></span>

<span data-ttu-id="cb55a-191">`@Html.Editor()` a `@Html.EditorFor()` použít speciální `ViewDataDictionary` položku s názvem `htmlAttributes` při provádění jejich výchozích šablon.</span><span class="sxs-lookup"><span data-stu-id="cb55a-191">`@Html.Editor()` and `@Html.EditorFor()` use a special `ViewDataDictionary` entry named `htmlAttributes` when executing their default templates.</span></span> <span data-ttu-id="cb55a-192">Toto chování je volitelně rozšířeno pomocí `additionalViewData` parametry.</span><span class="sxs-lookup"><span data-stu-id="cb55a-192">This behavior is optionally augmented using `additionalViewData` parameters.</span></span> <span data-ttu-id="cb55a-193">Klíč "htmlAttributes" je velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="cb55a-193">The key "htmlAttributes" is case-insensitive.</span></span> <span data-ttu-id="cb55a-194">Klíč "htmlAttributes" probíhá podobně jako `htmlAttributes` objekt předaný k zadání pomocných rutin, jako je `@Html.TextBox()`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-194">The key "htmlAttributes" is handled similarly to the `htmlAttributes` object passed to input helpers like `@Html.TextBox()`.</span></span>

```HTML
@Html.EditorFor(model => model.YourProperty, 
  new { htmlAttributes = new { @class="myCssClass", style="Width:100px" } })
```

### <a name="expression-names"></a><span data-ttu-id="cb55a-195">Názvy výrazů</span><span class="sxs-lookup"><span data-stu-id="cb55a-195">Expression names</span></span>

<span data-ttu-id="cb55a-196">`asp-for` Hodnota atributu je `ModelExpression` a pravou stranu výrazu lambda.</span><span class="sxs-lookup"><span data-stu-id="cb55a-196">The `asp-for` attribute value is a `ModelExpression` and the right hand side of a lambda expression.</span></span> <span data-ttu-id="cb55a-197">Proto `asp-for="Property1"` stane `m => m.Property1` ve vygenerovaném kódu, což je důvod, proč není nutné použijte předponu `Model`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-197">Therefore, `asp-for="Property1"` becomes `m => m.Property1` in the generated code which is why you don't need to prefix with `Model`.</span></span> <span data-ttu-id="cb55a-198">Můžete použít "\@" znak spuštění vložený výraz a před přesunout `m.`:</span><span class="sxs-lookup"><span data-stu-id="cb55a-198">You can use the "\@" character to start an inline expression and move before the `m.`:</span></span>

```HTML
@{
       var joe = "Joe";
   }
   <input asp-for="@joe" />
```

<span data-ttu-id="cb55a-199">Generuje následující:</span><span class="sxs-lookup"><span data-stu-id="cb55a-199">Generates the following:</span></span>

```HTML
<input type="text" id="joe" name="joe" value="Joe" />
```

<span data-ttu-id="cb55a-200">S vlastnostmi kolekce `asp-for="CollectionProperty[23].Member"` generuje stejný název jako `asp-for="CollectionProperty[i].Member"` při `i` má hodnotu `23`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-200">With collection properties, `asp-for="CollectionProperty[23].Member"` generates the same name as `asp-for="CollectionProperty[i].Member"` when `i` has the value `23`.</span></span>

<span data-ttu-id="cb55a-201">Když ASP.NET Core MVC vypočítá hodnotu `ModelExpression`, zkontroluje několik zdrojů, včetně `ModelState`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-201">When ASP.NET Core MVC calculates the value of `ModelExpression`, it inspects several sources, including `ModelState`.</span></span> <span data-ttu-id="cb55a-202">Vezměte v úvahu `<input type="text" asp-for="@Name" />`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-202">Consider `<input type="text" asp-for="@Name" />`.</span></span> <span data-ttu-id="cb55a-203">Vypočítané `value` atribut je první nenulová hodnota z:</span><span class="sxs-lookup"><span data-stu-id="cb55a-203">The calculated `value` attribute is the first non-null value from:</span></span>

* <span data-ttu-id="cb55a-204">`ModelState` Položka s klíčem "Name".</span><span class="sxs-lookup"><span data-stu-id="cb55a-204">`ModelState` entry with key "Name".</span></span>
* <span data-ttu-id="cb55a-205">Výsledek výrazu `Model.Name`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-205">Result of the expression `Model.Name`.</span></span>

### <a name="navigating-child-properties"></a><span data-ttu-id="cb55a-206">Podřízené vlastnosti navigace</span><span class="sxs-lookup"><span data-stu-id="cb55a-206">Navigating child properties</span></span>

<span data-ttu-id="cb55a-207">Můžete také přejít na podřízené vlastnosti pomocí cesta k vlastnosti zobrazení modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-207">You can also navigate to child properties using the property path of the view model.</span></span> <span data-ttu-id="cb55a-208">Vezměte v úvahu složitější třídu modelu, která obsahuje podřízenou `Address` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="cb55a-208">Consider a more complex model class that contains a child `Address` property.</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/AddressViewModel.cs?highlight=1,2,3,4&range=5-8)]

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/RegisterAddressViewModel.cs?highlight=8&range=5-13)]

<span data-ttu-id="cb55a-209">V zobrazení, můžeme vytvořit vazbu k `Address.AddressLine1`:</span><span class="sxs-lookup"><span data-stu-id="cb55a-209">In the view, we bind to `Address.AddressLine1`:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterAddress.cshtml?highlight=6)]

<span data-ttu-id="cb55a-210">Následující kód HTML je generován pro `Address.AddressLine1`:</span><span class="sxs-lookup"><span data-stu-id="cb55a-210">The following HTML is generated for `Address.AddressLine1`:</span></span>

```HTML
<input type="text" id="Address_AddressLine1" name="Address.AddressLine1" value="" />
```

### <a name="expression-names-and-collections"></a><span data-ttu-id="cb55a-211">Názvy výrazů a kolekce</span><span class="sxs-lookup"><span data-stu-id="cb55a-211">Expression names and Collections</span></span>

<span data-ttu-id="cb55a-212">Ukázkový model obsahující pole `Colors`:</span><span class="sxs-lookup"><span data-stu-id="cb55a-212">Sample, a model containing an array of `Colors`:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/Person.cs?highlight=3&range=5-10)]

<span data-ttu-id="cb55a-213">Metoda akce:</span><span class="sxs-lookup"><span data-stu-id="cb55a-213">The action method:</span></span>

```csharp
public IActionResult Edit(int id, int colorIndex)
   {
       ViewData["Index"] = colorIndex;
       return View(GetPerson(id));
   }
```

<span data-ttu-id="cb55a-214">Následující syntaxe Razor ukazuje, jak získat přístup k určitému `Color` element:</span><span class="sxs-lookup"><span data-stu-id="cb55a-214">The following Razor shows how you access a specific `Color` element:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/EditColor.cshtml)]

<span data-ttu-id="cb55a-215">*Views/Shared/EditorTemplates/String.cshtml* šablony:</span><span class="sxs-lookup"><span data-stu-id="cb55a-215">The *Views/Shared/EditorTemplates/String.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/String.cshtml)]

<span data-ttu-id="cb55a-216">Ukázkový používání `List<T>`:</span><span class="sxs-lookup"><span data-stu-id="cb55a-216">Sample using `List<T>`:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/ToDoItem.cs?range=3-8)]

<span data-ttu-id="cb55a-217">Následující syntaxe Razor ukazuje, jak k iteraci v kolekci:</span><span class="sxs-lookup"><span data-stu-id="cb55a-217">The following Razor shows how to iterate over a collection:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/Edit.cshtml)]

<span data-ttu-id="cb55a-218">*Views/Shared/EditorTemplates/ToDoItem.cshtml* šablony:</span><span class="sxs-lookup"><span data-stu-id="cb55a-218">The *Views/Shared/EditorTemplates/ToDoItem.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/ToDoItem.cshtml)]

<span data-ttu-id="cb55a-219">`foreach` má být použit pokud je to možné, při hodnotě se bude používat v `asp-for` nebo `Html.DisplayFor` ekvivalentní kontextu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-219">`foreach` should be used if possible when the value is going to be used in an `asp-for` or `Html.DisplayFor` equivalent context.</span></span> <span data-ttu-id="cb55a-220">Obecně platí `for` je obecně lepší než `foreach` (Pokud tento scénář umožňuje) vzhledem k tomu, že to nemusí přidělovat enumerátor; ale vyhodnocování indexeru ve výrazu LINQ může být nákladné a byste měli minimalizovat.</span><span class="sxs-lookup"><span data-stu-id="cb55a-220">In general, `for` is better than `foreach` (if the scenario allows it) because it doesn't need to allocate an enumerator; however, evaluating an indexer in a LINQ expression can be expensive and should be minimized.</span></span>

&nbsp;

>[!NOTE]
><span data-ttu-id="cb55a-221">Výše uvedené komentářem ukázkový kód ukazuje, jak by nahradit výraz lambda s `@` operátor má přístup ke všem `ToDoItem` v seznamu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-221">The commented sample code above shows how you would replace the lambda expression with the `@` operator to access each `ToDoItem` in the list.</span></span>

## <a name="the-textarea-tag-helper"></a><span data-ttu-id="cb55a-222">Pomocná rutina značky Textarea</span><span class="sxs-lookup"><span data-stu-id="cb55a-222">The Textarea Tag Helper</span></span>

<span data-ttu-id="cb55a-223">`Textarea Tag Helper` Pomocné rutiny značky je podobný pomocné rutiny značky vstup.</span><span class="sxs-lookup"><span data-stu-id="cb55a-223">The `Textarea Tag Helper` tag helper is  similar to the Input Tag Helper.</span></span>

* <span data-ttu-id="cb55a-224">Generuje `id` a `name` atributů a atributů ověření dat z modelu pro [ \<textarea >](https://www.w3.org/wiki/HTML/Elements/textarea) elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-224">Generates the `id` and `name` attributes, and the data validation attributes from the model for a [\<textarea>](https://www.w3.org/wiki/HTML/Elements/textarea) element.</span></span>

* <span data-ttu-id="cb55a-225">Poskytuje silné typování.</span><span class="sxs-lookup"><span data-stu-id="cb55a-225">Provides strong typing.</span></span>

* <span data-ttu-id="cb55a-226">Pomocné rutiny HTML ve zkratce: `Html.TextAreaFor`</span><span class="sxs-lookup"><span data-stu-id="cb55a-226">HTML Helper alternative: `Html.TextAreaFor`</span></span>

<span data-ttu-id="cb55a-227">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-227">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/DescriptionViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterTextArea.cshtml?highlight=4)]

<span data-ttu-id="cb55a-228">Následující kód HTML je vygenerována:</span><span class="sxs-lookup"><span data-stu-id="cb55a-228">The following HTML is generated:</span></span>

```HTML
<form method="post" action="/Demo/RegisterTextArea">
  <textarea data-val="true"
   data-val-maxlength="The field Description must be a string or array type with a maximum length of &#x27;1024&#x27;."
   data-val-maxlength-max="1024"
   data-val-minlength="The field Description must be a string or array type with a minimum length of &#x27;5&#x27;."
   data-val-minlength-min="5"
   id="Description" name="Description">
  </textarea>
  <button type="submit">Test</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

## <a name="the-label-tag-helper"></a><span data-ttu-id="cb55a-229">Pomocná rutina značky popisek</span><span class="sxs-lookup"><span data-stu-id="cb55a-229">The Label Tag Helper</span></span>

* <span data-ttu-id="cb55a-230">Generuje titulek popisek a `for` atribut na [ <label> ](https://www.w3.org/wiki/HTML/Elements/label) – element pro název výrazu</span><span class="sxs-lookup"><span data-stu-id="cb55a-230">Generates the label caption and `for` attribute on a [<label>](https://www.w3.org/wiki/HTML/Elements/label) element for an expression name</span></span>

* <span data-ttu-id="cb55a-231">Pomocné rutiny HTML alternativní: `Html.LabelFor`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-231">HTML Helper alternative: `Html.LabelFor`.</span></span>

<span data-ttu-id="cb55a-232">`Label Tag Helper` Přes čistě element HTML label poskytuje následující výhody:</span><span class="sxs-lookup"><span data-stu-id="cb55a-232">The `Label Tag Helper`  provides the following benefits over a pure HTML label element:</span></span>

* <span data-ttu-id="cb55a-233">Automaticky získána hodnota popisné označení `Display` atribut.</span><span class="sxs-lookup"><span data-stu-id="cb55a-233">You automatically get the descriptive label value from the `Display` attribute.</span></span> <span data-ttu-id="cb55a-234">Zamýšlený zobrazované jméno může změnit postupem času zdokonalují kombinace `Display` atribut a pomocná rutina značek v popisku se vztahují `Display` všude, kde se používá.</span><span class="sxs-lookup"><span data-stu-id="cb55a-234">The intended display name might change over time, and the combination of `Display` attribute and Label Tag Helper will apply the `Display` everywhere it's used.</span></span>

* <span data-ttu-id="cb55a-235">Méně značek ve zdrojovém kódu</span><span class="sxs-lookup"><span data-stu-id="cb55a-235">Less markup in source code</span></span>

* <span data-ttu-id="cb55a-236">Silné typování s vlastností modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-236">Strong typing with the model property.</span></span>

<span data-ttu-id="cb55a-237">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-237">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/SimpleViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterLabel.cshtml?highlight=4)]

<span data-ttu-id="cb55a-238">Následující kód HTML je generován pro `<label>` element:</span><span class="sxs-lookup"><span data-stu-id="cb55a-238">The following HTML is generated for the `<label>` element:</span></span>

```HTML
<label for="Email">Email Address</label>
```

<span data-ttu-id="cb55a-239">Pomocná rutina značky popisek, vygeneruje `for` hodnotu atributu "Email", což je Identifikátor přidružený `<input>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-239">The Label Tag Helper generated the `for` attribute value of "Email", which is the ID associated with the `<input>` element.</span></span> <span data-ttu-id="cb55a-240">Pomocné rutiny značek generovat konzistentní `id` a `for` prvky, aby mohly být správně přidružena.</span><span class="sxs-lookup"><span data-stu-id="cb55a-240">The Tag Helpers generate consistent `id` and `for` elements so they can be correctly associated.</span></span> <span data-ttu-id="cb55a-241">Titulek v této ukázce se segmenty Convenience `Display` atribut.</span><span class="sxs-lookup"><span data-stu-id="cb55a-241">The caption in this sample comes from the `Display` attribute.</span></span> <span data-ttu-id="cb55a-242">Pokud model neobsahovalo `Display` atribut, popisek bude název vlastnosti výrazu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-242">If the model didn't contain a `Display` attribute, the caption would be the property name of the expression.</span></span>

## <a name="the-validation-tag-helpers"></a><span data-ttu-id="cb55a-243">Pomocné rutiny značek ověření</span><span class="sxs-lookup"><span data-stu-id="cb55a-243">The Validation Tag Helpers</span></span>

<span data-ttu-id="cb55a-244">Existují dva pomocných rutin značek ověření.</span><span class="sxs-lookup"><span data-stu-id="cb55a-244">There are two Validation Tag Helpers.</span></span> <span data-ttu-id="cb55a-245">`Validation Message Tag Helper` (Který zobrazí zprávu ověření pro jedinou vlastnost v modelu) a `Validation Summary Tag Helper` (který zobrazuje souhrn chyb ověřování).</span><span class="sxs-lookup"><span data-stu-id="cb55a-245">The `Validation Message Tag Helper` (which displays a validation message for a single property on your model), and the `Validation Summary Tag Helper` (which displays a summary of validation errors).</span></span> <span data-ttu-id="cb55a-246">`Input Tag Helper` Přidá atributů ověření na straně HTML5 klienta k zadání prvky založené na datech anotace atributů ve třídách modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-246">The `Input Tag Helper` adds HTML5 client side validation attributes to input elements based on data annotation attributes on your model classes.</span></span> <span data-ttu-id="cb55a-247">Ověřování provádí na serveru.</span><span class="sxs-lookup"><span data-stu-id="cb55a-247">Validation is also performed on the server.</span></span> <span data-ttu-id="cb55a-248">Pomocná rutina značky ověření zobrazí těchto chybových zpráv při výskytu chyby ověření.</span><span class="sxs-lookup"><span data-stu-id="cb55a-248">The Validation Tag Helper displays these error messages when a validation error occurs.</span></span>

### <a name="the-validation-message-tag-helper"></a><span data-ttu-id="cb55a-249">Pomocná rutina značky zpráva ověření</span><span class="sxs-lookup"><span data-stu-id="cb55a-249">The Validation Message Tag Helper</span></span>

* <span data-ttu-id="cb55a-250">Přidá [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-valmsg-for="property"` atribut [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) element, který připojí chybové zprávy ověření na vstupní pole vlastnosti zadaného modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-250">Adds the [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5)  `data-valmsg-for="property"` attribute to the [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) element, which attaches the validation error messages on the input field of the specified model property.</span></span> <span data-ttu-id="cb55a-251">Pokud dojde k chybě ověření na straně klienta, [jQuery](https://jquery.com/) zobrazí chybová zpráva portálu `<span>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-251">When a client side validation error occurs, [jQuery](https://jquery.com/) displays the error message in the `<span>` element.</span></span>

* <span data-ttu-id="cb55a-252">Taky uplatněním ověřování na serveru.</span><span class="sxs-lookup"><span data-stu-id="cb55a-252">Validation also takes place on the server.</span></span> <span data-ttu-id="cb55a-253">Klienti mohou mít zakázaný JavaScript a nějaké ověření lze provést pouze na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="cb55a-253">Clients may have JavaScript disabled and some validation can only be done on the server side.</span></span>

* <span data-ttu-id="cb55a-254">Pomocné rutiny HTML ve zkratce: `Html.ValidationMessageFor`</span><span class="sxs-lookup"><span data-stu-id="cb55a-254">HTML Helper alternative: `Html.ValidationMessageFor`</span></span>

<span data-ttu-id="cb55a-255">`Validation Message Tag Helper` Se používá s `asp-validation-for` atribut HTML [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-255">The `Validation Message Tag Helper`  is used with the `asp-validation-for` attribute on a HTML [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) element.</span></span>

```HTML
<span asp-validation-for="Email"></span>
```

<span data-ttu-id="cb55a-256">Pomocná rutina značky zpráva ověření bude generovat následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-256">The Validation Message Tag Helper will generate the following HTML:</span></span>

```HTML
<span class="field-validation-valid"
  data-valmsg-for="Email"
  data-valmsg-replace="true"></span>
```

<span data-ttu-id="cb55a-257">Obvykle použijete `Validation Message Tag Helper` po `Input` pomocné rutiny značky pro stejnou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="cb55a-257">You generally use the `Validation Message Tag Helper`  after an `Input` Tag Helper for the same property.</span></span> <span data-ttu-id="cb55a-258">Tím se zobrazí chybové zprávy ověření téměř vstup, který způsobil chybu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-258">Doing so displays any validation error messages near the input that caused the error.</span></span>

> [!NOTE]
> <span data-ttu-id="cb55a-259">Musíte mít zobrazení správné JavaScript a [jQuery](https://jquery.com/) skriptu odkazy na místě pro ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="cb55a-259">You must have a view with the correct JavaScript and [jQuery](https://jquery.com/) script references in place for client side validation.</span></span> <span data-ttu-id="cb55a-260">Zobrazit [ověření modelu](../models/validation.md) Další informace.</span><span class="sxs-lookup"><span data-stu-id="cb55a-260">See [Model Validation](../models/validation.md) for more information.</span></span>

<span data-ttu-id="cb55a-261">Pokud dojde k chybě ověření na straně serveru, (například když máte vlastní server ověřování na straně nebo je zakázáno ověřování na straně klienta), MVC umístí danou chybovou zprávu jako text `<span>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-261">When a server side validation error occurs (for example when you have custom server side validation or client-side validation is disabled), MVC places that error message as the body of the `<span>` element.</span></span>

```HTML
<span class="field-validation-error" data-valmsg-for="Email"
            data-valmsg-replace="true">
   The Email Address field is required.
</span>
```

### <a name="the-validation-summary-tag-helper"></a><span data-ttu-id="cb55a-262">Pomocná rutina pro ověření Summary – značka</span><span class="sxs-lookup"><span data-stu-id="cb55a-262">The Validation Summary Tag Helper</span></span>

* <span data-ttu-id="cb55a-263">Cíle `<div>` elementy `asp-validation-summary` atribut</span><span class="sxs-lookup"><span data-stu-id="cb55a-263">Targets `<div>` elements with the `asp-validation-summary` attribute</span></span>

* <span data-ttu-id="cb55a-264">Pomocné rutiny HTML ve zkratce: `@Html.ValidationSummary`</span><span class="sxs-lookup"><span data-stu-id="cb55a-264">HTML Helper alternative: `@Html.ValidationSummary`</span></span>

<span data-ttu-id="cb55a-265">`Validation Summary Tag Helper` Slouží k zobrazení shrnutí ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="cb55a-265">The `Validation Summary Tag Helper`  is used to display a summary of validation messages.</span></span> <span data-ttu-id="cb55a-266">`asp-validation-summary` Hodnota atributu může být cokoli z následujícího:</span><span class="sxs-lookup"><span data-stu-id="cb55a-266">The `asp-validation-summary` attribute value can be any of the following:</span></span>

|<span data-ttu-id="cb55a-267">asp-validation-summary</span><span class="sxs-lookup"><span data-stu-id="cb55a-267">asp-validation-summary</span></span>|<span data-ttu-id="cb55a-268">Zobrazí ověřovacích zpráv</span><span class="sxs-lookup"><span data-stu-id="cb55a-268">Validation messages displayed</span></span>|
|--- |--- |
|<span data-ttu-id="cb55a-269">ValidationSummary.All</span><span class="sxs-lookup"><span data-stu-id="cb55a-269">ValidationSummary.All</span></span>|<span data-ttu-id="cb55a-270">Vlastnost a model úroveň</span><span class="sxs-lookup"><span data-stu-id="cb55a-270">Property and model level</span></span>|
|<span data-ttu-id="cb55a-271">ValidationSummary.ModelOnly</span><span class="sxs-lookup"><span data-stu-id="cb55a-271">ValidationSummary.ModelOnly</span></span>|<span data-ttu-id="cb55a-272">Model</span><span class="sxs-lookup"><span data-stu-id="cb55a-272">Model</span></span>|
|<span data-ttu-id="cb55a-273">ValidationSummary.None</span><span class="sxs-lookup"><span data-stu-id="cb55a-273">ValidationSummary.None</span></span>|<span data-ttu-id="cb55a-274">Žádná</span><span class="sxs-lookup"><span data-stu-id="cb55a-274">None</span></span>|

### <a name="sample"></a><span data-ttu-id="cb55a-275">Ukázka</span><span class="sxs-lookup"><span data-stu-id="cb55a-275">Sample</span></span>

<span data-ttu-id="cb55a-276">V následujícím příkladu je doplněn datový model `DataAnnotation` atributy, které generuje chybové zprávy ověření na `<input>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-276">In the following example, the data model is decorated with `DataAnnotation` attributes, which generates validation error messages on the `<input>` element.</span></span>  <span data-ttu-id="cb55a-277">Pokud dojde k chybě ověření, zobrazí pomocná rutina značky ověření chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="cb55a-277">When a validation error occurs, the Validation Tag Helper displays the error message:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/RegisterViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterValidation.cshtml?highlight=4,6,8&range=1-10)]

<span data-ttu-id="cb55a-278">Generovaný kód HTML, (když je model platný):</span><span class="sxs-lookup"><span data-stu-id="cb55a-278">The generated HTML (when the model is valid):</span></span>

```HTML
<form action="/DemoReg/Register" method="post">
  <div class="validation-summary-valid" data-valmsg-summary="true">
  <ul><li style="display:none"></li></ul></div>
  Email:  <input name="Email" id="Email" type="email" value=""
   data-val-required="The Email field is required."
   data-val-email="The Email field is not a valid email address."
   data-val="true"> <br>
  <span class="field-validation-valid" data-valmsg-replace="true"
   data-valmsg-for="Email"></span><br>
  Password: <input name="Password" id="Password" type="password"
   data-val-required="The Password field is required." data-val="true"><br>
  <span class="field-validation-valid" data-valmsg-replace="true"
   data-valmsg-for="Password"></span><br>
  <button type="submit">Register</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

## <a name="the-select-tag-helper"></a><span data-ttu-id="cb55a-279">Pomocná rutina vyberte značky</span><span class="sxs-lookup"><span data-stu-id="cb55a-279">The Select Tag Helper</span></span>

* <span data-ttu-id="cb55a-280">Generuje [vyberte](https://www.w3.org/wiki/HTML/Elements/select) a přidružených [možnost](https://www.w3.org/wiki/HTML/Elements/option) prvky pro vlastnosti modelu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-280">Generates [select](https://www.w3.org/wiki/HTML/Elements/select) and associated [option](https://www.w3.org/wiki/HTML/Elements/option) elements for properties of your model.</span></span>

* <span data-ttu-id="cb55a-281">Má alternativu pomocné rutiny HTML `Html.DropDownListFor` a `Html.ListBoxFor`</span><span class="sxs-lookup"><span data-stu-id="cb55a-281">Has an HTML Helper alternative `Html.DropDownListFor` and `Html.ListBoxFor`</span></span>

<span data-ttu-id="cb55a-282">`Select Tag Helper` `asp-for` Určuje název vlastnosti modelu [vyberte](https://www.w3.org/wiki/HTML/Elements/select) elementu a `asp-items` Určuje [možnost](https://www.w3.org/wiki/HTML/Elements/option) elementy.</span><span class="sxs-lookup"><span data-stu-id="cb55a-282">The `Select Tag Helper` `asp-for` specifies the model property  name for the [select](https://www.w3.org/wiki/HTML/Elements/select) element  and `asp-items` specifies the [option](https://www.w3.org/wiki/HTML/Elements/option) elements.</span></span>  <span data-ttu-id="cb55a-283">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb55a-283">For example:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Home/Index.cshtml?range=4)]

<span data-ttu-id="cb55a-284">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-284">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryViewModel.cs)]

<span data-ttu-id="cb55a-285">`Index` Metoda inicializuje `CountryViewModel`, nastaví pro vybranou zemi a předává jej do `Index` zobrazení.</span><span class="sxs-lookup"><span data-stu-id="cb55a-285">The `Index` method initializes the `CountryViewModel`, sets the selected country and passes it to the `Index` view.</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=8-13)]

<span data-ttu-id="cb55a-286">HTTP POST `Index` metoda zobrazí výběr:</span><span class="sxs-lookup"><span data-stu-id="cb55a-286">The HTTP POST `Index` method displays the selection:</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=15-27)]

<span data-ttu-id="cb55a-287">`Index` Zobrazení:</span><span class="sxs-lookup"><span data-stu-id="cb55a-287">The `Index` view:</span></span>

[!code-cshtml[](working-with-forms/sample/final/Views/Home/Index.cshtml?highlight=4)]

<span data-ttu-id="cb55a-288">Které generují následující kód HTML (s "CA" vybrali):</span><span class="sxs-lookup"><span data-stu-id="cb55a-288">Which generates the following HTML (with "CA" selected):</span></span>

```html
<form method="post" action="/">
     <select id="Country" name="Country">
       <option value="MX">Mexico</option>
       <option selected="selected" value="CA">Canada</option>
       <option value="US">USA</option>
     </select>
       <br /><button type="submit">Register</button>
     <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
   </form>
```

> [!NOTE]
> <span data-ttu-id="cb55a-289">Nedoporučujeme ale používat `ViewBag` nebo `ViewData` s pomocné rutiny značky vyberte.</span><span class="sxs-lookup"><span data-stu-id="cb55a-289">We don't recommend using `ViewBag` or `ViewData` with the Select Tag Helper.</span></span> <span data-ttu-id="cb55a-290">Model zobrazení je na poskytování metadat MVC více robustní a obecně menší problém.</span><span class="sxs-lookup"><span data-stu-id="cb55a-290">A view model is more robust at providing MVC metadata and generally less problematic.</span></span>

<span data-ttu-id="cb55a-291">`asp-for` Hodnota atributu je zvláštní případ a nevyžaduje, aby `Model` prefix, ostatní atributy pomocné rutiny značky (například `asp-items`)</span><span class="sxs-lookup"><span data-stu-id="cb55a-291">The `asp-for` attribute value is a special case and doesn't require a `Model` prefix, the other Tag Helper attributes do (such as `asp-items`)</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Home/Index.cshtml?range=4)]

### <a name="enum-binding"></a><span data-ttu-id="cb55a-292">Výčet vazby</span><span class="sxs-lookup"><span data-stu-id="cb55a-292">Enum binding</span></span>

<span data-ttu-id="cb55a-293">Často je vhodné použít `<select>` s `enum` vlastnost a generovat `SelectListItem` elementy ze `enum` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="cb55a-293">It's often convenient to use `<select>` with an `enum` property and generate the `SelectListItem` elements from the `enum` values.</span></span>

<span data-ttu-id="cb55a-294">Ukázka:</span><span class="sxs-lookup"><span data-stu-id="cb55a-294">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnumViewModel.cs?range=3-7)]

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnum.cs)]

<span data-ttu-id="cb55a-295">`GetEnumSelectList` Generuje metodu `SelectList` objekt výčtu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-295">The `GetEnumSelectList` method generates a `SelectList` object for an enum.</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexEnum.cshtml?highlight=5)]

<span data-ttu-id="cb55a-296">Můžete uspořádání seznamu výčtu s `Display` atribut získat bohatší uživatelské rozhraní:</span><span class="sxs-lookup"><span data-stu-id="cb55a-296">You can decorate your enumerator list with the `Display` attribute to get a richer UI:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnum.cs?highlight=5,7)]

<span data-ttu-id="cb55a-297">Následující kód HTML je vygenerována:</span><span class="sxs-lookup"><span data-stu-id="cb55a-297">The following HTML is generated:</span></span>

```HTML
  <form method="post" action="/Home/IndexEnum">
         <select data-val="true" data-val-required="The EnumCountry field is required."
                 id="EnumCountry" name="EnumCountry">
             <option value="0">United Mexican States</option>
             <option value="1">United States of America</option>
             <option value="2">Canada</option>
             <option value="3">France</option>
             <option value="4">Germany</option>
             <option selected="selected" value="5">Spain</option>
         </select>
         <br /><button type="submit">Register</button>
         <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
    </form>
```

### <a name="option-group"></a><span data-ttu-id="cb55a-298">Možnost skupiny</span><span class="sxs-lookup"><span data-stu-id="cb55a-298">Option Group</span></span>

<span data-ttu-id="cb55a-299">Kód HTML [ \<skupiny voleb >](https://www.w3.org/wiki/HTML/Elements/optgroup) element se vygeneruje, když model zobrazení obsahuje jednu nebo více `SelectListGroup` objekty.</span><span class="sxs-lookup"><span data-stu-id="cb55a-299">The HTML  [\<optgroup>](https://www.w3.org/wiki/HTML/Elements/optgroup) element is generated when the view model contains one or more `SelectListGroup` objects.</span></span>

<span data-ttu-id="cb55a-300">`CountryViewModelGroup` Skupin `SelectListItem` prvky do skupiny "Severní Amerika" a "Evropa":</span><span class="sxs-lookup"><span data-stu-id="cb55a-300">The `CountryViewModelGroup` groups the `SelectListItem` elements into the "North America" and "Europe" groups:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/CountryViewModelGroup.cs?highlight=5,6,14,20,26,32,38,44&range=6-56)]

<span data-ttu-id="cb55a-301">Dvě skupiny jsou uvedeny níže:</span><span class="sxs-lookup"><span data-stu-id="cb55a-301">The two groups are shown below:</span></span>

![Příklad možnost skupiny](working-with-forms/_static/grp.png)

<span data-ttu-id="cb55a-303">Generovaný kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-303">The generated HTML:</span></span>

```HTML
 <form method="post" action="/Home/IndexGroup">
      <select id="Country" name="Country">
          <optgroup label="North America">
              <option value="MEX">Mexico</option>
              <option value="CAN">Canada</option>
              <option value="US">USA</option>
          </optgroup>
          <optgroup label="Europe">
              <option value="FR">France</option>
              <option value="ES">Spain</option>
              <option value="DE">Germany</option>
          </optgroup>
      </select>
      <br /><button type="submit">Register</button>
      <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
 </form>
```

### <a name="multiple-select"></a><span data-ttu-id="cb55a-304">Vícenásobný výběr</span><span class="sxs-lookup"><span data-stu-id="cb55a-304">Multiple select</span></span>

<span data-ttu-id="cb55a-305">Pomocná rutina značky vyberte automaticky vygeneruje [více = "více"](http://w3c.github.io/html-reference/select.html) atribut, pokud v rámci specifikovaná vlastnost `asp-for` atribut je `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="cb55a-305">The Select Tag Helper  will automatically generate the [multiple = "multiple"](http://w3c.github.io/html-reference/select.html)  attribute if the property specified in the `asp-for` attribute is an `IEnumerable`.</span></span> <span data-ttu-id="cb55a-306">Mějme například následující model:</span><span class="sxs-lookup"><span data-stu-id="cb55a-306">For example, given the following model:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/CountryViewModelIEnumerable.cs?highlight=6)]

<span data-ttu-id="cb55a-307">S následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="cb55a-307">With the following view:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexMultiSelect.cshtml?highlight=4)]

<span data-ttu-id="cb55a-308">Generuje následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-308">Generates the following HTML:</span></span>

```HTML
<form method="post" action="/Home/IndexMultiSelect">
    <select id="CountryCodes"
    multiple="multiple"
    name="CountryCodes"><option value="MX">Mexico</option>
<option value="CA">Canada</option>
<option value="US">USA</option>
<option value="FR">France</option>
<option value="ES">Spain</option>
<option value="DE">Germany</option>
</select>
    <br /><button type="submit">Register</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

### <a name="no-selection"></a><span data-ttu-id="cb55a-309">Žádný výběr</span><span class="sxs-lookup"><span data-stu-id="cb55a-309">No selection</span></span>

<span data-ttu-id="cb55a-310">Pokud se pomocí možnosti "nebyl zadán" ve více stránek, můžete vytvořit šablonu chcete-li odstranit opakující se kód HTML:</span><span class="sxs-lookup"><span data-stu-id="cb55a-310">If you find yourself using the "not specified" option in multiple pages, you can create a template to eliminate repeating the HTML:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexEmptyTemplate.cshtml?highlight=5)]

<span data-ttu-id="cb55a-311">*Views/Shared/EditorTemplates/CountryViewModel.cshtml* šablony:</span><span class="sxs-lookup"><span data-stu-id="cb55a-311">The *Views/Shared/EditorTemplates/CountryViewModel.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/CountryViewModel.cshtml)]

<span data-ttu-id="cb55a-312">Přidání kódu HTML [ \<možnost >](https://www.w3.org/wiki/HTML/Elements/option) se neomezuje na prvky *žádný výběr* případ.</span><span class="sxs-lookup"><span data-stu-id="cb55a-312">Adding HTML [\<option>](https://www.w3.org/wiki/HTML/Elements/option) elements isn't limited to the *No selection* case.</span></span> <span data-ttu-id="cb55a-313">Například následující metodu pro zobrazení a akce se generují kód HTML podobně jako výše uvedený kód:</span><span class="sxs-lookup"><span data-stu-id="cb55a-313">For example, the following view and action method will generate HTML similar to the code above:</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=114-119)]

[!code-HTML[](working-with-forms/sample/final/Views/Home/IndexOption.cshtml)]

<span data-ttu-id="cb55a-314">Správné `<option>` bude vybraný element (obsahují `selected="selected"` atribut) v závislosti na aktuální `Country` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="cb55a-314">The correct `<option>` element will be selected ( contain the `selected="selected"` attribute) depending on the current `Country` value.</span></span>

```HTML
 <form method="post" action="/Home/IndexEmpty">
      <select id="Country" name="Country">
          <option value="">&lt;none&gt;</option>
          <option value="MX">Mexico</option>
          <option value="CA" selected="selected">Canada</option>
          <option value="US">USA</option>
      </select>
      <br /><button type="submit">Register</button>
   <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
 </form>
 ```

## <a name="additional-resources"></a><span data-ttu-id="cb55a-315">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="cb55a-315">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* [<span data-ttu-id="cb55a-316">Element formuláře HTML</span><span class="sxs-lookup"><span data-stu-id="cb55a-316">HTML Form element</span></span>](https://www.w3.org/TR/html401/interact/forms.html)
* [<span data-ttu-id="cb55a-317">Požádat o Token pro ověření</span><span class="sxs-lookup"><span data-stu-id="cb55a-317">Request Verification Token</span></span>](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)
* <xref:mvc/models/model-binding>
* <xref:mvc/models/validation>
* [<span data-ttu-id="cb55a-318">IAttributeAdapter rozhraní</span><span class="sxs-lookup"><span data-stu-id="cb55a-318">IAttributeAdapter Interface</span></span>](/dotnet/api/Microsoft.AspNetCore.Mvc.DataAnnotations.IAttributeAdapter)
* [<span data-ttu-id="cb55a-319">Fragmenty kódu pro tento dokument</span><span class="sxs-lookup"><span data-stu-id="cb55a-319">Code snippets for this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/working-with-forms/sample/final)
