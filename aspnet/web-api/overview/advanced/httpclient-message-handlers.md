---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Obslužné rutiny zpráv HttpClient v rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: Vytvoření obslužné rutiny vlastních zpráv pro ASP.NET Web API v ASP.NET 4.x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: bd52396064cd7007ee17705ba86b02aaf27cb4f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401722"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>Obslužné rutiny zpráv HttpClient ve webovém rozhraní API technologie ASP.NET

podle [Mike Wasson](https://github.com/MikeWasson)

A *obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.

Řada obslužné rutiny zpráv jsou obvykle zřetězen dohromady. První obslužná rutina požadavku HTTP, provádí nějaké zpracování a poskytuje k další obslužná rutina požadavku. V určitém okamžiku odpovědi se vytvoří a vrátí řetězem. Tento model se nazývá *delegování* obslužné rutiny.

![](httpclient-message-handlers/_static/image1.png)

Na straně klienta **HttpClient** třída používá obslužné rutiny zpráv pro zpracování žádostí. Je výchozí obslužnou rutinu **HttpClientHandler**, který odešle požadavek v síti a získá odpověď ze serveru. Obslužné rutiny vlastních zpráv můžete vložit do kanálu klienta:

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> Rozhraní ASP.NET Web API také používá obslužné rutiny zpráv na straně serveru. Další informace najdete v tématu [obslužné rutiny zpráv HTTP](http-message-handlers.md).


## <a name="custom-message-handlers"></a>Obslužné rutiny vlastních zpráv

Zápis obslužné rutiny vlastních zpráv, jsou odvozeny z **System.Net.Http.DelegatingHandler** a přepsat **SendAsync** metody. Následuje podpis metody:

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

Tato metoda přebírá **HttpRequestMessage** jako vstup a asynchronně vrátí **objekt HttpResponseMessage**. Obvyklá implementace provede následující akce:

1. Zpracování zprávy s požadavkem.
2. Volání `base.SendAsync` odešlete žádost na vnitřní obslužnou rutinu.
3. Vnitřní obslužná rutina vrátí zprávu odpovědi. (Tento krok je asynchronní.)
4. Zpracování odpovědi a vrátí řízení volajícímu.

Následující příklad ukazuje popisovač zpráv, který přidá vlastní hlavičku na odchozí žádost:

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

Volání `base.SendAsync` je asynchronní. Pokud obslužná rutina nemá žádnou práci po tomto volání, použijte **await** – klíčové slovo pokračování provádění po dokončení metody. Následující příklad ukazuje obslužnou rutinu, která protokoluje kódy chyb. Protokolování samotný není moc zajímavý, ale tento příklad ukazuje, jak získat odpovědi uvnitř obslužné rutiny.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>Přidání obslužných rutin zpráv do kanálu klienta

Chcete-li přidat vlastní obslužné rutiny pro **HttpClient**, použijte **HttpClientFactory.Create** metody:

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

Obslužné rutiny zpráv jsou volány v pořadí, ve kterém můžete předat je do **vytvořit** metody. Vzhledem k tomu, že jsou vnořené obslužných rutin, v opačném směru přenáší zprávy s odpovědí. To znamená že poslední obslužnou rutinou je první získá zprávu odpovědi.
