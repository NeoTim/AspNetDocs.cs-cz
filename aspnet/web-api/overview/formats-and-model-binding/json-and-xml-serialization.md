---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Serializace Jazyka JSON a XML ve webovém rozhraní API ASP.NET – ASP.NET 4.x
author: MikeWasson
description: Popisuje formáty JSON a XML v ASP.NET webovém rozhraní API pro ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676221"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="a8a7d-103">Serializace JSON a XML v ASP.NET webovérozhraní API</span><span class="sxs-lookup"><span data-stu-id="a8a7d-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="a8a7d-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a8a7d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a8a7d-105">Tento článek popisuje položky JSON a XML formatters v ASP.NET webovérozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="a8a7d-106">V ASP.NET webovérozhraní API je *formatter typu média* objekt, který může:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="a8a7d-107">Čtení objektů CLR z textu zprávy HTTP</span><span class="sxs-lookup"><span data-stu-id="a8a7d-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="a8a7d-108">Zápis objektů CLR do těla zprávy HTTP</span><span class="sxs-lookup"><span data-stu-id="a8a7d-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="a8a7d-109">Webové rozhraní API poskytuje formáty typu médií pro jazyk JSON i XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="a8a7d-110">Rozhraní framework vloží tyto formatters do kanálu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="a8a7d-111">Klienti mohou požádat o JSON nebo XML v hlavičce Přijmout požadavek HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="a8a7d-112">Obsah</span><span class="sxs-lookup"><span data-stu-id="a8a7d-112">Contents</span></span>

