---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: Pomocí třída TagBuilder pro sestavení pomocných rutin HTML (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Stephen Walther vás seznámí s třídu v rozhraní ASP.NET MVC s názvem třída TagBuilder užitečné nástroje. Třída TagBuilder pro můžete snadno použít...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 9759ea9b05ba5eba268901d3d2d1a15b2afe6202
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075439"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>Pomocí třída TagBuilder pro sestavení pomocných rutin HTML (C#)
====================
podle [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther vás seznámí s třídu v rozhraní ASP.NET MVC s názvem třída TagBuilder užitečné nástroje. Třída TagBuilder můžete použít k snadnému vytváření značky HTML.


Architektura ASP.NET MVC zahrnuje užitečný nástroj pro třídu s názvem třída TagBuilder, který vám pomůže při vytváření pomocných rutin HTML. Třída TagBuilder jako název třídy navrhuje, vám umožní snadno vytvářet značky HTML. V tomto kurzu (BRIEF) k dispozici máte přehled o třída TagBuilder a zjistíte, jak použít tuto třídu při vytváření jednoduchých pomocné rutiny HTML, který vykreslí HTML &lt;img&gt; značky.

## <a name="overview-of-the-tagbuilder-class"></a>Třída TagBuilder-přehled

Třída TagBuilder je obsažen v oboru názvů System.Web.Mvc. Má pět metod:

- AddCssClass() – umožňuje přidat nový *třídy = ""* atributů pro značku.
- GenerateId() – umožňuje přidat atribut id značky. Tato metoda automaticky nahrazuje tečky v id (ve výchozím nastavení, tečky jsou nahrazené podtržítka)
- MergeAttribute() – umožňuje přidat atributů pro značku. Existuje více přetížení této metody.
- SetInnerText() – umožňuje nastavit vnitřní text značky. Vnitřní text je automaticky použije kódování HTML.
- ToString() – Umožňuje vykreslit značky. Můžete určit, zda chcete vytvořit značku normální, počáteční značku, koncovou značku nebo samouzavírací značky.
  

Třída TagBuilder má čtyři důležité vlastnosti:

- Atributy – reprezentuje všechny atributy značky.
- IdAttributeDotReplacement - hodnota představuje znak metodou GenerateId() používá k nahrazení tečky (výchozí hodnota je podtržítko).
- InnerHTML – představuje vnitřní obsah značky. Přiřazení k této vlastnosti řetězce *nemá* řetězec s kódováním HTML.
- TagName – představuje název značky.

Tyto metody a vlastnosti získáte všechny základní metody a vlastnosti, které potřebujete k vytvoření značky jazyka HTML. Není nutné opravdu použít třída TagBuilder. Třída StringBuilder můžete místo toho použít. Nicméně třída TagBuilder vám život o něco jednodušší.

## <a name="creating-an-image-html-helper"></a>Vytvoření pomocné rutiny HTML bitové kopie

Při vytváření instance třídy TagBuilder předat název značky, který má být sestaveno TagBuilder konstruktoru. V dalším kroku může volat metody jako metody AddCssClass a MergeAttribute() změnit atributy značky. Nakonec proveďte volání metody ToString() k vykreslení značky.

Výpis 1 obsahuje například pomocné rutiny HTML bitové kopie. Pomocná rutina obrázku je implementována interně pomocí TagBuilder, který představuje HTML &lt;img&gt; značky.

**Výpis 1 - Helpers\ImageHelper.cs**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

Třída v informacích 1 obsahuje dvě statické přetížené metody s názvem obrázku. Při volání metody Image(), můžete předat objekt, který představuje sadu atributů HTML, nebo ne.

Všimněte si, jak metoda TagBuilder.MergeAttribute() umožňuje přidat jednotlivé atributy, jako je například atribut src TagBuilder. Všimněte si, jak metoda TagBuilder.MergeAttributes() umožňuje přidat kolekci atributů TagBuilder. Metoda MergeAttributes() přijímá slovník&lt;řetězec, objekt&gt; parametru. Třída RouteValueDictionary se používá k převodu objekt představující kolekci atributů do slovníku&lt;řetězec, objekt&gt;.

Po vytvoření Image pomocné rutiny, můžete v zobrazení ASP.NET MVC stejně jako u libovolné ostatní standardní pomocných rutin HTML pomocné rutiny. Zobrazení výpisu 2 používá pomocná rutina obrázku pro zobrazení zobrazí stejný obraz Xboxu dvakrát (viz obrázek 1). Pomocná rutina Image() je volána s i bez kolekce atributů HTML.

**Výpis 2 - Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


[![Dialogové okno Nový projekt](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**Obrázek 01**: Použití pomocné rutiny bitové kopie ([kliknutím ji zobrazíte obrázek v plné velikosti](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))


Všimněte si, že je nutné naimportovat přidružené pomocná rutina obrázku v horní části zobrazení Index.aspx obor názvů. Pomocné rutiny s následující direktivy importu:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [Předchozí](creating-custom-html-helpers-cs.md)
> [další](creating-page-layouts-with-view-master-pages-cs.md)
