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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="fbd21-103">ASP.NET obslužné rutiny WebHooks</span><span class="sxs-lookup"><span data-stu-id="fbd21-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="fbd21-104">Jakmile webhooks požadavky byly ověřeny přijímačem WebHook, je připraven ke zpracování podle uživatelského kódu.</span><span class="sxs-lookup"><span data-stu-id="fbd21-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="fbd21-105">Tady přicházejí *manipulátoři.*</span><span class="sxs-lookup"><span data-stu-id="fbd21-105">This is where *handlers* come in.</span></span> <span data-ttu-id="fbd21-106">Obslužné rutiny jsou odvozeny z rozhraní [IWebHookHandler,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) ale obvykle používají třídu [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) namísto odvození přímo z rozhraní.</span><span class="sxs-lookup"><span data-stu-id="fbd21-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="fbd21-107">Požadavek WebHook může zpracovat jeden nebo více obslužných rutin.</span><span class="sxs-lookup"><span data-stu-id="fbd21-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="fbd21-108">Obslužné rutiny jsou volány v pořadí na základě jejich příslušné *Order* vlastnost bude od nejnižší k nejvyšší, kde Order je jednoduché celé číslo (navrhl být mezi 1 a 100):</span><span class="sxs-lookup"><span data-stu-id="fbd21-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Diagram vlastností objednávky obslužné rutiny webhooku](_static/Handlers.png)

<span data-ttu-id="fbd21-110">Obslužná rutina může volitelně nastavit *vlastnost Response* na WebHookHandlerContext, což povede zpracování zastavit a odpověď, která má být odeslána zpět jako odpověď HTTP na WebHook.</span><span class="sxs-lookup"><span data-stu-id="fbd21-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="fbd21-111">Ve výše uvedeném případě handler C nebude mít volána, protože má vyšší pořadí než B a B nastaví odpověď.</span><span class="sxs-lookup"><span data-stu-id="fbd21-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="fbd21-112">Nastavení odpovědi je obvykle relevantní pouze pro WebHooks, kde odpověď může přenášet informace zpět do původního rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fbd21-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="fbd21-113">To je například případ Slack WebHooks, kde je odpověď vyslán zpět do kanálu, odkud pochází WebHook.</span><span class="sxs-lookup"><span data-stu-id="fbd21-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="fbd21-114">Obslužné rutiny můžete nastavit Receiver vlastnost, pokud chtějí přijímat pouze WebHooks z tohoto konkrétního příjemce.</span><span class="sxs-lookup"><span data-stu-id="fbd21-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="fbd21-115">Pokud nenastaví přijímač, jsou voláni pro všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="fbd21-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="fbd21-116">Jedním z dalších běžných použití odpovědi je použít *odpověď 410 Gone* k označení, že WebHook již není aktivní a žádné další požadavky by měly být předloženy.</span><span class="sxs-lookup"><span data-stu-id="fbd21-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="fbd21-117">Ve výchozím nastavení bude obslužná rutina volána všemi příjemci WebHook.</span><span class="sxs-lookup"><span data-stu-id="fbd21-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="fbd21-118">Pokud je však vlastnost *Receiver* nastavena na název obslužné rutiny, bude tato obslužná rutina přijímat pouze požadavky WebHook od tohoto příjemce.</span><span class="sxs-lookup"><span data-stu-id="fbd21-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="fbd21-119">Zpracování webhooku</span><span class="sxs-lookup"><span data-stu-id="fbd21-119">Processing a WebHook</span></span>

<span data-ttu-id="fbd21-120">Při volání obslužné rutiny získá [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) obsahující informace o požadavku WebHook.</span><span class="sxs-lookup"><span data-stu-id="fbd21-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="fbd21-121">Data, obvykle tělo požadavku HTTP, je k dispozici z *Data* vlastnost.</span><span class="sxs-lookup"><span data-stu-id="fbd21-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="fbd21-122">Typ dat je obvykle JSON nebo HTML data formuláře, ale je možné přetypovat na konkrétnější typ v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="fbd21-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="fbd21-123">Například vlastní WebHooks generované ASP.NET WebHooks lze přetypovat na typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) takto:</span><span class="sxs-lookup"><span data-stu-id="fbd21-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="fbd21-124">Zpracování ve frontě</span><span class="sxs-lookup"><span data-stu-id="fbd21-124">Queued Processing</span></span>

<span data-ttu-id="fbd21-125">Většina odesílatelů WebHook znovu odešle WebHook, pokud odpověď není generována během několika sekund.</span><span class="sxs-lookup"><span data-stu-id="fbd21-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="fbd21-126">To znamená, že obslužná rutina musí dokončit zpracování v tomto časovém rámci, aby nebyla znovu volána.</span><span class="sxs-lookup"><span data-stu-id="fbd21-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="fbd21-127">Pokud zpracování trvá déle nebo je lépe zpracována samostatně pak [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) lze odeslat požadavek WebHook do fronty, například [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbd21-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="fbd21-128">Osnova implementace [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="fbd21-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
