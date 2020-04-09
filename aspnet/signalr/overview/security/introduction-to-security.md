---
uid: signalr/overview/security/introduction-to-security
title: Úvod do zabezpečení SignalR | Dokumenty společnosti Microsoft
author: bradygaster
description: Popisuje problémy se zabezpečením, které je třeba vzít v úvahu při vývoji aplikace SignalR.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676193"
---
# <a name="introduction-to-signalr-security"></a>Úvod do zabezpečení knihovnou SignalR

podle [Patrick Fletcher](https://github.com/pfletcher), Tom [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje problémy se zabezpečením, které je třeba zvážit při vývoji aplikace SignalR.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
>
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Koncepty zabezpečení SignalR](#concepts)

    - [Ověřování a autorizace](#authentication)
    - [Token připojení](#connectiontoken)
    - [Opětovné připojení skupin při opětovném připojení](#rejoingroup)
- [Jak SignalR zabraňuje padělání žádostí mezi pracovinami](#csrf)
- [Doporučení zabezpečení SignalR](#recommendations)

    - [Protokol SSL (Secure Socket Layers)](#ssl)
    - [Nepoužívejte skupiny jako bezpečnostní mechanismus](#groupsecurity)
    - [Bezpečná manipulace se vstupy od klientů](#input)
    - [Sladění změny stavu uživatele s aktivním připojením](#reconcile)
    - [Automaticky generované soubory proxy JavaScriptu](#autogen)
    - [Výjimky](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>Koncepty zabezpečení SignalR

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Ověřování a autorizace

SignalR neposkytuje žádné funkce pro ověřování uživatelů. Místo toho integrujete funkce SignalR do existující struktury ověřování pro aplikaci. Ověřujete uživatele jako obvykle ve vaší aplikaci a pracovat s výsledky ověřování v kódu SignalR. Můžete například ověřit uživatele pomocí ověřování pomocí ASP.NET formulářů a potom ve vašem centru vynutit, kteří uživatelé nebo role jsou oprávněni volat metodu. V centru můžete také předat klientovi ověřovací informace, například uživatelské jméno nebo to, zda uživatel patří do role.

SignalR poskytuje [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) atribut určit, kteří uživatelé mají přístup k rozbočovačnebo metodu. Atribut Authorize použijete buď na rozbočovač, nebo na konkrétní metody v rozbočovači. Bez autorizovat atribut všechny veřejné metody v rozbočovači jsou k dispozici pro klienta, který je připojen k rozbočovači. Další informace o rozbočovačích naleznete v [tématu Ověřování a autorizace rozbočovačů SignalR](hub-authorization.md).

Atribut použijete na `Authorize` rozbočovače, ale ne na trvalá připojení. Chcete-li vynutit `PersistentConnection` autorizační pravidla `AuthorizeRequest` při použití, musíte přepsat metodu. Další informace o trvalých připojeních naleznete v [tématu Ověřování a autorizace trvalých připojení SignalR](persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Token připojení

SignalR zmírňuje riziko provádění škodlivých příkazů ověřením identity odesílatele. Pro každý požadavek klient a server předají token připojení, který obsahuje ID připojení a uživatelské jméno pro ověřené uživatele. ID připojení jednoznačně identifikuje každého připojeného klienta. Server náhodně vygeneruje ID připojení při vytvoření nového připojení a zachová toto ID po dobu trvání připojení. Mechanismus ověřování pro webovou aplikaci poskytuje uživatelské jméno. SignalR používá šifrování a digitální podpis k ochraně tokenu připojení.

![](introduction-to-security/_static/image2.png)

Pro každý požadavek server ověří obsah tokenu, aby bylo zajištěno, že požadavek pochází od zadaného uživatele. Uživatelské jméno musí odpovídat id připojení. Ověřením id připojení a uživatelského jména signalr zabrání uživateli se zlými úmysly snadno zosobnit jiného uživatele. Pokud server nemůže ověřit token připojení, požadavek se nezdaří.

![](introduction-to-security/_static/image4.png)

Vzhledem k tomu, že ID připojení je součástí procesu ověření, neměli byste odhalit id připojení jednoho uživatele jiným uživatelům nebo uložit hodnotu na straně klienta, například do souboru cookie.

#### <a name="connection-tokens-vs-other-token-types"></a>Tokeny připojení vs. jiné typy tokenů

Tokeny připojení jsou občas označeny nástroji zabezpečení, protože se zdají být tokeny relace nebo ověřovací tokeny, což představuje riziko, pokud jsou vystaveny.

Token připojení SignalR není ověřovací token. Používá se k potvrzení, že uživatel, který tento požadavek provádí, je stejný, který vytvořil připojení. Token připojení je nezbytné, protože ASP.NET SignalR umožňuje připojení pro pohyb mezi servery. Token přidruží připojení k určitému uživateli, ale neuplatňuje identitu uživatele, který žádost provádí. Pro požadavek SignalR správně ověřena, musí mít jiný token, který uplatňuje identitu uživatele, jako je například soubor cookie nebo nosný token. Samotný token připojení však netvrdí, že požadavek byl proveden tímto uživatelem, pouze že ID připojení obsažené v tokenu je přidruženo k tomuto uživateli.

Vzhledem k tomu, že token připojení neposkytuje žádné vlastní deklarace zabezpečení, není považován za token "relace" nebo "ověřování". Převzetí tokenu připojení daného uživatele a jeho přehrání v požadavku ověřeném jako jiný uživatel (nebo neověřený požadavek) se nezdaří, protože identita uživatele požadavku a identita uložená v tokenu se neshodují.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Opětovné připojení skupin při opětovném připojení

Ve výchozím nastavení aplikace SignalR automaticky znovu přiřadí uživatele k příslušným skupinám při opětovném připojení z dočasného přerušení, například když je připojení přerušeno a obnoveno před časovým limitem připojení. Při opětovném připojení klient předá token skupiny, který obsahuje ID připojení a přiřazené skupiny. Token skupiny je digitálně podepsaný a šifrovaný. Klient si po opětovném připojení zachová stejné id připojení. Proto id připojení předané z znovu připojeného klienta musí odpovídat předchozí id připojení používané klientem. Toto ověření zabrání uživateli se zlými úmysly v předávání požadavků na připojení k neoprávněným skupinám při opětovném připojení.

Je však důležité si uvědomit, že platnost tokenu skupiny nevyprší. Pokud uživatel patřil do skupiny v minulosti, ale byl zakázán z této skupiny, tento uživatel může být schopen napodobit token skupiny, která zahrnuje zakázané skupiny. Pokud potřebujete bezpečně spravovat, kteří uživatelé patří ke kterým skupinám, je třeba tato data uložit na server, například do databáze. Potom přidejte logiku do aplikace, která ověří na serveru, zda uživatel patří do skupiny. Příklad ověření členství ve skupinách naleznete v tématu [Práce se skupinami](../guide-to-the-api/working-with-groups.md).

Automatické opětovné připojení skupin platí pouze v případě, že je připojení znovu připojeno po dočasném přerušení. Pokud se uživatel odpojí tím, že přejdete mimo aplikaci nebo se aplikace restartuje, aplikace musí zpracovat, jak přidat tohoto uživatele do správných skupin. Další informace naleznete v [tématu Práce se skupinami](../guide-to-the-api/working-with-groups.md).

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>Jak SignalR zabraňuje padělání žádostí mezi pracovinami

Padělání požadavků mezi sítěmi (CSRF) je útok, při kterém škodlivý web odešle požadavek na ohrožený web, kde je uživatel aktuálně přihlášen. SignalR zabraňuje CSRF tím, že je velmi nepravděpodobné, že škodlivý web vytvořit platný požadavek pro aplikaci SignalR.

### <a name="description-of-csrf-attack"></a>Popis útoku CSRF

Zde je příklad útoku CSRF:

1. Uživatel se přihlásí k www.example.com pomocí ověřování pomocí formulářů.
2. Server ověřuje uživatele. Odpověď ze serveru obsahuje ověřovací soubor cookie.
3. Bez odhlášení uživatel navštíví škodlivý web. Tento škodlivý web obsahuje následující formulář HTML:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Všimněte si, že akce formuláře příspěvky na ohrožený web, nikoli na škodlivý web. Jedná se o "cross-site" část CSRF.
4. Uživatel klepne na tlačítko odeslat. Prohlížeč obsahuje ověřovací soubor cookie s požadavkem.
5. Požadavek je spuštěn na example.com serveru s kontextem ověřování uživatele a může dělat cokoli, co může provést ověřený uživatel.

I když tento příklad vyžaduje, aby uživatel kliknul na tlačítko formuláře, škodlivá stránka může stejně snadno spustit skript, který odešle požadavek AJAX do aplikace SignalR. Použití protokolu SSL navíc nebrání útoku CSRF, protože škodlivý web může odeslat požadavek "https://".

Útoky CSRF jsou obvykle možné proti webovým stránkám, které používají soubory cookie pro ověřování, protože prohlížeče odesílají všechny příslušné soubory cookie na cílovou webovou stránku. Útoky CSRF se však neomezují pouze na zneužívání souborů cookie. Například základní a digest ověřování jsou také ohroženy. Po přihlášení uživatele pomocí základního ověřování nebo ověřování algoritmem Digest prohlížeč automaticky odešle pověření až do ukončení relace.

### <a name="csrf-mitigations-taken-by-signalr"></a>Zmírnění CSRF přijatá signalorem

SignalR provede následující kroky, aby zabránil škodlivému webu ve vytváření platných požadavků na vaši aplikaci. SignalR provede tyto kroky ve výchozím nastavení, není nutné provádět žádné akce v kódu.

- **Zakázání požadavků na příčné domény** SignalR zakáže požadavky mezi doménami zabránit uživatelům v volání koncového bodu SignalR z externí domény. SignalR považuje jakýkoli požadavek z externí domény za neplatný a blokuje požadavek. Doporučujeme zachovat toto výchozí chování; v opačném případě by škodlivý web mohl uživatele přimět k odesílání příkazů na váš web. Pokud potřebujete použít požadavky napříč doménami, přečtěte si informace [o tom, jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .
- **Předat token připojení v řetězci dotazu, nikoli v souboru cookie** SignalR předá token připojení jako hodnotu řetězce dotazu, nikoli jako soubor cookie. Uložení tokenu připojení do souboru cookie není bezpečné, protože prohlížeč může neúmyslně předat token připojení, když dojde ke škodlivému kódu. Také předání tokenu připojení v řetězci dotazu zabrání tokenu připojení přetrvávat za aktuální připojení. Uživatel se zlými úmysly proto nemůže podat požadavek pod pověřením ověřování jiného uživatele.
- **Ověření tokenu připojení** Jak je popsáno v části [Token připojení,](#connectiontoken) server ví, které ID připojení je přidruženo ke každému ověřenému uživateli. Server nezpracovává žádný požadavek z ID připojení, které neodpovídá uživatelskému jménu. Je nepravděpodobné, že by uživatel se zlými úmysly mohl uhodnout platný požadavek, protože uživatel se zlými úmysly by musel znát uživatelské jméno a aktuální id náhodně generovaného připojení. Toto id připojení se stane neplatným ihned po ukončení připojení. Anonymní uživatelé by neměli mít přístup k žádným citlivým informacím.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>Doporučení zabezpečení SignalR

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Protokol SSL (Secure Socket Layers)

Protokol SSL používá šifrování k zabezpečení přenosu dat mezi klientem a serverem. Pokud aplikace SignalR přenáší citlivé informace mezi klientem a serverem, použijte pro přenos ssl. Další informace o nastavení ssl naleznete v [tématu Jak nastavit ssl ve službě IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Nepoužívejte skupiny jako bezpečnostní mechanismus

Skupiny jsou pohodlným způsobem shromažďování souvisejících uživatelů, ale nejsou bezpečným mechanismem pro omezení přístupu k citlivým informacím. To platí zejména v případě, že uživatelé mohou automaticky znovu připojit skupiny během opětovného připojení. Místo toho zvažte přidání privilegovaných uživatelů do role a omezení přístupu k metodě rozbočovače pouze na členy této role. Příklad omezení přístupu na základě role naleznete v tématu [Ověřování a autorizace pro rozbočovače SignalR](hub-authorization.md). Příklad kontroly přístupu uživatelů ke skupinám při opětovném připojení naleznete v tématu [Práce se skupinami](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>Bezpečná manipulace se vstupy od klientů

Chcete-li zajistit, aby uživatel se zlými úmysly neodesílal skript jiným uživatelům, je nutné zakódovat veškerý vstup od klientů, který je určen pro vysílání jiným klientům. Měli byste kódovat zprávy na přijímající klienty, nikoli na serveru, protože aplikace SignalR může mít mnoho různých typů klientů. Kódování HTML proto funguje pro webového klienta, ale ne pro jiné typy klientů. Například metoda webového klienta pro zobrazení zprávy chatu by bezpečně `html()` zpracovat uživatelské jméno a zprávu voláním funkce.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Sladění změny stavu uživatele s aktivním připojením

Pokud se stav ověřování uživatele změní, zatímco existuje aktivní připojení, uživatel obdrží chybu, která uvádí, že identita uživatele se nemůže změnit během aktivního připojení SignalR. V takovém případě by se aplikace měla znovu připojit k serveru a ujistit se, že id připojení a uživatelské jméno jsou koordinovány. Například pokud aplikace umožňuje uživateli odhlásit, zatímco existuje aktivní připojení, uživatelské jméno pro připojení již nebude odpovídat název, který je předán pro další požadavek. Budete chtít zastavit připojení před uživatelem odhlásí a potom jej restartujte.

Je však důležité si uvědomit, že většina aplikací nebude nutné ručně zastavit a spustit připojení. Pokud aplikace přesměruje uživatele na samostatnou stránku po odhlášení, jako je například výchozí chování v aplikaci webových formulářů nebo MVC, nebo aktualizuje aktuální stránku po odhlášení, aktivní připojení se automaticky odpojí a nevyžaduje žádnou další akci.

Následující příklad ukazuje, jak zastavit a spustit připojení při změně stavu uživatele.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Nebo stav ověřování uživatele se může změnit, pokud váš web používá klouzavé vypršení platnosti s ověřováním pomocí formulářů a neexistuje žádná aktivita, která by udržela ověřovací soubor cookie platný. V takovém případě bude uživatel odhlášen a uživatelské jméno se již nebude shodovat s uživatelským jménem v tokenu připojení. Tento problém můžete vyřešit přidáním skriptu, který pravidelně požaduje prostředek na webovém serveru, aby byl ověřovací soubor cookie platný. Následující příklad ukazuje, jak požádat o prostředek každých 30 minut.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Automaticky generované soubory proxy JavaScriptu

Pokud nechcete zahrnout všechny rozbočovače a metody do souboru proxy JavaScript u každého uživatele, můžete zakázat automatické generování souboru. Tuto možnost můžete zvolit, pokud máte více rozbočovačů a metod, ale nechcete, aby si každý uživatel uvědomoval všechny metody. Automatické generování zakážete nastavením **enablejavascriptproxies** na **hodnotu false**.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

Další informace o souborech proxy javascriptu naleznete [v tématu Vygenerovaný proxy server a o tom, co pro vás dělá](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy). <a id="exceptions"></a>

### <a name="exceptions"></a>Výjimky

Měli byste se vyhnout předávání objektů výjimek klientům, protože objekty mohou klientům vystavit citlivé informace. Místo toho volání metody na straně klienta, který zobrazí příslušnou chybovou zprávu.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
