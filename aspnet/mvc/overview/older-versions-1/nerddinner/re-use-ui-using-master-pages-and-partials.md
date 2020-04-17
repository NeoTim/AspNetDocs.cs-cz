---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Opakované použití ui pomocí vzorových stránek a částečných částek | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 7 se zabývá způsoby, jak můžeme použít "Suchý princip" v našich šablonách zobrazení, abychom eliminovali duplikaci kódu pomocí šablon částečného zobrazení a stránek předlohy.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542596"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Opakované použití uživatelského rozhraní pomocí stránek předloh a částečných zobrazení

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 7 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 7 se zabývá způsoby, jak můžeme použít "SUCHÝ princip" v našich šablonách zobrazení, abychom eliminovali duplikaci kódu pomocí šablon částečného zobrazení a stránek předlohy.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner Krok 7: Částečné a vzorové stránky

Jednou z filozofií návrhu, ASP.NET MVC zahrnuje, je princip "Neopakujte se" (běžně označovaný jako "DRY"). Návrh DRY pomáhá eliminovat duplikaci kódu a logiky, což v konečném důsledku umožňuje rychlejší vytváření aplikací a snadnější údržbu.

Již jsme viděli princip DRY aplikovaný v několika našich scénářích NerdDinner. Několik příkladů: naše logika ověřování je implementována v rámci naší vrstvy modelu, což umožňuje její vynucení v rámci úprav a vytváření scénářů v našem řadiči; znovu používáme šablonu zobrazení "NotFound" v metodách akce Úpravy, Podrobnosti a Odstranit; používáme konvence- pojmenování vzor s našimi šablonami zobrazení, což eliminuje potřebu explicitně zadat název, když voláme View() pomocné metody; a znovu používáme třídu DinnerFormViewModel pro scénáře akce Úpravy i Vytvoření.

Podívejme se nyní na způsoby, jak můžeme použít "DRY Princip" v našem zobrazení šablony k odstranění duplikace kódu tam také.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Opětovné navštěvujeme naše šablony pro úpravy a vytváření zobrazení

V současné době používáme dvě různé šablony zobrazení – "Edit.aspx" a "Create.aspx" – k zobrazení našeho uživatelského nastavení formuláře Večeři. Rychlé vizuální srovnání z nich zdůrazňuje, jak podobné jsou. Níže je uvedeno, jak vypadá formulář pro vytvoření:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

A tady je to, co naše "Edit" formulář vypadá:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Není v tom velký rozdíl? Kromě textu nadpisu a záhlaví jsou ovládací prvky rozložení formuláře a zadávání identické.

Pokud otevřeme šablony zobrazení "Edit.aspx" a "Create.aspx", zjistíme, že obsahují stejné rozložení formuláře a vstupní řídicí kód. Tato duplikace znamená, že nakonec budeme muset provádět změny dvakrát, kdykoli zavedeme nebo změníme novou vlastnost Dinner - což není dobré.

### <a name="using-partial-view-templates"></a>Použití šablon částečného zobrazení

ASP.NET MVC podporuje možnost definovat šablony "částečné zobrazení", které lze použít k zapouzdření logiky vykreslování zobrazení pro dílčí část stránky. "Částečné" poskytují užitečný způsob, jak definovat logiku vykreslování zobrazení jednou a pak znovu použít na více místech v aplikaci.

Chcete-li pomoci "DRY-up" naše Edit.aspx a Create.aspx zobrazení šablony duplikace, můžeme vytvořit částečné zobrazení šablony s názvem "DinnerForm.ascx", který zapouzdřuje rozložení formuláře a vstupní prvky společné pro oba. Uděláme to tak, že klikneme pravým tlačítkem myši na náš&gt;adresář /Views/Dinners a vybereme příkaz nabídky "Přidat zobrazení":

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

