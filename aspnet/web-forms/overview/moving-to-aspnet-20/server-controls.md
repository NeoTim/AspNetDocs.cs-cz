---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Serverové ovládací prvky | Dokumenty společnosti Microsoft
author: rick-anderson
description: ASP.NET 2.0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu se podíváme na některé architektonické změny ve způsobu, jakým ASP.NET 2.0 a Visual Studio 200...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543740"
---
# <a name="server-controls"></a>Serverové ovládací prvky

podle [společnosti Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu pokryjeme některé architektonické změny ve způsobu, jakým ASP.NET 2.0 a Visual Studio 2005 řeší serverové ovládací prvky.

ASP.NET 2.0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu pokryjeme některé architektonické změny ve způsobu, jakým ASP.NET 2.0 a Visual Studio 2005 řeší serverové ovládací prvky.

## <a name="view-state"></a>Zobrazit stav

Primární změnou stavu zobrazení v ASP.NET 2.0 je dramatické zmenšení velikosti. Zvažte stránku, na které je pouze ovládací prvek Kalendář. Zde je stav zobrazení v ASP.NET 1.1.

[!code-css[Main](server-controls/samples/sample1.css)]

Nyní je zde stav zobrazení na stejné stránce v ASP.NET 2.0.

[!code-css[Main](server-controls/samples/sample2.css)]

To je docela významná změna, a vzhledem k tomu, že stav zobrazení se provádí tam a zpět přes drát, tato změna může dát vývojářům významné zvýšení výkonu. Zmenšení velikosti stavu zobrazení je do značné míry způsobeno způsobem, jakým s ním zacházíme interně. Nezapomeňte, že stav zobrazení je řetězec kódovaný base64. Chcete-li lépe porozumět změně stavu zobrazení v ASP.NET 2.0, podívejme se na dekódované hodnoty z výše uvedených příkladů.

Zde je 1,1 zobrazení stavu dekódovat:

[!code-css[Main](server-controls/samples/sample3.css)]

To může vypadat trochu jako blábol, ale je zde vzor. V ASP.NET 1.x jsme použili jednotlivé znaky k identifikaci &lt; &gt; datových typů a oddělených hodnot pomocí znaků. "t" ve výše uvedeném vzorku stavu zobrazení představuje trojčata. Trojčata obsahuje dvojici ArrayLists ("l" představuje ArrayList.) Jeden z těchto ArrayLists obsahuje Int32 ("i") s hodnotou 1 a druhý obsahuje další Trojčata. Trojčata obsahuje dvojici ArrayLists, atd. Důležité mít na paměti, je, že používáme trojčata, které obsahují dvojice, identifikujeme datové typy prostřednictvím dopisu a používáme znaky &lt; a &gt; jako oddělovače.

V ASP.NET 2.0 vypadá dekódovaný stav zobrazení trochu jinak.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Měli byste si všimnout obrovské změny ve vzhledu stavu dekódovaného zobrazení. Tato změna má několik architektonických základů. Stav zobrazení v ASP.NET 1.x používá LosFormatter serializovat data. V 2.0 používáme novou třídu ObjectStateFormatter. Tato třída byla speciálně navržena pro podporu serializace a deserializace stavu zobrazení a stavu řízení. (Stav řízení bude popsán v další části.) Existuje mnoho výhod získaných změnou metody, kterou serializace a deserializace probíhat. Jedním z nejdramatičtějších je skutečnost, že na rozdíl od LosFormatter, který používá TextWriter, ObjectStateFormatter používá BinaryWriter. To umožňuje ASP.NET 2.0 uložit stav zobrazení řady bajtů namísto řetězců. Vezměte si například celé číslo. V ASP.NET 1.1 vyžadovalo celé číslo stav zobrazení 4 bajty. V ASP.NET 2.0, stejné celé číslo vyžaduje pouze 1 bajt. Další vylepšení byly provedeny ke snížení množství stavu zobrazení, který je uložen. DateTime hodnoty, například jsou nyní uloženy pomocí TickCount místo řetězce.

Jako by to všechno nestačilo, zvláštní pozornost byla věnována skutečnosti, že jedním z největších spotřebitelů stavu zobrazení v 1.x byl DataGrid a podobné ovládací prvky. Hlavní nevýhodou ovládacích prvků, jako je například DataGrid, kde se týká stav zobrazení je, že často obsahuje velké množství opakovaných informací. V ASP.NET 1.x, že opakované informace byly jednoduše uloženy znovu a znovu za následek nafouklý stav zobrazení. V ASP.NET 2.0 používáme novou třídu IndexedString k ukládání těchto dat. Pokud se řetězec opakuje, uložíme token pro IndexedString a index v rámci spuštěné tabulky objektů IndexedString.

## <a name="control-state"></a>Stav ovládacího prvku

Jedním z hlavních uzlů, které vývojáři měli se stavem zobrazení, byla velikost, kterou přidal do datové části protokolu HTTP. Jak již bylo zmíněno, jedním z největších spotřebitelů stavu zobrazení je ovládací prvek DataGrid. Chcete-li se vyhnout obrovské množství stavu zobrazení generované DataGrid, mnoho vývojářů jednoduše zakázánstav zobrazení pro tento ovládací prvek. Bohužel, toto řešení nebylo vždy dobré. Stav zobrazení v ASP.NET 1.x obsahuje nejen data nezbytná pro správnou funkci ovládacího prvku. Obsahuje také informace týkající se stavu ovládacího prvku. To znamená, že pokud chcete povolit stránkování na DataGrid, musíte povolit stav zobrazení i v případě, že nepotřebujete všechny informace uživatelského panelu, které obsahuje stav zobrazení. Je to scénář "všechno nebo nic".

V ASP.NET 2.0, kontrolní stav řeší tento problém pěkně zavedením kontrolního stavu. Stav ovládacího prvku obsahuje data, která jsou nezbytně nutná pro správnou funkci ovládacího prvku. Na rozdíl od stavu zobrazení nelze zakázat stav ovládacího prvku. Proto je důležité, aby data ukládajících se ve stavu řízení je pečlivě kontrolována.

> [!NOTE]
> Stav ovládacího prvku je trvalý spolu \_ \_se stavem zobrazení v poli skrytý formulář VIEWSTATE.

Toto video je návod emituje stav zobrazení a stav ovládacího prvku.

![](server-controls/_static/image1.png)

[Otevřít video na celou obrazovku](server-controls/_static/state1.wmv)

Aby serverový ovládací prvek číst a zapisovat do stavu řízení, je nutné provést tři kroky.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>Krok 1: Volání metody RegisterRequiresControlState

Metoda RegisterRequiresControlState informuje ASP.NET, že ovládací prvek potřebuje zachovat stav ovládacího prvku. Trvá jeden argument typu Control, který je ovládací prvek, který je registrován.

Je důležité si uvědomit, že registrace nepřetrvává od požadavku na požadavek. Proto tato metoda musí být volána na každý požadavek, pokud ovládací prvek má zachovat stav ovládacího prvku. Doporučuje se, aby metoda byla volána v OnInit.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>Krok 2: Přepsat SaveControlState

Metoda SaveControlState ukládá změny stavu ovládacího prvku pro ovládací prvek od posledního příspěvku zpět. Vrátí objekt představující stav ovládacího prvku.

## <a name="step-3-override-loadcontrolstate"></a>Krok 3: Přepsat LoadControlState

Metoda LoadControlState načte uložený stav do ovládacího prvku. Metoda trvá jeden argument typu Object, který obsahuje uložený stav pro ovládací prvek.

## <a name="full-xhtml-compliance"></a>Úplná shoda s XHTML

Každý vývojář webu zná důležitost standardů ve webových aplikacích. Za účelem zachování vývojového prostředí založeného na standardech je ASP.NET 2.0 plně kompatibilní s XHTML. Proto jsou všechny značky vykresleny podle standardů XHTML v prohlížečích, které podporují HTML 4.0 nebo vyšší.

Definice doctype v ASP.NET 1.1 byla následující:

[!code-html[Main](server-controls/samples/sample6.html)]

Ve ASP.NET 2.0 je výchozí definice DOCTYPE následující:

[!code-html[Main](server-controls/samples/sample7.html)]

Pokud se rozhodnete, můžete změnit výchozí kompatibilitu XHTML prostřednictvím uzlu xhtmlConformance v konfiguračním souboru. Například následující uzel v souboru web.config změní kompatibilitu XHTML na XHTML 1.0 Strict:

[!code-xml[Main](server-controls/samples/sample8.xml)]

Pokud se rozhodnete, můžete také nakonfigurovat ASP.NET tak, aby používalstarší konfiguraci použitou v ASP.NET 1.x následujícím způsobem:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Adaptivní vykreslování pomocí adaptérů

V ASP.NET 1.x obsahoval konfigurační soubor oddíl &lt;BrowserCaps,&gt; který naplnil objekt HttpBrowserCapabilities. Tento objekt umožnil vývojáři určit, které zařízení provádí konkrétní požadavek a vykreslit kód odpovídajícím způsobem. V ASP.NET 2.0 se model zlepšil a nyní používá novou třídu ControlAdapter. Třída ControlAdapter přepíše události v životním cyklu ovládacího prvku a řídí vykreslování ovládacích prvků na základě možností uživatelského agenta. Možnosti konkrétního uživatelského agenta jsou definovány souborem definice prohlížeče (souborem s příponou .browser file) uloženým v c:\windows\microsoft.net\framework\v2.0. \* \* \*\CONFIG\Browsers. \*

> [!NOTE]
> ControlAdapter Třída je abstraktní třídy.

Podobně jako &lt;v&gt; části browserCaps v 1.x používá soubor definice prohlížeče regulární výraz k analýzě řetězce uživatelského agenta za účelem identifikace prohlížeče, který o to žádá. Je definuje konkrétní možnosti pro daného agenta uživatele. ControlAdapter vykreslí ovládací prvek prostřednictvím render metoda. Proto pokud přepíšete Render metoda, neměli byste volat Render na základní třídy. To může způsobit vykreslování dojít dvakrát, jednou pro adaptér a jednou pro samotný ovládací prvek.

## <a name="developing-a-custom-adapter"></a>Vývoj vlastního adaptéru

Můžete vytvořit vlastní adaptér děděním z ControlAdapter. Kromě toho můžete dědit z abstraktní třídy PageAdapter v případech, kdy je potřeba adaptér pro stránku. Mapování ovládacích prvků na vlastní adaptér &lt;se&gt; provádí prostřednictvím elementu controlAdapters v souboru definice prohlížeče. Například následující XML z definičního souboru prohlížeče mapuje ovládací prvek Menu na třídu MenuAdapter:

[!code-html[Main](server-controls/samples/sample10.html)]

Pomocí tohoto modelu je pro vývojáře ovládacího prvku poměrně snadné cílit na konkrétní zařízení nebo prohlížeč. Je to také docela jednoduché pro vývojáře mít úplnou kontrolu nad tím, jak stránky vykreslit na každém zařízení.

## <a name="per-device-rendering"></a>Vykreslování podle zařízení

Vlastnosti řízení serveru v ASP.NET 2.0 lze zadat pro jedno zařízení pomocí předpony specifické pro prohlížeč. Níže uvedený kód například změní text popisku v závislosti na tom, které zařízení se používá k procházení stránky.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Při procházení stránky obsahující tento popisek z aplikace Internet Explorer se na štítku zobrazí text "Procházíte z aplikace Internet Explorer". Při procházení stránky z Firefoxu se na štítku zobrazí text "Procházíte z Firefoxu". Při procházení stránky z jiného zařízení se zobrazí "Procházíte z neznámého zařízení". Libovolnou vlastnost lze zadat pomocí této speciální syntaxe.

## <a name="setting-focus"></a>Nastavení fokusu

ASP.NET vývojáři 1.x často dotázáni, jak nastavit počáteční zaměření na konkrétní ovládací prvek. Například na přihlašovací stránce je užitečné, aby textové pole ID uživatele získalo fokus při prvním načtení stránky. V ASP.NET 1.x, to vyžaduje psaní některých skriptů na straně klienta. I když takový skript je triviální úkol, je to již není nutné v ASP.NET 2.0 díky SetFocus metody. SetFocus Metoda trvá jeden argument označující ovládací prvek, který by měl získat fokus. Tento argument může být id klienta ovládacího prvku jako řetězec nebo název ovládacího prvku Server jako objekt Control. Chcete-li například nastavit počáteční fokus na ovládací prvek TextBox s názvem txtUserID při prvním načtení stránky, přidejte do načtení stránky\_následující kód:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-- nebo

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 používá obslužnou rutinu Webresource.axd (již bylo popsáno dříve) k vykreslení funkce na straně klienta, která nastavuje fokus. Název funkce na straně klienta\_je Automatické zaostření webového formuláře, jak je znázorněno zde:

[!code-html[Main](server-controls/samples/sample14.html)]

Alternativně můžete použít Focus metoda pro ovládací prvek nastavit počáteční fokus na tento ovládací prvek. Focus Metoda je odvozena z Control třídy a je k dispozici pro všechny ASP.NET ovládací prvky 2.0. Je také možné nastavit fokus na konkrétní ovládací prvek, když dojde k chybě ověření. To bude pokryto pozdějším modulem.

## <a name="new-server-controls-in-aspnet-20"></a>Nové serverové ovládací prvky v ASP.NET 2.0

Následují nové serverové ovládací prvky v ASP.NET 2.0. Budeme se podrobněji podrobněji zabývat některými z nich v pozdějších modulech.

## <a name="imagemap-control"></a>Ovládací prvek ImageMap

Ovládací prvek ImageMap umožňuje přidat aktivní oblasti do obrazu, který může spustit příspěvek zpět nebo přejít na adresu URL. K dispozici jsou tři typy hotspotů; CircleHotSpot, RectangleHotSpot a PolygonHotSpot. Aktivní oblasti se přidávají prostřednictvím editoru kolekce v sadě Visual Studio nebo programově v kódu. Pro kreslení aktivních oblastí v obraze není k dispozici žádné uživatelské rozhraní. Souřadnice a velikost nebo poloměr aktivní hospořitelně musí být specifikovány deklarativně. V návrháři také neexistuje vizuální reprezentace hotspotu. Pokud je aktivní oblast nakonfigurována pro přechod na adresu URL, je adresa URL určena prostřednictvím vlastnosti NavigateUrl aktivního bodu. V případě post back hotspot, PostBackValue vlastnost umožňuje předat řetězec v post zpět, které lze načíst v kódu na straně serveru.

![Editor kolekce HotSpot v sadě Visual Studio](server-controls/_static/image1.jpg)

**Obrázek 1**: Editor kolekce HotSpot v sadě Visual Studio

## <a name="bulletedlist-control"></a>Ovládací prvek BulletedList

Ovládací prvek BulletedList je seznam s odrážkami, který může být snadno vázán na data. Seznam lze objednat (číslované) nebo neuspořádané prostřednictvím BulletStyle vlastnost. Každá položka v seznamu je reprezentována objektem ListItem.

![Ovládací prvek BulletedList v sadě Visual Studio](server-controls/_static/image1.gif)

**Obrázek 2**: Ovládací prvek BulletedList v sadě Visual Studio

## <a name="hiddenfield-control"></a>Ovládací prvek HiddenField

Ovládací prvek HiddenField přidá na stránku skryté pole formuláře, jehož hodnota je k dispozici v kódu na straně serveru. Obecně se očekává, že hodnota skrytého pole formuláře zůstane mezi zavěšeními příspěvku beze změny. Je však možné, aby uživatel se zlými úmysly změnil hodnotu před odesláním zpět. Pokud k tomu dojde, ovládací prvek HiddenField vyvolá ValueChanged událost. Pokud máte citlivé informace v Ovládací prvek HiddenField a chcete zajistit, že zůstane beze změny, měli byste zpracovat ValueChanged událost v kódu.

## <a name="fileupload-control"></a>Ovládací prvek FileUpload

Ovládací prvek FileUpload v ASP.NET 2.0 umožňuje nahrávat soubory na webový server prostřednictvím stránky ASP.NET. Tento ovládací prvek je velmi podobný ASP.NET třídy 1.x HtmlInputFile s několika výjimkami. V ASP.NET 1.x bylo doporučeno, aby vlastnost PostedFile byla zkontrolována na hodnotu null, aby bylo možné zjistit, zda jste měli dobrý soubor. Ovládací prvek FileUpload v ASP.NET 2.0 přidá novou vlastnost HasFile, kterou můžete použít ke stejnému účelu a je to o něco efektivnější.

Vlastnost PostedFile je stále k dispozici pro přístup k objektu HttpPostedFile, ale některé funkce Souboru HttpPostedFile je nyní k dispozici vnitřně s ovládacím prvkem FileUpload. Chcete-li například uložit nahraný soubor v ASP.NET 1.x, zavolejte metodu SaveAs na objektU HttpPostedFile. Pomocí FileUpload ovládacíprvek v ASP.NET 2.0, byste volat SaveAs metoda na FileUpload ovládacího prvku samotného.

Další významnou změnou v chování 2.0 (a pravděpodobně nejvýznamnější změnou) je, že již není nutné načíst celý nahraný soubor do paměti před uložením. V 1.x, každý soubor, který byl nahrán je uložen zcela do paměti před zápisem na disk. Tato architektura zabraňuje odesílání velkých souborů.

V ASP.NET 2.0, requestLengthDiskThreshold atribut httpRuntime element umožňuje nakonfigurovat, kolik kilobajtů jsou uloženy ve vyrovnávací paměti před zápisem na disk.

**DŮLEŽITÉ:** Dokumentace MSDN (a dokumentace jinde) určuje, že tato hodnota je v bajtech (ne kilobajtů) a že výchozí hodnota je 256. Hodnota je ve skutečnosti zadána v kilobajtech a výchozí hodnota je 80. Tím, že výchozí hodnotu 80 kM, zajistíme, že vyrovnávací paměť neskončí na haldě velkého objektu.

## <a name="wizard-control"></a>Ovládací prvek Průvodce

Je poměrně běžné setkat se s ASP.NET vývojáři zápasí s pokusem o shromažďování informací v sérii "stránek" pomocí panelů nebo přenosem ze stránky na stránku. Více často než ne, úsilí je frustrující jeden a je časově náročné. Nový ovládací prvek Průvodce řeší problémy povolením lineárních a nelineárních kroků v rozhraní průvodce, které uživatelé znají. Ovládací prvek Průvodce představuje vstupní formuláře v řadě kroků. Každý krok je určitého typu určeného vlastností StepType ovládacího prvku. Dostupné typy kroků jsou následující:

| **Typ kroku** | **Vysvětlení** |
| --- | --- |
| Auto | Průvodce automaticky určí typ kroku na základě jeho umístění v hierarchii kroků. |
| Spustit | První krok, často používaný k prezentaci úvodního prohlášení. |
| Krok | Normální krok. |
| Dokončit | Poslední krok, obvykle slouží k prezentaci tlačítka k dokončení průvodce. |
| Dokončit | Zobrazí zprávu s dělající úspěch nebo neúspěch. |

> [!NOTE]
> Ovládací prvek Průvodce udržuje informace o stavu pomocí stavu ovládacího prvku ASP.NET. Proto EnableViewState vlastnost může být nastavena na false bez jakékoli újmy.

Toto video je návod emagwizard ovládacího prvku.

![](server-controls/_static/image2.png)

[Otevřít video na celou obrazovku](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Lokalizovat ovládací prvek

Ovládací prvek Localize je podobný literální ovládací prvek. Ovládací prvek Localize má však **Mode** vlastnost, která řídí, jak je vykreslen značky, které jsou přidány do něj. Vlastnost Mode podporuje následující hodnoty:

| **Mode** | **Vysvětlení** |
| --- | --- |
| Transformace | Značky se transformují podle protokolu prohlížeče, který požadavek podává. |
| Passthrough | Označení je vykresleno tak, jak je. |
| Kódování | Značky, které jsou přidány do ovládacího prvku, jsou kódovány pomocí htmlEncode. |

## <a name="multiview-and-view-controls"></a>Ovládací prvky MultiView a Zobrazení

Ovládací prvek MultiView funguje jako kontejner pro ovládací prvky View a ovládací prvek View funguje jako kontejner (podobně jako ovládací prvek Panel) pro jiné ovládací prvky. Každé zobrazení v ovládacím prvku MultiView je reprezentováno jedním ovládacím prvkem zobrazení. První ovládací prvek Zobrazení v MultiView je zobrazení 0, druhý je zobrazení 1, atd. Zobrazení můžete přepínat zadáním activeviewindex ovládacího prvku MultiView.

## <a name="substitution-control"></a>Řízení substituce

Substituční řízení se používá ve spojení s ukládáním do mezipaměti ASP.NET. V případech, kdy chcete využít výhod ukládání do mezipaměti, ale máte části stránky, které musí být aktualizovány na každý požadavek (jinými slovy části stránky, které jsou osvobozeny od ukládání do mezipaměti), substituční komponenta poskytuje skvělé řešení. Ovládací prvek není ve skutečnosti vykreslen žádný výstup na jeho vlastní. Místo toho je vázán na metodu v kódu na straně serveru. Když je stránka požadována, je volána metoda a vrácená značka je vykreslena místo substitučního ovládacího prvku.

Metoda, ke které je vázán substituční ovládací prvek je určen prostřednictvím **MethodName** vlastnost. Tato metoda musí splňovat tato kritéria:

- Musí se jednat o statickou (sdílenou v VB) metodu.
- Přijímá jeden parametr typu HttpContext.
- Vrátí řetězec představující značky, které by měly nahradit ovládací prvek na stránce.

Substituční ovládací prvek nemá možnost upravit jakýkoli jiný ovládací prvek na stránce, ale má přístup k aktuálníhttpContext prostřednictvím jeho parametru.

## <a name="gridview-control"></a>Ovládací prvek GridView

Ovládací prvek GridView je náhradou ovládacího prvku DataGrid. Tento ovládací prvek bude podrobněji popsán v pozdějším modulu.

## <a name="detailsview-control"></a>Ovládací prvek DetailsView

Ovládací prvek DetailsView umožňuje zobrazit jeden záznam ze zdroje dat a upravit nebo odstranit. Podrobněji se jedná o pozdější modul.

## <a name="formview-control"></a>Ovládací prvek FormView

Ovládací prvek FormView se používá k zobrazení jednoho záznamu ze zdroje dat v konfigurovatelném rozhraní. Podrobněji se jedná o pozdější modul.

## <a name="accessdatasource-control"></a>Ovládací prvek AccessDataSource

Ovládací prvek AccessDataSource se používá k vytvoření datové vazby databáze aplikace Access. Podrobněji se jedná o pozdější modul.

## <a name="objectdatasource-control"></a>Ovládací prvek ObjectDataSource

Ovládací prvek ObjectDataSource se používá k podpoře třívrstvé architektury, takže ovládací prvky mohou být vázány na obchodní objekt střední vrstvy na rozdíl od dvouvrstvého modelu, kde jsou ovládací prvky vázány přímo na zdroj dat. Podrobněji se o tom bude diskutovat v pozdějším modulu.

## <a name="xmldatasource-control"></a>Ovládací prvek XmlDataSource

Ovládací prvek XmlDataSource se používá k vytvoření datové vazby na zdroj dat XML. Podrobněji se jedná o pozdější modul.

## <a name="sitemapdatasource-control"></a>Ovládací prvek SiteMapDataSource

Ovládací prvek SiteMapDataSource poskytuje datovou vazbu pro ovládací prvky navigace na webu založené na mapě webu. Podrobněji se o tom bude diskutovat v pozdějším modulu.

## <a name="sitemappath-control"></a>Ovládací prvek SiteMapPath

Ovládací prvek SiteMapPath zobrazuje řadu navigačních odkazů běžně označovaných jako popis cesty. Podrobněji se jedná o pozdější modul.

## <a name="menu-control"></a>Ovládací prvek nabídky

Ovládací prvek Nabídka zobrazuje dynamické nabídky pomocí DHTML. Podrobněji se jedná o pozdější modul.

## <a name="treeview-control"></a>TreeView – ovládací prvek

TreeView ovládací prvek se používá k zobrazení hierarchické stromové zobrazení dat. Podrobněji se jedná o pozdější modul.

## <a name="login-control"></a>Řízení přihlášení

Ovládací prvek Přihlášení poskytuje mechanismus pro přihlášení k webu. Podrobněji se jedná o pozdější modul.

## <a name="loginview-control"></a>Ovládací prvek LoginView

Ovládací prvek LoginView umožňuje zobrazení různých šablon na základě stavu přihlášení uživatele. Podrobněji se jedná o pozdější modul.

## <a name="passwordrecovery-control"></a>Ovládací prvek Obnovení hesla

Ovládací prvek PasswordRecovery se používá k načtení zapomenutých hesel uživateli ASP.NET aplikace. Podrobněji se jedná o pozdější modul.

## <a name="loginstatus"></a>Loginstatus

Ovládací prvek LoginStatus zobrazuje stav přihlášení uživatele. Podrobněji se jedná o pozdější modul.

## <a name="loginname"></a>Loginname

Ovládací prvek LoginName zobrazí uživatelské jméno uživatele po přihlášení do ASP.NET aplikace. Podrobněji se jedná o pozdější modul.

## <a name="createuserwizard"></a>Createuserwizard

CreateUserWizard je konfigurovatelný průvodce, který dává uživatelům možnost vytvořit účet členství ASP.NET pro použití v ASP.NET aplikaci. Podrobněji se jedná o pozdější modul.

## <a name="changepassword"></a>Changepassword

Ovládací prvek ChangePassword umožňuje uživatelům změnit své heslo pro ASP.NET aplikaci. Podrobněji se jedná o pozdější modul.

## <a name="various-webparts"></a>Různé webové části

ASP.NET 2.0 je dodáván s různými webovými částmi. Ty budou podrobně popsány v pozdějším modulu.
