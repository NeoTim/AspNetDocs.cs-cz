---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Zahrnutí v OData v4 použití rozhraní Web API 2.2 | Dokumentace Microsoftu
author: rick-anderson
description: Tradičně entita může přistupovat pouze pokud byly zapouzdřený v sadu entit. Ale OData v4 poskytuje dvě další možnosti, jednotlivý prvek a Con...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: fed55a4bf01e82af5167018f03e28a6274fcda78
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382196"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="50522-104">Zahrnutí v OData v4 použití rozhraní Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="50522-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="50522-105">podle Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="50522-105">by Jinfu Tan</span></span>

> <span data-ttu-id="50522-106">Tradičně entita může přistupovat pouze pokud byly zapouzdřený v sadu entit.</span><span class="sxs-lookup"><span data-stu-id="50522-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="50522-107">Ale OData v4 poskytuje dvě další možnosti, jednotlivý prvek a členství ve skupině, které podporuje WebAPI 2.2.</span><span class="sxs-lookup"><span data-stu-id="50522-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="50522-108">Toto téma ukazuje, jak definovat členství ve skupině v koncový bod OData v WebApi 2.2.</span><span class="sxs-lookup"><span data-stu-id="50522-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="50522-109">Další informace o členství ve skupině najdete v tématu [členství ve skupině se chystá pro OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span><span class="sxs-lookup"><span data-stu-id="50522-109">For more information about containment, see [Containment is coming with OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx).</span></span> <span data-ttu-id="50522-110">Vytvoření koncového bodu OData V4 v rozhraní Web API najdete v tématu [vytvořit OData v4 koncový bod pomocí rozhraní ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="50522-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="50522-111">Nejprve vytvoříme doménový model členství ve skupině služby OData, pomocí tohoto modelu dat:</span><span class="sxs-lookup"><span data-stu-id="50522-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![Datový model](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="50522-113">Účet obsahuje mnoho PaymentInstruments (PÍ), ale není definujeme sadu pro na PI entit.</span><span class="sxs-lookup"><span data-stu-id="50522-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="50522-114">Místo toho instrukce pro zpracování je přístupný pouze prostřednictvím účtu.</span><span class="sxs-lookup"><span data-stu-id="50522-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="50522-115">Řešení použité v tomto tématu si můžete stáhnout [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span><span class="sxs-lookup"><span data-stu-id="50522-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="50522-116">Definování datového modelu</span><span class="sxs-lookup"><span data-stu-id="50522-116">Defining the data model</span></span>

1. <span data-ttu-id="50522-117">Definování typů CLR.</span><span class="sxs-lookup"><span data-stu-id="50522-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="50522-118">`Contained` Atribut se používá pro zahrnutí navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="50522-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="50522-119">Generovat model EDM založený na typy CLR.</span><span class="sxs-lookup"><span data-stu-id="50522-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="50522-120">`ODataConventionModelBuilder` Bude zpracovávat sestavení modelu EDM, pokud `Contained` přidání atributu do odpovídající navigační vlastnost.</span><span class="sxs-lookup"><span data-stu-id="50522-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="50522-121">Pokud je vlastnost typu kolekce `GetCount(string NameContains)` funkce se také vytvoří.</span><span class="sxs-lookup"><span data-stu-id="50522-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="50522-122">Vygenerovaný metadata bude vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="50522-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="50522-123">`ContainsTarget` Atribut označuje, že je vlastnost navigace členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="50522-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="50522-124">Definování řadičem obsahující sadu entit</span><span class="sxs-lookup"><span data-stu-id="50522-124">Define the containing entity set controller</span></span>

<span data-ttu-id="50522-125">Omezením entity nemají své vlastní kontroler; akce je definované v kontroleru obsahující sadu entit.</span><span class="sxs-lookup"><span data-stu-id="50522-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="50522-126">V této ukázce je AccountsController, ale žádné PaymentInstrumentsController.</span><span class="sxs-lookup"><span data-stu-id="50522-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="50522-127">Pokud cestu OData je 4 nebo více segmentů, pouze atribut směrování funguje, jako například `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` ve výše uvedené kontroleru.</span><span class="sxs-lookup"><span data-stu-id="50522-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="50522-128">V opačném případě funguje atribut a konvenční směrování: například `GetPayInPIs(int key)` odpovídá `GET ~/Accounts(1)/PayinPIs`.</span><span class="sxs-lookup"><span data-stu-id="50522-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

*<span data-ttu-id="50522-129">Děkujeme, že k leo by patřil velice Hu původní obsah tohoto článku.</span><span class="sxs-lookup"><span data-stu-id="50522-129">Thanks to Leo Hu for the original content of this article.</span></span>*
