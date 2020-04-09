---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Výuka: Vysílání serveru s SignalR 2 | Dokumenty společnosti Microsoft'
author: tdykstra
description: Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá ASP.NET SignalR 2 poskytovat funkce vysílání serveru.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676095"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="5e122-103">Výuka: Vysílání serveru se signálem2</span><span class="sxs-lookup"><span data-stu-id="5e122-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="5e122-104">Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá ASP.NET SignalR 2 poskytovat funkce vysílání serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="5e122-105">Vysílání serveru znamená, že server spustí komunikaci odeslanou klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="5e122-106">Aplikace, kterou vytvoříte v tomto kurzu simuluje burzovní burzovní burzovní, typický scénář pro funkce vysílání serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="5e122-107">Server pravidelně náhodně aktualizuje ceny akcií a vysílá aktualizace všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="5e122-108">V prohlížeči se čísla a symboly v **change** a **%** sloupcích dynamicky mění v reakci na oznámení ze serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="5e122-109">Pokud otevřete další prohlížeče na stejnou adresu URL, zobrazí se všechna stejná data a stejné změny dat současně.</span><span class="sxs-lookup"><span data-stu-id="5e122-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Vytvořit web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="5e122-111">V tomto kurzu jste:</span><span class="sxs-lookup"><span data-stu-id="5e122-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e122-112">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="5e122-112">Create the project</span></span>
> * <span data-ttu-id="5e122-113">Nastavení kódu serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-113">Set up the server code</span></span>
> * <span data-ttu-id="5e122-114">Zkontrolujte kód serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-114">Examine the server code</span></span>
> * <span data-ttu-id="5e122-115">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-115">Set up the client code</span></span>
> * <span data-ttu-id="5e122-116">Zkontrolujte kód klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-116">Examine the client code</span></span>
> * <span data-ttu-id="5e122-117">Testování aplikace</span><span class="sxs-lookup"><span data-stu-id="5e122-117">Test the application</span></span>
> * <span data-ttu-id="5e122-118">Povolit protokolování</span><span class="sxs-lookup"><span data-stu-id="5e122-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e122-119">Pokud nechcete pracovat přes kroky vytváření aplikace, můžete nainstalovat SignalR.Sample balíček v novém projektu Prázdné ASP.NET webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="5e122-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="5e122-120">Pokud nainstalujete balíček NuGet bez provedení kroků v tomto kurzu, je nutné postupovat podle pokynů v souboru *readme.txt.*</span><span class="sxs-lookup"><span data-stu-id="5e122-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="5e122-121">Chcete-li spustit balíček, musíte přidat spouštěcí `ConfigureSignalR` třídu OWIN, která volá metodu v nainstalovaném balíčku.</span><span class="sxs-lookup"><span data-stu-id="5e122-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="5e122-122">Pokud nepřidáte spouštěcí třídu OWIN, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="5e122-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="5e122-123">Viz [instalace ukázkové části StockTicker](#install-the-stockticker-sample) v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="5e122-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e122-124">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5e122-124">Prerequisites</span></span>

* <span data-ttu-id="5e122-125">Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.</span><span class="sxs-lookup"><span data-stu-id="5e122-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="5e122-126">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="5e122-126">Create the project</span></span>

<span data-ttu-id="5e122-127">Tato část ukazuje, jak pomocí sady Visual Studio 2017 vytvořit prázdnou ASP.NET webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5e122-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="5e122-128">V sadě Visual Studio vytvořte ASP.NET webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5e122-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Vytvořit web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="5e122-130">V okně **Nová ASP.NET webová aplikace - SignalR.StockTicker** ponechejte **prázdné** vybrané a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e122-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="5e122-131">Nastavení kódu serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-131">Set up the server code</span></span>

<span data-ttu-id="5e122-132">V této části nastavíte kód, který běží na serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="5e122-133">Vytvoření třídy Stock</span><span class="sxs-lookup"><span data-stu-id="5e122-133">Create the Stock class</span></span>

<span data-ttu-id="5e122-134">Začnete vytvořením třídy *stock* modelu, kterou použijete k ukládání a přenosu informací o akciích.</span><span class="sxs-lookup"><span data-stu-id="5e122-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="5e122-135">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **třídu**.</span><span class="sxs-lookup"><span data-stu-id="5e122-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="5e122-136">Pojmenujte třídu *Stock* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="5e122-137">Nahraďte kód v *souboru Stock.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="5e122-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="5e122-138">Dvě vlastnosti, které nastavíte při `Symbol` vytváření akcií, jsou (například `Price`MSFT pro Microsoft) a .</span><span class="sxs-lookup"><span data-stu-id="5e122-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="5e122-139">Ostatní vlastnosti závisí na tom, jak a kdy nastavíte `Price`.</span><span class="sxs-lookup"><span data-stu-id="5e122-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="5e122-140">Při prvním nastavení `Price`se hodnota rozšíří na `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="5e122-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="5e122-141">`Price`Poté, když nastavíte , aplikace `Change` `PercentChange` vypočítá hodnoty vlastností `Price` a `DayOpen`na základě rozdílu mezi a .</span><span class="sxs-lookup"><span data-stu-id="5e122-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="5e122-142">Vytvoření tříd StockTickerHub a StockTicker</span><span class="sxs-lookup"><span data-stu-id="5e122-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="5e122-143">K zpracování interakce mezi serverem a klientem budete používat rozhraní API hubu SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="5e122-144">Třída, `StockTickerHub` která je odvozena `Hub` od třídy SignalR bude zpracovávat přijímající připojení a volání metod z klientů.</span><span class="sxs-lookup"><span data-stu-id="5e122-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="5e122-145">Je také nutné udržovat data `Timer` zásob a spustit objekt.</span><span class="sxs-lookup"><span data-stu-id="5e122-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="5e122-146">Objekt `Timer` bude pravidelně spouštět aktualizace cen nezávisle na připojení klientů.</span><span class="sxs-lookup"><span data-stu-id="5e122-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="5e122-147">Tyto funkce nelze umístit do `Hub` třídy, protože centra jsou přechodné.</span><span class="sxs-lookup"><span data-stu-id="5e122-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="5e122-148">Aplikace vytvoří `Hub` instanci třídy pro každou úlohu v rozbočovači, jako jsou připojení a volání z klienta na server.</span><span class="sxs-lookup"><span data-stu-id="5e122-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="5e122-149">Takže mechanismus, který uchovává data o akciích, aktualizuje ceny a vysílá aktualizace cen, musí být spuštěn v samostatné třídě.</span><span class="sxs-lookup"><span data-stu-id="5e122-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="5e122-150">Pojmenujete třídu `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="5e122-150">You'll name the class `StockTicker`.</span></span>

![Vysílání z StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="5e122-152">Chcete spustit pouze jednu instanci `StockTicker` třídy na serveru, takže budete muset `StockTickerHub` nastavit odkaz z `StockTicker` každé instance na instanci singleton.</span><span class="sxs-lookup"><span data-stu-id="5e122-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="5e122-153">Třída `StockTicker` musí vysílat klientům, protože má skladová data `StockTicker` a aktivuje `Hub` aktualizace, ale není třída.</span><span class="sxs-lookup"><span data-stu-id="5e122-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="5e122-154">Třída `StockTicker` musí získat odkaz na objekt kontextu připojení signalr hub.</span><span class="sxs-lookup"><span data-stu-id="5e122-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="5e122-155">Potom můžete použít objekt kontextu připojení SignalR k vysílání klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="5e122-156">Vytvořit StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="5e122-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="5e122-157">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="5e122-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="5e122-158">V **přidejte novou položku - SignalR.StockTicker**vyberte **nainstalovaný** > **vizuální C#** > **Web** > **SignalR** a pak vyberte **Třída rozbočovače SignalR (v2)**.</span><span class="sxs-lookup"><span data-stu-id="5e122-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="5e122-159">Pojmenujte třídu *StockTickerHub* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="5e122-160">Tento krok vytvoří soubor *třídy StockTickerHub.cs.*</span><span class="sxs-lookup"><span data-stu-id="5e122-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="5e122-161">Současně přidá sadu souborů skriptů a odkazy na sestavení, které podporují SignalR do projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="5e122-162">Nahraďte kód v *souboru StockTickerHub.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="5e122-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="5e122-163">Uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="5e122-163">Save the file.</span></span>

<span data-ttu-id="5e122-164">Aplikace používá třídu [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) k definování metod, které mohou klienti volat na serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="5e122-165">Definujete jednu metodu: `GetAllStocks()`.</span><span class="sxs-lookup"><span data-stu-id="5e122-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="5e122-166">Když se klient zpočátku připojí k serveru, zavolá tuto metodu, aby získal seznam všech akcií s aktuálními cenami.</span><span class="sxs-lookup"><span data-stu-id="5e122-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="5e122-167">Metoda může být spuštěna synchronně a vrátit, `IEnumerable<Stock>` protože vrací data z paměti.</span><span class="sxs-lookup"><span data-stu-id="5e122-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="5e122-168">Pokud metoda měla získat data tím, že dělá něco, co by znamenalo čekání, jako `Task<IEnumerable<Stock>>` je vyhledávání databáze nebo volání webové služby, byste zadat jako vrácenou hodnotu povolit asynchronní zpracování.</span><span class="sxs-lookup"><span data-stu-id="5e122-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="5e122-169">Další informace naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Při spuštění asynchronně](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="5e122-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="5e122-170">Atribut `HubName` určuje, jak bude aplikace odkazovat na hub v kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="5e122-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="5e122-171">Výchozí název na straně klienta, pokud tento atribut nepoužíváte, je camelCase verze názvu `stockTickerHub`třídy, která by v tomto případě byla .</span><span class="sxs-lookup"><span data-stu-id="5e122-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="5e122-172">Jak uvidíte později při `StockTicker` vytváření třídy, aplikace vytvoří singleton instanci této třídy v jeho statické `Instance` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5e122-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="5e122-173">Tato instance singleton `StockTicker` je v paměti bez ohledu na to, kolik klientů se připojí nebo odpojí.</span><span class="sxs-lookup"><span data-stu-id="5e122-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="5e122-174">Tato instance je `GetAllStocks()` to, co metoda používá k vrácení aktuální informace o zásobách.</span><span class="sxs-lookup"><span data-stu-id="5e122-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="5e122-175">Vytvořit StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="5e122-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="5e122-176">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **třídu**.</span><span class="sxs-lookup"><span data-stu-id="5e122-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="5e122-177">Pojmenujte třídu *StockTicker* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="5e122-178">Nahraďte kód v *souboru StockTicker.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="5e122-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="5e122-179">Vzhledem k tomu, že všechna vlákna budou spuštěna ve stejné instanci kódu StockTicker, musí být třída StockTicker bezpečná pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="5e122-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="5e122-180">Zkontrolujte kód serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-180">Examine the server code</span></span>

<span data-ttu-id="5e122-181">Pokud zkontrolujete kód serveru, pomůže vám to pochopit, jak aplikace funguje.</span><span class="sxs-lookup"><span data-stu-id="5e122-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="5e122-182">Uložení instance singletonu do statického pole</span><span class="sxs-lookup"><span data-stu-id="5e122-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="5e122-183">Kód inicializuje statické `_instance` pole, které `Instance` podporuje vlastnost s instancí třídy.</span><span class="sxs-lookup"><span data-stu-id="5e122-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="5e122-184">Protože konstruktor je soukromý, je to jediná instance třídy, kterou může aplikace vytvořit.</span><span class="sxs-lookup"><span data-stu-id="5e122-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="5e122-185">Aplikace používá [opožděné inicializace](/dotnet/framework/performance/lazy-initialization) pro `_instance` pole.</span><span class="sxs-lookup"><span data-stu-id="5e122-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="5e122-186">Není to z důvodů výkonu.</span><span class="sxs-lookup"><span data-stu-id="5e122-186">It's not for performance reasons.</span></span> <span data-ttu-id="5e122-187">Je to ujistěte se, že vytvoření instance je bezpečné pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="5e122-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="5e122-188">Pokaždé, když se klient připojí k serveru, nová instance třídy StockTickerHub spuštěné v samostatném `StockTicker.Instance` vlákně získá instanci `StockTickerHub` singleton StockTicker ze statické vlastnosti, jak jste viděli dříve ve třídě.</span><span class="sxs-lookup"><span data-stu-id="5e122-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="5e122-189">Ukládání skladových dat v concurrentdictionary</span><span class="sxs-lookup"><span data-stu-id="5e122-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="5e122-190">Konstruktor inicializuje `_stocks` kolekci s některými `GetAllStocks` ukázkovými skladovými daty a vrátí zásoby.</span><span class="sxs-lookup"><span data-stu-id="5e122-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="5e122-191">Jak jste viděli dříve, tato kolekce `StockTickerHub.GetAllStocks`zásob je vrácena `Hub` , což je serverová metoda ve třídě, kterou mohou klienti volat.</span><span class="sxs-lookup"><span data-stu-id="5e122-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="5e122-192">Kolekce zásob je definována jako [concurrentdictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečnost podprocesu.</span><span class="sxs-lookup"><span data-stu-id="5e122-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="5e122-193">Jako alternativu můžete použít [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) objekt a explicitně zamknout slovník při provádění změn v něm.</span><span class="sxs-lookup"><span data-stu-id="5e122-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="5e122-194">Pro tuto ukázkovou aplikaci je v pořádku ukládat data aplikace do paměti `StockTicker` a ztratit data, když aplikace nakládá s instancí.</span><span class="sxs-lookup"><span data-stu-id="5e122-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="5e122-195">V reálné aplikaci byste pracovat s úložiště dat back-end jako databáze.</span><span class="sxs-lookup"><span data-stu-id="5e122-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="5e122-196">Pravidelná aktualizace cen akcií</span><span class="sxs-lookup"><span data-stu-id="5e122-196">Periodically updating stock prices</span></span>

<span data-ttu-id="5e122-197">Konstruktor spustí `Timer` objekt, který pravidelně volá metody, které aktualizují ceny akcií nanáhodném základě.</span><span class="sxs-lookup"><span data-stu-id="5e122-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="5e122-198">`Timer`volání `UpdateStockPrices`, která předává hodnotu null v parametru stavu.</span><span class="sxs-lookup"><span data-stu-id="5e122-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="5e122-199">Před aktualizací cen aplikace zamyká `_updateStockPricesLock` objekt.</span><span class="sxs-lookup"><span data-stu-id="5e122-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="5e122-200">Kód zkontroluje, zda jiné vlákno již aktualizuje `TryUpdateStockPrice` ceny a pak volá na každé zásoby v seznamu.</span><span class="sxs-lookup"><span data-stu-id="5e122-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="5e122-201">Metoda `TryUpdateStockPrice` rozhodne, zda změnit cenu akcií, a kolik ji změnit.</span><span class="sxs-lookup"><span data-stu-id="5e122-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="5e122-202">Pokud se cena akcií změní, aplikace zavolá `BroadcastStockPrice` k vysílání změny ceny akcií všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="5e122-203">Příznak `_updatingStockPrices` označený [volatile,](https://msdn.microsoft.com/library/x13ttww7.aspx) aby se ujistil, že je bezpečný pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="5e122-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="5e122-204">V reálné aplikaci `TryUpdateStockPrice` by metoda volala webovou službu, aby vyhledává cenu.</span><span class="sxs-lookup"><span data-stu-id="5e122-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="5e122-205">V tomto kódu aplikace používá generátor náhodných čísel k náhodným změnám.</span><span class="sxs-lookup"><span data-stu-id="5e122-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="5e122-206">Získání kontextu SignalR tak, aby třída StockTicker může vysílat klientům</span><span class="sxs-lookup"><span data-stu-id="5e122-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="5e122-207">Vzhledem k tomu, že `StockTicker` změny cen pocházejí zde v objektu, je to objekt, který potřebuje volat metodu `updateStockPrice` na všechny připojené klienty.</span><span class="sxs-lookup"><span data-stu-id="5e122-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="5e122-208">Ve `Hub` třídě máte rozhraní API pro volání `StockTicker` klientských metod, `Hub` ale není odvozeno z třídy a nemá odkaz na žádný `Hub` objekt.</span><span class="sxs-lookup"><span data-stu-id="5e122-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="5e122-209">Chcete-li vysílat do `StockTicker` připojených klientů, třída musí `StockTickerHub` získat instance kontextu SignalR pro třídu a použít ji k volání metod na klienty.</span><span class="sxs-lookup"><span data-stu-id="5e122-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="5e122-210">Kód získá odkaz na kontext SignalR při vytvoření instance třídy singleton, předá tento odkaz na `Clients` konstruktoru a konstruktor jej vloží do vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5e122-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="5e122-211">Existují dva důvody, proč chcete získat kontext pouze jednou: získání kontextu je nákladný úkol a získání jednou zajistí, že aplikace zachová zamýšlené pořadí zpráv odeslaných klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="5e122-212">Získání `Clients` vlastnost kontextu a jeho vložení `StockTickerClient` do vlastnosti umožňuje psát kód pro volání klientských `Hub` metod, které vypadají stejně jako ve třídě.</span><span class="sxs-lookup"><span data-stu-id="5e122-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="5e122-213">Chcete-li například vysílat všem `Clients.All.updateStockPrice(stock)`klientům, můžete psát .</span><span class="sxs-lookup"><span data-stu-id="5e122-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="5e122-214">Metoda, `updateStockPrice` kterou voláte, `BroadcastStockPrice` ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="5e122-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="5e122-215">Přidáte jej později při psaní kódu, který běží na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="5e122-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="5e122-216">Můžete odkazovat `updateStockPrice` zde, protože `Clients.All` je dynamický, což znamená, že aplikace vyhodnotí výraz za běhu.</span><span class="sxs-lookup"><span data-stu-id="5e122-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="5e122-217">Při spuštění tohoto volání metody SignalR odešle název metody a hodnotu parametru klientovi `updateStockPrice`a pokud má klient metodu s názvem , aplikace zavolá tuto metodu a předá jí hodnotu parametru.</span><span class="sxs-lookup"><span data-stu-id="5e122-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="5e122-218">`Clients.All`znamená poslat všem klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="5e122-219">SignalR poskytuje další možnosti určit, které klienty nebo skupiny klientů chcete odeslat.</span><span class="sxs-lookup"><span data-stu-id="5e122-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="5e122-220">Další informace naleznete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="5e122-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="5e122-221">Registrace trasy SignalR</span><span class="sxs-lookup"><span data-stu-id="5e122-221">Register the SignalR route</span></span>

<span data-ttu-id="5e122-222">Server potřebuje vědět, která adresa URL zachytit a přímo signalr.</span><span class="sxs-lookup"><span data-stu-id="5e122-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="5e122-223">Chcete-li to provést, přidejte spouštěcí třídu OWIN:</span><span class="sxs-lookup"><span data-stu-id="5e122-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="5e122-224">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="5e122-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="5e122-225">V **pole Přidat novou položku - SignalR.StockTicker** vyberte **nainstalovaný** > **visual c#** > **web** a pak vyberte **OWIN Startup Class**.</span><span class="sxs-lookup"><span data-stu-id="5e122-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="5e122-226">Pojmenujte položku *Spuštění* a vyberte **ok**.</span><span class="sxs-lookup"><span data-stu-id="5e122-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="5e122-227">Nahraďte výchozí kód v *souboru Startup.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="5e122-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="5e122-228">Nyní jste dokončili nastavení kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="5e122-229">V další části nastavíte klienta.</span><span class="sxs-lookup"><span data-stu-id="5e122-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="5e122-230">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-230">Set up the client code</span></span>

<span data-ttu-id="5e122-231">V této části nastavíte kód, který běží na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="5e122-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="5e122-232">Vytvoření stránky HTML a souboru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="5e122-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="5e122-233">Stránka HTML zobrazí data a soubor JavaScript uvede data.</span><span class="sxs-lookup"><span data-stu-id="5e122-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="5e122-234">Vytvořit stockticker.html</span><span class="sxs-lookup"><span data-stu-id="5e122-234">Create StockTicker.html</span></span>

<span data-ttu-id="5e122-235">Nejprve přidáte klienta HTML.</span><span class="sxs-lookup"><span data-stu-id="5e122-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="5e122-236">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **stránku HTML**.</span><span class="sxs-lookup"><span data-stu-id="5e122-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="5e122-237">Pojmenujte soubor *StockTicker* a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e122-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="5e122-238">Nahraďte výchozí kód v souboru *StockTicker.html* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="5e122-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="5e122-239">Html vytvoří tabulku s pěti sloupci, řádek záhlaví a datový řádek s jednou buňkou, která pokrývá všech pět sloupců.</span><span class="sxs-lookup"><span data-stu-id="5e122-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="5e122-240">Na řádku dat se zobrazuje "načítání..." chvíli při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="5e122-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="5e122-241">Kód JavaScriptu tento řádek odstraní a přidá na jeho místo řádky s daty zásob načtenými ze serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="5e122-242">Značky skriptů určují:</span><span class="sxs-lookup"><span data-stu-id="5e122-242">The script tags specify:</span></span>

    * <span data-ttu-id="5e122-243">Soubor skriptu jQuery.</span><span class="sxs-lookup"><span data-stu-id="5e122-243">The jQuery script file.</span></span>

    * <span data-ttu-id="5e122-244">Základní skript SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="5e122-245">Soubor skriptu proxy SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="5e122-246">Soubor skriptu StockTicker, který vytvoříte později.</span><span class="sxs-lookup"><span data-stu-id="5e122-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="5e122-247">Aplikace dynamicky generuje soubor skriptu proxy signalr.</span><span class="sxs-lookup"><span data-stu-id="5e122-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="5e122-248">Určuje adresu URL "/signalr/hubs" a definuje metody proxy pro metody na hub `StockTickerHub.GetAllStocks`třídy, v tomto případě pro .</span><span class="sxs-lookup"><span data-stu-id="5e122-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="5e122-249">Pokud chcete, můžete tento soubor JavaScript vygenerovat ručně pomocí [signalr utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span><span class="sxs-lookup"><span data-stu-id="5e122-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="5e122-250">Nezapomeňte zakázat dynamické vytváření souborů `MapHubs` ve volání metody.</span><span class="sxs-lookup"><span data-stu-id="5e122-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="5e122-251">V **Průzkumníku řešení**rozbalte **položku Skripty**.</span><span class="sxs-lookup"><span data-stu-id="5e122-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="5e122-252">Skriptknihovny pro jQuery a SignalR jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5e122-253">Správce balíčků nainstaluje novější verzi skriptů SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="5e122-254">Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptů v projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="5e122-255">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na *soubor StockTicker.html*a pak vyberte **příkaz Nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="5e122-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="5e122-256">Vytvořit soubor StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="5e122-256">Create StockTicker.js</span></span>

<span data-ttu-id="5e122-257">Nyní vytvořte soubor JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="5e122-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="5e122-258">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **soubor JavaScript .**</span><span class="sxs-lookup"><span data-stu-id="5e122-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="5e122-259">Pojmenujte soubor *StockTicker* a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e122-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="5e122-260">Přidejte tento kód do souboru *StockTicker.js:*</span><span class="sxs-lookup"><span data-stu-id="5e122-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="5e122-261">Zkontrolujte kód klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-261">Examine the client code</span></span>

<span data-ttu-id="5e122-262">Pokud zkontrolujete kód klienta, pomůže vám zjistit, jak klientský kód spolupracuje s kódem serveru, aby aplikace fungovala.</span><span class="sxs-lookup"><span data-stu-id="5e122-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="5e122-263">Spuštění připojení</span><span class="sxs-lookup"><span data-stu-id="5e122-263">Starting the connection</span></span>

<span data-ttu-id="5e122-264">`$.connection`odkazuje na proxy servery SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="5e122-265">Kód získá odkaz na proxy `StockTickerHub` pro třídu a `ticker` vloží jej do proměnné.</span><span class="sxs-lookup"><span data-stu-id="5e122-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="5e122-266">Název proxy serveru je název, `HubName` který byl nastaven atributem:</span><span class="sxs-lookup"><span data-stu-id="5e122-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="5e122-267">Po definování všech proměnných a funkcí poslední řádek kódu v souboru inicializuje připojení `start` SignalR voláním funkce SignalR.</span><span class="sxs-lookup"><span data-stu-id="5e122-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="5e122-268">Funkce `start` se spustí asynchronně a vrátí [jQuery Odložené objektu](http://api.jquery.com/category/deferred-object/).</span><span class="sxs-lookup"><span data-stu-id="5e122-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="5e122-269">Můžete volat hotovou funkci a určit funkci, která má být volána, když aplikace dokončí asynchronní akci.</span><span class="sxs-lookup"><span data-stu-id="5e122-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="5e122-270">Získání všech zásob</span><span class="sxs-lookup"><span data-stu-id="5e122-270">Getting all the stocks</span></span>

<span data-ttu-id="5e122-271">Funkce `init` volá `getAllStocks` funkci na serveru a používá informace, které server vrátí k aktualizaci burzovní tabulky.</span><span class="sxs-lookup"><span data-stu-id="5e122-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="5e122-272">Všimněte si, že ve výchozím nastavení je třeba použít camelCasing na straně klienta, i když název metody je pascal-cased na serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="5e122-273">Pravidlo camelCasing se vztahuje pouze na metody, nikoli na objekty.</span><span class="sxs-lookup"><span data-stu-id="5e122-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="5e122-274">Například odkazujete `stock.Symbol` na `stock.Price`a `stock.symbol` `stock.price`, not nebo .</span><span class="sxs-lookup"><span data-stu-id="5e122-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="5e122-275">V `init` metodě aplikace vytvoří HTML pro řádek tabulky pro každý skladový objekt přijatý `formatStock` ze serveru voláním do formátu `rowTemplate` vlastností `stock` `stock` objektu a pak voláním `supplant` nahradit zástupné symboly v proměnné hodnotami vlastností objektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="5e122-276">Výsledný kód HTML je pak připojen k burzovní tabulce.</span><span class="sxs-lookup"><span data-stu-id="5e122-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="5e122-277">Volání `init` předáním jako `callback` funkce, která se spustí po `start` dokončení asynchronní funkce.</span><span class="sxs-lookup"><span data-stu-id="5e122-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="5e122-278">Pokud jste `init` po volání `start`volali jako samostatný příkaz JavaScript , funkce by se nezdaří, protože by se spustila okamžitě, aniž by čekala na dokončení počáteční funkce připojení.</span><span class="sxs-lookup"><span data-stu-id="5e122-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="5e122-279">V takovém případě `init` by se funkce `getAllStocks` pokusila volat funkci předtím, než aplikace naváže připojení k serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="5e122-280">Získání aktualizovaných cen akcií</span><span class="sxs-lookup"><span data-stu-id="5e122-280">Getting updated stock prices</span></span>

<span data-ttu-id="5e122-281">Když server změní cenu akcie, zavolá `updateStockPrice` na připojené klienty.</span><span class="sxs-lookup"><span data-stu-id="5e122-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="5e122-282">Aplikace přidá funkci do vlastnosti `stockTicker` klienta proxy serveru, aby byla k dispozici pro volání ze serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="5e122-283">Funkce `updateStockPrice` formátuje skladový objekt přijatý ze serveru do řádku tabulky `init` stejným způsobem jako ve funkci.</span><span class="sxs-lookup"><span data-stu-id="5e122-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="5e122-284">Místo připojení řádku k tabulce najde aktuální řádek akcie v tabulce a nahradí tento řádek novým.</span><span class="sxs-lookup"><span data-stu-id="5e122-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="5e122-285">Testování aplikace</span><span class="sxs-lookup"><span data-stu-id="5e122-285">Test the application</span></span>

<span data-ttu-id="5e122-286">Aplikaci můžete otestovat, abyste se ujistili, že funguje.</span><span class="sxs-lookup"><span data-stu-id="5e122-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="5e122-287">Zobrazí se ve všech oknech prohlížeče, kde se zobrazí tabulka živých akcií s kolísavými cenami akcií.</span><span class="sxs-lookup"><span data-stu-id="5e122-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="5e122-288">Na panelu nástrojů zapněte ladění **skriptů** a pak vyberte tlačítko přehrát pro spuštění aplikace v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="5e122-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Snímek obrazovky s uživatelem, který zapne režim ladění a vybere možnost Přehrát.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="5e122-290">Otevře se okno prohlížeče s živou **skladovou tabulkou**.</span><span class="sxs-lookup"><span data-stu-id="5e122-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="5e122-291">Tabulka zásob zpočátku zobrazuje "loading..." line, pak, po krátké době, aplikace zobrazí počáteční údaje o akciích, a pak ceny akcií začnou měnit.</span><span class="sxs-lookup"><span data-stu-id="5e122-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="5e122-292">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do panelů adresaí.</span><span class="sxs-lookup"><span data-stu-id="5e122-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="5e122-293">Počáteční zobrazení zásob je stejné jako první prohlížeč a změny se dějí současně.</span><span class="sxs-lookup"><span data-stu-id="5e122-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="5e122-294">Zavřete všechny prohlížeče, otevřete nový prohlížeč a přejděte na stejnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="5e122-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="5e122-295">StockTicker singleton objekt pokračoval v běhu na serveru.</span><span class="sxs-lookup"><span data-stu-id="5e122-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="5e122-296">**Tabulka živých akcií** ukazuje, že zásoby se nadále mění.</span><span class="sxs-lookup"><span data-stu-id="5e122-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="5e122-297">Nevidíte počáteční tabulku s nulovými změnami.</span><span class="sxs-lookup"><span data-stu-id="5e122-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="5e122-298">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="5e122-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="5e122-299">Povolit protokolování</span><span class="sxs-lookup"><span data-stu-id="5e122-299">Enable logging</span></span>

<span data-ttu-id="5e122-300">SignalR má vestavěnou funkci protokolování, kterou můžete povolit na straně klienta na pomoc při řešení potíží.</span><span class="sxs-lookup"><span data-stu-id="5e122-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="5e122-301">V této části povolíte protokolování a zobrazí tepříklady, které ukazují, jak protokoly zjistit, které z následujících metod přenosu SignalR používá:</span><span class="sxs-lookup"><span data-stu-id="5e122-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="5e122-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), podporované službou IIS 8 a aktuálními prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5e122-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="5e122-303">[Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events)podporované jinými prohlížeči než internet explorer.</span><span class="sxs-lookup"><span data-stu-id="5e122-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="5e122-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), podporovaný aplikací Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5e122-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="5e122-305">[Ajax dlouhé dotazování](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), podporované všemi prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5e122-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="5e122-306">Pro dané připojení SignalR zvolí nejlepší způsob přenosu, který server i klient podporují.</span><span class="sxs-lookup"><span data-stu-id="5e122-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="5e122-307">Otevřete *soubor StockTicker.js*.</span><span class="sxs-lookup"><span data-stu-id="5e122-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="5e122-308">Přidejte tento zvýrazněný řádek kódu, který povolí protokolování bezprostředně před kódem, který inicializuje připojení na konci souboru:</span><span class="sxs-lookup"><span data-stu-id="5e122-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="5e122-309">Spuštění projektu stisknutím **klávesy F5.**</span><span class="sxs-lookup"><span data-stu-id="5e122-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="5e122-310">Otevřete okno vývojářských nástrojů prohlížeče a vyberte konzolu, chcete-li protokoly zobrazit.</span><span class="sxs-lookup"><span data-stu-id="5e122-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="5e122-311">Bude pravděpodobně nutné aktualizovat stránku zobrazíte protokoly SignalR vyjednávání způsob přenosu pro nové připojení.</span><span class="sxs-lookup"><span data-stu-id="5e122-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="5e122-312">Pokud používáte aplikaci Internet Explorer 10 v systému Windows 8 (IIS 8), je způsob přenosu **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="5e122-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="5e122-313">Pokud používáte aplikaci Internet Explorer 10 v systému Windows 7 (IIS 7.5), je způsob přenosu **iframe**.</span><span class="sxs-lookup"><span data-stu-id="5e122-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="5e122-314">Pokud používáte Firefox 19 ve Windows 8 (IIS 8), je způsob přenosu **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="5e122-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="5e122-315">Ve Firefoxu nainstalujte doplněk Firebug, abyste získali okno konzoly.</span><span class="sxs-lookup"><span data-stu-id="5e122-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="5e122-316">Pokud používáte Firefox 19 v systému Windows 7 (IIS 7.5), způsob přenosu je **událost mizející serverem.**</span><span class="sxs-lookup"><span data-stu-id="5e122-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="5e122-317">Instalace ukázky StockTicker</span><span class="sxs-lookup"><span data-stu-id="5e122-317">Install the StockTicker sample</span></span>

<span data-ttu-id="5e122-318">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) nainstaluje aplikaci StockTicker.</span><span class="sxs-lookup"><span data-stu-id="5e122-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="5e122-319">Balíček NuGet obsahuje více funkcí než zjednodušená verze, kterou jste vytvořili od začátku.</span><span class="sxs-lookup"><span data-stu-id="5e122-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="5e122-320">V této části kurzu nainstalujete balíček NuGet a zkontrolujte nové funkce a kód, který je implementuje.</span><span class="sxs-lookup"><span data-stu-id="5e122-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e122-321">Pokud nainstalujete balíček bez provedení předchozíkroky tohoto kurzu, je nutné přidat spouštěcí třídy OWIN do projektu.</span><span class="sxs-lookup"><span data-stu-id="5e122-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="5e122-322">Tento soubor readme.txt pro balíček NuGet vysvětluje tento krok.</span><span class="sxs-lookup"><span data-stu-id="5e122-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="5e122-323">Instalace balíčku SignalR.Sample NuGet</span><span class="sxs-lookup"><span data-stu-id="5e122-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="5e122-324">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **příkaz Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5e122-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="5e122-325">Ve **správci balíčků NuGet: SignalR.StockTicker**vyberte **Procházet**.</span><span class="sxs-lookup"><span data-stu-id="5e122-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="5e122-326">Ve **zdroji balíčku**vyberte **nuget.org**.</span><span class="sxs-lookup"><span data-stu-id="5e122-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="5e122-327">Do vyhledávacího pole zadejte *položku SignalR.Sample* a vyberte **položku Microsoft.AspNet.SignalR.Sample** > **Install**.</span><span class="sxs-lookup"><span data-stu-id="5e122-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="5e122-328">V **Průzkumníku řešení**rozbalte složku *SignalR.Sample.*</span><span class="sxs-lookup"><span data-stu-id="5e122-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="5e122-329">Instalace balíčku SignalR.Sample vytvořila složku a její obsah.</span><span class="sxs-lookup"><span data-stu-id="5e122-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="5e122-330">Ve složce *SignalR.Sample* klepněte pravým tlačítkem myši na *soubor StockTicker.html*a pak vyberte **příkaz Nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="5e122-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e122-331">Instalace balíčku SignalR.Sample NuGet může změnit verzi jQuery, kterou máte ve složce *Skripty.*</span><span class="sxs-lookup"><span data-stu-id="5e122-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="5e122-332">Nový soubor *StockTicker.html,* který balíček nainstaluje do složky *SignalR.Sample,* bude synchronizován s verzí jQuery, kterou balíček nainstaluje, ale pokud chcete znovu spustit původní soubor *StockTicker.html,* budete muset nejprve aktualizovat odkaz jQuery ve značce skriptu.</span><span class="sxs-lookup"><span data-stu-id="5e122-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="5e122-333">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="5e122-333">Run the application</span></span>

 <span data-ttu-id="5e122-334">Tabulka, kterou jste viděli v první aplikaci, měla užitečné funkce.</span><span class="sxs-lookup"><span data-stu-id="5e122-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="5e122-335">Plná burzovní aplikace zobrazuje nové funkce: vodorovně rolovací okno, které zobrazuje údaje o zásobách a zásoby, které mění barvu, když stoupají a klesají.</span><span class="sxs-lookup"><span data-stu-id="5e122-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="5e122-336">Stisknutím **klávesy F5** aplikaci spusťte.</span><span class="sxs-lookup"><span data-stu-id="5e122-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="5e122-337">Při prvním spuštění aplikace je "trh" "zavřený" a zobrazí se statická tabulka a okno, které se neposouvá.</span><span class="sxs-lookup"><span data-stu-id="5e122-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="5e122-338">Vyberte **možnost Otevřít trh**.</span><span class="sxs-lookup"><span data-stu-id="5e122-338">Select **Open Market**.</span></span>

    ![Snímek obrazovky s živým telegrafem](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="5e122-340">Pole **Live Stock Ticker** se začne posouvat vodorovně a server začne náhodně vysílat změny cen akcií.</span><span class="sxs-lookup"><span data-stu-id="5e122-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="5e122-341">Pokaždé, když se změní cena akcií, aplikace aktualizuje **tabulku živých akcií** i **službu Live Stock Ticker**.</span><span class="sxs-lookup"><span data-stu-id="5e122-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="5e122-342">Když je změna ceny akcie kladná, aplikace zobrazí akcie se zeleným pozadím.</span><span class="sxs-lookup"><span data-stu-id="5e122-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="5e122-343">Když je změna záporná, aplikace zobrazí akcie s červeným pozadím.</span><span class="sxs-lookup"><span data-stu-id="5e122-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="5e122-344">Vyberte **Zavřít trh**.</span><span class="sxs-lookup"><span data-stu-id="5e122-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="5e122-345">Aktualizace tabulky se zastaví.</span><span class="sxs-lookup"><span data-stu-id="5e122-345">The table updates stop.</span></span>

    * <span data-ttu-id="5e122-346">Ticker přestane posouvání.</span><span class="sxs-lookup"><span data-stu-id="5e122-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="5e122-347">Vyberte **Resetovat**.</span><span class="sxs-lookup"><span data-stu-id="5e122-347">Select **Reset**.</span></span>

    * <span data-ttu-id="5e122-348">Všechna skladová data jsou resetována.</span><span class="sxs-lookup"><span data-stu-id="5e122-348">All stock data is reset.</span></span>

    * <span data-ttu-id="5e122-349">Aplikace obnoví počáteční stav před zahájením změn cen.</span><span class="sxs-lookup"><span data-stu-id="5e122-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="5e122-350">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do panelů adresaí.</span><span class="sxs-lookup"><span data-stu-id="5e122-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="5e122-351">V každém prohlížeči se dynamicky aktualizují stejná data současně.</span><span class="sxs-lookup"><span data-stu-id="5e122-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="5e122-352">Když vyberete některý z ovládacích prvků, všechny prohlížeče reagují stejným způsobem současně.</span><span class="sxs-lookup"><span data-stu-id="5e122-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="5e122-353">Živý burzovní displej</span><span class="sxs-lookup"><span data-stu-id="5e122-353">Live Stock Ticker display</span></span>

<span data-ttu-id="5e122-354">Zobrazení **Live Stock Ticker** je neuspořádaný seznam v `<div>` prvku formátovaném do jednoho řádku styly CSS.</span><span class="sxs-lookup"><span data-stu-id="5e122-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="5e122-355">Aplikace inicializuje a aktualizuje ticker stejným způsobem jako tabulka: nahrazením `<li>` zástupných symbolů `<li>` v řetězci šablony a dynamickým přidáním prvků do `<ul>` prvku.</span><span class="sxs-lookup"><span data-stu-id="5e122-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="5e122-356">Aplikace zahrnuje posouvání pomocí funkce `animate` jQuery, která mění okraj vlevo od `<div>`neuspořádaného seznamu v rámci .</span><span class="sxs-lookup"><span data-stu-id="5e122-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="5e122-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="5e122-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="5e122-358">Html kód burzovního poletoru:</span><span class="sxs-lookup"><span data-stu-id="5e122-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="5e122-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="5e122-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="5e122-360">Burzovní kód CSS:</span><span class="sxs-lookup"><span data-stu-id="5e122-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="5e122-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="5e122-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="5e122-362">JQuery kód, který dělá to posun:</span><span class="sxs-lookup"><span data-stu-id="5e122-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="5e122-363">Další metody na serveru, které může klient volat</span><span class="sxs-lookup"><span data-stu-id="5e122-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="5e122-364">Chcete-li aplikaci zvýšit flexibilitu, existují další metody, které může aplikace volat.</span><span class="sxs-lookup"><span data-stu-id="5e122-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="5e122-365">SignalR.Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="5e122-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="5e122-366">Třída `StockTickerHub` definuje čtyři další metody, které může klient volat:</span><span class="sxs-lookup"><span data-stu-id="5e122-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="5e122-367">Aplikace volá `OpenMarket` `CloseMarket`, `Reset` a v reakci na tlačítka v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="5e122-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="5e122-368">Ukazují vzor jednoho klienta, který aktivuje změnu stavu, která je okamžitě rozšířena na všechny klienty.</span><span class="sxs-lookup"><span data-stu-id="5e122-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="5e122-369">Každá z těchto metod volá `StockTicker` metodu ve třídě, která způsobuje změnu stavu trhu a poté vysílá nový stav.</span><span class="sxs-lookup"><span data-stu-id="5e122-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="5e122-370">SignalR.Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="5e122-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="5e122-371">Ve `StockTicker` třídě aplikace udržuje stav trhu s vlastností, `MarketState` která `MarketState` vrací hodnotu výčtu:</span><span class="sxs-lookup"><span data-stu-id="5e122-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="5e122-372">Každá z metod, které mění stav trhu, tak `StockTicker` činí uvnitř bloku zámku, protože třída musí být bezpečná pro přístup z více vláken:</span><span class="sxs-lookup"><span data-stu-id="5e122-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="5e122-373">Chcete-li se ujistit, že `_marketState` tento kód `MarketState` je `volatile`bezpečný pro přístup z více vláken, pole, které podporuje vlastnost určenou :</span><span class="sxs-lookup"><span data-stu-id="5e122-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="5e122-374">Metody `BroadcastMarketStateChange` `BroadcastMarketReset` a jsou podobné metodě BroadcastStockPrice, kterou jste již viděli, s výjimkou volání různých metod definovaných na straně klienta:</span><span class="sxs-lookup"><span data-stu-id="5e122-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="5e122-375">Další funkce v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="5e122-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="5e122-376">Funkce `updateStockPrice` nyní zpracovává tabulku i ticker displej a `jQuery.Color` používá k blikání červené a zelené barvy.</span><span class="sxs-lookup"><span data-stu-id="5e122-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="5e122-377">Nové funkce v *Souboru SignalR.StockTicker.js* povolit a zakázat tlačítka na základě stavu trhu.</span><span class="sxs-lookup"><span data-stu-id="5e122-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="5e122-378">Oni také zastavit nebo spustit **Live Stock Ticker** horizontální rolování.</span><span class="sxs-lookup"><span data-stu-id="5e122-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="5e122-379">Vzhledem k tomu, `ticker.client`že mnoho funkcí jsou přidávány do aplikace používá [jQuery rozšířit funkci](http://api.jquery.com/jQuery.extend/) přidat.</span><span class="sxs-lookup"><span data-stu-id="5e122-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="5e122-380">Další nastavení klienta po navázání připojení</span><span class="sxs-lookup"><span data-stu-id="5e122-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="5e122-381">Poté, co klient naváže připojení, má některé další práce provést:</span><span class="sxs-lookup"><span data-stu-id="5e122-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="5e122-382">Zjistěte, zda je trh otevřený nebo `marketOpened` `marketClosed` uzavřený, abyste zavolali příslušnou nebo funkci.</span><span class="sxs-lookup"><span data-stu-id="5e122-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="5e122-383">Připojte volání metody serveru k tlačítkům.</span><span class="sxs-lookup"><span data-stu-id="5e122-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="5e122-384">Metody serveru nejsou připojeny k tlačítkům až poté, co aplikace naváže připojení.</span><span class="sxs-lookup"><span data-stu-id="5e122-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="5e122-385">Je to tak, že kód nemůže volat metody serveru dříve, než jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="5e122-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e122-386">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="5e122-386">Additional resources</span></span>

<span data-ttu-id="5e122-387">V tomto kurzu jste se naučili, jak naprogramovat aplikaci SignalR, která vysílá zprávy ze serveru všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="5e122-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="5e122-388">Nyní můžete vysílat zprávy v pravidelných intervalech a v reakci na oznámení od libovolného klienta.</span><span class="sxs-lookup"><span data-stu-id="5e122-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="5e122-389">Koncept vícevláknové instance singleton uchovávat stav serveru ve scénářích online her pro více hráčů.</span><span class="sxs-lookup"><span data-stu-id="5e122-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="5e122-390">Viz [například hra ShootR založená na SignalR](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="5e122-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="5e122-391">Kurzy, které zobrazují scénáře komunikace mezi dvěma účastníky, naleznete [v tématu Začínáme s SignalR](introduction-to-signalr.md) a [Aktualizace v reálném čase s SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="5e122-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="5e122-392">Další informace o SignalR naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="5e122-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="5e122-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="5e122-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="5e122-394">Projekt SignalR</span><span class="sxs-lookup"><span data-stu-id="5e122-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="5e122-395">SignalR GitHub a ukázky</span><span class="sxs-lookup"><span data-stu-id="5e122-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="5e122-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="5e122-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="5e122-397">Další kroky</span><span class="sxs-lookup"><span data-stu-id="5e122-397">Next steps</span></span>

<span data-ttu-id="5e122-398">V tomto kurzu jste:</span><span class="sxs-lookup"><span data-stu-id="5e122-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e122-399">Byl vytvořen projekt</span><span class="sxs-lookup"><span data-stu-id="5e122-399">Created the project</span></span>
> * <span data-ttu-id="5e122-400">Nastavení kódu serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-400">Set up the server code</span></span>
> * <span data-ttu-id="5e122-401">Zkontrolovánkód serveru</span><span class="sxs-lookup"><span data-stu-id="5e122-401">Examined the server code</span></span>
> * <span data-ttu-id="5e122-402">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-402">Set up the client code</span></span>
> * <span data-ttu-id="5e122-403">Zkontrolován kód klienta</span><span class="sxs-lookup"><span data-stu-id="5e122-403">Examined the client code</span></span>
> * <span data-ttu-id="5e122-404">Otestování aplikace</span><span class="sxs-lookup"><span data-stu-id="5e122-404">Tested the application</span></span>
> * <span data-ttu-id="5e122-405">Povolené protokolování</span><span class="sxs-lookup"><span data-stu-id="5e122-405">Enabled logging</span></span>

<span data-ttu-id="5e122-406">Přejdete k dalšímu článku a dozvíte se, jak vytvořit webovou aplikaci v reálném čase, která používá ASP.NET SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="5e122-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5e122-407">Vytvoření webové aplikace v reálném čase s SignalR</span><span class="sxs-lookup"><span data-stu-id="5e122-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
