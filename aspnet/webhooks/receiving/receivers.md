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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET přijímače WebHooks

Příjem WebHooks závisí na tom, kdo je odesílatel. Někdy existují další kroky registrace WebHook ověření, že odběratel je opravdu naslouchání. Některé WebHooks poskytují model push-to-pull, kde požadavek HTTP POST obsahuje pouze odkaz na informace o události, které mají být načteny nezávisle. Často se model zabezpečení liší docela dost.

Účelem Microsoft ASP.NET WebHooks je, aby bylo jednodušší a konzistentnější, aby se vaše rozhraní API, aniž by strávil spoustu času přijít na to, jak zacházet s konkrétní variantou WebHooks.

Přijímač WebHook je zodpovědný za přijetí a ověření WebHooks od konkrétního odesílatele. Přijímač WebHook může podporovat libovolný počet WebHooks, každý s vlastní konfigurací. Například přijímač GitHub WebHook může přijímat WebHooks z libovolného počtu úložišť GitHub.

## <a name="webhook-receiver-uris"></a>WebHook přijímač URis

Instalací microsoft ASP.NET WebHooks získáte obecný řadič WebHook, který přijímá požadavky WebHook z otevřeného počtu služeb. Když přijde požadavek, vybere příslušný příjemce, který jste nainstalovali pro zpracování konkrétní webhooku odesílatele.

Identifikátor URI tohoto řadiče je identifikátor URI WebHook, který se zaregistrujete u služby a je formuláře:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Z bezpečnostních důvodů mnoho přijímačů WebHook vyžaduje, aby identifikátor URI byl *identifikátor URI https* a v některých případech musí také obsahovat další parametr dotazu, který se používá k vynucení, že pouze zamýšlená strana může odeslat WebHooks do identifikátoru URI výše.

Komponenta `<receiver>` je název příjemce, `github` například `slack`nebo .

*{id}* je volitelný identifikátor, který lze použít k identifikaci konkrétní konfigurace přijímače WebHook. To lze použít k registraci N WebHooks s konkrétním přijímačem. Například následující tři identifikátory URI lze použít k registraci pro tři nezávislé WebHooks:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Instalace přijímače WebHook

Chcete-li přijímat WebHooks pomocí Microsoft ASP.NET WebHooks, nejprve nainstalovat balíček Nuget pro webhooku poskytovatele nebo zprostředkovatele, které chcete přijímat WebHooks od. Balíčky Nuget se nazývají [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) kde poslední část označuje podporovanou službu. Například

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) poskytuje podporu pro příjem WebHooks z GitHub a [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) poskytuje podporu pro příjem WebHooks generované ASP.NET WebHooks.

Po vybalení z krabice můžete najít podporu pro Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello a WordPress, ale je možné podporovat libovolný počet dalších poskytovatelů.

## <a name="configuring-a-webhook-receiver"></a>Konfigurace přijímače WebHook

WebHook přijímače jsou konfigurovány prostřednictvím [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface a konkrétní implementace tohoto rozhraní lze zaregistrovat pomocí libovolného modelu vkládání závislostí. Výchozí implementace používá nastavení aplikace, které lze nastavit v souboru Web.config, nebo pokud používáte Azure Web Apps, lze nastavit prostřednictvím [portálu Azure Portal](https://portal.azure.com/).

![Nastavení aplikace Azure](_static/AzureAppSettings.png)

Formát kláves nastavení aplikace je následující:

```
MS_WebHookReceiverSecret_<receiver>
```

Hodnota je seznam hodnot oddělených čárkami, které odpovídají *hodnotám {id},* pro které byly zaregistrovány webhooky, například:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Inicializace přijímače WebHook

WebHook Přijímače jsou inicializovány jejich registrací, obvykle ve statické třídě *WebApiConfig,* například:

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
