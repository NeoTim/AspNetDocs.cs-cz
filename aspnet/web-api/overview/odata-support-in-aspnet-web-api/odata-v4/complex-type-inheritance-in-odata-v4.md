---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Komplexní dědičnost typu v OData v4 s ASP.NET web API | Dokumenty společnosti Microsoft
author: rick-anderson
description: Podle specifikace OData v4 může komplexní typ dědit z jiného komplexního typu. (Komplexní typ je strukturovaný typ bez klíče.) Webové rozhraní API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543597"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="7a896-104">Komplexní dědičnost typu v OData v4 s ASP.NET webové rozhraní API</span><span class="sxs-lookup"><span data-stu-id="7a896-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="7a896-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7a896-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7a896-106">Podle [specifikace](http://www.odata.org/documentation/odata-version-4-0/)OData v4 může komplexní typ dědit z jiného komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="7a896-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="7a896-107">(Komplexní *complex* typ je strukturovaný typ bez klíče.) Webové rozhraní API OData 5.3 podporuje komplexní dědičnost typů.</span><span class="sxs-lookup"><span data-stu-id="7a896-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="7a896-108">Toto téma ukazuje, jak vytvořit datový model entity (EDM) se složitými typy dědičnosti.</span><span class="sxs-lookup"><span data-stu-id="7a896-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="7a896-109">Úplný zdrojový kód naleznete v tématu [Ukázka dědičnosti komplexního typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="7a896-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7a896-110">Verze softwaru použité v kurzu</span><span class="sxs-lookup"><span data-stu-id="7a896-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7a896-111">Webové rozhraní API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="7a896-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="7a896-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="7a896-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="7a896-113">Hierarchie modelů</span><span class="sxs-lookup"><span data-stu-id="7a896-113">Model Hierarchy</span></span>

<span data-ttu-id="7a896-114">Pro ilustraci komplexní dědičnosti typů použijeme následující hierarchii tříd.</span><span class="sxs-lookup"><span data-stu-id="7a896-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="7a896-115">`Shape`je abstraktní komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="7a896-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="7a896-116">`Rectangle`, `Triangle`a `Circle` jsou složité typy `Shape`odvozené z , a `RoundRectangle` pochází z `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="7a896-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="7a896-117">`Window`je typ entity a `Shape` obsahuje instanci.</span><span class="sxs-lookup"><span data-stu-id="7a896-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="7a896-118">Zde jsou třídy CLR, které definují tyto typy.</span><span class="sxs-lookup"><span data-stu-id="7a896-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="7a896-119">Sestavení modelu EDM</span><span class="sxs-lookup"><span data-stu-id="7a896-119">Build the EDM Model</span></span>

<span data-ttu-id="7a896-120">Chcete-li vytvořit EDM, můžete použít **ODataConventionModelBuilder**, který odvodí vztahy dědičnosti z clr typy.</span><span class="sxs-lookup"><span data-stu-id="7a896-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="7a896-121">Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="7a896-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="7a896-122">To trvá více kódu, ale poskytuje větší kontrolu nad EDM.</span><span class="sxs-lookup"><span data-stu-id="7a896-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="7a896-123">Tyto dva příklady vytvořit stejné schéma EDM.</span><span class="sxs-lookup"><span data-stu-id="7a896-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="7a896-124">Dokument metadat</span><span class="sxs-lookup"><span data-stu-id="7a896-124">Metadata Document</span></span>

<span data-ttu-id="7a896-125">Zde je dokument metadat OData, který zobrazuje komplexní dědičnost typu.</span><span class="sxs-lookup"><span data-stu-id="7a896-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="7a896-126">Z dokumentu metadat vidíte, že:</span><span class="sxs-lookup"><span data-stu-id="7a896-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="7a896-127">Komplexní `Shape` typ je abstraktní.</span><span class="sxs-lookup"><span data-stu-id="7a896-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="7a896-128">Typ `Rectangle` `Triangle`, `Circle` a komplexní mají `Shape`základní typ .</span><span class="sxs-lookup"><span data-stu-id="7a896-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="7a896-129">Typ `RoundRectangle` má základní `Rectangle`typ .</span><span class="sxs-lookup"><span data-stu-id="7a896-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="7a896-130">Casting komplexní typy</span><span class="sxs-lookup"><span data-stu-id="7a896-130">Casting Complex Types</span></span>

<span data-ttu-id="7a896-131">Casting na složité typy je nyní podporována.</span><span class="sxs-lookup"><span data-stu-id="7a896-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="7a896-132">Například následující dotaz přetypování `Shape` `Rectangle`a do .</span><span class="sxs-lookup"><span data-stu-id="7a896-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="7a896-133">Zde je užitečné zatížení odezvy:</span><span class="sxs-lookup"><span data-stu-id="7a896-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
