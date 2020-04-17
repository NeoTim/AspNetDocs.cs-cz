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
# <a name="katana-samples"></a>Příklady použití sady Katana

podle [společnosti Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Příklady použití sady Katana

**zdrojový** | [kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes) tras ASP.NET  
V některých aplikacích budete chtít připojit komponenty OWIN do Asp.Net směrovací tabulky vedle sebe s komponentami, které nejsou OWIN. Tato ukázka ukazuje, jak používat metody rozšíření RouteCollection MapOwinPath a MapOwinRoute poskytované společností Microsoft.Owin.Host.SystemWeb.

**Branching Pipelines Sample** | [Zdrojový kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines) větvení kanálů  
Kanály pro zpracování požadavků OWIN nemusí být lineární, mohou být rozvětvené pro zpracování požadavků různými způsoby. Tato ukázka ukazuje, jak vytvořit kanál větvení na základě cest požadavků nebo jiných dat požadavku, jako jsou například záhlaví. Tyto součásti jsou k dispozici v balíčku nuget Microsoft.Owin.Mapping.

**Ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) vlastního serveru   
Ukazuje, jak používat vlastní OWIN server při self-hosting OWIN.

**Vložený zdrojový** | [kód ukázky](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Některé Servery OWIN lze spustit uvnitř&quot;vlastního procesu (vlastní hostované).&quot; Tato ukázka ukazuje, jak spustit aplikaci OWIN pomocí nástrojů poskytovaných microsoft.Owin.Hosting nuget balíčku.

**Ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) HelloWorld  
OWIN je abstrakce rozhraní API HTTP serveru, která umožňuje přenositelnost aplikací na různých serverech. Tato ukázka ukazuje, jak napsat hello world aplikace pomocí některé **jednoduché obálky** kolem syrové OWIN abstrakce a spustit jej na webovém serveru, jako je ASP.NET.

**Hello World Raw OWIN ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
Tato ukázka ukazuje, jak napsat hello world aplikace pomocí **nezpracované** OWIN abstrakce a spustit ji na webovém serveru, jako je Asp.Net.

**Zdrojový** | kód ukázkového[signálu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
Ukazuje, jak samoobslužné SignalR pomocí OWIN / Katana. Další informace o samoobslužnésignalr naleznete [v tématu Výuka: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Zdrojový** | [kód ukázkového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) statických souborů   
Ukazuje, jak podporovat HTTP požadavky na statické soubory pomocí OWIN / Katana.

**Zdrojový** | [kód webového](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) rozhraní API   
Tato ukázka ukazuje, jak hostovat OWIN ve službě IIS a přidat webové rozhraní API do kanálu OWIN.

**Zdrojový kód ukázkového umítku webového** | [soketu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
Ukazuje, jak podporovat webové sokety v OWIN pomocí třídy [System.Net.WebSockets.WebSocket.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)
