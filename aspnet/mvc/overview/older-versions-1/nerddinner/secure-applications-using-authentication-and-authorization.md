---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Zabezpečené aplikace pomocí ověřování a autorizace | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 9 ukazuje, jak přidat ověřování a autorizaci pro zabezpečení naší aplikace NerdDinner, takže uživatelé se musí zaregistrovat a přihlásit se k webu, aby vytvořili...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542570"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Zabezpečení aplikací ověřováním a autorizací

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 9 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 9 ukazuje, jak přidat ověřování a autorizaci k zabezpečení naší aplikace NerdDinner, takže uživatelé se musí zaregistrovat a přihlásit se k webu, aby vytvořili nové večeře, a pouze uživatel, který hostuje večeři, ji může později upravit.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner Krok 9: Ověřování a autorizace

Právě teď naše aplikace NerdDinner uděluje každému, kdo navštíví stránky, možnost vytvářet a upravovat podrobnosti o každé večeři. Změníme to tak, aby se uživatelé museli zaregistrovat a přihlásit k webu, aby vytvořili nové večeře, a přidejte omezení tak, aby jej později mohl upravit pouze uživatel, který hostuje večeři.

K tomu to použijeme k zabezpečení naší aplikace pomocí ověřování a autorizace.

### <a name="understanding-authentication-and-authorization"></a>Principy ověřování a autorizace

*Ověřování* je proces identifikace a ověření identity klienta přistupujícího k aplikaci. Jednodušeji řečeno, je to o identifikaci "kdo" koncový uživatel je, když navštíví webové stránky. ASP.NET podporuje několik způsobů ověřování uživatelů prohlížeče. U internetových webových aplikací se nejběžnější používaný přístup ověřování nazývá "Ověřování pomocí formulářů". Ověřování pomocí formulářů umožňuje vývojáři vytvořit přihlašovací formulář HTML v rámci své aplikace a potom ověřit uživatelské jméno nebo heslo, které koncový uživatel odešle v databázi nebo jiném úložišti pověření heslem. Pokud je kombinace uživatelského jména a hesla správná, může vývojář požádat ASP.NET o vydání šifrovaného souboru cookie HTTP, který identifikuje uživatele v rámci budoucích požadavků. Budeme pomocí ověřování pomocí formulářů s naší aplikace NerdDinner.

*Autorizace* je proces určení, zda má ověřený uživatel oprávnění k přístupu k určité adrese URL nebo prostředku nebo k provedení určité akce. Například v rámci naší aplikace NerdDinner budeme chtít autorizovat, že pouze uživatelé, kteří jsou přihlášeni, mají přístup k *adrese /Dinners/Create* URL a vytvořit nové večeře. Budeme také chtít přidat logiku autorizace tak, aby ji mohl upravovat pouze uživatel, který hostuje večeři – a odepřít přístup k úpravám všem ostatním uživatelům.

### <a name="forms-authentication-and-the-accountcontroller"></a>Ověřování pomocí formulářů a accountcontroller

Výchozí šablona projektu sady Visual Studio pro ASP.NET MVC automaticky povolí ověřování pomocí formulářů při vytváření nových aplikací ASP.NET MVC. Automaticky také přidává do projektu předem vytvořenou implementaci přihlašovací stránky účtu - což umožňuje opravdu snadné integrovat zabezpečení v rámci webu.

Výchozí stránka předlohy Site.master zobrazuje odkaz "Přihlásit se" v pravém horním rohu webu, když uživatel, který k ní přistupuje, není ověřen:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

Kliknutím na odkaz "Přihlásit se" přenesete uživatele na adresu URL */Account/LogOn:*

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Návštěvníci, kteří se nezaregistrovali, tak mohou učinit kliknutím na odkaz "Registrovat", který je přenese na adresu URL */Účet/Registr a* umožní jim zadat podrobnosti o účtu:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

Kliknutím na tlačítko "Registrovat" vytvoříte nového uživatele v rámci systému členství ASP.NET a ověříte uživatele na webu pomocí ověřování pomocí formulářů.

Když je uživatel přihlášen, site.master změní vpravo nahoře na stránce a vyjádřil "Welcome [uživatelské jméno]!" a vykreslí odkaz "Odhlásit" namísto "Přihlásit" jeden. Kliknutím na odkaz "Odhlásit" odhlásí uživatele:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

Výše uvedené přihlašovací, odhlašovací a registrační funkce je implementována v rámci AccountController třídy, která byla přidána do našeho projektu Visual Studio při vytvoření projektu. Uživatelské rozhraní pro AccountController je implementováno pomocí šablon zobrazení v adresáři \Views\Account:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

