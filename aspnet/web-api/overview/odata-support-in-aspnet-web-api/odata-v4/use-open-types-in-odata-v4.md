---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Otevřete typy v OData v4 s rozhraním ASP.NET Web API | Dokumentace Microsoftu
author: microsoft
description: V OData v4 je otevřený typ strukturovaný typ, který obsahuje dynamické vlastnosti, kromě všechny vlastnosti, které jsou deklarovány v definici typu. Otevřete...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108465"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Otevřete typy v OData v4 s rozhraním ASP.NET Web API

by [Microsoft](https://github.com/microsoft)

> V OData v4 *otevřený typ.* strukturovaný typ, který obsahuje dynamické vlastnosti, kromě všechny vlastnosti, které jsou deklarovány v definici typu. Otevřené typy umožňují zvýšit flexibilitu datových modelů. Tento kurz ukazuje, jak používat otevřené typy v ASP.NET Web API OData.
> 
> Tento kurz předpokládá, že už víte, jak vytvořit koncový bod OData v rozhraní ASP.NET Web API. Pokud ne, začněte tím, že čtení [vytvoření koncového bodu OData v4](create-an-odata-v4-endpoint.md) první.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>V tomto kurzu použili verze softwaru
> 
> 
> - Web API OData 5.3
> - OData v4

První, některé OData terminologie:

- Typ entity: Strukturovaný typ. s klíčem.
- Komplexní typ: Strukturovaný typ. bez klíče.
- Otevřený typ: Typ s dynamických vlastností. Typy entit a komplexní typy možné otevřít.

Hodnotu dynamické vlastnosti může být primitivní typ, komplexního typu nebo typu výčtu nebo jakýkoli z těchto typů kolekce. Další informace o typech otevřít, najdete v článku [specifikace v4 pracovní verze protokolu OData](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Instalace knihoven OData Web

Použití Správce balíčků NuGet k instalaci nejnovějších knihoven Web API OData. Z okna konzoly Správce balíčků:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definování typů CLR

Začněte tím, že definice modelu EDM jako typy CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Vytvoření Entity Data Model (EDM)

- `Category` je typ výčtu.
- `Address` je komplexního typu. (Nemá klíč, takže není typem entity.)
- `Customer` je typ entity. (Nemá klíč.)
- `Press` je otevřít komplexního typu.
- `Book` je typu open entity.

Chcete-li vytvořit otevřený typ, typ CLR musí mít zadanou vlastnost typu `IDictionary<string, object>`, který obsahuje dynamických vlastností.

## <a name="build-the-edm-model"></a>Sestavení modelu EDM

Pokud používáte **ODataConventionModelBuilder** k vytvoření modelu EDM `Press` a `Book` jsou automaticky přidány jako typy open, podle přítomnosti `IDictionary<string, object>` vlastnost.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Můžete také sestavit EDM explicitně, pomocí **Tvůrce ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Přidat kontroler OData

V dalším kroku přidáte kontroler OData. Pro účely tohoto kurzu používáme zjednodušený kontroler, podporuje jenom získat po požadavků a přehledu v paměti používá k uložení entity.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Všimněte si, že první `Book` instance nemá žádné dynamické vlastnosti. Druhá `Book` instance má následující dynamické vlastnosti:

- "Publikováno": primitivní typ
- "Authors": Kolekce primitivních typů
- "OtherCategories": Kolekce typů výčtu.

Také `Press` vlastnost, která `Book` instance má následující dynamické vlastnosti:

- "Blog": primitivní typ
- "Address": komplexní typ

## <a name="query-the-metadata"></a>Dotaz Metadata

K získání dokumentu metadata OData, odeslat požadavek GET na `~/$metadata`. Tělo odpovědi by měl vypadat nějak takto:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Dokument metadat uvidíte, které:

- Pro `Book` a `Press` zadá hodnotu `OpenType` atribut má hodnotu true. `Customer` a `Address` typy nemají tento atribut.
- `Book` Typ entity má tři vlastnosti prohlášené: ISBN, název a stiskněte klávesu. OData metadata se nenachází `Book.Properties` vlastnost z třídy CLR.
- Podobně platí `Press` komplexní typ má jenom dvě deklarované vlastnosti: Název a kategorie. Metadata nezahrnují `Press.DynamicProperties` vlastnost z třídy CLR.

## <a name="query-an-entity"></a>Dotazování Entity

Chcete-li získat knihu s ISBN rovno "978-0-7356-7942-9", odešlete požadavek GET na `~/Books('978-0-7356-7942-9')`. Tělo odpovědi by měl vypadat nějak takto. (Chcete-li lépe čitelný odsazena.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Všimněte si, že dynamické vlastnosti jsou zahrnuty vložené pomocí vlastnosti prohlášené.

## <a name="post-an-entity"></a>PŘÍSPĚVEK Entity

Přidání entity knihy, odeslat požadavek POST do `~/Books`. Klienta můžete nastavit dynamické vlastnosti datové části požadavku.

Tady je příklad žádosti. Všimněte si vlastnosti "Price" a "Publikováno".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Pokud nastavíte zarážku v metodě kontroleru, uvidíte, že webové rozhraní API přidá vlastnosti tak, aby `Properties` slovníku.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Další prostředky

[Typ vzorku OData Open](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
