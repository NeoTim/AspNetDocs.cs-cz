---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: Zobrazení vlastní chybové stránky (C#) | Microsoft Docs
author: rick-anderson
description: Co uživatel uvidí, když dojde k běhové chybě ve webové aplikaci v ASP.NET? Odpověď závisí na tom, jak je &lt; Konfigurace customErrors webu &gt; ....
ms.author: riande
ms.date: 06/09/2009
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 777948732690443d63f1fb2afd6f72a33a496c44
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2020
ms.locfileid: "86211046"
---
# <a name="displaying-a-custom-error-page-c"></a>Zobrazení vlastní chybové stránky (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> Co uživatel uvidí, když dojde k běhové chybě ve webové aplikaci v ASP.NET? Odpověď závisí na tom, jak je &lt; Konfigurace customErrors webu &gt; . Ve výchozím nastavení se uživatelům zobrazí nemonitorované žluté zobrazení, že došlo k chybě za běhu. V tomto kurzu se dozvíte, jak přizpůsobit tato nastavení, aby se zobrazila vlastní chybová stránka aesthetically-přitažlivé, která odpovídá vzhledu a chování vašeho webu.

## <a name="introduction"></a>Úvod

V ideálním světě by nedocházelo k žádným chybám za běhu. Programátoři by napsali kód s Nary chybou a robustním ověřováním vstupu uživatele a externí prostředky, jako jsou databázové servery a e-mailové servery, nikdy nepřešly do offline režimu. V průběhu realit je samozřejmě nevyhnutelné chyby. Třídy v .NET Framework signalizují chybu vyvoláním výjimky. Například volání metody Open objektu SqlConnection naváže připojení k databázi určené připojovacím řetězcem. Pokud je však databáze mimo provoz nebo pokud jsou přihlašovací údaje v připojovacím řetězci neplatné, vyvolá metoda Open výjimku `SqlException` . Výjimky lze zpracovat pomocí `try/catch/finally` bloků. Pokud kód v rámci `try` bloku vyvolá výjimku, řízení se převede na příslušný blok catch, kde se vývojář může pokusit o zotavení z chyby. Pokud neexistuje žádný odpovídající blok catch nebo pokud kód, který vyvolal výjimku, není v bloku try, výjimka percolates zásobník volání v hledání `try/catch/finally` bloků.

Pokud se výjimka objeví v bublinách až po ASP.NET modulu runtime bez zpracování, je vyvolána [ `Error` událost](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) [ `HttpApplication` třídy](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)a zobrazí se nakonfigurovaná *chybová stránka* . Ve výchozím nastavení ASP.NET zobrazí chybovou stránku, na kterou se affectionately říká [žlutá obrazovka smrti](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) (YSOD). Existují dvě verze YSOD: jedna zobrazuje podrobnosti výjimky, trasování zásobníku a další informace, které jsou užitečné pro vývojáře s laděním aplikace (viz **Obrázek 1**); Druhá hodnota se jednoduše uvádí, že došlo k chybě za běhu (viz **Obrázek 2**).

Podrobnosti o výjimce YSOD je poměrně užitečná pro vývojáře, kteří aplikaci ladí, ale zobrazuje YSOD pro koncové uživatele je směrové a neprofesionální. Místo toho je potřeba, aby se koncoví uživatelé převzali na chybovou stránku, která udržuje vzhled webu a má pocit, že se s tím postará prose popis situace. Dobrá zpráva je, že vytvoření takové vlastní chybové stránky je poměrně snadné. Tento kurz začíná pohledem na ASP. Různé chybové stránky sítě. Pak ukazuje, jak nakonfigurovat webovou aplikaci tak, aby zobrazovala uživatele vlastní chybovou stránku na tváři chyby.

### <a name="examining-the-three-types-of-error-pages"></a>Prozkoumání tří typů chybových stránek

Pokud dojde k neošetřené výjimce v aplikaci ASP.NET, zobrazí se jeden ze tří typů chybových stránek:

- Podrobnosti výjimky žlutá obrazovka na chybové stránce smrti,
- Chyba za běhu žlutá obrazovka chybové stránky smrti nebo
- Vlastní chybová stránka

Stránka s chybou, kterou vývojáři znají, je YSOD podrobnosti o výjimce. Ve výchozím nastavení se tato stránka zobrazuje uživatelům, kteří jsou místně navštíveni, a proto je stránka, která se zobrazí, když při testování webu ve vývojovém prostředí dojde k chybě. Jak je uvedeno, informace o výjimce YSOD poskytuje podrobnosti o výjimce – typ, zprávu a trasování zásobníku. Co více, pokud byla výjimka vyvolána kódem na pozadí vaší stránky ASP.NET a pokud je aplikace nakonfigurována pro ladění, pak podrobnosti o výjimce YSOD také zobrazí tento řádek kódu (a několik řádků kódu nad a pod ním).

**Obrázek 1** znázorňuje stránku podrobností o výjimce YSOD. Poznamenejte si adresu URL v okně Adresa prohlížeče: `http://localhost:62275/Genre.aspx?ID=foo` . Odvolá na `Genre.aspx` stránku seznam revizí knihy v konkrétním žánru. Vyžaduje, aby `GenreId` hodnota (a `uniqueidentifier` ) byla předána řetězcem QueryString; například příslušná adresa URL pro zobrazení fiktivních recenzí `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146` . Pokud `uniqueidentifier` je hodnota bez hodnoty předána prostřednictvím řetězce dotazu (například "foo"), je vyvolána výjimka.

> [!NOTE]
> Chcete-li regenerovat tuto chybu v ukázkové webové aplikaci, která je k dispozici ke stažení, můžete buď přejít `Genre.aspx?ID=foo` přímo, nebo kliknout na odkaz "generovat chybu za běhu" v tématu `Default.aspx` .

Všimněte si informací o výjimce prezentovaných na **obrázku 1**. Zpráva o výjimce, "převod se nezdařil při převodu ze znakového řetězce na typ uniqueidentifier" je přítomen v horní části stránky. Typ výjimky, `System.Data.SqlClient.SqlException` , je uveden také. K dispozici je také trasování zásobníku.

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**Obrázek 1**: YSOD podrobnosti o výjimce obsahuje informace o výjimce.  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](displaying-a-custom-error-page-cs/_static/image3.png))

