---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Vytvoření objektů pro přenos dat (DTO) | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 1af29955e8040c34840d4c77fc2006f59d2324dd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395274"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="3b5e4-102">Vytvoření objektů pro přenos dat (DTO)</span><span class="sxs-lookup"><span data-stu-id="3b5e4-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="3b5e4-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3b5e4-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3b5e4-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="3b5e4-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="3b5e4-105">Pravé teď naše webové rozhraní API zveřejňuje entity databáze do klienta.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="3b5e4-106">Klient obdrží data, která mapuje přímo na databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="3b5e4-107">Nicméně, který není vždy vhodné.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-107">However, that's not always a good idea.</span></span> <span data-ttu-id="3b5e4-108">Někdy budete chtít změnit tvar data, která odesíláte do klienta.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="3b5e4-109">Například můžete chtít:</span><span class="sxs-lookup"><span data-stu-id="3b5e4-109">For example, you might want to:</span></span>

- <span data-ttu-id="3b5e4-110">Odeberte cyklické odkazy (viz předchozí část).</span><span class="sxs-lookup"><span data-stu-id="3b5e4-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="3b5e4-111">Skryjte určité vlastnosti, které klienti neměl zobrazit.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="3b5e4-112">Vynechte některé vlastnosti, aby bylo možné zmenšit velikost datové části.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="3b5e4-113">Sloučení grafů objektů, které obsahují vnořené objekty, aby se daly vhodnější pro klienty.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="3b5e4-114">Vyhněte se "over-pass-the účtování" ohrožení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="3b5e4-115">(Viz [ověření modelu](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) diskuzi o navýšení účtování.)</span><span class="sxs-lookup"><span data-stu-id="3b5e4-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="3b5e4-116">Oddělte vrstvě služby z vrstvy vaší databáze.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="3b5e4-117">Chcete-li to provést, můžete definovat *objekt pro přenos dat* (DTO).</span><span class="sxs-lookup"><span data-stu-id="3b5e4-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="3b5e4-118">Objekt DTO je objekt, který definuje, jak data se odešlou přes síť.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="3b5e4-119">Podívejme se, jak to funguje s entitou knihy.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="3b5e4-120">Ve složce modely přidejte dvě DTO třídy:</span><span class="sxs-lookup"><span data-stu-id="3b5e4-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="3b5e4-121">`BookDetailDTO` Třída zahrnuje všechny vlastnosti z knihy modelu, s výjimkou, že `AuthorName` je řetězec, který bude obsahovat jméno autora.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="3b5e4-122">`BookDTO` Třída obsahuje podmnožinu vlastností z `BookDetailDTO`.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="3b5e4-123">Tyto dvě metody GET v dalším kroku nahraďte `BooksController` třídy s verzemi, které vracejí DTO.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="3b5e4-124">Použijeme LINQ **vyberte** příkaz Převést ze seznamu entit na DTO.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="3b5e4-125">Tady je SQL vygeneroval nový `GetBooks` metody.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="3b5e4-126">Uvidíte, že překládá EF LINQ **vyberte** do příkazu SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="3b5e4-127">Nakonec upravte `PostBook` metoda vrátí objekt DTO.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="3b5e4-128">V tomto kurzu převádíme na DTO ručně v kódu.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="3b5e4-129">Další možností je použít knihovnu jako [AutoMapper](http://automapper.org/) , která zpracovává server převod automaticky.</span><span class="sxs-lookup"><span data-stu-id="3b5e4-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="3b5e4-130">[Předchozí](part-4.md)
> [další](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="3b5e4-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
