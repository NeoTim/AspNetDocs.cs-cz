---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: Zkoumání podrobností a metod Delete | Dokumentace Microsoftu
author: Rick-Anderson
description: 'Poznámka: Najít aktualizovanou verzi tohoto kurzu je k dispozici tady, která používá ASP.NET MVC 5 a Visual Studio 2013. Je bezpečnější, sledovat a ukázka mnohem jednodušší...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 0359af8d5558bdaa6a73be9774fec2284ab87c73
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384763"
---
# <a name="examining-the-details-and-delete-methods"></a>Zkoumání metod Details a Delete

Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > Je k dispozici aktualizovaná verze tohoto kurzu [tady](../../getting-started/introduction/getting-started.md) , která používá ASP.NET MVC 5 a Visual Studio 2013. Je bezpečnější, postupujte podle mnohem jednodušší a ukazuje další funkce.


V této části kurzu se podíváme souvislosti automaticky generované `Details` a `Delete` metody.

## <a name="examining-the-details-and-delete-methods"></a>Zkoumání metod Details a Delete

Otevřít `Movie` kontroleru a prozkoumejte `Details` metoda.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

Modul generování uživatelského rozhraní MVC, který vytvořili této metodě akce přidá komentář zobrazující požadavku HTTP, který vyvolá metodu. V tomto případě je `GET` požadavek s tři segmenty adres URL, `Movies` řadič, `Details` metoda a `ID` hodnotu.

Kód nejprve umožňuje snadno vyhledat data s využitím `Find` metody. Důležitou funkci zabezpečení integrované do metody je, že kód ověří, zda `Find` metoda našla filmu předtím, než kód se pokusí provádět s ním. Například se hacker by mohla zanést chyby do lokality tak, že změníte adresu URL vytvořené odkazy z `http://localhost:xxxx/Movies/Details/1` na něco jako `http://localhost:xxxx/Movies/Details/12345` (nebo jinou hodnotu, která nepředstavuje skutečný film). Pokud jste nekontrolovaly null film, výsledkem by bylo null filmu chybě databáze.

Zkontrolujte `Delete` a `DeleteConfirmed` metody.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

Všimněte si, že `HTTP Get``Delete` metody nedojde k odstranění zadaného film, vracel zobrazení videa, kde můžete odeslat (`HttpPost`) odstranění... Operace delete v reakci na příkaz GET požádat o (nebo k tomuto účelu, provádění operace úpravy, vytváření operace nebo jiné operace, která se mění data) otevře bezpečnostní riziko. Další informace o tom, najdete v blogu Stephen Walther [46 Tip # aplikace ASP.NET MVC – nepoužívejte odstranit odkazy, protože uživatel vytvořit bezpečnostní díry](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

`HttpPost` Pojmenovanou metodu, která odstraní data `DeleteConfirmed` poskytnout metodu HTTP POST jedinečný podpis nebo název. Níže jsou zobrazena podpisy dvou metod:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

Modul CLR (CLR) vyžaduje přetížené metody mají jedinečný podpis (stejný název metody, ale jiný seznam parametrů). Tady však dvou metod Delete – jeden u metody GET - a jeden pro metodu POST, že mají stejný podpis parametru. (I potřebují tak, aby přijímal celá čísla jako parametr.)

Řazení, to zjistit, můžete provést několik věcí. Jeden je poskytnout metody různými názvy. Je to, co mechanismu generování uživatelského rozhraní nebyl v předchozím příkladu. Ale zavádí malé problému: ASP.NET mapuje segmentů adresy URL na metody akce podle názvu, a Pokud přejmenujete metodu, obvykle směrování nebude moci najít tuto metodu. Řešení se zobrazí v příkladu, který je přidat `ActionName("Delete")` atribut `DeleteConfirmed` metoda. Efektivně provede mapování pro směrování systém tak, aby adresa URL, která zahrnuje <em>/Delete/</em>příspěvek požadavku najdete `DeleteConfirmed` metody.

Dalším běžným způsobem vyhnout potížím s metodami, které mají stejné názvy a podpisy se uměle změna podpisu metody POST, která zahrnují Nepoužitý parametr. Někteří vývojáři přidat například typ parametru `FormCollection` , který je předán metodě příspěvku a poté jednoduše nepoužívejte parametr:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>Souhrn

Teď máte dokončené aplikace ASP.NET MVC, která ukládá data v databázi místní databáze. Můžete vytvořit, číst, aktualizovat, odstranit a hledat videa.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>Další kroky

Dalším krokem po vytvořené a testování webové aplikace je zpřístupnit ostatním uživatelům přes Internet. K tomuto účelu, budete muset nasadit na web poskytovatele hostitelských služeb. Společnost Microsoft nabízí bezplatné webových hostitelských služeb pro až 10 webových serverů ve [Bezplatný zkušební účet Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Můžu navrhnout další využijte tento kurz [Nasaďte aplikaci zabezpečení rozhraní ASP.NET MVC s nástroji Membership, OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Vynikající kurz je středně Petr Dykstra [vytváření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). [Stackoverflow](http://stackoverflow.com/help) a [fóra ASP.NET MVC](https://forums.asp.net/1146.aspx) jsou skvělý umístí klást otázky. Postupujte podle [mě](https://twitter.com/RickAndMSFT) na twitteru, můžete získat aktualizace na můj poslední kurzy.

Zpětná vazba je Vítejte.

– [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
– [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [Předchozí](adding-validation-to-the-model.md)