Zobrazí se dialogové okno "Přidat zobrazení". Pojmenujeme nové zobrazení, které chceme vytvořit "DinnerForm", vyberte zaškrtávací políčko "Vytvořit částečné zobrazení" v dialogovém okně a označíme, že mu předáme třídu DinnerFormViewModel:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

Po kliknutí na tlačítko "Přidat" visual studio vytvoří novou šablonu zobrazení "DinnerForm.ascx" pro nás v adresáři "\Views\Dinners".

Poté můžeme zkopírovat/vložit duplicitní rozložení formuláře / vstupní řídicí kód z našich šablon zobrazení Edit.aspx/ Create.aspx do naší nové šablony částečného zobrazení "DinnerForm.ascx":

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Můžeme pak aktualizovat naše upravit a vytvořit zobrazení šablony volat DinnerForm částečnou šablonu a odstranit duplikaci formuláře. Můžeme to provést voláním Html.RenderPartial("DinnerForm") v rámci našich šablon zobrazení:

##### <a name="createaspx"></a>Vytvořit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Můžete explicitně kvalifikovat cestu částečné šablony, kterou chcete při volání Html.RenderPartial (například~ Zobrazení/Večeře/DinnerForm.ascx"). V našem kódu výše však využíváme vzory pojmenování založené na konvencích v rámci ASP.NET MVC a pouze zadejte "DinnerForm" jako název částečného vykreslení. Když to uděláme ASP.NET MVC bude vypadat nejprve v adresáři zobrazení na základě konvence (pro DinnersController by to /Views/Dinners). Pokud nenajde částečnou šablonu tam, pak se na něj podívá v adresáři /Views/Shared.

Při Html.RenderPartial() je volána pouze s názvem částečné zobrazení, ASP.NET MVC předá částečné zobrazení stejné model a ViewData slovníkobjekty používané volající zobrazení šablony. Alternativně existují přetížené verze Html.RenderPartial(), které umožňují předat alternativní model objektu nebo ViewData slovníku pro částečné zobrazení použít. To je užitečné pro scénáře, kde chcete předat pouze podmnožinu úplnémodel/ViewModel.

