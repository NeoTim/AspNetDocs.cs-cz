---
uid: webhooks/index
title: ASP.NET WebHooks Přehled | Dokumenty společnosti Microsoft
author: rick-anderson
description: Úvod do ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675433"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="c1189-103">přehled ASP.NET WebHooks</span><span class="sxs-lookup"><span data-stu-id="c1189-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="c1189-104">WebHooks je lehký http vzor poskytující jednoduchý pub/sub model pro zapojení spolu webová api a saas služby.</span><span class="sxs-lookup"><span data-stu-id="c1189-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="c1189-105">Pokud dojde k události ve službě, je odesláno oznámení ve formě požadavku HTTP POST registrovaným odběratelům.</span><span class="sxs-lookup"><span data-stu-id="c1189-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="c1189-106">Požadavek POST obsahuje informace o události, která umožňuje příjemci jednat odpovídajícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="c1189-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="c1189-107">Vzhledem k jejich jednoduchosti, WebHooks jsou již vystaveny velké množství služeb, včetně [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), a mnoho dalších.</span><span class="sxs-lookup"><span data-stu-id="c1189-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="c1189-108">WebHook může například znamenat, že se v [Dropboxu](http://dropbox.com/)změnil soubor nebo že byla v GitHubu spáchána změna kódu, nebo byla v [PayPalu](http://www.paypal.com/)zahájena platba nebo byla vytvořena karta v [Trello](http://www.trello.com/).</span><span class="sxs-lookup"><span data-stu-id="c1189-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="c1189-109">Možnosti jsou nekonečné!</span><span class="sxs-lookup"><span data-stu-id="c1189-109">The possibilities are endless!</span></span>

<span data-ttu-id="c1189-110">Microsoft ASP.NET WebHooks usnadňuje odesílání i přijímání WebHooks jako součást vaší ASP.NET aplikace:</span><span class="sxs-lookup"><span data-stu-id="c1189-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="c1189-111">Na straně příjmu poskytuje společný model pro příjem a zpracování WebHooks z libovolného počtu zprostředkovatelů WebHook.</span><span class="sxs-lookup"><span data-stu-id="c1189-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="c1189-112">Přichází z krabice s podporou [Dropbox](http://dropbox.com/), [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) a [Zendesk,](https://www.zendesk.com/) ale je snadné přidat podporu pro další.</span><span class="sxs-lookup"><span data-stu-id="c1189-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="c1189-113">Na straně odesílání poskytuje podporu pro správu a ukládání odběrů, stejně jako pro odesílání oznámení událostí na správnou sadu odběratelů.</span><span class="sxs-lookup"><span data-stu-id="c1189-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="c1189-114">To vám umožní definovat vlastní sadu událostí, ke kterým se mohou odběratelé přihlásit, a upozornit je, když se něco stane.</span><span class="sxs-lookup"><span data-stu-id="c1189-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="c1189-115">Obě části lze použít společně nebo odděleně v závislosti na vašem scénáři.</span><span class="sxs-lookup"><span data-stu-id="c1189-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="c1189-116">Pokud potřebujete pouze přijímat WebHooks z jiných služeb, pak můžete použít pouze část přijímače; Pokud chcete pouze vystavit WebHooks pro ostatní konzumovat, pak můžete udělat právě to.</span><span class="sxs-lookup"><span data-stu-id="c1189-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="c1189-117">Kód cílí ASP.NET web API 2 a ASP.NET MVC 5 a je k dispozici jako [OSS na GitHubu](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="c1189-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="c1189-118">WebHooks – přehled</span><span class="sxs-lookup"><span data-stu-id="c1189-118">WebHooks Overview</span></span>

<span data-ttu-id="c1189-119">WebHooks je vzor, což znamená, že se liší, jak se používá od služby ke službě, ale základní myšlenka je stejná.</span><span class="sxs-lookup"><span data-stu-id="c1189-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="c1189-120">WebHooks si můžete myslet jako jednoduchý model pub/sub, kde se uživatel může přihlásit k odběru událostí, které se dějí jinde.</span><span class="sxs-lookup"><span data-stu-id="c1189-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="c1189-121">Oznámení událostí jsou šířeny jako požadavky HTTP POST obsahující informace o samotné události.</span><span class="sxs-lookup"><span data-stu-id="c1189-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="c1189-122">Požadavek HTTP POST obvykle obsahuje data jazyka JSON nebo formuláře HTML určená odesílatelem WebHooku, včetně informací o události, která způsobuje aktivaci webhooku.</span><span class="sxs-lookup"><span data-stu-id="c1189-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="c1189-123">Například tělo požadavku WebHook POST z [GitHubu](https://www.github.com/) vypadá takto v důsledku otevření nového problému v určitém úložišti:</span><span class="sxs-lookup"><span data-stu-id="c1189-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="c1189-124">Chcete-li zajistit, že WebHook je skutečně od zamýšleného odesílatele, požadavek POST je zabezpečen nějakým způsobem a poté ověřen příjemcem.</span><span class="sxs-lookup"><span data-stu-id="c1189-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="c1189-125">Například [GitHub WebHooks](https://developer.github.com/webhooks/) obsahuje hlavičku HTTP s podpisem *X-Hub* s hodnotou hash těla požadavku, která je kontrolována implementací příjemce, takže se o to nemusíte starat.</span><span class="sxs-lookup"><span data-stu-id="c1189-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="c1189-126">Tok WebHook obecně jde něco takového:</span><span class="sxs-lookup"><span data-stu-id="c1189-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="c1189-127">Odesílatel WebHook zveřejňuje události, které klient může přihlásit k odběru.</span><span class="sxs-lookup"><span data-stu-id="c1189-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="c1189-128">Události popisují pozorovatelné změny v systému, například, že byla vložena nová datová položka, že byl dokončen proces nebo něco jiného.</span><span class="sxs-lookup"><span data-stu-id="c1189-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="c1189-129">WebHook přijímač přihlásí registrací WebHook skládající se ze čtyř věcí:</span><span class="sxs-lookup"><span data-stu-id="c1189-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="c1189-130">Identifikátor URI, pro kde by mělo být oznámení o události zaúčtováno ve formě požadavku HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="c1189-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="c1189-131">Sada filtrů popisující konkrétní události, pro které by měl být aktivován WebHook;</span><span class="sxs-lookup"><span data-stu-id="c1189-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="c1189-132">Tajný klíč, který se používá k podepsání požadavku HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="c1189-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="c1189-133">Další data, která mají být zahrnuta do požadavku HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c1189-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="c1189-134">Může se například jedná například o další pole záhlaví PROTOKOLU HTTP nebo vlastnosti zahrnuté v textu požadavku HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c1189-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="c1189-135">Jakmile dojde k události, jsou nalezeny odpovídající Registrace WebHook a http post požadavky jsou odeslány.</span><span class="sxs-lookup"><span data-stu-id="c1189-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="c1189-136">Generování požadavků HTTP POST jsou obvykle opakovány několikrát, pokud z nějakého důvodu příjemce neodpovídá nebo požadavek HTTP POST má za následek odpověď na chybu.</span><span class="sxs-lookup"><span data-stu-id="c1189-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="c1189-137">Kanál zpracování webhooků</span><span class="sxs-lookup"><span data-stu-id="c1189-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="c1189-138">Kanál zpracování Microsoft ASP.NET WebHooks pro příchozí WebHooks vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="c1189-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET kanál pro zpracování webhooků](_static/WebHookReceivers.png)

<span data-ttu-id="c1189-140">Dva klíčové pojmy zde jsou *přijímače* a *obslužné rutiny*:</span><span class="sxs-lookup"><span data-stu-id="c1189-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="c1189-141">*Příjemci* jsou zodpovědní za zpracování konkrétní příchuť WebHook od daného odesílatele a pro vynucení bezpečnostních kontrol, aby bylo zajištěno, že požadavek WebHook skutečně pochází od zamýšleného odesílatele.</span><span class="sxs-lookup"><span data-stu-id="c1189-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="c1189-142">*Obslužné rutiny* jsou obvykle tam, kde uživatelský kód běží zpracování konkrétní WebHook.</span><span class="sxs-lookup"><span data-stu-id="c1189-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="c1189-143">V následujících uzlech jsou tyto koncepty popsány podrobněji.</span><span class="sxs-lookup"><span data-stu-id="c1189-143">In the following nodes these concepts are described in more details.</span></span>
