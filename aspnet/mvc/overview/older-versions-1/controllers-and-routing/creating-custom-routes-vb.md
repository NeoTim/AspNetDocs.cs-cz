---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Vytváření vlastních tras (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542739"
---
# <a name="creating-custom-routes-vb"></a>Vytváření vlastních tras (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak přidat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se dozvíte, jak upravit výchozí tabulku tras v souboru Global.asax.

V tomto kurzu se dozvíte, jak přidat vlastní trasu do ASP.NET aplikace MVC. Dozvíte se, jak upravit výchozí směrovací tabulku v souboru Global.asax s vlastní trasou.

V ASP.NET aplikací MVC bude výchozí směrovací tabulka fungovat dobře. Můžete však zjistit, že máte specializované potřeby směrování. V takovém případě můžete vytvořit vlastní trasu.

Představte si například, že vytváříte blogovou aplikaci. Můžete chtít zpracovat příchozí požadavky, které vypadají takto:

/Archiv/12-25-2009

Když uživatel zadá tento požadavek, chcete vrátit položku blogu, která odpovídá datu 12/25/2009. Chcete-li zpracovat tento typ požadavku, musíte vytvořit vlastní trasu.

Soubor Global.asax v seznamu 1 obsahuje novou vlastní trasu s názvem Blog, která zpracovává požadavky, které vypadají jako /Archive/*datum zadání*.

**Výpis 1 - Global.asax (s vlastní trasou)**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

Pořadí tras, které přidáte do tabulky tras, je důležité. Naše nová vlastní trasa blogu je přidána před existující výchozí trasu. Pokud jste stornovat pořadí, pak výchozí trasa vždy dostane volána namísto vlastní trasy.

Vlastní blog směrování odpovídá všechny požadavky, které začínají /Archive/. Takže odpovídá všem následujícím adresám URL:

- /Archiv/12-25-2009

- /Archiv/10-6-2004

- /Archiv/jablko

Vlastní trasa mapuje příchozí požadavek na řadič s názvem Archive a vyvolá akci Entry(). Při volání Entry() metoda je volána, datum zadání je předán jako parametr s názvem entryDate.

Vlastní trasu blogu můžete použít s ovladačem v seznamu 2.

**Výpis 2 - ArchiveController.vb**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

Všimněte si, že Entry() metoda v Výpis 2 přijímá parametr typu DateTime. Rozhraní MVC je dostatečně inteligentní, aby automaticky převádí datum zadání z adresy URL na hodnotu DateTime. Pokud parametr data zadání z adresy URL nelze převést na DateTime, je vyvolána chyba (viz obrázek 1).

**Obrázek 1 – Chyba z převodu parametru**

[![Dialogové okno New Project (Nový projekt)](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**Obrázek 01**: Chyba při převodu parametru[(Kliknutím zobrazíte obrázek v plné velikosti)](creating-custom-routes-vb/_static/image2.png)

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo ukázat, jak můžete vytvořit vlastní trasu. Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global.asax, který představuje položky blogu. Diskutovali jsme o tom, jak mapovat požadavky na položky blogu na řadič s názvem ArchiveController a akce řadiče s názvem Entry().

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-controller-overview-vb.md)
> [další](creating-a-route-constraint-vb.md)
