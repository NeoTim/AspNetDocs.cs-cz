---
title: Dvoufaktorové ověřování přes SMS v ASP.NET Core
author: rick-anderson
description: Zjistěte, jak nastavit dvojúrovňového ověřování (2FA) s aplikací ASP.NET Core.
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 09/22/2018
ms.custom: seodec18
uid: security/authentication/2fa
ms.openlocfilehash: 48bfc50378fc0ec212f5b9d4e7ce05bb4fc97b9d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074476"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a>Dvoufaktorové ověřování přes SMS v ASP.NET Core

Podle [Rick Anderson](https://twitter.com/RickAndMSFT) a [Swiss vývojáři](https://github.com/Swiss-Devs)

>[!WARNING]
> Dva faktoru ověřování (2FA), pomocí časovou synchronizací jednorázové heslo algoritmus (TOTP), jsou tyto aplikace v oboru doporučenému přístupu pro 2FA. 2FA pomocí TOTP je upřednostňována před SMS 2FA. Další informace najdete v tématu [generování kódu QR povolit pro TOTP aplikace v ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) pro ASP.NET Core 2.0 a novější.

Tento kurz ukazuje, jak nastavit dvojúrovňového ověřování (2FA) pomocí serveru SMS. Jsou uvedeny pokyny pro [twilio](https://www.twilio.com/) a [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), ale můžete použít jakýkoli jiný poskytovatel serveru SMS. Doporučujeme je provést [potvrzení účtu a obnovení hesla](xref:security/authentication/accconfirm) před zahájením tohoto kurzu.

[Zobrazení nebo stažení ukázkového kódu](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA). [Jak stáhnout](xref:index#how-to-download-a-sample).

## <a name="create-a-new-aspnet-core-project"></a>Vytvořte nový projekt ASP.NET Core

Vytvořit novou webovou aplikaci ASP.NET Core s názvem `Web2FA` s jednotlivými uživatelskými účty. Postupujte podle pokynů v <xref:security/enforcing-ssl> nastavit a vyžadují protokol HTTPS.

### <a name="create-an-sms-account"></a>Vytvoření účtu služby SMS

Vytvoření účtu služby SMS, například [twilio](https://www.twilio.com/) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/). Zaznamenejte přihlašovací údaje pro ověřování (pro twilio: accountSid a pro ASPSMS ověřovacího tokenu: Vlastnosti userkey jedná a heslo).

#### <a name="figuring-out-sms-provider-credentials"></a>Zjištění přihlašovací údaje poskytovatele serveru SMS

**Twilio:** Z karty řídicí panel svého účtu Twilio, zkopírujte **SID účtu** a **ověřovací token**.

**ASPSMS:** V nastavení účtu, přejděte na **vlastnosti userkey jedná** a zkopírujte ho spolu s vaší **heslo**.

Později jsme uloží tyto hodnoty se pomocí nástroje Správce tajný klíč v rámci klíče `SMSAccountIdentification` a `SMSAccountPassword`.

#### <a name="specifying-senderid--originator"></a>Určení SenderID / původce

**Twilio:** Na kartě čísla zkopírujte váš Twilio **telefonní číslo**.

**ASPSMS:** V rámci nabídky autoru odemknout odemknout jeden nebo více autoru nebo zvolte příkazce alfanumerické znaky (není podporováno ve všech sítích).

Dále jsme uloží tuto hodnotu pomocí nástroje Správce tajný klíč v klíči `SMSAccountFrom`.


### <a name="provide-credentials-for-the-sms-service"></a>Zadejte přihlašovací údaje služby SMS

Použijeme [možnosti vzor](xref:fundamentals/configuration/options) pro přístup k účtu a klíč nastavení.

   * Vytvoření třídy k načtení zabezpečený klíč serveru SMS. V tomto příkladu `SMSoptions` třída se vytvoří v *Services/SMSoptions.cs* souboru.

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

Nastavte `SMSAccountIdentification`, `SMSAccountPassword` a `SMSAccountFrom` s [manažera tajných nástroj](xref:security/app-secrets). Příklad:

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* Přidání balíčku NuGet pro poskytovatele serveru SMS. Z balíčku správce konzoly (konzolu PMC) spusťte:

**Twilio:**
`Install-Package Twilio`

**ASPSMS:**
`Install-Package ASPSMS`


* Přidejte kód *Services/MessageServices.cs* soubor serveru SMS. Použijte Twilio nebo ASPSMS části:


**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]

**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]

### <a name="configure-startup-to-use-smsoptions"></a>Konfigurace spuštění používat `SMSoptions`

Přidat `SMSoptions` ke kontejneru služby v `ConfigureServices` metodu *Startup.cs*:

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a>Povolení dvoufaktorového ověřování

Otevřít *Views/Manage/Index.cshtml* soubor zobrazení Razor a odeberte znaky komentáře (takže žádné značky je odkomentovaný).

## <a name="log-in-with-two-factor-authentication"></a>Přihlaste se pomocí dvojúrovňového ověřování

* Spusťte aplikaci a zaregistrovat nový uživatel

![Webová aplikace zaregistrovat, zobrazení otevřít v Microsoft Edge](2fa/_static/login2fa1.png)

* Klepněte na jméno uživatele, která se aktivuje `Index` metody akce v kontroleru spravovat. Potom klepněte na telefonní číslo **přidat** odkaz.

![Správa zobrazení – klepnout na odkaz "Přidání"](2fa/_static/login2fa2.png)

* Přidat telefonní číslo, který bude přijímat ověřovací kód a klepněte na **poslat ověřovací kód**.

![Přidat telefonní číslo stránky](2fa/_static/login2fa3.png)

* Zobrazí se zpráva SMS s ověřovacím kódem. Zadejte je a klepněte na **odeslat**

![Ověřit telefonní číslo stránky](2fa/_static/login2fa4.png)

Pokud vám textovou zprávu, přečtěte si téma twilio protokolu stránky.

* Správa zobrazení ukazuje že vaše telefonní číslo bylo úspěšně přidán.

![Správa zobrazení – telefonní číslo se úspěšně přidal](2fa/_static/login2fa5.png)

* Klepněte na **povolit** povolení dvoufaktorového ověřování.

![Správa zobrazení – povolení dvoufaktorového ověřování](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a>Test dvoufaktorového ověřování

* Odhlaste se.

* Přihlásit se.

* Uživatelský účet povolila dvojúrovňové ověřování, takže je nutné zadat druhý faktor ověřování. V tomto kurzu jste povolili ověření pomocí telefonu. Integrované šablony lze také nastavit e-mail jako druhý faktor. Můžete nastavit další druhý faktory pro ověřování, jako je kódy QR. Klepněte na **odeslat**.

![Poslat ověřovací kód zobrazení](2fa/_static/login2fa7.png)

* Zadejte kód, který se zobrazí ve zprávě SMS.

* Kliknutím na **chcete Zapamatovat tento prohlížeč** zaškrtávacího políčka můžete vyloučit před nutností pomocí 2FA přihlášení při použití stejného zařízení a prohlížeče. Povolení 2FA a kliknete na **chcete Zapamatovat tento prohlížeč** vám poskytne silné 2FA ochrany z uživateli se zlými úmysly pokusu o přístup ke svému účtu, za předpokladu, že nemají přístup k zařízení. Můžete to provést na libovolném privátní zařízení, kterou používáte pravidelně. Nastavením **chcete Zapamatovat tento prohlížeč**, získat zvýšení zabezpečení 2FA ze zařízení, které nepoužíváte pravidelně, a získáte usnadnění práce na nebudete muset absolvovat 2FA na vlastních zařízeních.

![Ověření zobrazení](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a>Uzamčení účtu pro ochranu před útoky hrubou silou

Uzamčení účtu, doporučujeme pomocí 2FA. Když se uživatel přihlásí pomocí místního účtu nebo účtu na sociální síti, se ukládají jednotlivé neúspěšné pokusy o na 2FA. Pokud je dosaženo maximální neúspěšných pokusů o přístup, je uživatel uzamčen (výchozí: 5 minut uzamčení po 5 neúspěšných pokusů o přístup). Po provedení úspěšného ověření resetuje počet pokusů o neúspěšných přístupů a resetuje na hodiny. Maximální počet neúspěšných pokusů o přístup a doby uzamčení lze nastavit pomocí [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) a [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan). Následující nakonfiguruje uzamčení účtu po dobu 10 minut po 10 neúspěšných pokusů o přístup:

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

Ujistěte se, že [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) nastaví `lockoutOnFailure` k `true`:

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
