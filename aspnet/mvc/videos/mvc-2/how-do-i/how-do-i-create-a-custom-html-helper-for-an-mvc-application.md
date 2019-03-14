---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 'Postup: Vytvoření vlastní pomocné rutiny HTML pro aplikaci MVC? | Dokumenty Microsoft'
author: rick-anderson
description: V tomto videu pixelů na Chris ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sady v aplikaci MVC. První, aplikace MVC ukázka...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 4061c06cfeab2278e5732295b034f81f7995c2a4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071836"
---
<a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="17ae4-105">Postup: Vytvoření vlastní pomocné rutiny HTML pro aplikaci MVC?</span><span class="sxs-lookup"><span data-stu-id="17ae4-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>
====================
<span data-ttu-id="17ae4-106">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="17ae4-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="17ae4-107">V tomto videu pixelů na Chris ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sady v aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="17ae4-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="17ae4-108">Nejprve ukázkové aplikace MVC se vytvoří s ukázka kontroler a zobrazení k testování vlastních HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="17ae4-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="17ae4-109">V dalším kroku se vytvoří modul s veřejné funkce, která je metodu rozšíření, která představuje implementaci vlastní HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="17ae4-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="17ae4-110">Je vlastního pomocného objektu pro vytváření `<img>` značky na stránce a přijímá několik vstupních parametrů včetně id, adresy url a alternativní text obrázku značky.</span><span class="sxs-lookup"><span data-stu-id="17ae4-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="17ae4-111">Logika se pak přidá do funkce pro vracení dokončené `<img>` značky se zadanými informacemi.</span><span class="sxs-lookup"><span data-stu-id="17ae4-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="17ae4-112">Vlastní HtmlHelper použije se na stránce Ukázky obrázek.</span><span class="sxs-lookup"><span data-stu-id="17ae4-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="17ae4-113">Nakonec je vlastní HtmlHelper rozšířen, aby zahrnoval několik konstruktor přepsání, které poskytují flexibilitu pro více snadno vytvářet různé `<img>` značky.</span><span class="sxs-lookup"><span data-stu-id="17ae4-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="17ae4-114">&#9654;Podívejte se na video (18 minut)</span><span class="sxs-lookup"><span data-stu-id="17ae4-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="17ae4-115">[Předchozí](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [další](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="17ae4-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>