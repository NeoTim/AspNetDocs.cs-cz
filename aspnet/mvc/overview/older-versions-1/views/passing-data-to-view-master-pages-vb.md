---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: Předávání dat do zobrazení stránek předlohy (VB) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Cílem tohoto kurzu je vysvětlit, jak můžete předat data z řadiče na stránku předlohy zobrazení. Zkoumáme dvě strategie pro předávání dat do zobrazení m...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: ef65541a5f2297414f923e2f8108a14de67531e5
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542466"
---
# <a name="passing-data-to-view-master-pages-vb"></a>Předání dat stránkám předlohy pro zobrazení (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> Cílem tohoto kurzu je vysvětlit, jak můžete předat data z řadiče na stránku předlohy zobrazení. Zkoumáme dvě strategie pro předávání dat na stránku předlohy zobrazení. Nejprve diskutujeme o jednoduché řešení, které má za následek aplikace, která je obtížné udržovat. Dále zkoumáme mnohem lepší řešení, které vyžaduje trochu více počáteční práce, ale výsledkem je mnohem více udržovatelné aplikace.

## <a name="passing-data-to-view-master-pages"></a>Předávání dat do zobrazení stránek předlohy

Cílem tohoto kurzu je vysvětlit, jak můžete předat data z řadiče na stránku předlohy zobrazení. Zkoumáme dvě strategie pro předávání dat na stránku předlohy zobrazení. Nejprve diskutujeme o jednoduché řešení, které má za následek aplikace, která je obtížné udržovat. Dále zkoumáme mnohem lepší řešení, které vyžaduje trochu více počáteční práce, ale výsledkem je mnohem více udržovatelné aplikace.

### <a name="the-problem"></a>Problém

Představte si, že vytváříte aplikaci pro databázi filmů a chcete zobrazit seznam kategorií filmů na každé stránce aplikace (viz obrázek 1). Představte si navíc, že seznam kategorií filmů je uložen v databázové tabulce. V takovém případě by mělo smysl načíst kategorie z databáze a vykreslit seznam kategorií filmů v rámci stránky předlohy zobrazení.

