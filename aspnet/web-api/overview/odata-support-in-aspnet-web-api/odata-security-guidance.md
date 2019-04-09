---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Doprovodné materiály zabezpečení pro ASP.NET Web API 2 OData – ASP.NET 4.x
author: MikeWasson
description: Popisuje problémy se zabezpečením vzít v úvahu při zpřístupňování datovou sadu prostřednictvím prostředí OData pro ASP.NET Web API 2 technologie ASP.NET 4.x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393506"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>Doprovodné materiály zabezpečení pro ASP.NET Web API 2 OData

podle [Mike Wasson](https://github.com/MikeWasson)

Toto téma popisuje některé problémy se zabezpečením, které byste měli zvážit při zpřístupňování datovou sadu prostřednictvím prostředí OData pro ASP.NET Web API 2 technologie ASP.NET 4.x.

## <a name="edm-security"></a>Zabezpečení EDM

Sémantiku dotazů jsou založeny na entity data model (EDM), nikoli základní typy modelů. Může být z modelu EDM vyloučena určitá vlastnost a nebude viditelná pro dotaz. Předpokládejme například, že váš model obsahuje typ zaměstnance s vlastností Salary. Můžete chtít vyloučit tuto vlastnost z modelu EDM skrýt od klientů.

Existují dva způsoby, jak být vyloučena určitá vlastnost z modelu EDM. Můžete nastavit **[IgnoreDataMember]** atribut na vlastnost ve třídě modelu:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

Můžete také odebrat vlastnost z modelu EDM prostřednictvím kódu programu:

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>Zabezpečení dotazu

Škodlivý nebo naivní klienta může být schopen vytvořit dotaz, který trvá velmi dlouho ke spuštění. V nejhorším případě může to narušit přístup k službě.

**[Queryable]** je atribut filtru akce, které analyzuje, ověří a použije dotaz. Filtr převede možnosti dotazu výrazu LINQ. Při vrácení kontroler OData **IQueryable** typ, **IQueryable** zprostředkovatele LINQ Převede výraz LINQ dotaz. Výkon proto závisí na zprostředkovatele LINQ, který se používá a také na konkrétní charakteristiky schéma datové sady nebo databáze.

Další informace o použití možnosti dotazu OData v rozhraní ASP.NET Web API najdete v tématu [podporuje možnosti dotazu OData](supporting-odata-query-options.md).

Pokud víte, že všichni klienti jsou důvěryhodné (například v podnikovém prostředí), nebo pokud vaše datová sada je malá, výkon dotazů, nemusí být problém. V opačném případě byste měli zvážit následující doporučení.

- Testování služby s různé dotazy a Profilovat databáze.
- Povolte stránkování řízených serverem, aby se zabránilo vrácení velké sady dat v jednom dotazu. Další informace najdete v tématu [stránkování Server-Driven](supporting-odata-query-options.md#server-paging). 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- Je třeba $filter a $orderby? Některé aplikace může dovolit klientským stránkování, $top a $skip, ale zakázat další možnosti dotazu. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- Zvažte omezení $orderby na vlastnosti v clusterovaném indexu. Řazení velkých dat bez clusterovaného indexu je pomalé. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- Maximální počet uzlů: **MaxNodeCount** vlastnost **[Queryable]** Nastaví maximální počtu uzlů, které jsou povoleny ve stromu syntaxe $filter. Výchozí hodnota je 100, ale můžete chtít nastavit nižší hodnotu, protože velký počet uzlů, může trvat dlouho. kompilace. To platí zejména pokud používáte LINQ to Objects (například LINQ dotazy na kolekce v paměti, ale bez použití zprostředkující zprostředkovatele LINQ). 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Zvažte zakázání funkce metoda any() a all(), protože to může být pomalé. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- Pokud jakékoli vlastnosti řetězce obsahují dlouhých řetězců&#8212;například popis produktu nebo blogu&#8212;zvažte zakázání funkce řetězec. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- Zvažte zákaz filtrování na navigační vlastnosti. Filtrování na navigační vlastnosti může mít za následek spojení, což může být pomalé, v závislosti na schématu databáze. Následující kód ukazuje validátor dotazu, který zabraňuje filtrování na navigační vlastnosti. Další informace o dotazu validátory najdete v tématu [dotaz ověření](supporting-odata-query-options.md#query-validation). 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- Zvažte omezení $filter dotazy napsáním validátor, který je přizpůsobený pro vaši databázi. Představte si třeba tyto dva dotazy: 

  - Všechna videa pomocí objektů actor, jejichž příjmení začíná "A".
  - Všechny filmy vydána v roce 1994.

    Pokud filmy jsou indexovány pomocí objektů actor, první dotaz může vyžadovat databázový stroj kontrolovat celý seznam videa. Zatímco druhý dotaz může být přijatelný, předpokládá filmy jsou indexovány pomocí rok vydání.

    Následující kód ukazuje validátor umožňuje filtrování podle vlastnosti "ReleaseYear" a "Title", ale žádné jiné vlastnosti.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- Obecně platí zvažte možnost $filter funkcích, které potřebujete. Pokud vaši klienti nepotřebují úplné expresivity $filter, můžete omezit povolené funkce.
