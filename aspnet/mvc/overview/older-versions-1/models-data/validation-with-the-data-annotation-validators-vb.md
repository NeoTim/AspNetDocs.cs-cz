---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Ověření pomocí validátorů anotace dat (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Využijte binder modelu poznámky k ověření v rámci aplikace ASP.NET MVC. Naučte se používat různé typy validátoru...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542635"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="6e006-104">Ověřování validátory datových poznámek (VB)</span><span class="sxs-lookup"><span data-stu-id="6e006-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="6e006-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6e006-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6e006-106">Využijte binder modelu poznámky k ověření v rámci aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6e006-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="6e006-107">Naučte se používat různé typy atributů validátoru a pracovat s nimi v microsoft entity frameworku.</span><span class="sxs-lookup"><span data-stu-id="6e006-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="6e006-108">V tomto kurzu se dozvíte, jak používat validátory anotace dat k ověření v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6e006-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="6e006-109">Výhodou použití validátorů anotace dat je, že umožňují provádět ověření jednoduše přidáním jednoho nebo více atributů – například atributu Required nebo StringLength – do vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="6e006-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="6e006-110">Před použitím validátorů anotace dat je nutné stáhnout datové poznámky model pořadače.</span><span class="sxs-lookup"><span data-stu-id="6e006-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="6e006-111">Ukázku datových anotací model binder si můžete stáhnout z webových stránek CodePlex kliknutím [zde](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span><span class="sxs-lookup"><span data-stu-id="6e006-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="6e006-112">Je důležité si uvědomit, že data poznámky model binder není oficiální součástí rozhraní Microsoft ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6e006-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="6e006-113">Přestože data poznámky model pořadač byl vytvořen týmem Microsoft ASP.NET MVC, Společnost Microsoft nenabízí oficiální podporu produktu pro data poznámky model pořadač popsané a používané v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="6e006-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="6e006-114">Použití pořadače modelu poznámky dat</span><span class="sxs-lookup"><span data-stu-id="6e006-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="6e006-115">Chcete-li použít pořadač modelu datových anotací v aplikaci mvc ASP.NET, musíte nejprve přidat odkaz na sestavení Microsoft.Web.Mvc.DataAnnotations.dll a sestavení System.ComponentModel.DataAnnotations.dll.</span><span class="sxs-lookup"><span data-stu-id="6e006-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="6e006-116">Vyberte volbu nabídky **Projekt, Přidat odkaz**.</span><span class="sxs-lookup"><span data-stu-id="6e006-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="6e006-117">Dále klikněte na kartu **Procházet** a vyhledejte umístění, kde jste stáhli (a rozbalili) ukázku datové poznámky model binder (viz **obrázek 1).**</span><span class="sxs-lookup"><span data-stu-id="6e006-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="6e006-118">**Obrázek 1**: Přidání odkazu na pořadač modelu datových poznámk[(Kliknutím zobrazíte obrázek v plné velikosti)](validation-with-the-data-annotation-validators-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6e006-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="6e006-119">Vyberte sestavení Microsoft.Web.Mvc.DataAnnotations.dll a sestavení System.ComponentModel.DataAnnotations.dll a klepněte na tlačítko **OK.**</span><span class="sxs-lookup"><span data-stu-id="6e006-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="6e006-120">Sestavení System.ComponentModel.DataAnnotations.dll, které je součástí aktualizace .NET Framework Service Pack 1 s vazbami modelu datových anotací, nelze použít.</span><span class="sxs-lookup"><span data-stu-id="6e006-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="6e006-121">Je nutné použít verzi sestavení System.ComponentModel.DataAnnotations.dll, která je součástí ukázkového stažení modelu datových poznámk.</span><span class="sxs-lookup"><span data-stu-id="6e006-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="6e006-122">Nakonec je třeba zaregistrovat DataAnnotations Model Binder v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="6e006-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="6e006-123">Přidejte následující řádek kódu\_do obslužné rutiny události Start() aplikace tak, aby metoda Start() aplikace\_vypadala takto:</span><span class="sxs-lookup"><span data-stu-id="6e006-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="6e006-124">Tento řádek kódu registruje DataAnnotationsModelBinder jako výchozí pořadač modelu pro celou ASP.NET aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="6e006-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="6e006-125">Použití atributů validátoru anotace dat</span><span class="sxs-lookup"><span data-stu-id="6e006-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="6e006-126">Při použití data poznámky model binder, použijete atributy validátoru k provedení ověření.</span><span class="sxs-lookup"><span data-stu-id="6e006-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="6e006-127">Obor názvů System.ComponentModel.DataAnnotations obsahuje následující atributy validátoru:</span><span class="sxs-lookup"><span data-stu-id="6e006-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="6e006-128">Rozsah – umožňuje ověřit, zda hodnota vlastnosti spadá mezi zadaný rozsah hodnot.</span><span class="sxs-lookup"><span data-stu-id="6e006-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="6e006-129">RegularExpression – Umožňuje ověřit, zda hodnota vlastnosti odpovídá zadanému vzoru regulárního výrazu.</span><span class="sxs-lookup"><span data-stu-id="6e006-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="6e006-130">Povinné – Umožňuje označit vlastnost podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="6e006-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="6e006-131">StringLength – Umožňuje zadat maximální délku vlastnosti řetězce.</span><span class="sxs-lookup"><span data-stu-id="6e006-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="6e006-132">Ověření – základní třída pro všechny atributy validátoru.</span><span class="sxs-lookup"><span data-stu-id="6e006-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e006-133">Pokud vaše potřeby ověření nejsou splněny některé standardní validátory pak máte vždy možnost vytvořit vlastní atribut validátoru deducem nový atribut validátoru ze základního atributu Validation.</span><span class="sxs-lookup"><span data-stu-id="6e006-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="6e006-134">Třída Product v **seznamu 1** ukazuje, jak používat tyto atributy validátoru.</span><span class="sxs-lookup"><span data-stu-id="6e006-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="6e006-135">Vlastnosti Název, Popis a UnitPrice jsou označeny podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="6e006-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="6e006-136">Vlastnost Name musí mít délku řetězce, která je menší než 10 znaků.</span><span class="sxs-lookup"><span data-stu-id="6e006-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="6e006-137">Nakonec UnitPrice vlastnost musí odpovídat vzor regulárního výrazu, který představuje částku měny.</span><span class="sxs-lookup"><span data-stu-id="6e006-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="6e006-138">**Výpis 1**: Modely\Product.vb</span><span class="sxs-lookup"><span data-stu-id="6e006-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="6e006-139">Třída Product ukazuje, jak použít jeden další atribut: atribut DisplayName.</span><span class="sxs-lookup"><span data-stu-id="6e006-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="6e006-140">Atribut DisplayName umožňuje změnit název vlastnosti, když je vlastnost zobrazena v chybové zprávě.</span><span class="sxs-lookup"><span data-stu-id="6e006-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="6e006-141">Namísto zobrazení chybové zprávy "Pole UnitPrice je povinné" můžete zobrazit chybovou zprávu "Pole Cena je povinné".</span><span class="sxs-lookup"><span data-stu-id="6e006-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e006-142">Pokud chcete zcela přizpůsobit chybovou zprávu zobrazenou validátorem, můžete přiřadit vlastní chybovou zprávu vlastnosti ErrorMessage validátoru takto:`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="6e006-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="6e006-143">Třídu Produkt můžete použít ve **výpisu 1** s akcí Vytvořit() kontrolora v **výpisu 2**.</span><span class="sxs-lookup"><span data-stu-id="6e006-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="6e006-144">Tato akce kontroler znovu zobrazí vytvořit pohled, když stav modelu obsahuje nějaké chyby.</span><span class="sxs-lookup"><span data-stu-id="6e006-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="6e006-145">**Výpis 2**: Řadiče\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="6e006-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="6e006-146">Nakonec můžete vytvořit zobrazení v **výpisu 3** klepnutím pravým tlačítkem myši na akci Vytvořit() a výběrem možnosti nabídky **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="6e006-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="6e006-147">Vytvořte zobrazení silného typu s třídou Product jako třídou modelu.</span><span class="sxs-lookup"><span data-stu-id="6e006-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="6e006-148">V rozevíracím seznamu obsahu zobrazení vyberte **Vytvořit** (viz **obrázek 2).**</span><span class="sxs-lookup"><span data-stu-id="6e006-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="6e006-149">**Obrázek 2**: Přidání zobrazení vytvoření</span><span class="sxs-lookup"><span data-stu-id="6e006-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="6e006-150">**Výpis 3**: Zobrazení\Produkt\Vytvořit.aspx</span><span class="sxs-lookup"><span data-stu-id="6e006-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e006-151">Odeberte pole Id z formuláře Vytvořit generovaného možností nabídky **Přidat zobrazení.**</span><span class="sxs-lookup"><span data-stu-id="6e006-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="6e006-152">Vzhledem k tomu, že pole Id odpovídá sloupci Identita, nechcete uživatelům povolit zadání hodnoty pro toto pole.</span><span class="sxs-lookup"><span data-stu-id="6e006-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="6e006-153">Pokud odešlete formulář pro vytvoření produktu a nezadáte hodnoty pro požadovaná pole, zobrazí se chybové zprávy ověření na **obrázku 3.**</span><span class="sxs-lookup"><span data-stu-id="6e006-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="6e006-154">**Obrázek 3**: Chybějící povinná pole</span><span class="sxs-lookup"><span data-stu-id="6e006-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="6e006-155">Pokud zadáte neplatnou částku měny, zobrazí se chybová zpráva **na obrázku 4.**</span><span class="sxs-lookup"><span data-stu-id="6e006-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="6e006-156">**Obrázek 4**: Neplatná částka měny</span><span class="sxs-lookup"><span data-stu-id="6e006-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="6e006-157">Použití validátorů anotace dat s rámcem entity</span><span class="sxs-lookup"><span data-stu-id="6e006-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="6e006-158">Pokud používáte Microsoft Entity Framework ke generování tříd datového modelu, pak nelze použít atributy validátoru přímo na vaše třídy.</span><span class="sxs-lookup"><span data-stu-id="6e006-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="6e006-159">Vzhledem k tomu, že Návrhář rozhraní entity generuje třídy modelu, všechny změny, které provedete ve třídách modelu, budou přepsány při příštím provádění změn v návrháři.</span><span class="sxs-lookup"><span data-stu-id="6e006-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="6e006-160">Pokud chcete použít validátory s třídami generovanými entity framework pak je třeba vytvořit meta datové třídy.</span><span class="sxs-lookup"><span data-stu-id="6e006-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="6e006-161">Validátory použijete na třídu metadat meta namísto použití validátorů na skutečnou třídu.</span><span class="sxs-lookup"><span data-stu-id="6e006-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="6e006-162">Představte si například, že jste vytvořili třídu Movie pomocí entity Framework (viz **obrázek 5).**</span><span class="sxs-lookup"><span data-stu-id="6e006-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="6e006-163">Představte si, kromě toho, že chcete, aby název filmu a ředitel vlastnosti požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6e006-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="6e006-164">V takovém případě můžete vytvořit třídu částečné třídy a meta datové třídy v **výpisu 4**.</span><span class="sxs-lookup"><span data-stu-id="6e006-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="6e006-165">**Obrázek 5**: Třída filmu generovaná rozhraním Entity Framework</span><span class="sxs-lookup"><span data-stu-id="6e006-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="6e006-166">**Výpis 4**: Modely\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="6e006-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="6e006-167">Soubor v **seznamu 4** obsahuje dvě třídy s názvem Film a MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="6e006-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="6e006-168">Třída Movie je částečná třída.</span><span class="sxs-lookup"><span data-stu-id="6e006-168">The Movie class is a partial class.</span></span> <span data-ttu-id="6e006-169">Odpovídá částečné třídy generované entity framework, který je obsažen v souboru DataModel.Designer.vb.</span><span class="sxs-lookup"><span data-stu-id="6e006-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="6e006-170">V současné době rozhraní .NET framework nepodporuje částečné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6e006-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="6e006-171">Proto neexistuje žádný způsob, jak použít atributy validátoru na vlastnosti třídy Movie definované v souboru DataModel.Designer.vb použitím atributů validátoru na vlastnosti třídy Movie definované v souboru v **seznamu 4**.</span><span class="sxs-lookup"><span data-stu-id="6e006-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="6e006-172">Všimněte si, že movie částečná třída je zdobena MetadataType atribut, který odkazuje na MovieMetaData třídy.</span><span class="sxs-lookup"><span data-stu-id="6e006-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="6e006-173">Třída MovieMetaData obsahuje vlastnosti proxy vlastností třídy Movie.</span><span class="sxs-lookup"><span data-stu-id="6e006-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="6e006-174">Atributy validátoru jsou použity na vlastnosti třídy MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="6e006-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="6e006-175">Vlastnosti Title, Director a DateReleased jsou označeny jako požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6e006-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="6e006-176">Vlastnost Director musí být přiřazen řetězec, který obsahuje méně než 5 znaků.</span><span class="sxs-lookup"><span data-stu-id="6e006-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="6e006-177">Nakonec displayname atribut je použit a DateReleased vlastnost zobrazit chybovou zprávu, jako je "Datum Vydáno pole je požadováno."</span><span class="sxs-lookup"><span data-stu-id="6e006-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="6e006-178">místo chyby "Pole DateReleased je povinné."</span><span class="sxs-lookup"><span data-stu-id="6e006-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6e006-179">Všimněte si, že proxy vlastnosti ve třídě MovieMetaData nemusí představovat stejné typy jako odpovídající vlastnosti ve třídě Movie.</span><span class="sxs-lookup"><span data-stu-id="6e006-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="6e006-180">Například Director Vlastnost je vlastnost řetězce ve třídě Movie a vlastnost objektu ve třídě MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="6e006-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="6e006-181">Stránka na **obrázku 6** znázorňuje chybové zprávy vrácené při zadávání neplatných hodnot vlastností filmu.</span><span class="sxs-lookup"><span data-stu-id="6e006-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="6e006-182">**Obrázek 6**: Použití validátorů s rozhraním Entity Framework[(Klepnutím zobrazíte obrázek v plné velikosti)](validation-with-the-data-annotation-validators-vb/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="6e006-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="6e006-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="6e006-183">Summary</span></span>

<span data-ttu-id="6e006-184">V tomto kurzu jste se naučili, jak využít data poznámky model binder k provedení ověření v rámci ASP.NET aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="6e006-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="6e006-185">Jste se naučili používat různé typy atributů validátoru, jako jsou povinné a StringLength atributy.</span><span class="sxs-lookup"><span data-stu-id="6e006-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="6e006-186">Také jste se naučili používat tyto atributy při práci s rozhraním Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6e006-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6e006-187">Předchozí</span><span class="sxs-lookup"><span data-stu-id="6e006-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
