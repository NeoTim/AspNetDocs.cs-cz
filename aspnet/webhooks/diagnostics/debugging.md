---
uid: webhooks/diagnostics/debugging
title: ladění ASP.NET WebHooks | Dokumenty společnosti Microsoft
author: rick-anderson
description: Jak ladit ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675372"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="53656-103">ladění ASP.NET WebHooks</span><span class="sxs-lookup"><span data-stu-id="53656-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="53656-104">Ladění v Azure</span><span class="sxs-lookup"><span data-stu-id="53656-104">Debugging in Azure</span></span>

<span data-ttu-id="53656-105">Chcete-li ladit webovou aplikaci při spuštění v Azure, přečtěte si kurz [Poradce při potížích s webovou aplikací ve službě Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="53656-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="53656-106">Ladění se zdrojem a symboly</span><span class="sxs-lookup"><span data-stu-id="53656-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="53656-107">Kromě ladění vlastního kódu je možné ladit přímo do microsoft ASP.NET WebHooks a ve skutečnosti všechny .NET.</span><span class="sxs-lookup"><span data-stu-id="53656-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="53656-108">To funguje bez ohledu na to, zda ladění místně nebo vzdáleně.</span><span class="sxs-lookup"><span data-stu-id="53656-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="53656-109">Nejprve nakonfigurujte Visual Studio najít zdroj a symboly podle ladění **a** potom **možnosti a nastavení**.</span><span class="sxs-lookup"><span data-stu-id="53656-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="53656-110">Nastavte volby takto:</span><span class="sxs-lookup"><span data-stu-id="53656-110">Set the options like this:</span></span>

![Možnosti a nastavení](_static/SourceSymbols.png)

<span data-ttu-id="53656-112">Pak přidejte odkaz na [symbolsource.org](http://symbolsource.org) pro stažení zdroje a symbolů.</span><span class="sxs-lookup"><span data-stu-id="53656-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="53656-113">Přejděte na kartu **Symboly** ve výše uvedené nabídce a jako umístění symbolu přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="53656-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="53656-114">Kromě toho se ujistěte, že adresář mezipaměti má krátký název; v opačném případě mohou být názvy souborů příliš dlouhé, což způsobí, že se symboly nenačtou.</span><span class="sxs-lookup"><span data-stu-id="53656-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="53656-115">Ukázková cesta je:</span><span class="sxs-lookup"><span data-stu-id="53656-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="53656-116">Nastavení by mělo vypadat podobně jako toto:</span><span class="sxs-lookup"><span data-stu-id="53656-116">The settings should look similar to this:</span></span>

![Příklad umístění souboru symbolu voleb](_static/SymSource.png)
