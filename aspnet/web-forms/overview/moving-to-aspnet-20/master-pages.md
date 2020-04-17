---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Vzorové stránky | Dokumenty společnosti Microsoft
author: rick-anderson
description: Jednou z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1.x vývojáři používali uživatelské ovládací prvky k replikaci společné stránky elem ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543181"
---
# <a name="master-pages"></a>Stránky předlohy

podle [společnosti Microsoft](https://github.com/microsoft)

> Jednou z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1.x vývojáři používali uživatelské ovládací prvky k replikaci běžných prvků stránky ve webové aplikaci. I když to je jistě funkční řešení, pomocí uživatelských ovládacích prvků má některé nevýhody. Změna polohy uživatelského ovládacího prvku například vyžaduje změnu více stránek na webu. Uživatelské ovládací prvky se také nezobrazují v návrhovém zobrazení po vložení na stránku.

Jednou z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1.x vývojáři používali uživatelské ovládací prvky k replikaci běžných prvků stránky ve webové aplikaci. I když to je jistě funkční řešení, pomocí uživatelských ovládacích prvků má některé nevýhody. Změna polohy uživatelského ovládacího prvku například vyžaduje změnu více stránek na webu. Uživatelské ovládací prvky se také nezobrazují v návrhovém zobrazení po vložení na stránku.

ASP.NET 2.0 zavádí stránky předlohy jako způsob zachování konzistentního vzhledu a chování, a jak brzy uvidíte, stránky předlohy představují významné zlepšení oproti metodě uživatelského ovládacího prvku.

## <a name="why-master-pages"></a>Proč stránky předlohy?

Možná se divíte, proč byly v ASP.NET 2.0 potřeba stránky předlohy. Koneckonců, vývojáři webu již používají uživatelské ovládací prvky v ASP.NET 1.x ke sdílení oblastí obsahu mezi stránkami. Ve skutečnosti existuje několik důvodů, proč jsou uživatelské ovládací prvky méně než optimální řešení pro vytvoření společného rozložení.

Uživatelské ovládací prvky ve skutečnosti nedefinují rozložení stránky. Místo toho definují rozložení a funkce pro část stránky. Rozdíl mezi těmito dvěma je důležité, protože to dělá ovladatelnost řešení uživatelského ovládacího prvku mnohem obtížnější. Chcete-li například změnit umístění uživatelského ovládacího prvku na stránce, je nutné upravit skutečnou stránku, na které se uživatelský ovládací prvek zobrazí. To je v pořádku, pokud máte jen několik stránek, ale ve velkých místech, to se rychle stává noční můrou pro správu webu!

Další nevýhodou použití uživatelských ovládacích prvků pro definování společnérozložení je zakořeněna v architektuře ASP.NET samotného. Pokud se změní libovolný veřejný člen uživatelského ovládacího prvku, vyžaduje, abyste překompilovali všechny stránky, které používají uživatelský ovládací prvek. Na druhé straně ASP.NET bude re-JIT vaše stránky při prvním přístupu. To opět vytváří neškálovatelnou architekturu a problém se správou lokalit y pro větší weby.

Oba tyto problémy (a mnoho dalších) jsou pěkně řešeny stránek předlohy v ASP.NET 2.0.

## <a name="how-master-pages-work"></a>Jak stránky předlohy fungují

Stránka předlohy je obdobou šablony pro jiné stránky. Na stránku předlohy se přidají prvky stránky, které by měly být sdíleny mezi jinými stránkami (tj. nabídkami, ohraničeními atd.). Když jsou na web přidány nové stránky, můžete je přidružit ke stránce předlohy. Stránka přidružená ke stránce předlohy se nazývá **stránka obsahu**. Ve výchozím nastavení se stránka obsahu uchyluje k vzhledu ze stránky předlohy. Při vytváření stránky předlohy však můžete definovat části stránky, které může stránka obsahu nahradit vlastním obsahem. Tyto části jsou definovány pomocí nového ovládacího prvku zavedeného v ASP.NET 2.0; ovládací prvek **ContentPlaceHolder.**

Stránka předlohy může obsahovat libovolný počet ovládacích prvků ContentPlaceHolder (nebo vůbec žádné.) Na stránce obsahu se obsah z ovládacích prvků ContentPlaceHolder zobrazí uvnitř ovládacích prvků **Content,** což je další nový ovládací prvek v ASP.NET 2.0. Ve výchozím nastavení jsou ovládací prvky obsahu stránky obsahu prázdné, takže můžete zadat vlastní obsah. Pokud chcete použít obsah ze stránky předlohy uvnitř ovládacích prvků Obsah, můžete tak učinit tak, jak uvidíte dále v tomto modulu. Ovládací prvek Content je mapován na ovládací prvek ContentPlaceHolder prostřednictvím atributu ContentPlaceHolderID ovládacího prvku Content. Níže uvedený kód mapuje ovládací prvek Content na ovládací prvek ContentPlaceHolder nazvaný mainBody na vzorové stránce.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Často uslyšíte, jak lidé popisují stránky předlohy jako základní třídu pro jiné stránky. To vlastně není pravda. Vztah mezi stránkami předlohy a stránkami obsahu není vztahem dědičnosti.

**Obrázek 1** znázorňuje stránku předlohy a přidruženou stránku obsahu tak, jak jsou zobrazeny v sadě Visual Studio 2005. Ovládací prvek ContentPlaceHolder můžete zobrazit na stránce předlohy a odpovídající ovládací prvek Obsah na stránce obsahu. Všimněte si, že obsah předlohy stránek, který je mimo ContentPlaceHolder je viditelný, ale šedě na stránce obsahu. Stránka obsahu může nahradit pouze obsah uvnitř contentplaceholderu. Veškerý další obsah, který pochází ze stránky předlohy, je neměnný.

![Stránka předlohy a její přidružená stránka obsahu](master-pages/_static/image1.jpg)

**Obrázek 1**: Stránka předlohy a její přidružená stránka obsahu

## <a name="creating-a-master-page"></a>Vytvoření stránky předlohy

Vytvoření nové stránky předlohy:

1. Otevřete visual studio 2005 a vytvořte nový web.
2. Klikněte na Soubor, Nový, Soubor.
3. Zvolte Hlavní soubor z dialogového okna Přidat novou položku, jak je znázorněno **na obrázku 2**.
4. Klikněte na Přidat.

![Vytvoření nové stránky předlohy](master-pages/_static/image2.jpg)

**Obrázek 2**: Vytvoření nové stránky předlohy

Všimněte si, že přípona souboru pro stránku předlohy je *.master*. Jedná se o jeden ze způsobů, jak se stránka předlohy liší od běžné stránky. Další primární rozdíl je, že @Page namísto směrnice, stránka @Master předlohy obsahuje směrnice. Přepněte do zdrojového zobrazení pro stránku předlohy, kterou jste právě vytvořili, a zkontrolujte kód.

Nová stránka předlohy bude mít ve výchozím nastavení jeden ovládací prvek ContentPlaceHolder. Ve většině případů má větší smysl nejprve vytvořit prvky společné stránky a potom vložit ovládací prvky ContentPlaceHolder tam, kde je požadován vlastní obsah. V těchto případech budou vývojáři chtít odstranit výchozí ovládací prvek ContentPlaceHolder a vložit nové, jakmile bude stránka vyvíjena. Ovládací prvky ContentPlaceHolder nelze zmenšit navzdory skutečnosti, že zobrazují úchyty pro nastavení velikosti. ContentPlaceHolder velikosti ovládacího prvku automaticky na základě obsahu, který obsahuje s jednou výjimkou; Pokud umístíte ovládací prvek ContentPlaceHolder uvnitř prvku bloku, jako je například buňka tabulky, bude velikost podle velikosti prvku.

## <a name="lab-1-working-with-master-pages"></a>Laboratoř 1 Práce se stránkami předlohy

V tomto testovacím prostředí vytvoříte novou stránku předlohy a definujete tři ovládací prvky ContentPlaceHolder. Poté vytvoříte novou stránku Obsahu a nahradíte obsah alespoň z jednoho z ovládacích prvků ContentPlaceHolder.

1. Vytvořte vzorovou stránku a vložte ovládací prvky ContentPlaceHolder. 

    1. Vytvořte novou stránku předlohy, jak je popsáno výše.
    2. Odstraňte výchozí ovládací prvek ContentPlaceHolder.
    3. Vyberte ovládací prvek ContentPlaceHolder kliknutím na stínované horní ohraničení ovládacího prvku a pak jej odstraňte stisknutím klávesy DEL na klávesnici.
    4. Vložte novou tabulku pomocí *šablony Záhlaví a boční* stránky, jak je znázorněno na obrázku 3. Změňte šířku a výšku na 90 % každý tak, aby celá tabulka je viditelná v návrháři.

![](master-pages/_static/image3.jpg)

**Obrázek 3**

1. Umístěte kurzor do každé buňky tabulky a nastavte vlastnost *valign* na *začátek*.
2. V panelu nástrojů vložte ovládací prvek ContentPlaceHolder do horní buňky tabulky (buňky záhlaví).)
3. Když vložíte tento ovládací prvek ContentPlaceHolder, všimnete si, že výška řádku zabere téměř celou stránku, jak je znázorněno na obrázku 4. V tuto chvíli se tím neznepokojuj.

