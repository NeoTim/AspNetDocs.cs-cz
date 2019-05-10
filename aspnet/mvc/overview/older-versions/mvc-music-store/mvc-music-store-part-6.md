---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 'Část 6: Používání datových poznámek k ověření modelu | Dokumentace Microsoftu'
author: jongalloway
description: V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store. 6. část se věnuje anotacemi dat pro Model V...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129659"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="b05a7-104">Část 6: Používání datových poznámek k ověření modelu</span><span class="sxs-lookup"><span data-stu-id="b05a7-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="b05a7-105">podle [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="b05a7-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b05a7-106">MVC Music Store jde o kurz, který se seznámíte, podrobné postupy pro vývoj pro web pomocí ASP.NET MVC a sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b05a7-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b05a7-107">Music Store MVC je jednoduché ukázku implementace úložiště prodává hudebních alb online, který implementuje správu základního webu, přihlášení uživatele a nákupního košíku funkce.</span><span class="sxs-lookup"><span data-stu-id="b05a7-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b05a7-108">V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store.</span><span class="sxs-lookup"><span data-stu-id="b05a7-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b05a7-109">6. část se věnuje datových poznámek k ověření modelu.</span><span class="sxs-lookup"><span data-stu-id="b05a7-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="b05a7-110">Máme závažný problém s naší vytvořit a upravit formuláři: Nejedná se žádné ověření.</span><span class="sxs-lookup"><span data-stu-id="b05a7-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="b05a7-111">Můžeme udělat kroky, jako je nechat prázdné povinná pole nebo typ písmena v poli pro cenu a první chyba, kterou uvidíme se z databáze.</span><span class="sxs-lookup"><span data-stu-id="b05a7-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="b05a7-112">Jsme můžete snadno přidat ověření pro naši aplikaci tak, že přidáte datových poznámek k naší tříd modelu.</span><span class="sxs-lookup"><span data-stu-id="b05a7-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="b05a7-113">Datové poznámky umožňují nám pro popis pravidla, která chceme, aby u našich vlastnosti modelu a ASP.NET MVC se postará o vynucení a zobrazení příslušné zprávy pro naše uživatele.</span><span class="sxs-lookup"><span data-stu-id="b05a7-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="b05a7-114">Přidání ověřování do našich alba formulářů</span><span class="sxs-lookup"><span data-stu-id="b05a7-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="b05a7-115">Použijeme následující atributy dat. Poznámka:</span><span class="sxs-lookup"><span data-stu-id="b05a7-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="b05a7-116">**Požadované** – označuje, že vlastnost je povinné pole.</span><span class="sxs-lookup"><span data-stu-id="b05a7-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="b05a7-117">**DisplayName** – definuje text jsme má být použit na pole formuláře a ověřovacích zpráv</span><span class="sxs-lookup"><span data-stu-id="b05a7-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="b05a7-118">**StringLength** – definuje maximální délku pole řetězce</span><span class="sxs-lookup"><span data-stu-id="b05a7-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="b05a7-119">**Rozsah** – poskytuje maximální a minimální hodnoty pro číselné pole</span><span class="sxs-lookup"><span data-stu-id="b05a7-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="b05a7-120">**Vytvoření vazby** – obsahuje pole, které chcete vyloučit nebo zahrnout při vytváření vazby hodnoty parametru nebo formuláře na vlastnosti modelu</span><span class="sxs-lookup"><span data-stu-id="b05a7-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="b05a7-121">**ScaffoldColumn** – umožňuje skrýt pole z editoru formuláře</span><span class="sxs-lookup"><span data-stu-id="b05a7-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="b05a7-122">*Poznámka: Další informace o ověření modelu pomocí atributů dat poznámky v dokumentaci MSDN na*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="b05a7-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="b05a7-123">Otevřete třídu alba a přidejte následující *pomocí* příkazy.</span><span class="sxs-lookup"><span data-stu-id="b05a7-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="b05a7-124">Dále aktualizujte vlastnosti, které chcete přidat atributy zobrazení a ověření, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="b05a7-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="b05a7-125">Když jsme už máte, jste změnili jsme taky žánr a interpreta virtuálních vlastností.</span><span class="sxs-lookup"><span data-stu-id="b05a7-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="b05a7-126">Díky rozhraní Entity Framework pro opožděné načtení je podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="b05a7-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="b05a7-127">Po těchto atributů s přidá náš model alb, naše vytvořit a Upravit obrazovku okamžitě začne ověřování polí a pomocí zobrazované názvy jsme zvolili (například alba obrázky místo adresu Url AlbumArtUrl).</span><span class="sxs-lookup"><span data-stu-id="b05a7-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="b05a7-128">Spusťte aplikaci a přejděte do /StoreManager/Create.</span><span class="sxs-lookup"><span data-stu-id="b05a7-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="b05a7-129">V dalším kroku budete věcí některé ověřovací pravidla.</span><span class="sxs-lookup"><span data-stu-id="b05a7-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="b05a7-130">Zadejte cenu 0 a nechte prázdný název.</span><span class="sxs-lookup"><span data-stu-id="b05a7-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="b05a7-131">Když klikneme na tlačítka pro vytvoření, uvidíme formuláře, zobrazí se chybové zprávy ověření na zobrazení, která pole nevyhovuje ověřovacích pravidel, že jsme definovali.</span><span class="sxs-lookup"><span data-stu-id="b05a7-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="b05a7-132">Testování ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="b05a7-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="b05a7-133">Ověřování na straně serveru je velmi důležité z pohledu aplikace, protože uživatelé mohou obejít ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="b05a7-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="b05a7-134">Webové formuláře, implementující pouze ověření na straně serveru ale vykazuje tři významné problémy.</span><span class="sxs-lookup"><span data-stu-id="b05a7-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="b05a7-135">Uživatel má počkat pro formulář k publikování, ověřit na serveru a pro odpověď k odeslání do svého prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b05a7-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="b05a7-136">Uživatel nezíská okamžitou zpětnou vazbu, když neopraví pole tak, aby teď projde ověřovacím pravidlům.</span><span class="sxs-lookup"><span data-stu-id="b05a7-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="b05a7-137">Můžeme se plýtvání prostředky serveru k provedení ověření logic namísto využití webového prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b05a7-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="b05a7-138">Naštěstí šablony vygenerované uživatelské rozhraní ASP.NET MVC 3 mají na straně klienta ověření integrované vyžadující žádné další kroky, které jsou jakýmkoli způsobem.</span><span class="sxs-lookup"><span data-stu-id="b05a7-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="b05a7-139">Zadáte jedno písmeno v poli s názvem splňuje požadavky ověřování, tak ověření zprávy se okamžitě odebere.</span><span class="sxs-lookup"><span data-stu-id="b05a7-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="b05a7-140">[Předchozí](mvc-music-store-part-5.md)
> [další](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b05a7-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
