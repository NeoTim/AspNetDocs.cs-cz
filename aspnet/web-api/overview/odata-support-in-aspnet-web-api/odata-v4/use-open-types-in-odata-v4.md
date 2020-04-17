---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Otevřít typy v OData v4 s ASP.NET web API | Dokumenty společnosti Microsoft
author: rick-anderson
description: V OData v4 otevřený typ je strukturovaný typ, který obsahuje dynamické vlastnosti, kromě všech vlastností, které jsou deklarovány v definici typu. Otevřít...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543727"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="6050f-104">Otevřít typy v OData v4 s ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6050f-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="6050f-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6050f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6050f-106">V OData v4 otevřený *typ* je strukturovaný typ, který obsahuje dynamické vlastnosti, kromě všech vlastností, které jsou deklarovány v definici typu.</span><span class="sxs-lookup"><span data-stu-id="6050f-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="6050f-107">Otevřené typy umožňují přidat flexibilitu datových modelů.</span><span class="sxs-lookup"><span data-stu-id="6050f-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="6050f-108">Tento kurz ukazuje, jak používat otevřené typy v ASP.NET web API OData.</span><span class="sxs-lookup"><span data-stu-id="6050f-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="6050f-109">Tento kurz předpokládá, že již víte, jak vytvořit koncový bod OData v ASP.NET webovérozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6050f-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="6050f-110">Pokud ne, začněte nejprve [čtením Vytvořit koncový bod OData v4.](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="6050f-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6050f-111">Verze softwaru použité v kurzu</span><span class="sxs-lookup"><span data-stu-id="6050f-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6050f-112">Webové rozhraní API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="6050f-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="6050f-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="6050f-113">OData v4</span></span>

<span data-ttu-id="6050f-114">Za prvé, některé OData terminologie:</span><span class="sxs-lookup"><span data-stu-id="6050f-114">First, some OData terminology:</span></span>

- <span data-ttu-id="6050f-115">Typ entity: Strukturovaný typ s klíčem.</span><span class="sxs-lookup"><span data-stu-id="6050f-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="6050f-116">Komplexní typ: Strukturovaný typ bez klíče.</span><span class="sxs-lookup"><span data-stu-id="6050f-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="6050f-117">Otevřený typ: Typ s dynamickými vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="6050f-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="6050f-118">Typy entit i složité typy mohou být otevřené.</span><span class="sxs-lookup"><span data-stu-id="6050f-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="6050f-119">Hodnota dynamické vlastnosti může být primitivní typ, komplexní typ nebo typ výčtu; nebo sbírku některého z těchto typů.</span><span class="sxs-lookup"><span data-stu-id="6050f-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="6050f-120">Další informace o otevřených typech naleznete ve [specifikaci OData v4](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="6050f-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="6050f-121">Instalace webových knihoven OData</span><span class="sxs-lookup"><span data-stu-id="6050f-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="6050f-122">Pomocí Správce balíčků NuGet nainstalujte nejnovější knihovny OData webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6050f-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="6050f-123">Z okna Konzoly správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="6050f-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="6050f-124">Definování typů CLR</span><span class="sxs-lookup"><span data-stu-id="6050f-124">Define the CLR Types</span></span>

<span data-ttu-id="6050f-125">Začněte definováním modelů EDM jako typů CLR.</span><span class="sxs-lookup"><span data-stu-id="6050f-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="6050f-126">Při vytvoření datového modelu entity (EDM)</span><span class="sxs-lookup"><span data-stu-id="6050f-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="6050f-127">`Category`je typ výčtu.</span><span class="sxs-lookup"><span data-stu-id="6050f-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="6050f-128">`Address`je komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="6050f-128">`Address` is a complex type.</span></span> <span data-ttu-id="6050f-129">(Nemá klíč, takže se nejedná o typ entity.)</span><span class="sxs-lookup"><span data-stu-id="6050f-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="6050f-130">`Customer`je typ entity.</span><span class="sxs-lookup"><span data-stu-id="6050f-130">`Customer` is an entity type.</span></span> <span data-ttu-id="6050f-131">(Má klíč.)</span><span class="sxs-lookup"><span data-stu-id="6050f-131">(It has a key.)</span></span>
- <span data-ttu-id="6050f-132">`Press`je otevřený komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="6050f-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="6050f-133">`Book`je otevřený typ entity.</span><span class="sxs-lookup"><span data-stu-id="6050f-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="6050f-134">Chcete-li vytvořit otevřený typ, musí mít typ `IDictionary<string, object>`CLR vlastnost typu , která obsahuje dynamické vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6050f-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="6050f-135">Sestavení modelu EDM</span><span class="sxs-lookup"><span data-stu-id="6050f-135">Build the EDM Model</span></span>

<span data-ttu-id="6050f-136">Pokud použijete **ODataConventionModelBuilder** k vytvoření `Press` `Book` EDM a jsou automaticky přidány jako `IDictionary<string, object>` otevřené typy, na základě přítomnosti vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6050f-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="6050f-137">Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="6050f-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="6050f-138">Přidání řadiče OData</span><span class="sxs-lookup"><span data-stu-id="6050f-138">Add an OData Controller</span></span>

<span data-ttu-id="6050f-139">Dále přidejte řadič OData.</span><span class="sxs-lookup"><span data-stu-id="6050f-139">Next, add an OData controller.</span></span> <span data-ttu-id="6050f-140">Pro účely tohoto kurzu použijeme zjednodušený řadič, který podporuje pouze požadavky GET a POST a používá seznam v paměti k ukládání entit.</span><span class="sxs-lookup"><span data-stu-id="6050f-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="6050f-141">Všimněte si, že první `Book` instance nemá žádné dynamické vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6050f-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="6050f-142">Druhá `Book` instance má následující dynamické vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="6050f-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="6050f-143">"Publikováno": Primitivní typ</span><span class="sxs-lookup"><span data-stu-id="6050f-143">"Published": Primitive type</span></span>
- <span data-ttu-id="6050f-144">"Autoři": Kolekce primitivních typů</span><span class="sxs-lookup"><span data-stu-id="6050f-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="6050f-145">"OtherCategories": Kolekce typů výčtu.</span><span class="sxs-lookup"><span data-stu-id="6050f-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="6050f-146">`Press` Vlastnost této `Book` instance má také následující dynamické vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="6050f-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="6050f-147">"Blog": Primitivní typ</span><span class="sxs-lookup"><span data-stu-id="6050f-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="6050f-148">"Adresa": Komplexní typ</span><span class="sxs-lookup"><span data-stu-id="6050f-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="6050f-149">Dotaz na metadata</span><span class="sxs-lookup"><span data-stu-id="6050f-149">Query the Metadata</span></span>

<span data-ttu-id="6050f-150">Chcete-li získat dokument metadat OData, `~/$metadata`odešlete požadavek GET společnosti .</span><span class="sxs-lookup"><span data-stu-id="6050f-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="6050f-151">Tělo odpovědi by mělo vypadat podobně jako toto:</span><span class="sxs-lookup"><span data-stu-id="6050f-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="6050f-152">Z dokumentu metadat vidíte, že:</span><span class="sxs-lookup"><span data-stu-id="6050f-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="6050f-153">`Book` Pro `Press` a typy je hodnota `OpenType` atributu true.</span><span class="sxs-lookup"><span data-stu-id="6050f-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="6050f-154">A `Customer` `Address` typy nemají tento atribut.</span><span class="sxs-lookup"><span data-stu-id="6050f-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="6050f-155">Typ `Book` entity má tři deklarované vlastnosti: ISBN, Title a Press.</span><span class="sxs-lookup"><span data-stu-id="6050f-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="6050f-156">Metadata OData nezahrnuje `Book.Properties` vlastnost z třídy CLR.</span><span class="sxs-lookup"><span data-stu-id="6050f-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="6050f-157">Podobně `Press` komplexní typ má pouze dvě deklarované vlastnosti: Name a Category.</span><span class="sxs-lookup"><span data-stu-id="6050f-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="6050f-158">Metadata nezahrnuje `Press.DynamicProperties` vlastnost z clr třídy.</span><span class="sxs-lookup"><span data-stu-id="6050f-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="6050f-159">Dotaz na entitu</span><span class="sxs-lookup"><span data-stu-id="6050f-159">Query an Entity</span></span>

<span data-ttu-id="6050f-160">Chcete-li získat knihu s ISBN rovná "978-0-7356-7942-9", pošlete žádost GET na `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="6050f-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="6050f-161">Tělo odpovědi by mělo vypadat podobně jako následující.</span><span class="sxs-lookup"><span data-stu-id="6050f-161">The response body should look similar to the following.</span></span> <span data-ttu-id="6050f-162">(Odsazeno, aby bylo čitelnější.)</span><span class="sxs-lookup"><span data-stu-id="6050f-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="6050f-163">Všimněte si, že dynamické vlastnosti jsou zahrnuty v souladu s deklarované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6050f-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="6050f-164">ZAÚČTOVAT entitu</span><span class="sxs-lookup"><span data-stu-id="6050f-164">POST an Entity</span></span>

<span data-ttu-id="6050f-165">Chcete-li přidat entitu Kniha, odešlete požadavek POST společnosti `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="6050f-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="6050f-166">Klient může nastavit dynamické vlastnosti v datové části požadavku.</span><span class="sxs-lookup"><span data-stu-id="6050f-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="6050f-167">Zde je příklad požadavku.</span><span class="sxs-lookup"><span data-stu-id="6050f-167">Here is an example request.</span></span> <span data-ttu-id="6050f-168">Všimněte si vlastností "Cena" a "Publikováno".</span><span class="sxs-lookup"><span data-stu-id="6050f-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="6050f-169">Pokud nastavíte zarážku v metodě řadiče, uvidíte, že webové rozhraní API přidalo tyto vlastnosti do slovníku. `Properties`</span><span class="sxs-lookup"><span data-stu-id="6050f-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="6050f-170">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="6050f-170">Additional Resources</span></span>

[<span data-ttu-id="6050f-171">Ukázka otevřeného typu OData</span><span class="sxs-lookup"><span data-stu-id="6050f-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
