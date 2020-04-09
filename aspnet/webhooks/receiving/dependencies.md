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
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET závislostí přijímače WebHooks

Microsoft ASP.NET WebHooks je navržen s vkládání závislostí v mysli. Většinu závislostí v systému lze nahradit alternativními implementacemi pomocí modulu vstřikování závislostí.

Seznam závislostí příjemce naleznete v tématu [DependencyScopeExtensions.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) Pokud nebyla zaregistrována žádná závislost, použije se výchozí implementace. Seznam výchozích implementací naleznete v tématu [ReceiverServices.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)
