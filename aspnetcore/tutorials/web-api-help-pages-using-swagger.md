---
title: Stránky nápovědy ASP.NET Core webového rozhraní API ve Swaggeru / OpenAPI
author: rsuter
description: Tento kurz poskytuje návod k přidávání Swagger generovat dokumentaci a stránky aplikace webového rozhraní API nápovědy.
ms.author: scaddie
ms.custom: mvc
ms.date: 09/20/2018
uid: tutorials/web-api-help-pages-using-swagger
ms.openlocfilehash: d7a6ed158dcb464bb80c83773ed7d455b25ce44b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073642"
---
# <a name="aspnet-core-web-api-help-pages-with-swagger--openapi"></a><span data-ttu-id="fee33-103">ASP.NET Core webové rozhraní API nápovědy stránky ve Swaggeru / OpenAPI</span><span class="sxs-lookup"><span data-stu-id="fee33-103">ASP.NET Core web API help pages with Swagger / OpenAPI</span></span>

<span data-ttu-id="fee33-104">Podle [Christoph Nienaber](https://twitter.com/zuckerthoben) a [Rico Suter](http://rsuter.com)</span><span class="sxs-lookup"><span data-stu-id="fee33-104">By [Christoph Nienaber](https://twitter.com/zuckerthoben) and [Rico Suter](http://rsuter.com)</span></span>

<span data-ttu-id="fee33-105">Při využívání webové rozhraní API, může vývojář náročné Principy jeho různé metody.</span><span class="sxs-lookup"><span data-stu-id="fee33-105">When consuming a Web API, understanding its various methods can be challenging for a developer.</span></span> <span data-ttu-id="fee33-106">[Swagger](https://swagger.io/), označované také jako [OpenAPI](https://www.openapis.org/), řeší problém generování užitečné stránky dokumentace a nápovědu pro webová rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fee33-106">[Swagger](https://swagger.io/), also known as [OpenAPI](https://www.openapis.org/), solves the problem of generating useful documentation and help pages for Web APIs.</span></span> <span data-ttu-id="fee33-107">Poskytuje výhody, jako je například interaktivní dokumentace, generování klientských sad SDK a rozhraní API zjistitelnost.</span><span class="sxs-lookup"><span data-stu-id="fee33-107">It provides benefits such as interactive documentation, client SDK generation, and API discoverability.</span></span>

<span data-ttu-id="fee33-108">V tomto článku [Swashbuckle.AspNetCore](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) a [službou NSwag](https://github.com/RSuter/NSwag) jsou konferenci .NET Swagger implementace:</span><span class="sxs-lookup"><span data-stu-id="fee33-108">In this article, the [Swashbuckle.AspNetCore](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) and [NSwag](https://github.com/RSuter/NSwag) .NET Swagger implementations are showcased:</span></span>

* <span data-ttu-id="fee33-109">**Swashbuckle.AspNetCore** je projekt open source pro generování dokumentů Swagger pro rozhraní Web API ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fee33-109">**Swashbuckle.AspNetCore** is an open source project for generating Swagger documents for ASP.NET Core Web APIs.</span></span>

* <span data-ttu-id="fee33-110">**Službou NSwag** je jiný projekt open source pro generování dokumentů Swagger a integraci [uživatelské rozhraní Swagger](https://swagger.io/swagger-ui/) nebo [ReDoc](https://github.com/Rebilly/ReDoc) do ASP.NET Core webová rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fee33-110">**NSwag** is another open source project for generating Swagger documents and integrating [Swagger UI](https://swagger.io/swagger-ui/) or [ReDoc](https://github.com/Rebilly/ReDoc) into ASP.NET Core web APIs.</span></span> <span data-ttu-id="fee33-111">Kromě toho službou NSwag nabízí přístupy ke generování jazyka C# a TypeScript klientský kód pro vaše rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fee33-111">Additionally, NSwag offers approaches to generate C# and TypeScript client code for your API.</span></span>

## <a name="what-is-swagger--openapi"></a><span data-ttu-id="fee33-112">Co je Swagger / OpenAPI?</span><span class="sxs-lookup"><span data-stu-id="fee33-112">What is Swagger / OpenAPI?</span></span>

<span data-ttu-id="fee33-113">Swagger se specifikace bez ohledu na jazyk pro popis [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fee33-113">Swagger is a language-agnostic specification for describing [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) APIs.</span></span> <span data-ttu-id="fee33-114">Projekt Swagger byl věnován na [OpenAPI iniciativy](https://www.openapis.org/), kde ji se nyní označuje jako OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="fee33-114">The Swagger project was donated to the [OpenAPI Initiative](https://www.openapis.org/), where it's now referred to as OpenAPI.</span></span> <span data-ttu-id="fee33-115">Oba názvy jsou používány Zaměnitelně; je však upřednostňované OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="fee33-115">Both names are used interchangeably; however, OpenAPI is preferred.</span></span> <span data-ttu-id="fee33-116">Umožňuje počítačům a lidí na široké možnosti produktu služby bez jakékoli přímý přístup k implementaci (zdrojový kód, přístup k síti, dokumentace ke službě).</span><span class="sxs-lookup"><span data-stu-id="fee33-116">It allows both computers and humans to understand the capabilities of a service without any direct access to the implementation (source code, network access, documentation).</span></span> <span data-ttu-id="fee33-117">Chcete-li minimalizovat množství práce potřebné pro připojení služby zrušeným přidružením je jedním z cílů.</span><span class="sxs-lookup"><span data-stu-id="fee33-117">One goal is to minimize the amount of work needed to connect disassociated services.</span></span> <span data-ttu-id="fee33-118">Jiné cílem je omezit množství času potřebného k přesně dokumentu služby.</span><span class="sxs-lookup"><span data-stu-id="fee33-118">Another goal is to reduce the amount of time needed to accurately document a service.</span></span>

## <a name="swagger-specification-swaggerjson"></a><span data-ttu-id="fee33-119">Specifikace swagger (swagger.json)</span><span class="sxs-lookup"><span data-stu-id="fee33-119">Swagger specification (swagger.json)</span></span>

<span data-ttu-id="fee33-120">Core do služby flow Swaggeru je specifikace Swagger&mdash;ve výchozím nastavení, dokumentu s názvem *swagger.json*.</span><span class="sxs-lookup"><span data-stu-id="fee33-120">The core to the Swagger flow is the Swagger specification&mdash;by default, a document named *swagger.json*.</span></span> <span data-ttu-id="fee33-121">Vygenerovala Swagger nástroj řetězu (nebo implementace jiných výrobců jeho) založené na vaši službu.</span><span class="sxs-lookup"><span data-stu-id="fee33-121">It's generated by the Swagger tool chain (or third-party implementations of it) based on your service.</span></span> <span data-ttu-id="fee33-122">Popisuje možnosti přístupu k němu přes HTTP a rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="fee33-122">It describes the capabilities of your API and how to access it with HTTP.</span></span> <span data-ttu-id="fee33-123">Řídí uživatelské rozhraní Swagger a používá řetězce nástrojů na povolit generování kódu klienta a zjišťování.</span><span class="sxs-lookup"><span data-stu-id="fee33-123">It drives the Swagger UI and is used by the tool chain to enable discovery and client code generation.</span></span> <span data-ttu-id="fee33-124">Tady je příklad specifikace Swagger pro zkrácení snížit:</span><span class="sxs-lookup"><span data-stu-id="fee33-124">Here's an example of a Swagger specification, reduced for brevity:</span></span>

```json
{
   "swagger": "2.0",
   "info": {
       "version": "v1",
       "title": "API V1"
   },
   "basePath": "/",
   "paths": {
       "/api/Todo": {
           "get": {
               "tags": [
                   "Todo"
               ],
               "operationId": "ApiTodoGet",
               "consumes": [],
               "produces": [
                   "text/plain",
                   "application/json",
                   "text/json"
               ],
               "responses": {
                   "200": {
                       "description": "Success",
                       "schema": {
                           "type": "array",
                           "items": {
                               "$ref": "#/definitions/TodoItem"
                           }
                       }
                   }
                }
           },
           "post": {
               ...
           }
       },
       "/api/Todo/{id}": {
           "get": {
               ...
           },
           "put": {
               ...
           },
           "delete": {
               ...
   },
   "definitions": {
       "TodoItem": {
           "type": "object",
            "properties": {
                "id": {
                    "format": "int64",
                    "type": "integer"
                },
                "name": {
                    "type": "string"
                },
                "isComplete": {
                    "default": false,
                    "type": "boolean"
                }
            }
       }
   },
   "securityDefinitions": {}
}
```

## <a name="swagger-ui"></a><span data-ttu-id="fee33-125">Uživatelské rozhraní swagger</span><span class="sxs-lookup"><span data-stu-id="fee33-125">Swagger UI</span></span>

<span data-ttu-id="fee33-126">[Uživatelské rozhraní swagger](https://swagger.io/swagger-ui/) nabízí uživatelské rozhraní založené na web, poskytující informace o službě pomocí generovaného specifikace Swagger.</span><span class="sxs-lookup"><span data-stu-id="fee33-126">[Swagger UI](https://swagger.io/swagger-ui/) offers a web-based UI that provides information about the service, using the generated Swagger specification.</span></span> <span data-ttu-id="fee33-127">Swashbuckle a službou NSwag obsahovat vložený verzi uživatelské rozhraní Swagger, tak, že je možné hostovat ve vaší aplikaci ASP.NET Core pomocí volání registrace middlewaru.</span><span class="sxs-lookup"><span data-stu-id="fee33-127">Both Swashbuckle and NSwag include an embedded version of Swagger UI, so that it can be hosted in your ASP.NET Core app using a middleware registration call.</span></span> <span data-ttu-id="fee33-128">Webové uživatelské rozhraní vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="fee33-128">The web UI looks like this:</span></span>

![Uživatelské rozhraní swagger](web-api-help-pages-using-swagger/_static/swagger-ui.png)

<span data-ttu-id="fee33-130">Každá metoda public akce ve vašich kontrolerech můžete otestovat v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="fee33-130">Each public action method in your controllers can be tested from the UI.</span></span> <span data-ttu-id="fee33-131">Klikněte na název metody, rozbalte v části.</span><span class="sxs-lookup"><span data-stu-id="fee33-131">Click a method name to expand the section.</span></span> <span data-ttu-id="fee33-132">Přidat všechny potřebné parametry a klikněte na tlačítko **vyzkoušejte ji!**.</span><span class="sxs-lookup"><span data-stu-id="fee33-132">Add any necessary parameters, and click **Try it out!**.</span></span>

![Příklad Swagger získat testu](web-api-help-pages-using-swagger/_static/get-try-it-out.png)

> [!NOTE]
> <span data-ttu-id="fee33-134">Uživatelské rozhraní Swagger verze použitá pro snímky obrazovky je verze 2.</span><span class="sxs-lookup"><span data-stu-id="fee33-134">The Swagger UI version used for the screenshots is version 2.</span></span> <span data-ttu-id="fee33-135">Například verze 3, naleznete v tématu [Petstore příklad](http://petstore.swagger.io/).</span><span class="sxs-lookup"><span data-stu-id="fee33-135">For a version 3 example, see [Petstore example](http://petstore.swagger.io/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fee33-136">Další kroky</span><span class="sxs-lookup"><span data-stu-id="fee33-136">Next steps</span></span>

* [<span data-ttu-id="fee33-137">Začínáme se službou Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="fee33-137">Get started with Swashbuckle</span></span>](xref:tutorials/get-started-with-swashbuckle)
* [<span data-ttu-id="fee33-138">Začínáme se službou NSwag</span><span class="sxs-lookup"><span data-stu-id="fee33-138">Get started with NSwag</span></span>](xref:tutorials/get-started-with-nswag)
