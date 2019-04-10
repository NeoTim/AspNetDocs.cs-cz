---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Vytvoření akce (C#) | Dokumentace Microsoftu
author: microsoft
description: Zjistěte, jak přidat novou akci kontroler ASP.NET MVC. Další informace o požadavcích pro metodu na akci.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: c66e066bd3e241e667924dacc114f57151df822a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59389554"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="0161b-104">Vytvoření akce (C#)</span><span class="sxs-lookup"><span data-stu-id="0161b-104">Creating an Action (C#)</span></span>

<span data-ttu-id="0161b-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0161b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0161b-106">Zjistěte, jak přidat novou akci kontroler ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0161b-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="0161b-107">Další informace o požadavcích pro metodu na akci.</span><span class="sxs-lookup"><span data-stu-id="0161b-107">Learn about the requirements for a method to be an action.</span></span>


<span data-ttu-id="0161b-108">Cílem tohoto kurzu je vysvětlují, jak můžete vytvořit nové akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0161b-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="0161b-109">Informace o požadavky na metodu akce.</span><span class="sxs-lookup"><span data-stu-id="0161b-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="0161b-110">Také se dozvíte, jak zabránit metodu vystaven jako akci.</span><span class="sxs-lookup"><span data-stu-id="0161b-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="0161b-111">Přidání akce Kontroleru</span><span class="sxs-lookup"><span data-stu-id="0161b-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="0161b-112">Přidejte novou akci k řadiči tak, že přidáte nové metody pro kontroler.</span><span class="sxs-lookup"><span data-stu-id="0161b-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="0161b-113">Například řadič v informacích 1 obsahuje akce s názvem Index() a akce s názvem SayHello().</span><span class="sxs-lookup"><span data-stu-id="0161b-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="0161b-114">Obě metody jsou vystaveny jako akce.</span><span class="sxs-lookup"><span data-stu-id="0161b-114">Both methods are exposed as actions.</span></span>

**<span data-ttu-id="0161b-115">Výpis 1 - Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="0161b-115">Listing 1 - Controllers\HomeController.cs</span></span>**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="0161b-116">Aby bylo možné vystavit rozhraní universe jako akci, metoda musí splňovat určité požadavky:</span><span class="sxs-lookup"><span data-stu-id="0161b-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="0161b-117">Metoda musí být veřejné.</span><span class="sxs-lookup"><span data-stu-id="0161b-117">The method must be public.</span></span>
- <span data-ttu-id="0161b-118">Metoda nemůže být statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="0161b-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="0161b-119">Metoda nemůže být metodou rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0161b-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="0161b-120">Metoda nemůže být konstruktor, metoda getter nebo setter.</span><span class="sxs-lookup"><span data-stu-id="0161b-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="0161b-121">Metoda nemůže mít otevřených obecných typů.</span><span class="sxs-lookup"><span data-stu-id="0161b-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="0161b-122">Metoda není metodu základní třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0161b-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="0161b-123">Metoda nemůže obsahovat **ref** nebo **si** parametry.</span><span class="sxs-lookup"><span data-stu-id="0161b-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="0161b-124">Všimněte si, že neexistují žádná omezení u návratového typu akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0161b-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="0161b-125">Akce kontroleru vrátit řetězec, DateTime, instance třídy Random nebo void.</span><span class="sxs-lookup"><span data-stu-id="0161b-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="0161b-126">Architektura ASP.NET MVC se převést návratový typ, který není výsledek akce do řetězce a vykreslit řetězec, který se v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="0161b-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="0161b-127">Když přidáte jakoukoli metodu, která nebudou porušovat tyto požadavky na řadič, metoda je vystavena jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0161b-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="0161b-128">Buďte opatrní tady.</span><span class="sxs-lookup"><span data-stu-id="0161b-128">Be careful here.</span></span> <span data-ttu-id="0161b-129">Akce kontroleru můžete vyvolat každý připojený k Internetu.</span><span class="sxs-lookup"><span data-stu-id="0161b-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="0161b-130">Ne, například vytvořit DeleteMyWebsite() akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0161b-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="0161b-131">Brání veřejnou metodu volanou</span><span class="sxs-lookup"><span data-stu-id="0161b-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="0161b-132">Pokud je potřeba vytvořit veřejnou metodu do třídy kontroleru a nechcete vystavit metodu akce kontroleru můžete zabránit metody vyvolání pomocí atributu [NonAction].</span><span class="sxs-lookup"><span data-stu-id="0161b-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="0161b-133">Například kontroler v informacích 2 obsahuje veřejnou metodu s názvem CompanySecrets(), který je upraven pomocí atributu [NonAction].</span><span class="sxs-lookup"><span data-stu-id="0161b-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

**<span data-ttu-id="0161b-134">Výpis 2 - Controllers\WorkController.cs</span><span class="sxs-lookup"><span data-stu-id="0161b-134">Listing 2 - Controllers\WorkController.cs</span></span>**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="0161b-135">Pokud při pokusu o vyvolání akce kontroleru CompanySecrets() zadáním /Work/CompanySecrets do adresního řádku prohlížeče zobrazí se zpráva chyby na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="0161b-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>


[![I<span data-ttu-id="0161b-136">Metoda NonAction nvoking]</span><span class="sxs-lookup"><span data-stu-id="0161b-136">nvoking a NonAction method]</span></span>(creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

<span data-ttu-id="0161b-137">**Obrázek 01**: Volání metody NonAction ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="0161b-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0161b-138">[Předchozí](creating-a-controller-cs.md)
> [další](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0161b-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