Druhý typ YSOD je Běhová chyba YSOD a je zobrazen na **obrázku 2**. Běhová chyba YSOD informuje návštěvníka, že došlo k chybě za běhu, ale nezahrnuje žádné informace o výjimce, která byla vyvolána. (Nicméně obsahuje pokyny k tomu, jak zobrazit podrobnosti o chybě úpravou `Web.config` souboru, který je součástí toho, co YSOD vypadá neprofesionálně.)

Ve výchozím nastavení se chyba modulu runtime YSOD zobrazuje uživatelům, kteří se vzdáleně navštěvují (přes, jak je uvedeno v adrese http://www.yoursite.com) URL na adresním řádku prohlížeče na **obrázku 2**: `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo` . K dispozici jsou dvě různé obrazovky YSOD, protože vývojáři mají zájem o informace o chybě, ale tyto informace by se neměly zobrazovat na živém webu, protože mohou odhalit potenciální slabá místa zabezpečení nebo jiné citlivé informace pro kohokoli, kdo navštívil web.

> [!NOTE]
> Pokud používáte a používáte jako webového hostitele DiscountASP.NET, můžete si všimnout, že při návštěvě živého webu se nezobrazuje YSOD chyba modulu runtime. Důvodem je to, že DiscountASP.NET má své servery konfigurované tak, aby ve výchozím nastavení zobrazovaly podrobnosti o výjimce YSOD. Dobrá zpráva je, že toto výchozí chování můžete přepsat přidáním `<customErrors>` oddílu do `Web.config` souboru. V části konfigurace, která chybová stránka se zobrazuje, se podrobně podíváme na `<customErrors>` část.

[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**Obrázek 2**: Běhová chyba YSOD neobsahuje žádné podrobnosti o chybě.  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](displaying-a-custom-error-page-cs/_static/image6.png))

Třetí typ chybové stránky je vlastní chybová stránka, která je webovou stránkou, kterou vytvoříte. Výhodou vlastní chybové stránky je, že máte plnou kontrolu nad informacemi, které se zobrazí uživateli, spolu s jeho vzhledem a chováním stránky. vlastní chybová stránka může používat stejnou stránku předlohy a styly jako vaše jiné stránky. Část "použití vlastní chybové stránky" vás provede vytvořením vlastní chybové stránky a její konfigurací, aby se zobrazila v případě neošetřené výjimky. **Obrázek 3** nabízí špičku vás zajímá této vlastní chybové stránky. Jak vidíte, vzhled a chování chybové stránky je mnohem lepší než na žlutých obrazovkách smrti uvedených na obrázcích 1 a 2.

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**Obrázek 3**: vlastní chybová stránka nabízí lépe přizpůsobený vzhled a chování.  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](displaying-a-custom-error-page-cs/_static/image9.png))