[![Zobrazení kategorií filmů na vzorové stránce zobrazení](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**Obrázek 01**: Zobrazení kategorií filmů na vzorové stránce zobrazení[(Obrázek v plné velikosti zobrazíte klepnutím)](passing-data-to-view-master-pages-vb/_static/image3.png)

Tady je problém. Jak načtete seznam kategorií filmů na stránce předlohy? Je lákavé volat metody tříd modelu přímo na stránce předlohy. Jinými slovy je lákavé zahrnout kód pro načítání dat z databáze přímo na stránce předlohy. Vynechání řadiče MVC pro přístup k databázi by však porušovat čisté oddělení obavy, které je jednou z hlavních výhod vytváření aplikace MVC.

V aplikaci MVC chcete, aby všechny interakce mezi zobrazeními MVC a modelem MVC byly zpracovány řadiči MVC. Toto oddělení obav vede k více udržovatelné, adaptabilní a testovatelné aplikace.

V aplikaci MVC by měla být všechna data předaná zobrazení – včetně stránky předlohy zobrazení – předána zobrazení akcí kontroleru. Kromě toho by měly být předány údaje s využitím dat zobrazení. Ve zbývající části tohoto kurzu zkoumám dvě metody předávání dat zobrazení na stránku předlohy zobrazení.

### <a name="the-simple-solution"></a>Jednoduché řešení

Začněme nejjednodušším řešením předávání dat zobrazení z řadiče na stránku předlohy zobrazení. Nejjednodušším řešením je předat data zobrazení pro stránku předlohy v každé akci kontroleru.

Zvažte řadič v výpisu 1. Zveřejňuje dvě akce `Index()` s `Details()`názvem a . Metoda `Index()` akce vrátí každý film v databázové tabulce Filmy. Metoda `Details()` akce vrátí každý film v určité kategorii filmu.

**Výpis 1 –`Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

Všimněte si, že `Index()` akce a `Details()` akce přidat dvě položky pro zobrazení dat. Akce `Index()` přidá dvě klávesy: kategorie a filmy. Klíč kategorie představuje seznam kategorií filmů zobrazených na stránce předlohy zobrazení. Klíč filmy představuje seznam filmů zobrazených na stránce zobrazení rejstříku.

Akce `Details()` také přidá dvě klávesy s názvem kategorie a filmy. Klíč kategorie opět představuje seznam kategorií filmů zobrazených na stránce předlohy zobrazení. Klíč filmy představuje seznam filmů v určité kategorii zobrazený na stránce zobrazení podrobností (viz obrázek 2).

[![Zobrazení Podrobnosti](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**Obrázek 02**: Zobrazení podrobností[(Kliknutím zobrazíte obrázek v plné velikosti)](passing-data-to-view-master-pages-vb/_static/image6.png)

Zobrazení Rejstřík je obsaženo v seznamu 2. Jednoduše iteruje seznam filmů reprezentovaných položkou filmů v zobrazení dat.

**Výpis 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

Stránka předlohy zobrazení je obsažena v seznamu 3. Stránka předlohy zobrazení itetuje a vykresluje všechny kategorie filmů reprezentované položkou kategorií z dat ze zobrazení.

**Výpis 3 –`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

Všechna data jsou předána zobrazení a stránku předlohy zobrazení prostřednictvím dat zobrazení. To je správný způsob předání dat na stránku předlohy.

Takže, co je špatného na tomto řešení? Problém je v tom, že toto řešení porušuje princip DRY (Don't Repeat Yourself). Každá akce řadiče musí přidat stejný seznam kategorií filmů, aby bylo možné zobrazit data. Duplicitní kód v aplikaci je vaše aplikace mnohem obtížnější udržovat, přizpůsobovat a upravovat.

### <a name="the-good-solution"></a>Dobré řešení

V této části zkontrolujeme alternativní a lepší řešení předávání dat z akce kontroleru na stránku předlohy zobrazení. Namísto přidání kategorií filmů pro stránku předlohy v každé akci kontroleru přidáme kategorie filmů do dat zobrazení pouze jednou. Všechna data zobrazení používaná stránkou předlohy zobrazení jsou přidána do řadiče aplikace.

Třída ApplicationController je obsažena v výpisu 4.

Třída ApplicationController je obsažena v výpisu 4.

**Výpis 4 –`Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

Existují tři věci, které byste si měli všimnout o řadiči aplikace v seznamu 4. Nejprve si všimněte, že třída dědí ze základní třídy System.Web.Mvc.Controller. Řadič aplikace je třída řadiče.

Za druhé všimněte si, že třída řadiče aplikace je MustInherit třídy. Třída MustInherit je třída, která musí být implementována konkrétní třídou. Vzhledem k tomu, že řadič aplikace je třída MustInherit, nelze vyvolat žádné metody definované ve třídě přímo. Pokud se pokusíte vyvolat třídu Aplikace přímo, zobrazí se chybová zpráva Prostředek nelze najít.

Za třetí všimněte si, že řadič aplikace obsahuje konstruktor, který přidá seznam kategorií filmu pro zobrazení dat. Každá třída kontroleru, která dědí z řadiče aplikace, volá konstruktor aplikačního kontroléru automaticky. Kdykoli zavoláte jakoukoli akci na libovolném řadiči, který dědí z řadiče aplikace, kategorie filmů se automaticky zahrnou do dat zobrazení.

Řadič Filmy v seznamu 5 dědí z řadiče aplikace.

**Výpis 5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

Řadič Filmy, stejně jako domácí řadič popisovaný v předchozí `Index()` části, zveřejňuje dvě metody akce s názvem a `Details()`. Všimněte si, že seznam kategorií filmů zobrazených na stránce předlohy zobrazení není přidán k zobrazení dat v metodě `Index()` nebo. `Details()` Vzhledem k tomu, že řadič Filmy dědí z řadiče aplikace, přidá se seznam kategorií filmů, aby se data automaticky zobrazila.

Všimněte si, že toto řešení pro přidání dat zobrazení pro stránku předlohy zobrazení neporušuje princip DRY (Neopakujte sami). Kód pro přidání seznamu kategorií filmů pro zobrazení dat je obsažen pouze v jednom umístění: konstruktor pro řadič aplikace.

### <a name="summary"></a>Souhrn

V tomto kurzu jsme diskutovali o dvou přístupech k předávání dat zobrazení z řadiče na stránku předlohy zobrazení. Nejprve jsme zkoumali jednoduchý, ale obtížně udržovatelné přístup. V první části jsme probrali, jak můžete přidat data zobrazení pro stránku předlohy zobrazení v každé akci kontroleru ve vaší aplikaci. Dospěli jsme k závěru, že to byl špatný přístup, protože porušuje zásadu DRY (Don't Repeat Yourself).

Dále jsme zkoumali mnohem lepší strategii pro přidávání dat vyžadované stránkou předlohy zobrazení pro zobrazení dat. Namísto přidání dat zobrazení v každé akci kontrolora jsme data zobrazení přidali pouze jednou v rámci řadiče aplikace. Tímto způsobem se můžete vyhnout duplicitní kód při předávání dat na stránku předlohy zobrazení v aplikaci ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](creating-page-layouts-with-view-master-pages-vb.md)
