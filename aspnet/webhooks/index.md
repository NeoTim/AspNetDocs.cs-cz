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
# <a name="aspnet-webhooks-overview"></a>přehled ASP.NET WebHooks

WebHooks je lehký http vzor poskytující jednoduchý pub/sub model pro zapojení spolu webová api a saas služby. Pokud dojde k události ve službě, je odesláno oznámení ve formě požadavku HTTP POST registrovaným odběratelům. Požadavek POST obsahuje informace o události, která umožňuje příjemci jednat odpovídajícím způsobem.

Vzhledem k jejich jednoduchosti, WebHooks jsou již vystaveny velké množství služeb, včetně [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), a mnoho dalších. WebHook může například znamenat, že se v [Dropboxu](http://dropbox.com/)změnil soubor nebo že byla v GitHubu spáchána změna kódu, nebo byla v [PayPalu](http://www.paypal.com/)zahájena platba nebo byla vytvořena karta v [Trello](http://www.trello.com/). Možnosti jsou nekonečné!

Microsoft ASP.NET WebHooks usnadňuje odesílání i přijímání WebHooks jako součást vaší ASP.NET aplikace:

* Na straně příjmu poskytuje společný model pro příjem a zpracování WebHooks z libovolného počtu zprostředkovatelů WebHook. Přichází z krabice s podporou [Dropbox](http://dropbox.com/), [GitHub,](https://www.github.com/) [Bitbucket,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [PayPal,](http://www.paypal.com/) [Pusher,](http://www.pusher.com) [Salesforce,](http://www.salesforce.com) [Slack,](http://www.slack.com) [Stripe,](http://www.stripe.com) [Trello,](http://www.trello.com/)[WordPress](http://www.wordpress.com) a [Zendesk,](https://www.zendesk.com/) ale je snadné přidat podporu pro další.

* Na straně odesílání poskytuje podporu pro správu a ukládání odběrů, stejně jako pro odesílání oznámení událostí na správnou sadu odběratelů. To vám umožní definovat vlastní sadu událostí, ke kterým se mohou odběratelé přihlásit, a upozornit je, když se něco stane.

Obě části lze použít společně nebo odděleně v závislosti na vašem scénáři. Pokud potřebujete pouze přijímat WebHooks z jiných služeb, pak můžete použít pouze část přijímače; Pokud chcete pouze vystavit WebHooks pro ostatní konzumovat, pak můžete udělat právě to.

Kód cílí ASP.NET web API 2 a ASP.NET MVC 5 a je k dispozici jako [OSS na GitHubu](https://github.com/aspnet/WebHooks).

## <a name="webhooks-overview"></a>WebHooks – přehled

WebHooks je vzor, což znamená, že se liší, jak se používá od služby ke službě, ale základní myšlenka je stejná. WebHooks si můžete myslet jako jednoduchý model pub/sub, kde se uživatel může přihlásit k odběru událostí, které se dějí jinde. Oznámení událostí jsou šířeny jako požadavky HTTP POST obsahující informace o samotné události.

Požadavek HTTP POST obvykle obsahuje data jazyka JSON nebo formuláře HTML určená odesílatelem WebHooku, včetně informací o události, která způsobuje aktivaci webhooku. Například tělo požadavku WebHook POST z [GitHubu](https://www.github.com/) vypadá takto v důsledku otevření nového problému v určitém úložišti:

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

Chcete-li zajistit, že WebHook je skutečně od zamýšleného odesílatele, požadavek POST je zabezpečen nějakým způsobem a poté ověřen příjemcem. Například [GitHub WebHooks](https://developer.github.com/webhooks/) obsahuje hlavičku HTTP s podpisem *X-Hub* s hodnotou hash těla požadavku, která je kontrolována implementací příjemce, takže se o to nemusíte starat.

Tok WebHook obecně jde něco takového:

* Odesílatel WebHook zveřejňuje události, které klient může přihlásit k odběru. Události popisují pozorovatelné změny v systému, například, že byla vložena nová datová položka, že byl dokončen proces nebo něco jiného.

* WebHook přijímač přihlásí registrací WebHook skládající se ze čtyř věcí:

     1. Identifikátor URI, pro kde by mělo být oznámení o události zaúčtováno ve formě požadavku HTTP POST;

     2. Sada filtrů popisující konkrétní události, pro které by měl být aktivován WebHook;

     3. Tajný klíč, který se používá k podepsání požadavku HTTP POST;

     4. Další data, která mají být zahrnuta do požadavku HTTP POST. Může se například jedná například o další pole záhlaví PROTOKOLU HTTP nebo vlastnosti zahrnuté v textu požadavku HTTP POST.

* Jakmile dojde k události, jsou nalezeny odpovídající Registrace WebHook a http post požadavky jsou odeslány. Generování požadavků HTTP POST jsou obvykle opakovány několikrát, pokud z nějakého důvodu příjemce neodpovídá nebo požadavek HTTP POST má za následek odpověď na chybu.

## <a name="webhooks-processing-pipeline"></a>Kanál zpracování webhooků

Kanál zpracování Microsoft ASP.NET WebHooks pro příchozí WebHooks vypadá takto:

![ASP.NET kanál pro zpracování webhooků](_static/WebHookReceivers.png)

Dva klíčové pojmy zde jsou *přijímače* a *obslužné rutiny*:

* *Příjemci* jsou zodpovědní za zpracování konkrétní příchuť WebHook od daného odesílatele a pro vynucení bezpečnostních kontrol, aby bylo zajištěno, že požadavek WebHook skutečně pochází od zamýšleného odesílatele.

* *Obslužné rutiny* jsou obvykle tam, kde uživatelský kód běží zpracování konkrétní WebHook.

V následujících uzlech jsou tyto koncepty popsány podrobněji.
