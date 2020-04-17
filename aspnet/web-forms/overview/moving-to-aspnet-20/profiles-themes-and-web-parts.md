---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Profily, motivy a webové části | Dokumenty společnosti Microsoft
author: rick-anderson
description: V ASP.NET 2.0 došlo k významným změnám v konfiguraci a instrumentaci. Nové konfigurační rozhraní API ASP.NET umožňuje provést změny konfigurace pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: 4bc98cca226a0bd9bd766a21e88b0facf2a4b610
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543636"
---
# <a name="profiles-themes-and-web-parts"></a>Profily, motivy a webové části

podle [společnosti Microsoft](https://github.com/microsoft)

> V ASP.NET 2.0 došlo k významným změnám v konfiguraci a instrumentaci. Nové konfigurační rozhraní API ASP.NET umožňuje provádění změn konfigurace programově. Kromě toho existuje mnoho nových nastavení konfigurace umožňují nové konfigurace a instrumentace.

ASP.NET 2.0 představuje podstatné zlepšení v oblasti personalizovaných webových stránek. Kromě funkcí členství, které jsme již pokryli, ASP.NET profily, motivy a webové části výrazně zvyšují personalizaci na webových stránkách.

## <a name="aspnet-profiles"></a>ASP.NET profily

ASP.NET profily jsou podobné relacím. Rozdíl je v tom, že profil je trvalý, zatímco relace je ztracena při zavření prohlížeče. Dalším velkým rozdílem mezi relacemi a profily je, že profily jsou silně zadávány, a proto vám během procesu vývoje poskytuje technologie IntelliSense.

Profil je definován v konfiguračním souboru počítačů nebo v souboru web.config pro aplikaci. (Profil nelze definovat v souboru web.config podsložek.) Níže uvedený kód definuje profil pro uložení prvního a příjmení návštěvníků webu.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

Výchozí datový typ vlastnosti profilu je System.String. Ve výše uvedeném příkladu nebyl zadán žádný datový typ. Proto firstname a lastname vlastnosti jsou oba typu String. Jak již bylo zmíněno, vlastnosti profilu jsou silně zadávány. Níže uvedený kód přidá novou vlastnost pro stáří, která je typu Int32.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Profily se obvykle používají s ověřováním ASP.NET formulářů. Při použití v kombinaci s ověřováním pomocí formulářů má každý uživatel samostatný profil přidružený k id uživatele. Je však také možné povolit použití profilů v &lt;anonymní&gt; aplikaci pomocí prvku anonymousIdentification v konfiguračním souboru spolu s atributem **allowAnonymous,** jak je znázorněno níže:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Když anonymní uživatel prochází web, ASP.NET vytvoří instanci **ProfileCommon** pro uživatele. Tento profil používá jedinečné ID uložené v souboru cookie v prohlížeči k identifikaci uživatele jako jedinečného návštěvníka. Tímto způsobem můžete ukládat informace o profilu pro uživatele, kteří procházejí anonymně.

## <a name="profile-groups"></a>Skupiny profilů

Je možné seskupit vlastnosti profilů. Seskupením vlastností je možné simulovat více profilů pro konkrétní aplikaci.

Následující konfigurace konfiguruje vlastnost FirstName a LastName pro dvě skupiny. Kupující a vyhlídky.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Poté je možné nastavit vlastnosti pro určitou skupinu takto:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Ukládání složitých objektů

Příklady, které jsme prohledali, zatím v profilu uložily jednoduché datové typy. Je také možné ukládat komplexní datové typy v profilu zadáním metody serializace pomocí **serializeAs** atribut takto:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

V tomto případě je typem PurchaseInvoice. Třída PurchaseInvoice musí být označena jako serializovatelná a může obsahovat libovolný počet vlastností. Například pokud PurchaseInvoice má vlastnost s názvem **NumItemsPurchased**, můžete odkazovat na tuto vlastnost v kódu takto:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Dědičnost profilu

Je možné vytvořit profil pro použití ve více aplikacích. Vytvořením třídy profilu, která je odvozena z ProfileBase, můžete znovu použít profil v několika aplikacích pomocí atributu **inherits,** jak je znázorněno níže:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

V tomto případě třídy **PurchasingProfile** bude vypadat takto:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Zprostředkovatelé profilů

ASP.NET profily používají model zprostředkovatele. Výchozí zprostředkovatel ukládá informace v databázi SQL\_Server Express ve složce Data aplikace webové aplikace pomocí zprostředkovatele SqlProfileProvider. Pokud databáze neexistuje, ASP.NET ji automaticky vytvoří, když se profil pokusí uložit informace.

V některých případech však můžete chtít vytvořit vlastního poskytovatele profilu. Funkce ASP.NET profilu umožňuje snadné použití různých poskytovatelů.

Vlastního poskytovatele profilu se vytvoří, když:

- Je třeba ukládat informace o profilu ve zdroji dat, například v databázi FoxPro nebo v databázi Oracle, která není podporována zprostředkovateli profilu, kteří jsou součástí rozhraní .NET Framework.
- Je třeba spravovat informace o profilu pomocí schématu databáze, které se liší od schématu databáze používaného zprostředkovateli, kteří jsou součástí rozhraní .NET Framework. Běžným příkladem je, že chcete integrovat informace o profilu s uživatelskými daty v existující databázi serveru SQL Server.

### <a name="required-classes"></a>Požadované třídy

Chcete-li implementovat zprostředkovatele profilu, vytvořte třídu, která dědí abstraktní třídu System.Web.Profile.ProfileProvider. Abstraktní třída **ProfileProvider** zase zdědí abstraktní třídu System.Configuration.SettingsProvider, která zdědí abstraktní třídu System.Configuration.Provider.ProviderBase. Z důvodu tohoto řetězce dědičnosti, kromě požadovaných členů **ProfileProvider** třídy, je nutné implementovat požadované členy **SettingsProvider** a **ProviderBase** třídy.

Následující tabulky popisují vlastnosti a metody, které je nutné implementovat z abstraktních tříd **ProviderBase**, **SettingsProvider**a **ProfileProvider.**

### <a name="providerbase-members"></a>Členové ProviderBase

| **Člen** | **Popis** |
| --- | --- |
| Initialize – metoda | Bere jako vstup název instance zprostředkovatele a NameValueCollection nastavení konfigurace. Slouží k nastavení možností a hodnot vlastností instance zprostředkovatele, včetně hodnot a možností specifických pro implementaci určených v konfiguraci počítače nebo souboru Web.config. |

### <a name="settingsprovider-members"></a>Členové Uživatele SettingsProvider

| **Člen** | **Popis** |
| --- | --- |
| ApplicationName, vlastnost | Název aplikace, který je uložen s každým profilem. Zprostředkovatel profilu používá název aplikace k samostatnému ukládání informací o profilu pro každou aplikaci. To umožňuje více ASP.NET aplikacím používat stejný zdroj dat bez konfliktu, pokud je v různých aplikacích vytvořeno stejné uživatelské jméno. Alternativně více ASP.NET aplikací můžete sdílet zdroj dat profilu zadáním stejného názvu aplikace. |
| Metoda GetPropertyValues | Bere jako vstup SettingsContext a SettingsPropertyCollection objektu. **SettingsContext** poskytuje informace o uživateli. Tyto informace můžete použít jako primární klíč k načtení informací o vlastnostech profilu pro uživatele. Pomocí objektu **SettingsContext** získáte uživatelské jméno a zda je uživatel ověřen nebo anonymní. **SettingsPropertyCollection** obsahuje kolekci SettingsProperty objekty. Každý objekt **SettingsProperty** poskytuje název a typ vlastnosti a další informace, jako je například výchozí hodnota vlastnosti a zda je vlastnost jen pro čtení. Metoda **GetPropertyValues** naplní objekty SettingsPropertyValueCollection objekty SettingsPropertyValue založenými na objektech **SettingsProperty,** které jsou poskytnuty jako vstup. Hodnoty ze zdroje dat pro určeného uživatele jsou přiřazeny vlastnostem PropertyValue pro každý objekt **SettingsPropertyValue** a je vrácena celá kolekce. Volání metody také aktualizuje hodnotu LastActivityDate pro zadaný profil uživatele na aktuální datum a čas. |
| Metoda SetPropertyValues | Bere jako vstup **SettingsContext** a **SettingsPropertyValueCollection** objektu. **SettingsContext** poskytuje informace o uživateli. Tyto informace můžete použít jako primární klíč k načtení informací o vlastnostech profilu pro uživatele. Pomocí objektu **SettingsContext** získáte uživatelské jméno a zda je uživatel ověřen nebo anonymní. **PropertyPropertyCollection** obsahuje kolekci objektů **SettingsPropertyValue.** Každý objekt **SettingsPropertyValue** poskytuje název, typ a hodnotu vlastnosti a další informace, jako je například výchozí hodnota vlastnosti a zda je vlastnost jen pro čtení. Metoda **SetPropertyValues** aktualizuje hodnoty vlastností profilu ve zdroji dat pro určeného uživatele. Volání metody také aktualizuje **lastactivitydate** a lastupdateddate hodnoty pro zadaný profil uživatele na aktuální datum a čas. |

### <a name="profileprovider-members"></a>Členové ProfileProvider

| **Člen** | **Popis** |
| --- | --- |
| Metoda DeleteProfiles | Vezme jako vstup řetězec pole uživatelských jmen a odstraní ze zdroje dat všechny informace o profilu a hodnoty vlastností pro zadané názvy, kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Pokud zdroj dat podporuje transakce, doporučujeme zahrnout všechny operace odstranění do transakce a vrátit transakci zpět a vyvolat výjimku, pokud se nezdaří jakákoli operace odstranění. |
| Metoda DeleteProfiles | Bere jako vstup kolekce ProfileInfo objekty a odstraní ze zdroje dat všechny informace o profilu a hodnoty vlastností pro každý profil, kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Pokud zdroj dat podporuje transakce, doporučujeme zahrnout všechny operace odstranění do transakce a vrátit transakci zpět a vyvolat výjimku, pokud se nezdaří jakákoli operace odstranění. |
| DeleteInactiveProfiles metoda | Bere jako vstup ProfileAuthenticationOption hodnotu a DateTime objekt a odstraní ze zdroje dat všechny informace profilu a hodnoty vlastností, kde poslední datum aktivity je menší nebo rovno zadané datum a čas a kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Parametr **ProfileAuthenticationOption** určuje, zda mají být odstraněny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud zdroj dat podporuje transakce, doporučujeme zahrnout všechny operace odstranění do transakce a vrátit transakci zpět a vyvolat výjimku, pokud se nezdaří jakákoli operace odstranění. |
| Metoda GetAllProfiles | Bere jako vstup **ProfileAuthenticationOption** hodnotu, celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí profileinfocollection, který obsahuje **ProfileInfo** objekty pro všechny profily ve zdroji dat, kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Výsledky vrácené metodou **GetAllProfiles** jsou omezeny hodnotami indexu stránky a velikosti stránky. Hodnota velikosti stránky určuje maximální počet objektů **ProfileInfo,** které mají být vráceny v **kolekci ProfileInfoCollection**. Hodnota indexu stránky určuje, která stránka výsledků má být vrácena, kde 1 identifikuje první stránku. Parametr pro celkový počet záznamů je out parametr (můžete použít **ByRef** v jazyce Visual Basic), který je nastaven na celkový počet profilů. Například pokud úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, **ProfileInfoCollection** vrácena obsahuje šestý až desátý profily. Celková hodnota záznamů je nastavena na 13 při návratu metody. |
| Metoda GetAllInactiveProfiles | Bere jako vstupní **profileauthenticationoption** hodnotu, **DateTime** objekt, celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **profileinfocollection,** který obsahuje **ProfileInfo** objekty pro všechny profily ve zdroji dat, kde poslední datum aktivity je menší nebo rovno zadané **DateTime** a kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Výsledky vrácené metodou **GetAllInactiveProfiles** jsou omezeny hodnotami indexu stránky a velikosti stránky. Hodnota velikosti stránky určuje maximální počet objektů **ProfileInfo,** které mají být vráceny v **kolekci ProfileInfoCollection**. Hodnota indexu stránky určuje, která stránka výsledků má být vrácena, kde 1 identifikuje první stránku. Parametr pro celkový počet záznamů je out parametr (můžete použít **ByRef** v jazyce Visual Basic), který je nastaven na celkový počet profilů. Například pokud úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, **ProfileInfoCollection** vrácena obsahuje šestý až desátý profily. Celková hodnota záznamů je nastavena na 13 při návratu metody. |
| FindProfilesByUserName metoda | Bere jako vstup **ProfileAuthenticationOption** hodnotu, řetězec obsahující uživatelské jméno, celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **profileinfocollection,** který obsahuje **ProfileInfo** objekty pro všechny profily ve zdroji dat, kde uživatelské jméno odpovídá zadané uživatelské jméno a kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud zdroj dat podporuje další možnosti vyhledávání, například zástupné znaky, můžete poskytnout podrobnější možnosti vyhledávání pro uživatelská jména. Výsledky vrácené metodou **FindProfilesByUserName** jsou omezeny hodnotami indexu stránky a velikosti stránky. Hodnota velikosti stránky určuje maximální počet objektů **ProfileInfo,** které mají být vráceny v **kolekci ProfileInfoCollection**. Hodnota indexu stránky určuje, která stránka výsledků má být vrácena, kde 1 identifikuje první stránku. Parametr pro celkový počet záznamů je out parametr (můžete použít **ByRef** v jazyce Visual Basic), který je nastaven na celkový počet profilů. Například pokud úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, **ProfileInfoCollection** vrácena obsahuje šestý až desátý profily. Celková hodnota záznamů je nastavena na 13 při návratu metody. |
| Metoda FindInactiveProfilesByUserName | Bere jako vstup **ProfileAuthenticationOption** hodnotu, řetězec obsahující uživatelské jméno, **DateTime** objekt, celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **profil ProfileInfoCollection,** který obsahuje objekty **ProfileInfo** pro všechny profily ve zdroji dat, kde se uživatelské jméno shoduje se zadaným uživatelským jménem, kde je datum poslední aktivity menší nebo rovno zadanému **datetime**a kde název aplikace odpovídá hodnotě **vlastnosti ApplicationName.** Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud zdroj dat podporuje další možnosti vyhledávání, například zástupné znaky, můžete poskytnout podrobnější možnosti vyhledávání pro uživatelská jména. Výsledky vrácené metodou **FindInactiveProfilesByUserName** jsou omezeny hodnotami indexu stránky a velikosti stránky. Hodnota velikosti stránky určuje maximální počet objektů **ProfileInfo,** které mají být vráceny v **kolekci ProfileInfoCollection**. Hodnota indexu stránky určuje, která stránka výsledků má být vrácena, kde 1 identifikuje první stránku. Parametr pro celkový počet záznamů je out parametr (můžete použít **ByRef** v jazyce Visual Basic), který je nastaven na celkový počet profilů. Například pokud úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, **ProfileInfoCollection** vrácena obsahuje šestý až desátý profily. Celková hodnota záznamů je nastavena na 13 při návratu metody. |
| Metoda GetNumberOfInActiveProfiles | Bere jako vstup **profileauthenticationoption** hodnotu a **DateTime** objekt a vrátí počet všech profilů ve zdroji dat, kde poslední datum aktivity je menší nebo rovno zadané **DateTime** a kde název aplikace odpovídá **ApplicationName** hodnotu vlastnosti. Parametr **ProfileAuthenticationOption** určuje, zda mají být spočítány pouze anonymní profily, pouze ověřené profily nebo všechny profily. |

### <a name="applicationname"></a>ApplicationName

Vzhledem k tomu, že poskytovatelé profilů ukládají informace o profilu samostatně pro každou aplikaci, je nutné zajistit, aby schéma dat obsahovalo název aplikace a aby dotazy a aktualizace zahrnovaly také název aplikace. Následující příkaz se například používá k načtení hodnoty vlastnosti z databáze založené na uživatelském jménu a na tom, zda je profil anonymní, a zajišťuje, že hodnota **ApplicationName** je zahrnuta do dotazu.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET témata

## <a name="what-are-aspnet-20-themes"></a>Co jsou ASP.NET 2.0 Témata?

Jedním z nejdůležitějších aspektů webové aplikace je konzistentní vzhled a chování na celém webu. ASP.NET vývojáři 1.x obvykle používají kaskádové šablony stylů (CSS) k implementaci konzistentního vzhledu. ASP.NET 2.0 témata výrazně zlepšit css, protože dávají ASP.NET vývojář i schopnost definovat vzhled ASP.NET serverových ovládacích prvků, stejně jako HTML prvky. ASP.NET motivy lze použít pro jednotlivé ovládací prvky, určitou webovou stránku nebo celou webovou aplikaci. Motivy používají kombinaci souborů CSS, volitelný soubor vzhledu a volitelný adresář Images, pokud jsou obrázky potřeba. Soubor vzhledu řídí vizuální vzhled ASP.NET serverových ovládacích prvků.

## <a name="where-are-themes-stored"></a>Kde jsou uloženy motivy?

Umístění, kde jsou uloženy motivy se liší v závislosti na jejich oboru. Motivy, které lze použít pro libovolnou aplikaci, jsou uloženy v následující složce:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Motiv, který je specifický pro konkrétní aplikaci, je uložen v `App\_Themes\<Theme\_Name>` adresáři v kořenovém adresáři webu.

> [!NOTE]
> Soubor vzhledu by měl upravovat pouze vlastnosti serveru ovládacího prvku, které ovlivňují vzhled.

Globální motiv je motiv, který lze použít pro libovolnou aplikaci nebo web spuštěný na webovém serveru. Tyto motivy jsou ve výchozím nastavení uloženy v adresáři ASP.NETClientfiles\Themes, který je uvnitř adresáře v2.x.xxxxx. Případně můžete soubory motivů přesunout do složky aspnet\_client/system\_web/[version]/Themes/[theme\_name] v kořenovém adresáři webu.

Motivy specifické pro aplikaci lze použít pouze pro aplikaci, ve které jsou soubory umístěny. Tyto soubory jsou `App\_Themes/<theme\_name>` uloženy v adresáři v kořenovém adresáři webu.

## <a name="the-components-of-a-theme"></a>Součásti tématu

Motiv se skládá z jednoho nebo více souborů CSS, volitelného souboru vzhledu a volitelné složky Obrázky. CSS soubory mohou být libovolný název, který chcete (tj. default.css nebo theme.css, atd.) a musí být v kořenovém adresáři složky motivů. Soubory CSS se používají k definování běžných tříd CSS a atributů pro konkrétní voliče. Chcete-li použít jednu z tříd CSS na prvek stránky, použije se vlastnost **CSSClass.**

Soubor vzhledu je soubor XML, který obsahuje definice vlastností pro ASP.NET serverových ovládacích prvků. Níže uvedený kód je ukázkovým souborem vzhledu.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**Obrázek 1** níže znázorňuje malou ASP.NET stránku, která byla procházena bez použitého motivu. **Obrázek 2** znázorňuje stejný soubor s použitým tématem. Barva pozadí a barva textu jsou konfigurovány prostřednictvím souboru CSS. Vzhled tlačítka a textového pole jsou konfigurovány pomocí výše uvedeného souboru vzhledu.

![Žádné téma](profiles-themes-and-web-parts/_static/image1.gif)

**Obrázek 1**: Žádný motiv

![Použitý motiv](profiles-themes-and-web-parts/_static/image2.gif)

**Obrázek 2**: Použitý motiv

Výše uvedený soubor vzhledu definuje výchozí vzhled pro všechny ovládací prvky TextBox a Button. To znamená, že každý ovládací prvek TextBox a button vložený na stránce převezme tento vzhled. Můžete také definovat vzhled, který lze použít na určité instance těchto ovládacích prvků pomocí **skinid** vlastnost ovládacího prvku.

Níže uvedený kód definuje vzhled pro ovládací prvek Button. Pouze Button ovládací prvky s **SkinID** vlastnost **goButton** bude mít na vzhled vzhledu.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Můžete mít pouze jeden výchozí vzhled na typ ovládacího prvku serveru. Pokud požadujete další vzhledy, měli byste použít vlastnost SkinID.

## <a name="applying-themes-to-pages"></a>Aplikování motivů na stránky

Motiv lze použít pomocí některé z následujících metod:

- V &lt;elementu stránky&gt; souboru web.config
- Ve @Page směrnici stránky
- Prostřednictvím kódu programu

## <a name="applying-a-theme-in-the-configuration-file"></a>Použití motivu v konfiguračním souboru

Chcete-li použít motiv v konfiguračním souboru aplikací, použijte následující syntaxi:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

Zde uvedený název motivu se musí shodovat s názvem složky motivů. Tato složka může existovat buď v některém z umístění uvedených dříve v tomto kurzu. Pokud se pokusíte použít motiv, který neexistuje, dojde k chybě konfigurace.

## <a name="applying-a-theme-in-the-page-directive"></a>Použití motivu ve směrnici o stránce

Motiv můžete použít také ve směrnici @ Page. Tato metoda umožňuje použít motiv pro určitou stránku.

Chcete-li použít motiv @Page v direktivě, použijte následující syntaxi:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Opět platí, že téma zde uvedené musí odpovídat složky motivu, jak je uvedeno výše. Pokud se pokusíte použít motiv, který neexistuje, dojde k selhání sestavení. Visual Studio také zvýrazní atribut a upozorní vás, že žádný takový motiv neexistuje.

## <a name="applying-a-theme-programmatically"></a>Programové použití motivu

Chcete-li použít motiv programově, musíte zadat vlastnost **Motiv** pro stránku v metodě **Page\_PreInit.**

Chcete-li použít motiv programově, použijte následující syntaxi:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

Je nutné použít motiv v Metodě PreInit z důvodu životního cyklu stránky. Pokud jej použijete po tomto bodu, motiv stránek již byly použity v běhu runtime a změna v tomto okamžiku je příliš pozdě v životním cyklu. Pokud použijete motiv, který neexistuje, dojde k **httpexception.** Při použití motivu programově dojde k upozornění sestavení, pokud všechny serverové ovládací prvky mají zadanou vlastnost SkinID. Toto upozornění je určena k informování, že žádný motiv je deklarativně použita a může být ignorována.

## <a name="exercise-1--applying-a-theme"></a>Cvičení 1 : Použití tématu

V tomto cvičení použijete ASP.NET motiv na webu.

> [!IMPORTANT]
> Pokud používáte aplikaci Microsoft Word k zadávání informací do souboru vzhledu, ujistěte se, že nenahrazujete běžné uvozovky inteligentními uvozovkami. Inteligentní uvozovky způsobí problémy se soubory vzhledu.

1. Vytvořte nový ASP.NET web.
2. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a zvolte Přidat novou položku.
3. Ze seznamu souborů zvolte Webový konfigurační soubor a klepněte na Přidat.
4. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a zvolte Přidat novou položku.
5. Zvolte Soubor vzhledu a klikněte na Přidat.
6. Na dotaz, jestli chcete soubor umístit do složky\_Motivy aplikací, klikněte na Ano.
7. Klikněte pravým tlačítkem myši na\_složku SkinFile uvnitř složky Motivy aplikací v Průzkumníku řešení a zvolte Přidat novou položku.
8. Ze seznamu souborů zvolte Šablona stylů a klikněte na Přidat. Nyní máte všechny soubory potřebné k implementaci nového motivu. Visual Studio však pojmenovalo složku motivů SkinFile. Klikněte pravým tlačítkem myši na tuto složku a změňte název na CoolTheme.
9. Otevřete soubor SkinFile.skin a na konec souboru přidejte následující kód: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. Uložte soubor SkinFile.skin.
11. Otevřete soubor StyleSheet.css.
12. Nahraďte celý text v něm následujícími: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. Uložte soubor StyleSheet.css.
14. Otevřete stránku Default.aspx.
15. Přidejte ovládací prvek TextBox a Button.
16. Uložte stránku. Nyní projděte stránku Default.aspx. Měl by se zobrazit jako normální webový formulář.
17. Otevřete soubor web.config.
18. Přímo pod otevírací `<system.web>` značku přidejte následující: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Uložte soubor web.config. Nyní projděte stránku Default.aspx. Měl by se zobrazit s použitým tématem.
20. Pokud ještě není otevřená, otevřete stránku Default.aspx v sadě Visual Studio.
21. Vyberte tlačítko.
22. Změňte vlastnost **SkinID** na goButton. Všimněte si, že Visual Studio poskytuje rozevírací seznam s platnými hodnotami SkinID pro ovládací prvek Button.
23. Uložte stránku. Nyní znovu zobrazte náhled stránky v prohlížeči. Tlačítko by nyní mělo říkat "jít" a mělo by být širší vzhled.

Pomocí vlastnosti **SkinID** můžete snadno nakonfigurovat různé vzhledy pro různé instance určitého typu serverového ovládacího prvku.

## <a name="the-stylesheettheme-property"></a>Vlastnost StyleSheetTheme

Zatím jsme mluvili jen o použití tématpomocí objektu Téma. Při použití vlastnosti Motiv soubor vzhled přepíše všechna deklarativní nastavení pro serverové ovládací prvky. Například v cvičení 1 jste zadali SkinID "goButton" pro button ovládací prvek a který změnil button text na "go". Možná jste si všimli, že vlastnost Text tlačítka v návrháři byla nastavena na "Button", ale téma to přehlašuje. Motiv vždy přepíše všechna nastavení vlastností v návrháři.

Pokud chcete mít možnost přepsat vlastnosti definované v souboru vzhledu motivu vlastnostmi určenými v návrháři, můžete místo vlastnosti Motiv použít vlastnost **StyleSheetTheme.** Vlastnost StyleSheetTheme je stejná jako vlastnost Motiv s tím rozdílem, že nepřepíše všechna explicitní nastavení vlastností, jako je vlastnost Motiv.

Chcete-li to vidět v akci, otevřete soubor web.config `<pages>` z projektu v cvičení 1 a změňte prvek na následující:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Nyní procházet Stránku Default.aspx a uvidíte, že button ovládací prvek má text vlastnost "Button" znovu. Je to proto, že explicitní nastavení vlastnosti v návrháři přepíše vlastnost Text nastavenou id vzhledu goButton.

## <a name="overriding-themes"></a>Přepsání motivů

Globální motiv lze přepsat použitím motivu se stejným názvem ve\_složce Motivy aplikací aplikace. Motiv však není použit ve scénáři true přepsat. Pokud modul runtime narazí na soubory\_motivů ve složce Motivy aplikací, použije motiv pomocí těchto souborů a bude globální motiv ignorovat.

Vlastnost StyleSheetTheme je overridable a může být přepsána v kódu následujícím způsobem:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Webové části

ASP.NET webových částí je integrovaná sada ovládacích prvků pro vytváření webových serverů, které koncovým uživatelům umožňují upravovat obsah, vzhled a chování webových stránek přímo z prohlížeče. Změny lze použít pro všechny uživatele na webu nebo pro jednotlivé uživatele. Když uživatelé upravují stránky a ovládací prvky, nastavení lze uložit, aby se zachovaly osobní předvolby uživatele v budoucích relacích prohlížeče, což je funkce nazvaná přizpůsobení. Tyto funkce webových částí znamenají, že vývojáři mohou koncovým uživatelům zmocnit dynamické přizpůsobení webové aplikace bez zásahu vývojáře nebo správce.

Pomocí sady ovládacích prvku Webové části můžete jako vývojář povolit koncovým uživatelům:

- Přizpůsobení obsahu stránky. Uživatelé mohou na stránku přidávat nové ovládací prvky webových částí, odebírat je, skrývat nebo minimalizovat jako běžná okna.
- Přizpůsobení rozložení stránky. Uživatelé mohou přetáhnout ovládací prvek webových částí do jiné zóny na stránce nebo změnit jeho vzhled, vlastnosti a chování.
- Kontroly exportu a importu. Uživatelé mohou importovat nebo exportovat nastavení ovládacích prvků webových částí pro použití na jiných stránkách nebo webech a zachovat vlastnosti, vzhled a dokonce i data v ovládacích prvcích. To snižuje požadavky na zadávání dat a konfiguraci koncových uživatelů.
- Vytvořte připojení. Uživatelé mohou vytvořit připojení mezi ovládacími prvky tak, aby například ovládací prvek grafu mohl zobrazit graf pro data v ovládacím prvku burzovního panelu. Uživatelé mohli přizpůsobit nejen samotné připojení, ale i vzhled a podrobnosti o tom, jak ovládací prvek grafu zobrazuje data.
- Spravujte a přizpůsobte nastavení na úrovni webu. Oprávnění uživatelé mohou konfigurovat nastavení na úrovni webu, určit, kdo má přístup k webu nebo stránce, nastavit přístup k ovládacím prvkům na základě rolí a tak dále. Uživatel v roli pro správu může například nastavit ovládací prvek webových částí, který bude sdílen všemi uživateli, a zabránit uživatelům, kteří nejsou správci, v přizpůsobení sdíleného ovládacího prvku.

S webovými částmi obvykle pracujete jedním ze tří způsobů: vytvářením stránek, které používají ovládací prvky webových částí, vytvářením jednotlivých ovládacích prvků webových částí nebo vytvářením úplných, přizpůsobitelných webových aplikací, například portálu.

## <a name="page-development"></a>Vývoj stránky

Vývojáři stránek mohou pomocí nástrojů pro vizuální návrh, jako je například Microsoft Visual Studio 2005, vytvářet stránky, které používají webové části. Jednou z výhod při používání nástroje, jako je například Visual Studio je, že sada ovládacích prvků webových částí poskytuje funkce pro vytváření a konfiguraci ovládacích prvků webových částí v vizuálním návrháři. Pomocí návrháře můžete například přetáhnout zónu webových částí nebo ovládací prvek editoru webových částí na návrhovou plochu a potom nakonfigurovat ovládací prvek přímo v návrháři pomocí uživatelského rozhraní poskytovaného sadou ovládacích prvku Webové části. To může urychlit vývoj aplikací webových částí a snížit množství kódu, který je třeba napsat.

## <a name="control-development"></a>Vývoj řízení

Jako ovládací prvek webových částí můžete použít libovolný existující ovládací prvek ASP.NET, včetně standardních ovládacích prvků webového serveru, vlastních serverových ovládacích prvků a uživatelských ovládacích prvků. Pro maximální programovou kontrolu prostředí můžete také vytvořit vlastní ovládací prvky webových částí, které jsou odvozeny z třídy WebPart. Pro vývoj jednotlivých webových částí obvykle vytvoříte uživatelský ovládací prvek a použijete jej jako ovládací prvek webových částí nebo vytvoříte vlastní ovládací prvek webových částí.

Jako příklad vývoje vlastního ovládacího prvku webových částí můžete vytvořit ovládací prvek, který poskytne některou z funkcí poskytovaných jinými ASP.NET serverovými ovládacími prvky, které by mohly být užitečné pro balíček jako personalizovatelný ovládací prvek webových částí: kalendáře, seznamy, finanční informace, zprávy, kalkulačky, ovládací prvky ve formátovaném textu pro aktualizaci obsahu, upravitelné mřížky, které se připojují k databázím, grafy, které dynamicky aktualizují jejich displeje nebo informace o počasí a cestování. Pokud poskytnete vizuální návrhář s ovládacím prvkem, pak každý vývojář stránky pomocí sady Visual Studio můžete jednoduše přetáhnout ovládací prvek do zóny webových částí a nakonfigurovat jej v době návrhu bez nutnosti psát další kód.

Přizpůsobení je základem funkce webových částí. Umožňuje uživatelům upravovat nebo přizpůsobovat rozložení, vzhled a chování ovládacích prvků webových částí na stránce. Individuální nastavení jsou dlouhodobá: jsou zachována nejen během aktuální relace prohlížeče (jako u stavu zobrazení), ale také v dlouhodobém úložišti, takže nastavení uživatele jsou uložena i pro budoucí relace prohlížeče. Přizpůsobení je ve výchozím nastavení povoleno pro stránky webových částí.

Konstrukční součásti uživatelského rozhraní spoléhají na přizpůsobení a poskytují základní strukturu a služby potřebné pro všechny ovládací prvky webových částí. Jedna konstrukční součást uživatelského portálu vyžadované na každé stránce webových částí je ovládací prvek WebPartManager. I když nikdy viditelné, tento ovládací prvek má kritický úkol koordinaci všech ovládacích prvků webových částí na stránce. Sleduje například všechny jednotlivé ovládací prvky webových částí. Spravuje zóny webových částí (oblasti, které obsahují ovládací prvky webových částí na stránce) a které ovládací prvky jsou ve kterých zónách. Sleduje a řídí také různé režimy zobrazení, ve kterých se stránka může nacházet, například procházet, připojovat, upravovat nebo katalogovat a zda se změny přizpůsobení vztahují na všechny uživatele nebo na jednotlivé uživatele. Nakonec iniciuje a sleduje připojení a komunikaci mezi ovládacími prvky webových částí.

Druhým druhem konstrukční součásti ui je zóna. Zóny fungují jako správci rozložení na stránce webových částí. Obsahují a uspořádají ovládací prvky, které jsou odvozeny od třídy Part (ovládací prvky součástí) a poskytují možnost provést modulární rozložení stránky v horizontální nebo svislé orientaci. Zóny také nabízejí společné a konzistentní prvky uživatelského rozhraní (například styl záhlaví a zápatí, název, styl ohraničení, tlačítka akcí a tak dále) pro každý ovládací prvek, který obsahují; tyto společné prvky jsou označovány jako chrom ovládacího prvku. V různých režimech zobrazení a s různými ovládacími prvky se používá několik specializovaných typů zón. Různé typy zón jsou popsány v části Základní ovládací prvky webových částí níže.

Ovládací prvky uživatelského rozhraní webových částí, které jsou všechny odvozeny ze třídy **Part,** obsahují primární uživatelské rozhraní na stránce webových částí. Sada ovládacích prvků webových částí je flexibilní a zahrnutá v možnostech, které poskytuje pro vytváření ovládacích prvků součástí. Kromě vytváření vlastních ovládacích prvků webových částí můžete jako ovládací prvky webových částí použít také existující ovládací prvky ASP.NET serveru, uživatelské ovládací prvky nebo vlastní serverové ovládací prvky. Základní ovládací prvky, které se nejčastěji používají pro vytváření stránek webových částí, jsou popsány v další části.

## <a name="web-parts-essential-controls"></a>Základní ovládací prvky webových částí

Sada ovládacích prvků webových částí je rozsáhlá, ale některé ovládací prvky jsou nezbytné buď proto, že jsou vyžadovány pro práci webových částí, nebo proto, že se jedná o ovládací prvky nejčastěji používané na stránkách webových částí. Při používání webových částí a vytváření základních stránek webových částí je užitečné seznámit se se základními ovládacími prvky webových částí popsanými v následující tabulce.

| **Řízení webových částí** | **Popis** |
| --- | --- |
| Webpartmanager | Spravuje všechny ovládací prvky webových částí na stránce. Pro každou stránku webových částí je vyžadován jeden (a pouze jeden) ovládací prvek **WebPartManager.** |
| Catalogzone | Obsahuje ovládací prvky CatalogPart. Tato zóna slouží k vytvoření katalogu ovládacích prvků webových částí, ze kterých mohou uživatelé vybírat ovládací prvky, které mají přidat na stránku. |
| Editorzone | Obsahuje ovládací prvky EditorPart. Tato zóna slouží k tomu, aby uživatelé mohli upravovat a přizpůsobovat ovládací prvky webových částí na stránce. |
| Webpartzone | Obsahuje a poskytuje celkové rozložení pro ovládací prvky WebPart, které tvoří hlavní uživatelské rozhraní stránky. Tuto zónu použijte při vytváření stránek s ovládacími prvky webových částí. Stránky mohou obsahovat jednu nebo více zón. |
| Connectionszone | Obsahuje ovládací prvky WebPartConnection a poskytuje uživatelské rozhraní pro správu připojení. |
| Webová část (GenericWebPart) | Vykreslí primární ui; většina ovládacích prvků uživatelského rozhraní webových částí spadá do této kategorie. Pro maximální programový ovládací prvek můžete vytvořit vlastní ovládací prvky webových částí, které jsou odvozeny ze základního ovládacího prvku **WebPart.** Jako ovládací prvky webových částí můžete také použít existující serverové ovládací prvky, uživatelské ovládací prvky nebo vlastní ovládací prvky. Vždy, když některý z těchto ovládacích prvků jsou umístěny v zóně, **ovládací prvek WebPartManager** automaticky zabalí je s **GenericWebPart** ovládací prvky za běhu, takže je můžete použít s funkcemi webových částí. |
| Catalogpart | Obsahuje seznam dostupných ovládacích prvků webových částí, které mohou uživatelé přidat na stránku. |
| Webpartconnection | Vytvoří spojení mezi dvěma ovládacími prvky webových částí na stránce. Připojení definuje jeden z ovládacích prvků webových částí jako zprostředkovatele (dat) a druhý jako příjemce. |
| Editorpart | Slouží jako základní třída pro specializované ovládací prvky editoru. |
| Ovládací prvky EditorPart (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart a PropertyGridEditorPart) | Povolit uživatelům přizpůsobit různé aspekty ovládacích prvků uživatelského rozhraní webových částí na stránce |

## <a name="lab-create-a-web-part-page"></a>Lab: Vytvoření stránky webových částí

V tomto testovacím prostředí vytvoříte stránku webové části, která bude uchovávat informace prostřednictvím ASP.NET profilů.

### <a name="creating-a-simple-page-with-web-parts"></a>Vytvoření jednoduché stránky s webovými částmi

V této části návodu vytvoříte stránku, která používá ovládací prvky webových částí k zobrazení statického obsahu. Prvním krokem při práci s webovými částmi je vytvoření stránky se dvěma požadovanými konstrukčními prvky. Za prvé, webová část stránka potřebuje ovládací prvek WebPartManager sledovat a koordinovat všechny ovládací prvky webových částí. Za druhé, stránka webových částí potřebuje jednu nebo více zón, což jsou složené ovládací prvky, které obsahují ovládací prvky WebPart nebo jiné serverové a zabírají zadanou oblast stránky.

> [!NOTE]
> Nemusíte dělat nic pro povolení přizpůsobení webových částí; je ve výchozím nastavení povolena pro sadu ovládacích prvku Webové části. Při prvním spuštění stránky webových částí na webu ASP.NET nastaví výchozího zprostředkovatele individuálního nastavení pro ukládání nastavení individuálního nastavení uživatelů. Další informace o přizpůsobení naleznete v tématu Přehled individuálního nastavení webových částí.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>Vytvoření stránky obsahující ovládací prvky webových částí

1. Zavřete výchozí stránku a přidejte novou stránku na web s názvem WebPartsDemo.aspx.
2. Přepněte do **návrhového** zobrazení.
3. V nabídce **Zobrazení** zkontrolujte, zda jsou vybrány možnosti **Nevizuální ovládací prvky** a **Podrobnosti,** abyste viděli značky rozložení a ovládací prvky, které nemají uživatelské rozhraní.
4. Umístěte textový kurzor před `<div>` tagy na návrhovou plochu a stisknutím klávesy ENTER přidejte nový řádek. Umístěte textový kurzor před nový znak řádku, klepněte v nabídce na ovládací prvek rozevíracího seznamu **Blokformát** a vyberte možnost **Nadpis 1.** Do záhlaví přidejte text **stránku pro vykazování webových částí**.
5. Na kartě **WebParts** panelu nástrojů přetáhněte ovládací prvek **WebPartManager** na stránku a umístěte `<div>`jej těsně za nový znak řádku a před značky.   
  
   Ovládací prvek **WebPartManager** nevykreslí žádný výstup, takže se zobrazí jako šedé pole na povrchu návrháře.
6. Umístěte textový kurzor mezi `<div>` tagy.
7. V nabídce **Rozložení** klikněte na **Vložit tabulku**a vytvořte novou tabulku s jedním řádkem a třemi sloupci. Klepněte na tlačítko **Vlastnosti buňky,** vyberte **horní část** rozevíracího seznamu **Svislé zarovnání,** klepněte na **tlačítko OK**a tabulku znovu vytvořte klepnutím na tlačítko **OK.**
8. Přetáhněte ovládací prvek WebPartZone do levého sloupce tabulky. Klepněte pravým tlačítkem myši na ovládací prvek **WebPartZone,** zvolte **Vlastnosti**a nastavte následující vlastnosti:   
  
   ID: SidebarZone   
  
   HeaderText: Postranní panel
9. Přetáhněte druhý ovládací prvek **WebPartZone** do sloupce prostřední tabulky a nastavte následující vlastnosti:   
  
   ID: MainZone   
  
   HeaderText: Hlavní
10. Uložte soubor.

Stránka má nyní dvě odlišné zóny, které můžete ovládat samostatně. Žádná zóna však nemá žádný obsah, takže dalším krokem je vytvoření obsahu. V tomto návodu pracujete s ovládacími prvky webových částí, které zobrazují pouze statický obsah.

Rozložení zóny webových částí je &lt;určeno&gt; elementem zonetemplate. Uvnitř šablony zóny můžete přidat libovolný ovládací prvek ASP.NET, ať už se jedná o vlastní ovládací prvek webových částí, uživatelský ovládací prvek nebo existující serverový ovládací prvek. Všimněte si, že zde používáte Label ovládací prvek a že jste jednoduše přidání statického textu. Pokud umístíte běžný serverový ovládací prvek do zóny **WebPartZone,** ASP.NET bude s ovládacím prvkem webových částí za běhu považovat ovládací prvek webových částí, který umožňuje funkce webových částí v ovládacím prvku.

**Vytvoření obsahu pro hlavní zónu**

1. V **návrhovém** zobrazení přetáhněte ovládací **prvek Popisek** z karty **Standardní** v panelu nástrojů do oblasti obsahu zóny, jejíž vlastnost **ID** je nastavena na MainZone.
2. Přepněte do **zobrazení zdroje.** Všimněte &lt;si,&gt; že element zonetemplate byl přidán k zalomení label ovládacího **prvku** v MainZone.
3. Přidejte atribut **title** s &lt;názvem title&gt; do elementu asp:label a nastavte jeho hodnotu na Obsah. Odeberte atribut Text="Label" z &lt;&gt; elementu asp:label. Mezi otevírací a uzavírací &lt;značky&gt; elementu asp:label přidejte nějaký text, &lt;například&gt; Vítá vás **domovská stránka** v rámci dvojice značek prvků h2. Váš kód by měl vypadat takto. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Uložte soubor.

Dále vytvořte uživatelský ovládací prvek, který lze také přidat na stránku jako ovládací prvek webových částí.

### <a name="to-create-a-user-control"></a>Vytvoření uživatelského ovládacího prvku

1. Přidejte na web nový ovládací prvek webového uživatele, který bude sloužit jako ovládací prvek vyhledávání. Odznačte **volbu, chcete-li umístit zdrojový kód do samostatného souboru**. Přidejte jej do stejného adresáře jako stránku WebPartsDemo.aspx a pojmenujte ji SearchUserControl.ascx.   
  
    > [!NOTE]
    > Uživatelský ovládací prvek pro tento návod neimplementuje skutečné funkce vyhledávání. používá se pouze k předvádění funkcí webových částí.
2. Přepněte do **návrhového** zobrazení. Na kartě **Standardní** v panelu nástrojů přetáhněte ovládací prvek TextBox na stránku.
3. Umístěte textový kurzor za textové pole, které jste právě přidali, a stisknutím klávesy ENTER přidejte nový řádek.
4. Přetáhněte ovládací prvek Tlačítko na stránku na novém řádku pod textovým polem, které jste právě přidali.
5. Přepněte do **zobrazení zdroje.** Ujistěte se, že zdrojový kód pro uživatelský ovládací prvek vypadá jako v následujícím příkladu. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Uložte soubor a zavřete ho.

Nyní můžete přidat ovládací prvky webových částí do zóny postranního panelu. Do zóny postranního panelu přidáváte dva ovládací prvky, jeden obsahující seznam odkazů a druhý, který je uživatelským ovládacím prvkem, který jste vytvořili v předchozím postupu. Odkazy jsou přidány jako standardní ovládací prvek **serveru Label,** podobně jako jste vytvořili statický text pro hlavní zónu. I když jednotlivé serverové ovládací prvky obsažené v uživatelském ovládacím prvku mohou být obsaženy přímo v zóně (například ovládací prvek popisek), v tomto případě nejsou. Místo toho jsou součástí uživatelského ovládacího prvku, který jste vytvořili v předchozím postupu. To ukazuje běžný způsob, jak zabalit jakékoli ovládací prvky a další funkce, které chcete v uživatelském ovládacím prvku, a potom odkazovat na tento ovládací prvek v zóně jako ovládací prvek webových částí.

Za běhu sada ovládacích prvků webových částí zabalí oba ovládací prvky pomocí ovládacích prvků GenericWebPart. Když ovládací prvek **GenericWebPart** zabalí ovládací prvek webového serveru, obecný ovládací prvek součásti je nadřazený ovládací prvek a můžete přistupovat k ovládacímu prvku serveru prostřednictvím nadřazeného ovládacího prvku ChildControl vlastnost. Toto použití obecných ovládacích prvků součástí umožňuje standardním ovládacím prvkům webového serveru mít stejné základní chování a atributy jako ovládací prvky webových částí, které jsou odvozeny od třídy **WebPart.**

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>Přidání ovládacích prvků webových částí do zóny postranního panelu

1. Otevřete stránku WebPartsDemo.aspx.
2. Přepněte do **návrhového** zobrazení.
3. Přetáhněte stránku uživatelského ovládacího prvku, kterou jste vytvořili, SearchUserControl.ascx z **Průzkumníka řešení** do zóny, jejíž vlastnost **ID** je nastavena na SidebarZone, a tam ji přetáhněte.
4. Uložte stránku WebPartsDemo.aspx.
5. Přepněte do **zobrazení zdroje.**
6. Uvnitř &lt;elementu asp:webpartzone&gt; pro SidebarZone, těsně nad odkazem &lt;na uživatelský&gt; ovládací prvek, přidejte element asp:label s obsaženými odkazy, jak je znázorněno v následujícím příkladu. Do značky uživatelského ovládacího prvku také přidejte atribut **Title** s hodnotou **Hledat**, jak je znázorněno na obrázku. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Uložte soubor a zavřete ho.

Nyní můžete otestovat stránku procházením v prohlížeči. Na stránce se zobrazí dvě zóny. Následující snímek obrazovky ukazuje stránku.

**Ukázková stránka webových částí se dvěma zónami**

![Webový chod VS Návod 1 Snímek obrazovky](profiles-themes-and-web-parts/_static/image3.gif)

**Obrázek 3**: Webový průchod VS 1 Snímek obrazovky

V záhlaví každého ovládacího prvku je šipka dolů, která poskytuje přístup k nabídce sloves dostupných akcí, které můžete provádět s ovládacím prvkem. Klepněte na nabídku sloves pro jeden z ovládacích prvků, potom klepněte na **minimalizovat** sloveso a všimněte si, že ovládací prvek je minimalizován. V nabídce slovesklepněte na tlačítko **Obnovit**a ovládací prvek se vrátí do normální velikosti.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Povolení uživatelům upravovat stránky a měnit rozložení

Webové části poskytují uživatelům možnost změnit rozložení ovládacích prvků webových částí jejich přetažením z jedné zóny do druhé. Kromě toho, že uživatelům umožňujete přesouvat ovládací prvky **webové části** z jedné zóny do druhé, můžete uživatelům povolit úpravy různých charakteristik ovládacích prvků, včetně jejich vzhledu, rozložení a chování. Sada ovládacích prvků Webových částí poskytuje základní funkce úprav ovládacích prvků **webparts.** I když to v tomto návodu neučiníte, můžete také vytvořit vlastní ovládací prvky editoru, které uživatelům umožní upravovat funkce ovládacích prvků **webpart.** Stejně jako při změně umístění ovládacího prvku **WebPart,** úpravy vlastností ovládacího prvku závisí na ASP.NET přizpůsobení uložit změny, které uživatelé provést.

V této části návodu přidáte uživatelům možnost upravit základní charakteristiky libovolného ovládacího prvku **WebPart** na stránce. Chcete-li povolit tyto funkce, přidejte na stránku další vlastní uživatelský ovládací prvek spolu s elementem &lt;asp:editorzone&gt; a dvěma ovládacími prvky pro úpravy.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>Vytvoření uživatelského ovládacího prvku, který umožňuje změnu rozložení stránky

1. V sadě Visual Studio vyberte v nabídce **Soubor** podnabídku **Nový** a klepněte na možnost **Soubor.**
2. V dialogovém okně **Přidat novou položku** vyberte **položku Webový uživatelský ovládací prvek**. Pojmenujte nový soubor DisplayModeMenu.ascx. Odznačte volbu **Umístit zdrojový kód do samostatného souboru**.
3. Chcete-li vytvořit nový ovládací prvek, klepněte na tlačítko Přidat.
4. Přepněte do **zobrazení zdroje.**
5. Odeberte veškerý existující kód v novém souboru a vložte následující kód. Tento kód uživatelského ovládacího prvku používá funkce sady ovládacích prvků webových částí, které umožňují stránce změnit režim zobrazení nebo zobrazení a také umožňují změnit fyzický vzhled a rozložení stránky v určitých režimech zobrazení. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Soubor uložte klepnutím na ikonu uložit na panelu nástrojů nebo výběrem **možnosti Uložit** v nabídce **Soubor.**

### <a name="to-enable-users-to-change-the-layout"></a>Povolení uživatelům ke změně rozložení

1. Otevřete stránku WebPartsDemo.aspx a přepněte do **návrhového** zobrazení.
2. Umístěte textový kurzor do **návrhového** zobrazení těsně za ovládací prvek **WebPartManager,** který jste přidali dříve. Přidejte pevný návrat za text tak, aby byl prázdný řádek za ovládacím prvkem **WebPartManager.** Umístěte textový kurzor na prázdný řádek.
3. Přetáhněte uživatelský ovládací prvek, který jste právě vytvořili (soubor se jmenuje DisplayModeMenu.ascx) na stránku WebPartsDemo.aspx a přetáhněte jej na prázdný řádek.
4. Přetáhněte ovládací prvek EditorZone z části **Webové části** panelu nástrojů do zbývající buňky otevřené tabulky na stránce WebPartsDemo.aspx.
5. V části **Webové části** panelu nástrojů přetáhněte ovládací prvek AppearanceEditorPart a ovládací prvek LayoutEditorPart do ovládacího prvku **EditorZone.**
6. Přepněte do **zobrazení zdroje.** Výsledný kód v buňce tabulky by měl vypadat podobně jako následující kód. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. Uložte soubor WebPartsDemo.aspx. Vytvořili jste uživatelský ovládací prvek, který umožňuje měnit režimy zobrazení a měnit rozložení stránky, a odkazovali jste na ovládací prvek na primární webové stránce.

Nyní můžete otestovat možnost úprav stránek a změnit rozložení.

### <a name="to-test-layout-changes"></a>Testování změn rozložení

1. Načtěte stránku do prohlížeče.
2. Klepněte na rozevírací **nabídku Režim zobrazení** a vyberte **upravit**. Zobrazí se názvy zón.
3. Přetáhněte ovládací prvek **Moje odkazy** podle záhlaví ze zóny Postranní panel do dolní části hlavní zóny. Stránka by měla vypadat jako následující snímek obrazovky.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Ukázková stránka webových částí s přesunutým ovládacím prvkem Moje odkazy

![Snímek obrazovky Web Parts VS Walkthrough 2](profiles-themes-and-web-parts/_static/image4.gif)

**Obrázek 4**: Webový průchod VS Návod 2 Snímek obrazovky

1. Klepněte na rozevírací **nabídku Režim zobrazení** a vyberte **procházet**. Stránka se aktualizuje, názvy zón zmizí a ovládací prvek **Moje odkazy** zůstane tam, kam jste ji umístili.
2. Chcete-li prokázat, že přizpůsobení funguje, zavřete prohlížeč a znovu načtěte stránku. Provedené změny se uloží pro budoucí relace prohlížeče.
3. V nabídce **Režim zobrazení** vyberte **Upravit**.   
  
   Každý ovládací prvek na stránce je nyní zobrazen se šipkou dolů v záhlaví, která obsahuje rozevírací nabídku sloves.
4. Kliknutím na šipku zobrazíte nabídku sloves v ovládacím prvku **Moje odkazy.** Klikněte na **příkaz Upravit** sloveso.   
  
   Zobrazí se ovládací prvek **EditorZone,** který zobrazuje ovládací prvky EditorPart, které jste přidali.
5. V části **Vzhled** ovládacího prvku úprav změňte **název** na Moje oblíbené položky, pomocí rozevíracího seznamu **Typ Chromu** vyberte **pouze nadpis**a pak klepněte na **tlačítko Použít**. Následující snímek obrazovky zobrazuje stránku v režimu úprav.

### <a name="web-parts-demo-page-in-edit-mode"></a>Ukázková stránka webových částí v režimu úprav

![Snímek obrazovky Web Parts VS Walkthrough 3](profiles-themes-and-web-parts/_static/image5.gif)

**Obrázek 5**: Webový chod VS Návod 3 Snímek obrazovky

1. Klepněte na **nabídku Režim zobrazení** a výběrem **možnosti Procházet** se vraťte do režimu procházení.
2. Ovládací prvek má nyní aktualizovaný název a žádné ohraničení, jak je znázorněno na následujícím snímku obrazovky.

### <a name="edited-web-parts-demo-page"></a>Ukázková stránka upravených webových částí

![Webových částí VS Návod 4 Snímek obrazovky](profiles-themes-and-web-parts/_static/image6.gif)

**Obrázek 4**: Webový chod VS Návod 4 Snímek obrazovky

### <a name="adding-web-parts-at-run-time"></a>Přidání webových částí za běhu

Můžete také povolit uživatelům přidávat ovládací prvky webových částí na jejich stránku za běhu. Chcete-li tak učinit, nakonfigurujte stránku katalogem webových částí, který obsahuje seznam ovládacích prvků webových částí, které chcete zpřístupnit uživatelům.

**Povolení uživatelům přidávat webové části za běhu**

1. Otevřete stránku WebPartsDemo.aspx a přepněte do **návrhového** zobrazení.
2. Na kartě **WebParts** panelu nástrojů přetáhněte ovládací prvek CatalogZone do pravého sloupce tabulky pod ovládacím prvkem **EditorZone.**   
  
   Oba ovládací prvky mohou být ve stejné buňce tabulky, protože nebudou zobrazeny současně.
3. V podokně Vlastnosti přiřaďte řetězec **Přidat webové části** vlastnosti HeaderText ovládacího prvku **CatalogZone.**
4. V části **Webové části** panelu nástrojů přetáhněte ovládací prvek DeclarativeCatalogPart do oblasti obsahu ovládacího prvku **CatalogZone.**
5. Kliknutím na šipku v pravém horním rohu ovládacího **prvku DeclarativeCatalogPart** zpřístupníte jeho nabídku **Úkoly**a pak vyberte Upravit šablony .
6. V části **Standard** panelu nástrojů přetáhněte ovládací prvek **FileUpload** a **calendar** do části **WebPartsTemplate** ovládacího prvku **DeclarativeCatalogPart.**
7. Přepněte do **zobrazení zdroje.** Zkontrolujte zdrojový kód &lt;elementu asp:catalogzone.&gt; Všimněte si, že **declarativeCatalogPart** ovládací prvek obsahuje prvek &lt;webpartstemplate&gt; se dvěma uzavřenými serverovými ovládacími prvky, které budete moci přidat na stránku z katalogu.
8. Přidejte vlastnost **Title** ke každému z ovládacích prvků, které jste přidali do katalogu, pomocí hodnoty řetězce zobrazené pro každý titul v příkladu kódu níže. I když název není vlastnost, kterou můžete normálně nastavit na tyto dva serverové ovládací prvky v době návrhu, když uživatel přidá tyto ovládací prvky do zóny **WebPartZone** z katalogu za běhu, jsou každý zabalen s **ovládacím prvkem GenericWebPart.** To jim umožňuje fungovat jako ovládací prvky webových částí, takže budou moci zobrazovat názvy.   
  
   Kód pro dva ovládací prvky obsažené v **declarativeCatalogPart** ovládacíprvek by měl vypadat takto. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Uložte stránku.

Nyní můžete otestovat katalog.

### <a name="to-test-the-web-parts-catalog"></a>Testování katalogu webových částí

1. Načtěte stránku do prohlížeče.
2. Klepněte na rozevírací **nabídku Režim zobrazení** a vyberte **možnost Katalog**.   
  
   Zobrazí se katalog s názvem **Přidat webové části.**
3. Přetáhněte ovládací prvek **Oblíbené položky** z hlavní zóny zpět do horní části zóny postranního panelu a tam ho přetáhněte.
4. V katalogu **Přidat webové části** zaškrtněte obě políčka a v rozevíracím seznamu, který obsahuje dostupné zóny, vyberte možnost **Main.**
5. Klikněte na **Přidat** v katalogu. Ovládací prvky jsou přidány do hlavní zóny. Pokud chcete, můžete na stránku přidat více instancí ovládacích prvků z katalogu.   
  
   Následující snímek obrazovky zobrazuje stránku s ovládacím prvkem nahrávání souborů a kalendářem v hlavní zóně. 

![Ovládací prvky přidané do hlavní zóny z katalogu](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. Klepněte na rozevírací **nabídku Režim zobrazení** a vyberte **procházet**. Katalog zmizí a stránka se aktualizuje.
7. Zavřete prohlížeč. Načtěte stránku znovu. Provedené změny přetrvávají.
