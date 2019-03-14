---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072319"
---
# <a name="key-vault-configuration-provider-sample-app"></a>Ukázkovou aplikaci v trezoru klíčů konfigurace zprostředkovatele

Tento příklad ukazuje použití konfigurace zprostředkovatele služby Azure Key Vault.

Ukázka spouští v jednom ze dvou režimů používaných určené `#define` příkazu v horní části *Program.cs* souboru. Pokyny najdete v tématu [direktivy preprocesoru ve vzorovém kódu](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):

* `Basic` &ndash; Ukazuje použití ID klienta aplikace Azure Key Vault a tajný klíč do access tajnými kódy uloženými v Azure Key Vault. Tuto verzi vzorku můžete spustit z libovolného místa a nasadit do Azure App Service nebo libovolného hostitele, která je schopná obsluhovat aplikace ASP.NET Core.
* `Managed` &ndash; Ukazuje, jak používat Azure [identita spravované služby](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) k ověření aplikace do služby Azure Key Vault pomocí ověřování Azure AD bez přihlašovacích údajů v kódu nebo konfigurace aplikace. ID klienta služby Azure AD a tajný kód se nevyžadují pro aplikace k ověření pomocí služby Azure Key Vault. Tato ukázka se musí nasadit do Azure App Service a prozkoumejte scearnio spravovaná identita.

Další informace najdete v tématu [konfigurace zprostředkovatele služby Azure Key Vault](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration).
