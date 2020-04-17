---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Principy filtrů akcí (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akce je atribut, který můžete použít na akci kontroleru nebo na celý řadič...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542180"
---
# <a name="understanding-action-filters-c"></a>Principy filtrů akcí (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akce je atribut, který můžete použít pro akci kontroleru nebo celý řadič , který upravuje způsob, jakým je akce provedena.

## <a name="understanding-action-filters"></a>Principy filtrů akcí

Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akce je atribut, který můžete použít pro akci kontroleru nebo celý řadič , který upravuje způsob, jakým je akce provedena. Rozhraní ASP.NET MVC obsahuje několik akčních filtrů:

- OutputCache – Tento filtr akce ukládá výstup akce řadiče po určitou dobu.
- HandleError – Tento filtr akce zpracovává chyby vyvolané při spuštění akce kontroleru.
- Autorizace – Tento filtr akce umožňuje omezit přístup k určitému uživateli nebo roli.

Můžete také vytvořit vlastní filtry akcí. Můžete například vytvořit vlastní filtr akcí, abyste mohli implementovat vlastní ověřovací systém. Nebo můžete chtít vytvořit filtr akce, který upravuje data zobrazení vrácená akcí kontroleru.

V tomto kurzu se dozvíte, jak vytvořit filtr akce od základu. Vytvoříme filtr akce protokolu, který zaznamenává různé fáze zpracování akce do okna Visual Studio Output.

### <a name="using-an-action-filter"></a>Použití filtru akcí

Filtr akce je atribut. Většinu filtrů akcí můžete použít na jednotlivou akci kontroleru nebo na celý ovladač.

Například správce dat v výpisu 1 `Index()` zpřístupňuje akci s názvem, která vrací aktuální čas. Tato akce je `OutputCache` zdobena filtrem akce. Tento filtr způsobí, že hodnota vrácená akcí bude uložena do mezipaměti po dobu 10 sekund.

**Výpis 1 –`Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

Pokud akci opakovaně `Index()` vyvoláte zadáním adresy URL /Data/Index do adresního řádku prohlížeče a opakovaným stisknutím tlačítka Aktualizovat, zobrazí se stejný čas po dobu 10 sekund. Výstup akce `Index()` je uložen do mezipaměti po dobu 10 sekund (viz obrázek 1).

[![Čas uložený v mezipaměti](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**Obrázek 01**: Čas uložený v mezipaměti[(Kliknutím zobrazíte obrázek v plné velikosti)](understanding-action-filters-cs/_static/image3.png)

V seznamu 1 se na `OutputCache` `Index()` metodu použije jeden filtr akce – filtr akce. Pokud potřebujete, můžete použít více filtrů akcí na stejnou akci. Můžete například použít filtry `OutputCache` i `HandleError` filtry akcí pro stejnou akci.

V seznamu 1 `OutputCache` se na `Index()` akci použije filtr akce. Tento atribut můžete také `DataController` použít pro samotnou třídu. V takovém případě výsledek vrácený jakoukoli akcí vystavenou řadičem by byl uložen do mezipaměti po dobu 10 sekund.

### <a name="the-different-types-of-filters"></a>Různé typy filtrů

ASP.NET MVC framework podporuje čtyři různé typy filtrů:

1. Filtry autorizace `IAuthorizationFilter` – Implementuje atribut.
2. Akce filtry – `IActionFilter` Implementuje atribut.
3. Filtry výsledků – `IResultFilter` Implementuje atribut.
4. Filtry výjimek `IExceptionFilter` – Implementuje atribut.

Filtry jsou prováděny v pořadí uvedeném výše. Například filtry autorizace jsou vždy provedeny před filtry akcí a filtry výjimek jsou vždy provedeny po každém jiném typu filtru.

Filtry autorizace se používají k implementaci ověřování a autorizace akcí řadiče. Například filtr Autorizovat je příkladem filtru Autorizace.

Filtry akcí obsahují logiku, která je spuštěna před a po provedení akce kontroleru. Filtr akce můžete použít například k úpravě dat zobrazení, která vrátí akce kontroleru.

Filtry výsledků obsahují logiku, která je spuštěna před a po spuštění výsledku zobrazení. Můžete například chtít upravit výsledek zobrazení těsně před vykreslením zobrazení do prohlížeče.

Filtry výjimek jsou posledním typem filtru, který má být spuštěn. Filtr výjimek můžete použít ke zpracování chyb vydchlých vydazeným akcemi ovladače nebo výsledky akce kontroleru. Můžete také použít filtry výjimek k protokolování chyb.

Každý jiný typ filtru je proveden v určitém pořadí. Pokud chcete řídit pořadí, ve kterém jsou filtry stejného typu provedeny, můžete nastavit vlastnost objednávky filtru.

Základní třída pro všechny filtry `System.Web.Mvc.FilterAttribute` akcí je třída. Pokud chcete implementovat určitý typ filtru, musíte vytvořit třídu, která dědí ze základní třídy `IAuthorizationFilter`Filter `IActionFilter` `IResultFilter`a `IExceptionFilter` implementuje jedno nebo více rozhraní , , nebo rozhraní.

### <a name="the-base-actionfilterattribute-class"></a>Základní třída ActionFilterAttribute

Aby bylo možné usnadnit implementaci filtru vlastní akce, ASP.NET mvc `ActionFilterAttribute` rámec obsahuje základní třídy. Tato třída `IActionFilter` implementuje `IResultFilter` rozhraní a rozhraní `Filter` a dědí z třídy.

Terminologie zde není zcela konzistentní. Technicky je třída, která dědí z třídy ActionFilterAttribute, filtr akce i filtr výsledků. Ve volném smyslu se však filtr akce slova používá k odkazování na jakýkoli typ filtru v rámci ASP.NET MVC.

Základní `ActionFilterAttribute` třída má následující metody, které můžete přepsat:

- OnActionExecuting – Tato metoda je volána před provedením akce kontroleru.
- OnActionExecuted – Tato metoda je volána po provedení akce kontroleru.
- OnResultExecuting – Tato metoda je volána před spuštěním akce kontroleru.
- OnResultExecuted – Tato metoda je volána po provedení akce kontroléru.

V další části uvidíme, jak můžete implementovat každou z těchto různých metod.

### <a name="creating-a-log-action-filter"></a>Vytvoření filtru akce protokolu

Aby chomáč, jak můžete vytvořit vlastní akce filtr, vytvoříme vlastní akce filtr, který zaznamenává fáze zpracování akce kontroleru do okna Visual Studio Výstup. Naše `LogActionFilter` je obsažena v seznamu 2.

**Výpis 2 –`ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

`OnActionExecuting()`V výpisu 2, `OnResultExecuting()`, `OnResultExecuted()` `OnActionExecuted()`, a `Log()` metody všechny volání metody. Název metody a aktuální data trasy je `Log()` předán metodě. Metoda `Log()` zapíše zprávu do okna Visual Studio Output (viz obrázek 2).

[![Zápis do okna Výstup sady Visual Studio](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**Obrázek 02**: Zápis do okna Výstup sady Visual Studio[(Klepnutím zobrazíte obrázek v plné velikosti)](understanding-action-filters-cs/_static/image6.png)

Domácí kontroler v seznamu 3 ukazuje, jak můžete použít filtr akce protokolu na celou třídu kontroleru. Vždy, když některé akce vystavené řadič home `Index()` jsou vyvolány – metoda nebo `About()` metoda – fáze zpracování akce jsou zaznamenány do okna Visual Studio Výstup.

**Výpis 3 –`Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>Souhrn

V tomto kurzu jste byli představeni ASP.NET filtry akcí MVC. Dozvěděli jste se o čtyřech různých typech filtrů: filtrech autorizace, filtrech akcí, filtrech výsledků a filtrech výjimek. Také jste se `ActionFilterAttribute` dozvěděli o základní třídě.

Nakonec jste se naučili, jak implementovat jednoduchý filtr akce. Vytvořili jsme filtr akce protokolu, který zaznamenává fáze zpracování akce kontroleru do okna Visual Studio Output.

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-routing-overview-cs.md)
> [další](improving-performance-with-output-caching-cs.md)