| **Boční téma: &lt;Proč&gt; % &lt;%&gt;místo %= % ?** |
| --- |
| Jedna z jemných věcí, které jste si možná všimli &lt;s&gt; výše uvedeným &lt;kódem&gt; je, že používáme blok % % namísto bloku %= % při volání html.RenderPartial(). &lt;%=&gt; bloky v ASP.NET označují, že vývojář chce vykreslit zadanou hodnotu (například% &lt;= "Hello" %&gt; by vykreslil "Hello"). &lt;%&gt; bloků místo toho označují, že vývojář chce spustit kód a že všechny vykreslené &lt;výstup v nich musí být&gt;provedeno explicitně (například: % Response.Write("Hello") % . Důvod, proč používáme &lt;&gt; blok % % s naším výše uvedeným kódem Html.RenderPartial, je, že metoda Html.RenderPartial() nevrátí řetězec a místo toho vyvede obsah přímo do výstupního datového proudu šablony volajícího zobrazení. Provádí to z důvodů efektivity výkonu a tím se vyhne nutnosti vytvořit (potenciálně velmi velký) dočasný řetězec objektu. To snižuje využití paměti a zlepšuje celkovou propustnost aplikace. Jednou z běžných chyb při použití Html.RenderPartial() je zapomenout přidat středník na &lt;konci&gt; volání, pokud je v rámci bloku % %. Například tento kód způsobí chybu kompilátoru: &lt;% Html.RenderPartial("DinnerForm") %&gt; Místo toho je třeba napsat: &lt;% Html.RenderPartial("DinnerForm"); %&gt; Důvodem &lt;je, že % %&gt; bloků jsou samostatné příkazy kódu a při použití příkazů kódu jazyka C# je třeba ukončit středníkem. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Použití šablon částečného zobrazení k objasnění kódu

Vytvořili jsme šablonu částečného zobrazení "DinnerForm", abychom zabránili duplikování logiky vykreslování zobrazení na více místech. Toto je nejčastější důvod pro vytvoření šablon částečného zobrazení.

Někdy má stále smysl vytvářet částečné pohledy, i když jsou volány pouze na jednom místě. Velmi složité zobrazení šablony může být často mnohem jednodušší číst, když jejich logika vykreslování zobrazení je extrahována a rozdělena do jedné nebo více dobře pojmenované částečné šablony.

Zvažte například níže uvedený fragment kódu ze souboru Site.master v našem projektu (který se budeme v brzké době zabývat). Kód je relativně přímočarý ke čtení – částečně proto, že logika pro zobrazení odkazu pro přihlášení/odhlášení v pravém horním rohu obrazovky je zapouzdřena v části "LogOnUserControl" částečné:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Kdykoli se ocitnete zmateni, když se snažíte pochopit html / kód značky v rámci view-template, zvažte, zda by nebylo jasnější, kdyby některé z ní byly extrahovány a refaktorovány do dobře pojmenovaných částečných zobrazení.

### <a name="master-pages"></a>Stránky předlohy

Kromě podpory částečných zobrazení podporuje ASP.NET MVC také možnost vytvářet šablony "předlohy", které lze použít k definování společného rozložení a html webu nejvyšší úrovně. Ovládací prvky zástupného symbolu obsahu lze poté přidat na stránku předlohy a identifikovat nahraditelné oblasti, které lze přepsat nebo "vyplnit" zobrazeními. To poskytuje velmi efektivní (a SUCHý) způsob, jak použít společné rozložení v celé aplikaci.

Ve výchozím nastavení mají nové ASP.NET projekty MVC automaticky přidanou šablonu vzorové stránky. Tato stránka předlohy má název Site.master a je umístěna ve složce \Views\Shared\:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

Výchozí soubor Site.master vypadá níže. Definuje vnější html webu, spolu s nabídkou pro navigaci v horní části. Obsahuje dva nahraditelné zástupné ovládací prvky obsahu – jeden pro název a druhý pro kde by měl být nahrazen primární obsah stránky:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

Všechny šablony zobrazení, které jsme vytvořili pro naši aplikaci NerdDinner ("Seznam", "Podrobnosti", "Upravit", "Vytvořit", "Nenalezeno", atd.) byly založeny na této šabloně Site.master. To je indikováno pomocí atributu "MasterPageFile", &lt;který byl&gt; ve výchozím nastavení přidán do horní % @ Page % direktivy při vytváření našich zobrazení pomocí dialogového okna "Přidat zobrazení":

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

To znamená, že můžeme změnit obsah Site.master a změny budou automaticky použity a použity, když vykreslíme některou z našich šablon zobrazení.

Pojďme aktualizovat naše Site.master záhlaví části tak, aby záhlaví naší aplikace je "NerdDinner" místo "My MVC aplikace". Pojďme také aktualizovat naše navigační menu tak, aby první karta je "Najít večeři" (zpracovány HomeController index() metoda akce) a pojďme přidat novou kartu s názvem "Host večeři" (zpracovány DinnersController create() metoda akce):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Když uložíme soubor Site.master a aktualizujeme náš prohlížeč, uvidíme, jak se změny záhlaví zobrazí ve všech zobrazeních v naší aplikaci. Příklad:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

A s *adresou /Dinners/Edit/[id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Další krok

Částečné a vzorové stránky poskytují velmi flexibilní možnosti, které umožňují čistě uspořádat zobrazení. Zjistíte, že vám pomohou vyhnout se duplikaci obsahu/ kódu zobrazení a usnadnit čtení a údržbu šablon zobrazení.

Podívejme se nyní znovu na scénář výpisu, který jsme vytvořili dříve, a povolte podporu škálovatelného stránkování.

> [!div class="step-by-step"]
> [Předchozí](use-viewdata-and-implement-viewmodel-classes.md)
> [další](implement-efficient-data-paging.md)
