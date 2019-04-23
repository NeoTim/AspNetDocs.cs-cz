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
ms.lasthandoff: 04/17/2019
ms.locfileid: "59415151"
---
# <a name="add-a-new-item-to-the-database"></a>Přidání nové položky do databáze

podle [Mike Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části bude přidána možnost pro uživatele k vytvoření nového adresáře. V app.js přidejte následující kód k zobrazení modelu:

[!code-javascript[Main](part-9/samples/sample1.js)]

V Index.cshtml nahraďte následující značky:

[!code-html[Main](part-9/samples/sample2.html)]

Pomocí:

[!code-html[Main](part-9/samples/sample3.html)]

Tento kód vytvoří formulář pro odeslání nového Autor. Hodnoty pro autora rozevíracího seznamu je vázán na data `authors` pozorovatelných v modelu zobrazení. Pro ostatní vstupy formuláře, hodnoty jsou vázán na data `newBook` vlastnost modelu zobrazení.

Obslužné rutiny odeslání ve formuláři je vázán na `addBook` funkce:

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` Funkce přečte aktuální hodnoty vázané na data formuláře vstupy pro vytvoření objektu JSON. Pak odešle objekt JSON, který má `/api/books`.

> [!div class="step-by-step"]
> [Předchozí](part-8.md)
> [další](part-10.md)
