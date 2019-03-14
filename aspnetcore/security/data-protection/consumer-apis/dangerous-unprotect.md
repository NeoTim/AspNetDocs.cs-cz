---
title: Zrušení ochrany datových částí, které byly odvolány klíči v ASP.NET Core
author: rick-anderson
description: Zjistěte, jak zrušit ochranu dat, které jsou chráněné pomocí klíče, které od té doby byly odvolány, v aplikaci ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: security/data-protection/consumer-apis/dangerous-unprotect
ms.openlocfilehash: b93ab0fa650041afdfaf1ed5572cc7e081bba244
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077509"
---
# <a name="unprotect-payloads-whose-keys-have-been-revoked-in-aspnet-core"></a><span data-ttu-id="bce1a-103">Zrušení ochrany datových částí, které byly odvolány klíči v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bce1a-103">Unprotect payloads whose keys have been revoked in ASP.NET Core</span></span>


<a name="data-protection-consumer-apis-dangerous-unprotect"></a>

<span data-ttu-id="bce1a-104">Ochranu dat ASP.NET Core API nejsou určené především pro neomezenou trvalost důvěrné datových částí.</span><span class="sxs-lookup"><span data-stu-id="bce1a-104">The ASP.NET Core data protection APIs are not primarily intended for indefinite persistence of confidential payloads.</span></span> <span data-ttu-id="bce1a-105">Jiné technologie, jako je [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) a [Azure Rights Management](/rights-management/) jsou vhodnější pro scénář neomezené úložiště, a mají možnosti odpovídajícím způsobem silné správu klíčů.</span><span class="sxs-lookup"><span data-stu-id="bce1a-105">Other technologies like [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) and [Azure Rights Management](/rights-management/) are more suited to the scenario of indefinite storage, and they have correspondingly strong key management capabilities.</span></span> <span data-ttu-id="bce1a-106">Ale nutné dodat, není nic zakazují vývojář pro dlouhodobou ochranu důvěrných dat pomocí data protection API ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bce1a-106">That said, there's nothing prohibiting a developer from using the ASP.NET Core data protection APIs for long-term protection of confidential data.</span></span> <span data-ttu-id="bce1a-107">Odeberou se klíče nikdy z okruhu klíč, tedy `IDataProtector.Unprotect` zotaví vždy stávajících datových částí klíče jsou k dispozici a je platný.</span><span class="sxs-lookup"><span data-stu-id="bce1a-107">Keys are never removed from the key ring, so `IDataProtector.Unprotect` can always recover existing payloads as long as the keys are available and valid.</span></span>

<span data-ttu-id="bce1a-108">Však problém nastane, když se pokusí zrušit ochranu dat, která byla nastavená ochrana pomocí odvolané klíče, jako vývojář `IDataProtector.Unprotect` v tomto případě vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="bce1a-108">However, an issue arises when the developer tries to unprotect data that has been protected with a revoked key, as `IDataProtector.Unprotect` will throw an exception in this case.</span></span> <span data-ttu-id="bce1a-109">To může být u datových částí krátkodobé a jednorázové nebo přechodné (např. ověřovacích tokenů), a tyto druhy datových částí lze snadno znovu vytvořit v systému, v nejhorším případě návštěvník může být nutné se přihlásit znovu.</span><span class="sxs-lookup"><span data-stu-id="bce1a-109">This might be fine for short-lived or transient payloads (like authentication tokens), as these kinds of payloads can easily be recreated by the system, and at worst the site visitor might be required to log in again.</span></span> <span data-ttu-id="bce1a-110">Ale pro trvalých datových částí s `Unprotect` vyvolání výjimky může způsobit ztrátu dat nemůže být přijata.</span><span class="sxs-lookup"><span data-stu-id="bce1a-110">But for persisted payloads, having `Unprotect` throw could lead to unacceptable data loss.</span></span>

## <a name="ipersisteddataprotector"></a><span data-ttu-id="bce1a-111">IPersistedDataProtector</span><span class="sxs-lookup"><span data-stu-id="bce1a-111">IPersistedDataProtector</span></span>

<span data-ttu-id="bce1a-112">Aby podporoval scénář umožnit datové části má být zrušena ochrana dokonce i v případě odvolané klíče, obsahuje systém ochrany dat `IPersistedDataProtector` typu.</span><span class="sxs-lookup"><span data-stu-id="bce1a-112">To support the scenario of allowing payloads to be unprotected even in the face of revoked keys, the data protection system contains an `IPersistedDataProtector` type.</span></span> <span data-ttu-id="bce1a-113">Chcete-li získat instanci `IPersistedDataProtector`, stačí získat instanci `IDataProtector` v normálním způsobem a zkuste přetypování `IDataProtector` k `IPersistedDataProtector`.</span><span class="sxs-lookup"><span data-stu-id="bce1a-113">To get an instance of `IPersistedDataProtector`, simply get an instance of `IDataProtector` in the normal fashion and try casting the `IDataProtector` to `IPersistedDataProtector`.</span></span>

