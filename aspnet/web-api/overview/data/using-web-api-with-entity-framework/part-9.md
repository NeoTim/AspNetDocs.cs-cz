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
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415151"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="b0856-102">Přidání nové položky do databáze</span><span class="sxs-lookup"><span data-stu-id="b0856-102">Add a New Item to the Database</span></span>

<span data-ttu-id="b0856-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b0856-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b0856-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="b0856-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="b0856-105">V této části bude přidána možnost pro uživatele k vytvoření nového adresáře.</span><span class="sxs-lookup"><span data-stu-id="b0856-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="b0856-106">V app.js přidejte následující kód k zobrazení modelu:</span><span class="sxs-lookup"><span data-stu-id="b0856-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="b0856-107">V Index.cshtml nahraďte následující značky:</span><span class="sxs-lookup"><span data-stu-id="b0856-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="b0856-108">Pomocí:</span><span class="sxs-lookup"><span data-stu-id="b0856-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="b0856-109">Tento kód vytvoří formulář pro odeslání nového Autor.</span><span class="sxs-lookup"><span data-stu-id="b0856-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="b0856-110">Hodnoty pro autora rozevíracího seznamu je vázán na data `authors` pozorovatelných v modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b0856-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="b0856-111">Pro ostatní vstupy formuláře, hodnoty jsou vázán na data `newBook` vlastnost modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b0856-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="b0856-112">Obslužné rutiny odeslání ve formuláři je vázán na `addBook` funkce:</span><span class="sxs-lookup"><span data-stu-id="b0856-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="b0856-113">`addBook` Funkce přečte aktuální hodnoty vázané na data formuláře vstupy pro vytvoření objektu JSON.</span><span class="sxs-lookup"><span data-stu-id="b0856-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="b0856-114">Pak odešle objekt JSON, který má `/api/books`.</span><span class="sxs-lookup"><span data-stu-id="b0856-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0856-115">[Předchozí](part-8.md)
> [další](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="b0856-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
