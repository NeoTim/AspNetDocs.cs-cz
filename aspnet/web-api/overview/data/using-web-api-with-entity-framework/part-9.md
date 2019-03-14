---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Přidat novou položku do databáze | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 01586ef6eecdbe1acfadfcfcc0c9ca8b442de2d3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072151"
---
<a name="add-a-new-item-to-the-database"></a><span data-ttu-id="51b54-102">Přidání nové položky do databáze</span><span class="sxs-lookup"><span data-stu-id="51b54-102">Add a New Item to the Database</span></span>
====================
<span data-ttu-id="51b54-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="51b54-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="51b54-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="51b54-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="51b54-105">V této části bude přidána možnost pro uživatele k vytvoření nového adresáře.</span><span class="sxs-lookup"><span data-stu-id="51b54-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="51b54-106">V app.js přidejte následující kód k zobrazení modelu:</span><span class="sxs-lookup"><span data-stu-id="51b54-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="51b54-107">V Index.cshtml nahraďte následující značky:</span><span class="sxs-lookup"><span data-stu-id="51b54-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="51b54-108">Pomocí:</span><span class="sxs-lookup"><span data-stu-id="51b54-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="51b54-109">Tento kód vytvoří formulář pro odeslání nového Autor.</span><span class="sxs-lookup"><span data-stu-id="51b54-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="51b54-110">Hodnoty pro autora rozevíracího seznamu je vázán na data `authors` pozorovatelných v modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="51b54-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="51b54-111">Pro ostatní vstupy formuláře, hodnoty jsou vázán na data `newBook` vlastnost modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="51b54-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="51b54-112">Obslužné rutiny odeslání ve formuláři je vázán na `addBook` funkce:</span><span class="sxs-lookup"><span data-stu-id="51b54-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="51b54-113">`addBook` Funkce přečte aktuální hodnoty vázané na data formuláře vstupy pro vytvoření objektu JSON.</span><span class="sxs-lookup"><span data-stu-id="51b54-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="51b54-114">Pak odešle objekt JSON, který má `/api/books`.</span><span class="sxs-lookup"><span data-stu-id="51b54-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="51b54-115">[Předchozí](part-8.md)
> [další](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="51b54-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
