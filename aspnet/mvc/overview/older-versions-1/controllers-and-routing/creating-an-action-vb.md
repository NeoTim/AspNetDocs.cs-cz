---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Vytvoření akce (VB) | Dokumentace Microsoftu
author: microsoft
description: Zjistěte, jak přidat novou akci kontroler ASP.NET MVC. Další informace o požadavcích pro metodu na akci.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: 5f8eeeaa9bd77c0259f680198e57ade8d49cd06b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382613"
---
# <a name="creating-an-action-vb"></a>Vytvoření akce (VB)

by [Microsoft](https://github.com/microsoft)

> Zjistěte, jak přidat novou akci kontroler ASP.NET MVC. Další informace o požadavcích pro metodu na akci.


Cílem tohoto kurzu je vysvětlují, jak můžete vytvořit nové akce kontroleru. Informace o požadavky na metodu akce. Také se dozvíte, jak zabránit metodu vystaven jako akci.

## <a name="adding-an-action-to-a-controller"></a>Přidání akce Kontroleru

Přidejte novou akci k řadiči tak, že přidáte nové metody pro kontroler. Například řadič v informacích 1 obsahuje akce s názvem Index() a akce s názvem SayHello(). Obě metody jsou vystaveny jako akce.

**Výpis 1 - Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

Aby bylo možné vystavit rozhraní universe jako akci, metoda musí splňovat určité požadavky:

- Metoda musí být veřejné.
- Metoda nemůže být statickou metodu.
- Metoda nemůže být metodou rozšíření.
- Metoda nemůže být konstruktor, metoda getter nebo setter.
- Metoda nemůže mít otevřených obecných typů.
- Metoda není metodu základní třídy kontroleru.
- Metoda nemůže obsahovat **ref** nebo **si** parametry.

Všimněte si, že neexistují žádná omezení u návratového typu akce kontroleru. Akce kontroleru vrátit řetězec, DateTime, instance třídy Random nebo void. Architektura ASP.NET MVC se převést návratový typ, který není výsledek akce do řetězce a vykreslit řetězec, který se v prohlížeči.

Když přidáte jakoukoli metodu, která nebudou porušovat tyto požadavky na řadič, metoda je vystavena jako akce kontroleru. Buďte opatrní tady. Akce kontroleru můžete vyvolat každý připojený k Internetu. Ne, například vytvořit DeleteMyWebsite() akce kontroleru.

## <a name="preventing-a-public-method-from-being-invoked"></a>Brání veřejnou metodu volanou

Pokud je potřeba vytvořit veřejnou metodu do třídy kontroleru a nechcete vystavit metodu akce kontroleru, pak můžete zabránit metodu volanou pomocí &lt;NonAction&gt; atribut. Například kontroler v informacích 2 obsahuje veřejnou metodu s názvem CompanySecrets(), která je upravena pomocí &lt;NonAction&gt; atribut.

**Výpis 2 - Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Pokud při pokusu o vyvolání akce kontroleru CompanySecrets() zadáním /Work/CompanySecrets do adresního řádku prohlížeče zobrazí se zpráva chyby na obrázku 1.


[![IMetoda NonAction nvoking](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Obrázek 01**: Volání metody NonAction ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Předchozí](creating-a-controller-vb.md)
> [další](aspnet-mvc-controllers-overview-cs.md)
