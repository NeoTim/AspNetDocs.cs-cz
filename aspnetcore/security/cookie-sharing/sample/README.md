---
ms.openlocfilehash: c3b00951d2f9e22a1c677a88261a36238d2b12fc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077125"
---
# <a name="cookie-sharing-sample-app"></a>Ukázková aplikace pro sdílení obsahu souboru cookie

Ukázka ilustruje soubor cookie pro sdílení obsahu napříč tři aplikace, které používala ověřování souborů cookie:

| Project                             | Popis |
| ----------------------------------- | ----------- |
| CookieAuth.Core                     | Aplikace ASP.NET Core Razor Pages bez použití technologie ASP.NET Core Identity |
| CookieAuthWithIdentity.Core         | Aplikace ASP.NET Core MVC s ASP.NET Core Identity |
| CookieAuthWithIdentity.NETFramework | Aplikace MVC rozhraní ASP.NET s ASP.NET Identity |

Pokyny:

1. Spusťte aplikaci CookieAuth.Core. Registrace uživatele. Aplikace ověřuje uživatele při registraci uživatele. Odhlaste uživatele.
1. Ve stejné relaci prohlížeče spusťte aplikaci CookieAuthWithIdentity.Core. Stejný uživatel zaregistrujte jako používané s aplikací jádra. Aplikace ověřuje uživatele při registraci uživatele. Odhlaste uživatele.
1. Ve stejné relaci prohlížeče spusťte aplikaci CookieAuthWithIdentity.NETFramework. Stejný uživatel zaregistrujte jako s jinými aplikacemi. Aplikace ověřuje uživatele při registraci uživatele. Odhlaste uživatele.
1. Přihlášení uživatele do všech tří aplikací. Soubor cookie ověřování je sdílen mezi aplikací. Všimněte si, že uživatel je automaticky přihlášeni k dvě aplikace.
1. Odhlaste uživatele z některé z aplikací. Všimněte si, že uživatel je automaticky odhlásí dvě aplikace.

Tato ukázka demonstruje funkce popsané v [sdílení souborů cookie mezi aplikacemi](https://docs.microsoft.com/aspnet/core/security/cookie-sharing) tématu.
