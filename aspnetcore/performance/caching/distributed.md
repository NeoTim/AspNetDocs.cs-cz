---
title: Distribuované ukládání do mezipaměti v ASP.NET Core
author: guardrex
description: Další informace o použití ASP.NET Core distribuované mezipaměti ke zlepšení výkonu aplikací a škálovatelnost, obzvláště v prostředí cloudu nebo serveru farmy.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: performance/caching/distributed
ms.openlocfilehash: 7337ee3b823064c942832d8a44e4d4289bc4fd0e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074371"
---
# <a name="distributed-caching-in-aspnet-core"></a><span data-ttu-id="92efe-103">Distribuované ukládání do mezipaměti v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="92efe-103">Distributed caching in ASP.NET Core</span></span>

<span data-ttu-id="92efe-104">Podle [Steve Smith](https://ardalis.com/) a [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="92efe-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="92efe-105">Distribuované mezipaměti je mezipaměť sdílených více serverů aplikace, obvykle nakládat jako s externí služby na serverech aplikace, které k němu přístup.</span><span class="sxs-lookup"><span data-stu-id="92efe-105">A distributed cache is a cache shared by multiple app servers, typically maintained as an external service to the app servers that access it.</span></span> <span data-ttu-id="92efe-106">Distribuované mezipaměti může zlepšit výkon a škálovatelnost aplikace ASP.NET Core, zejména v případě, že je aplikace hostovaná v cloudové službě nebo v serverové farmě.</span><span class="sxs-lookup"><span data-stu-id="92efe-106">A distributed cache can improve the performance and scalability of an ASP.NET Core app, especially when the app is hosted by a cloud service or a server farm.</span></span>

<span data-ttu-id="92efe-107">Distribuované mezipaměti má několik výhod oproti jiné scénáře ukládání do mezipaměti ukládat data uložená v mezipaměti na serverech jednotlivých aplikací.</span><span class="sxs-lookup"><span data-stu-id="92efe-107">A distributed cache has several advantages over other caching scenarios where cached data is stored on individual app servers.</span></span>

<span data-ttu-id="92efe-108">Když se distribuuje data uložená v mezipaměti, data:</span><span class="sxs-lookup"><span data-stu-id="92efe-108">When cached data is distributed, the data:</span></span>

* <span data-ttu-id="92efe-109">Je *přeměnit* (konzistentní) v rámci celého žádosti více servery.</span><span class="sxs-lookup"><span data-stu-id="92efe-109">Is *coherent* (consistent) across requests to multiple servers.</span></span>
* <span data-ttu-id="92efe-110">Odolává server se restartuje a nasazení aplikací.</span><span class="sxs-lookup"><span data-stu-id="92efe-110">Survives server restarts and app deployments.</span></span>
* <span data-ttu-id="92efe-111">Nepoužívá místní paměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-111">Doesn't use local memory.</span></span>

<span data-ttu-id="92efe-112">Konfigurace distribuované mezipaměti závisí na konkrétní implementaci.</span><span class="sxs-lookup"><span data-stu-id="92efe-112">Distributed cache configuration is implementation specific.</span></span> <span data-ttu-id="92efe-113">Tento článek popisuje, jak nakonfigurovat SQL Server a distribuované mezipaměti Redis.</span><span class="sxs-lookup"><span data-stu-id="92efe-113">This article describes how to configure SQL Server and Redis distributed caches.</span></span> <span data-ttu-id="92efe-114">Implementace třetích stran jsou také k dispozici, například [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache na Githubu](https://github.com/Alachisoft/NCache)).</span><span class="sxs-lookup"><span data-stu-id="92efe-114">Third party implementations are also available, such as [NCache](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache)).</span></span> <span data-ttu-id="92efe-115">Bez ohledu na to, kterou implementaci je vybrána, aplikace komunikuje s potřebnou mezipaměť <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> rozhraní.</span><span class="sxs-lookup"><span data-stu-id="92efe-115">Regardless of which implementation is selected, the app interacts with the cache using the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface.</span></span>

<span data-ttu-id="92efe-116">[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([stažení](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="92efe-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92efe-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="92efe-117">Prerequisites</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="92efe-118">Použití SQL serveru distribuovaná mezipaměť, odkaz [Microsoft.AspNetCore.App Microsoft.aspnetcore.all](xref:fundamentals/metapackage-app) nebo přidat odkaz na balíček pro [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-118">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="92efe-119">Použití Redis distribuovaná mezipaměť, odkaz [Microsoft.AspNetCore.App Microsoft.aspnetcore.all](xref:fundamentals/metapackage-app) a přidejte odkaz na balíček [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-119">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis) package.</span></span> <span data-ttu-id="92efe-120">Není součástí balíčku Redis `Microsoft.AspNetCore.App` balíček, takže musí odkazujte na balíček Redis samostatně v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="92efe-120">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="92efe-121">Použití SQL serveru distribuovaná mezipaměť, odkaz [Microsoft.AspNetCore.App Microsoft.aspnetcore.all](xref:fundamentals/metapackage-app) nebo přidat odkaz na balíček pro [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-121">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="92efe-122">Použití Redis distribuovaná mezipaměť, odkaz [Microsoft.AspNetCore.App Microsoft.aspnetcore.all](xref:fundamentals/metapackage-app) a přidejte odkaz na balíček [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-122">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) and add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="92efe-123">Není součástí balíčku Redis `Microsoft.AspNetCore.App` balíček, takže musí odkazujte na balíček Redis samostatně v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="92efe-123">The Redis package isn't included in the `Microsoft.AspNetCore.App` package, so you must reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="92efe-124">Použití SQL serveru distribuovaná mezipaměť, odkaz [metabalíček Microsoft.aspnetcore.all](xref:fundamentals/metapackage) nebo přidat odkaz na balíček pro [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-124">To use a SQL Server distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="92efe-125">Použití Redis distribuovaná mezipaměť, odkaz [metabalíček Microsoft.aspnetcore.all](xref:fundamentals/metapackage) nebo přidat odkaz na balíček [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-125">To use a Redis distributed cache, reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span> <span data-ttu-id="92efe-126">Je součástí balíčku Redis `Microsoft.AspNetCore.All` balíček, takže není nutné chcete odkázat na balíček Redis samostatně v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="92efe-126">The Redis package is included in `Microsoft.AspNetCore.All` package, so you don't need to reference the Redis package separately in your project file.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="92efe-127">Chcete-li použít systém SQL Server distribuovaná mezipaměť, přidejte odkaz na balíček pro [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-127">To use a SQL Server distributed cache, add a package reference to the [Microsoft.Extensions.Caching.SqlServer](https://www.nuget.org/packages/Microsoft.Extensions.Caching.SqlServer) package.</span></span>

<span data-ttu-id="92efe-128">Použití Redis distribuovaná mezipaměť, přidejte odkaz na balíček [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) balíčku.</span><span class="sxs-lookup"><span data-stu-id="92efe-128">To use a Redis distributed cache, add a package reference to the [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis) package.</span></span>

::: moniker-end

## <a name="idistributedcache-interface"></a><span data-ttu-id="92efe-129">IDistributedCache rozhraní</span><span class="sxs-lookup"><span data-stu-id="92efe-129">IDistributedCache interface</span></span>

<span data-ttu-id="92efe-130"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> Rozhraní poskytuje následující metody k manipulaci s položkami v distribuované mezipaměti implementace:</span><span class="sxs-lookup"><span data-stu-id="92efe-130">The <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface provides the following methods to manipulate items in the distributed cache implementation:</span></span>

* <span data-ttu-id="92efe-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Přijímá s klíčem řetězce a načte položku v mezipaměti jako `byte[]` pole, pokud v mezipaměti nalezen.</span><span class="sxs-lookup"><span data-stu-id="92efe-131"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Get*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.GetAsync*> &ndash; Accepts a string key and retrieves a cached item as a `byte[]` array if found in the cache.</span></span>
* <span data-ttu-id="92efe-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Přidá položku (jako `byte[]` pole) do mezipaměti pomocí řetězce klíče.</span><span class="sxs-lookup"><span data-stu-id="92efe-132"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Set*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.SetAsync*> &ndash; Adds an item (as `byte[]` array) to the cache using a string key.</span></span>
* <span data-ttu-id="92efe-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Aktualizuje položku v mezipaměti na základě jeho klíče resetuje jeho časový limit klouzavé vypršení platnosti (pokud existuje).</span><span class="sxs-lookup"><span data-stu-id="92efe-133"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Refresh*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RefreshAsync*> &ndash; Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>
* <span data-ttu-id="92efe-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Odebere položku mezipaměti na základě jeho řetězec klíče.</span><span class="sxs-lookup"><span data-stu-id="92efe-134"><xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.Remove*>, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache.RemoveAsync*> &ndash; Removes a cache item based on its string key.</span></span>

## <a name="establish-distributed-caching-services"></a><span data-ttu-id="92efe-135">Vytvoření distribuované ukládání do mezipaměti služby</span><span class="sxs-lookup"><span data-stu-id="92efe-135">Establish distributed caching services</span></span>

<span data-ttu-id="92efe-136">Zaregistrujte implementace <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> v `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="92efe-136">Register an implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="92efe-137">Mezi poskytované rozhraním implementace, které jsou popsané v tomto tématu patří:</span><span class="sxs-lookup"><span data-stu-id="92efe-137">Framework-provided implementations described in this topic include:</span></span>

* [<span data-ttu-id="92efe-138">Distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="92efe-138">Distributed Memory Cache</span></span>](#distributed-memory-cache)
* [<span data-ttu-id="92efe-139">Distribuované mezipaměti serveru SQL Server</span><span class="sxs-lookup"><span data-stu-id="92efe-139">Distributed SQL Server cache</span></span>](#distributed-sql-server-cache)
* [<span data-ttu-id="92efe-140">Distribuované mezipaměti Redis</span><span class="sxs-lookup"><span data-stu-id="92efe-140">Distributed Redis cache</span></span>](#distributed-redis-cache)

### <a name="distributed-memory-cache"></a><span data-ttu-id="92efe-141">Distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="92efe-141">Distributed Memory Cache</span></span>

<span data-ttu-id="92efe-142">Distribuované mezipaměti (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) je implementace poskytované rozhraním <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> , který ukládá položky v paměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-142">The Distributed Memory Cache (<xref:Microsoft.Extensions.DependencyInjection.MemoryCacheServiceCollectionExtensions.AddDistributedMemoryCache*>) is a framework-provided implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> that stores items in memory.</span></span> <span data-ttu-id="92efe-143">Distribuované mezipaměti není skutečný distribuované mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-143">The Distributed Memory Cache isn't an actual distributed cache.</span></span> <span data-ttu-id="92efe-144">Položek v mezipaměti jsou uloženy v instanci aplikace na serveru, kde je aplikace spuštěna.</span><span class="sxs-lookup"><span data-stu-id="92efe-144">Cached items are stored by the app instance on the server where the app is running.</span></span>

<span data-ttu-id="92efe-145">Distribuované mezipaměti je užitečné implementace:</span><span class="sxs-lookup"><span data-stu-id="92efe-145">The Distributed Memory Cache is a useful implementation:</span></span>

* <span data-ttu-id="92efe-146">V vývojové a testovací scénáře.</span><span class="sxs-lookup"><span data-stu-id="92efe-146">In development and testing scenarios.</span></span>
* <span data-ttu-id="92efe-147">Pokud používáte jeden server v produkční a paměti spotřeby není problém.</span><span class="sxs-lookup"><span data-stu-id="92efe-147">When a single server is used in production and memory consumption isn't an issue.</span></span> <span data-ttu-id="92efe-148">Implementace distribuované mezipaměti přehledů v mezipaměti datové úložiště.</span><span class="sxs-lookup"><span data-stu-id="92efe-148">Implementing the Distributed Memory Cache abstracts cached data storage.</span></span> <span data-ttu-id="92efe-149">To umožňuje pro implementaci že hodnotu true distribuované řešení ukládání do mezipaměti v budoucích Pokud více uzly nebo nezbytné odolnost proti chybám.</span><span class="sxs-lookup"><span data-stu-id="92efe-149">It allows for implementing a true distributed caching solution in the future if multiple nodes or fault tolerance become necessary.</span></span>

<span data-ttu-id="92efe-150">Ukázková aplikace využívá distribuované mezipaměti při spuštění aplikace ve vývojovém prostředí:</span><span class="sxs-lookup"><span data-stu-id="92efe-150">The sample app makes use of the Distributed Memory Cache when the app is run in the Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=5)]

### <a name="distributed-sql-server-cache"></a><span data-ttu-id="92efe-151">Mezipaměť distribuovaná SQL serveru</span><span class="sxs-lookup"><span data-stu-id="92efe-151">Distributed SQL Server Cache</span></span>

<span data-ttu-id="92efe-152">Implementace distribuované mezipaměti serveru SQL (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>) umožňuje distribuované mezipaměti pro použití jiné databáze systému SQL Server jako svůj záložní úložiště.</span><span class="sxs-lookup"><span data-stu-id="92efe-152">The Distributed SQL Server Cache implementation (<xref:Microsoft.Extensions.DependencyInjection.SqlServerCachingServicesExtensions.AddDistributedSqlServerCache*>) allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="92efe-153">Chcete-li vytvořit tabulku položky uložené v mezipaměti serveru SQL Server v instanci systému SQL Server, můžete použít `sql-cache` nástroj.</span><span class="sxs-lookup"><span data-stu-id="92efe-153">To create a SQL Server cached item table in a SQL Server instance, you can use the `sql-cache` tool.</span></span> <span data-ttu-id="92efe-154">Nástroj vytvoří tabulku s názvem a schéma, které zadáte.</span><span class="sxs-lookup"><span data-stu-id="92efe-154">The tool creates a table with the name and schema that you specify.</span></span>

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="92efe-155">Přidat `SqlConfig.Tools` k `<ItemGroup>` element soubor projektu a spustit `dotnet restore`.</span><span class="sxs-lookup"><span data-stu-id="92efe-155">Add `SqlConfig.Tools` to the `<ItemGroup>` element of the project file and run `dotnet restore`.</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.Extensions.Caching.SqlConfig.Tools"
                          Version="2.0.2" />
</ItemGroup>
```

::: moniker-end

<span data-ttu-id="92efe-156">Vytvoření tabulky v SQL serveru spuštěním `sql-cache create` příkazu.</span><span class="sxs-lookup"><span data-stu-id="92efe-156">Create a table in SQL Server by running the `sql-cache create` command.</span></span> <span data-ttu-id="92efe-157">Zadejte instanci systému SQL Server (`Data Source`), database (`Initial Catalog`), schéma (například `dbo`) a název tabulky (například `TestCache`):</span><span class="sxs-lookup"><span data-stu-id="92efe-157">Provide the SQL Server instance (`Data Source`), database (`Initial Catalog`), schema (for example, `dbo`), and table name (for example, `TestCache`):</span></span>

```console
dotnet sql-cache create "Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
```

<span data-ttu-id="92efe-158">Bude zaznamenána zpráva označující, že nástroj byla úspěšná:</span><span class="sxs-lookup"><span data-stu-id="92efe-158">A message is logged to indicate that the tool was successful:</span></span>

```console
Table and index were created successfully.
```

<span data-ttu-id="92efe-159">Tabulky vytvořené `sql-cache` nástroj má následující schéma:</span><span class="sxs-lookup"><span data-stu-id="92efe-159">The table created by the `sql-cache` tool has the following schema:</span></span>

![Tabulka mezipaměti systému SQL Server](distributed/_static/SqlServerCacheTable.png)

> [!NOTE]
> <span data-ttu-id="92efe-161">Aplikace by měla manipulaci s hodnotami mezipaměti pomocí instance <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>, nikoli <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span><span class="sxs-lookup"><span data-stu-id="92efe-161">An app should manipulate cache values using an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>, not a <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache>.</span></span>

<span data-ttu-id="92efe-162">Implementuje ukázkové aplikace <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> v mimo vývojové prostředí:</span><span class="sxs-lookup"><span data-stu-id="92efe-162">The sample app implements <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCache> in a non-Development environment:</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_ConfigureServices&highlight=9-15)]

> [!NOTE]
> <span data-ttu-id="92efe-163">A <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (a volitelně také <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> a <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) jsou obvykle uložená mimo správy zdrojového kódu (například uložené [manažera tajných](xref:security/app-secrets) nebo v *appsettings.json* / *appsettings. {Prostředí} .json* soubory).</span><span class="sxs-lookup"><span data-stu-id="92efe-163">A <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.ConnectionString*> (and optionally, <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.SchemaName*> and <xref:Microsoft.Extensions.Caching.SqlServer.SqlServerCacheOptions.TableName*>) are typically stored outside of source control (for example, stored by the [Secret Manager](xref:security/app-secrets) or in *appsettings.json*/*appsettings.{Environment}.json* files).</span></span> <span data-ttu-id="92efe-164">Připojovací řetězec může obsahovat přihlašovací údaje, které by měly být neustále mimo systémy správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="92efe-164">The connection string may contain credentials that should be kept out of source control systems.</span></span>

### <a name="distributed-redis-cache"></a><span data-ttu-id="92efe-165">Distribuované Redis Cache</span><span class="sxs-lookup"><span data-stu-id="92efe-165">Distributed Redis Cache</span></span>

<span data-ttu-id="92efe-166">[Redis](https://redis.io/) je úložiště otevřít zdroj dat v paměti, což se často používá jako distribuované mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-166">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="92efe-167">Redis může používat místně, a můžete nakonfigurovat [Azure Redis Cache](https://azure.microsoft.com/services/cache/) pro aplikace ASP.NET Core hostovaných v Azure.</span><span class="sxs-lookup"><span data-stu-id="92efe-167">You can use Redis locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for an Azure-hosted ASP.NET Core app.</span></span> <span data-ttu-id="92efe-168">Aplikace nastaví implementaci mezipaměti pomocí <xref:Microsoft.Extensions.Caching.Redis.RedisCache> instance (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span><span class="sxs-lookup"><span data-stu-id="92efe-168">An app configures the cache implementation using a <xref:Microsoft.Extensions.Caching.Redis.RedisCache> instance (<xref:Microsoft.Extensions.DependencyInjection.RedisCacheServiceCollectionExtensions.AddDistributedRedisCache*>):</span></span>

```csharp
services.AddDistributedRedisCache(options =>
{
    options.Configuration = "localhost";
    options.InstanceName = "SampleInstance";
});
```

<span data-ttu-id="92efe-169">Chcete-li nainstalovat Redis na místním počítači:</span><span class="sxs-lookup"><span data-stu-id="92efe-169">To install Redis on your local machine:</span></span>

* <span data-ttu-id="92efe-170">Nainstalujte [Chocolatey Redis balíčku](https://chocolatey.org/packages/redis-64/).</span><span class="sxs-lookup"><span data-stu-id="92efe-170">Install the [Chocolatey Redis package](https://chocolatey.org/packages/redis-64/).</span></span>
* <span data-ttu-id="92efe-171">Spustit `redis-server` z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="92efe-171">Run `redis-server` from a command prompt.</span></span>

## <a name="use-the-distributed-cache"></a><span data-ttu-id="92efe-172">Pomocí distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="92efe-172">Use the distributed cache</span></span>

<span data-ttu-id="92efe-173">Použít <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> rozhraní, požádat o instanci <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> z jakéhokoli konstruktoru v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92efe-173">To use the <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> interface, request an instance of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> from any constructor in the app.</span></span> <span data-ttu-id="92efe-174">Instance je poskytován [injektáž závislostí (DI)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="92efe-174">The instance is provided by [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span>

<span data-ttu-id="92efe-175">Při spuštění aplikace <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> se vloží do `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="92efe-175">When the app starts, <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is injected into `Startup.Configure`.</span></span> <span data-ttu-id="92efe-176">Aktuální čas se uloží do mezipaměti pomocí <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (Další informace najdete v tématu [webového hostitele: Rozhraní IApplicationLifetime](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span><span class="sxs-lookup"><span data-stu-id="92efe-176">The current time is cached using <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime> (for more information, see [Web Host: IApplicationLifetime interface](xref:fundamentals/host/web-host#iapplicationlifetime-interface)):</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Startup.cs?name=snippet_Configure&highlight=10)]

<span data-ttu-id="92efe-177">Vloží ukázková aplikace <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> do `IndexModel` používají indexovou stránku.</span><span class="sxs-lookup"><span data-stu-id="92efe-177">The sample app injects <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> into the `IndexModel` for use by the Index page.</span></span>

<span data-ttu-id="92efe-178">Pokaždé, když je načten indexovou stránku, do mezipaměti se kontroluje u mezipaměti čas v `OnGetAsync`.</span><span class="sxs-lookup"><span data-stu-id="92efe-178">Each time the Index page is loaded, the cache is checked for the cached time in `OnGetAsync`.</span></span> <span data-ttu-id="92efe-179">Pokud v mezipaměti Doba nevypršela, zobrazí se čas.</span><span class="sxs-lookup"><span data-stu-id="92efe-179">If the cached time hasn't expired, the time is displayed.</span></span> <span data-ttu-id="92efe-180">Pokud 20 sekund uplynuly od posledního času v mezipaměti se použila (poslední čas na této stránce byl načten), na stránce se zobrazí *uložené v mezipaměti časový limit vypršel*.</span><span class="sxs-lookup"><span data-stu-id="92efe-180">If 20 seconds have elapsed since the last time the cached time was accessed (the last time this page was loaded), the page displays *Cached Time Expired*.</span></span>

<span data-ttu-id="92efe-181">Okamžitě aktualizovat uložené v mezipaměti Doba na aktuální čas tak, že vyberete **obnovit uložený v mezipaměti Doba** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="92efe-181">Immediately update the cached time to the current time by selecting the **Reset Cached Time** button.</span></span> <span data-ttu-id="92efe-182">Aktivacemi tlačítek `OnPostResetCachedTime` metodu obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="92efe-182">The button triggers the `OnPostResetCachedTime` handler method.</span></span>

[!code-csharp[](distributed/samples/2.x/DistCacheSample/Pages/Index.cshtml.cs?name=snippet_IndexModel&highlight=7,14-20,25-29)]

> [!NOTE]
> <span data-ttu-id="92efe-183">Není nutné používat jednotlivý prvek nebo rozsah doba života pro <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instance (nejméně pro předdefinované implementace).</span><span class="sxs-lookup"><span data-stu-id="92efe-183">There's no need to use a Singleton or Scoped lifetime for <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instances (at least for the built-in implementations).</span></span>
>
> <span data-ttu-id="92efe-184">Můžete také vytvořit <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instance bez ohledu na to může být nutné jednu namísto použití DI, ale vytvoření instance v kódu můžou znesnadnit kódu pro testování a je v rozporu [explicitní závislosti Princip](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span><span class="sxs-lookup"><span data-stu-id="92efe-184">You can also create an <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> instance wherever you might need one instead of using DI, but creating an instance in code can make your code harder to test and violates the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies).</span></span>

## <a name="recommendations"></a><span data-ttu-id="92efe-185">Doporučení</span><span class="sxs-lookup"><span data-stu-id="92efe-185">Recommendations</span></span>

<span data-ttu-id="92efe-186">Při rozhodování o tom, která implementace <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> je nejvhodnější pro vaši aplikaci, vezměte v úvahu následující:</span><span class="sxs-lookup"><span data-stu-id="92efe-186">When deciding which implementation of <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> is best for your app, consider the following:</span></span>

* <span data-ttu-id="92efe-187">Stávající infrastruktury</span><span class="sxs-lookup"><span data-stu-id="92efe-187">Existing infrastructure</span></span>
* <span data-ttu-id="92efe-188">Požadavky na výkon</span><span class="sxs-lookup"><span data-stu-id="92efe-188">Performance requirements</span></span>
* <span data-ttu-id="92efe-189">Náklady</span><span class="sxs-lookup"><span data-stu-id="92efe-189">Cost</span></span>
* <span data-ttu-id="92efe-190">Týmových zkušeností</span><span class="sxs-lookup"><span data-stu-id="92efe-190">Team experience</span></span>

<span data-ttu-id="92efe-191">Řešení ukládání do mezipaměti obvykle využívají úložiště v paměti zajistit rychlé načítání dat uložených v mezipaměti paměti je však omezená prostředků a nákladná rozbalte.</span><span class="sxs-lookup"><span data-stu-id="92efe-191">Caching solutions usually rely on in-memory storage to provide fast retrieval of cached data, but memory is a limited resource and costly to expand.</span></span> <span data-ttu-id="92efe-192">Pouze úložiště používaných dat v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-192">Only store commonly used data in a cache.</span></span>

<span data-ttu-id="92efe-193">Obecně platí Redis cache poskytuje vyšší propustnost a nižší latenci než mezipaměti serveru SQL Server.</span><span class="sxs-lookup"><span data-stu-id="92efe-193">Generally, a Redis cache provides higher throughput and lower latency than a SQL Server cache.</span></span> <span data-ttu-id="92efe-194">Srovnávací testy je však obvykle vyžaduje k určení výkonové charakteristiky strategií ukládání do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="92efe-194">However, benchmarking is usually required to determine the performance characteristics of caching strategies.</span></span>

<span data-ttu-id="92efe-195">Pokud SQL Server slouží jako záložní úložiště distribuované mezipaměti, použijte stejné databáze pro mezipaměť a aplikace běžné datové úložiště a načtení může mít negativní vliv na výkon obou.</span><span class="sxs-lookup"><span data-stu-id="92efe-195">When SQL Server is used as a distributed cache backing store, use of the same database for the cache and the app's ordinary data storage and retrieval can negatively impact the performance of both.</span></span> <span data-ttu-id="92efe-196">Doporučujeme použít vyhrazenou instanci systému SQL Server pro distribuované mezipaměti záložní úložiště.</span><span class="sxs-lookup"><span data-stu-id="92efe-196">We recommend using a dedicated SQL Server instance for the distributed cache backing store.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92efe-197">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="92efe-197">Additional resources</span></span>

* [<span data-ttu-id="92efe-198">Redis Cache v Azure</span><span class="sxs-lookup"><span data-stu-id="92efe-198">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="92efe-199">SQL Database v Azure</span><span class="sxs-lookup"><span data-stu-id="92efe-199">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* <span data-ttu-id="92efe-200">[ASP.NET Core IDistributedCache zprostředkovatele pro NCache ve webových farmách](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache na Githubu](https://github.com/Alachisoft/NCache))</span><span class="sxs-lookup"><span data-stu-id="92efe-200">[ASP.NET Core IDistributedCache Provider for NCache in Web Farms](http://www.alachisoft.com/ncache/aspnet-core-idistributedcache-ncache.html) ([NCache on GitHub](https://github.com/Alachisoft/NCache))</span></span>
* <xref:performance/caching/memory>
* <xref:fundamentals/change-tokens>
* <xref:performance/caching/response>
* <xref:performance/caching/middleware>
* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper>
* <xref:host-and-deploy/web-farm>