Chvíli počkejte, než zkontrolujete adresní řádek prohlížeče na **obrázku 3**. Všimněte si, že se v adresním řádku zobrazuje adresa URL vlastní chybové stránky ( `/ErrorPages/Oops.aspx` ). Na obrázcích 1 a 2 se žluté obrazovky smrti zobrazují na stejné stránce, na které chyba vznikla ( `Genre.aspx` ). Vlastní chybová stránka je předána adresa URL stránky, kde došlo k chybě prostřednictvím `aspxerrorpath` parametru QueryString.

## <a name="configuring-which-error-page-is-displayed"></a>Konfigurace zobrazené chybové stránky

To, jaké tři chybové stránky se zobrazí, je založené na dvou proměnných:

- Informace o konfiguraci v `<customErrors>` části a
- Zda uživatel navštíví web místně nebo vzdáleně.

[ `<customErrors>` Část](https://msdn.microsoft.com/library/h0hfz6fc.aspx) v `Web.config` má dva atributy, které mají vliv na zobrazenou chybovou stránku: `defaultRedirect` a `mode` . `defaultRedirect`Atribut je nepovinný. Pokud je tato stránka k dispozici, určuje adresu URL vlastní chybové stránky a označuje, že by se měla zobrazit vlastní chybová stránka namísto běhové chyby YSOD. `mode`Atribut je povinný a přijímá jednu ze tří hodnot: `On` , `Off` , nebo `RemoteOnly` . Tyto hodnoty mají následující chování:

- `On`– označuje, že vlastní chybová stránka nebo chyba modulu runtime YSOD se zobrazí všem návštěvníkům bez ohledu na to, jestli jsou místní nebo vzdálené.
- `Off`– Určuje, že podrobnosti o výjimce YSOD se zobrazí všem návštěvníkům bez ohledu na to, jestli jsou místní nebo vzdálené.
- `RemoteOnly`– označuje, že vlastní chybová stránka nebo chyba modulu runtime YSOD se zobrazuje vzdáleným návštěvníkům, zatímco podrobnosti o výjimce YSOD se zobrazují místním návštěvníkům.

Pokud neurčíte jinak, ASP.NET funguje jako v případě, že jste nastavili atribut Mode na `RemoteOnly` hodnotu a nezadali jste `defaultRedirect` hodnotu. Jinými slovy, výchozím chováním je, že podrobnosti o výjimce YSOD se zobrazují místním návštěvníkům, zatímco Běhová chyba YSOD se zobrazuje vzdáleným návštěvníkům. Toto výchozí chování můžete přepsat přidáním `<customErrors>` oddílu do webové aplikace.`Web.config file.`

## <a name="using-a-custom-error-page"></a>Použití vlastní chybové stránky

Každá webová aplikace by měla mít vlastní chybovou stránku. Nabízí pokročilejší alternativu k chybě za běhu YSOD, je snadné vytvořit a nakonfigurovat aplikaci, aby používala vlastní chybovou stránku, trvá jenom několik minut. Prvním krokem je vytvoření vlastní chybové stránky. Přidal (a) jsem novou složku do aplikace recenze `ErrorPages` a přidala do ní novou ASP.NET stránku s názvem `Oops.aspx` . Nechte stránku používat stejnou stránku předlohy jako zbytek stránek na webu tak, aby automaticky dědila stejný vzhled a chování.

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**Obrázek 4**: Vytvoření vlastní chybové stránky

Dále Věnujte několik minut vytváření obsahu pro chybovou stránku. Vytvořili jsem jednoduchou vlastní chybovou stránku se zprávou oznamující, že došlo k neočekávané chybě a odkaz zpátky na domovskou stránku webu.

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**Obrázek 5**: návrh vlastní chybové stránky  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](displaying-a-custom-error-page-cs/_static/image14.png))

Po dokončení chybové stránky nakonfigurujte webovou aplikaci tak, aby používala vlastní chybovou stránku místo chyby modulu runtime YSOD. To lze provést zadáním adresy URL chybové stránky v `<customErrors>` `defaultRedirect` atributu oddílu. Do souboru aplikace přidejte následující kód `Web.config` :

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

