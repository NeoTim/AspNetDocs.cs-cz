---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Vytváření vlastních tras (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542752"
---
# <a name="creating-custom-routes-c"></a>Vytváření vlastních tras (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.

V tomto kurzu se dozvíte, jak přidat vlastní trasu do ASP.NET aplikace MVC. Dozvíte se, jak upravit výchozí směrovací tabulku v souboru Global.asax s vlastní trasou.

Pro mnoho jednoduchých ASP.NET aplikací mvc jednoduché, bude výchozí směrovací tabulka fungovat v pohodě. Můžete však zjistit, že máte specializované potřeby směrování. V takovém případě můžete vytvořit vlastní trasu.

Představte si například, že vytváříte blogovou aplikaci. Můžete chtít zpracovat příchozí požadavky, které vypadají takto:

/Archiv/12-25-2009

Když uživatel zadá tento požadavek, chcete vrátit položku blogu, která odpovídá datu 12/25/2009. Chcete-li zpracovat tento typ požadavku, musíte vytvořit vlastní trasu.

Soubor Global.asax v seznamu 1 obsahuje novou vlastní trasu s názvem Blog, která zpracovává požadavky, které vypadají jako /Archive/*datum zadání*.

**Výpis 1 - Global.asax (s vlastní trasou)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

Pořadí tras, které přidáte do tabulky tras, je důležité. Naše nová vlastní trasa blogu je přidána před existující výchozí trasu. Pokud jste stornovat pořadí, pak výchozí trasa vždy dostane volána namísto vlastní trasy.

Vlastní blog směrování odpovídá všechny požadavky, které začínají /Archive/. Takže odpovídá všem následujícím adresám URL:

- /Archiv/12-25-2009

- /Archiv/10-6-2004

- /Archiv/jablko

Vlastní trasa mapuje příchozí požadavek na řadič s názvem Archive a vyvolá akci Entry(). Při volání Entry() metoda je volána, datum zadání je předán jako parametr s názvem entryDate.

Vlastní trasu blogu můžete použít s ovladačem v seznamu 2.

**Výpis 2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

Všimněte si, že Entry() metoda v Výpis 2 přijímá parametr typu DateTime. Rozhraní MVC je dostatečně inteligentní, aby automaticky převádí datum zadání z adresy URL na hodnotu DateTime. Pokud parametr data zadání z adresy URL nelze převést na DateTime, je vyvolána chyba (viz obrázek 1).

**Obrázek 1 – Chyba z převodu parametru**

[![Dialogové okno New Project (Nový projekt)](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**Obrázek 01**: Chyba při převodu parametru[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-custom-routes-cs/_static/image2.png)

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo ukázat, jak můžete vytvořit vlastní trasu. Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global.asax, který představuje položky blogu. Diskutovali jsme o tom, jak mapovat požadavky na položky blogu na řadič s názvem ArchiveController a akce řadiče s názvem Entry().

> [!div class="step-by-step"]
> [Předchozí](aspnet-mvc-controllers-overview-cs.md)
> [další](creating-a-route-constraint-cs.md)
