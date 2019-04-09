---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[Postup:] Export dat do souboru s oddělovači (CSV) čárkou pro aplikace, jako je Excel | Dokumentace Microsoftu'
author: rick-anderson
description: Chris pixelů na toto video ukazuje, jak vzít data z databáze nebo jiného zdroje a exportovat je do souboru s oddělovači čárkami, který slouží li aplikace...
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: f27873eee345fe5347023b154de2b3833c9b6138
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59383028"
---
# <a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="5c825-103">[Postup:] Export dat do souboru s oddělovači (CSV) čárkou pro aplikace, jako je Excel</span><span class="sxs-lookup"><span data-stu-id="5c825-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>

<span data-ttu-id="5c825-104">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="5c825-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="5c825-105">Chris pixelů na toto video ukazuje, jak vzít data z databáze nebo jiného zdroje a exportovat je do souboru s oddělovači čárkami, který lze použít v aplikaci, jako je Excel.</span><span class="sxs-lookup"><span data-stu-id="5c825-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="5c825-106">Nejprve se vytvoří sadu dat jako objekt DataTable.</span><span class="sxs-lookup"><span data-stu-id="5c825-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="5c825-107">V dalším kroku se vymaže odpovědi pro aktuální požadavek webové stránky a záhlaví a typu obsahu jsou nakonfigurované jako soubor csv.</span><span class="sxs-lookup"><span data-stu-id="5c825-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="5c825-108">Skutečná data se pak přidá do datového proudu odpovědi první napsáním záhlaví sloupců pro soubor csv, za nímž následuje datových hodnot.</span><span class="sxs-lookup"><span data-stu-id="5c825-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="5c825-109">Tento přístup může být užitečné, pokud uživatelé potřebují o export dat, takže ji lze ovládat místně v programu, jako je Excel.</span><span class="sxs-lookup"><span data-stu-id="5c825-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="5c825-110">&#9654;Podívejte se na video (19 minuty)</span><span class="sxs-lookup"><span data-stu-id="5c825-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
