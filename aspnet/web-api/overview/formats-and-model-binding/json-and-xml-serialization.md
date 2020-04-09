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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>Serializace JSON a XML v ASP.NET webovérozhraní API

podle [Mike Wasson](https://github.com/MikeWasson)

Tento článek popisuje položky JSON a XML formatters v ASP.NET webovérozhraní API.

V ASP.NET webovérozhraní API je *formatter typu média* objekt, který může:

- Čtení objektů CLR z textu zprávy HTTP
- Zápis objektů CLR do těla zprávy HTTP

Webové rozhraní API poskytuje formáty typu médií pro jazyk JSON i XML. Rozhraní framework vloží tyto formatters do kanálu ve výchozím nastavení. Klienti mohou požádat o JSON nebo XML v hlavičce Přijmout požadavek HTTP.

## <a name="contents"></a>Obsah

- [JSON Media-Typ formovna](#json_media_type_formatter)

    - [Vlastnosti jen pro čtení](#json_readonly)
    - [Dates](#json_dates)
    - [Odsazení](#json_indenting)
    - [Velbloudí plášť](#json_camelcasing)
    - [Anonymní a slabě zadaný objekt](#json_anon)
- [Formátovací modul typu média XML](#xml_media_type_formatter)

    - [Vlastnosti jen pro čtení](#xml_readonly)
    - [Dates](#xml_dates)
    - [Odsazení](#xml_indenting)
    - [Nastavení serializátorů XML podle typu](#xml_pertype)
- [Odebrání formátovacího modulu JSON nebo XML](#removing_the_json_or_xml_formatter)
- [Zpracování cyklické odkazy na objekty](#handling_circular_object_references)
- [Testování serializace objektů](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Media-Typ formovna

Formátování JSON je poskytováno třídou **JsonMediaTypeFormatter.** Ve výchozím nastavení **používá jazyk JsonMediaTypeFormatter** k serializaci knihovnu [Json.NET.](https://github.com/JamesNK/Newtonsoft.Json) Json.NET je open source projekt třetí strany.

Pokud dáváte přednost, můžete nakonfigurovat **třídu JsonMediaTypeFormatter** tak, aby místo Json.NET používala **dataContractJsonSerializer.** Chcete-li tak učinit, nastavte **vlastnost UseDataContractJsonSerializer** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>Serializace JSON

Tato část popisuje některé specifické chování json formabodu pomocí výchozí [ho Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializátor. To nemá být komplexní dokumentace Json.NET knihovny; Další informace naleznete v [Json.NET dokumentace](http://james.newtonking.com/projects/json/help/).

#### <a name="what-gets-serialized"></a>Co dostane serializované?

Ve výchozím nastavení jsou všechny veřejné vlastnosti a pole zahrnuty v serializované MSON. Chcete-li vynechat vlastnost nebo pole, ozdobte je atributem **JsonIgnore.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

Pokud dáváte &quot;přednost&quot; opt-in přístup, ozdobte třídu s **DataContract** atribut. Pokud je tento atribut k dispozici, členové jsou ignorovány, pokud mají **DataMember**. **DataMember** můžete také použít k serializaci soukromých členů.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Vlastnosti jen pro čtení

Vlastnosti jen pro čtení jsou ve výchozím nastavení serializovány.

<a id="json_dates"></a>
### <a name="dates"></a>Dates

Ve výchozím nastavení Json.NET zapisuje data ve formátu [ISO 8601.](http://www.w3.org/TR/NOTE-datetime) Data v UTC (Koordinovaný světový čas) jsou napsána s příponou "Z". Data v místním čase zahrnují posun časového pásma. Příklad:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Ve výchozím nastavení Json.NET zachová časové pásmo. Tuto vlastnost můžete přepsat nastavením vlastnosti DateTimeZoneHandling:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

Pokud dáváte přednost použití formátu data`"\/Date(ticks)\/"`Microsoft [JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) ( ) namísto ISO 8601, nastavte vlastnost **DateFormatHandling** v nastavení serializátoru:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Odsazení

Chcete-li zapsat odsazené json, nastavte nastavení **formátování** na **Formátování.Odsazené**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Velbloudí plášť

Chcete-li zapsat názvy vlastností JSON s camel case, beze změny datového modelu, nastavte **CamelCasePropertyNamesContractresolver** na serializátoru:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Anonymní a slabě zadaný objekt

Metoda akce můžete vrátit anonymní objekt a serializovat jej JSON. Příklad:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Text zprávy odpovědi bude obsahovat následující JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Pokud vaše webové rozhraní API obdrží volně strukturované objekty JSON od klientů, můžete rekonstruovat tělo požadavku na typ **Newtonsoft.Json.Linq.JObject.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

Je však obvykle lepší použít datové objekty silného typu. Pak není nutné analyzovat data sami a získáte výhody ověřování modelu.

Serializátor XML nepodporuje anonymní typy nebo instance **JObject.** Pokud používáte tyto funkce pro data JSON, měli byste odebrat formátovací modul XML z kanálu, jak je popsáno dále v tomto článku.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>Formátovací modul typu média XML

Formátování XML je poskytováno třídou **XmlMediaTypeFormatter.** Ve výchozím nastavení používá třída **DataContractSerializer** k serializaci třídu **DataMediaTypeFormatter.**

Pokud chcete, můžete nakonfigurovat **XmlMediaTypeFormatter** použít **XmlSerializer** místo **DataContractSerializer**. Chcete-li tak učinit, nastavte vlastnost **UseXmlSerializer** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

Třída **XmlSerializer** podporuje užší sadu typů než **DataContractSerializer**, ale poskytuje větší kontrolu nad výsledným XML. Zvažte použití **xmlserializeru,** pokud potřebujete porovnat existující schéma XML.

### <a name="xml-serialization"></a>Serializace XML

Tato část popisuje některé specifické chování formátovacímodul XML pomocí **výchozího datacontractserializer**.

Ve výchozím nastavení se datacontractserializer chová takto:

- Všechny veřejné vlastnosti čtení a zápisu a pole jsou serializovány. Chcete-li vynechat vlastnost nebo pole, ozdobte je atributem **IgnoreDataMember.**
- Soukromé a chráněné členy nejsou serializovány.
- Vlastnosti jen pro čtení nejsou serializovány. (Obsah vlastnosti kolekce jen pro čtení jsou však serializovány.)
- Názvy tříd a členů jsou zapsány ve formátu XML přesně tak, jak jsou uvedeny v deklaraci třídy.
- Používá se výchozí obor názvů XML.

Pokud potřebujete větší kontrolu nad serializace, můžete ozdobit třídu s **DataContract** atribut. Pokud je tento atribut přítomen, třída je serializována následujícím způsobem:

- &quot;Přístup&quot; k přihlášení: Vlastnosti a pole nejsou ve výchozím nastavení serializovány. Chcete-li serializovat vlastnost nebo pole, ozdobte je atributem **DataMember.**
- Chcete-li serializovat soukromý nebo chráněný člen, ozdobte jej atributem **DataMember.**
- Vlastnosti jen pro čtení nejsou serializovány.
- Chcete-li změnit vzhled názvu třídy ve formátu XML, nastavte parametr *Name* v atributu **DataContract.**
- Chcete-li změnit zobrazení názvu člena ve formátu XML, nastavte parametr *Name* v atributu **DataMember.**
- Chcete-li změnit obor názvů XML, nastavte parametr *Obor názvů* ve třídě **DataContract.**

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Vlastnosti jen pro čtení

Vlastnosti jen pro čtení nejsou serializovány. Pokud vlastnost jen pro čtení má záložní soukromé pole, můžete označit soukromé pole atributem **DataMember.** Tento přístup vyžaduje **DataContract** atribut na třídu.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Dates

Data jsou napsána ve formátu ISO 8601. Například &quot;2012-05-23T20:21:37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Odsazení

Chcete-li zapsat odsazené XML, nastavte vlastnost **Odsazení** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Nastavení serializátorů XML podle typu

Můžete nastavit různé serializátory XML pro různé typy CLR. Můžete mít například určitý datový objekt, který vyžaduje **xmlserializer** pro zpětnou kompatibilitu. Pro tento objekt můžete použít **xmlserializer** a nadále používat **DataContractSerializer** pro jiné typy.

Chcete-li nastavit serializátor XML pro určitý typ, zavolejte **SetSerializer**.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Můžete určit **XmlSerializer** nebo libovolný objekt, který je odvozen z **XmlObjectSerializer**.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>Odebrání formátovacího modulu JSON nebo XML

Formátovací modul JSON nebo formátovací modul XML můžete odebrat ze seznamu formátovacích modulů, pokud je nechcete používat. Hlavní důvody k tomu jsou:

- Omezení odpovědí webového rozhraní API na určitý typ média. Můžete se například rozhodnout podporovat pouze odpovědi JSON a odebrat formátovací modul XML.
- Chcete-li nahradit výchozí formatter vlastní formatter. Například můžete nahradit json foropoledne s vlastní implementaci json foropoledne.

Následující kód ukazuje, jak odebrat výchozí formatters. Volání z metody **Start aplikace,\_** definované v Global.asax.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Zpracování cyklické odkazy na objekty

Ve výchozím nastavení json a XML formatters zapisovat všechny objekty jako hodnoty. Pokud dvě vlastnosti odkazují na stejný objekt, nebo pokud stejný objekt se zobrazí dvakrát v kolekci, modul pro formátování bude serializovat objekt dvakrát. Jedná se o zvláštní problém, pokud objekt grafu obsahuje cykly, protože serializátor vyvolá výjimku, když zjistí smyčku v grafu.

Zvažte následující objektové modely a řadič.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Vyvolání této akce způsobí, že modul pro formátování vyvolá výjimku, která se překládá na odpověď stavového kódu 500 (Vnitřní chyba serveru) klientovi.

Chcete-li zachovat odkazy na objekty v json, přidejte následující kód do metody **Start aplikace\_** v souboru Global.asax:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Nyní akce řadiče vrátí JSON, který vypadá takto:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Všimněte si, že &quot;&quot; serializátor přidá vlastnost $id k oběma objektům. Také zjistí, že Employee.Department vlastnost vytvoří smyčku, tak nahradí hodnotu&quot;odkazem na objekt: { $ref&quot;:&quot;1&quot;}.

> [!NOTE]
> Odkazy na objekty nejsou v jsonu standardní. Před použitím této funkce zvažte, zda budou vaši klienti schopni analyzovat výsledky. To by mohlo být lepší jednoduše odstranit cykly z grafu. Například odkaz ze zaměstnance zpět na oddělení není opravdu potřeba v tomto příkladu.

Chcete-li zachovat odkazy na objekty v xml, máte dvě možnosti. Jednodušší možností je `[DataContract(IsReference=true)]` přidat do třídy modelu. Parametr *IsReference* umožňuje odkazy na objekty. Nezapomeňte, že **DataContract** provádí serializace opt-in, takže budete také muset přidat **DataMember** atributy vlastnosti:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Nyní formátovací modul bude produkovat XML podobné následující:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Pokud se chcete vyhnout atributy ve třídě modelu, je další možnost: Vytvořte nový typ specifické **DataContractSerializer** instance a nastavte *preserveObjectReferences* **true** v konstruktoru. Potom nastavte tuto instanci jako serializátor pro typ na formátovací modul typu média XML. Následující kód ukazuje, jak to provést:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Testování serializace objektů

Při navrhování webového rozhraní API je užitečné otestovat, jak budou vaše datové objekty serializovány. Můžete to provést bez vytvoření řadiče nebo vyvolání akce řadiče.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
