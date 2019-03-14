---
ms.openlocfilehash: 0084d8c6bc5d16eaa1c3fa36d8aabb2aa31e1283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067453"
---
<a name="cli"></a>
## <a name="perform-initial-migration"></a>Provést počáteční migraci

Z příkazového řádku spusťte následující příkazy rozhraní příkazového řádku .NET Core:

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

`dotnet ef migrations add InitialCreate` Příkaz vygeneruje kód pro vytvoření schématu počáteční databáze. Schéma je založen na zadaném v modelu `DbContext` (v *Models/MvcMovieContext.cs* souboru). `Initial` Argument se používá k pojmenování migrace. Můžete použít libovolný název, ale podle konvence zvolte název, který popisuje migraci. Zobrazit [Úvod do migrace](xref:data/ef-mvc/migrations#introduction-to-migrations) Další informace.

`dotnet ef database update` Příkaz spustí `Up` metodu *migrace /\<časové razítko > _InitialCreate.cs* soubor, který vytvoří databázi.
