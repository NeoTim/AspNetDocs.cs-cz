---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Principy procesu provádění ASP.NET MVC | Dokumenty společnosti Microsoft
author: rick-anderson
description: Zjistěte, jak ASP.NET rozhraní MVC zpracovává požadavek prohlížeče krok za krokem.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541023"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="dd904-103">Principy procesu spuštění ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="dd904-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="dd904-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dd904-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="dd904-105">Zjistěte, jak ASP.NET rozhraní MVC zpracovává požadavek prohlížeče krok za krokem.</span><span class="sxs-lookup"><span data-stu-id="dd904-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="dd904-106">Požadavky na ASP.NET webovou aplikaci založenou na MVC nejprve projdou objektem **UrlRoutingModule,** což je modul HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd904-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="dd904-107">Tento modul analyzuje požadavek a provede výběr trasy.</span><span class="sxs-lookup"><span data-stu-id="dd904-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="dd904-108">Objekt **UrlRoutingModule** vybere první objekt trasy, který odpovídá aktuálnímu požadavku.</span><span class="sxs-lookup"><span data-stu-id="dd904-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="dd904-109">(Objekt trasy je třída, která implementuje **RouteBase**a je obvykle instancí třídy **Route.)** Pokud se žádné trasy neshodují, objekt **UrlRoutingModule** neprovede žádnou akci a umožní požadavku vrátit se zpět k běžnému zpracování požadavků ASP.NET nebo IIS.</span><span class="sxs-lookup"><span data-stu-id="dd904-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="dd904-110">Z vybraného objektu **Route** získá objekt **UrlRoutingModule** objekt **IRouteHandler,** který je přidružen k objektu **Route.**</span><span class="sxs-lookup"><span data-stu-id="dd904-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="dd904-111">Obvykle v aplikaci MVC to bude instance **MvcRouteHandler**.</span><span class="sxs-lookup"><span data-stu-id="dd904-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="dd904-112">Instance **IRouteHandler** vytvoří objekt **IHttpHandler** a předá mu objekt **IHttpContext.**</span><span class="sxs-lookup"><span data-stu-id="dd904-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="dd904-113">Ve výchozím nastavení je instance **IHttpHandler** pro MVC **objektem MvcHandler.**</span><span class="sxs-lookup"><span data-stu-id="dd904-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="dd904-114">**MvcHandler** objekt pak vybere řadič, který bude nakonec zpracování požadavku.</span><span class="sxs-lookup"><span data-stu-id="dd904-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="dd904-115">Pokud je ve službě IIS 7.0 spuštěna ASP.NET webová aplikace MVC, není pro projekty MVC vyžadována žádná přípona názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="dd904-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="dd904-116">Ve službách IIS 6.0 však obslužná rutina vyžaduje, abyste namapovali příponu názvu souboru MVC na ASP.NET dll ISAPI.</span><span class="sxs-lookup"><span data-stu-id="dd904-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="dd904-117">Modul a obslužná rutina jsou vstupní body do ASP.NET rámci MVC.</span><span class="sxs-lookup"><span data-stu-id="dd904-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="dd904-118">Provádějí následující akce:</span><span class="sxs-lookup"><span data-stu-id="dd904-118">They perform the following actions:</span></span>

- <span data-ttu-id="dd904-119">Vyberte příslušný řadič ve webové aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="dd904-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="dd904-120">Získejte konkrétní instanci řadiče.</span><span class="sxs-lookup"><span data-stu-id="dd904-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="dd904-121">Volání metody **spuštění** řadiče.</span><span class="sxs-lookup"><span data-stu-id="dd904-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="dd904-122">V následujícím seznamu jsou uvedeny fáze provádění webového projektu MVC:</span><span class="sxs-lookup"><span data-stu-id="dd904-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="dd904-123">Přijmout první žádost o žádost</span><span class="sxs-lookup"><span data-stu-id="dd904-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="dd904-124">V souboru Global.asax jsou objekty **Route** přidány do objektu **RouteTable.**</span><span class="sxs-lookup"><span data-stu-id="dd904-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="dd904-125">Provedení směrování</span><span class="sxs-lookup"><span data-stu-id="dd904-125">Perform routing</span></span> 

    - <span data-ttu-id="dd904-126">Modul **UrlRoutingModule** používá první odpovídající objekt **Route** v kolekci **RouteTable** k vytvoření objektu **RouteData,** který pak použije k vytvoření objektu **RequestContext** (**IHttpContext).**</span><span class="sxs-lookup"><span data-stu-id="dd904-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="dd904-127">Vytvořit obslužnou rutinu požadavku MVC</span><span class="sxs-lookup"><span data-stu-id="dd904-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="dd904-128">Objekt **MvcRouteHandler** vytvoří instanci třídy **MvcHandler** a předá jí instanci **RequestContext.**</span><span class="sxs-lookup"><span data-stu-id="dd904-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="dd904-129">Vytvořit ovladač</span><span class="sxs-lookup"><span data-stu-id="dd904-129">Create controller</span></span> 

    - <span data-ttu-id="dd904-130">Objekt **MvcHandler** používá instanci **RequestContext** k identifikaci objektu **IControllerFactory** (obvykle instance třídy **DefaultControllerFactory)** k vytvoření instance řadiče.</span><span class="sxs-lookup"><span data-stu-id="dd904-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="dd904-131">Řadič spouštění – instance **MvcHandler** volá metodu s **Execute** řadiče.</span><span class="sxs-lookup"><span data-stu-id="dd904-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="dd904-132">Vyvolat akci</span><span class="sxs-lookup"><span data-stu-id="dd904-132">Invoke action</span></span> 

    - <span data-ttu-id="dd904-133">Většina řadičů dědí ze základní třídy **řadiče.**</span><span class="sxs-lookup"><span data-stu-id="dd904-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="dd904-134">Pro řadiče, které tak učiní, **ControllerActionInvoker** objekt, který je přidružen k řadiči určuje, které metody akce třídy kontroleru volat a pak volá tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="dd904-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="dd904-135">Výsledek provedení</span><span class="sxs-lookup"><span data-stu-id="dd904-135">Execute result</span></span> 

    - <span data-ttu-id="dd904-136">Typická metoda akce může přijímat vstup uživatele, připravit příslušná data odpovědi a potom provést výsledek vrácením typu výsledku.</span><span class="sxs-lookup"><span data-stu-id="dd904-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="dd904-137">Předdefinované typy výsledků, které lze provést, zahrnují následující: **ViewResult** (který vykresluje zobrazení a je nejčastěji používaným typem výsledku), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**a **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="dd904-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
