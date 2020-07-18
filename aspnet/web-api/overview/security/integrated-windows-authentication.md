---
uid: web-api/overview/security/integrated-windows-authentication
title: Integrované ověřování systému Windows | Microsoft Docs
author: MikeWasson
description: Popisuje použití integrovaného ověřování systému Windows ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424793"
---
# <a name="integrated-windows-authentication"></a><span data-ttu-id="0e661-103">Integrované ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="0e661-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="0e661-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0e661-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0e661-105">Integrované ověřování systému Windows umožňuje uživatelům přihlašovat se pomocí přihlašovacích údajů k Windows pomocí protokolu Kerberos nebo NTLM.</span><span class="sxs-lookup"><span data-stu-id="0e661-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="0e661-106">Klient odesílá pověření do autorizační hlavičky.</span><span class="sxs-lookup"><span data-stu-id="0e661-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="0e661-107">Ověřování systému Windows je nejvhodnější pro prostředí intranetu.</span><span class="sxs-lookup"><span data-stu-id="0e661-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="0e661-108">Další informace najdete v tématu [ověřování systému Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="0e661-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="0e661-109">Výhody</span><span class="sxs-lookup"><span data-stu-id="0e661-109">Advantages</span></span> | <span data-ttu-id="0e661-110">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="0e661-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="0e661-111">Integrováno do služby IIS.</span><span class="sxs-lookup"><span data-stu-id="0e661-111">Built into IIS.</span></span> | <span data-ttu-id="0e661-112">Nedoporučuje se pro internetové aplikace.</span><span class="sxs-lookup"><span data-stu-id="0e661-112">Not recommended for Internet applications.</span></span> | 
| <span data-ttu-id="0e661-113">Neposílá přihlašovací údaje uživatele v žádosti.</span><span class="sxs-lookup"><span data-stu-id="0e661-113">Does not send the user credentials in the request.</span></span> | <span data-ttu-id="0e661-114">Vyžaduje podporu protokolu Kerberos nebo NTLM v klientovi.</span><span class="sxs-lookup"><span data-stu-id="0e661-114">Requires Kerberos or NTLM support in the client.</span></span> |
| <span data-ttu-id="0e661-115">Pokud klientský počítač patří do domény (například intranetové aplikace), uživatel nemusí zadávat přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="0e661-115">If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="0e661-116">Klient musí být v doméně služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e661-116">Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="0e661-117">Pokud je vaše aplikace hostována v Azure a máte místní doménu služby Active Directory, zvažte federování vaší místní služby AD pomocí Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e661-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="0e661-118">Tímto způsobem se uživatelé můžou přihlašovat pomocí místních přihlašovacích údajů, ale ověřování provádí služba Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e661-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="0e661-119">Další informace najdete v tématu [ověřování Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0e661-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="0e661-120">Pokud chcete vytvořit aplikaci, která používá integrované ověřování systému Windows, vyberte šablonu intranetová aplikace v Průvodci projektem MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0e661-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="0e661-121">Tato šablona projektu vloží následující nastavení do souboru Web.config:</span><span class="sxs-lookup"><span data-stu-id="0e661-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="0e661-122">Na straně klienta funguje integrované ověřování systému Windows s jakýmkoli prohlížečem, který podporuje schéma ověřování [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , které zahrnuje většinu hlavních prohlížečů.</span><span class="sxs-lookup"><span data-stu-id="0e661-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="0e661-123">Pro klientské aplikace .NET třída **HttpClient** podporuje ověřování systému Windows:</span><span class="sxs-lookup"><span data-stu-id="0e661-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="0e661-124">Ověřování systému Windows je zranitelné vůči útokům prostřednictvím CSRF (mezi lokalitami).</span><span class="sxs-lookup"><span data-stu-id="0e661-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="0e661-125">Přečtěte si téma [prevence útoků proti falšování (CSRF) žádostí mezi weby](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="0e661-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
