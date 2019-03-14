---
title: Injektáž závislostí v obslužné rutině požadavek v ASP.NET Core
author: rick-anderson
description: Zjistěte, jak vložit obslužné rutiny požadavek ověřování do aplikace ASP.NET Core pomocí vkládání závislostí.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 71d563e11d308a95c08e6d012d3a071f4697d2de
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067582"
---
# <a name="dependency-injection-in-requirement-handlers-in-aspnet-core"></a><span data-ttu-id="64b42-103">Injektáž závislostí v obslužné rutině požadavek v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="64b42-103">Dependency injection in requirement handlers in ASP.NET Core</span></span>

<a name="security-authorization-di"></a>

<span data-ttu-id="64b42-104">[Povolení obslužné rutiny musí být zaregistrovaný](xref:security/authorization/policies#handler-registration) v kolekci služby během konfigurace (pomocí [injektáž závislostí](xref:fundamentals/dependency-injection)).</span><span class="sxs-lookup"><span data-stu-id="64b42-104">[Authorization handlers must be registered](xref:security/authorization/policies#handler-registration) in the service collection during configuration (using [dependency injection](xref:fundamentals/dependency-injection)).</span></span>

<span data-ttu-id="64b42-105">Předpokládejme, že jste měli úložiště pravidel, který chcete vyhodnotit uvnitř obslužné rutiny autorizace a tohoto úložiště bylo registrováno v kolekci služby.</span><span class="sxs-lookup"><span data-stu-id="64b42-105">Suppose you had a repository of rules you wanted to evaluate inside an authorization handler and that repository was registered in the service collection.</span></span> <span data-ttu-id="64b42-106">Autorizace se vyřešit a vložení, který do vašeho konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="64b42-106">Authorization will resolve and inject that into your constructor.</span></span>

<span data-ttu-id="64b42-107">Například, pokud jste chtěli použít ASP. NET je protokolování infrastruktury budete pravděpodobně chtít vložit `ILoggerFactory` do vaší obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="64b42-107">For example, if you wanted to use ASP.NET's logging infrastructure you would want to inject `ILoggerFactory` into your handler.</span></span> <span data-ttu-id="64b42-108">Tato obslužná rutina může vypadat:</span><span class="sxs-lookup"><span data-stu-id="64b42-108">Such a handler might look like:</span></span>

```csharp
public class LoggingAuthorizationHandler : AuthorizationHandler<MyRequirement>
   {
       ILogger _logger;

       public LoggingAuthorizationHandler(ILoggerFactory loggerFactory)
       {
           _logger = loggerFactory.CreateLogger(this.GetType().FullName);
       }

       protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MyRequirement requirement)
       {
           _logger.LogInformation("Inside my handler");
           // Check if the requirement is fulfilled.
           return Task.CompletedTask;
       }
   }
   ```

<span data-ttu-id="64b42-109">By zaregistrovat obslužnou rutinu s `services.AddSingleton()`:</span><span class="sxs-lookup"><span data-stu-id="64b42-109">You would register the handler with `services.AddSingleton()`:</span></span>

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

<span data-ttu-id="64b42-110">Instance se obslužná rutina se vytvoří při spuštění aplikace a bude DI vložit zaregistrovanou `ILoggerFactory` do vaší konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="64b42-110">An instance of the handler will be created when your application starts, and DI will inject the registered `ILoggerFactory` into your constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="64b42-111">Obslužné rutiny, které používají rozhraní Entity Framework by neměla být registrována jako jednotlivé prvky.</span><span class="sxs-lookup"><span data-stu-id="64b42-111">Handlers that use Entity Framework shouldn't be registered as singletons.</span></span>
