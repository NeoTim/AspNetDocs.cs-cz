---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073375"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>Jak sestavení nebo spuštění ukázková data zabezpečení uživatele

* Nastavení hesla pomocí nástroje Správce tajný kód:

  `dotnet user-secrets set SeedUserPW <pw>`

* Aktualizace databáze:

    `dotnet ef database update`

* Povolení HTTPS v projektu