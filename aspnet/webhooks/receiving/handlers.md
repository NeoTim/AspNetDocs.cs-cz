---
uid: webhooks/receiving/handlers
title: Obslužné rutiny ASP.NET – Webhooky | Dokumentace Microsoftu
author: rick-anderson
description: Způsob zpracování požadavků v ASP.NET – Webhooky.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067642"
---
# <a name="aspnet-webhooks-handlers"></a>Obslužné rutiny ASP.NET – Webhooky

Jakmile Webhooky požadavků byl ověřen voláním Webhooku příjemce, je zpracovat pomocí uživatelského kódu. Tady *obslužné rutiny* se dělí na. Obslužné rutiny jsou odvozeny z [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) rozhraní, ale obvykle používá [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) třídy namísto přímo z uživatelského rozhraní.

Požadavek Webhooku může zpracovat jeden nebo více obslužných rutin. Obslužné rutiny jsou volány v pořadí podle jejich příslušných *pořadí* vlastnost, že přejdete od nejnižší a nejvyšší kde pořadí je jednoduchý celé číslo (doporučujeme, abyste být v rozmezí od 1 do 100):

![Obslužná rutina pro WebHook pořadí vlastnosti diagramu](_static/Handlers.png)

Volitelně můžete nastavit obslužnou rutinu *odpovědi* vlastnost WebHookHandlerContext, což povede k zastavení a reakci na odeslána zpět jako odpověď HTTP k Webhooku zpracování. V případě výše nebude získat C obslužná rutina volat, protože má vyšší pořadí, než B a B nastaví odpověď.

Nastavení odpovědi je obvykle pouze relevantní pro Webhooky, kde bude odpověď přenášet informace zpět do původní rozhraní API. Je třeba v případě, kde se pošle odpověď zpět do kanálu Webhooku, odkud Webhooky Slack. Obslužné rutiny můžete nastavit vlastnost příjemce, pokud chtějí dostávat Webhooků z tohoto konkrétního příjemce. Pokud příjemce, které jsou volány pro všechny z nich není nastavená.

Jeden další běžné použití odpověď má používat *410 Gone* odpověď Webhooku už je aktivní a by měly být předloženy žádné další požadavky.

Ve výchozím nastavení bude volána obslužná rutina všechny spuštěné přijímače zpracovaly Webhooku. Nicméně pokud *příjemce* je nastavena na název obslužné rutiny, pak tato obslužná rutina bude přijímat pouze požadavky Webhooku z tento příjemce.

## <a name="processing-a-webhook"></a>Zpracování Webhooku

Když je volána obslužnou rutinu, získá [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) obsahující informace o požadavek Webhooku. Data, obvykle obsahu žádosti HTTP, je k dispozici *Data* vlastnost.

Typ dat je obvykle JSON nebo HTML data formuláře, ale je možné přetypovat na konkrétnější typ, v případě potřeby. Například vlastní Webhooky generovaných ASP.NET – Webhooky může být převeden na typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) následujícím způsobem:

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

Většina odesílatelů Webhooku se znovu odeslat Webhooku, pokud je odpověď, není vygenerovaný v rámci několika sekund. To znamená, že vaše obslužná rutina musí dokončit zpracování za toto časové období v pořadí není pro něj má být volána znovu.

Pokud zpracování trvá déle, nebo se lépe využívá samostatně pak bude [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) je možné odeslat požadavek Webhooku do fronty, například [fronty Azure Storage](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Přehled [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementace je k dispozici zde:

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
