---
title: Distribuovaná mezipaměť pomocná rutina značek v ASP.NET Core
author: pkellner
description: Další informace o použití distribuované mezipaměti pomocná rutina značek v.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: a5b33451a763c297c6d7885855a321c43435abb4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071818"
---
# <a name="distributed-cache-tag-helper-in-aspnet-core"></a>Distribuovaná mezipaměť pomocná rutina značek v ASP.NET Core

Podle [Peter Kellner](http://peterkellner.net) a [Luke Latham](https://github.com/guardrex)

Pomocná rutina značek distribuované mezipaměti umožňuje výrazně zlepšit výkon vaší aplikace ASP.NET Core pomocí ukládání do mezipaměti obsah ke zdroji distribuované mezipaměti.

Přehled pomocných rutin značek, naleznete v tématu <xref:mvc/views/tag-helpers/intro>.

Distribuované mezipaměti pomocná rutina značek v dědí ze základní třídy stejné jako pomocné rutiny značky mezipaměti. Všechny [pomocná rutina značek v mezipaměti](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper) atributy jsou k dispozici pomocné rutiny značky distribuován.

Používá distribuované mezipaměti pomocná rutina značek v [konstruktor vkládání](xref:fundamentals/dependency-injection#constructor-injection-behavior). <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> Rozhraní je předána do konstruktoru distribuované mezipaměti pomocné rutiny značky společnosti. Pokud žádné konkrétní implementaci `IDistributedCache` se vytvoří v `Startup.ConfigureServices` (*Startup.cs*), distribuované mezipaměti pomocná rutina značek v používá stejný zprostředkovatel v paměti pro ukládání dat uložených v mezipaměti, jako [pomocná rutina značek mezipaměti](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).

## <a name="distributed-cache-tag-helper-attributes"></a>Distribuovaná mezipaměť atributy pomocné rutiny značky

### <a name="attributes-shared-with-the-cache-tag-helper"></a>Atributy dostaly pomocné rutiny značky mezipaměti

* `enabled`
* `expires-on`
* `expires-after`
* `expires-sliding`
* `vary-by-header`
* `vary-by-query`
* `vary-by-route`
* `vary-by-cookie`
* `vary-by-user`
* `vary-by priority`

Distribuované mezipaměti pomocná rutina značek v dědí ze stejné třídy jako pomocná rutina značek v mezipaměti. Popis těchto atributů najdete v článku [pomocná rutina značek v mezipaměti](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).

### <a name="name"></a>name

| Typ atributu | Příklad                               |
| -------------- | ------------------------------------- |
| String         | `my-distributed-cache-unique-key-101` |

`name` je vyžadován. `name` Atribut se používá jako klíč pro každou instanci uložených mezipaměti. Na rozdíl od mezipaměti pomocné rutiny značky, který přiřazuje klíč mezipaměti ke každé instanci, na základě názvu stránky Razor a umístění v stránky Razor, distribuované mezipaměti pomocná rutina značek v pouze základů svůj klíč atributu `name`.

Příklad:

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a>Implementace distribuované mezipaměti IDistributedCache pomocné rutiny značky

Existují dvě implementace <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> součástí ASP.NET Core. Jeden je založena na SQL Server, a druhý je založen na Redis. Podrobnosti o těchto implementacích najdete <xref:performance/caching/distributed>. Obou implementacích zahrnují nastavení instance objektu `IDistributedCache` v `Startup`.

Neexistují žádné atributy značky konkrétně spojených s použitím žádnou konkrétní implementaci `IDistributedCache`.

## <a name="additional-resources"></a>Další zdroje

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