> [!NOTE]
> <span data-ttu-id="bce1a-114">Ne všechny `IDataProtector` instance může být převeden na `IPersistedDataProtector`.</span><span class="sxs-lookup"><span data-stu-id="bce1a-114">Not all `IDataProtector` instances can be cast to `IPersistedDataProtector`.</span></span> <span data-ttu-id="bce1a-115">Vývojáři měli použít C# jako operátor nebo podobné výjimky modulu CLR, aby způsobené neplatné přetypování a musí být připraveni odpovídajícím způsobem zpracovat případ selhání.</span><span class="sxs-lookup"><span data-stu-id="bce1a-115">Developers should use the C# as operator or similar to avoid runtime exceptions caused by invalid casts, and they should be prepared to handle the failure case appropriately.</span></span>

<span data-ttu-id="bce1a-116">`IPersistedDataProtector` poskytuje následující plochy rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="bce1a-116">`IPersistedDataProtector` exposes the following API surface:</span></span>

```csharp
DangerousUnprotect(byte[] protectedData, bool ignoreRevocationErrors,
     out bool requiresMigration, out bool wasRevoked) : byte[]
```

<span data-ttu-id="bce1a-117">Toto rozhraní API chráněné datové části (jako pole bajtů) přijímá a vrací nechráněné datové části.</span><span class="sxs-lookup"><span data-stu-id="bce1a-117">This API takes the protected payload (as a byte array) and returns the unprotected payload.</span></span> <span data-ttu-id="bce1a-118">Neexistuje žádné přetížení založené na řetězci.</span><span class="sxs-lookup"><span data-stu-id="bce1a-118">There's no string-based overload.</span></span> <span data-ttu-id="bce1a-119">Dvě výstupní parametry jsou následující.</span><span class="sxs-lookup"><span data-stu-id="bce1a-119">The two out parameters are as follows.</span></span>

* <span data-ttu-id="bce1a-120">`requiresMigration`: se nastavenou na hodnotu true, pokud klíč používaný k ochraně tato datová část už není aktivní výchozí klíč, například je starý klíč používaný k ochraně tato datová část a operace se zajištěním provozu klíči ještě zbývá od provedou místo.</span><span class="sxs-lookup"><span data-stu-id="bce1a-120">`requiresMigration`: will be set to true if the key used to protect this payload is no longer the active default key, e.g., the key used to protect this payload is old and a key rolling operation has since taken place.</span></span> <span data-ttu-id="bce1a-121">Volající může chtít vezměte v úvahu znovu se zapíná ochrana datové části v závislosti na svých obchodních potřeb.</span><span class="sxs-lookup"><span data-stu-id="bce1a-121">The caller may wish to consider reprotecting the payload depending on their business needs.</span></span>

* <span data-ttu-id="bce1a-122">`wasRevoked`: bude nastavena na hodnotu true, pokud klíč používaný k ochraně tato datová část byl odvolán.</span><span class="sxs-lookup"><span data-stu-id="bce1a-122">`wasRevoked`: will be set to true if the key used to protect this payload was revoked.</span></span>

>[!WARNING]
> <span data-ttu-id="bce1a-123">Výkon extrémně opatrní při předávání `ignoreRevocationErrors: true` k `DangerousUnprotect` metody.</span><span class="sxs-lookup"><span data-stu-id="bce1a-123">Exercise extreme caution when passing `ignoreRevocationErrors: true` to the `DangerousUnprotect` method.</span></span> <span data-ttu-id="bce1a-124">Pokud po volání této metody `wasRevoked` je hodnota true, pak klíč používaný k ochraně tato datová část byla odvolána a pravosti datové části mají být považována za podezřelé.</span><span class="sxs-lookup"><span data-stu-id="bce1a-124">If after calling this method the `wasRevoked` value is true, then the key used to protect this payload was revoked, and the payload's authenticity should be treated as suspect.</span></span> <span data-ttu-id="bce1a-125">V takovém případě pouze pokračujte provozní nechráněné datovou část, pokud máte některé samostatné zárukou, že je platná, například, že se chystá v zabezpečené databázi spíše než odesíláno nedůvěryhodné webového klienta.</span><span class="sxs-lookup"><span data-stu-id="bce1a-125">In this case, only continue operating on the unprotected payload if you have some separate assurance that it's authentic, e.g. that it's coming from a secure database rather than being sent by an untrusted web client.</span></span>

[!code-csharp[](dangerous-unprotect/samples/dangerous-unprotect.cs)]
