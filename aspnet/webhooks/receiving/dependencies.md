---
uid: webhooks/receiving/dependencies
title: ASP.NET závislostí přijímače WebHooks | Dokumenty společnosti Microsoft
author: rick-anderson
description: Závislosti přijímače a vkládání závislostí v ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675201"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="5e85e-103">ASP.NET závislostí přijímače WebHooks</span><span class="sxs-lookup"><span data-stu-id="5e85e-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="5e85e-104">Microsoft ASP.NET WebHooks je navržen s vkládání závislostí v mysli.</span><span class="sxs-lookup"><span data-stu-id="5e85e-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="5e85e-105">Většinu závislostí v systému lze nahradit alternativními implementacemi pomocí modulu vstřikování závislostí.</span><span class="sxs-lookup"><span data-stu-id="5e85e-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="5e85e-106">Seznam závislostí příjemce naleznete v tématu [DependencyScopeExtensions.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)</span><span class="sxs-lookup"><span data-stu-id="5e85e-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="5e85e-107">Pokud nebyla zaregistrována žádná závislost, použije se výchozí implementace.</span><span class="sxs-lookup"><span data-stu-id="5e85e-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="5e85e-108">Seznam výchozích implementací naleznete v tématu [ReceiverServices.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)</span><span class="sxs-lookup"><span data-stu-id="5e85e-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