![Prázdné místo je ve stejné buňce jako ContentPlaceHolder](master-pages/_static/image1.gif)

**Obrázek 4**: Prázdné místo je ve stejné buňce jako ContentPlaceHolder

1. Umístěte ovládací prvek ContentPlaceHolder do ostatních dvou buněk. Po vložení ostatních ovládacích prvků ContentPlaceHolder by měla být velikost buněk tabulky tak, jak byste očekávali. Stránka by nyní měla vypadat jako stránka zobrazená **na obrázku 5**.

![Master se všemi ovládacími prvky ContentPlaceHolder. Všimněte si, že výška buňky pro buňku záhlaví je nyní to, co by mělo být](master-pages/_static/image2.gif)

**Obrázek 5**: Předloha se všemi ovládacími prvky ContentPlaceHolder. Všimněte si, že výška buňky pro buňku záhlaví je nyní to, co by mělo být

1. Do každého ze tří ovládacích prvků ContentPlaceHolder zadejte nějaký text podle svého výběru.
2. Uložit stránku předlohy jako exercise1.master.
3. Vytvořte nový webový formulář a přidružte jej ke stránce předlohy exercise1.master.
4. V yberte Soubor, Nový, Soubor v sadě Visual Studio 2005.
5. V dialogovém okně Přidat novou položku vyberte **webový formulář.**
6. Zkontrolujte, zda je zaškrtnuté políčko Vybrat stránku předlohy, jak je znázorněno na obrázku 6.

