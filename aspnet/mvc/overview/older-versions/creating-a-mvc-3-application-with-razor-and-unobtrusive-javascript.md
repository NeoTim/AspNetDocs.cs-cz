---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Vytvoření aplikace MVC 3 s břitvou a nenápadným JavaScriptem | Dokumenty společnosti Microsoft
author: rick-anderson
description: Ukázková webová aplikace Seznamu uživatelů ukazuje, jak jednoduché je vytvářet ASP.NET aplikací MVC 3 pomocí modulu zobrazení Razor. Ukázková aplikace s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542453"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="d7d24-104">Vytvoření aplikace MVC 3 se syntaxí Razor a nerušivým JavaScriptem</span><span class="sxs-lookup"><span data-stu-id="d7d24-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="d7d24-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d7d24-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d7d24-106">Ukázková webová aplikace Seznamu uživatelů ukazuje, jak jednoduché je vytvářet ASP.NET aplikací MVC 3 pomocí modulu zobrazení Razor.</span><span class="sxs-lookup"><span data-stu-id="d7d24-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="d7d24-107">Ukázková aplikace ukazuje, jak používat nový modul zobrazení Razor s ASP.NET MVC verze 3 a Visual Studio 2010 k vytvoření fiktivního webu seznamu uživatelů, který obsahuje funkce, jako je vytváření, zobrazování, úpravy a odstranění uživatelů.</span><span class="sxs-lookup"><span data-stu-id="d7d24-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="d7d24-108">Tento kurz popisuje kroky, které byly podniknuty za účelem sestavení ukázky seznamu uživatelů ASP.NET aplikace MVC 3.</span><span class="sxs-lookup"><span data-stu-id="d7d24-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="d7d24-109">Projekt sady Visual Studio se zdrojovým kódem jazyka C# a VB je k dispozici jako doprovodný k tomuto tématu: [Stáhnout](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="d7d24-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="d7d24-110">Máte-li dotazy týkající se tohoto výukového programu, prosím, po nich na [fóru MVC](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7d24-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="d7d24-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="d7d24-111">Overview</span></span>

<span data-ttu-id="d7d24-112">Aplikace, kterou budete vytvářet, je jednoduchý seznam uživatelů webové stránky.</span><span class="sxs-lookup"><span data-stu-id="d7d24-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="d7d24-113">Uživatelé mohou zadávat, zobrazovat a aktualizovat informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="d7d24-113">Users can enter, view, and update user information.</span></span>

![Ukázkový web](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="d7d24-115">Můžete si stáhnout VB a C# dokončený projekt [zde](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span><span class="sxs-lookup"><span data-stu-id="d7d24-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="d7d24-116">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="d7d24-116">Creating the Web Application</span></span>

<span data-ttu-id="d7d24-117">Chcete-li kurz spustit, otevřete Visual Studio 2010 a vytvořte nový projekt pomocí ASP.NET *šablonu webové aplikace MVC 3.*</span><span class="sxs-lookup"><span data-stu-id="d7d24-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="d7d24-118">Pojmenujte &quot;aplikaci Mvc3Razor&quot;.</span><span class="sxs-lookup"><span data-stu-id="d7d24-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="d7d24-119">[![Nový projekt MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="d7d24-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="d7d24-120">V dialogovém **okně Nový ASP.NET MVC 3 Project** vyberte Možnost **Internetová aplikace**, vyberte modul zobrazení Holicí strojek a klepněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Nový ASP.NET dialogové okno Projektu MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="d7d24-122">V tomto kurzu nebudete používat ASP.NET poskytovatele členství, takže můžete odstranit všechny soubory spojené s přihlášením a členstvím.</span><span class="sxs-lookup"><span data-stu-id="d7d24-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="d7d24-123">V **Průzkumníku řešení**odeberte následující soubory a adresáře:</span><span class="sxs-lookup"><span data-stu-id="d7d24-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="d7d24-124">*Řadiče\AccountController*</span><span class="sxs-lookup"><span data-stu-id="d7d24-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="d7d24-125">*Modely\Modely účtů*</span><span class="sxs-lookup"><span data-stu-id="d7d24-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="d7d24-126">*Zobrazení\Sdílené\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="d7d24-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="d7d24-127">*Zobrazení\Účet* (a všechny soubory v tomto adresáři)</span><span class="sxs-lookup"><span data-stu-id="d7d24-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="d7d24-129">Upravte `<div>` `logindisplay` <em>&quot;</em>&quot; <em> \_soubor Layout.cshtml</em> a nahraďte značky uvnitř prvku s názvem Přihlášení zakázáno .</span><span class="sxs-lookup"><span data-stu-id="d7d24-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="d7d24-130">Následující příklad ukazuje nové značky:</span><span class="sxs-lookup"><span data-stu-id="d7d24-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="d7d24-131">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="d7d24-131">Adding the Model</span></span>

<span data-ttu-id="d7d24-132">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na složku *Modely,* vyberte **přidat**a potom klepněte na příkaz **Třída**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Třída Mdl nového uživatele](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="d7d24-134">Pojmenujte `UserModel`třídu .</span><span class="sxs-lookup"><span data-stu-id="d7d24-134">Name the class `UserModel`.</span></span> <span data-ttu-id="d7d24-135">Nahraďte obsah souboru *UserModel* následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d7d24-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="d7d24-136">Třída `UserModel` představuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="d7d24-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="d7d24-137">Každý člen třídy je anotován s [atributem Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) z oboru názvů [DataAnnotations.](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)</span><span class="sxs-lookup"><span data-stu-id="d7d24-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="d7d24-138">Atributy v oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytují automatické ověření na straně klienta a serveru pro webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="d7d24-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="d7d24-139">Otevřete `HomeController` třídu `using` a přidejte direktivu, abyste měli přístup k třídám `UserModel` a: `Users`</span><span class="sxs-lookup"><span data-stu-id="d7d24-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="d7d24-140">Hned za `HomeController` deklaraci přidejte následující komentář `Users` a odkaz na třídu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="d7d24-141">Třída `Users` je zjednodušené úložiště dat v paměti, které budete používat v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="d7d24-142">V reálné aplikaci byste použili databázi k ukládání informací o uživateli.</span><span class="sxs-lookup"><span data-stu-id="d7d24-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="d7d24-143">Prvních několik řádků `HomeController` souboru je zobrazeno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="d7d24-144">Vytvořte aplikaci tak, aby model uživatele bude k dispozici průvodce pomocí posla v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="d7d24-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="d7d24-145">Vytvoření výchozího zobrazení</span><span class="sxs-lookup"><span data-stu-id="d7d24-145">Creating the Default View</span></span>

<span data-ttu-id="d7d24-146">Dalším krokem je přidání metody akce a zobrazení pro zobrazení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="d7d24-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="d7d24-147">Odstraňte existující *soubor Zobrazení\Domů\Index.*</span><span class="sxs-lookup"><span data-stu-id="d7d24-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="d7d24-148">Vytvoříte nový soubor *indexu* pro zobrazení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="d7d24-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="d7d24-149">Ve `HomeController` třídě nahraďte obsah `Index` metody následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d7d24-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="d7d24-150">Klepněte pravým `Index` tlačítkem myši do metody a potom klepněte na příkaz **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Přidat zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="d7d24-152">Vyberte možnost **Vytvořit zobrazení silného typu.**</span><span class="sxs-lookup"><span data-stu-id="d7d24-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="d7d24-153">V **pole Zobrazit třídu dat**vyberte možnost **Mvc3Razor.Models.UserModel**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="d7d24-154">(Pokud nevidíte **Mvc3Razor.Models.UserModel** v poli **Zobrazit datové třídy,** je třeba vytvořit projekt.) Ujistěte se, že je modul zobrazení nastaven na **břitvu**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="d7d24-155">Nastavte **obsah zobrazení** na **seznam** a klepněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-155">Set **View content** to **List** and then click **Add**.</span></span>

![Přidat zobrazení indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="d7d24-157">Nové zobrazení automaticky přilne uživatelskými daty, která `Index` byla předána zobrazení.</span><span class="sxs-lookup"><span data-stu-id="d7d24-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="d7d24-158">Zkontrolujte nově generovaný soubor *Zobrazení\Home\Index.*</span><span class="sxs-lookup"><span data-stu-id="d7d24-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="d7d24-159">Odkazy **Vytvořit nové**, **Upravit**, **Podrobnosti**a **Odstranit** nefungují, ale zbytek stránky je funkční.</span><span class="sxs-lookup"><span data-stu-id="d7d24-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="d7d24-160">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="d7d24-160">Run the page.</span></span> <span data-ttu-id="d7d24-161">Zobrazí se seznam uživatelů.</span><span class="sxs-lookup"><span data-stu-id="d7d24-161">You see a list of users.</span></span>

![Stránka rejstříku](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="d7d24-163">Otevřete soubor *Index.cshtml* `ActionLink` a nahraďte značky **pro Úpravy**, **Podrobnosti**a **Odstranit** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d7d24-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="d7d24-164">Uživatelské jméno se používá jako ID pro vyhledání vybraného záznamu v odkazech **Upravit**, **Podrobnosti**a **Odstranit.**</span><span class="sxs-lookup"><span data-stu-id="d7d24-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="d7d24-165">Vytvoření zobrazení podrobností</span><span class="sxs-lookup"><span data-stu-id="d7d24-165">Creating the Details View</span></span>

<span data-ttu-id="d7d24-166">Dalším krokem je přidání `Details` metody akce a zobrazení pro zobrazení podrobností o uživateli.</span><span class="sxs-lookup"><span data-stu-id="d7d24-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="d7d24-168">Do domácího ovladače přidejte následující `Details` metodu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="d7d24-169">Klepněte pravým `Details` tlačítkem myši do metody a pak vyberte <strong>přidat zobrazení</strong>.</span><span class="sxs-lookup"><span data-stu-id="d7d24-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="d7d24-170">Ověřte, zda pole <strong>Zobrazit datovou třídu</strong> obsahuje <strong>model Mvc3Razor.Models.UserModel</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="d7d24-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="d7d24-171">Nastavte <strong>zobrazení obsahu</strong> na <strong>podrobnosti</strong> a klepněte na tlačítko <strong>Přidat</strong>.</span><span class="sxs-lookup"><span data-stu-id="d7d24-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Přidání zobrazení podrobností](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="d7d24-173">Spusťte aplikaci a vyberte odkaz podrobností.</span><span class="sxs-lookup"><span data-stu-id="d7d24-173">Run the application and select a details link.</span></span> <span data-ttu-id="d7d24-174">Automatické generování uživatelského zařízení zobrazuje každou vlastnost v modelu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-174">The automatic scaffolding shows each property in the model.</span></span>

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="d7d24-176">Vytvoření zobrazení úprav</span><span class="sxs-lookup"><span data-stu-id="d7d24-176">Creating the Edit View</span></span>

<span data-ttu-id="d7d24-177">Do domácího ovladače přidejte následující `Edit` metodu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="d7d24-178">Přidejte zobrazení jako v předchozích krocích, ale nastavte **obsah zobrazení** na **Upravit**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Přidat zobrazení pro úpravy](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="d7d24-180">Spusťte aplikaci a upravte jméno a příjmení jednoho z uživatelů.</span><span class="sxs-lookup"><span data-stu-id="d7d24-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="d7d24-181">Pokud porušíte omezení, `DataAnnotation` která byla `UserModel` použita pro třídu, při odeslání formuláře se zobrazí chyby ověření, které jsou vytvářeny kódem serveru.</span><span class="sxs-lookup"><span data-stu-id="d7d24-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="d7d24-182">Pokud například změníte křestní &quot;&quot; jméno &quot;&quot;Ann na A , zobrazí se ve formuláři následující chyba:</span><span class="sxs-lookup"><span data-stu-id="d7d24-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="d7d24-183">V tomto kurzu považujete uživatelské jméno za primární klíč.</span><span class="sxs-lookup"><span data-stu-id="d7d24-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="d7d24-184">Proto vlastnost uživatelského jména nelze změnit.</span><span class="sxs-lookup"><span data-stu-id="d7d24-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="d7d24-185">V souboru *Edit.cshtml* nastavte `Html.BeginForm` uživatelské jméno jako skryté pole.</span><span class="sxs-lookup"><span data-stu-id="d7d24-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="d7d24-186">To způsobí, že vlastnost, která má být předána v modelu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="d7d24-187">Následující fragment kódu ukazuje umístění `Hidden` příkazu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="d7d24-188">`TextBoxFor` Nahraďte `ValidationMessageFor` a značky pro `DisplayFor` uživatelské jméno voláním.</span><span class="sxs-lookup"><span data-stu-id="d7d24-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="d7d24-189">Metoda `DisplayFor` zobrazí vlastnost jako prvek jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="d7d24-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="d7d24-190">Následující příklad ukazuje dokončené značky.</span><span class="sxs-lookup"><span data-stu-id="d7d24-190">The following example shows the completed markup.</span></span> <span data-ttu-id="d7d24-191">Původní `TextBoxFor` a `ValidationMessageFor` volání jsou komentoval se břitva start-komentář`@* *@`a end-komentář znaky ( )</span><span class="sxs-lookup"><span data-stu-id="d7d24-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="d7d24-192">Povolení ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="d7d24-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="d7d24-193">Chcete-li povolit ověření na straně klienta v ASP.NET MVC 3, musíte nastavit dva příznaky a musíte zahrnout tři soubory JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="d7d24-194">Otevřete soubor *Web.config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="d7d24-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="d7d24-195">Ověřte `that ClientValidationEnabled` a `UnobtrusiveJavaScriptEnabled` jsou nastaveny na hodnotu true v nastavení aplikace.</span><span class="sxs-lookup"><span data-stu-id="d7d24-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="d7d24-196">Následující fragment z kořenového souboru *Web.config* zobrazuje správné nastavení:</span><span class="sxs-lookup"><span data-stu-id="d7d24-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="d7d24-197">Nastavení `UnobtrusiveJavaScriptEnabled` na hodnotu true umožňuje nenápadné ověřování klienta Ajax a nenápadný klient.</span><span class="sxs-lookup"><span data-stu-id="d7d24-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="d7d24-198">Při použití nenápadné ověření, ověřovací pravidla se změní na atributy HTML5.</span><span class="sxs-lookup"><span data-stu-id="d7d24-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="d7d24-199">Názvy atributů HTML5 se mohou skládat pouze z malých písmen, čísel a pomlček.</span><span class="sxs-lookup"><span data-stu-id="d7d24-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="d7d24-200">Nastavení `ClientValidationEnabled` na hodnotu true umožňuje ověření na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d7d24-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="d7d24-201">Nastavením těchto klíčů v souboru *Web.config* aplikace povolíte ověření klienta a nenápadný JavaScript pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d7d24-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="d7d24-202">Tato nastavení můžete také povolit nebo zakázat v jednotlivých zobrazeních nebo v metodách kontroleru pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="d7d24-203">Do vykresleného zobrazení je také nutné zahrnout několik souborů JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="d7d24-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="d7d24-204">Snadný způsob, jak zahrnout JavaScript do všech zobrazení, je přidat jej do souboru *Views\Shared\\_Layout.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="d7d24-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="d7d24-205">Nahraďte `<head>` prvek souboru \* \_Layout.cshtml\* následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d7d24-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="d7d24-206">První dva skripty jQuery jsou hostovány sítí CDN (Microsoft Ajax Content Delivery Network).</span><span class="sxs-lookup"><span data-stu-id="d7d24-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="d7d24-207">Využitím microsoft ajax CDN, můžete výrazně zlepšit první přístupů výkon vašich aplikací.</span><span class="sxs-lookup"><span data-stu-id="d7d24-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="d7d24-208">Spusťte aplikaci a klepněte na odkaz pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="d7d24-208">Run the application and click an edit link.</span></span> <span data-ttu-id="d7d24-209">Zobrazení zdroje stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="d7d24-209">View the page's source in the browser.</span></span> <span data-ttu-id="d7d24-210">Zdroj prohlížeče zobrazuje mnoho atributů `data-val` formuláře (pro ověření dat).</span><span class="sxs-lookup"><span data-stu-id="d7d24-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="d7d24-211">Pokud je povoleno ověření klienta a nenápadný JavaScript, vstupní pole `data-val="true"` s pravidlem ověření klienta obsahují atribut pro aktivaci nenápadného ověření klienta.</span><span class="sxs-lookup"><span data-stu-id="d7d24-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="d7d24-212">Například `City` pole v modelu bylo dekorováno atributem [Required,](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) což má za následek html zobrazený v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="d7d24-213">Pro každé pravidlo ověření klienta je přidán `data-val-rulename="message"`atribut, který má formulář .</span><span class="sxs-lookup"><span data-stu-id="d7d24-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="d7d24-214">Pomocí `City` předchozího příkladu pole vygeneruje požadované `data-val-required` pravidlo ověření &quot;klienta atribut&quot;a zprávu Pole Město je povinné .</span><span class="sxs-lookup"><span data-stu-id="d7d24-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="d7d24-215">Spusťte aplikaci, upravte jednoho `City` z uživatelů a zrušte zaškrtnutí pole.</span><span class="sxs-lookup"><span data-stu-id="d7d24-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="d7d24-216">Při out mimo pole se zobrazí chybová zpráva ověření na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d7d24-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Město požadováno](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="d7d24-218">Podobně pro každý parametr v pravidle ověření klienta je přidán `data-val-rulename-paramname=paramvalue`atribut, který má formulář .</span><span class="sxs-lookup"><span data-stu-id="d7d24-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="d7d24-219">Například `FirstName` vlastnost je anotována atributem [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) a určuje minimální délku 3 a maximální délku 8.</span><span class="sxs-lookup"><span data-stu-id="d7d24-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="d7d24-220">Pojmenované ověřovací pravidlo `length` dat má `max` název parametru a hodnotu parametru 8.</span><span class="sxs-lookup"><span data-stu-id="d7d24-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="d7d24-221">Následující text ukazuje kód HTML, `FirstName` který je generován pro pole při úpravě jednoho z uživatelů:</span><span class="sxs-lookup"><span data-stu-id="d7d24-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="d7d24-222">Další informace o nenápadném ověření klienta naleznete v položce [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) v blogu Brada Wilsona.</span><span class="sxs-lookup"><span data-stu-id="d7d24-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="d7d24-223">V ASP.NET MVC 3 Beta, někdy budete muset odeslat formulář, aby bylo možné spustit ověření na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d7d24-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="d7d24-224">To může být změněno pro konečnou verzi.</span><span class="sxs-lookup"><span data-stu-id="d7d24-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="d7d24-225">Vytvoření zobrazení vytvoření</span><span class="sxs-lookup"><span data-stu-id="d7d24-225">Creating the Create View</span></span>

<span data-ttu-id="d7d24-226">Dalším krokem je přidání `Create` metody a zobrazení akce, aby uživatel mohl vytvořit nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="d7d24-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="d7d24-227">Do domácího ovladače přidejte následující `Create` metodu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="d7d24-228">Přidejte zobrazení jako v předchozích krocích, ale nastavte **obsah zobrazení** na **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="d7d24-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="d7d24-230">Spusťte aplikaci, vyberte odkaz **Vytvořit** a přidejte nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="d7d24-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="d7d24-231">Metoda `Create` automaticky využívá ověřování na straně klienta a serveru.</span><span class="sxs-lookup"><span data-stu-id="d7d24-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="d7d24-232">Pokuste se zadat uživatelské jméno, které &quot;obsahuje&quot;prázdné znaky, například Ben X .</span><span class="sxs-lookup"><span data-stu-id="d7d24-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="d7d24-233">Při vybočování karty z pole uživatelského`White space is not allowed`jména se zobrazí chyba ověření na straně klienta ( ).</span><span class="sxs-lookup"><span data-stu-id="d7d24-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="d7d24-234">Přidat metodu Delete</span><span class="sxs-lookup"><span data-stu-id="d7d24-234">Add the Delete method</span></span>

<span data-ttu-id="d7d24-235">Chcete-li kurz dokončit, `Delete` přidejte do domácího ovladače následující metodu:</span><span class="sxs-lookup"><span data-stu-id="d7d24-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="d7d24-236">Přidejte `Delete` zobrazení jako v předchozích krocích a **nastavíte možnost Odstranit obsah zobrazení** . **Delete**</span><span class="sxs-lookup"><span data-stu-id="d7d24-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Odstranit zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="d7d24-238">Nyní máte jednoduchou, ale plně funkční aplikaci ASP.NET MVC 3 s ověřením.</span><span class="sxs-lookup"><span data-stu-id="d7d24-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
