---
title: Neměnnost klíče a nastavení klíče v ASP.NET Core
author: rick-anderson
description: Přečtěte si podrobnosti implementace neměnnost klíče na ochranu dat ASP.NET Core API.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-immutability
ms.openlocfilehash: 7796cb102c0f6f03809704016fd36b28c7a82438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069397"
---
# <a name="key-immutability-and-key-settings-in-aspnet-core"></a><span data-ttu-id="b259e-103">Neměnnost klíče a nastavení klíče v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b259e-103">Key immutability and key settings in ASP.NET Core</span></span>

<span data-ttu-id="b259e-104">Po trvalém uložení objektu do záložního úložiště je její znázornění vyřešen navždy.</span><span class="sxs-lookup"><span data-stu-id="b259e-104">Once an object is persisted to the backing store, its representation is forever fixed.</span></span> <span data-ttu-id="b259e-105">Nová data mohou být přidány do záložního úložiště, ale existující data může nikdy být mutována.</span><span class="sxs-lookup"><span data-stu-id="b259e-105">New data can be added to the backing store, but existing data can never be mutated.</span></span> <span data-ttu-id="b259e-106">Chcete-li zabránit poškození dat je primárním účelem toto chování.</span><span class="sxs-lookup"><span data-stu-id="b259e-106">The primary purpose of this behavior is to prevent data corruption.</span></span>

<span data-ttu-id="b259e-107">Důsledkem tohoto chování je, že jakmile klíč je zapsán do záložního úložiště, je neměnný.</span><span class="sxs-lookup"><span data-stu-id="b259e-107">One consequence of this behavior is that once a key is written to the backing store, it's immutable.</span></span> <span data-ttu-id="b259e-108">Jeho vytvoření, aktivace a datum vypršení platnosti může nikdy být změněn, i když můžete odvolat pomocí `IKeyManager`.</span><span class="sxs-lookup"><span data-stu-id="b259e-108">Its creation, activation, and expiration dates can never be changed, though it can revoked by using `IKeyManager`.</span></span> <span data-ttu-id="b259e-109">Kromě toho jeho základní informace o vylepšením, materiál hlavního klíče a šifrování na zbývající vlastnosti jsou také neměnné.</span><span class="sxs-lookup"><span data-stu-id="b259e-109">Additionally, its underlying algorithmic information, master keying material, and encryption at rest properties are also immutable.</span></span>

<span data-ttu-id="b259e-110">Pokud vývojář změní nastavení, která ovlivňuje trvalost klíče, tyto změny se projeví až při příštím klíč generován, buď prostřednictvím explicitní volání konstruktoru `IKeyManager.CreateNewKey` nebo přes data protection systému vlastní [automatické klíč generování](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) chování.</span><span class="sxs-lookup"><span data-stu-id="b259e-110">If the developer changes any setting that affects key persistence, those changes won't go into effect until the next time a key is generated, either via an explicit call to `IKeyManager.CreateNewKey` or via the data protection system's own [automatic key generation](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) behavior.</span></span> <span data-ttu-id="b259e-111">Nastavení, které ovlivňují trvalost klíče jsou následující:</span><span class="sxs-lookup"><span data-stu-id="b259e-111">The settings that affect key persistence are as follows:</span></span>

* [<span data-ttu-id="b259e-112">Výchozí doba platnosti klíče</span><span class="sxs-lookup"><span data-stu-id="b259e-112">The default key lifetime</span></span>](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)

* [<span data-ttu-id="b259e-113">Šifrování klíčů v mechanismu rest</span><span class="sxs-lookup"><span data-stu-id="b259e-113">The key encryption at rest mechanism</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest)

* [<span data-ttu-id="b259e-114">Vylepšením informací, které obsahuje daný klíč</span><span class="sxs-lookup"><span data-stu-id="b259e-114">The algorithmic information contained within the key</span></span>](xref:security/data-protection/configuration/overview#changing-algorithms-with-usecryptographicalgorithms)

<span data-ttu-id="b259e-115">Pokud budete potřebovat tato nastavení se rozjíždí dříve než Další automatické klíč času se zajištěním provozu, zvažte explicitní volání konstruktoru `IKeyManager.CreateNewKey` k vytvoření nového klíče.</span><span class="sxs-lookup"><span data-stu-id="b259e-115">If you need these settings to kick in earlier than the next automatic key rolling time, consider making an explicit call to `IKeyManager.CreateNewKey` to force the creation of a new key.</span></span> <span data-ttu-id="b259e-116">Nezapomeňte zadat datem explicitní aktivace ({nyní + 2 dny} je základním pravidlem na nějakou dobu počkat, změnit na dokončení propagace) a datum vypršení platnosti ve volání.</span><span class="sxs-lookup"><span data-stu-id="b259e-116">Remember to provide an explicit activation date ({ now + 2 days } is a good rule of thumb to allow time for the change to propagate) and expiration date in the call.</span></span>

>[!TIP]
> <span data-ttu-id="b259e-117">Všechny aplikace stisknutím úložiště by měl určit stejné nastavení s `IDataProtectionBuilder` metody rozšíření.</span><span class="sxs-lookup"><span data-stu-id="b259e-117">All applications touching the repository should specify the same settings with the `IDataProtectionBuilder` extension methods.</span></span> <span data-ttu-id="b259e-118">Vlastnosti trvalý klíč, jinak bude závisí na konkrétní aplikaci, která vyvolá rutiny generování klíčů.</span><span class="sxs-lookup"><span data-stu-id="b259e-118">Otherwise, the properties of the persisted key will be dependent on the particular application that invoked the key generation routines.</span></span>
