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
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="8fe18-105">Mapování uživatelů knihovny SignalR na připojení</span><span class="sxs-lookup"><span data-stu-id="8fe18-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="8fe18-106">, autor: [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8fe18-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="8fe18-107">Toto téma ukazuje, jak uchovávat informace o uživatelích a jejich připojeních.</span><span class="sxs-lookup"><span data-stu-id="8fe18-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="8fe18-108">Patrick Fletcher pomohl napsat toto téma.</span><span class="sxs-lookup"><span data-stu-id="8fe18-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="8fe18-109">Verze softwaru použité v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="8fe18-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="8fe18-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8fe18-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="8fe18-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="8fe18-111">.NET 4.5</span></span>
> - <span data-ttu-id="8fe18-112">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="8fe18-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="8fe18-113">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="8fe18-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="8fe18-114">Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="8fe18-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="8fe18-115">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="8fe18-115">Questions and comments</span></span>
>
> <span data-ttu-id="8fe18-116">Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="8fe18-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="8fe18-117">Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="8fe18-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="8fe18-118">Úvod</span><span class="sxs-lookup"><span data-stu-id="8fe18-118">Introduction</span></span>

<span data-ttu-id="8fe18-119">Každý klient, který se připojuje k rozbočovači, předá jedinečné id připojení. Tuto hodnotu můžete `Context.ConnectionId` načíst ve vlastnosti kontextu centra.</span><span class="sxs-lookup"><span data-stu-id="8fe18-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="8fe18-120">Pokud vaše aplikace potřebuje namapovat uživatele na id připojení a zachovat toto mapování, můžete použít jednu z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="8fe18-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="8fe18-121">Zprostředkovatel ID uživatele (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="8fe18-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="8fe18-122">[Úložiště v paměti](#inmemory), například slovník</span><span class="sxs-lookup"><span data-stu-id="8fe18-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="8fe18-123">Skupina SignalR pro každého uživatele</span><span class="sxs-lookup"><span data-stu-id="8fe18-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="8fe18-124">[Trvalé externí úložiště](#database), například databázová tabulka nebo úložiště tabulek Azure</span><span class="sxs-lookup"><span data-stu-id="8fe18-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="8fe18-125">Každá z těchto implementací je uvedena v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="8fe18-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="8fe18-126">Pomocí metody `OnConnected` `OnDisconnected`, `OnReconnected` a metody `Hub` třídy můžete sledovat stav připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="8fe18-127">Nejlepší přístup pro vaši aplikaci závisí na:</span><span class="sxs-lookup"><span data-stu-id="8fe18-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="8fe18-128">Počet webových serverů hostujících vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8fe18-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="8fe18-129">Zda potřebujete získat seznam aktuálně připojených uživatelů.</span><span class="sxs-lookup"><span data-stu-id="8fe18-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="8fe18-130">Zda potřebujete zachovat informace o skupině a uživateli při restartování aplikace nebo serveru.</span><span class="sxs-lookup"><span data-stu-id="8fe18-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="8fe18-131">Zda je problém latence volání externího serveru.</span><span class="sxs-lookup"><span data-stu-id="8fe18-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="8fe18-132">V následující tabulce je uvedeno, který přístup funguje pro tyto aspekty.</span><span class="sxs-lookup"><span data-stu-id="8fe18-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="8fe18-133">Více než jeden server</span><span class="sxs-lookup"><span data-stu-id="8fe18-133">More than one server</span></span> | <span data-ttu-id="8fe18-134">Získat seznam aktuálně připojených uživatelů</span><span class="sxs-lookup"><span data-stu-id="8fe18-134">Get list of currently connected users</span></span> | <span data-ttu-id="8fe18-135">Zachovat informace po restartování</span><span class="sxs-lookup"><span data-stu-id="8fe18-135">Persist information after restarts</span></span> | <span data-ttu-id="8fe18-136">Optimální výkon</span><span class="sxs-lookup"><span data-stu-id="8fe18-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8fe18-137">Zprostředkovatel Uživatelské ID</span><span class="sxs-lookup"><span data-stu-id="8fe18-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="8fe18-138">V paměti</span><span class="sxs-lookup"><span data-stu-id="8fe18-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="8fe18-139">Skupiny pro jednoho uživatele</span><span class="sxs-lookup"><span data-stu-id="8fe18-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="8fe18-140">Trvalé, vnější</span><span class="sxs-lookup"><span data-stu-id="8fe18-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="8fe18-141">Zprostředkovatel IUserID</span><span class="sxs-lookup"><span data-stu-id="8fe18-141">IUserID provider</span></span>

<span data-ttu-id="8fe18-142">Tato funkce umožňuje uživatelům určit, co userId je založena na IRequest prostřednictvím nového rozhraní IUserIdProvider.</span><span class="sxs-lookup"><span data-stu-id="8fe18-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="8fe18-143">**Zprostředkovatel IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="8fe18-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="8fe18-144">Ve výchozím nastavení bude existovat implementace, která `IPrincipal.Identity.Name` používá jako uživatelské jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="8fe18-145">Chcete-li to změnit, `IUserIdProvider` zaregistrujte implementaci s globálním hostitelem při spuštění aplikace:</span><span class="sxs-lookup"><span data-stu-id="8fe18-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="8fe18-146">Z centra budete moci odesílat zprávy těmto uživatelům prostřednictvím následujícího rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="8fe18-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="8fe18-147">**Odeslání zprávy konkrétnímu uživateli**</span><span class="sxs-lookup"><span data-stu-id="8fe18-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="8fe18-148">Úložiště v paměti</span><span class="sxs-lookup"><span data-stu-id="8fe18-148">In-memory storage</span></span>

<span data-ttu-id="8fe18-149">Následující příklady ukazují, jak zachovat informace o připojení a uživateli ve slovníku, který je uložen v paměti.</span><span class="sxs-lookup"><span data-stu-id="8fe18-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="8fe18-150">Slovník používá k `HashSet` uložení ID připojení. Uživatel může mít kdykoli více než jedno připojení k aplikaci SignalR.</span><span class="sxs-lookup"><span data-stu-id="8fe18-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="8fe18-151">Například uživatel, který je připojen prostřednictvím více zařízení nebo více než jednu kartu prohlížeče, by měl více než jedno id připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="8fe18-152">Pokud se aplikace vypne, dojde ke ztrátě všech informací, ale budou znovu vyplněny, jakmile uživatelé znovu naváže připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="8fe18-153">Úložiště v paměti nefunguje, pokud vaše prostředí obsahuje více než jeden webový server, protože každý server by měl samostatnou kolekci připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="8fe18-154">První příklad ukazuje třídu, která spravuje mapování uživatelů na připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="8fe18-155">Klíč pro HashSet bude jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="8fe18-156">Následující příklad ukazuje, jak používat třídu mapování připojení z rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="8fe18-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="8fe18-157">Instance třídy je uložena v `_connections`názvu proměnné .</span><span class="sxs-lookup"><span data-stu-id="8fe18-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="8fe18-158">Skupiny pro jednoho uživatele</span><span class="sxs-lookup"><span data-stu-id="8fe18-158">Single-user groups</span></span>

<span data-ttu-id="8fe18-159">Můžete vytvořit skupinu pro každého uživatele a potom odeslat zprávu do této skupiny, pokud chcete oslovit pouze tohoto uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="8fe18-160">Název každé skupiny je jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="8fe18-161">Pokud má uživatel více než jedno připojení, každé id připojení je přidándo skupiny uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="8fe18-162">Neměli byste ručně odebrat uživatele ze skupiny, když se uživatel odpojí.</span><span class="sxs-lookup"><span data-stu-id="8fe18-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="8fe18-163">Tato akce je automaticky provedena rozhraním SignalR.</span><span class="sxs-lookup"><span data-stu-id="8fe18-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="8fe18-164">Následující příklad ukazuje, jak implementovat skupiny pro jednoho uživatele.</span><span class="sxs-lookup"><span data-stu-id="8fe18-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="8fe18-165">Trvalé externí úložiště</span><span class="sxs-lookup"><span data-stu-id="8fe18-165">Permanent, external storage</span></span>

<span data-ttu-id="8fe18-166">Toto téma ukazuje, jak používat databázi nebo úložiště tabulek Azure pro ukládání informací o připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="8fe18-167">Tento přístup funguje, pokud máte více webových serverů, protože každý webový server může pracovat se stejným úložištěm dat.</span><span class="sxs-lookup"><span data-stu-id="8fe18-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="8fe18-168">Pokud vaše webové servery přestanou fungovat `OnDisconnected` nebo se aplikace restartuje, metoda není volána.</span><span class="sxs-lookup"><span data-stu-id="8fe18-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="8fe18-169">Proto je možné, že vaše úložiště dat bude mít záznamy pro ID připojení, které již nejsou platné.</span><span class="sxs-lookup"><span data-stu-id="8fe18-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="8fe18-170">Chcete-li vyčistit tyto osamocené záznamy, můžete chtít zrušit platnost připojení, které bylo vytvořeno mimo časový rámec, který je relevantní pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8fe18-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="8fe18-171">Příklady v této části zahrnují hodnotu pro sledování při vytvoření připojení, ale neukazují, jak vyčistit staré záznamy, protože to můžete chtít provést jako proces na pozadí.</span><span class="sxs-lookup"><span data-stu-id="8fe18-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="8fe18-172">databáze</span><span class="sxs-lookup"><span data-stu-id="8fe18-172">Database</span></span>

<span data-ttu-id="8fe18-173">Následující příklady ukazují, jak zachovat informace o připojení a uživateli v databázi.</span><span class="sxs-lookup"><span data-stu-id="8fe18-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="8fe18-174">Můžete použít libovolnou technologii přístupu k datům; však v příkladu ukazuje, jak definovat modely pomocí entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8fe18-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="8fe18-175">Tyto modely entit odpovídají databázovým tabulkám a polím.</span><span class="sxs-lookup"><span data-stu-id="8fe18-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="8fe18-176">Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="8fe18-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="8fe18-177">První příklad ukazuje, jak definovat entitu uživatele, která může být přidružena k mnoha entitám připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="8fe18-178">Potom z rozbočovače můžete sledovat stav každého připojení s níže uvedeným kódem.</span><span class="sxs-lookup"><span data-stu-id="8fe18-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="8fe18-179">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="8fe18-179">Azure table storage</span></span>

<span data-ttu-id="8fe18-180">Následující příklad úložiště tabulky Azure je podobný příkladu databáze.</span><span class="sxs-lookup"><span data-stu-id="8fe18-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="8fe18-181">Neobsahuje všechny informace, které byste potřebovali, abyste mohli začít se službou Azure Table Storage Service.</span><span class="sxs-lookup"><span data-stu-id="8fe18-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="8fe18-182">Další informace naleznete v tématu [Jak používat úložiště tabulky z rozhraní .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="8fe18-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="8fe18-183">Následující příklad ukazuje entitu tabulky pro ukládání informací o připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="8fe18-184">Rozdělí data podle uživatelského jména a identifikuje každou entitu podle ID připojení, takže uživatel může mít kdykoli více připojení.</span><span class="sxs-lookup"><span data-stu-id="8fe18-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="8fe18-185">V rozbočovači můžete sledovat stav připojení jednotlivých uživatelů.</span><span class="sxs-lookup"><span data-stu-id="8fe18-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
