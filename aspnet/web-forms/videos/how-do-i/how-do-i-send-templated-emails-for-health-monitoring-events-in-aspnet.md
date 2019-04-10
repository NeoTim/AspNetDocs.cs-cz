---
uid: web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
title: '[Postup:] Odeslání e-mailů bez vizuálního vzhledu pro událostech monitorování stavu v ASP.NET | Dokumentace Microsoftu'
author: rick-anderson
description: Chris pixelů na toto video ukazuje způsob použití TemplatedEmailWebEventProvider k odesílání e-mailů, když dojde k události monitorování stavu, které využívají šablonu pro t...
ms.author: riande
ms.date: 09/18/2008
ms.assetid: 5c107c6e-9fb7-4206-bd3f-221cb0767f8a
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
msc.type: video
ms.openlocfilehash: e7b929c6e186e59b43180e8f26cf0f8b4608328f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59417985"
---
# <a name="how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet"></a><span data-ttu-id="036d0-103">[Postup:] Odeslání e-mailů bez vizuálního vzhledu pro událostech monitorování stavu v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="036d0-103">[How Do I:] Send Templated Emails for Health Monitoring Events in ASP.NET</span></span>

<span data-ttu-id="036d0-104">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="036d0-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="036d0-105">Chris pixelů na toto video ukazuje způsob použití TemplatedEmailWebEventProvider k odesílání e-mailů, když dojde k události monitorování stavu, které využívají šablonu pro obsah e-mailu.</span><span class="sxs-lookup"><span data-stu-id="036d0-105">In this video Chris Pels shows how to use the TemplatedEmailWebEventProvider to send emails when health monitoring events occur that utilize a template for the email content.</span></span> <span data-ttu-id="036d0-106">Nejdříve si projděte postup konfigurace &lt;poskytovatele&gt; a &lt;pravidla&gt; elementy v souboru web.config implementovat pomocí e-mailu bez vizuálního vzhledu a přidružení stavu monitorování událostí s poskytovateli e-mailu bez vizuálního vzhledu.</span><span class="sxs-lookup"><span data-stu-id="036d0-106">First, see how to configure the &lt;provider&gt; and &lt;rules&gt; elements in the web.config file to implement the use of templated email and associate a health monitoring event with the templated email provider.</span></span> <span data-ttu-id="036d0-107">Po nakonfigurování poskytovateli bez vizuálního vzhledu najdete v části Vytvoření šablony e-mailu pomocí jako standardní stránky ASPX.</span><span class="sxs-lookup"><span data-stu-id="036d0-107">Once the templated provider is configured see how to create the email template using as standard .aspx page.</span></span> <span data-ttu-id="036d0-108">Zjistěte, jaké informace jsou k dispozici ve třídě MailEventNotificaitonInfo, který je předán podle TemplatedEmailWebEventProvider do stránky ASPX šablony.</span><span class="sxs-lookup"><span data-stu-id="036d0-108">Learn what information is available in the MailEventNotificaitonInfo class that is passed by the TemplatedEmailWebEventProvider to the template .aspx page.</span></span> <span data-ttu-id="036d0-109">Podívejte se, jak je možné zahrnout libovolné informace je vhodné pro obsah e-mailu.</span><span class="sxs-lookup"><span data-stu-id="036d0-109">See how it can be used to include whatever information is appropriate in the email content.</span></span> <span data-ttu-id="036d0-110">Nakonec zobrazte test webu, který odešle e-mailů v reakci na událostech monitorování stavu.</span><span class="sxs-lookup"><span data-stu-id="036d0-110">Finally, view the test web site which sends emails in response to health monitoring events.</span></span> <span data-ttu-id="036d0-111">Zobrazte skutečné e-mailech přijatých, které obsahují informace o události na základě šablony monitorování stavu.</span><span class="sxs-lookup"><span data-stu-id="036d0-111">Then view the actual emails received that contain the health monitoring event information based upon the template.</span></span>

[<span data-ttu-id="036d0-112">&#9654;Podívejte se na video (25 minut)</span><span class="sxs-lookup"><span data-stu-id="036d0-112">&#9654; Watch video (25 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet)