Třída AccountController používá systém ověřování ASP.NET formulářů k vydávání šifrovaných ověřovacích souborů cookie a ASP.NET rozhraní API členství k ukládání a ověřování uživatelských jmen/hesel. Rozhraní API pro ASP.NET členství je rozšiřitelné a umožňuje použití libovolného úložiště přihlašovacích údajů hesla. ASP.NET dodává s předdefinované implementace poskytovatele členství, které ukládají uživatelské jméno nebo hesla v databázi SQL nebo ve službě Active Directory.

Můžeme nakonfigurovat, který poskytovatel členství naše aplikace NerdDinner by měla používat otevřením souboru "web.config" v kořenovém adresáři projektu a hledáním &lt;části členství&gt; v něm. Výchozí web.config, který byl přidán při vytvoření projektu, zaregistruje poskytovatele členství SQL a nakonfiguruje jej tak, aby k určení umístění databáze použil připojovací řetězec s názvem ApplicationServices.

Výchozí připojovací řetězec ApplicationServices (který &lt;je&gt; určen v části connectionStrings souboru web.config) je nakonfigurován pro použití služby SQL Express. Odkazuje na databázi SQL Express s názvem "ASPNETDB. MDF" v adresáři aplikace\_"App Data". Pokud tato databáze neexistuje při prvním použití rozhraní API členství v rámci aplikace, ASP.NET automaticky vytvoří databázi a zřídí příslušné schéma databáze členství v ní:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

Pokud místo použití SQL Express jsme chtěli použít úplnou instanci SQL Server (nebo se připojit ke vzdálené databázi), vše, co bychom potřebovali provést, je aktualizovat připojovací řetězec "ApplicationServices" v souboru web.config a ujistěte se, že příslušné schéma členství bylo přidáno do databáze, na kterou odkazuje. Pomocí nástroje aspnet\_regsql.exe můžete spustit v adresáři \Windows\Microsoft.NET\Framework\v2.0.50727\ a přidat do databáze příslušné schéma pro členství a další ASP.NET aplikačních služeb.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>Autorizace adresy URL /Dinners/Create pomocí filtru [Autorizovat]

Nemuseli jsme psát žádný kód, který by umožnil zabezpečené ověřování a implementaci správy účtů pro aplikaci NerdDinner. Uživatelé mohou zaregistrovat nové účty s naší aplikací, a přihlášení / odhlášení z webu.

Nyní můžeme do aplikace přidat logiku autorizace a použít stav ověřování a uživatelské jméno návštěvníků k řízení toho, co mohou a nemohou dělat v rámci webu. Začněme přidáním logiky autorizace do metod akce "Vytvořit" naší třídy DinnersController. Konkrétně budeme vyžadovat, aby uživatelé, kteří přistupují k adrese *URL /Dinners/Create,* museli být přihlášeni. Pokud nejsou přihlášeni, přesměrujeme je na přihlašovací stránku, aby se mohli přihlásit.

Implementace této logiky je docela snadné. Vše, co potřebujeme provést, je přidat atribut filtru [Authorize] do našich metod akce Vytvořit takto:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC podporuje možnost vytvářet "filtry akcí", které lze použít k implementaci opakovaně použitelné logiky, která může být deklarativně použita pro metody akce. Filtr [Authorize] je jedním z předdefinovaných filtrů akcí poskytovaných ASP.NET MVC a umožňuje vývojáři deklarativně aplikovat autorizační pravidla na metody akce a třídy kontroleru.

Při použití bez jakýchkoli parametrů (jako výše) filtr [Authorize] vynucuje, že uživatel, který požaduje metodu akce, musí být přihlášen – a pokud není, automaticky přesměruje prohlížeč na přihlašovací adresu URL. Při tomto přesměrování je původně požadovaná adresa URL předána jako argument řetězce dotazu (například: /Account/LogOn? ReturnUrl=%2fDinners%2fCreate). AccountController pak přesměruje uživatele zpět na původně požadovanou adresu URL po přihlášení.

