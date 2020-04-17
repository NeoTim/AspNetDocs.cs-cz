---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Přidání dynamického obsahu na stránku uloženou v mezipaměti (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Přečtěte si, jak kombinovat dynamický obsah a obsah uložený v mezipaměti na stejné stránce. Substituce po mezipaměti umožňuje zobrazit dynamický obsah, například bannerové reklamy o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542258"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>Přidání dynamického obsahu do stránky v mezipaměti (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

> Přečtěte si, jak kombinovat dynamický obsah a obsah uložený v mezipaměti na stejné stránce. Nahrazení po mezipaměti umožňuje zobrazit dynamický obsah, například bannerové reklamy nebo zpravodajské položky, na stránce, která byla výstupní uložena v mezipaměti.

Využitím ukládání výstupu do mezipaměti můžete výrazně zlepšit výkon aplikace ASP.NET MVC. Namísto obnovení stránky každý a pokaždé, když je požadována stránka, stránka může být generována jednou a cache v paměti pro více uživatelů.

Ale je tu problém. Co když potřebujete na stránce zobrazit dynamický obsah? Představte si například, že chcete na stránce zobrazit bannerovou reklamu. Nechcete, aby bannerová reklama byla uložena do mezipaměti, aby každý uživatel viděl stejnou reklamu. Takhle bys nevydělával!

Naštěstí existuje jednoduché řešení. Můžete využít funkci ASP.NET frameworku nazvanou *substituce po mezipaměti*. Nahrazení po mezipaměti umožňuje nahradit dynamický obsah na stránce, která byla uložena do mezipaměti v paměti.

Za normálních okolností při výstupu &lt;mezipaměti stránky pomocí OutputCache&gt; atribut, stránka je uložena do mezipaměti na serveru i klienta (webový prohlížeč). Při použití nahrazení po mezipaměti je stránka uložena do mezipaměti pouze na serveru.

#### <a name="using-post-cache-substitution"></a>Použití nahrazení po mezipaměti

Použití nahrazení po mezipaměti vyžaduje dva kroky. Nejprve je třeba definovat metodu, která vrací řetězec, který představuje dynamický obsah, který chcete zobrazit na stránce uložené v mezipaměti. Dále zavoláte metodu HttpResponse.WriteSubstitution() a vstříknete dynamický obsah do stránky.

Představte si například, že chcete náhodně zobrazit různé zpravodajské položky na stránce uložené v mezipaměti. Třída v výpisu 1 zpřístupňuje jednu metodu s názvem RenderNews(), která náhodně vrátí jednu položku zprávy ze seznamu tří zpravodajských položek.

**Výpis 1 - Modely\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Chcete-li využít nahrazení po mezipaměti, zavolejte metodu HttpResponse.WriteSubstitution(). Metoda WriteSubstitution() nastaví kód tak, aby nahradil oblast stránky uložené v mezipaměti dynamickým obsahem. Metoda WriteSubstitution() se používá k zobrazení náhodné zpravodajské položky v zobrazení v seznamu 2.

**Výpis 2 – Zobrazení\Domů\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

Metoda RenderNews je předána metodě WriteSubstitution(). Všimněte si, že RenderNews metoda není volána. Místo toho odkaz na metodu je předán WriteSubstitution() pomocí AddressOf operátor.

Zobrazení rejstříku je uloženo do mezipaměti. Zobrazení je vráceno řadičem v výpisu 3. Všimněte si, že akce Index() je dekorována atributem &lt;OutputCache,&gt; který způsobí, že zobrazení indexu bude uloženo do mezipaměti po dobu 60 sekund.

**Výpis 3 – Řadiče\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

I když je zobrazení rejstříku uloženo do mezipaměti, při požadavku na stránku Index se zobrazí různé náhodné zpravodajské položky. Když požádáte o stránku Rejstřík, čas zobrazený na stránce se nezmění po dobu 60 sekund (viz obrázek 1). Skutečnost, že se čas nezmění, dokazuje, že stránka je uložena do mezipaměti. Obsah vstřikovaný metodou WriteSubstitution() – náhodná novinka – se však s každým požadavkem změní .

**Obrázek 1 – Vkládání dynamických zpravodajských položek na stránku uloženou v mezipaměti**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Použití nahrazení po mezipaměti v pomocných metodách

Jednodušší způsob, jak využít nahrazení po mezipaměti je zapouzdřit volání WriteSubstitution() metoda v rámci vlastní pomocné metody. Tento přístup je ilustrován pomocnou metodou v výpisu 4.

**Výpis 4 – Pomocníci\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

Výpis 4 obsahuje modul jazyka Visual Basic, který zveřejňuje dvě metody: RenderBanner() a RenderBannerInternal(). RenderBanner() Metoda představuje skutečnou pomocnou metodu. Tato metoda rozšiřuje standardní ASP.NET Třídy MVC HtmlHelper tak, aby bylo možné volat Html.RenderBanner() v zobrazení, stejně jako všechny ostatní pomocné metody.

Metoda RenderBanner() volá metodu HttpResponse.WriteSubstitution() předává metodu RenderBannerInternal() metodě WriteSubstitution().

Metoda RenderBannerInternal() je soukromá metoda. Tato metoda nebude vystavena jako pomocná metoda. Metoda RenderBannerInternal() náhodně vrátí jeden obrázek bannerové reklamy ze seznamu tří obrázků bannerové reklamy.

Upravené zobrazení indexu v výpisu 5 ukazuje, jak můžete použít RenderBanner() pomocné metody. Všimněte si, že &lt;&gt; další %@ Import % směrnice je zahrnuta v horní části zobrazení pro import mvcApplication1.Helpers obor názvů. Pokud zanedbáte import tohoto oboru názvů, pak RenderBanner() metoda se nezobrazí jako metoda na Html vlastnost.

**Výpis 5 – Zobrazení\Home\Index.aspx (s metodou RenderBanner()**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Když požádáte o stránku vykreslenou zobrazením v seznamu 5, zobrazí se u každého požadavku jiná bannerová reklama (viz obrázek 2). Stránka je uložena do mezipaměti, ale bannerová reklama je vložena dynamicky pomocnou metodou RenderBanner().

**Obrázek 2 – Zobrazení indexu zobrazující náhodnou bannerovou reklamu**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Souhrn

Tento kurz vysvětlil, jak můžete dynamicky aktualizovat obsah na stránce uložené v mezipaměti. Zjistili jste, jak používat metodu HttpResponse.WriteSubstitution() k povolení vkládání dynamického obsahu na stránku uloženou v mezipaměti. Také jste se naučili, jak zapouzdřit volání WriteSubstitution() metoda v rámci metody pomocné položky HTML.

Využijte ukládání do mezipaměti, kdykoli je to možné – může to mít dramatický dopad na výkon vašich webových aplikací. Jak je vysvětleno v tomto kurzu, můžete využít ukládání do mezipaměti, i když potřebujete zobrazit dynamický obsah na stránkách.

> [!div class="step-by-step"]
> [Předchozí](improving-performance-with-output-caching-vb.md)
> [další](creating-a-controller-vb.md)
