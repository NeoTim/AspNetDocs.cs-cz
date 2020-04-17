---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Použití CAPTCHA, aby se zabránilo Roboty z používání vašeho ASP.NET Web Břitva) stránek | Dokumenty společnosti Microsoft
author: rick-anderson
description: Tento článek vysvětluje, jak používat ReCaptcha (bezpečnostní opatření), aby se zabránilo automatizované programy (roboty) z provádění úkolů v ASP.NET webových stránek (Břitva) jsme ...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543753"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Použití CAPTCHA, aby se zabránilo Roboty z používání vašeho ASP.NET Web Břitva) stránek

podle [společnosti Microsoft](https://github.com/microsoft)

> Tento článek vysvětluje, jak pomocí recaptcha (bezpečnostní opatření) zabránit automatizovaným programům (robotům) v provádění úloh na webu ASP.NET webových stránek (Razor).
> 
> **Naučíte se:** 
> 
> - Jak přidat test CAPTCHA na vaše stránky.
> 
> Jedná se o ASP.NET funkce uvedené v článku:
> 
> - Pomocník. `ReCaptcha`
> 
> > [!NOTE]
> > Informace v tomto článku platí pro ASP.NET webových stránek 1.0 a webových stránek 2.

## <a name="about-captchas"></a>O captchas

Kdykoli vynecháte lidi zaregistrovat na vašem webu, nebo dokonce jen zadat jméno a URL (jako pro blog komentář), můžete získat záplavu falešných jmen. Ty jsou často ponechány automatizovanými programy (roboty), které se pokoušejí nechat adresy URL na všech webových stránkách, které mohou najít. (Běžnou motivací je zveřejňovat adresy URL produktů na prodej.)

Můžete pomoci zajistit, že uživatel je skutečná osoba a není počítačový program pomocí *CAPTCHA* k ověření uživatelů při registraci nebo jinak zadat jejich jméno a web. CAPTCHA je zkratka pro zcela automatizovaný veřejný Turingův test, který říká počítačům a lidem. CAPTCHA je *test výzvy a odezvy,* ve kterém je uživatel požádán, aby udělal něco, co je pro člověka snadné, ale pro automatizovaný program je těžké. Nejběžnějšítyp CAPTCHA je ten, kde vidíte některé zkreslené písmena a jsou vyzváni k jejich zadání. (Zkreslení má ztížit botům rozluštit písmena.)

## <a name="adding-a-recaptcha-test"></a>Přidání testu ReCaptcha

V ASP.NET stránek můžete `ReCaptcha` pomocí pomocné položky vykreslit test CAPTCHA, který[http://recaptcha.net](http://recaptcha.net)je založen na službě ReCaptcha ( ). Pomocník `ReCaptcha` zobrazí obrázek dvou zkreslených slov, které musí uživatelé zadat správně před ověřením stránky. Odpověď uživatele je ověřena službou ReCaptcha.Net.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Zaregistrujte své webové[http://recaptcha.net](http://recaptcha.net)stránky na ReCaptcha.Net ( ). Po dokončení registrace získáte veřejný a soukromý klíč.
2. Pokud jste tak ještě neučinili , přidejte na web knihovnu ASP.NET webových [pomocníků,](https://go.microsoft.com/fwlink/?LinkId=252372)jak je popsáno v části Instalace pomocníků na webu ASP.NET , pokud jste tak již neučinili.
3. Pokud ještě nemáte soubor * \_AppStart.cshtml,* vytvořte v kořenové složce webu soubor s názvem * \_AppStart.cshtml*.
4. Do souboru `Recaptcha` * \_AppStart.cshtml* přidejte následující nastavení pomocníka: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Nastavte `PublicKey` vlastnosti a `PrivateKey` pomocí vlastních veřejných a soukromých klíčů.
6. Uložte soubor * \_AppStart.cshtml* a zavřete jej.
7. V kořenové složce webu vytvořte novou stránku s názvem *Recaptcha.cshtml*.
8. Nahraďte existující obsah následujícím: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Spusťte stránku *Recaptcha.cshtml* v prohlížeči. Pokud `PrivateKey` je hodnota platná, stránka zobrazí ovládací prvek ReCaptcha a tlačítko. Pokud jste nenastavili klíče globálně v * \_AppStart.html*, stránka by se zobrazí chyba. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Zadejte slova pro test. Pokud projdete testrecaptcha, zobrazí se zpráva v tomto smyslu. V opačném případě se zobrazí chybová zpráva a ovládací prvek ReCaptcha se znovu zobrazí.

> [!NOTE]
> Pokud je počítač v doméně, která používá proxy `defaultproxy` server, bude pravděpodobně nutné nakonfigurovat prvek souboru *Web.config.* Následující příklad ukazuje soubor *Web.config* s `defaultproxy` prvkem nakonfigurovaným tak, aby služba ReCaptcha fungovala.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další zdroje

- [Přizpůsobení chování na celém webu pro ASP.NET weby webových stránek](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Web ReCaptcha](https://www.google.com/recaptcha)
