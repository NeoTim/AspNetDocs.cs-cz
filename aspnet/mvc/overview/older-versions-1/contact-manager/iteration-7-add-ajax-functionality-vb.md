---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 'Iterace #7 – Přidat funkci Ajax (VB) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: V sedmé iteraci zlepšujeme odezvu a výkon naší aplikace přidáním podpory pro Ajax.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: 04eaaa129a56b765c090e64118ed528c65987b50
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542297"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>Iterace č. 7 – přidání funkcí Ajax (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> V sedmé iteraci zlepšujeme odezvu a výkon naší aplikace přidáním podpory pro Ajax.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Vytvoření aplikace pro správu kontaktů ASP.NET MVC (VB)

V této sérii kurzů vytvoříme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Contact Manager umožňuje ukládat kontaktní informace - jména, telefonní čísla a e-mailové adresy - pro seznam osob.

Vytvoříme aplikaci přes více iterací. S každou iterací postupně vylepšujeme aplikaci. Cílem tohoto přístupu více iterace je umožnit pochopit důvod pro každou změnu.

- Iterace #1 - Vytvořte aplikaci. V první iteraci vytvoříme Správce kontaktů nejjednodušším možným způsobem. Přidáváme podporu pro základní databázové operace: Vytvořit, Číst, Aktualizovat a odstranit (CRUD).

- Iterace #2 - Make aplikace vypadat hezky. V této iteraci vylepšujeme vzhled aplikace úpravou výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů.

- #3 iterace – přidejte ověření formuláře. Ve třetí iteraci přidáme ověření základního formuláře. Bráníme uživatelům v odesílání formuláře bez vyplnění požadovaných polí formuláře. Ověřujeme také e-mailové adresy a telefonní čísla.

- Iterace #4 - Proveďte aplikaci volně spojená. V této čtvrté iteraci využíváme několik vzorů návrhu softwaru, abychom usnadnili údržbu a úpravu aplikace Správce kontaktů. Například refaktorujeme naši aplikaci tak, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 - vytvořit testy částí. V páté iteraci usnadňujeme údržbu a úpravy naší aplikace přidáním testů částí. Zesměšňujeme naše třídy datových modelů a vytváříme testy částí pro naše řadiče a logiku ověřování.

- Iterace #6 – použijte vývoj řízený testem. V této šesté iteraci přidáme nové funkce do naší aplikace zápisem testů částí první a psaní kódu proti testování částí. V této iteraci přidáme skupiny kontaktů.

- Iterace #7 - Přidat funkci Ajax. V sedmé iteraci zlepšujeme odezvu a výkon naší aplikace přidáním podpory pro Ajax.

## <a name="this-iteration"></a>Tato iterace

V této iteraci aplikace Contact Manager refaktorujeme naši aplikaci, abychom využili Ajax. Využitím Ajaxu, děláme naše aplikace citlivější. Můžeme se vyhnout vykreslování celé stránky, když potřebujeme aktualizovat pouze určitou oblast na stránce.

Refaktorujeme zobrazení indexu tak, abychom nemuseli znovu zobrazovat celou stránku, kdykoli někdo vybere novou skupinu kontaktů. Místo toho, když někdo klikne na skupinu kontaktů, aktualizujeme seznam kontaktů a zbytek stránky necháme na pokoji.

Změníme také způsob, jakým náš odkaz na odstranění funguje. Místo zobrazení samostatné potvrzovací stránky zobrazíme potvrzovací dialog JavaScriptu. Pokud potvrdíte, že chcete odstranit kontakt, operace HTTP DELETE se provádí proti serveru odstranit záznam kontaktu z databáze.

Kromě toho budeme využívat jQuery přidat animační efekty do našeho zobrazení indexu. Při načítání nového seznamu kontaktů ze serveru zobrazíme animaci.

Nakonec budeme využívat ASP.NET podporu rámce AJAX pro správu historie prohlížeče. Body historie vytvoříme vždy, když provedeme volání Ajaxu k aktualizaci seznamu kontaktů. Tímto způsobem budou fungovat tlačítka prohlížeče vzad a vpřed.

