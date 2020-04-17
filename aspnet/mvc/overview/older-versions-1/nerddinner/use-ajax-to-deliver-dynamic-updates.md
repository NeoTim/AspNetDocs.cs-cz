---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Použití ajaxu k doručování dynamických aktualizací | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 10 implementuje podporu pro přihlášené uživatele, aby RSVP jejich zájem o účast na večeři, pomocí Ajax-založený přístup integrovaný do detailu večeře ...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541244"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>Použití jazyka AJAX k dynamickým aktualizacím

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 10 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 10 implementuje podporu pro přihlášené uživatele, aby rsvp jejich zájem o účast na večeři, pomocí Přístup založený na Ajax integrované do stránky podrobnosti o večeři.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner Krok 10: AJAX Povolení RSVPs přijímá

Nyní implementujeme podporu přihlášených uživatelů, abychom odpověděli na jejich zájem o účast na večeři. Umožníme to pomocí přístupu založeného na AJAXintegrovaném na stránce s podrobnostmi o večeři.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Označuje, zda je uživatel rsvp'd

Uživatelé mohou navštívit adresu URL */Dinners/Details/[id]* a zobrazit podrobnosti o konkrétní večeři:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Metoda akce Details() je implementována takto:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

Náš první krok k implementaci podpory RSVP bude přidání "IsUserRegistered(uživatelské jméno)" pomocné metody naše Dinner objektu (v rámci Dinner.cs částečné třídy jsme vytvořili dříve). Tato pomocná metoda vrátí true nebo false v závislosti na tom, zda je uživatel aktuálně rsvp'd pro večeři:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Do šablony zobrazení Details.aspx pak můžeme přidat následující kód, který zobrazí příslušnou zprávu s uvedením, zda je uživatel pro událost zaregistrován nebo ne:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

A teď, když uživatel navštíví večeři, pro kterou je zaregistrován, zobrazí se tato zpráva:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

A když navštíví večeři, nejsou registrovány pro uvidí níže zprávu:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Implementace metody akce registru

Nyní přidáme funkce nezbytné k tomu, aby uživatelé mohli na večeři z podrobností povolit uživatelům rsvp pro večeři.

Chcete-li tento problém implementovat, vytvoříme novou třídu "RSVPController" kliknutím pravým tlačítkem myši na adresář \Controllers a výběrem příkazu nabídky&gt;Přidat řadič.

Budeme implementovat "Register" metoda akce v rámci nové třídy RSVPController, která trvá id pro Večeři jako argument, načte příslušný Dinner objekt, zkontroluje, zda přihlášený uživatel je aktuálně v seznamu uživatelů, kteří se zaregistrovali pro něj, a pokud ne přidá RSVP objekt pro ně:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Všimněte si, jak vracíme jednoduchý řetězec jako výstup metody akce. Mohli jsme vložit tuto zprávu do šablony zobrazení - ale protože je tak malá, použijeme pomocnou metodu Content() v základní třídě řadiče a vrátíme zprávu řetězce jako výše.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>Volání metody akce RSVPForEvent pomocí metody AJAX

Použijeme AJAX k vyvolání metody akce Register z našeho zobrazení Podrobnosti. Implementace je to docela snadné. Nejprve přidáme dva odkazy na knihovnu skriptů:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

První knihovna odkazuje na základní ASP.NET knihovny skriptů na straně klienta AJAX. Tento soubor má velikost přibližně 24 kB (komprimovaný) a obsahuje základní funkce AJAX na straně klienta. Druhá knihovna obsahuje užitné funkce, které se integrují s vestavěnými pomocnými metodami ASP.NET MVC AJAX (které budeme brzy používat).

Potom můžeme aktualizovat kód šablony zobrazení, který jsme přidali dříve, takže místo toho, abychom namísto vynětí zprávy "Nejste registrováni pro tuto událost", místo toho vykreslujeme odkaz, který při pushprovádí volání AJAX, které vyvolá naši metodu akce RSVPForEvent na našem řadiči RSVP a RSVP uživatele:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

Ajax.ActionLink() pomocná metoda použitá výše je vestavěná do ASP.NET MVC a je podobná metodě pomocného zařízení Html.ActionLink() s tím rozdílem, že namísto provedení standardní navigace provede volání AJAX na metodu akce po klepnutí na odkaz. Výše voláme metodu akce "Register" na řadiči "RSVP" a předáváme mu DinnerID jako parametr "id". Konečný parametr AjaxOptions, který předáváme, naznačuje, že chceme vzít obsah &lt;&gt; vrácený z metody akce a aktualizovat element HTML div na stránce, jehož id je "rsvpmsg".

A teď, když uživatel přejde na večeři, pro kterou ještě není zaregistrován, zobrazí se mu odkaz na rsvp:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

Pokud kliknou na odkaz "RSVP pro tuto událost", prodají volání AJAX metodě akce Register na kontroleru RSVP a po dokončení se jim zobrazí aktualizovaná zpráva jako níže:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

