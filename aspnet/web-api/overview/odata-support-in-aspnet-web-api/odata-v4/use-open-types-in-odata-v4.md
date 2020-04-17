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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Otevřít typy v OData v4 s ASP.NET Web API

podle [společnosti Microsoft](https://github.com/microsoft)

> V OData v4 otevřený *typ* je strukturovaný typ, který obsahuje dynamické vlastnosti, kromě všech vlastností, které jsou deklarovány v definici typu. Otevřené typy umožňují přidat flexibilitu datových modelů. Tento kurz ukazuje, jak používat otevřené typy v ASP.NET web API OData.
> 
> Tento kurz předpokládá, že již víte, jak vytvořit koncový bod OData v ASP.NET webovérozhraní API. Pokud ne, začněte nejprve [čtením Vytvořit koncový bod OData v4.](create-an-odata-v4-endpoint.md)
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v kurzu
> 
> 
> - Webové rozhraní API OData 5.3
> - OData v4

Za prvé, některé OData terminologie:

- Typ entity: Strukturovaný typ s klíčem.
- Komplexní typ: Strukturovaný typ bez klíče.
- Otevřený typ: Typ s dynamickými vlastnostmi. Typy entit i složité typy mohou být otevřené.

Hodnota dynamické vlastnosti může být primitivní typ, komplexní typ nebo typ výčtu; nebo sbírku některého z těchto typů. Další informace o otevřených typech naleznete ve [specifikaci OData v4](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Instalace webových knihoven OData

Pomocí Správce balíčků NuGet nainstalujte nejnovější knihovny OData webového rozhraní API. Z okna Konzoly správce balíčků:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definování typů CLR

Začněte definováním modelů EDM jako typů CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Při vytvoření datového modelu entity (EDM)

- `Category`je typ výčtu.
- `Address`je komplexní typ. (Nemá klíč, takže se nejedná o typ entity.)
- `Customer`je typ entity. (Má klíč.)
- `Press`je otevřený komplexní typ.
- `Book`je otevřený typ entity.

Chcete-li vytvořit otevřený typ, musí mít typ `IDictionary<string, object>`CLR vlastnost typu , která obsahuje dynamické vlastnosti.

## <a name="build-the-edm-model"></a>Sestavení modelu EDM

Pokud použijete **ODataConventionModelBuilder** k vytvoření `Press` `Book` EDM a jsou automaticky přidány jako `IDictionary<string, object>` otevřené typy, na základě přítomnosti vlastnosti.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Přidání řadiče OData

Dále přidejte řadič OData. Pro účely tohoto kurzu použijeme zjednodušený řadič, který podporuje pouze požadavky GET a POST a používá seznam v paměti k ukládání entit.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Všimněte si, že první `Book` instance nemá žádné dynamické vlastnosti. Druhá `Book` instance má následující dynamické vlastnosti:

- "Publikováno": Primitivní typ
- "Autoři": Kolekce primitivních typů
- "OtherCategories": Kolekce typů výčtu.

`Press` Vlastnost této `Book` instance má také následující dynamické vlastnosti:

- "Blog": Primitivní typ
- "Adresa": Komplexní typ

## <a name="query-the-metadata"></a>Dotaz na metadata

Chcete-li získat dokument metadat OData, `~/$metadata`odešlete požadavek GET společnosti . Tělo odpovědi by mělo vypadat podobně jako toto:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Z dokumentu metadat vidíte, že:

- `Book` Pro `Press` a typy je hodnota `OpenType` atributu true. A `Customer` `Address` typy nemají tento atribut.
- Typ `Book` entity má tři deklarované vlastnosti: ISBN, Title a Press. Metadata OData nezahrnuje `Book.Properties` vlastnost z třídy CLR.
- Podobně `Press` komplexní typ má pouze dvě deklarované vlastnosti: Name a Category. Metadata nezahrnuje `Press.DynamicProperties` vlastnost z clr třídy.

## <a name="query-an-entity"></a>Dotaz na entitu

Chcete-li získat knihu s ISBN rovná "978-0-7356-7942-9", pošlete žádost GET na `~/Books('978-0-7356-7942-9')`. Tělo odpovědi by mělo vypadat podobně jako následující. (Odsazeno, aby bylo čitelnější.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Všimněte si, že dynamické vlastnosti jsou zahrnuty v souladu s deklarované vlastnosti.

## <a name="post-an-entity"></a>ZAÚČTOVAT entitu

Chcete-li přidat entitu Kniha, odešlete požadavek POST společnosti `~/Books`. Klient může nastavit dynamické vlastnosti v datové části požadavku.

Zde je příklad požadavku. Všimněte si vlastností "Cena" a "Publikováno".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Pokud nastavíte zarážku v metodě řadiče, uvidíte, že webové rozhraní API přidalo tyto vlastnosti do slovníku. `Properties`

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Další zdroje

[Ukázka otevřeného typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
