---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Vzorky | Dokumenty společnosti Microsoft
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540438"
---
# <a name="katana-samples"></a><span data-ttu-id="e540a-102">Příklady použití sady Katana</span><span class="sxs-lookup"><span data-stu-id="e540a-102">Katana Samples</span></span>

<span data-ttu-id="e540a-103">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e540a-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="e540a-104">Příklady použití sady Katana</span><span class="sxs-lookup"><span data-stu-id="e540a-104">Katana Samples</span></span>

<span data-ttu-id="e540a-105">**zdrojový** | [kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes) tras ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e540a-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="e540a-106">V některých aplikacích budete chtít připojit komponenty OWIN do Asp.Net směrovací tabulky vedle sebe s komponentami, které nejsou OWIN.</span><span class="sxs-lookup"><span data-stu-id="e540a-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="e540a-107">Tato ukázka ukazuje, jak používat metody rozšíření RouteCollection MapOwinPath a MapOwinRoute poskytované společností Microsoft.Owin.Host.SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="e540a-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="e540a-108">**Branching Pipelines Sample** | [Zdrojový kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines) větvení kanálů</span><span class="sxs-lookup"><span data-stu-id="e540a-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="e540a-109">Kanály pro zpracování požadavků OWIN nemusí být lineární, mohou být rozvětvené pro zpracování požadavků různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="e540a-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="e540a-110">Tato ukázka ukazuje, jak vytvořit kanál větvení na základě cest požadavků nebo jiných dat požadavku, jako jsou například záhlaví.</span><span class="sxs-lookup"><span data-stu-id="e540a-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="e540a-111">Tyto součásti jsou k dispozici v balíčku nuget Microsoft.Owin.Mapping.</span><span class="sxs-lookup"><span data-stu-id="e540a-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="e540a-112">**Ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) vlastního serveru </span><span class="sxs-lookup"><span data-stu-id="e540a-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="e540a-113">Ukazuje, jak používat vlastní OWIN server při self-hosting OWIN.</span><span class="sxs-lookup"><span data-stu-id="e540a-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="e540a-114">**Vložený zdrojový** | [kód ukázky](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="e540a-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="e540a-115">Některé Servery OWIN lze spustit uvnitř&quot;vlastního procesu (vlastní hostované).&quot;</span><span class="sxs-lookup"><span data-stu-id="e540a-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="e540a-116">Tato ukázka ukazuje, jak spustit aplikaci OWIN pomocí nástrojů poskytovaných microsoft.Owin.Hosting nuget balíčku.</span><span class="sxs-lookup"><span data-stu-id="e540a-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="e540a-117">**Ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) HelloWorld</span><span class="sxs-lookup"><span data-stu-id="e540a-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="e540a-118">OWIN je abstrakce rozhraní API HTTP serveru, která umožňuje přenositelnost aplikací na různých serverech.</span><span class="sxs-lookup"><span data-stu-id="e540a-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="e540a-119">Tato ukázka ukazuje, jak napsat hello world aplikace pomocí některé **jednoduché obálky** kolem syrové OWIN abstrakce a spustit jej na webovém serveru, jako je ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e540a-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="e540a-120">**Hello World Raw OWIN ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="e540a-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="e540a-121">Tato ukázka ukazuje, jak napsat hello world aplikace pomocí **nezpracované** OWIN abstrakce a spustit ji na webovém serveru, jako je Asp.Net.</span><span class="sxs-lookup"><span data-stu-id="e540a-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="e540a-122">**Zdrojový** | kód ukázkového[signálu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="e540a-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="e540a-123">Ukazuje, jak samoobslužné SignalR pomocí OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="e540a-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="e540a-124">Další informace o samoobslužnésignalr naleznete [v tématu Výuka: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="e540a-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="e540a-125">**Zdrojový** | [kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) statických souborů </span><span class="sxs-lookup"><span data-stu-id="e540a-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="e540a-126">Ukazuje, jak podporovat HTTP požadavky na statické soubory pomocí OWIN / Katana.</span><span class="sxs-lookup"><span data-stu-id="e540a-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="e540a-127">**Zdrojový** | [kód webového](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) rozhraní API </span><span class="sxs-lookup"><span data-stu-id="e540a-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="e540a-128">Tato ukázka ukazuje, jak hostovat OWIN ve službě IIS a přidat webové rozhraní API do kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="e540a-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="e540a-129">**Zdrojový kód ukázkového umítku webového** | [soketu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="e540a-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="e540a-130">Ukazuje, jak podporovat webové sokety v OWIN pomocí třídy [System.Net.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="e540a-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
