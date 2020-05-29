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
# <a name="containment-in-odata-v4-using-web-api-22"></a>Zahrnutí v OData v4 pomocí webového rozhraní API 2,2

od Jinfu Tan

> Obvykle by entita mohla být k dispozici pouze v případě, že byla zapouzdřena v sadě entit. OData v4 ale nabízí dvě další možnosti, singleton a omezení, z nichž WebAPI 2,2 podporuje.

V tomto tématu se dozvíte, jak definovat omezení v koncovém bodu OData v WebApi 2,2. Další informace o omezení najdete v tématu [omezení se dokoná s OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/). Informace o vytvoření koncového bodu OData v4 ve webovém rozhraní API najdete v tématu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní api ASP.NET 2,2](create-an-odata-v4-endpoint.md).

Nejprve vytvoříme model domény s omezením ve službě OData pomocí tohoto datového modelu:

![Datový model](odata-containment-in-web-api-22/_static/image1.png)

Účet obsahuje mnoho PaymentInstruments (PI), ale nedefinujeme sadu entit pro PI. Místo toho je k PIs možné přihlédnout jenom prostřednictvím účtu.

Řešení používané v tomto tématu si můžete stáhnout z [webu CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).

## <a name="defining-the-data-model"></a>Definování datového modelu

1. Definujte typy CLR.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`Atribut se používá pro navigační vlastnosti zahrnutí.
2. Vygenerujte model EDM na základě typů CLR.

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder`Bude zpracovávat vytváření modelu EDM, pokud `Contained` je atribut přidán do odpovídající navigační vlastnosti. Pokud je vlastnost typem kolekce, vytvoří se `GetCount(string NameContains)` i funkce.

    Vygenerovaná metadata budou vypadat takto:

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`Atribut označuje, že navigační vlastnost je omezení.

## <a name="define-the-containing-entity-set-controller"></a>Definovat nadřazený kontroler sad entit

Obsažené entity nemají svůj vlastní kontroler; akce je definována v nadřazeném řadiči sady entit. V této ukázce je k dispozici AccountsController, ale ne PaymentInstrumentsController.

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

Pokud je cesta OData 4 nebo více segmentů, funguje pouze směrování atributů, například `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` ve výše uvedeném řadiči. V opačném případě funguje atribut i konvenční směrování: například, `GetPayInPIs(int key)` odpovídá `GET ~/Accounts(1)/PayinPIs` .

*Díky Leo hu pro původní obsah tohoto článku.*