Výše uvedený kód nakonfiguruje aplikaci tak, aby zobrazovala podrobnosti o výjimce YSOD uživatelům, kteří se lokálně navštěvují, a při použití vlastní chybové stránky se na vzdálené návštěvě těchto uživatelů bohužel nezobrazuje. aspx. Pokud to chcete vidět v akci, nasaďte svůj web do provozního prostředí a pak na živém webu navštivte stránku Žánr. aspx s neplatnou hodnotou QueryString. Měla by se zobrazit vlastní chybová stránka (odkaz zpět na **Obrázek 3**).

Chcete-li ověřit, zda se vlastní chybová stránka zobrazuje pouze vzdáleným uživatelům, navštivte `Genre.aspx` stránku s neplatným řetězcem dotazu z vývojového prostředí. Stále byste měli vidět podrobnosti o výjimce YSOD (zpět na **Obrázek 1**). `RemoteOnly`Nastavení zajišťuje, že uživatelé, kteří navštíví web v produkčním prostředí, uvidí vlastní chybovou stránku, zatímco vývojáři pracují místně i nadále, aby viděli podrobnosti o výjimce.

## <a name="notifying-developers-and-logging-error-details"></a>Oznamování vývojářů a protokolování podrobností o chybách

Chyby, ke kterým došlo ve vývojovém prostředí, byly způsobeny vývojářem v jeho počítači. Zobrazuje informace o výjimce v YSOD Details výjimky a ví, jaké kroky prováděly při výskytu chyby. Pokud ale dojde k chybě v produkčním prostředí, vývojář nemá žádné informace o tom, že došlo k chybě, pokud koncový uživatel, který navštívil web, nezíská čas k nahlášení chyby. A dokonce i v případě, že se uživatel dostane k upozornění vývojového týmu, že došlo k chybě, bez znalosti typu výjimky, zprávy a trasování zásobníku může být obtížné diagnostikovat příčinu chyby, ať už ji opravit.

Z těchto důvodů je nejdůležitější, že všechny chyby v produkčním prostředí jsou protokolovány do některého trvalého úložiště (například databáze) a že se vývojářům zobrazí upozornění na tuto chybu. Vlastní chybová stránka může vypadat jako vhodné místo pro toto protokolování a oznámení. Vlastní chybová stránka bohužel nemá přístup k podrobnostem o chybě, a proto ji nelze použít k zaznamenání těchto informací. Dobrá zpráva je, že existuje několik způsobů, jak zachytit podrobnosti o chybě a přihlásit se k nim, a další tři kurzy si podrobněji Prozkoumejte toto téma.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>Používání různých vlastních chybových stránek pro různé stavy chyb protokolu HTTP

Pokud je výjimka vyvolána stránkou ASP.NET a není zpracována, výjimka percolates až do běhového prostředí ASP.NET, které zobrazuje konfigurovanou chybovou stránku. Pokud přijde požadavek do modulu ASP.NET, ale nedá se z nějakého důvodu zpracovat, možná se nenašlo požadovaný soubor nebo pro něj jsou zakázaná oprávnění ke čtení, modul ASP.NET vyvolá `HttpException` . Tato výjimka, jako jsou výjimky vyvolané z ASP.NET stránek, bubliny až do modulu runtime, což způsobí zobrazení příslušné chybové stránky.

To znamená, že pokud uživatel požádá o nenalezenou stránku, zobrazí se jim vlastní chybová stránka, která je pro webovou aplikaci v provozu. **Obrázek 6** znázorňuje příklad. Vzhledem k tomu, že žádost je určena pro neexistující stránku ( `NoSuchPage.aspx` ), `HttpException` je vyvolána a zobrazí se vlastní chybová stránka (Všimněte si odkazu na `NoSuchPage.aspx` v `aspxerrorpath` parametru QueryString).

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**Obrázek 6**: modul runtime ASP.NET zobrazí nakonfigurovanou chybovou stránku v reakci na neplatnou žádost ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-a-custom-error-page-cs/_static/image17.png)

Ve výchozím nastavení všechny typy chyb způsobují zobrazení stejné vlastní chybové stránky. Můžete však zadat jinou vlastní chybovou stránku pro určitý stavový kód HTTP pomocí `<error>` podřízených elementů v `<customErrors>` oddílu. Například pokud chcete, aby se v případě chyby stránky, která nebyla nalezena, zobrazila jiná chybová stránka, která má stavový kód HTTP 404, aktualizujte `<customErrors>` oddíl tak, aby obsahoval následující kód:

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

