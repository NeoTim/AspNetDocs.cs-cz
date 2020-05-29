---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Volání webového rozhraní API z klienta .NET (C#) – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET 4. x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172936"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="b762e-103">Volání webového rozhraní API z klienta .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="b762e-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="b762e-104">[Jan Wasson](https://github.com/MikeWasson) a [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b762e-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b762e-105">[Stažení dokončeného projektu](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="b762e-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="b762e-106">[Pokyny ke stažení](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b762e-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="b762e-107">V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET pomocí [System .NET. http. HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b762e-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="b762e-108">V tomto kurzu se napíše klientská aplikace, která využívá následující webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="b762e-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="b762e-109">Akce</span><span class="sxs-lookup"><span data-stu-id="b762e-109">Action</span></span> | <span data-ttu-id="b762e-110">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="b762e-110">HTTP method</span></span> | <span data-ttu-id="b762e-111">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="b762e-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b762e-112">Získat produkt podle ID</span><span class="sxs-lookup"><span data-stu-id="b762e-112">Get a product by ID</span></span> | <span data-ttu-id="b762e-113">GET</span><span class="sxs-lookup"><span data-stu-id="b762e-113">GET</span></span> | <span data-ttu-id="b762e-114">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="b762e-114">/api/products/*id*</span></span> |
| <span data-ttu-id="b762e-115">Vytvořit nový produkt</span><span class="sxs-lookup"><span data-stu-id="b762e-115">Create a new product</span></span> | <span data-ttu-id="b762e-116">POST</span><span class="sxs-lookup"><span data-stu-id="b762e-116">POST</span></span> | <span data-ttu-id="b762e-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="b762e-117">/api/products</span></span> |
| <span data-ttu-id="b762e-118">Aktualizace produktu</span><span class="sxs-lookup"><span data-stu-id="b762e-118">Update a product</span></span> | <span data-ttu-id="b762e-119">PUT</span><span class="sxs-lookup"><span data-stu-id="b762e-119">PUT</span></span> | <span data-ttu-id="b762e-120">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="b762e-120">/api/products/*id*</span></span> |
| <span data-ttu-id="b762e-121">Odstranění produktu</span><span class="sxs-lookup"><span data-stu-id="b762e-121">Delete a product</span></span> | <span data-ttu-id="b762e-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="b762e-122">DELETE</span></span> | <span data-ttu-id="b762e-123">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="b762e-123">/api/products/*id*</span></span> |

<span data-ttu-id="b762e-124">Informace o tom, jak implementovat toto rozhraní API s webovým rozhraním API ASP.NET, najdete v tématu [Vytvoření webového rozhraní API, které podporuje operace CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="b762e-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="b762e-125">Pro zjednodušení je klientská aplikace v tomto kurzu pro konzolovou aplikaci systému Windows.</span><span class="sxs-lookup"><span data-stu-id="b762e-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="b762e-126">**HttpClient** se také podporuje pro aplikace Windows Phone a Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b762e-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="b762e-127">Další informace najdete v tématu [Zápis kódu klienta webového rozhraní API pro více platforem pomocí přenosných knihoven](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b762e-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<span data-ttu-id="b762e-128">**Poznámka:** Pokud předáte základní adresy URL a relativní identifikátory URI jako pevně zakódované hodnoty, nezapomeňte na pravidla pro použití `HttpClient` rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b762e-128">**NOTE:** If you pass base URLs and relative URIs as hard-coded values, be mindful of the rules for utilizing the `HttpClient` API.</span></span> <span data-ttu-id="b762e-129">`HttpClient.BaseAddress`Vlastnost by měla být nastavená na adresu s koncovým lomítkem ( `/` ).</span><span class="sxs-lookup"><span data-stu-id="b762e-129">The `HttpClient.BaseAddress` property should be set to an address with a trailing forward slash (`/`).</span></span> <span data-ttu-id="b762e-130">Například při předávání pevně kódovaných identifikátorů URI prostředků do `HttpClient.GetAsync` metody nezahrnujte lomítko.</span><span class="sxs-lookup"><span data-stu-id="b762e-130">For example, when passing hard-coded resource URIs to the `HttpClient.GetAsync` method, don't include a leading forward slash.</span></span> <span data-ttu-id="b762e-131">Jak získat `Product` ID:</span><span class="sxs-lookup"><span data-stu-id="b762e-131">To get a `Product` by ID:</span></span>

1. <span data-ttu-id="b762e-132">Stanovenými`client.BaseAddress = new Uri("https://localhost:5001/");`</span><span class="sxs-lookup"><span data-stu-id="b762e-132">Set `client.BaseAddress = new Uri("https://localhost:5001/");`</span></span>
1. <span data-ttu-id="b762e-133">Žádost a `Product` .</span><span class="sxs-lookup"><span data-stu-id="b762e-133">Request a `Product`.</span></span> <span data-ttu-id="b762e-134">Například, `client.GetAsync<Product>("api/products/4");`.</span><span class="sxs-lookup"><span data-stu-id="b762e-134">For example, `client.GetAsync<Product>("api/products/4");`.</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="b762e-135">Vytvoření konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="b762e-135">Create the Console Application</span></span>

<span data-ttu-id="b762e-136">V aplikaci Visual Studio vytvořte novou konzolovou aplikaci pro Windows s názvem **HttpClientSample** a vložte ji do následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="b762e-136">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="b762e-137">Předchozí kód je kompletní klientská aplikace.</span><span class="sxs-lookup"><span data-stu-id="b762e-137">The preceding code is the complete client app.</span></span>

<span data-ttu-id="b762e-138">`RunAsync`spouští a blokuje až do dokončení.</span><span class="sxs-lookup"><span data-stu-id="b762e-138">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="b762e-139">Většina metod **HttpClient** je asynchronní, protože provádí v/v sítě.</span><span class="sxs-lookup"><span data-stu-id="b762e-139">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="b762e-140">Všechny asynchronní úlohy jsou prováděny v rámci `RunAsync` .</span><span class="sxs-lookup"><span data-stu-id="b762e-140">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="b762e-141">Obvykle aplikace neblokuje hlavní vlákno, ale tato aplikace nepovoluje žádnou interakci.</span><span class="sxs-lookup"><span data-stu-id="b762e-141">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="b762e-142">Instalace klientských knihoven webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="b762e-142">Install the Web API Client Libraries</span></span>

<span data-ttu-id="b762e-143">Pomocí Správce balíčků NuGet nainstalujte balíček klientské knihovny webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b762e-143">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="b762e-144">V nabídce **nástroje** vyberte možnost **Správce balíčků NuGet**  >  **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="b762e-144">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b762e-145">V konzole správce balíčků (PMC) zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="b762e-145">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="b762e-146">Předchozí příkaz přidá do projektu následující balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="b762e-146">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="b762e-147">Microsoft. AspNet. WebApi. Client</span><span class="sxs-lookup"><span data-stu-id="b762e-147">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="b762e-148">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b762e-148">Newtonsoft.Json</span></span>

<span data-ttu-id="b762e-149">Netwonsoft. JSON (označované také jako Json.NET) je oblíbený vysoce výkonný rozhraní JSON pro rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="b762e-149">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="b762e-150">Přidat třídu modelu</span><span class="sxs-lookup"><span data-stu-id="b762e-150">Add a Model Class</span></span>

<span data-ttu-id="b762e-151">Prověřte `Product` třídu:</span><span class="sxs-lookup"><span data-stu-id="b762e-151">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="b762e-152">Tato třída se shoduje s datovým modelem používaným webovým rozhraním API.</span><span class="sxs-lookup"><span data-stu-id="b762e-152">This class matches the data model used by the web API.</span></span> <span data-ttu-id="b762e-153">Aplikace může použít **HttpClient** ke čtení `Product` instance z odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="b762e-153">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="b762e-154">Aplikace nemusí zapisovat žádný kód deserializace.</span><span class="sxs-lookup"><span data-stu-id="b762e-154">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="b762e-155">Vytvoření a inicializace HttpClient</span><span class="sxs-lookup"><span data-stu-id="b762e-155">Create and Initialize HttpClient</span></span>

<span data-ttu-id="b762e-156">Prověřte vlastnost Static **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="b762e-156">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="b762e-157">**HttpClient** má být vytvořena instance jednou a znovu použita po celou dobu životnosti aplikace.</span><span class="sxs-lookup"><span data-stu-id="b762e-157">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="b762e-158">Následující podmínky mohou způsobit chyby **SocketException** :</span><span class="sxs-lookup"><span data-stu-id="b762e-158">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="b762e-159">Vytváří se nová instance **HttpClient** na žádost.</span><span class="sxs-lookup"><span data-stu-id="b762e-159">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="b762e-160">Server v případě vysoké zátěže.</span><span class="sxs-lookup"><span data-stu-id="b762e-160">Server under heavy load.</span></span>

<span data-ttu-id="b762e-161">Vytvoření nové instance **HttpClient** na žádost může vyčerpat dostupné sokety.</span><span class="sxs-lookup"><span data-stu-id="b762e-161">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="b762e-162">Následující kód Inicializuje instanci **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="b762e-162">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="b762e-163">Předcházející kód:</span><span class="sxs-lookup"><span data-stu-id="b762e-163">The preceding code:</span></span>

* <span data-ttu-id="b762e-164">Nastaví základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="b762e-164">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="b762e-165">Změňte číslo portu na port použitý v serverové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b762e-165">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="b762e-166">Aplikace nebude fungovat, pokud se nepoužije port pro serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b762e-166">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="b762e-167">Nastaví hlavičku Accept na "Application/JSON".</span><span class="sxs-lookup"><span data-stu-id="b762e-167">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="b762e-168">Nastavení této hlavičky oznamuje serveru, aby odesílal data ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="b762e-168">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="b762e-169">Odeslat požadavek GET k načtení prostředku</span><span class="sxs-lookup"><span data-stu-id="b762e-169">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="b762e-170">Následující kód odešle požadavek GET na produkt:</span><span class="sxs-lookup"><span data-stu-id="b762e-170">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="b762e-171">Metoda **GetAsync** ODEŠLE požadavek HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="b762e-171">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="b762e-172">Po dokončení metody vrátí **HttpResponseMessage** , který obsahuje odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="b762e-172">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="b762e-173">Pokud je stavový kód v odpovědi kód úspěšnosti, tělo odpovědi obsahuje reprezentaci kódu Product.</span><span class="sxs-lookup"><span data-stu-id="b762e-173">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="b762e-174">Zavolejte **ReadAsAsync** k deserializaci datové části JSON do `Product` instance.</span><span class="sxs-lookup"><span data-stu-id="b762e-174">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="b762e-175">Metoda **ReadAsAsync** je asynchronní, protože tělo odpovědi může být libovolně velké.</span><span class="sxs-lookup"><span data-stu-id="b762e-175">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="b762e-176">**HttpClient** nevyvolá výjimku, pokud odpověď HTTP obsahuje kód chyby.</span><span class="sxs-lookup"><span data-stu-id="b762e-176">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="b762e-177">Místo toho má vlastnost **IsSuccessStatusCode** **hodnotu false** , pokud je stav kód chyby.</span><span class="sxs-lookup"><span data-stu-id="b762e-177">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="b762e-178">Pokud dáváte přednost považovat kódy chyb HTTP jako výjimky, zavolejte [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) objektu Response.</span><span class="sxs-lookup"><span data-stu-id="b762e-178">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="b762e-179">`EnsureSuccessStatusCode`vyvolá výjimku, pokud stavový kód spadá mimo rozsah 200 &ndash; 299.</span><span class="sxs-lookup"><span data-stu-id="b762e-179">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="b762e-180">Všimněte si, že **HttpClient** může vyvolat výjimky z jiných důvodů &mdash; například v případě, že vyprší časový limit požadavku.</span><span class="sxs-lookup"><span data-stu-id="b762e-180">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="b762e-181">Formátovací moduly typu Media k deserializaci</span><span class="sxs-lookup"><span data-stu-id="b762e-181">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="b762e-182">Pokud je **ReadAsAsync** volán bez parametrů, používá výchozí sadu *formátovacích modulů médií* pro čtení těla odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b762e-182">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="b762e-183">Výchozí formátovací moduly podporují data zakódovaná JSON, XML a Form-URL.</span><span class="sxs-lookup"><span data-stu-id="b762e-183">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="b762e-184">Namísto použití výchozích formátovacích modulů můžete zadat seznam formátovacích modulů do metody **ReadAsAsync** .</span><span class="sxs-lookup"><span data-stu-id="b762e-184">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="b762e-185">Použití seznamu formátovacích modulů je užitečné, pokud máte vlastní formátovací modul typu média:</span><span class="sxs-lookup"><span data-stu-id="b762e-185">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="b762e-186">Další informace najdete v tématu [Formátování médií ve webovém rozhraní API 2 pro ASP.NET](../formats-and-model-binding/media-formatters.md) .</span><span class="sxs-lookup"><span data-stu-id="b762e-186">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="b762e-187">Odeslání požadavku POST k vytvoření prostředku</span><span class="sxs-lookup"><span data-stu-id="b762e-187">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="b762e-188">Následující kód odešle požadavek POST, který obsahuje `Product` instanci ve formátu JSON:</span><span class="sxs-lookup"><span data-stu-id="b762e-188">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="b762e-189">Metoda **PostAsJsonAsync** :</span><span class="sxs-lookup"><span data-stu-id="b762e-189">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="b762e-190">Serializace objektu do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="b762e-190">Serializes an object to JSON.</span></span>
* <span data-ttu-id="b762e-191">Odešle datovou část JSON v žádosti POST.</span><span class="sxs-lookup"><span data-stu-id="b762e-191">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="b762e-192">Pokud je požadavek úspěšný:</span><span class="sxs-lookup"><span data-stu-id="b762e-192">If the request succeeds:</span></span>

* <span data-ttu-id="b762e-193">Měla by vrátit odpověď 201 (vytvořeno).</span><span class="sxs-lookup"><span data-stu-id="b762e-193">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="b762e-194">Odpověď by měla obsahovat adresu URL vytvořených prostředků v hlavičce umístění.</span><span class="sxs-lookup"><span data-stu-id="b762e-194">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="b762e-195">Odeslání žádosti o vložení za účelem aktualizace prostředku</span><span class="sxs-lookup"><span data-stu-id="b762e-195">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="b762e-196">Následující kód odešle požadavek PUT k aktualizaci produktu:</span><span class="sxs-lookup"><span data-stu-id="b762e-196">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="b762e-197">Metoda **PutAsJsonAsync** funguje jako **PostAsJsonAsync**s tím rozdílem, že ODEŠLE požadavek PUT namísto post.</span><span class="sxs-lookup"><span data-stu-id="b762e-197">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="b762e-198">Odeslání žádosti o odstranění k odstranění prostředku</span><span class="sxs-lookup"><span data-stu-id="b762e-198">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="b762e-199">Následující kód pošle žádost o odstranění produktu:</span><span class="sxs-lookup"><span data-stu-id="b762e-199">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="b762e-200">Podobně jako GET, žádost o odstranění neobsahuje tělo žádosti.</span><span class="sxs-lookup"><span data-stu-id="b762e-200">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="b762e-201">Pomocí DELETE není nutné zadávat formát JSON nebo XML.</span><span class="sxs-lookup"><span data-stu-id="b762e-201">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="b762e-202">Test ukázky</span><span class="sxs-lookup"><span data-stu-id="b762e-202">Test the sample</span></span>

<span data-ttu-id="b762e-203">Testování klientské aplikace:</span><span class="sxs-lookup"><span data-stu-id="b762e-203">To test the client app:</span></span>

1. <span data-ttu-id="b762e-204">[Stáhněte](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) a spusťte serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b762e-204">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="b762e-205">[Pokyny ke stažení](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b762e-205">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="b762e-206">Ověřte, že aplikace serveru pracuje.</span><span class="sxs-lookup"><span data-stu-id="b762e-206">Verify the server app is working.</span></span> <span data-ttu-id="b762e-207">Například `http://localhost:64195/api/products` by měl vracet seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="b762e-207">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="b762e-208">Nastavte základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="b762e-208">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="b762e-209">Změňte číslo portu na port použitý v serverové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b762e-209">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="b762e-210">Spusťte klientskou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b762e-210">Run the client app.</span></span> <span data-ttu-id="b762e-211">Vytvoří se následující výstup:</span><span class="sxs-lookup"><span data-stu-id="b762e-211">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
