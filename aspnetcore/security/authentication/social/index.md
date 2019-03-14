---
title: 'Facebook, Google a externí zprostředkovatel ověřování v ASP.NET Core'
author: rick-anderson
description: Tento kurz ukazuje vytvoření ASP.NET Core 2.x aplikace pomocí externího zprostředkovatele ověřování OAuth 2.0.
ms.author: riande
ms.custom: mvc
ms.date: 1/19/2019
uid: security/authentication/social/index
---
# <a name="facebook-google-and-external-provider-authentication-in-aspnet-core"></a>Facebook, Google a externí zprostředkovatel ověřování v ASP.NET Core

Podle [Valeriy Novytskyy](https://github.com/01binary) a [Rick Anderson](https://twitter.com/RickAndMSFT)

Tento kurz ukazuje, jak vytvořit aplikaci 2.2 technologie ASP.NET Core, která umožňuje uživatelům přihlášení pomocí přihlašovacích údajů z externího zprostředkovatele ověřování OAuth 2.0.

[Facebook](xref:security/authentication/facebook-logins), [Twitter](xref:security/authentication/twitter-logins), [Google](xref:security/authentication/google-logins), a [Microsoft](xref:security/authentication/microsoft-logins) poskytovatelé jsou popsané v následujících částech. Ostatní zprostředkovatelé jsou k dispozici v balíčky třetích stran, jako [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) a [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers).

![Ikony sociálních médií pro Facebook, Twitter, Google, plus a Windows](index/_static/social.png)

Umožňuje uživatelům přihlašovat se pomocí existujících přihlašovacích údajů je pro uživatele pohodlný a posune mnoho složitých úkolů při správě procesu přihlašování do jiného výrobce. Příklady, jak sociální přihlášení můžete jednotka provoz a zákazníka převody, naleznete v tématu případové studie podle [Facebook](https://www.facebook.com/unsupportedbrowser) a [Twitter](https://dev.twitter.com/resources/case-studies).

## <a name="create-a-new-aspnet-core-project"></a>Vytvořte nový projekt ASP.NET Core

* V sadě Visual Studio 2017, vytvořte nový projekt z úvodní stránky, nebo prostřednictvím **souboru** > **nový** > **projektu**.

* Vyberte **webové aplikace ASP.NET Core** šablony, které jsou k dispozici v **Visual C#**   >  **.NET Core** kategorie:
* Vyberte **změna ověřování** a ověřování sady **jednotlivé uživatelské účty**.

## <a name="apply-migrations"></a>Použití migrace

* Spusťte aplikaci a vyberte **zaregistrovat** odkaz.
* Zadejte e-mail a heslo pro nový účet a potom vyberte **zaregistrovat**.
* Postupujte podle pokynů a použití migrace.

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a>Pomocí SecretManager ukládat tokeny přiřadil zprostředkovatele přihlášení

Přiřadit zprostředkovatele přihlášení prostřednictvím sociální sítě **Id aplikace** a **tajný klíč aplikace** tokeny během procesu registrace. Přesné token názvy lišit podle zprostředkovatele. Tyto tokeny představují přihlašovací údaje, které vaše aplikace používá pro přístup k rozhraní API. Tokeny představují "tajné", které lze propojit s díky konfiguraci aplikací [manažera tajných](xref:security/app-secrets#secret-manager). Tajný klíč správce je bezpečnější alternativu pro ukládání tokenů v konfiguračním souboru, například *appsettings.json*.

> [!IMPORTANT]
> Tajný klíč správce je jenom pro účely vývoje. Můžete ukládat a chránit Azure testovací a produkční tajných kódů pomocí [poskytovatele konfigurace služby Azure Key Vault](xref:security/key-vault-configuration).

Postupujte podle kroků v [bezpečné ukládání tajných kódů aplikace při vývoji v ASP.NET Core](xref:security/app-secrets) tématu pro ukládání tokenů přiřadil každý zprostředkovatele přihlášení níže.

## <a name="setup-login-providers-required-by-your-application"></a>Instalační program zprostředkovatele přihlášení požadovaná vaší aplikací

Ke konfiguraci vaší aplikaci použít příslušné poskytovatele použijte následující témata:

* [Facebook](xref:security/authentication/facebook-logins) pokyny
* [Twitter](xref:security/authentication/twitter-logins) pokyny
* [Google](xref:security/authentication/google-logins) pokyny
* [Microsoft](xref:security/authentication/microsoft-logins) pokyny
* [Jiný poskytovatel](xref:security/authentication/otherlogins) pokyny

[!INCLUDE[](includes/chain-auth-providers.md)]

## <a name="optionally-set-password"></a>Volitelně můžete nastavit heslo

Při registraci se externího zprostředkovatele přihlášení, není nutné heslo registrován s aplikací. To řeší jste od vytvoření a zapamatování hesla pro lokalitu, ale také umožňuje závisí na externího zprostředkovatele přihlášení. Pokud není k dispozici na externího zprostředkovatele přihlášení, nebudete moct přihlásit k webu.

Chcete-li vytvořit heslo a přihlaste se pomocí e-mailu, kterou jste nastavili během procesu přihlašování s externí zprostředkovatele:

* Vyberte **Hello &lt;e-mailový alias&gt;**  v pravém horním rohu přejít na odkaz **spravovat** zobrazení.

![Zobrazení Správa webové aplikace](index/_static/pass1a.png)

* Vyberte **Vytvořit**.

![Nastavte heslo stránku](index/_static/pass2a.png)

* Nastavili platné heslo a může být využit k přihlášení pomocí e-mailu.

## <a name="next-steps"></a>Další kroky

* Tento článek zavedené externího ověřování a vysvětlení požadovaných součástí pro přidání externí přihlášení do aplikace ASP.NET Core.

* Referenční stránky specifickým pro zprostředkovatele konfigurace přihlášení pro zprostředkovatele, které vaše aplikace vyžaduje.

* Můžete chtít zachovat další data o uživateli a jejich přístup a obnovovací tokeny. Další informace naleznete v tématu <xref:security/authentication/social/additional-claims>.
