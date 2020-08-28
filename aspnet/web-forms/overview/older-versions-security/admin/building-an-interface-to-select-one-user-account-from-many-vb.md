---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: Sestavení rozhraní pro výběr jednoho uživatelského účtu z mnoha (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu sestavíme uživatelské rozhraní se stránkou, kterou filtrovatelné mřížky. Zejména naše uživatelské rozhraní se bude skládat z řady LinkButtons pro...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044581"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>Vytvoření rozhraní pro výběr jednoho uživatelského účtu z mnoha (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> V tomto kurzu sestavíme uživatelské rozhraní se stránkou, kterou filtrovatelné mřížky. Zejména naše uživatelské rozhraní se bude skládat z řady prvků LinkButtons pro filtrování výsledků na základě počátečního písmene uživatelského jména a ovládacího prvku GridView pro zobrazení vyhovujících uživatelů. Začneme výpisem všech uživatelských účtů v prvku GridView. V kroku 3 potom přidáme filtr LinkButtons. Krok 4 vyhledá filtrované výsledky na stránkování. Rozhraní vytvořené v krocích 2 až 4 se použije v následujících kurzech k provádění úloh správy pro konkrétní uživatelský účet.

## <a name="introduction"></a>Úvod

V kurzu <a id="_msoanchor_1"></a> [*přiřazování rolí k uživatelům*](../roles/assigning-roles-to-users-vb.md) jsme vytvořili rozhraní základní, ve kterém může správce vybrat uživatele a spravovat jeho role. Konkrétně rozhraní prezentuje správce s rozevíracím seznamem všech uživatelů. Toto rozhraní je vhodné v případě, že existují i desítkové uživatelské účty, ale je nepraktický pro weby se stovkami nebo tisíci účtů. Stránkovaná tabulka, která se filtruje, je vhodnějším uživatelským rozhraním pro weby s velkými základy uživatelů.

V tomto kurzu vytvoříme takové uživatelské rozhraní. Zejména naše uživatelské rozhraní se bude skládat z řady prvků LinkButtons pro filtrování výsledků na základě počátečního písmene uživatelského jména a ovládacího prvku GridView pro zobrazení vyhovujících uživatelů. Začneme výpisem všech uživatelských účtů v prvku GridView. V kroku 3 potom přidáme filtr LinkButtons. Krok 4 vyhledá filtrované výsledky na stránkování. Rozhraní vytvořené v krocích 2 až 4 se použije v následujících kurzech k provádění úloh správy pro konkrétní uživatelský účet.

Pusťme se do toho.

## <a name="step-1-adding-new-aspnet-pages"></a>Krok 1: přidání nových stránek ASP.NET

V tomto kurzu a dalších dvou budeme zkoumat různé funkce a možnosti související se správou. K implementaci témat prověřených v rámci těchto kurzů budeme potřebovat řadu ASP.NET stránek. Pojďme vytvořit tyto stránky a aktualizovat mapu webu.

Začněte vytvořením nové složky v projektu s názvem `Administration` . V dalším kroku přidejte do složky dvě nové stránky ASP.NET a propojíte každou stránku se `Site.master` stránkou předlohy. Pojmenujte stránky:

- `ManageUsers.aspx`
- `UserInformation.aspx`

Přidejte také dvě stránky do kořenového adresáře webu: `ChangePassword.aspx` a `RecoverPassword.aspx` .

Tyto čtyři stránky by měly v tomto okamžiku mít dva ovládací prvky obsahu, jeden pro každý prvek prvků hlavní stránky: `MainContent` a `LoginContent` .

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

Pro `LoginContent` tyto stránky chceme pro prvky ContentPlaceHolder zobrazit výchozí označení stránky předlohy. Proto odeberte deklarativní označení pro `Content2` ovládací prvek obsahu. Až to uděláte, značky Pages by měly obsahovat jenom jeden ovládací prvek obsahu.

Stránky ASP.NET ve `Administration` složce jsou určené pouze pro uživatele s právy pro správu. Do systému jsme přidali roli správců v <a id="_msoanchor_2"></a> kurzu [*vytváření a Správa rolí*](../roles/creating-and-managing-roles-vb.md) ; omezení přístupu na tyto dvě stránky na tuto roli. Chcete-li to provést, přidejte `Web.config` soubor do `Administration` složky a nakonfigurujte jeho `<authorization>` element tak, aby připustit uživatele v roli správců a odepřeli všechny ostatní.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

V tomto okamžiku by Průzkumník řešení projektu vypadala podobně jako snímek obrazovky, který ukazuje obrázek 1.

[![Na web se přidaly čtyři nové stránky a Web.config soubor.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**Obrázek 1**: na web se přidaly čtyři nové stránky a `Web.config` soubor ([kliknutím zobrazíte obrázek v plné velikosti).](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png)

Nakonec aktualizujte mapu webu ( `Web.sitemap` ) tak, aby zahrnovala položku na `ManageUsers.aspx` stránce. Po `<siteMapNode>` Přidání pro kurzy rolí přidejte následující kód XML.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

Po aktualizaci mapy webu navštivte web prostřednictvím prohlížeče. Jak ukazuje obrázek 2, navigace na levé straně teď obsahuje položky pro kurzy pro správu.

[![Mapa webu zahrnuje uzel s názvem Správa uživatelů](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**Obrázek 2**: Mapa webu obsahuje uzel s názvem Správa uživatele ([kliknutím zobrazíte obrázek v plné velikosti).](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png)

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>Krok 2: výpis všech uživatelských účtů v prvku GridView

Naším koncovým cílem tohoto kurzu je vytvořit stránku, kterou lze filtrovat, pomocí které může správce vybrat uživatelský účet, který chcete spravovat. Pojďme začít výpisem *všech* uživatelů v prvku GridView. Až to bude hotové, přidáme rozhraní a funkce pro filtrování a stránkování.

Otevřete `ManageUsers.aspx` stránku ve `Administration` složce a přidejte prvek GridView, jeho nastavení na hodnotu `ID` `UserAccounts` za chvíli, napíšeme kód, který bude navazovat sadu uživatelských účtů k prvku GridView pomocí `Membership` `GetAllUsers` metody třídy. Jak je popsáno v předchozích kurzech, `GetAllUsers` Metoda vrátí `MembershipUserCollection` objekt, který je kolekcí `MembershipUser` objektů. Každý `MembershipUser` v kolekci obsahuje vlastnosti, například,, `UserName` `Email` `IsApproved` a tak dále.

Chcete-li zobrazit informace o požadovaném uživatelském účtu v prvku GridView, nastavte vlastnost prvku GridView `AutoGenerateColumns` na hodnotu false a přidejte BoundFields pro `UserName` , a `Email` `Comment` vlastnosti a CheckBoxFields pro `IsApproved` vlastnosti, a `IsLockedOut` `IsOnline` . Tuto konfiguraci lze použít prostřednictvím deklarativního kódu ovládacího prvku nebo pomocí dialogového okna pole. Obrázek 3 ukazuje snímek obrazovky dialogového okna pole po zrušení zaškrtnutí políčka automaticky generovat pole a přidání a nakonfigurování BoundFields a CheckBoxFields.

[![Přidat tři BoundFields a tři CheckBoxFields do prvku GridView.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**Obrázek 3**: přidejte do prvku GridView tři BoundFields a tři CheckBoxFields ([kliknutím zobrazíte obrázek v plné velikosti).](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png)

Po nakonfigurování prvku GridView se ujistěte, že jeho deklarativní označení vypadá takto:

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

Dále je potřeba napsat kód, který váže uživatelské účty k prvku GridView. Vytvořte metodu nazvanou `BindUserAccounts` k provedení této úlohy a pak ji zavolejte z `Page_Load` obslužné rutiny události na první stránku.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

Chvíli počkejte, než otestujete stránku pomocí prohlížeče. Jak ukazuje obrázek 4, zobrazí `UserAccounts` GridView uživatelské jméno, e-mailovou adresu a další informace o relevantním účtu pro všechny uživatele v systému.

[![Uživatelské účty jsou uvedeny v prvku GridView.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**Obrázek 4**: uživatelské účty jsou uvedeny v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png)).

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>Krok 3: filtrování výsledků podle prvního písmene uživatelského jména

V současné době se v `UserAccounts` prvku GridView zobrazují *všechny* uživatelské účty. Pro weby se stovkami nebo tisíci uživatelských účtů je nezbytné, aby uživatel mohl rychle zredukovali zobrazené účty. To lze provést přidáním filtru LinkButtons na stránku. Přidejte na stránku 27 LinkButtons: jeden s názvem vše společně s jedním LinkButton pro každé písmeno abecedy. Pokud návštěvník klikne na vše, zobrazí se v prvku GridView všechny uživatele. Pokud kliknete na konkrétní písmeno, zobrazí se jenom uživatelé, jejichž uživatelské jméno začíná s vybraným písmenem.

Naším prvním úkolem je přidat do 27 ovládací prvky LinkButton. Jednou z možností je vytvořit 27 LinkButtons deklarativně, jeden po druhém. Pružnější přístup je použití ovládacího prvku Repeater s objektem `ItemTemplate` , který vykresluje LinkButton a následně váže možnosti filtrování na Repeater jako `String` pole.

Začněte přidáním ovládacího prvku Repeater na stránku nad ovládací prvek `UserAccounts` GridView. Nastavte `ID` Vlastnost Repeater pro `FilteringUI` konfiguraci šablon REPEAT tak, aby `ItemTemplate` vykreslía objekt LinkButton, jehož `Text` `CommandName` vlastnosti a jsou svázány s aktuálním elementem pole. Jak jsme viděli v kurzu <a id="_msoanchor_3"></a> [*přiřazování rolí uživatelům*](../roles/assigning-roles-to-users-vb.md) , můžete to udělat pomocí `Container.DataItem` syntaxe datové vazby. `SeparatorTemplate`K zobrazení svislé čáry mezi jednotlivými odkazy použijte Repeater.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

K naplnění tohoto opakovače pomocí požadovaných možností filtrování vytvořte metodu s názvem `BindFilteringUI` . Nezapomeňte zavolat tuto metodu z `Page_Load` obslužné rutiny události při prvním načtení stránky.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

Tato metoda určuje možnosti filtrování jako prvky v poli `String` `filterOptions` pro každý prvek v poli, opakuje vykreslí LinkButton s jeho `Text` `CommandName` vlastnostmi a přiřazenými k hodnotě elementu pole.

Obrázek 5 zobrazuje `ManageUsers.aspx` stránku při prohlížení v prohlížeči.

[![Repeater obsahuje 27 pro filtrování LinkButtons](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**Obrázek 5**: Repeater obsahuje 27 filtrů LinkButtons ([kliknutím zobrazíte obrázek v plné velikosti](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png)).

> [!NOTE]
> Uživatelská jména mohou začínat libovolným znakem, včetně čísel a interpunkce. Aby bylo možné zobrazit tyto účty, bude muset správce použít možnost všechny možnosti LinkButton. Alternativně můžete přidat LinkButton, který vrátí všechny uživatelské účty, které začínají číslem. Tuto funkci mám jako cvičení pro čtenáře.

Kliknutím na některý z filtrovacích LinkButtonů dojde k postbacku a dojde k `ItemCommand` vyvolání události opakování, ale v mřížce se nemění, protože ještě jsme napsali kód pro filtrování výsledků. `Membership`Třída obsahuje [ `FindUsersByName` metodu](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) , která vrátí tyto uživatelské účty, jejichž uživatelské jméno odpovídá zadanému vyhledávacímu vzoru. Tuto metodu můžeme použít k načtení pouze těch uživatelských účtů, jejichž uživatelské jméno začíná písmenem určeným pomocí `CommandName` filtrovaného typu LinkButton, na který jste klikli.

Začněte aktualizací `ManageUser.aspx` třídy kódu na pozadí stránky tak, aby obsahovala vlastnost s názvem `UsernameToMatch` Tato vlastnost uchovává řetězec filtru uživatelského jména v rámci zpětného odeslání:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch`Vlastnost ukládá její hodnotu, která je přiřazena do `ViewState` kolekce pomocí klíče ' usernameToMatch '. Je-li hodnota této vlastnosti čtena, zkontroluje, zda v kolekci existuje hodnota `ViewState` . Pokud ne, vrátí výchozí hodnotu prázdný řetězec. `UsernameToMatch`Vlastnost vykazuje společný vzor, což znamená zachování hodnoty pro zobrazení stavu, aby všechny změny vlastnosti byly trvale v rámci zpětného odeslání. Další informace o tomto modelu najdete v tématu [Principy stavu zobrazení ASP.NET](https://msdn.microsoftn-us/library/ms972976.aspx).

Dále aktualizujte `BindUserAccounts` metodu tak, aby namísto volání `Membership.GetAllUsers` volána, `Membership.FindUsersByName` `UsernameToMatch` předávala hodnotu vlastnosti připojené se zástupným znakem SQL,%.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

Chcete-li zobrazit pouze ty uživatele, jejichž uživatelské jméno začíná písmenem A, nastavte `UsernameToMatch` vlastnost na hodnotu a pak volání `BindUserAccounts` tohoto by vedlo k volání `Membership.FindUsersByName("A%")` , které vrátí všechny uživatele, jejichž uživatelské jméno začíná na. Podobně, pro vrácení *všech* uživatelů, přiřazení prázdného řetězce k `UsernameToMatch` vlastnosti tak, aby `BindUserAccounts` Metoda vyvolala a `Membership.FindUsersByName("%")` vrátila všechny uživatelské účty.

Vytvořte obslužnou rutinu události pro `ItemCommand` událost Repeater. Tato událost se vyvolá vždy, když se klikne na jeden z filtrů LinkButtons; je předána hodnota prvku LinkButton po kliknutí `CommandName` prostřednictvím `RepeaterCommandEventArgs` objektu. Pro vlastnost musíme přiřadit příslušnou hodnotu `UsernameToMatch` a pak zavolat `BindUserAccounts` metodu. Pokud `CommandName` je to vše, přiřaďte prázdný řetězec k `UsernameToMatch` , aby se zobrazily všechny uživatelské účty. V opačném případě přiřaďte `CommandName` hodnotu `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

Když je tento kód na místě, otestujte funkce filtrování. Při prvním navštívení stránky se zobrazí všechny uživatelské účty (viz obrázek 5). Kliknutím na prvek LinkButton dojde k zpětnému odeslání a filtrování výsledků, zobrazení pouze těch uživatelských účtů, které začínají na.

[![Pomocí filtrování LinkButtons zobrazíte uživatele, jejichž uživatelské jméno začíná určitým písmenem.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**Obrázek 6**: pomocí filtrování LinkButtons zobrazíte uživatele, jejichž uživatelské jméno začíná určitým písmenem ([kliknutím zobrazíte obrázek v plné velikosti).](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png)

## <a name="step-4-updating-the-gridview-to-use-paging"></a>Krok 4: aktualizace prvku GridView na použití stránkování

Prvek GridView zobrazený na obrázcích 5 a 6 zobrazí seznam všech záznamů vrácených z `FindUsersByName` metody. Pokud máte stovky nebo tisíce uživatelských účtů, může to vést k přetížení informací při zobrazení všech účtů (stejně jako případ při kliknutí na vše na webu nebo při počáteční návštěvě stránky). Chcete-li zobrazit uživatelské účty ve více spravovatelných blocích, nakonfigurujeme prvek GridView tak, aby zobrazoval 10 uživatelských účtů najednou.

Ovládací prvek GridView nabízí dva typy stránkování:

- **Výchozí stránkování** – snadno se implementuje, ale neefektivně. V kostce s výchozím stránkováním ovládací prvek GridView očekává *všechny* záznamy z jejího zdroje dat. Pak zobrazí jenom odpovídající stránku záznamů.
- **Vlastní stránkování** – vyžaduje implementaci více práce, ale je efektivnější než výchozí stránkování, protože s vlastním stránkováním vrátí zdroj dat pouze přesnou sadu záznamů, které se mají zobrazit.

Rozdíl mezi výchozím a vlastním stránkováním může být po stránkování v tisících záznamů poměrně podstatný. Vzhledem k tomu, že toto rozhraní sestavíme za předpokladu, že se může jednat o stovky nebo tisíce uživatelských účtů, použijte vlastní stránkování.

> [!NOTE]
> Podrobnější diskuzi o rozdílech mezi výchozím a vlastním stránkováním a také s problémy, které se týkají implementace vlastního stránkování, najdete v tématu [efektivní stránkování prostřednictvím velkých objemů dat](https://asp.net/learn/data-access/tutorial-25-vb.aspx). Analýzu rozdílu výkonu mezi výchozími a vlastními stránkováními najdete v tématu [vlastní stránkování v ASP.NET s SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx).

K implementaci vlastního stránkování musíme nejdřív potřebovat nějaký mechanismus, pomocí kterého načtete přesnou podmnožinu záznamů, které se zobrazí v prvku GridView. Dobrá zpráva je, že `Membership` `FindUsersByName` Metoda třídy má přetížení, které nám umožňuje určit index stránky a velikost stránky a vrátí pouze takové uživatelské účty, které spadají do daného rozsahu záznamů.

Konkrétně toto přetížení má následující signaturu: [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) .

Parametr *pageIndex* Určuje stránku uživatelských účtů, které se mají vrátit. *PageSize* označuje počet záznamů, které se mají zobrazit na stránce. Parametr *totalRecords* je `ByRef` parametr, který vrací celkový počet uživatelských účtů v úložišti uživatele.

> [!NOTE]
> Data vrácená nástrojem `FindUsersByName` jsou řazena podle uživatelského jména; kritéria řazení nelze přizpůsobit.

Prvek GridView lze nakonfigurovat tak, aby využíval vlastní stránkování, ale pouze v případě, že je svázán s ovládacím prvkem ObjectDataSource. Pro ovládací prvek ObjectDataSource pro implementaci vlastního stránkování vyžaduje dvě metody: jeden, který je předán indexu počátečního řádku, a maximální počet zobrazených záznamů a vrací přesné podmnožiny záznamů, které spadají do daného rozsahu. a metodu, která vrátí celkový počet záznamů, které jsou stránkou. `FindUsersByName`Přetížení akceptuje index stránky a velikost stránky a vrátí celkový počet záznamů prostřednictvím `ByRef` parametru. A tady je neshoda rozhraní.

Jednou z možností je vytvořit proxy třídu, která zpřístupňuje rozhraní, které prvek ObjectDataSource očekává, a pak interně zavolá `FindUsersByName` metodu. Další možnost – a ta, kterou budeme používat pro tento článek, je vytvořit vlastní rozhraní stránkování a použít ho místo předdefinovaného rozhraní stránkování prvku GridView.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>Vytvoření prvního, předchozího, následujícího, posledního stránkovacího rozhraní

Pojďme sestavit rozhraní stránkování s prvními, předchozími, dalšími a posledními LinkButtons. První LinkButton, při kliknutí, převezme uživatele na první stránku dat, zatímco předchozí se vrátí na předchozí stránku. Podobně, další a poslední přesune uživatele na další a poslední stránku v uvedeném pořadí. Přidejte čtyři ovládací prvky LinkButton pod `UserAccounts` prvek GridView.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

Dále vytvořte obslužnou rutinu události pro každou z `Click` událostí LinkButton.

Obrázek 7 zobrazuje čtyři LinkButtony při zobrazení pomocí zobrazení Návrh aplikace Visual Web Developer.

[![Přidat první, předchozí, další a poslední LinkButtons pod prvek GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**Obrázek 7**: Přidání prvního, předchozího, následujícího a posledního prvku LinkButtons pod prvek GridView ([kliknutím zobrazíte obrázek v plné velikosti](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))

### <a name="keeping-track-of-the-current-page-index"></a>Udržování přehledu o aktuálním indexu stránky

Když uživatel poprvé navštíví `ManageUsers.aspx` stránku nebo klikne na jedno z filtrovacích tlačítek, chceme zobrazit první stránku dat v prvku GridView. Když však uživatel klikne na jeden z navigačních LinkButtonů, musíme aktualizovat index stránky. Chcete-li zachovat index stránky a počet záznamů, které se mají zobrazit na stránce, přidejte následující dvě vlastnosti do třídy kódu na pozadí stránky:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

Podobně jako `UsernameToMatch` vlastnost `PageIndex` vlastnost uchovává svou hodnotu pro zobrazení stavu. Vlastnost jen pro čtení `PageSize` vrací pevně zakódované hodnoty 10. Pozváním ke stejnému čtenáři, aby tuto vlastnost aktualizovala tak, aby používalo stejný vzor jako `PageIndex` , a následně pro rozšíření `ManageUsers.aspx` stránky tak, aby osoba, která navštíví stránku, mohla určit, kolik uživatelských účtů se má zobrazit na stránce.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>Načítání pouze záznamů aktuální stránky, aktualizace indexu stránky a povolení a zakázání stránkovacího rozhraní LinkButtons

Po zaplnění stránkovacího rozhraní a `PageIndex` `PageSize` Přidání vlastností a je připraveno aktualizovat `BindUserAccounts` metodu tak, aby používala příslušné `FindUsersByName` přetížení. Kromě toho musíme tuto metodu povolit nebo zakázat stránkování rozhraní v závislosti na tom, která stránka se zobrazuje. Při prohlížení první stránky dat by se měla vypnout první a předchozí propojení. Při prohlížení poslední stránky by měla být zakázána další a poslední.

Aktualizujte `BindUserAccounts` metodu následujícím kódem:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

Všimněte si, že celkový počet záznamů, které jsou stránkou, je určen posledním parametrem `FindUsersByName` metody. Po vrácení zadané stránky uživatelských účtů jsou čtyři LinkButtons buď povoleny, nebo zakázány v závislosti na tom, zda je zobrazena první nebo poslední stránka dat.

Posledním krokem je napsat kód pro čtyři `Click` obslužné rutiny událostí LinkButtons. Tyto obslužné rutiny události musí aktualizovat `PageIndex` vlastnost a poté znovu navazovat vazby na ovládací prvek GridView prostřednictvím volání `BindUserAccounts` první, předchozí a další obslužné rutiny události jsou velmi jednoduché. `Click`Obslužná rutina události pro poslední LinkButton je ale trochu složitější, protože potřebujeme určit, kolik záznamů se zobrazuje, aby bylo možné určit poslední index stránky.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

Obrázky 8 a 9 ukazují vlastní rozhraní stránkování v akci. Obrázek 8 zobrazuje `ManageUsers.aspx` stránku při prohlížení první stránky dat pro všechny uživatelské účty. Všimněte si, že se zobrazí pouze 10 účtů 13. Kliknutí na další nebo poslední odkaz způsobí postback, aktualizuje na `PageIndex` 1 a vytvoří vazbu druhé stránky uživatelských účtů k mřížce (viz obrázek 9).

[![Zobrazí se prvních 10 uživatelských účtů.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**Obrázek 8**: zobrazí se prvních 10 uživatelských účtů ([kliknutím zobrazíte obrázek v plné velikosti](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png)).

[![Kliknutím na další odkaz se zobrazí druhá stránka uživatelských účtů.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**Obrázek 9**: kliknutí na další odkaz zobrazí druhou stránku uživatelských účtů ([kliknutím zobrazíte obrázek v plné velikosti).](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png)

## <a name="summary"></a>Souhrn

Správci často potřebují vybrat uživatele ze seznamu účtů. V předchozích kurzech jsme se podívali na používání rozevíracího seznamu naplněný uživateli, ale tento postup se nedokáže dobře škálovat. V tomto kurzu jsme prozkoumali lepší alternativu: filtrovací rozhraní, jehož výsledky se zobrazují ve stránkovém prvku GridView. Pomocí tohoto uživatelského rozhraní můžou správci rychle a efektivně najít a vybrat jeden uživatelský účet mezi tisíci.

Šťastné programování!

### <a name="further-reading"></a>Další materiály

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vlastní stránkování v ASP.NET s SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [Efektivní stránkování prostřednictvím velkých objemů dat](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [Postup při zavedení vlastního nástroje pro správu webu](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott se dá kontaktovat na [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) blogu nebo přes jeho blog na adrese [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Alicja Maziarz. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte čáru na

> [!div class="step-by-step"]
> [Předchozí](unlocking-and-approving-user-accounts-cs.md) 
>  [Další](recovering-and-changing-passwords-vb.md)
