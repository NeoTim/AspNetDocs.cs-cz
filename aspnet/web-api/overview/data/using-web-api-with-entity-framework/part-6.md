---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: Vytvoření Javascriptového klienta | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59413890"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="a6334-102">Vytvoření javascriptového klienta</span><span class="sxs-lookup"><span data-stu-id="a6334-102">Create the JavaScript Client</span></span>

<span data-ttu-id="a6334-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a6334-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a6334-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="a6334-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="a6334-105">V této části vytvoříte klienta pro aplikaci v jazyce HTML, JavaScript a [knihovnou Knockout.js](http://knockoutjs.com/) knihovny.</span><span class="sxs-lookup"><span data-stu-id="a6334-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="a6334-106">Vytvoříme klientskou aplikaci ve fázích:</span><span class="sxs-lookup"><span data-stu-id="a6334-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="a6334-107">Zobrazuje seznam knihy.</span><span class="sxs-lookup"><span data-stu-id="a6334-107">Showing a list of books.</span></span>
- <span data-ttu-id="a6334-108">Zobrazuje podrobnosti adresáře.</span><span class="sxs-lookup"><span data-stu-id="a6334-108">Showing a book detail.</span></span>
- <span data-ttu-id="a6334-109">Přidává se nová kniha.</span><span class="sxs-lookup"><span data-stu-id="a6334-109">Adding a new book.</span></span>

<span data-ttu-id="a6334-110">Knihovny Knockout používá vzor Model-View-ViewModel (MVVM):</span><span class="sxs-lookup"><span data-stu-id="a6334-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="a6334-111">**Modelu** je reprezentace dat v doméně business (v našich případu, knihy a autoři) na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="a6334-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="a6334-112">**Zobrazení** je prezentační vrstvy (HTML).</span><span class="sxs-lookup"><span data-stu-id="a6334-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="a6334-113">**Model zobrazení** je objekt jazyka JavaScript obsahující modely.</span><span class="sxs-lookup"><span data-stu-id="a6334-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="a6334-114">Model zobrazení je abstrakce kód uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a6334-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="a6334-115">Nemá žádné znalosti jazyka HTML představující.</span><span class="sxs-lookup"><span data-stu-id="a6334-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="a6334-116">Místo toho představuje abstraktní funkce zobrazení, jako například &quot;seznam knihy&quot;.</span><span class="sxs-lookup"><span data-stu-id="a6334-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="a6334-117">Zobrazení je vázaný na data do modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a6334-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="a6334-118">Aktualizace zobrazení modelu se automaticky projeví v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a6334-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="a6334-119">Model zobrazení také načte události z zobrazení, jako je tlačítko klikne.</span><span class="sxs-lookup"><span data-stu-id="a6334-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="a6334-120">Tento přístup umožňuje snadno změnit rozložení a uživatelského rozhraní aplikace, protože vazby, můžete změnit bez přepsání jakéhokoli kódu.</span><span class="sxs-lookup"><span data-stu-id="a6334-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="a6334-121">Například může zobrazit seznam položek jako `<ul>`, pak ji později změnit na tabulku.</span><span class="sxs-lookup"><span data-stu-id="a6334-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="a6334-122">Přidání knihovny Knockout</span><span class="sxs-lookup"><span data-stu-id="a6334-122">Add the Knockout Library</span></span>

<span data-ttu-id="a6334-123">V sadě Visual Studio z **nástroje** nabídce vyberte možnost **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a6334-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="a6334-124">Potom vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="a6334-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="a6334-125">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="a6334-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="a6334-126">Tento příkaz přidá Knockout soubory do složky skriptů.</span><span class="sxs-lookup"><span data-stu-id="a6334-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="a6334-127">Vytvoření zobrazení modelu</span><span class="sxs-lookup"><span data-stu-id="a6334-127">Create the View Model</span></span>

<span data-ttu-id="a6334-128">Přidejte soubor JavaScriptu s názvem app.js do složky skriptů.</span><span class="sxs-lookup"><span data-stu-id="a6334-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="a6334-129">(V Průzkumníku řešení klikněte pravým tlačítkem na složku skripty, vyberte **přidat**a pak vyberte **soubor JavaScript**.) Vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="a6334-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="a6334-130">V Knockout `observable` třída umožňuje datové vazby.</span><span class="sxs-lookup"><span data-stu-id="a6334-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="a6334-131">Při změně obsahu pozorovat, upozorní pozorovat všechny ovládací prvky vázané na data, tak mohou aktualizovat sami.</span><span class="sxs-lookup"><span data-stu-id="a6334-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="a6334-132">( `observableArray` Třídy je pole verze *pozorovat*.) Začněte tím náš model zobrazení má dvě pozorovatelné objekty:</span><span class="sxs-lookup"><span data-stu-id="a6334-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- `books` <span data-ttu-id="a6334-133">obsahuje seznam knihy.</span><span class="sxs-lookup"><span data-stu-id="a6334-133">holds the list of books.</span></span>
- `error` <span data-ttu-id="a6334-134">obsahuje chybovou zprávu, pokud selže volání AJAX.</span><span class="sxs-lookup"><span data-stu-id="a6334-134">contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="a6334-135">`getAllBooks` Metoda provádí volání AJAX k získání seznamu knihy.</span><span class="sxs-lookup"><span data-stu-id="a6334-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="a6334-136">Pak uloží výsledek do `books` pole.</span><span class="sxs-lookup"><span data-stu-id="a6334-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="a6334-137">`ko.applyBindings` Metoda je součástí knihovny Knockout.</span><span class="sxs-lookup"><span data-stu-id="a6334-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="a6334-138">Model zobrazení jako parametr přijímá a nastaví datovou vazbu.</span><span class="sxs-lookup"><span data-stu-id="a6334-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="a6334-139">Přidat sadu skriptů</span><span class="sxs-lookup"><span data-stu-id="a6334-139">Add a Script Bundle</span></span>

<span data-ttu-id="a6334-140">Sdružování je funkce v technologii ASP.NET 4.5, který umožňuje snadno kombinovat nebo sady více souborů do jediného souboru.</span><span class="sxs-lookup"><span data-stu-id="a6334-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="a6334-141">Sdružování snižuje počet požadavků na server, což může zlepšit čas načítání stránky.</span><span class="sxs-lookup"><span data-stu-id="a6334-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="a6334-142">Otevřete soubor aplikace\_Start/BundleConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="a6334-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="a6334-143">Přidejte následující kód k metodě RegisterBundles.</span><span class="sxs-lookup"><span data-stu-id="a6334-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="a6334-144">[Předchozí](part-5.md)
> [další](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="a6334-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
