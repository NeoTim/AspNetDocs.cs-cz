---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130447"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a><span data-ttu-id="018b4-101">Vpřed žádost o informace o proxy serveru nebo nástroj pro vyrovnávání zatížení</span><span class="sxs-lookup"><span data-stu-id="018b4-101">Forward request information with a proxy or load balancer</span></span>

<span data-ttu-id="018b4-102">Pokud je aplikace nasazena za proxy server nebo nástroje pro vyrovnávání zatížení, některé z původní informace o požadavku může být přeposílán aplikace v záhlaví požadavku.</span><span class="sxs-lookup"><span data-stu-id="018b4-102">If the app is deployed behind a proxy server or load balancer, some of the original request information might be forwarded to the app in request headers.</span></span> <span data-ttu-id="018b4-103">Tyto informace obvykle obsahuje schéma požadavku zabezpečení (`https`), hostitele a IP adresu klienta.</span><span class="sxs-lookup"><span data-stu-id="018b4-103">This information usually includes the secure request scheme (`https`), host, and client IP address.</span></span> <span data-ttu-id="018b4-104">Aplikace si automaticky tyto hlavičky žádosti mohli objevit a používat původní informace o žádostech.</span><span class="sxs-lookup"><span data-stu-id="018b4-104">Apps don't automatically read these request headers to discover and use the original request information.</span></span>

<span data-ttu-id="018b4-105">Schéma se používá při generování odkazů, které má vliv na tok ověřování u externích poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="018b4-105">The scheme is used in link generation that affects the authentication flow with external providers.</span></span> <span data-ttu-id="018b4-106">Zabezpečený režim ztráty (`https`) výsledkem generování adresy URL pro přesměrování nesprávné nezabezpečené aplikace.</span><span class="sxs-lookup"><span data-stu-id="018b4-106">Losing the secure scheme (`https`) results in the app generating incorrect insecure redirect URLs.</span></span>

<span data-ttu-id="018b4-107">Předané Middleware záhlaví využívat k zpřístupňování původní informace o požadavku do aplikace pro zpracování požadavku.</span><span class="sxs-lookup"><span data-stu-id="018b4-107">Use Forwarded Headers Middleware to make the original request information available to the app for request processing.</span></span>

<span data-ttu-id="018b4-108">Další informace naleznete v tématu <xref:host-and-deploy/proxy-load-balancer>.</span><span class="sxs-lookup"><span data-stu-id="018b4-108">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>