Šířka pásma sítě a provoz zapojených při tomto volání AJAX je opravdu lehký. Když uživatel klikne na odkaz "RSVP pro tuto událost", je malý požadavek na síť HTTP POST proveden na adresu URL */Dinners/Register/1,* která vypadá níže na lince:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

A odpověď z naší metody Registrace akce je jednoduše:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Toto lehké volání je rychlé a bude fungovat i přes pomalou síť.

### <a name="adding-a-jquery-animation"></a>Přidání animace jQuery

Funkce AJAX, kterou jsme implementovali, funguje dobře a rychle. Někdy se to může stát tak rychle, že si uživatel nemusí všimnout, že odkaz RSVP byl nahrazen novým textem. Chcete-li výsledek trochu více zřejmé, můžeme přidat jednoduchou animaci upozornit na aktualizační zprávu.

Výchozí ASP.NET šablona projektu MVC obsahuje jQuery - vynikající (a velmi populární) open source JavaScript knihovnu, která je také podporována společností Microsoft. jQuery poskytuje řadu funkcí, včetně pěkné HTML DOM výběra efektů knihovny.

Chcete-li použít jQuery, nejprve na něj přidáme odkaz na skript. Vzhledem k tomu, že budeme používat jQuery v různých místech v rámci našich stránek, přidáme odkaz na skript v našem souboru stránky předlohy Site.master, aby jej mohly používat všechny stránky.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*Tip: Ujistěte se, že jste nainstalovali opravu hotfix JavaScript intellisense pro vs 2008 SP1, která umožňuje bohatší podporu intellisense pro soubory JavaScript (včetně jQuery). Můžete si jej stáhnout z:http://tinyurl.com/vs2008javascripthotfix*

Kód napsaný pomocí JQuery často používá globální metodu JavaScriptu "$()", která načítá jeden nebo více elementů HTML pomocí voliče CSS. Například *$("#rsvpmsg")* vybere libovolný element HTML s id rsvpmsg, zatímco *$(".something")* vybere všechny prvky s názvem třídy CSS "něco". Můžete také psát pokročilejší dotazy, jako je "vrátit všechna zaškrtnutá přepínací tlačítka" pomocí výběrového dotazu, jako je: *$("input[@type=radio][@checked]")*.

Jakmile vyberete prvky, můžete volat metody na ně provést akci, jako je jejich skrytí: *$("#rsvpmsg").hide();*

Pro náš scénář RSVP definujeme jednoduchou funkci JavaScriptu s názvem "AnimateRSVPMessage", &lt;která&gt; vybere div "rsvpmsg" a animuje velikost jeho textového obsahu. Níže uvedený kód spustí text malý a pak způsobí, že zvýšení v průběhu 400 milisekund časový rámec:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Můžeme pak wire-up tuto funkci JavaScript, které mají být volány po našem volání AJAX úspěšně dokončí předáním jeho jméno naše Ajax.ActionLink() pomocné metody (přes AjaxOptions "OnSuccess" vlastnost události):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

A teď, když je kliknuto na odkaz "RSVP pro tuto událost" a naše volání AJAX úspěšně dokončí, obsahová zpráva odeslaná zpět se animuje a roste:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

Kromě poskytování "OnSuccess" událost AjaxOptions objekt zpřístupňuje OnBegin, OnFailure a OnComplete události, které můžete zpracovat (spolu s řadou dalších vlastností a užitečných možností).

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Vyčištění - refaktorovat částečné zobrazení RSVP

Naše šablona zobrazení podrobností začíná být trochu dlouhá, což přesčas trochu ztíží pochopení. Chcete-li zlepšit čitelnost kódu, dokončeme vytvořením částečného zobrazení – RSVPStatus.ascx – které zapouzdřuje veškerý kód zobrazení RSVP pro naši stránku Podrobnosti.

Můžeme to udělat kliknutím pravým tlačítkem myši na složku \Views\Dinners a výběrem příkazu nabídky Přidat-&gt;zobrazit. Budeme mít to trvat Dinner objekt jako jeho silně typed ViewModel. Poté můžeme zkopírovat/vložit obsah RSVP z našeho zobrazení Details.aspx do něj.

Poté, co jsme udělali, že pojďme také vytvořit další částečné zobrazení - EditAndDeleteLinks.ascx - to zapouzdřuje naše Upravit a odstranit odkaz zobrazit kód. Budeme také mít vzít Dinner objekt jako jeho silně typed ViewModel a zkopírujte nebo vložte upravit a odstranit logiku z našeho Details.aspx zobrazení do něj.

Naše podrobnosti zobrazení šablony pak můžete zahrnout pouze dvě html.RenderPartial() volání metody v dolní části:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

Díky čistič kódu číst a udržovat.

### <a name="next-step"></a>Další krok

Podívejme se nyní na to, jak můžeme ajax dále používat a přidat interaktivní podporu mapování do naší aplikace.

> [!div class="step-by-step"]
> [Předchozí](secure-applications-using-authentication-and-authorization.md)
> [další](use-ajax-to-implement-mapping-scenarios.md)