## <a name="why-use-ajax"></a>Proč použít Ajax?

Použití Ajax má mnoho výhod. Za prvé, přidání funkce Ajax do aplikace má za následek lepší uživatelské zkušenosti. V normální webové aplikaci musí být celá stránka zaúčtována zpět na server pokaždé, když uživatel provede akci. Kdykoli provedete akci, prohlížeč uzamkne a uživatel musí počkat, dokud se načte a znovu zobrazí celá stránka.

To by bylo nepřijatelné zkušenosti v případě desktopové aplikace. Ale tradičně jsme žili s touto špatnou uživatelskou zkušeností v případě webové aplikace, protože jsme nevěděli, že bychom mohli udělat něco lepšího. Mysleli jsme, že je to omezení webových aplikací, když ve skutečnosti to bylo jen omezení naší představivosti.

V aplikaci Ajax, nemusíte přinést uživatelské zkušenosti zastavit jen aktualizovat stránku. Místo toho můžete provést asynchronní požadavek na pozadí aktualizovat stránku. Nenutíte uživatele čekat, zatímco část stránky se aktualizuje.

Využitím Ajax, můžete také zlepšit výkon vaší aplikace. Zvažte, jak aplikace Contact Manager funguje právě teď bez funkce Ajax. Po kliknutí na skupinu kontaktů musí být znovu zobrazeno celé zobrazení rejstříku. Seznam kontaktů a seznam skupin kontaktů musí být načten z databázového serveru. Všechna tato data musí být předána přes drát z webového serveru do webového prohlížeče.

Poté, co přidáme funkce Ajax do naší aplikace, se však můžeme vyhnout opětovnému zobrazení celé stránky, když uživatel klikne na skupinu kontaktů. Už nepotřebujeme, abychom z databáze brali kontaktní skupiny. Také nemusíme tlačit celý index pohled přes drát. Využitím Ajaxu snižujeme množství práce, kterou musí náš databázový server vykonávat, a snižujeme množství síťového provozu vyžadovaného naší aplikací.

## <a name="don-t-be-afraid-of-ajax"></a>Nebojte se Ajaxu

Někteří vývojáři se vyhýbají používání Ajaxu, protože se obávají o prohlížeče nižší úrovně. Chtějí se ujistit, že jejich webové aplikace budou i nadále fungovat při přístupu prohlížeče, který nepodporuje JavaScript. Vzhledem k tomu, Ajax závisí na JavaScriptu, někteří vývojáři se vyhýbají použití Ajax.

Nicméně, pokud jste opatrní, jak implementovat Ajax pak můžete vytvářet aplikace, které pracují s oběma vyšší úrovni a nižší úrovni prohlížečů. Naše aplikace Contact Manager bude pracovat s prohlížeči, které podporují JavaScript a prohlížeče, které nemají.

Pokud používáte aplikaci Contact Manager s prohlížečem, který podporuje JavaScript, pak budete mít lepší uživatelské prostředí. Pokud například klepnete na skupinu kontaktů, bude aktualizována pouze oblast stránky, která zobrazuje kontakty.

Pokud na druhou stranu používáte aplikaci Contact Manager s prohlížečem, který nepodporuje JavaScript (nebo který má vypnutý JavaScript), pak budete mít o něco méně žádoucí uživatelské zkušenosti. Pokud například klepnete na skupinu kontaktů, musí být celé zobrazení rejstříku zaúčtováno zpět do prohlížeče, aby se zobrazil odpovídající seznam kontaktů.

## <a name="adding-the-required-javascript-files"></a>Přidání požadovaných souborů JavaScriptu

Budeme muset použít tři soubory JavaScript přidat Ajax funkce do naší aplikace. Všechny tři tyto soubory jsou zahrnuty do složky Skripty nové aplikace ASP.NET MVC.

Pokud máte v plánu použít Ajax ve více stránkách ve vaší aplikaci, pak má smysl zahrnout požadované soubory JavaScript u vaší aplikace s zobrazení stránky předlohy. Tímto způsobem budou soubory JavaScriptu automaticky zahrnuty do všech stránek ve vaší aplikaci.