![Přidání nové stránky obsahu](master-pages/_static/image3.gif)

**Obrázek 6**: Přidání nové stránky obsahu

1. Klikněte na Přidat.
2. Vyberte cvičení1.master v dialogovém okně Vybrat stránku předlohy, jak je znázorněno na obrázku 7.
3. Kliknutím na OK přidejte novou stránku obsahu.

Nová stránka obsahu se zobrazí v sadě Visual Studio s jedním ovládacím prvkem Obsah pro každý ovládací prvek ContentPlaceHolder na stránce předlohy. Ve výchozím nastavení jsou ovládací prvky obsahu prázdné, takže můžete přidat vlastní obsah. Pokud chcete, aby použili obsah z ovládacího prvku ContentPlaceHolder na stránce předlohy, jednoduše klikněte na symbol inteligentní značky (malá černá šipka v pravém horním rohu ovládacího prvku) a z chytré značky zvolte *Výchozí pro předlohy obsahu,* jak je znázorněno na **obrázku 8**. Pokud tak učiníte, položka nabídky se změní na *Vytvořit vlastní obsah*. Kliknutím na něj v tomto okamžiku odeberete obsah ze stránky předlohy, což vám umožní definovat vlastní obsah pro daný ovládací prvek Obsah.

![Nastavení ovládacího prvku obsahu na výchozí hodnotu pro obsah vzorových stránek](master-pages/_static/image4.gif)

**Obrázek 7**: Nastavení ovládacího prvku obsahu na výchozí hodnotu obsahu předlohy

## <a name="connecting-master-page-and-content-pages"></a>Připojení stránky předlohy a stránek obsahu

Přidružení mezi stránkou předlohy a stránkou obsahu lze nakonfigurovat jedním ze čtyř různých způsobů:

- Atribut <strong>MasterPageFile</strong> @Page směrnice
- Nastavení vlastnosti **Page.MasterPageFile** v kódu.
- Element ** &lt;&gt; stránky** v konfiguračním souboru aplikací (web.config v kořenové složce aplikace)
- Element ** &lt;&gt; stránky** v konfiguračním souboru podsložek (web.config v podsložce)

