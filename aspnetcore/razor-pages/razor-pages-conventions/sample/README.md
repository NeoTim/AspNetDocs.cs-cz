---
ms.openlocfilehash: 68a77fffb9e2ed0eba05cceb2bff041f159501c6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072619"
---
# <a name="aspnet-core-model-providers-sample"></a><span data-ttu-id="5be9b-101">Ukázka zprostředkovatele modelu ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5be9b-101">ASP.NET Core Model Providers Sample</span></span>

<span data-ttu-id="5be9b-102">Tento příklad ukazuje použití stránky Razor vlastní trasy a stránku zprostředkovatele modelu.</span><span class="sxs-lookup"><span data-stu-id="5be9b-102">This sample illustrates use of Razor Pages custom route and page model providers.</span></span> <span data-ttu-id="5be9b-103">Tato ukázka demonstruje funkce popsané v [trasy a aplikační konvence pro stránky Razor](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features) tématu.</span><span class="sxs-lookup"><span data-stu-id="5be9b-103">This sample demonstrates the features described in the [Razor Pages route and app conventions](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features) topic.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="5be9b-104">Příklady v této ukázce</span><span class="sxs-lookup"><span data-stu-id="5be9b-104">Examples in this sample</span></span>

| <span data-ttu-id="5be9b-105">Scénář</span><span class="sxs-lookup"><span data-stu-id="5be9b-105">Scenario</span></span> | <span data-ttu-id="5be9b-106">Ukázka vzorku</span><span class="sxs-lookup"><span data-stu-id="5be9b-106">Sample demo</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="5be9b-107">Vytváření modelu</span><span class="sxs-lookup"><span data-stu-id="5be9b-107">Model conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#model-conventions) | <span data-ttu-id="5be9b-108">Přidáte atribut trasy a záhlaví stránek vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="5be9b-108">Add a route attribute and header to the app's pages.</span></span> |
| [<span data-ttu-id="5be9b-109">Pomocí AddPageRoute přidejte trasu stránky</span><span class="sxs-lookup"><span data-stu-id="5be9b-109">Use AddPageRoute to add a page route</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#configure-a-page-route) | <span data-ttu-id="5be9b-110">Přidá zadanou trasu na stránku na zadanou stránku.</span><span class="sxs-lookup"><span data-stu-id="5be9b-110">Adds the specified route to the page at the specified page.</span></span> |
| [<span data-ttu-id="5be9b-111">Konvence akce modelu stránky</span><span class="sxs-lookup"><span data-stu-id="5be9b-111">Page model action conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#page-model-action-conventions) | <span data-ttu-id="5be9b-112">Přidat záhlaví stránky ve složce, přidat hlavičku do jediné stránce a konfigurace továrny filtru chcete přidat záhlaví stránek vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="5be9b-112">Add a header to pages in a folder, add a header to a single page, and configure a filter factory to add a header to the app's pages.</span></span> |
| [<span data-ttu-id="5be9b-113">Nahraďte stránky výchozího zprostředkovatele modelu aplikace</span><span class="sxs-lookup"><span data-stu-id="5be9b-113">Replace the default page app model provider</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#replace-the-default-page-app-model-provider) | <span data-ttu-id="5be9b-114">Změňte konvence pro pojmenovávání obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="5be9b-114">Change the conventions for handler naming.</span></span> |
