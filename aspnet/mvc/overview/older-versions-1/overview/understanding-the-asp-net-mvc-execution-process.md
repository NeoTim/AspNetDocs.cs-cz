---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Principy procesu spuštění ASP.NET MVC | Dokumentace Microsoftu
author: microsoft
description: Zjistěte, jak rozhraní ASP.NET MVC zpracovává žádost prohlížeče krok za krokem.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125473"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Principy procesu spuštění ASP.NET MVC

by [Microsoft](https://github.com/microsoft)

> Zjistěte, jak rozhraní ASP.NET MVC zpracovává žádost prohlížeče krok za krokem.

Požadavky na aplikace založené na ASP.NET MVC nejdřív projít **UrlRoutingModule** objekt, který je modul HTTP. Tento modul analyzuje požadavek a provádí výběr trasy. **UrlRoutingModule** objekt vybere první objekt trasy, která odpovídá aktuální požadavek. (Objekt trasy je třída, která implementuje **RouteBase**, a je obvykle instance **trasy** třídy.) Pokud neodpovídají žádné trasy **UrlRoutingModule** objekt nemá žádný účinek a umožňuje vrátit zpět k pravidelné žádosti ASP.NET nebo IIS zpracování požadavku.

Z vybraného **trasy** objektu, **UrlRoutingModule** získává objekt **IRouteHandler** objekt, který je přidružený **trasy**objektu. V aplikaci MVC to bude obvykle instance **MvcRouteHandler**. **IRouteHandler** vytvoří instanci **IHttpHandler** objektu a předává je **IHttpContext** objektu. Ve výchozím nastavení **IHttpHandler** instance pro MVC je **MvcHandler** objektu. **MvcHandler** objekt potom vybere kontroler, který bude žádost zpracovat.

> [!NOTE]
> Při spuštění aplikace ASP.NET MVC Web ve službě IIS 7.0, bez přípony názvu souboru je vyžadována pro projekty MVC. Ale ve službě IIS 6.0, obslužná rutina vyžaduje namapovat příponu názvu souboru .mvc na knihovnu DLL ISAPI technologie ASP.NET.

Modul a obslužné rutiny jsou vstupními body k rozhraní ASP.NET MVC. Provádějí následující akce:

- Vyberte příslušný řadič v MVC webovou aplikaci.
- Získání instance konkrétní kontroleru.
- Volání kontroler **Execute** metody.

Následuje seznam fáze spuštění pro projekt MVC:

- Zobrazí první požadavek pro aplikaci 

    - V souboru Global.asax **trasy** objekty jsou přidány do **směrovací tabulky** objektu.
- Provést směrování 

    - **UrlRoutingModule** modul použije první odpovídající **trasy** objekt **směrovací tabulky** kolekce k vytvoření **RouteData** objekt, který pak použije k vytvoření **RequestContext** (**IHttpContext**) objektu.
- Vytvořte obslužnou rutinu požadavků MVC 

    - **MvcRouteHandler** vytvoří instanci objektu **MvcHandler** třídy a předává je **RequestContext** instance.
- Vytvoření kontroleru 

    - **MvcHandler** objektu používá **RequestContext** k identifikaci instance **IControllerFactory** objektu (obvykle instance  **DefaultControllerFactory** třídy) k vytvoření instance kontroleru se.
- Spustit kontroler – **MvcHandler** instance volá řadiče s **Execute** – metoda. |
- Vyvolání akce 

    - Většina řadičů dědí **řadič** základní třídy. Pro kontrolery, které uděláte to tak **ControllerActionInvoker** objekt, který je spojen s řadičem Určuje, jakou metodu akce kontroleru třídy volat a pak volá tuto metodu.
- Spuštění výsledku 

    - Metoda typické akce může přijímat uživatelský vstup, připravit data odpovídající odpověď a následné provádění výsledek tak, že vrací typ výsledku. Typy integrovaných výsledků, které mohou být provedeny, patří: **ViewResult** (který vykreslí zobrazení a je většina často používaný výsledným typem), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**,  **JsonResult**, a **EmptyResult**.
