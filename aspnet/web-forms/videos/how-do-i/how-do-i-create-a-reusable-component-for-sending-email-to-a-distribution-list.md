---
uid: web-forms/videos/how-do-i/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list
title: '[Postup:] Vytvoření opakovaně použitelné komponenty pro odesílání e-mailu distribučního seznamu | Dokumentace Microsoftu'
author: rick-anderson
description: V toto video pixelů na Chris ukazuje, jak vytvořit komponentu, která lze použít na více webových stránek a webových serverů, která odesílá e-maily do seznamu příjemců. Firs...
ms.author: riande
ms.date: 12/04/2008
ms.assetid: 13dd3a26-c210-432e-91fe-355c979060b3
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list
msc.type: video
ms.openlocfilehash: 6a117d0bf029245c4929e903e0c0494f6ba2b072
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400396"
---
# <a name="how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list"></a><span data-ttu-id="29955-104">[Postup:] Vytvoření opakovaně použitelné komponenty pro odesílání e-mailu lidem v distribučním seznamu</span><span class="sxs-lookup"><span data-stu-id="29955-104">[How Do I:] Create a Reusable Component for Sending Email to a Distribution List</span></span>

<span data-ttu-id="29955-105">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="29955-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="29955-106">V toto video pixelů na Chris ukazuje, jak vytvořit komponentu, která lze použít na více webových stránek a webových serverů, která odesílá e-maily do seznamu příjemců.</span><span class="sxs-lookup"><span data-stu-id="29955-106">In this video Chris Pels shows how to create a component that can be used on multiple web pages and web sites that sends emails to a list of recipients.</span></span> <span data-ttu-id="29955-107">Nejprve se nakonfigurují na webu technologie ASP.NET k odeslání e-mailům prostřednictvím &lt;mailSettings&gt; v souboru web.config.</span><span class="sxs-lookup"><span data-stu-id="29955-107">First, the ASP.NET web site will be configured to send email using the &lt;mailSettings&gt; in the web.config file.</span></span> <span data-ttu-id="29955-108">Načítá seznam příjemců, kterým se ze zdroje dat (databáze, XML atd.) a odesílá e-mailovou zprávu do každého z příjemců pomocí tříd System.Net.Mail se pak vytvoří třídu a několik metod.</span><span class="sxs-lookup"><span data-stu-id="29955-108">Then a class and several methods are created to read a list of recipients from a data source (DB, XML, etc.) and send an email message to each of the recipients using the System.Net.Mail classes.</span></span> <span data-ttu-id="29955-109">Jako součást tohoto procesu výjimka zpracování je zahrnuté.</span><span class="sxs-lookup"><span data-stu-id="29955-109">As part of this process exception handling is included.</span></span> <span data-ttu-id="29955-110">Kromě toho se vytvoří uživatelské rozhraní umožňující uživateli zadat položky jako je například adresa odesílatele, na základě práv subjektů, přidejte přílohu atd.</span><span class="sxs-lookup"><span data-stu-id="29955-110">In addition, a user interface is created to allow the user to specify items such as the From address, Subject, add an attachment, etc.</span></span>

[<span data-ttu-id="29955-111">&#9654;Podívejte se na video (35 minut)</span><span class="sxs-lookup"><span data-stu-id="29955-111">&#9654; Watch video (35 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list)