- [<span data-ttu-id="a8a7d-113">JSON Media-Typ formovna</span><span class="sxs-lookup"><span data-stu-id="a8a7d-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="a8a7d-114">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="a8a7d-115">Dates</span><span class="sxs-lookup"><span data-stu-id="a8a7d-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="a8a7d-116">Odsazení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="a8a7d-117">Velbloudí plášť</span><span class="sxs-lookup"><span data-stu-id="a8a7d-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="a8a7d-118">Anonymní a slabě zadaný objekt</span><span class="sxs-lookup"><span data-stu-id="a8a7d-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="a8a7d-119">Formátovací modul typu média XML</span><span class="sxs-lookup"><span data-stu-id="a8a7d-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="a8a7d-120">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="a8a7d-121">Dates</span><span class="sxs-lookup"><span data-stu-id="a8a7d-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="a8a7d-122">Odsazení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="a8a7d-123">Nastavení serializátorů XML podle typu</span><span class="sxs-lookup"><span data-stu-id="a8a7d-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="a8a7d-124">Odebrání formátovacího modulu JSON nebo XML</span><span class="sxs-lookup"><span data-stu-id="a8a7d-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="a8a7d-125">Zpracování cyklické odkazy na objekty</span><span class="sxs-lookup"><span data-stu-id="a8a7d-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="a8a7d-126">Testování serializace objektů</span><span class="sxs-lookup"><span data-stu-id="a8a7d-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="a8a7d-127">JSON Media-Typ formovna</span><span class="sxs-lookup"><span data-stu-id="a8a7d-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="a8a7d-128">Formátování JSON je poskytováno třídou **JsonMediaTypeFormatter.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="a8a7d-129">Ve výchozím nastavení **používá jazyk JsonMediaTypeFormatter** k serializaci knihovnu [Json.NET.](https://github.com/JamesNK/Newtonsoft.Json)</span><span class="sxs-lookup"><span data-stu-id="a8a7d-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="a8a7d-130">Json.NET je open source projekt třetí strany.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="a8a7d-131">Pokud dáváte přednost, můžete nakonfigurovat **třídu JsonMediaTypeFormatter** tak, aby místo Json.NET používala **dataContractJsonSerializer.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="a8a7d-132">Chcete-li tak učinit, nastavte **vlastnost UseDataContractJsonSerializer** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="a8a7d-133">Serializace JSON</span><span class="sxs-lookup"><span data-stu-id="a8a7d-133">JSON Serialization</span></span>

<span data-ttu-id="a8a7d-134">Tato část popisuje některé specifické chování json formabodu pomocí výchozí [ho Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializátor.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="a8a7d-135">To nemá být komplexní dokumentace Json.NET knihovny; Další informace naleznete v [Json.NET dokumentace](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="a8a7d-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="a8a7d-136">Co dostane serializované?</span><span class="sxs-lookup"><span data-stu-id="a8a7d-136">What Gets Serialized?</span></span>

<span data-ttu-id="a8a7d-137">Ve výchozím nastavení jsou všechny veřejné vlastnosti a pole zahrnuty v serializované MSON.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="a8a7d-138">Chcete-li vynechat vlastnost nebo pole, ozdobte je atributem **JsonIgnore.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="a8a7d-139">Pokud dáváte &quot;přednost&quot; opt-in přístup, ozdobte třídu s **DataContract** atribut.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="a8a7d-140">Pokud je tento atribut k dispozici, členové jsou ignorovány, pokud mají **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="a8a7d-141">**DataMember** můžete také použít k serializaci soukromých členů.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="a8a7d-142">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-142">Read-Only Properties</span></span>

<span data-ttu-id="a8a7d-143">Vlastnosti jen pro čtení jsou ve výchozím nastavení serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="a8a7d-144">Dates</span><span class="sxs-lookup"><span data-stu-id="a8a7d-144">Dates</span></span>

<span data-ttu-id="a8a7d-145">Ve výchozím nastavení Json.NET zapisuje data ve formátu [ISO 8601.](http://www.w3.org/TR/NOTE-datetime)</span><span class="sxs-lookup"><span data-stu-id="a8a7d-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="a8a7d-146">Data v UTC (Koordinovaný světový čas) jsou napsána s příponou "Z".</span><span class="sxs-lookup"><span data-stu-id="a8a7d-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="a8a7d-147">Data v místním čase zahrnují posun časového pásma.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="a8a7d-148">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="a8a7d-149">Ve výchozím nastavení Json.NET zachová časové pásmo.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="a8a7d-150">Tuto vlastnost můžete přepsat nastavením vlastnosti DateTimeZoneHandling:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="a8a7d-151">Pokud dáváte přednost použití formátu data`"\/Date(ticks)\/"`Microsoft [JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ( ) namísto ISO 8601, nastavte vlastnost **DateFormatHandling** v nastavení serializátoru:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="a8a7d-152">Odsazení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-152">Indenting</span></span>

<span data-ttu-id="a8a7d-153">Chcete-li zapsat odsazené json, nastavte nastavení **formátování** na **Formátování.Odsazené**:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="a8a7d-154">Velbloudí plášť</span><span class="sxs-lookup"><span data-stu-id="a8a7d-154">Camel Casing</span></span>

<span data-ttu-id="a8a7d-155">Chcete-li zapsat názvy vlastností JSON s camel case, beze změny datového modelu, nastavte **CamelCasePropertyNamesContractresolver** na serializátoru:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="a8a7d-156">Anonymní a slabě zadaný objekt</span><span class="sxs-lookup"><span data-stu-id="a8a7d-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="a8a7d-157">Metoda akce můžete vrátit anonymní objekt a serializovat jej JSON.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="a8a7d-158">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="a8a7d-159">Text zprávy odpovědi bude obsahovat následující JSON:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="a8a7d-160">Pokud vaše webové rozhraní API obdrží volně strukturované objekty JSON od klientů, můžete rekonstruovat tělo požadavku na typ **Newtonsoft.Json.Linq.JObject.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="a8a7d-161">Je však obvykle lepší použít datové objekty silného typu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="a8a7d-162">Pak není nutné analyzovat data sami a získáte výhody ověřování modelu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="a8a7d-163">Serializátor XML nepodporuje anonymní typy nebo instance **JObject.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="a8a7d-164">Pokud používáte tyto funkce pro data JSON, měli byste odebrat formátovací modul XML z kanálu, jak je popsáno dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="a8a7d-165">Formátovací modul typu média XML</span><span class="sxs-lookup"><span data-stu-id="a8a7d-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="a8a7d-166">Formátování XML je poskytováno třídou **XmlMediaTypeFormatter.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="a8a7d-167">Ve výchozím nastavení používá třída **DataContractSerializer** k serializaci třídu **DataMediaTypeFormatter.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="a8a7d-168">Pokud chcete, můžete nakonfigurovat **XmlMediaTypeFormatter** použít **XmlSerializer** místo **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="a8a7d-169">Chcete-li tak učinit, nastavte vlastnost **UseXmlSerializer** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="a8a7d-170">Třída **XmlSerializer** podporuje užší sadu typů než **DataContractSerializer**, ale poskytuje větší kontrolu nad výsledným XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="a8a7d-171">Zvažte použití **xmlserializeru,** pokud potřebujete porovnat existující schéma XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="a8a7d-172">Serializace XML</span><span class="sxs-lookup"><span data-stu-id="a8a7d-172">XML Serialization</span></span>

<span data-ttu-id="a8a7d-173">Tato část popisuje některé specifické chování formátovacímodul XML pomocí **výchozího datacontractserializer**.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="a8a7d-174">Ve výchozím nastavení se datacontractserializer chová takto:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="a8a7d-175">Všechny veřejné vlastnosti čtení a zápisu a pole jsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="a8a7d-176">Chcete-li vynechat vlastnost nebo pole, ozdobte je atributem **IgnoreDataMember.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="a8a7d-177">Soukromé a chráněné členy nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="a8a7d-178">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="a8a7d-179">(Obsah vlastnosti kolekce jen pro čtení jsou však serializovány.)</span><span class="sxs-lookup"><span data-stu-id="a8a7d-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="a8a7d-180">Názvy tříd a členů jsou zapsány ve formátu XML přesně tak, jak jsou uvedeny v deklaraci třídy.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="a8a7d-181">Používá se výchozí obor názvů XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-181">A default XML namespace is used.</span></span>

<span data-ttu-id="a8a7d-182">Pokud potřebujete větší kontrolu nad serializace, můžete ozdobit třídu s **DataContract** atribut.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="a8a7d-183">Pokud je tento atribut přítomen, třída je serializována následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="a8a7d-184">&quot;Přístup&quot; k přihlášení: Vlastnosti a pole nejsou ve výchozím nastavení serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="a8a7d-185">Chcete-li serializovat vlastnost nebo pole, ozdobte je atributem **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="a8a7d-186">Chcete-li serializovat soukromý nebo chráněný člen, ozdobte jej atributem **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="a8a7d-187">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="a8a7d-188">Chcete-li změnit vzhled názvu třídy ve formátu XML, nastavte parametr *Name* v atributu **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="a8a7d-189">Chcete-li změnit zobrazení názvu člena ve formátu XML, nastavte parametr *Name* v atributu **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="a8a7d-190">Chcete-li změnit obor názvů XML, nastavte parametr *Obor názvů* ve třídě **DataContract.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="a8a7d-191">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-191">Read-Only Properties</span></span>

<span data-ttu-id="a8a7d-192">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="a8a7d-193">Pokud vlastnost jen pro čtení má záložní soukromé pole, můžete označit soukromé pole atributem **DataMember.**</span><span class="sxs-lookup"><span data-stu-id="a8a7d-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="a8a7d-194">Tento přístup vyžaduje **DataContract** atribut na třídu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="a8a7d-195">Dates</span><span class="sxs-lookup"><span data-stu-id="a8a7d-195">Dates</span></span>

<span data-ttu-id="a8a7d-196">Data jsou napsána ve formátu ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="a8a7d-197">Například &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="a8a7d-198">Odsazení</span><span class="sxs-lookup"><span data-stu-id="a8a7d-198">Indenting</span></span>

<span data-ttu-id="a8a7d-199">Chcete-li zapsat odsazené XML, nastavte vlastnost **Odsazení** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="a8a7d-200">Nastavení serializátorů XML podle typu</span><span class="sxs-lookup"><span data-stu-id="a8a7d-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="a8a7d-201">Můžete nastavit různé serializátory XML pro různé typy CLR.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="a8a7d-202">Můžete mít například určitý datový objekt, který vyžaduje **xmlserializer** pro zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="a8a7d-203">Pro tento objekt můžete použít **xmlserializer** a nadále používat **DataContractSerializer** pro jiné typy.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="a8a7d-204">Chcete-li nastavit serializátor XML pro určitý typ, zavolejte **SetSerializer**.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="a8a7d-205">Můžete určit **XmlSerializer** nebo libovolný objekt, který je odvozen z **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="a8a7d-206">Odebrání formátovacího modulu JSON nebo XML</span><span class="sxs-lookup"><span data-stu-id="a8a7d-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="a8a7d-207">Formátovací modul JSON nebo formátovací modul XML můžete odebrat ze seznamu formátovacích modulů, pokud je nechcete používat.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="a8a7d-208">Hlavní důvody k tomu jsou:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="a8a7d-209">Omezení odpovědí webového rozhraní API na určitý typ média.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="a8a7d-210">Můžete se například rozhodnout podporovat pouze odpovědi JSON a odebrat formátovací modul XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="a8a7d-211">Chcete-li nahradit výchozí formatter vlastní formatter.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="a8a7d-212">Například můžete nahradit json foropoledne s vlastní implementaci json foropoledne.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="a8a7d-213">Následující kód ukazuje, jak odebrat výchozí formatters.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="a8a7d-214">Volání z metody **Start aplikace,\_** definované v Global.asax.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="a8a7d-215">Zpracování cyklické odkazy na objekty</span><span class="sxs-lookup"><span data-stu-id="a8a7d-215">Handling Circular Object References</span></span>

<span data-ttu-id="a8a7d-216">Ve výchozím nastavení json a XML formatters zapisovat všechny objekty jako hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="a8a7d-217">Pokud dvě vlastnosti odkazují na stejný objekt, nebo pokud stejný objekt se zobrazí dvakrát v kolekci, modul pro formátování bude serializovat objekt dvakrát.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="a8a7d-218">Jedná se o zvláštní problém, pokud objekt grafu obsahuje cykly, protože serializátor vyvolá výjimku, když zjistí smyčku v grafu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="a8a7d-219">Zvažte následující objektové modely a řadič.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="a8a7d-220">Vyvolání této akce způsobí, že modul pro formátování vyvolá výjimku, která se překládá na odpověď stavového kódu 500 (Vnitřní chyba serveru) klientovi.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="a8a7d-221">Chcete-li zachovat odkazy na objekty v json, přidejte následující kód do metody **Start aplikace\_** v souboru Global.asax:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="a8a7d-222">Nyní akce řadiče vrátí JSON, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="a8a7d-223">Všimněte si, že &quot;&quot; serializátor přidá vlastnost $id k oběma objektům.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="a8a7d-224">Také zjistí, že Employee.Department vlastnost vytvoří smyčku, tak nahradí hodnotu&quot;odkazem na objekt: { $ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="a8a7d-225">Odkazy na objekty nejsou v jsonu standardní.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="a8a7d-226">Před použitím této funkce zvažte, zda budou vaši klienti schopni analyzovat výsledky.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="a8a7d-227">To by mohlo být lepší jednoduše odstranit cykly z grafu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="a8a7d-228">Například odkaz ze zaměstnance zpět na oddělení není opravdu potřeba v tomto příkladu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="a8a7d-229">Chcete-li zachovat odkazy na objekty v xml, máte dvě možnosti.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="a8a7d-230">Jednodušší možností je `[DataContract(IsReference=true)]` přidat do třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="a8a7d-231">Parametr *IsReference* umožňuje odkazy na objekty.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="a8a7d-232">Nezapomeňte, že **DataContract** provádí serializace opt-in, takže budete také muset přidat **DataMember** atributy vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="a8a7d-233">Nyní formátovací modul bude produkovat XML podobné následující:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="a8a7d-234">Pokud se chcete vyhnout atributy ve třídě modelu, je další možnost: Vytvořte nový typ specifické **DataContractSerializer** instance a nastavte *preserveObjectReferences* **true** v konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="a8a7d-235">Potom nastavte tuto instanci jako serializátor pro typ na formátovací modul typu média XML.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="a8a7d-236">Následující kód ukazuje, jak to provést:</span><span class="sxs-lookup"><span data-stu-id="a8a7d-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="a8a7d-237">Testování serializace objektů</span><span class="sxs-lookup"><span data-stu-id="a8a7d-237">Testing Object Serialization</span></span>

<span data-ttu-id="a8a7d-238">Při navrhování webového rozhraní API je užitečné otestovat, jak budou vaše datové objekty serializovány.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="a8a7d-239">Můžete to provést bez vytvoření řadiče nebo vyvolání akce řadiče.</span><span class="sxs-lookup"><span data-stu-id="a8a7d-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
