---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Mapování uživatelů signalismu na připojení | Dokumenty společnosti Microsoft
author: bradygaster
description: Toto téma ukazuje, jak uchovávat informace o uživatelích a jejich připojeních. Patrick Fletcher pomohl napsat toto téma. Verze softwaru použité v tomto tématu...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676158"
---
# <a name="mapping-signalr-users-to-connections"></a>Mapování uživatelů knihovny SignalR na připojení

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma ukazuje, jak uchovávat informace o uživatelích a jejich připojeních.
>
> Patrick Fletcher pomohl napsat toto téma.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
>
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="introduction"></a>Úvod

Každý klient, který se připojuje k rozbočovači, předá jedinečné id připojení. Tuto hodnotu můžete `Context.ConnectionId` načíst ve vlastnosti kontextu centra. Pokud vaše aplikace potřebuje namapovat uživatele na id připojení a zachovat toto mapování, můžete použít jednu z následujících možností:

- [Zprostředkovatel ID uživatele (SignalR 2)](#IUserIdProvider)
- [Úložiště v paměti](#inmemory), například slovník
- [Skupina SignalR pro každého uživatele](#groups)
- [Trvalé externí úložiště](#database), například databázová tabulka nebo úložiště tabulek Azure

Každá z těchto implementací je uvedena v tomto tématu. Pomocí metody `OnConnected` `OnDisconnected`, `OnReconnected` a metody `Hub` třídy můžete sledovat stav připojení uživatele.

Nejlepší přístup pro vaši aplikaci závisí na:

- Počet webových serverů hostujících vaši aplikaci.
- Zda potřebujete získat seznam aktuálně připojených uživatelů.
- Zda potřebujete zachovat informace o skupině a uživateli při restartování aplikace nebo serveru.
- Zda je problém latence volání externího serveru.

V následující tabulce je uvedeno, který přístup funguje pro tyto aspekty.

|  | Více než jeden server | Získat seznam aktuálně připojených uživatelů | Zachovat informace po restartování | Optimální výkon |
| --- | --- | --- | --- | --- |
| Zprostředkovatel Uživatelské ID | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| V paměti |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Skupiny pro jednoho uživatele | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Trvalé, vnější | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>Zprostředkovatel IUserID

Tato funkce umožňuje uživatelům určit, co userId je založena na IRequest prostřednictvím nového rozhraní IUserIdProvider.

**Zprostředkovatel IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Ve výchozím nastavení bude existovat implementace, která `IPrincipal.Identity.Name` používá jako uživatelské jméno uživatele. Chcete-li to změnit, `IUserIdProvider` zaregistrujte implementaci s globálním hostitelem při spuštění aplikace:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

Z centra budete moci odesílat zprávy těmto uživatelům prostřednictvím následujícího rozhraní API:

**Odeslání zprávy konkrétnímu uživateli**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Úložiště v paměti

Následující příklady ukazují, jak zachovat informace o připojení a uživateli ve slovníku, který je uložen v paměti. Slovník používá k `HashSet` uložení ID připojení. Uživatel může mít kdykoli více než jedno připojení k aplikaci SignalR. Například uživatel, který je připojen prostřednictvím více zařízení nebo více než jednu kartu prohlížeče, by měl více než jedno id připojení.

Pokud se aplikace vypne, dojde ke ztrátě všech informací, ale budou znovu vyplněny, jakmile uživatelé znovu naváže připojení. Úložiště v paměti nefunguje, pokud vaše prostředí obsahuje více než jeden webový server, protože každý server by měl samostatnou kolekci připojení.

První příklad ukazuje třídu, která spravuje mapování uživatelů na připojení. Klíč pro HashSet bude jméno uživatele.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Následující příklad ukazuje, jak používat třídu mapování připojení z rozbočovače. Instance třídy je uložena v `_connections`názvu proměnné .

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Skupiny pro jednoho uživatele

Můžete vytvořit skupinu pro každého uživatele a potom odeslat zprávu do této skupiny, pokud chcete oslovit pouze tohoto uživatele. Název každé skupiny je jméno uživatele. Pokud má uživatel více než jedno připojení, každé id připojení je přidándo skupiny uživatele.

Neměli byste ručně odebrat uživatele ze skupiny, když se uživatel odpojí. Tato akce je automaticky provedena rozhraním SignalR.

Následující příklad ukazuje, jak implementovat skupiny pro jednoho uživatele.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Trvalé externí úložiště

Toto téma ukazuje, jak používat databázi nebo úložiště tabulek Azure pro ukládání informací o připojení. Tento přístup funguje, pokud máte více webových serverů, protože každý webový server může pracovat se stejným úložištěm dat. Pokud vaše webové servery přestanou fungovat `OnDisconnected` nebo se aplikace restartuje, metoda není volána. Proto je možné, že vaše úložiště dat bude mít záznamy pro ID připojení, které již nejsou platné. Chcete-li vyčistit tyto osamocené záznamy, můžete chtít zrušit platnost připojení, které bylo vytvořeno mimo časový rámec, který je relevantní pro vaši aplikaci. Příklady v této části zahrnují hodnotu pro sledování při vytvoření připojení, ale neukazují, jak vyčistit staré záznamy, protože to můžete chtít provést jako proces na pozadí.

### <a name="database"></a>databáze

Následující příklady ukazují, jak zachovat informace o připojení a uživateli v databázi. Můžete použít libovolnou technologii přístupu k datům; však v příkladu ukazuje, jak definovat modely pomocí entity Framework. Tyto modely entit odpovídají databázovým tabulkám a polím. Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.

První příklad ukazuje, jak definovat entitu uživatele, která může být přidružena k mnoha entitám připojení.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Potom z rozbočovače můžete sledovat stav každého připojení s níže uvedeným kódem.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure Table Storage

Následující příklad úložiště tabulky Azure je podobný příkladu databáze. Neobsahuje všechny informace, které byste potřebovali, abyste mohli začít se službou Azure Table Storage Service. Další informace naleznete v tématu [Jak používat úložiště tabulky z rozhraní .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

Následující příklad ukazuje entitu tabulky pro ukládání informací o připojení. Rozdělí data podle uživatelského jména a identifikuje každou entitu podle ID připojení, takže uživatel může mít kdykoli více připojení.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

V rozbočovači můžete sledovat stav připojení jednotlivých uživatelů.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
