---
uid: webhooks/receiving/receivers
title: ASP.NET WebHooks přijímače | Dokumenty společnosti Microsoft
author: rick-anderson
description: ASP.NET přijímače WebHooks
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675168"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="3e60f-103">ASP.NET přijímače WebHooks</span><span class="sxs-lookup"><span data-stu-id="3e60f-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="3e60f-104">Příjem WebHooks závisí na tom, kdo je odesílatel.</span><span class="sxs-lookup"><span data-stu-id="3e60f-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="3e60f-105">Někdy existují další kroky registrace WebHook ověření, že odběratel je opravdu naslouchání.</span><span class="sxs-lookup"><span data-stu-id="3e60f-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="3e60f-106">Některé WebHooks poskytují model push-to-pull, kde požadavek HTTP POST obsahuje pouze odkaz na informace o události, které mají být načteny nezávisle.</span><span class="sxs-lookup"><span data-stu-id="3e60f-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="3e60f-107">Často se model zabezpečení liší docela dost.</span><span class="sxs-lookup"><span data-stu-id="3e60f-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="3e60f-108">Účelem Microsoft ASP.NET WebHooks je, aby bylo jednodušší a konzistentnější, aby se vaše rozhraní API, aniž by strávil spoustu času přijít na to, jak zacházet s konkrétní variantou WebHooks.</span><span class="sxs-lookup"><span data-stu-id="3e60f-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="3e60f-109">Přijímač WebHook je zodpovědný za přijetí a ověření WebHooks od konkrétního odesílatele.</span><span class="sxs-lookup"><span data-stu-id="3e60f-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="3e60f-110">Přijímač WebHook může podporovat libovolný počet WebHooks, každý s vlastní konfigurací.</span><span class="sxs-lookup"><span data-stu-id="3e60f-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="3e60f-111">Například přijímač GitHub WebHook může přijímat WebHooks z libovolného počtu úložišť GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e60f-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="3e60f-112">WebHook přijímač URis</span><span class="sxs-lookup"><span data-stu-id="3e60f-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="3e60f-113">Instalací microsoft ASP.NET WebHooks získáte obecný řadič WebHook, který přijímá požadavky WebHook z otevřeného počtu služeb.</span><span class="sxs-lookup"><span data-stu-id="3e60f-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="3e60f-114">Když přijde požadavek, vybere příslušný příjemce, který jste nainstalovali pro zpracování konkrétní webhooku odesílatele.</span><span class="sxs-lookup"><span data-stu-id="3e60f-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="3e60f-115">Identifikátor URI tohoto řadiče je identifikátor URI WebHook, který se zaregistrujete u služby a je formuláře:</span><span class="sxs-lookup"><span data-stu-id="3e60f-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="3e60f-116">Z bezpečnostních důvodů mnoho přijímačů WebHook vyžaduje, aby identifikátor URI byl *identifikátor URI https* a v některých případech musí také obsahovat další parametr dotazu, který se používá k vynucení, že pouze zamýšlená strana může odeslat WebHooks do identifikátoru URI výše.</span><span class="sxs-lookup"><span data-stu-id="3e60f-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="3e60f-117">Komponenta `<receiver>` je název příjemce, `github` například `slack`nebo .</span><span class="sxs-lookup"><span data-stu-id="3e60f-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="3e60f-118">*{id}* je volitelný identifikátor, který lze použít k identifikaci konkrétní konfigurace přijímače WebHook.</span><span class="sxs-lookup"><span data-stu-id="3e60f-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="3e60f-119">To lze použít k registraci N WebHooks s konkrétním přijímačem.</span><span class="sxs-lookup"><span data-stu-id="3e60f-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="3e60f-120">Například následující tři identifikátory URI lze použít k registraci pro tři nezávislé WebHooks:</span><span class="sxs-lookup"><span data-stu-id="3e60f-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="3e60f-121">Instalace přijímače WebHook</span><span class="sxs-lookup"><span data-stu-id="3e60f-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="3e60f-122">Chcete-li přijímat WebHooks pomocí Microsoft ASP.NET WebHooks, nejprve nainstalovat balíček Nuget pro webhooku poskytovatele nebo zprostředkovatele, které chcete přijímat WebHooks od.</span><span class="sxs-lookup"><span data-stu-id="3e60f-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="3e60f-123">Balíčky Nuget se nazývají [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) kde poslední část označuje podporovanou službu.</span><span class="sxs-lookup"><span data-stu-id="3e60f-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="3e60f-124">Například</span><span class="sxs-lookup"><span data-stu-id="3e60f-124">For example</span></span>

<span data-ttu-id="3e60f-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) poskytuje podporu pro příjem WebHooks z GitHub a [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) poskytuje podporu pro příjem WebHooks generované ASP.NET WebHooks.</span><span class="sxs-lookup"><span data-stu-id="3e60f-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="3e60f-126">Po vybalení z krabice můžete najít podporu pro Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello a WordPress, ale je možné podporovat libovolný počet dalších poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="3e60f-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="3e60f-127">Konfigurace přijímače WebHook</span><span class="sxs-lookup"><span data-stu-id="3e60f-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="3e60f-128">WebHook přijímače jsou konfigurovány prostřednictvím [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface a konkrétní implementace tohoto rozhraní lze zaregistrovat pomocí libovolného modelu vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="3e60f-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="3e60f-129">Výchozí implementace používá nastavení aplikace, které lze nastavit v souboru Web.config, nebo pokud používáte Azure Web Apps, lze nastavit prostřednictvím [portálu Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3e60f-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Nastavení aplikace Azure](_static/AzureAppSettings.png)

<span data-ttu-id="3e60f-131">Formát kláves nastavení aplikace je následující:</span><span class="sxs-lookup"><span data-stu-id="3e60f-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="3e60f-132">Hodnota je seznam hodnot oddělených čárkami, které odpovídají *hodnotám {id},* pro které byly zaregistrovány webhooky, například:</span><span class="sxs-lookup"><span data-stu-id="3e60f-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="3e60f-133">Inicializace přijímače WebHook</span><span class="sxs-lookup"><span data-stu-id="3e60f-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="3e60f-134">WebHook Přijímače jsou inicializovány jejich registrací, obvykle ve statické třídě *WebApiConfig,* například:</span><span class="sxs-lookup"><span data-stu-id="3e60f-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
