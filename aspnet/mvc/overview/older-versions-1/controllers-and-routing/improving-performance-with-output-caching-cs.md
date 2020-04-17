---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: Zlepšení výkonu pomocí ukládání výstupu do mezipaměti (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto kurzu se dozvíte, jak můžete dramaticky zlepšit výkon vašich webových aplikací ASP.NET MVC využitím výstupního ukládání do mezipaměti. Vy...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542713"
---
# <a name="improving-performance-with-output-caching-c"></a>Zlepšení výkonu ukládáním výstupů do mezipaměti (C#)

podle [společnosti Microsoft](https://github.com/microsoft)

> V tomto kurzu se dozvíte, jak můžete dramaticky zlepšit výkon vašich webových aplikací ASP.NET MVC využitím výstupního ukládání do mezipaměti. Dozvíte se, jak uložit do mezipaměti výsledek vrácený z akce řadiče tak, aby stejný obsah nemusí být vytvořen každý a pokaždé, když nový uživatel vyvolá akci.

Cílem tohoto kurzu je vysvětlit, jak můžete dramaticky zlepšit výkon aplikace ASP.NET MVC s využitím výstupní mezipaměti. Výstupní mezipaměť umožňuje ukládat obsah vrácený akcí řadiče do mezipaměti. Tímto způsobem nemusí být generován stejný obsah pokaždé, když je vyvolána stejná akce kontroleru.

Představte si například, že aplikace ASP.NET MVC zobrazí seznam databázových záznamů v zobrazení s názvem Index. Za normálních okolností každý a pokaždé, když uživatel vyvolá akce řadiče, který vrátí zobrazení indexu, sada databázových záznamů musí být načteny z databáze spuštěním databázového dotazu.

Pokud na druhé straně můžete využít výstupní mezipaměti pak můžete vyhnout provádění databázový dotaz pokaždé, když každý uživatel vyvolá stejnou akci řadiče. Zobrazení lze načíst z mezipaměti namísto regenerovány z akce kontroleru. Ukládání do mezipaměti umožňuje vyhnout se provádění redundantní práce na serveru.

## <a name="enabling-output-caching"></a>Povolení ukládání výstupu do mezipaměti

Ukládání výstupu do mezipaměti povolíte přidáním atributu [OutputCache] do akce jednotlivých řadičů nebo celé třídy řadiče. Například řadič v výpisu 1 zpřístupňuje akci s názvem Index(). Výstup akce Index() je uložen do mezipaměti po dobu 10 sekund.

**Výpis 1 – Řadiče\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

V beta verzi ASP.NET MVC, výstup ukládání do mezipaměti [http://www.MySite.com/](http://www.mysite.com/)nefunguje pro URL jako . Místo toho je nutné [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)zadat adresu URL, která se líbí . 

V výpisu 1 je výstup akce Index() uložen do mezipaměti po dobu 10 sekund. Pokud chcete, můžete určit mnohem delší dobu trvání mezipaměti. Chcete-li například uložit výstup akce řadiče do mezipaměti na jeden den, můžete určit dobu trvání \* mezipaměti \* 86400 sekund (60 sekund 60 minut 24 hodin).

Neexistuje žádná záruka, že obsah bude uložen do mezipaměti po dobu, kterou zadáte. Když dojde k nedostatku prostředků paměti, mezipaměť spustí automatické vyřazování obsahu.

Ovladač Domů v seznamu 1 vrátí zobrazení indexu v seznamu 2. Na tomto pohledu není nic zvláštního. Zobrazení Rejstřík uvidíte pouze aktuální čas (viz obrázek 1).

**Výpis 2 – Zobrazení\Domů\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**Obrázek 1 – Zobrazení indexu v mezipaměti**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

Pokud vyvoláte akci Index() vícekrát zadáním adresy URL /Home/Index do adresního řádku prohlížeče a opakovaným stisknutím tlačítka Aktualizovat/Znovu načíst v prohlížeči, čas zobrazený v zobrazení rejstříku se nezmění po dobu 10 sekund. Současně se zobrazí stejný čas, protože zobrazení je uloženo do mezipaměti.

Je důležité si uvědomit, že stejné zobrazení je uloženo do mezipaměti pro každého, kdo navštíví vaši aplikaci. Každý, kdo vyvolá akci Index() získá stejnou verzi zobrazení indexu v mezipaměti. To znamená, že množství práce, které musí webový server provést, aby sloužil zobrazení indexu, je výrazně sníženo.

Pohled v Listing 2 se stane dělat něco opravdu jednoduchého. Zobrazení zobrazuje pouze aktuální čas. Stejně snadno však můžete uložit do mezipaměti zobrazení, které zobrazuje sadu databázových záznamů. V takovém případě by nebylo nutné načíst sadu databázových záznamů z databáze pokaždé, když je vyvolána akce kontrolora, která vrací zobrazení. Ukládání do mezipaměti může snížit množství práce, kterou musí webový i databázový server provést.

Nepoužívejte direktivu stránky &lt;&gt; %@ OutputCache % v zobrazení MVC. Tato směrnice je krvácení přes ze světa webových formulářů a by neměl být používán v ASP.NET aplikace MVC.

## <a name="where-content-is-cached"></a>Kde je obsah uložen do mezipaměti

Ve výchozím nastavení je obsah při použití atributu [OutputCache] uložen do mezipaměti ve třech umístěních: na webovém serveru, na serverech proxy a ve webovém prohlížeči. Přesně můžete určit, kde je obsah uložen do mezipaměti, úpravou vlastnosti Location atributu [OutputCache].

Vlastnost Location můžete nastavit na některou z následujících hodnot:

> · Jakékoli
> 
> · Klienta
> 
> · Následný
> 
> · Server
> 
> · Žádný
> 
> · ServerandClient

Ve výchozím nastavení má vlastnost Location hodnotu Any. Existují však situace, ve kterých můžete chtít do mezipaměti pouze v prohlížeči nebo pouze na serveru. Pokud například ukládáte informace do mezipaměti, které jsou přizpůsobeny pro každého uživatele, neměli byste je ukládat do mezipaměti na serveru. Pokud zobrazujete různé informace pro různé uživatele, měli byste je ukládat do mezipaměti pouze na straně klienta.

Například řadič v listing 3 zpřístupňuje akci s názvem GetName(), která vrací aktuální uživatelské jméno. Pokud Jack přihlásí k webu a vyvolá GetName() akce pak akce vrátí řetězec "Hi Jack". Pokud, následně Jill přihlásí na webové stránky a vyvolá GetName() akce pak se také dostane řetězec "Hi Jack". Řetězec je uložen do mezipaměti na webovém serveru pro všechny uživatele poté, co Jack zpočátku vyvolá akci řadiče.

**Výpis 3 – Řadiče\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

S největší pravděpodobností ovladač v listingu 3 nefunguje tak, jak chcete. Nechceš jill zobrazit zprávu "Ahoj Jacku".

Nikdy byste neměli ukládat osobní obsah do mezipaměti serveru. Chcete-li však zvýšit výkon, můžete chtít ukládat personalizovaný obsah do mezipaměti prohlížeče do mezipaměti. Pokud ukládáte obsah do mezipaměti v prohlížeči a uživatel vyvolá stejnou akci řadiče vícekrát, lze obsah načíst z mezipaměti prohlížeče namísto serveru.

Upravený řadič v listingu 4 ukládá výstup akce GetName(). Obsah je však uložen do mezipaměti pouze v prohlížeči a nikoli na serveru. Tímto způsobem, když více uživatelů vyvolat GetName() metoda, každý člověk získá své vlastní uživatelské jméno a nikoli jiné osoby uživatelské jméno.

**Výpis 4 – Řadiče\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

Všimněte si, že atribut [OutputCache] v listingu 4 obsahuje vlastnost Location nastavenou na hodnotu OutputCacheLocation.Client. Atribut [OutputCache] také obsahuje vlastnost NoStore. Vlastnost NoStore se používá k informování proxy serverů a prohlížeče, že by neměly ukládat trvalou kopii obsahu uloženého v mezipaměti.

## <a name="varying-the-output-cache"></a>Změna výstupní mezipaměti

V některých situacích můžete chtít různé verze stejného obsahu uložené v mezipaměti. Představte si například, že vytváříte stránku předlohy/podrobností. Na stránce předlohy se zobrazí seznam názvů filmů. Po klepnutí na název získáte podrobnosti o vybraném filmu.

Pokud uložíte stránku podrobností do mezipaměti, zobrazí se podrobnosti o stejném filmu bez ohledu na to, na který film klepnete. První film vybraný prvním uživatelem se zobrazí všem budoucím uživatelům.

Tento problém můžete vyřešit využitím varyByParam vlastnost atributu [OutputCache]. Tato vlastnost umožňuje vytvářet různé verze uložených v mezipaměti stejného obsahu, pokud se parametr formuláře nebo parametr řetězce dotazu liší.

Například řadič v výpisu 5 zpřístupňuje dvě akce s názvem Master() a Details(). Akce Master() vrátí seznam názvů filmů a akce Podrobnosti() vrátí podrobnosti vybraného filmu.

**Výpis 5 – Controllers\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Akce Master() zahrnuje vlastnost VaryByParam s hodnotou "none". Při vyvolání akce Master() je vrácena stejná verze zobrazení předlohy v mezipaměti. Všechny parametry formuláře nebo parametry řetězce dotazu jsou ignorovány (viz obrázek 2).

**Obrázek 2 – Zobrazení /Filmy/Hlavní**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**Obrázek 3 – Zobrazení /Filmy/Podrobnosti**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

Akce Details() zahrnuje vlastnost VaryByParam s hodnotou "Id". Pokud jsou akci kontroleru předány různé hodnoty parametru Id, jsou generovány různé verze zobrazení Podrobnosti v mezipaměti.

Je důležité si uvědomit, že použití VaryByParam vlastnost má za následek více ukládání do mezipaměti a ne méně. Pro každou jinou verzi parametru Id je vytvořena jiná verze zobrazení Podrobnosti v mezipaměti.

Vlastnost VaryByParam můžete nastavit na následující hodnoty:

> \*= Vždy, když se parametr řetězce formuláře nebo řetězce dotazu liší, vytvořte jinou verzi uloženou v mezipaměti.
> 
> none = Nikdy nevytvářet různé verze uložené v mezipaměti
> 
> Středník seznam parametrů = Vytvořit různé verze uložené v mezipaměti vždy, když některý z parametrů formuláře nebo parametry řetězce dotazu v seznamu se liší

## <a name="creating-a-cache-profile"></a>Vytvoření profilu mezipaměti

Jako alternativu ke konfiguraci vlastností výstupní mezipaměti úpravou vlastností atributu [OutputCache] můžete vytvořit profil mezipaměti v souboru webové konfigurace (web.config). Vytvoření profilu mezipaměti ve webovém konfiguračním souboru nabízí několik důležitých výhod.

Nejprve konfigurací ukládání výstupu do mezipaměti ve webovém konfiguračním souboru můžete řídit způsob, jakým akce řadiče uchovává obsah do mezipaměti v jednom centrálním umístění. Můžete vytvořit jeden profil mezipaměti a použít profil na několik řadičů nebo akcí řadiče.

Za druhé můžete upravit webový konfigurační soubor bez nutnosti opětovné kompilace aplikace. Pokud potřebujete zakázat ukládání do mezipaměti pro aplikaci, která již byla nasazena do produkčního prostředí, můžete jednoduše upravit profily mezipaměti definované v konfiguračním souboru webu. Všechny změny webového konfiguračního souboru budou rozpoznány automaticky a použity.

Například oddíl &lt;konfigurace&gt; webu ukládání do mezipaměti v seznamu 6 definuje profil mezipaměti s názvem Cache1Hour. Oddíl &lt;ukládání&gt; do mezipaměti &lt;se musí&gt; zobrazit v části system.web webového konfiguračního souboru.

**Výpis 6 - Ukládání do mezipaměti sekce pro web.config**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

Řadič v seznamu 7 ukazuje, jak můžete použít profil Cache1Hour na akci řadiče s atributem [OutputCache].

**Výpis 7 – Řadiče\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

Pokud vyvoláte akci Index() vystavenou řadičem v výpisu 7, bude stejný čas vrácen po dobu 1 hodiny.

## <a name="summary"></a>Souhrn

Ukládání výstupu do mezipaměti poskytuje velmi snadný způsob, jak dramaticky zlepšit výkon aplikací ASP.NET MVC. V tomto kurzu jste se naučili, jak používat atribut [OutputCache] k ukládání výstupu akcí řadiče do mezipaměti. Také jste se dozvěděli, jak upravit vlastnosti atributu [OutputCache], jako jsou vlastnosti Duration a VaryByParam, chcete-li upravit způsob ukládání obsahu do mezipaměti. Nakonec jste se naučili definovat profily mezipaměti ve webovém konfiguračním souboru.

> [!div class="step-by-step"]
> [Předchozí](understanding-action-filters-cs.md)
> [další](adding-dynamic-content-to-a-cached-page-cs.md)
