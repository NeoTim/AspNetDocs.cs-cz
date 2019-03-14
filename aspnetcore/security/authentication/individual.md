---
title: Články podle projekty ASP.NET Core, které jsou vytvořené pomocí jednotlivých uživatelských účtů
author: rick-anderson
description: Vyhledat články založené na projekty ASP.NET Core, které jsou vytvořené pomocí jednotlivých uživatelských účtů.
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: c73365eafaf2c38ef02c3c83ccf5ced4264f7dc0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068770"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a><span data-ttu-id="63984-103">Články podle projekty ASP.NET Core, které jsou vytvořené pomocí jednotlivých uživatelských účtů</span><span class="sxs-lookup"><span data-stu-id="63984-103">Articles based on ASP.NET Core projects created with individual user accounts</span></span>

<span data-ttu-id="63984-104">ASP.NET Core Identity je součástí šablony projektů v sadě Visual Studio s parametrem "Jednotlivých uživatelských účtů".</span><span class="sxs-lookup"><span data-stu-id="63984-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="63984-105">Ověřování šablony jsou k dispozici v rozhraní .NET Core CLI s `-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="63984-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapp -au Individual
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new razor -au Individual
```

::: moniker-end

<span data-ttu-id="63984-106">Zobrazit [tento problém Githubu](https://github.com/aspnet/AspNetCore/issues/5833) pro ověřování webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="63984-106">See [this GitHub issue](https://github.com/aspnet/AspNetCore/issues/5833) for web API authentication.</span></span>

<a name="no"></a>
## <a name="no-authentication"></a><span data-ttu-id="63984-107">Bez ověřování</span><span class="sxs-lookup"><span data-stu-id="63984-107">No Authentication</span></span>

<span data-ttu-id="63984-108">Ověřování je zadaný v rozhraní příkazového řádku .NET Core s `-au` možnost.</span><span class="sxs-lookup"><span data-stu-id="63984-108">Authentication is specified in the .NET Core CLI with the `-au` option.</span></span> <span data-ttu-id="63984-109">V sadě Visual Studio **změna ověřování** dialogové okno je k dispozici pro nové webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="63984-109">In Visual Studio, the **Change Authentication** dialog is available for new web applications.</span></span> <span data-ttu-id="63984-110">Výchozí pro nové webové aplikace v sadě Visual Studio je **bez ověřování**.</span><span class="sxs-lookup"><span data-stu-id="63984-110">The default for new web apps in Visual Studio is **No Authentication**.</span></span>

<span data-ttu-id="63984-111">Projekty vytvořené bez ověřování:</span><span class="sxs-lookup"><span data-stu-id="63984-111">Projects created with no authentication:</span></span>

* <span data-ttu-id="63984-112">Neobsahují webových stránek a uživatelského rozhraní pro přihlášení a odhlášení.</span><span class="sxs-lookup"><span data-stu-id="63984-112">Don't contain web pages and UI to sign in and sign out.</span></span>
* <span data-ttu-id="63984-113">Neobsahují ověřovacího kódu.</span><span class="sxs-lookup"><span data-stu-id="63984-113">Don't contain authentication code.</span></span>

<a name="win"></a>
## <a name="windows-authentication"></a><span data-ttu-id="63984-114">Ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="63984-114">Windows Authentication</span></span>

<span data-ttu-id="63984-115">Ověřování Windows je určená pro nové webové aplikace v rozhraní příkazového řádku .NET Core s `-au Windows` možnost.</span><span class="sxs-lookup"><span data-stu-id="63984-115">Windows Authentication is specified for new web apps in the .NET Core CLI with the `-au Windows` option.</span></span> <span data-ttu-id="63984-116">V sadě Visual Studio **změna ověřování** dialogové okno obsahuje **ověřování Windows** možnosti.</span><span class="sxs-lookup"><span data-stu-id="63984-116">In Visual Studio, the **Change Authentication** dialog provides the **Windows Authentication** options.</span></span>

<span data-ttu-id="63984-117">Pokud je vybrána možnost ověření Windows, aplikace je nakonfigurovaná pro používání [modul IIS ověřování Windows](xref:host-and-deploy/iis/modules).</span><span class="sxs-lookup"><span data-stu-id="63984-117">If Windows Authentication is selected, the app is configured to use the [Windows Authentication IIS module](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="63984-118">Ověřování Windows je určená pro intranetové weby.</span><span class="sxs-lookup"><span data-stu-id="63984-118">Windows Authentication is intended for Intranet web sites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63984-119">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="63984-119">Additional resources</span></span>

<span data-ttu-id="63984-120">Následující články popisují, jak používat kód vygenerovaný v šablony ASP.NET Core, které používají jednotlivých uživatelských účtů:</span><span class="sxs-lookup"><span data-stu-id="63984-120">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="63984-121">Dvoufaktorové ověřování přes SMS</span><span class="sxs-lookup"><span data-stu-id="63984-121">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="63984-122">Potvrzení účtu a obnovení hesla v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="63984-122">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="63984-123">Vytvoření aplikace ASP.NET Core s uživatelskými daty chráněnými autorizací</span><span class="sxs-lookup"><span data-stu-id="63984-123">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