Přidejte následující javascript, &lt;&gt; který obsahuje, do značky hlavy stránky předlohy zobrazení:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Refaktoring zobrazení indexu používat Ajax

Umožňuje začít úpravou zobrazení rejstříku tak, aby kliknutí na skupinu kontaktů pouze aktualizuje oblast zobrazení, které zobrazuje kontakty. Červené pole na obrázku 1 obsahuje oblast, kterou chceme aktualizovat.

[![Aktualizace pouze kontaktů](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**Obrázek 01**: Aktualizace pouze[kontaktů(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-7-add-ajax-functionality-vb/_static/image2.png)

Prvním krokem je oddělit část zobrazení, které chceme aktualizovat asynchronně do samostatné částečné (zobrazit uživatelský ovládací prvek). Část zobrazení Rejstřík, která zobrazuje tabulku kontaktů, byla přesunuta do části Částečné v seznamu 1.

**Výpis 1 - Zobrazení\Kontakt\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

Všimněte si, že částečné v Listing 1 má jiný model než zobrazení indexu. Atribut *Inherits* ve &lt;směrnici %@ Page %&gt; určuje, že částečné&lt;dědí z třídy ViewUserControl Group.&gt;

Aktualizované zobrazení indexu je obsaženo v seznamu 2.

**Výpis 2 - Zobrazení\Kontakt\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

Existují dvě věci, které byste si měli všimnout aktualizovaného zobrazení v seznamu 2. Nejprve všimněte si, že veškerý obsah přesunutdo částečné je nahrazen volání Html.RenderPartial(). Metoda Html.RenderPartial() je volána při prvním požadavku na zobrazení indexu za účelem zobrazení počáteční sady kontaktů.

Za druhé, všimněte si, že Html.ActionLink() slouží k zobrazení skupiny kontaktů byl nahrazen Ajax.ActionLink(). Ajax.ActionLink() se nazývá s následujícími parametry:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

První parametr představuje text, který se má zobrazit pro propojení, druhý parametr představuje hodnoty trasy a třetí parametr představuje možnosti Ajax. V tomto případě použijeme UpdateTargetId Ajax možnost &lt;přejděte na značku HTML div,&gt; které chceme aktualizovat po dokončení požadavku Ajax. Chceme aktualizovat &lt;značku&gt; div s novým seznamem kontaktů.

Aktualizovaná metoda Index() řadiče kontaktu je obsažena v výpisu 3.

**Výpis 3 - Řadiče\ContactController.vb (Metoda indexu)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

Aktualizovaná akce Index() podmíněně vrátí jednu ze dvou věcí. Pokud index() akce je vyvolána požadavek Ajax pak řadič vrátí částečné. V opačném případě vrátí akce Index() celé zobrazení.

Všimněte si, že akce Index() není nutné vrátit tolik dat při vyvolání požadavek Ajax. V kontextu normálního požadavku vrátí akce Index seznam všech skupin kontaktů a vybrané skupiny kontaktů. V kontextu požadavku Ajax akce Index() vrátí pouze vybranou skupinu. Ajax znamená méně práce na databázovém serveru.

Naše upravené zobrazení indexu funguje v případě prohlížečů vyšší i nižší úrovně. Pokud klepnete na skupinu kontaktů a prohlížeč podporuje JavaScript, aktualizuje se pouze oblast zobrazení, která obsahuje seznam kontaktů. Pokud na druhou stranu váš prohlížeč nepodporuje JavaScript, bude aktualizováno celé zobrazení.

Naše aktualizované zobrazení indexu má jeden problém. Když kliknete na skupinu kontaktů, vybraná skupina se nezvýrazní. Vzhledem k tomu, že seznam skupin se zobrazí mimo oblast, která je aktualizována během požadavku Ajax, správná skupina není zvýrazněna. Tento problém vyřešíme v další části.

## <a name="adding-jquery-animation-effects"></a>Přidání animačních efektů jQuery

Za normálních okolností, když klepnete na odkaz na webové stránce, můžete pomocí indikátoru průběhu prohlížeče zjistit, zda prohlížeč aktivně načítá aktualizovaný obsah. Při provádění požadavku Ajax, na druhé straně indikátor průběhu prohlížeče nezobrazuje žádný pokrok. To může uživatele znervóznit. Jak víte, zda prohlížeč zamrzl?

Existuje několik způsobů, které můžete uživateli označit, že práce se provádí při provádění požadavku Ajax. Jedním z přístupů je zobrazení jednoduché animace. Můžete například zeslabit oblast, když začne a zmizí požadavek Ajax v oblasti po dokončení požadavku.

Budeme používat knihovnu jQuery, která je součástí microsoft ASP.NET MVC framework, k vytvoření animačních efektů. Aktualizované zobrazení indexu je obsaženo v seznamu 4.

**Výpis 4 - Zobrazení\Kontakt\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

Všimněte si, že aktualizované zobrazení indexu obsahuje tři nové funkce jazyka JavaScript. První dvě funkce používají jQuery k zeslabování a zeslábnutí v seznamu kontaktů, když kliknete na novou skupinu kontaktů. Třetí funkce zobrazí chybovou zprávu, když výsledkem požadavku Ajax dojde k chybě (například časový mat v síti).

První funkce se také stará o zvýraznění vybrané skupiny. Class = vybraný atribut je přidán do nadřazeného prvku (elementU LI) prvku, na který jste klepnuli. Opět platí, že jQuery usnadňuje výběr správného prvku a přidat třídu CSS.

Tyto skripty jsou vázány na odkazy skupiny pomocí Ajax.ActionLink() AjaxOptions parametr. Aktualizované Ajax.ActionLink() volání metody vypadá takto:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Přidání podpory historie prohlížeče

Za normálních okolností, když kliknete na odkaz aktualizovat stránku, historie prohlížeče se aktualizuje. Tímto způsobem můžete kliknout na tlačítko Zpět v prohlížeči a přesunout se zpět v čase do předchozího stavu stránky. Pokud například kliknete na skupinu kontaktů Přátelé a potom kliknete na skupinu obchodních kontaktů, můžete klepnutím na tlačítko Zpět v prohlížeči přejít zpět do stavu stránky, když byla vybrána skupina kontaktů Přátelé.

Bohužel provedení požadavku Ajax neaktualizuje historii prohlížeče automaticky. Pokud kliknete na skupinu kontaktů a seznam odpovídajících kontaktů se načte s požadavkem Ajax, historie prohlížeče se neaktualizuje. Tlačítko Zpět v prohlížeči nelze použít k přechodu zpět do skupiny kontaktů po výběru nové skupiny kontaktů.

Pokud chcete, aby uživatelé mohli používat tlačítko Zpět v prohlížeči po provedení požadavků Ajax, musíte provést trochu více práce. Musíte využít funkce správy historie prohlížeče integrované v ASP.NET AJAX Framework.

ASP.NET historii prohlížeče AJAX, musíte udělat tři věci:

1. Povolte historii prohlížeče nastavením vlastnosti enableBrowserHistory na hodnotu true.
2. Uložit body historie při změně stavu zobrazení voláním metody addHistoryPoint().
3. Rekonstruujte stav zobrazení při vyvolání události navigate.

Aktualizované zobrazení indexu je obsaženo v seznamu 5.

**Výpis 5 - Zobrazení\Kontakt\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

V výpisu 5 je ve funkci pageInit() povolena historie prohlížeče. PageInit() Funkce se také používá k nastavení obslužné rutiny události pro navigate události. Přejít událost je aktivována vždy, když prohlížeč vpřed nebo zpět tlačítko způsobí změnu stavu stránky.

Metoda beginContactList() je volána po klepnutí na skupinu kontaktů. Tato metoda vytvoří nový bod historie voláním metody addHistoryPoint(). Id kliknuté skupiny kontaktů je přidáno do historie.

ID skupiny je načteno z atributu expando na odkazu skupiny kontaktů. Odkaz je vykreslen s následujícím voláním Ajax.ActionLink().

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

Poslední parametr předaný Ajax.ActionLink() přidá expando atribut s názvem groupid k odkazu (malá písmena pro kompatibilitu XHTML).

Když uživatel stiskne tlačítko Zpět nebo Vpřed v prohlížeči, je vyvolána událost navigate a volá se metoda navigate(). Tato metoda aktualizuje kontakty zobrazené na stránce tak, aby odpovídaly stavu stránky, která odpovídá bodu historie prohlížeče předané metodě navigace.

## <a name="performing-ajax-deletes"></a>Provedení Ajax odstraní

V současné době, aby bylo možné odstranit kontakt, musíte kliknout na odkaz Odstranit a poté kliknout na tlačítko Odstranit zobrazené na stránce potvrzení odstranění (viz obrázek 2). To vypadá jako mnoho žádostí o stránku udělat něco jednoduchého, jako je odstranění záznamu databáze.

[![Stránka potvrzení odstranění](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**Obrázek 02**: Stránka potvrzení odstranění[(Kliknutím zobrazíte obrázek v plné velikosti)](iteration-7-add-ajax-functionality-vb/_static/image4.png)

Je lákavé přeskočit stránku potvrzení odstranění a odstranit kontakt přímo ze zobrazení rejstříku. Měli byste se tomuto pokušení vyhnout, protože tento přístup otevírá vaši aplikaci do bezpečnostních děr. Obecně nechcete provádět operaci HTTP GET při vyvolání akce, která upravuje stav webové aplikace. Při provádění odstranění chcete provést operaci HTTP POST nebo ještě lépe operaci HTTP DELETE.

Odkaz Odstranit je obsažen v částečném seznamu contactlist. Aktualizovaná verze částečnécontactlist je obsažena v výpisu 6.

**Výpis 6 - Zobrazení\Kontakt\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

Odkaz Delete je vykreslen s následujícím voláním metody Ajax.ImageActionLink():

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink() není standardní součástí rozhraní ASP.NET MVC. Ajax.ImageActionLink() je vlastní pomocné metody zahrnuté v projektu Správce kontaktů.

Parametr AjaxOptions má dvě vlastnosti. Nejprve se k zobrazení dialogového okna pro potvrzení vyskakovacího javascriptu použije vlastnost Confirm. Za druhé, HttpMethod vlastnost se používá k provedení operace HTTP DELETE.

Výpis 7 obsahuje novou akci AjaxDelete(), která byla přidána do kontroleru kontaktů.

**Výpis 7 - Controllers\ContactController.vb (AjaxDelete)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

Akce AjaxDelete() je dekorována atributem AcceptVerbs. Tento atribut zabrání vyvolání akce s výjimkou jakékoli jiné operace HTTP než operace HTTP DELETE. Zejména nelze vyvolat tuto akci s HTTP GET.

Po odstranění záznamu databáze je třeba zobrazit aktualizovaný seznam kontaktů, který odstraněný záznam neobsahuje. Metoda AjaxDelete() vrátí částečné contactlist a aktualizovaný seznam kontaktů.

## <a name="summary"></a>Souhrn

V této iteraci jsme přidali funkce Ajax do naší aplikace Contact Manager. Použili jsme Ajax ke zlepšení odezvy a výkonu naší aplikace.

Nejprve jsme refaktorovali zobrazení rejstříku tak, aby kliknutí na skupinu kontaktů neaktualizovalo celé zobrazení. Místo toho kliknutím na skupinu kontaktů aktualizujete pouze seznam kontaktů.

Dále jsme použili jQuery animační efekty vyblednout a slábnout v seznamu kontaktů. Přidání animace do aplikace Ajax lze poskytnout uživatelům aplikace s ekvivalentem indikátoru průběhu prohlížeče.

Do naší aplikace Ajax jsme také přidali podporu historie prohlížeče. Povolili jsme uživatelům kliknout na tlačítka Zpět a Vpřed prohlížeče a změnit tak stav zobrazení rejstříku.

Nakonec jsme vytvořili odkaz na odstranění, který podporuje operace HTTP DELETE. Provedením Ajax odstraní, umožňujeme uživatelům odstranit záznamy databáze bez nutnosti uživatel požadovat další odstranění potvrzení stránky.

> [!div class="step-by-step"]
> [Předchozí](iteration-6-use-test-driven-development-vb.md)
