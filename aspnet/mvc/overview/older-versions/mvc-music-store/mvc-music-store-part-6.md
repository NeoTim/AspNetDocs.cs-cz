---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6. část: použití datových poznámek pro ověření modelu | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 6 pokrývá použití datových poznámek pro model V...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044945"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="d8f50-104">Část 6: Používání datových poznámek k ověření modelu</span><span class="sxs-lookup"><span data-stu-id="d8f50-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="d8f50-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="d8f50-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="d8f50-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="d8f50-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="d8f50-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="d8f50-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="d8f50-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="d8f50-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="d8f50-109">Část 6 pokrývá použití datových poznámek pro ověřování modelu.</span><span class="sxs-lookup"><span data-stu-id="d8f50-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="d8f50-110">Máme velký problém s našimi formuláři pro vytváření a úpravy: neprovádí žádné ověření.</span><span class="sxs-lookup"><span data-stu-id="d8f50-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="d8f50-111">Můžeme dělat věci, jako je třeba ponechat povinná pole prázdná, nebo zadat písmena v poli Price a první chyba, kterou uvidíme z databáze.</span><span class="sxs-lookup"><span data-stu-id="d8f50-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="d8f50-112">Do naší aplikace můžeme snadno přidat ověřování tím, že do našich tříd modelů přidáte datové poznámky.</span><span class="sxs-lookup"><span data-stu-id="d8f50-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="d8f50-113">Poznámky k datům nám umožňují popsat pravidla, která chceme použít pro vlastnosti modelu, a ASP.NET MVC se postará o vynucování a zobrazování vhodných zpráv pro naše uživatele.</span><span class="sxs-lookup"><span data-stu-id="d8f50-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="d8f50-114">Přidání ověřování do našich formulářů alba</span><span class="sxs-lookup"><span data-stu-id="d8f50-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="d8f50-115">Použijeme následující atributy poznámky k datům:</span><span class="sxs-lookup"><span data-stu-id="d8f50-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="d8f50-116">**Required** – označuje, že vlastnost je povinné pole.</span><span class="sxs-lookup"><span data-stu-id="d8f50-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="d8f50-117">**DisplayName** – definuje text, který se má použít u polí formuláře a ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="d8f50-117">**DisplayName** – Defines the text to use on form fields and validation messages</span></span>
- <span data-ttu-id="d8f50-118">**StringLength** – definuje maximální délku pole řetězce.</span><span class="sxs-lookup"><span data-stu-id="d8f50-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="d8f50-119">**Rozsah** – poskytuje maximální a minimální hodnotu pro číselné pole.</span><span class="sxs-lookup"><span data-stu-id="d8f50-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="d8f50-120">**BIND** – vypíše pole, která se mají vyloučit nebo zahrnout, když jsou parametry vazby nebo hodnoty formulářů na vlastnosti modelu.</span><span class="sxs-lookup"><span data-stu-id="d8f50-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="d8f50-121">**ScaffoldColumn** – umožňuje skrývání polí z formulářů editoru.</span><span class="sxs-lookup"><span data-stu-id="d8f50-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="d8f50-122">*Poznámka: Další informace o ověřování modelu pomocí atributů datových poznámek najdete v dokumentaci MSDN na adrese*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="d8f50-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="d8f50-123">Otevřete třídu alba a přidejte následující příkazy *using* do horní části.</span><span class="sxs-lookup"><span data-stu-id="d8f50-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="d8f50-124">Dále aktualizujte vlastnosti tak, aby se přidaly atributy zobrazení a ověření, jak je vidět níže.</span><span class="sxs-lookup"><span data-stu-id="d8f50-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="d8f50-125">I když tam máme, změnili jsme také Žánr a umělec na virtuální vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d8f50-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="d8f50-126">To umožňuje Entity Framework opožděně načítat je podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="d8f50-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="d8f50-127">Po přidání těchto atributů do našeho modelu alba si naše obrazovka pro vytvoření a úpravu hned spustí ověřování polí a použití zobrazovaných názvů, které jsme zvolili (např. adresa URL alba alba místo AlbumArtUrl).</span><span class="sxs-lookup"><span data-stu-id="d8f50-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="d8f50-128">Spusťte aplikaci a přejděte do/StoreManager/Create.</span><span class="sxs-lookup"><span data-stu-id="d8f50-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="d8f50-129">Dále porušíme některá pravidla ověřování.</span><span class="sxs-lookup"><span data-stu-id="d8f50-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="d8f50-130">Zadejte cenu 0 a nechejte název prázdný.</span><span class="sxs-lookup"><span data-stu-id="d8f50-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="d8f50-131">Po kliknutí na tlačítko vytvořit se zobrazí formulář s chybovými zprávami ověřování, které zobrazují, která pole nesplňovala vámi definovaná pravidla ověřování.</span><span class="sxs-lookup"><span data-stu-id="d8f50-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="d8f50-132">Testování ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="d8f50-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="d8f50-133">Ověřování na straně serveru je velmi důležité z hlediska aplikace, protože uživatelé mohou obejít ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d8f50-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="d8f50-134">Formuláře webové stránky, které implementují pouze ověřování na straně serveru, však projeví tři významné problémy.</span><span class="sxs-lookup"><span data-stu-id="d8f50-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="d8f50-135">Uživatel musí počkat na publikování formuláře, jeho ověření na serveru a odeslání odpovědi do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="d8f50-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="d8f50-136">Uživatel nezíská okamžitou zpětnou vazbu, když opraví pole tak, aby nyní prošl pravidla ověřování.</span><span class="sxs-lookup"><span data-stu-id="d8f50-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="d8f50-137">Nepotřebujeme k provádění logiky ověřování místo využití prohlížeče uživatele prostředky serveru.</span><span class="sxs-lookup"><span data-stu-id="d8f50-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="d8f50-138">Naštěstí šablony uživatelského rozhraní ASP.NET MVC 3 obsahují integrované ověřování na straně klienta, které nevyžadují žádnou další práci.</span><span class="sxs-lookup"><span data-stu-id="d8f50-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="d8f50-139">Zadáním jednoho písmena v poli název splníte požadavky na ověření, takže se ověřovací zpráva okamžitě odebere.</span><span class="sxs-lookup"><span data-stu-id="d8f50-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="d8f50-140">[Předchozí](mvc-music-store-part-5.md) 
>  [Další](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="d8f50-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
