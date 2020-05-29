---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Zahrnutí v OData v4 pomocí webového rozhraní API 2,2 | Microsoft Docs
author: rick-anderson
description: Obvykle by entita mohla být k dispozici pouze v případě, že byla zapouzdřena v sadě entit. OData v4 ale nabízí dvě další možnosti, singleton a Con...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173001"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="9ff15-104">Zahrnutí v OData v4 pomocí webového rozhraní API 2,2</span><span class="sxs-lookup"><span data-stu-id="9ff15-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="9ff15-105">od Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="9ff15-105">by Jinfu Tan</span></span>

> <span data-ttu-id="9ff15-106">Obvykle by entita mohla být k dispozici pouze v případě, že byla zapouzdřena v sadě entit.</span><span class="sxs-lookup"><span data-stu-id="9ff15-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="9ff15-107">OData v4 ale nabízí dvě další možnosti, singleton a omezení, z nichž WebAPI 2,2 podporuje.</span><span class="sxs-lookup"><span data-stu-id="9ff15-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="9ff15-108">V tomto tématu se dozvíte, jak definovat omezení v koncovém bodu OData v WebApi 2,2.</span><span class="sxs-lookup"><span data-stu-id="9ff15-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="9ff15-109">Další informace o omezení najdete v tématu [omezení se dokoná s OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span><span class="sxs-lookup"><span data-stu-id="9ff15-109">For more information about containment, see [Containment is coming with OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span></span> <span data-ttu-id="9ff15-110">Informace o vytvoření koncového bodu OData v4 ve webovém rozhraní API najdete v tématu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní api ASP.NET 2,2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9ff15-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="9ff15-111">Nejprve vytvoříme model domény s omezením ve službě OData pomocí tohoto datového modelu:</span><span class="sxs-lookup"><span data-stu-id="9ff15-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![Datový model](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="9ff15-113">Účet obsahuje mnoho PaymentInstruments (PI), ale nedefinujeme sadu entit pro PI.</span><span class="sxs-lookup"><span data-stu-id="9ff15-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="9ff15-114">Místo toho je k PIs možné přihlédnout jenom prostřednictvím účtu.</span><span class="sxs-lookup"><span data-stu-id="9ff15-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="9ff15-115">Řešení používané v tomto tématu si můžete stáhnout z [webu CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span><span class="sxs-lookup"><span data-stu-id="9ff15-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="9ff15-116">Definování datového modelu</span><span class="sxs-lookup"><span data-stu-id="9ff15-116">Defining the data model</span></span>

1. <span data-ttu-id="9ff15-117">Definujte typy CLR.</span><span class="sxs-lookup"><span data-stu-id="9ff15-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="9ff15-118">`Contained`Atribut se používá pro navigační vlastnosti zahrnutí.</span><span class="sxs-lookup"><span data-stu-id="9ff15-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="9ff15-119">Vygenerujte model EDM na základě typů CLR.</span><span class="sxs-lookup"><span data-stu-id="9ff15-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="9ff15-120">`ODataConventionModelBuilder`Bude zpracovávat vytváření modelu EDM, pokud `Contained` je atribut přidán do odpovídající navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ff15-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="9ff15-121">Pokud je vlastnost typem kolekce, vytvoří se `GetCount(string NameContains)` i funkce.</span><span class="sxs-lookup"><span data-stu-id="9ff15-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="9ff15-122">Vygenerovaná metadata budou vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9ff15-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="9ff15-123">`ContainsTarget`Atribut označuje, že navigační vlastnost je omezení.</span><span class="sxs-lookup"><span data-stu-id="9ff15-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="9ff15-124">Definovat nadřazený kontroler sad entit</span><span class="sxs-lookup"><span data-stu-id="9ff15-124">Define the containing entity set controller</span></span>

<span data-ttu-id="9ff15-125">Obsažené entity nemají svůj vlastní kontroler; akce je definována v nadřazeném řadiči sady entit.</span><span class="sxs-lookup"><span data-stu-id="9ff15-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="9ff15-126">V této ukázce je k dispozici AccountsController, ale ne PaymentInstrumentsController.</span><span class="sxs-lookup"><span data-stu-id="9ff15-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="9ff15-127">Pokud je cesta OData 4 nebo více segmentů, funguje pouze směrování atributů, například `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` ve výše uvedeném řadiči.</span><span class="sxs-lookup"><span data-stu-id="9ff15-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="9ff15-128">V opačném případě funguje atribut i konvenční směrování: například, `GetPayInPIs(int key)` odpovídá `GET ~/Accounts(1)/PayinPIs` .</span><span class="sxs-lookup"><span data-stu-id="9ff15-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="9ff15-129">*Díky Leo hu pro původní obsah tohoto článku.*</span><span class="sxs-lookup"><span data-stu-id="9ff15-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
