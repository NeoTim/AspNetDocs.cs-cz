---
uid: webhooks/receiving/handlers
title: ASP.NET obslužné rutiny WebHooks | Dokumenty společnosti Microsoft
author: rick-anderson
description: Jak zpracovat požadavky v ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675219"
---
# <a name="aspnet-webhooks-handlers"></a>ASP.NET obslužné rutiny WebHooks

Jakmile webhooks požadavky byly ověřeny přijímačem WebHook, je připraven ke zpracování podle uživatelského kódu. Tady přicházejí *manipulátoři.* Obslužné rutiny jsou odvozeny z rozhraní [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) ale obvykle používají třídu [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) namísto odvození přímo z rozhraní.

Požadavek WebHook může zpracovat jeden nebo více obslužných rutin. Obslužné rutiny jsou volány v pořadí na základě jejich příslušné *Order* vlastnost bude od nejnižší k nejvyšší, kde Order je jednoduché celé číslo (navrhl být mezi 1 a 100):

![Diagram vlastností objednávky obslužné rutiny webhooku](_static/Handlers.png)

Obslužná rutina může volitelně nastavit *vlastnost Response* na WebHookHandlerContext, což povede zpracování zastavit a odpověď, která má být odeslána zpět jako odpověď HTTP na WebHook. Ve výše uvedeném případě handler C nebude mít volána, protože má vyšší pořadí než B a B nastaví odpověď.

Nastavení odpovědi je obvykle relevantní pouze pro WebHooks, kde odpověď může přenášet informace zpět do původního rozhraní API. To je například případ Slack WebHooks, kde je odpověď vyslán zpět do kanálu, odkud pochází WebHook. Obslužné rutiny můžete nastavit Receiver vlastnost, pokud chtějí přijímat pouze WebHooks z tohoto konkrétního příjemce. Pokud nenastaví přijímač, jsou voláni pro všechny z nich.

Jedním z dalších běžných použití odpovědi je použít *odpověď 410 Gone* k označení, že WebHook již není aktivní a žádné další požadavky by měly být předloženy.

Ve výchozím nastavení bude obslužná rutina volána všemi příjemci WebHook. Pokud je však vlastnost *Receiver* nastavena na název obslužné rutiny, bude tato obslužná rutina přijímat pouze požadavky WebHook od tohoto příjemce.

## <a name="processing-a-webhook"></a>Zpracování webhooku

Při volání obslužné rutiny získá [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) obsahující informace o požadavku WebHook. Data, obvykle tělo požadavku HTTP, je k dispozici z *Data* vlastnost.

Typ dat je obvykle JSON nebo HTML data formuláře, ale je možné přetypovat na konkrétnější typ v případě potřeby. Například vlastní WebHooks generované ASP.NET WebHooks lze přetypovat na typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) takto:

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>Zpracování ve frontě

Většina odesílatelů WebHook znovu odešle WebHook, pokud odpověď není generována během několika sekund. To znamená, že obslužná rutina musí dokončit zpracování v tomto časovém rámci, aby nebyla znovu volána.

Pokud zpracování trvá déle nebo je lépe zpracována samostatně pak [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) lze odeslat požadavek WebHook do fronty, například [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Osnova implementace [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) je k dispozici zde:

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
