---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Prozkoumání metod Details a DELETE | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 9c4e66454d6995bd750b62ef8b461bcfbdfb4b4f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045088"
---
# <a name="examining-the-details-and-delete-methods"></a>Zkoumání metod Details a Delete

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

V této části kurzu prohlížíte automaticky generované `Details` a `Delete` metody.

## <a name="examining-the-details-and-delete-methods"></a>Zkoumání metod Details a Delete

Otevřete `Movie` kontroler a prověřte `Details` metodu.

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

Modul generování uživatelského rozhraní MVC, který vytvořil tuto metodu Action, přidá komentář ukazující požadavek HTTP, který vyvolá metodu. V tomto případě se jedná `GET` o požadavek se třemi segmenty adresy URL, `Movies` kontrolérem, `Details` metodou a `ID` hodnotou.

Code First usnadňuje hledání dat pomocí `Find` metody. Důležitou funkcí zabezpečení, která je integrována v metodě, je, že kód ověřuje, že `Find` Metoda našla film předtím, než se kód pokusí s ním něco udělat. Hacker by například mohl do lokality způsobit chyby změnou adresy URL vytvořené odkazy z `http://localhost:xxxx/Movies/Details/1` na něco podobného `http://localhost:xxxx/Movies/Details/12345` (nebo jiné hodnoty, která nepředstavuje skutečný film). Pokud jste nezkontrolovali film s hodnotou null, výsledkem prázdného filmu je chyba databáze.

Projděte `Delete` si `DeleteConfirmed` metody a.

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

Všimněte si, že metoda HTTP GET `Delete` neodstraní zadaný film, vrátí zobrazení videa, kde můžete odeslat ( `HttpPost` ) odstranění. Provádění operace odstranění v reakci na požadavek GET (nebo pro tuto skutečnost, provádění operace Edit, operace vytvoření nebo jakékoli jiné operace, která mění data) otevře bezpečnostní riziko. Další informace najdete v tématu Stephen položky blogu Walther pro [ASP.NET #46 MVC – nepoužívejte odstranění odkazů, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

`HttpPost`Metoda, která odstraňuje data, je pojmenována `DeleteConfirmed` tak, aby metodě http post poskytovala jedinečný podpis nebo název. Níže jsou uvedené signatury dvou metod:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

Modul CLR (Common Language Runtime) vyžaduje, aby přetížené metody měly jedinečný podpis parametru (stejný název metody, ale jiný seznam parametrů). Tady ale budete potřebovat dvě metody odstranění – jednu pro GET a jednu pro POST--oba mají stejný podpis parametru. (Obě musí přijmout jedno celé číslo jako parametr.)

Pokud je chcete seřadit, můžete provést několik věcí. Jedním z nich je poskytnout metody různé názvy. To je to, co byl mechanismus generování uživatelského rozhraní použit v předchozím příkladu. To však přináší malý problém: ASP.NET mapuje segmenty adresy URL na metody akcí podle názvu a Pokud přejmenujete metodu, směrování normálně nedokáže tuto metodu najít. Řešení je to, co vidíte v příkladu, což je přidání `ActionName("Delete")` atributu do `DeleteConfirmed` metody. To efektivně provádí mapování pro systém směrování, takže adresa URL, která obsahuje */Delete/* pro požadavek post, tuto metodu najde `DeleteConfirmed` .

Dalším běžným způsobem, jak se vyhnout problému s metodami, které mají stejný název a signatury, je umělá změna signatury metody POST tak, aby zahrnovala nepoužitý parametr. Například někteří vývojáři přidávají typ parametru `FormCollection` , který je předán metodě post, a pak jednoduše nepoužijí parametr:

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>Souhrn

Teď máte úplnou aplikaci ASP.NET MVC, která ukládá data do místní databáze DB. Můžete vytvářet, číst, aktualizovat, odstraňovat a hledat filmy.

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>Další kroky

Po sestavení a otestování webové aplikace je dalším krokem zpřístupnění ostatním uživatelům, kteří budou moci používat Internet. Chcete-li to provést, je nutné jej nasadit do poskytovatele hostování webu. Microsoft nabízí bezplatné webové hostování až pro 10 webů v [bezplatném zkušebním účtu Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Doporučujeme, abyste v dalším kurzu [nasadili zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Vynikající kurz má na úrovni Dykstra [vytvořit datový Model Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). [StackOverflow](http://stackoverflow.com/help) a [fóra ASP.NET MVC](https://forums.asp.net/1146.aspx) jsou skvělými místy pro dotazování na otázky. Sledujte [mě](https://twitter.com/RickAndMSFT) na Twitteru, abyste mohli získat aktualizace na mých nejnovějších kurzech.

Váš názor je Vítejte.

– [Rick Anderson](https://blogs.msdn.com/rickAndy) Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
– [Scott Hanselman](http://www.hanselman.com/blog/) Twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [Předchozí](adding-validation.md)
