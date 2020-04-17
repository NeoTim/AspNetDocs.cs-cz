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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Komplexní dědičnost typu v OData v4 s ASP.NET webové rozhraní API

podle [společnosti Microsoft](https://github.com/microsoft)

> Podle [specifikace](http://www.odata.org/documentation/odata-version-4-0/)OData v4 může komplexní typ dědit z jiného komplexního typu. (Komplexní *complex* typ je strukturovaný typ bez klíče.) Webové rozhraní API OData 5.3 podporuje komplexní dědičnost typů.
> 
> Toto téma ukazuje, jak vytvořit datový model entity (EDM) se složitými typy dědičnosti. Úplný zdrojový kód naleznete v tématu [Ukázka dědičnosti komplexního typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v kurzu
> 
> 
> - Webové rozhraní API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>Hierarchie modelů

Pro ilustraci komplexní dědičnosti typů použijeme následující hierarchii tříd.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`je abstraktní komplexní typ. `Rectangle`, `Triangle`a `Circle` jsou složité typy `Shape`odvozené z , a `RoundRectangle` pochází z `Rectangle`. `Window`je typ entity a `Shape` obsahuje instanci.

Zde jsou třídy CLR, které definují tyto typy.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Sestavení modelu EDM

Chcete-li vytvořit EDM, můžete použít **ODataConventionModelBuilder**, který odvodí vztahy dědičnosti z clr typy.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**. To trvá více kódu, ale poskytuje větší kontrolu nad EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Tyto dva příklady vytvořit stejné schéma EDM.

## <a name="metadata-document"></a>Dokument metadat

Zde je dokument metadat OData, který zobrazuje komplexní dědičnost typu.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Z dokumentu metadat vidíte, že:

- Komplexní `Shape` typ je abstraktní.
- Typ `Rectangle` `Triangle`, `Circle` a komplexní mají `Shape`základní typ .
- Typ `RoundRectangle` má základní `Rectangle`typ .

## <a name="casting-complex-types"></a>Casting komplexní typy

Casting na složité typy je nyní podporována. Například následující dotaz přetypování `Shape` `Rectangle`a do .

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Zde je užitečné zatížení odezvy:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
