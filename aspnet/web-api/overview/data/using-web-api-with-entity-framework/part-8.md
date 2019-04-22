---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Zobrazit podrobnosti o položkách | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389047"
---
# <a name="display-item-details"></a>Zobrazení podrobností o položkách

podle [Mike Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části přidáte možnost, chcete-li zobrazit podrobnosti pro jednotlivé knihy. V app.js přidejte následující kód k zobrazení modelu:

[!code-javascript[Main](part-8/samples/sample1.js)]

V Views/Home/Index.cshtml přidejte odkaz na podrobnosti o prvek svázat data:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Tím je vytvořena vazba obslužné rutiny kliknutí pro &lt;&gt; elementu `getBookDetail` funkce na model zobrazení.

Ve stejném souboru nahraďte následujícím mark-up:

[!code-html[Main](part-8/samples/sample3.html)]

tímto kódem:

[!code-html[Main](part-8/samples/sample4.html)]

Tento kód vytvoří tabulku, která je vázán na data vlastnosti `detail` pozorovatelných v modelu zobrazení.

"&lt;!--Ko –&gt; &quot; syntaxe umožňuje zahrnout Knockout vazby mimo prvek modelu DOM. V takovém případě `if` vazby způsobí, že v této části kódu, který se má zobrazit pouze tehdy, když `details` je jiná než null.

[!code-html[Main](part-8/samples/sample5.html)]

Když teď spusťte aplikaci a klikněte na některou &quot;podrobností&quot; odkazy, aplikace se zobrazí podrobnosti adresáře.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Předchozí](part-7.md)
> [další](part-9.md)