Filtr [Authorize] volitelně podporuje možnost zadat vlastnost "Users" nebo "Roles", která může být použita k vyžadování, že uživatel je přihlášen i v rámci seznamu povolených uživatelů nebo členem povolené role zabezpečení. Například níže uvedený kód umožňuje dvěma konkrétním uživatelům, "scottgu" a "billg", přístup /Dinners/Create URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Vkládání konkrétních uživatelských jmen v rámci kódu má tendenci být docela un-udržovatelné ačkoli. Lepším přístupem je definovat vyšší úroveň "role", které kód kontroluje proti a pak mapovat uživatele do role pomocí databáze nebo systému active directory (povolení skutečného seznamu mapování uživatelů, které mají být uloženy externě z kódu). ASP.NET obsahuje integrované rozhraní API pro správu rolí a také integrovanou sadu poskytovatelů rolí (včetně těch pro SQL a Active Directory), které mohou pomoci s prováděním tohoto mapování uživatelů nebo rolí. Pak můžeme aktualizovat kód tak, aby umožňoval uživatelům v rámci konkrétní role správce přístup k adrese /Dinners/Create URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Použití vlastnosti User.Identity.Name při vytváření večeří

Můžeme načíst uživatelské jméno aktuálně přihlášeného uživatele požadavku pomocí vlastnosti User.Identity.Name vystavené v základní třídě řadiče.

Dříve, když jsme implementovali http-post verzi naší Create() metody akce jsme hardcoded "HostedBy" vlastnost Dinner na statický řetězec. Nyní můžeme aktualizovat tento kód místo použití User.Identity.Name vlastnost, stejně jako automaticky přidat RSVP pro hostitele vytváření večeři:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Protože jsme přidali atribut [Authorize] do metody Create(), ASP.NET MVC zajistí, že metoda akce se spustí pouze v případě, že uživatel, který navštíví adresu URL /Dinners/Create, je přihlášen na webu. Jako takové User.Identity.Name hodnota vlastnosti bude vždy obsahovat platné uživatelské jméno.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Použití vlastnosti User.Identity.Name při úpravách večeří

Nyní přidáme nějakou logiku autorizace, která omezuje uživatele tak, aby mohli upravovat pouze vlastnosti večeří, které sami hostují.

Chcete-li pomoci s tím, nejprve přidáme "IsHostedBy(uživatelské jméno)" pomocnou metodu do našeho objektu Dinner (v rámci Dinner.cs částečné třídy, kterou jsme vytvořili dříve). Tato pomocná metoda vrátí true nebo false v závislosti na tom, zda zadané uživatelské jméno odpovídá Večeři HostedBy vlastnost a zapouzdřuje logiku potřebnou k provedení porovnání řetězce bez rozlišování velkých a malých písmen z nich:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Potom přidáme atribut [Authorize] do metod akce Edit() v rámci naší třídy DinnersController. Tím zajistíte, že uživatelé musí být přihlášeni, aby požadovali adresu URL */Dinners/Edit/[id].*

Potom můžeme přidat kód do našich Edit metody, které používá Dinner.IsHostedBy(uživatelské jméno) pomocná metoda k ověření, že přihlášený uživatel odpovídá Večeři hostitele. Pokud uživatel není hostitelem, zobrazíse zobrazení "InvalidOwner" a požadavek ukončíme. Kód k tomu vypadá takto:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Potom můžeme kliknout pravým tlačítkem myši na adresář \Views\Dinners a vybrat příkaz nabídky Přidat-&gt;zobrazení a vytvořit tak nové zobrazení "InvalidOwner". Naplníme ji níže uvedenou chybovou zprávou:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

A teď, když se uživatel pokusí upravit večeři, kterou nevlastní, zobrazí se chybová zpráva:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Můžeme opakovat stejné kroky pro Delete() metody akce v rámci našeho řadiče uzamknout oprávnění k odstranění Dinners také a ujistěte se, že pouze hostitel Dinner můžete odstranit.

### <a name="showinghiding-edit-and-delete-links"></a>Zobrazení/skrytí odkazů pro úpravy a odstranění

Odkazujeme na metodu akce Upravit a odstranit naší třídy DinnersController z naší adresy URL podrobností:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

V současné době zobrazujeme odkazy akce Upravit a odstranit bez ohledu na to, zda je návštěvník adresy URL podrobností hostitelem večeře. Změníme to tak, aby odkazy byly zobrazeny pouze v případě, že hostující uživatel je vlastníkem večeře.

Details() metoda akce v rámci našeDinnersController načte Dinner objekt a pak předá jako objekt modelu naší šabloně zobrazení:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Můžeme aktualizovat naše zobrazení šablony podmíněně zobrazit / skrýt upravit a odstranit odkazy pomocí Dinner.IsHostedBy() pomocná metoda, jako je níže:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Další kroky

Podívejme se nyní na to, jak můžeme umožnit ověřeným uživatelům RSVP pro večeře pomocí AJAX.

> [!div class="step-by-step"]
> [Předchozí](implement-efficient-data-paging.md)
> [další](use-ajax-to-deliver-dynamic-updates.md)
