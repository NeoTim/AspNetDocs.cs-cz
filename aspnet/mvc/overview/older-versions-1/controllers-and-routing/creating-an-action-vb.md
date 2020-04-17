---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Vytvoření akce (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak přidat novou akci do ASP.NET řadiče MVC. Přečtěte si o požadavcích na metodu, která má být akcí.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542245"
---
# <a name="creating-an-action-vb"></a>Vytvoření akce (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak přidat novou akci do ASP.NET řadiče MVC. Přečtěte si o požadavcích na metodu, která má být akcí.

Cílem tohoto kurzu je vysvětlit, jak můžete vytvořit novou akci řadiče. Dozvíte se o požadavcích metody akce. Také se dozvíte, jak zabránit tomu, aby byla metoda vystavena jako akce.

## <a name="adding-an-action-to-a-controller"></a>Přidání akce do řadiče

Přidáním nové metody do řadiče přidáte novou akci do kontroleru. Například kontroler v výpisu 1 obsahuje akci s názvem Index() a akce s názvem SayHello(). Obě metody jsou vystaveny jako akce.

**Výpis 1 - Řadiče\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

Aby byla metoda vystavena vesmíru jako akce, musí splňovat určité požadavky:

- Metoda musí být veřejná.
- Metoda nemůže být statickou metodou.
- Metoda nemůže být metoda rozšíření.
- Metoda nemůže být konstruktor, getter nebo setter.
- Metoda nemůže mít otevřené obecné typy.
- Metoda není metodou základní třídy řadiče.
- Metoda nemůže obsahovat parametry **ref** nebo **out.**

Všimněte si, že neexistují žádná omezení na návratový typ akce kontroleru. Akce kontroleru může vrátit řetězec, DateTime, instanci random třídy nebo void. Rozhraní ASP.NET MVC převede libovolný návratový typ, který není výsledkem akce, na řetězec a vykreslí řetězec do prohlížeče.

Přidáte-li libovolnou metodu, která neporušuje tyto požadavky do řadiče, metoda je vystavena jako akce řadiče. Buď opatrná. Akci kontroleru může vyvolat kdokoli připojený k Internetu. Nevytvářejte například akci řadiče DeleteMyWebsite().

## <a name="preventing-a-public-method-from-being-invoked"></a>Zabránění vyvolání veřejné metody

Pokud potřebujete vytvořit veřejnou metodu ve třídě kontroleru a nechcete vystavit metodu jako akci kontroleru, můžete &lt;zabránit&gt; vyvolání metody pomocí atributu NonAction. Například kontroler v listing 2 obsahuje veřejnou metodu s &lt;názvem&gt; CompanySecrets(), která je zdobena atributem NonAction.

**Výpis 2 - Řadiče\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Pokud se pokusíte vyvolat CompanySecrets() akce řadiče zadáním /Work/CompanySecrets do adresního řádku prohlížeče pak se zobrazí chybová zpráva na obrázku 1.

[![Vyvolání metody NonAction](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Obrázek 01**: Vyvolání metody NonAction([Klepnutím zobrazíte obrázek v plné velikosti)](creating-an-action-vb/_static/image2.png)

> [!div class="step-by-step"]
> [Předchozí](creating-a-controller-vb.md)
> [další](aspnet-mvc-controllers-overview-cs.md)
