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
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Principy procesu spuštění ASP.NET MVC

podle [společnosti Microsoft](https://github.com/microsoft)

> Zjistěte, jak ASP.NET rozhraní MVC zpracovává požadavek prohlížeče krok za krokem.

Požadavky na ASP.NET webovou aplikaci založenou na MVC nejprve projdou objektem **UrlRoutingModule,** což je modul HTTP. Tento modul analyzuje požadavek a provede výběr trasy. Objekt **UrlRoutingModule** vybere první objekt trasy, který odpovídá aktuálnímu požadavku. (Objekt trasy je třída, která implementuje **RouteBase**a je obvykle instancí třídy **Route.)** Pokud se žádné trasy neshodují, objekt **UrlRoutingModule** neprovede žádnou akci a umožní požadavku vrátit se zpět k běžnému zpracování požadavků ASP.NET nebo IIS.

Z vybraného objektu **Route** získá objekt **UrlRoutingModule** objekt **IRouteHandler,** který je přidružen k objektu **Route.** Obvykle v aplikaci MVC to bude instance **MvcRouteHandler**. Instance **IRouteHandler** vytvoří objekt **IHttpHandler** a předá mu objekt **IHttpContext.** Ve výchozím nastavení je instance **IHttpHandler** pro MVC **objektem MvcHandler.** **MvcHandler** objekt pak vybere řadič, který bude nakonec zpracování požadavku.

> [!NOTE]
> Pokud je ve službě IIS 7.0 spuštěna ASP.NET webová aplikace MVC, není pro projekty MVC vyžadována žádná přípona názvu souboru. Ve službách IIS 6.0 však obslužná rutina vyžaduje, abyste namapovali příponu názvu souboru MVC na ASP.NET dll ISAPI.

Modul a obslužná rutina jsou vstupní body do ASP.NET rámci MVC. Provádějí následující akce:

- Vyberte příslušný řadič ve webové aplikaci MVC.
- Získejte konkrétní instanci řadiče.
- Volání metody **spuštění** řadiče.

V následujícím seznamu jsou uvedeny fáze provádění webového projektu MVC:

- Přijmout první žádost o žádost 

    - V souboru Global.asax jsou objekty **Route** přidány do objektu **RouteTable.**
- Provedení směrování 

    - Modul **UrlRoutingModule** používá první odpovídající objekt **Route** v kolekci **RouteTable** k vytvoření objektu **RouteData,** který pak použije k vytvoření objektu **RequestContext** (**IHttpContext).**
- Vytvořit obslužnou rutinu požadavku MVC 

    - Objekt **MvcRouteHandler** vytvoří instanci třídy **MvcHandler** a předá jí instanci **RequestContext.**
- Vytvořit ovladač 

    - Objekt **MvcHandler** používá instanci **RequestContext** k identifikaci objektu **IControllerFactory** (obvykle instance třídy **DefaultControllerFactory)** k vytvoření instance řadiče.
- Řadič spouštění – instance **MvcHandler** volá metodu s **Execute** řadiče. |
- Vyvolat akci 

    - Většina řadičů dědí ze základní třídy **řadiče.** Pro řadiče, které tak učiní, **ControllerActionInvoker** objekt, který je přidružen k řadiči určuje, které metody akce třídy kontroleru volat a pak volá tuto metodu.
- Výsledek provedení 

    - Typická metoda akce může přijímat vstup uživatele, připravit příslušná data odpovědi a potom provést výsledek vrácením typu výsledku. Předdefinované typy výsledků, které lze provést, zahrnují následující: **ViewResult** (který vykresluje zobrazení a je nejčastěji používaným typem výsledku), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**a **EmptyResult**.