## <a name="masterpagefile-attribute"></a>Atribut MasterPageFile

Atribut MasterPageFile usnadňuje použití stránky předlohy na určitou stránku ASP.NET. Je to také metoda použitá k použití stránky předlohy při zaškrtnutí políčka **Vybrat stránku předlohy** stejně jako ve cvičení 1.

## <a name="setting-pagemasterpagefile-in-code"></a>Nastavení souboru Page.MasterPageFile v kódu

Nastavením vlastnosti MasterPageFile v kódu můžete použít určitou stránku předlohy na obsah za běhu. To je užitečné v případech, kdy může být nutné použít určitou stránku předlohy na základě role uživatelů nebo jiných kritérií. Vlastnost MasterPageFile musí být nastavena v metodě PreInit. Pokud je nastavena po PreInit metoda, invalidOperationException bude vyvolána. Stránka, na které je tato vlastnost nastavena, musí mít také ovládací prvek Content jako ovládací prvek nejvyšší úrovně pro stránku. V opačném případě bude vyvolána výjimka HttpException, když je nastavena vlastnost MasterPageFile.

## <a name="using-the-ltpagesgt-element"></a>Použití &lt;stránek&gt; Element

Stránku předlohy pro stránky můžete nakonfigurovat nastavením &lt;&gt; atributu masterPageFile v elementu stránky souboru web.config. Při použití této metody mějte na paměti, že soubory web.config nižší ve struktuře aplikace mohou toto nastavení přepsat. Toto nastavení také přepíše všechny atributy MasterPageFile nastavené @Page v direktivě. Použití &lt;prvku&gt; stránky usnadňuje vytvoření *vzorové* stránky, kterou lze v případě potřeby přepsat v konkrétních složkách nebo souborech.

## <a name="properties-in-master-pages"></a>Vlastnosti na vzorových stránkách

Stránka předlohy může zpřístupnit vlastnosti prostým zveřejněním těchto vlastností na stránce předlohy. Například následující kód definuje vlastnost s názvem SomeProperty:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Chcete-li získat přístup k vlastnosti SomeProperty ze stránky Obsah, budete muset použít vlastnost Master takto:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Vnoření stránek předlohy

Vzorové stránky jsou ideálním řešením pro zajištění společného vzhledu a chování ve velké webové aplikaci. Není však neobvyklé, že určité části velkého webu sdílejí společné rozhraní, zatímco jiné části sdílejí jiné rozhraní. Chcete-li tuto potřebu vyřešit, je ideálním řešením více stránek předlohy. To však stále neřeší skutečnost, že velká aplikace může mít určité součásti (například nabídku), které jsou sdíleny mezi všemi stránkami a dalšími součástmi, které jsou sdíleny pouze mezi určitými částmi webu. Pro tento typ situace vnořené stránky předlohy vyplnit potřebu pěkně. Jak jste viděli, normální stránka předlohy se skládá ze stránky předlohy a stránky obsahu. V situaci vnořené stránky předlohy existují dvě stránky předlohy; nadřazený předloha a podřízený předloha. Podřízená stránka předlohy je také stránka obsahu a její předloha je nadřazenou stránkou předlohy.

Zde je kód pro typickou stránku předlohy:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

V vnořeném hlavním scénáři by to byl nadřazený předloha. Jiná stránka předlohy by tuto stránku použila jako stránku předlohy a tento kód by vypadal takto:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Všimněte si, že v tomto scénáři podřízená předloha je také stránka obsahu pro nadřazenou předlohu. Veškerý obsah podřízeného předlohy se zobrazí uvnitř ovládacího prvku Content, který získá jeho obsah z nadřazeného ovládacího prvku ContentPlaceHolder.

> [!NOTE]
> Podpora návrháře není k dispozici pro vnořené stránky předlohy. Při vývoji pomocí vnořených předloh budete muset použít zdrojové zobrazení.

Toto video ukazuje návod k použití vnořených stránek předlohy.

![](master-pages/_static/image1.png)

[Otevřít video na celou obrazovku](master-pages/_static/nested1.wmv)

![Výběr stránky předlohy](master-pages/_static/image4.jpg)

**Obrázek 8**: Výběr stránky předlohy
