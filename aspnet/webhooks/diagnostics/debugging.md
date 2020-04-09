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
# <a name="aspnet-webhooks-debugging"></a>ladění ASP.NET WebHooks

## <a name="debugging-in-azure"></a>Ladění v Azure

Chcete-li ladit webovou aplikaci při spuštění v Azure, přečtěte si kurz [Poradce při potížích s webovou aplikací ve službě Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Ladění se zdrojem a symboly

Kromě ladění vlastního kódu je možné ladit přímo do microsoft ASP.NET WebHooks a ve skutečnosti všechny .NET. To funguje bez ohledu na to, zda ladění místně nebo vzdáleně. Nejprve nakonfigurujte Visual Studio najít zdroj a symboly podle ladění **a** potom **možnosti a nastavení**. Nastavte volby takto:

![Možnosti a nastavení](_static/SourceSymbols.png)

Pak přidejte odkaz na [symbolsource.org](http://symbolsource.org) pro stažení zdroje a symbolů. Přejděte na kartu **Symboly** ve výše uvedené nabídce a jako umístění symbolu přidejte následující:

```
http://srv.symbolsource.org/pdb/Public
```

Kromě toho se ujistěte, že adresář mezipaměti má krátký název; v opačném případě mohou být názvy souborů příliš dlouhé, což způsobí, že se symboly nenačtou. Ukázková cesta je:

```
C:\SymCache
```

Nastavení by mělo vypadat podobně jako toto:

![Příklad umístění souboru symbolu voleb](_static/SymSource.png)