Pokud se tato změna provádí, kdykoli uživatel, který se vzdáleně navštíví, vyžádá prostředek ASP.NET, který neexistuje, bude přesměrován na `404.aspx` vlastní chybovou stránku, nikoli na `Oops.aspx` . Jak ukazuje **Obrázek 7** , `404.aspx` Stránka může obsahovat konkrétnější zprávu, než je obecná vlastní chybová stránka.

> [!NOTE]
> Další informace najdete na [stránce s chybovými stránkami 404, kde najdete](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) pokyny k vytváření efektivních chybových stránek 404.

[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)

**Obrázek 7**: vlastní chybová stránka 404 zobrazuje více cílené zprávy, než`Oops.aspx`  
([Kliknutím zobrazíte obrázek v plné velikosti.](displaying-a-custom-error-page-cs/_static/image20.png)) 

Vzhledem k tomu, že víte, že `404.aspx` stránka je k dispozici pouze v případě, že uživatel provede požadavek na stránku, která nebyla nalezena, můžete tuto vlastní chybovou stránku rozšířit, aby zahrnovala funkce, aby uživatel mohl vyřešit tento konkrétní typ chyby. Můžete například sestavit databázovou tabulku, která mapuje známé chybné adresy URL na dobré adresy URL a pak má `404.aspx` vlastní chybovou stránku spustit dotaz proti této tabulce a stránky navrhnout, se kterým se uživatel může pokusit spojit.

> [!NOTE]
> Vlastní chybová stránka se zobrazí pouze v případě, že je proveden požadavek na prostředek zpracovávaný modulem ASP.NET. Jak jsme probrali v [základních rozdílech mezi službou IIS a vývojovým serverem ASP.NET](core-differences-between-iis-and-the-asp-net-development-server-cs.md) , může webový server zpracovávat určité požadavky samostatně. Webový server služby IIS ve výchozím nastavení zpracovává požadavky na statický obsah, jako jsou obrázky a soubory HTML bez vyvolání modulu ASP.NET. V důsledku toho, pokud si uživatel požádá o neexistující soubor bitové kopie, vrátí zpět výchozí 404 chybovou zprávu služby IIS, a ne ASP. Chybná stránka konfigurace sítě

## <a name="summary"></a>Shrnutí

Pokud dojde k neošetřené výjimce v aplikaci ASP.NET, zobrazí se na uživateli jedna ze tří chybových stránek: informace o výjimce žlutá obrazovka smrti; Chyba za běhu žlutá obrazovka smrti; nebo vlastní chybovou stránku. Která chybová stránka se zobrazí v závislosti na konfiguraci aplikace `<customErrors>` a na tom, jestli se uživatel místně nebo vzdáleně navštíví. Výchozím chováním je zobrazit podrobnosti o výjimce YSOD místním návštěvníkům a běhové chybě YSOD pro vzdálené návštěvníky.

I když Běhová chyba YSOD skrývá potenciálně citlivé informace o chybách uživatele, který navštívil web, přeruší se vzhled a chování vaší lokality a aplikace bude ladit. Lepším řešením je použití vlastní chybové stránky, která zahrnuje vytvoření a návrh vlastní chybové stránky a určení její adresy URL v `<customErrors>` `defaultRedirect` atributu oddílu. Můžete mít i několik vlastních chybových stránek pro různé stavy chyb protokolu HTTP.

Vlastní chybová stránka je prvním krokem v komplexní strategii zpracování chyb pro web v produkčním prostředí. Důležité kroky jsou také upozorňující vývojáře na chybu a protokolování jeho podrobností. V následujících třech kurzech se seznámíte s postupy pro oznamování chyb a protokolování.

Šťastné programování!

### <a name="further-reading"></a>Další materiály

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Chybové stránky, ještě jeden další čas](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [Pokyny k návrhu pro výjimky](https://msdn.microsoft.com/library/ms229014.aspx)
- [Uživatelsky přívětivé chybové stránky](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Zpracování a vyvolávání výjimek](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [Správné používání vlastní chybové stránky v ASP.NET](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)
- [Přehled trasování ASP.NET](/previous-versions/aspnet/bb386420(v%3Dvs.100))

> [!div class="step-by-step"]
> [Předchozí](strategies-for-database-development-and-deployment-cs.md) 
>  [Další](processing-unhandled-exceptions-cs.md)
