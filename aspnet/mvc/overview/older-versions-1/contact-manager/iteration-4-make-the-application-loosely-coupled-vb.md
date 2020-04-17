---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: 'Iterace #4 – Proveďte aplikaci volně spřažené (VB) | Dokumenty společnosti Microsoft'
author: rick-anderson
description: V této čtvrté iteraci využíváme několik vzorů návrhu softwaru, abychom usnadnili údržbu a úpravu aplikace Správce kontaktů. Pro...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 1026e307b7e498a8b1392f2907c08cdcd05a3199
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542765"
---
# <a name="iteration-4--make-the-application-loosely-coupled-vb"></a>Iterace č. 4 – vytvoření volně spárované aplikace (VB)

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout kód](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> V této čtvrté iteraci využíváme několik vzorů návrhu softwaru, abychom usnadnili údržbu a úpravu aplikace Správce kontaktů. Například refaktorujeme naši aplikaci tak, aby používala vzor úložiště a vzor vkládání závislostí.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Vytvoření aplikace pro správu kontaktů ASP.NET MVC (VB)

V této sérii kurzů vytvoříme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Contact Manager umožňuje ukládat kontaktní informace - jména, telefonní čísla a e-mailové adresy - pro seznam osob.

Vytvoříme aplikaci přes více iterací. S každou iterací postupně vylepšujeme aplikaci. Cílem tohoto přístupu více iterace je umožnit pochopit důvod pro každou změnu.

- Iterace #1 - Vytvořte aplikaci. V první iteraci vytvoříme Správce kontaktů nejjednodušším možným způsobem. Přidáváme podporu pro základní databázové operace: Vytvořit, Číst, Aktualizovat a odstranit (CRUD).

- Iterace #2 - Make aplikace vypadat hezky. V této iteraci vylepšujeme vzhled aplikace úpravou výchozí ASP.NET stránku předlohy zobrazení MVC a kaskádovou šablonu stylů.

- #3 iterace – přidejte ověření formuláře. Ve třetí iteraci přidáme ověření základního formuláře. Bráníme uživatelům v odesílání formuláře bez vyplnění požadovaných polí formuláře. Ověřujeme také e-mailové adresy a telefonní čísla.

- Iterace #4 - Proveďte aplikaci volně spojená. V této čtvrté iteraci využíváme několik vzorů návrhu softwaru, abychom usnadnili údržbu a úpravu aplikace Správce kontaktů. Například refaktorujeme naši aplikaci tak, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 - vytvořit testy částí. V páté iteraci usnadňujeme údržbu a úpravy naší aplikace přidáním testů částí. Zesměšňujeme naše třídy datových modelů a vytváříme testy částí pro naše řadiče a logiku ověřování.

- Iterace #6 – použijte vývoj řízený testem. V této šesté iteraci přidáme nové funkce do naší aplikace zápisem testů částí první a psaní kódu proti testování částí. V této iteraci přidáme skupiny kontaktů.

- Iterace #7 - Přidat funkci Ajax. V sedmé iteraci zlepšujeme odezvu a výkon naší aplikace přidáním podpory pro Ajax.

## <a name="this-iteration"></a>Tato iterace

V této čtvrté iteraci aplikace Contact Manager refaktorujeme aplikaci tak, aby byla aplikace volněji spojena. Pokud je aplikace volně spojena, můžete upravit kód v jedné části aplikace bez nutnosti měnit kód v jiných částech aplikace. Volně vázané aplikace jsou odolnější vůči změnám.

V současné době je veškerá logika přístupu k datům a ověřování používaná aplikací Správce kontaktů obsažena ve třídách kontroleru. Tohle je špatný nápad. Kdykoli budete potřebovat upravit jednu část aplikace, riskujete zavedení chyb do jiné části aplikace. Pokud například změníte logiku ověřování, riskujete zavedení nových chyb do logiky přístupu k datům nebo řadiče.

> [!NOTE] 
> 
> (SRP), třída by nikdy neměla mít více než jeden důvod ke změně. Míchání řadič, ověřování a databázové logiky je masivní porušení principu jednotné odpovědnosti.

Existuje několik důvodů, které může být nutné upravit aplikaci. Možná budete muset přidat novou funkci do aplikace, budete muset opravit chybu v aplikaci nebo budete muset změnit způsob implementace funkce aplikace. Aplikace jsou zřídka statické. Mají tendenci růst a mutovat v průběhu času.

Představte si například, že se rozhodnete změnit způsob implementace vrstvy přístupu k datům. Aplikace Správce kontaktů právě teď používá rozhraní Microsoft Entity Framework pro přístup k databázi. Můžete se však rozhodnout pro migraci na novou nebo alternativní technologii přístupu k datům, jako je ADO.NET datové služby nebo NHibernate. Však vzhledem k tomu, že přístupový kód dat není izolován od ověřovacího kódu a kódu řadiče, neexistuje žádný způsob, jak změnit kód přístupu k datům ve vaší aplikaci bez úpravy jiného kódu, který přímo nesouvisí s přístupem k datům.

Pokud je aplikace volně spojena, můžete naopak provádět změny v jedné části aplikace, aniž byste se dotkli jiných částí aplikace. Můžete například přepínat technologie přístupu k datům bez změny logiky ověřování nebo řadiče.

V této iteraci využíváme několik vzorů návrhu softwaru, které nám umožňují refaktorovat naši aplikaci Contact Manager do volněji vázané aplikace. Po dokončení správce kontaktů neuděláte nic, co předtím neudělal. V budoucnu však budeme moci aplikaci snadněji změnit.

> [!NOTE] 
> 
> Refaktoring je proces přepisování aplikace takovým způsobem, že neztratí žádné existující funkce.

## <a name="using-the-repository-software-design-pattern"></a>Použití návrhu softwaru úložiště

Naší první změnou je využít vzor návrhu softwaru nazvaný vzor úložiště. Vzor úložiště použijeme k izolujeme náš přístupový kód k datům od zbytku naší aplikace.

Implementace vzoru úložiště vyžaduje, abychom dokončili následující dva kroky:

1. Vytvoření rozhraní
2. Vytvoření konkrétní třídy, která implementuje rozhraní

Nejprve musíme vytvořit rozhraní, které popisuje všechny metody přístupu k datům, které musíme provést. Rozhraní IContactManagerRepository je obsaženo v výpisu 1. Toto rozhraní popisuje pět metod: CreateContact(), DeleteContact(), EditContact(), GetContact a ListContacts().

**Výpis 1 - Modely\IContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

Dále potřebujeme vytvořit konkrétní třídu, která implementuje rozhraní IContactManagerRepository. Protože používáme Microsoft Entity Framework pro přístup k databázi, vytvoříme novou třídu s názvem EntityContactManagerRepository. Tato třída je obsažena v výpisu 2.

**Výpis 2 - Modely\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

Všimněte si, že třída EntityContactManagerRepository implementuje rozhraní IContactManagerRepository. Třída implementuje všech pět metod popsaných tímto rozhraním.

Možná se divíte, proč se musíme obtěžovat s rozhraním. Proč musíme vytvořit rozhraní a třídu, která jej implementuje?

S jednou výjimkou bude zbytek naší aplikace pracovat s rozhraním a nikoli s konkrétní třídou. Místo volání metody vystavené EntityContactManagerRepository třídy, budeme volat metody vystavené rozhraní IContactManagerRepository.

Tímto způsobem můžeme implementovat rozhraní s novou třídou bez nutnosti upravovat zbytek naší aplikace. Například v nějaké budoucí datum můžeme chtít implementovat Třídu DataServicesContactManagerRepository, která implementuje rozhraní IContactManagerRepository. Třída DataServicesContactManagerRepository může používat ADO.NET datové služby pro přístup k databázi namísto rozhraní Microsoft Entity Framework.

Pokud je náš kód aplikace naprogramován proti rozhraní IContactManagerRepository namísto konkrétní třídy EntityContactManagerRepository, můžeme přepnout konkrétní třídy bez úpravy některého z našich kódů. Například můžeme přepnout z entityContactManagerRepository třídy do třídy DataServicesContactManagerRepository bez změny naší logiky přístupu k datům nebo ověření.

Programování proti rozhraní (abstrakce) namísto konkrétní třídy je naše aplikace odolnější vůči změnám.

> [!NOTE] 
> 
> Můžete rychle vytvořit rozhraní z konkrétní třídy v rámci sady Visual Studio výběrem možnosti nabídky Refactor, Extrahovat rozhraní. Můžete například nejprve vytvořit třídu EntityContactManagerRepository a potom použít rozhraní Extrahovat k automatickému generování rozhraní IContactManagerRepository.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Použití návrhového vzoru softwaru vkládání závislostí

Teď, když jsme migrovali náš kód pro přístup k datům do samostatné třídy úložiště, musíme upravit náš řadič kontaktů tak, aby používal tuto třídu. Budeme využívat vzor návrhu softwaru s názvem Vkládání závislostí k použití třídy úložiště v našem řadiči.

Upravený řadič kontaktů je obsažen v výpisu 3.

**Výpis 3 - Řadiče\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

Všimněte si, že řadič kontaktu v výpisu 3 má dva konstruktory. První konstruktor předá konkrétní instanci rozhraní IContactManagerRepository druhému konstruktoru. Třída řadiče Kontakt používá *vkládání závislostí konstruktoru*.

Jediné místo, které entityContactManagerRepository třídy se používá je v prvním konstruktoru. Zbytek třídy používá rozhraní IContactManagerRepository namísto konkrétní entityContactManagerRepository třídy.

To usnadňuje přepínání implementace třídy IContactManagerRepository v budoucnu. Pokud chcete použít třídu DataServicesContactRepository namísto třídy EntityContactManagerRepository, stačí upravit první konstruktor.

Vkládání závislostí konstruktoru také umožňuje třídu řadiče Kontaktu velmi testovatelnou. V testování částí můžete vytvořit instanci řadiče kontaktu předáním falešné implementace třídy IContactManagerRepository. Tato funkce vkládání závislostí bude pro nás velmi důležité v další iteraci při vytváření testů částí pro aplikaci Správce kontaktů.

> [!NOTE] 
> 
> Pokud chcete zcela oddělit třídu řadiče kontaktu od konkrétní implementace rozhraní IContactManagerRepository, můžete využít výhod rozhraní, které podporuje vkládání závislostí, jako je StructureMap nebo Microsoft Entity Framework (MEF). Využitím rozhraní vkládání závislostí, nikdy nebudete muset odkazovat na konkrétní třídy v kódu.

## <a name="creating-a-service-layer"></a>Vytvoření vrstvy služby

Možná jste si všimli, že naše logika ověřování je stále smíchána s naší logikou řadiče v upravené třídě kontroleru v výpisu 3. Ze stejného důvodu, že je vhodné izolovat naši logiku přístupu k datům, je vhodné izolovat naši logiku ověřování.

Chcete-li tento problém vyřešit, můžeme vytvořit samostatnou [vrstvu služby](http://martinfowler.com/eaaCatalog/serviceLayer.html). Vrstva služby je samostatná vrstva, kterou můžeme vložit mezi naše třídy řadiče a úložiště. Vrstva služby obsahuje naši obchodní logiku včetně veškeré naší logiky ověřování.

Služba ContactManagerService je obsažena ve výpisu 4. Obsahuje logiku ověření z třídy řadič kontakt.

**Výpis 4 - Modely\ContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

Všimněte si, že konstruktor pro ContactManagerService vyžaduje ValidationDictionary. Vrstva služby komunikuje s vrstvou kontroleru prostřednictvím tohoto ValidationDictionary. Budeme diskutovat ValidationDictionary podrobně v následující části, když budeme diskutovat decorator vzor.

Všimněte si dále, že ContactManagerService implementuje rozhraní IContactManagerService. Vždy byste měli usilovat o program proti rozhraní namísto konkrétní třídy. Ostatní třídy v aplikaci Správce kontaktů nepracují přímo s třídou ContactManagerService. Místo toho s jednou výjimkou je zbytek aplikace Contact Manager naprogramován proti rozhraní IContactManagerService.

Rozhraní IContactManagerService je obsaženo v výpisu 5.

**Výpis 5 - Modely\IContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

Upravená třída kontrolora kontaktu je obsažena v výpisu 6. Všimněte si, že řadič kontaktů již nespolupracuje s úložištěm ContactManager. Místo toho řadič kontaktu spolupracuje se službou ContactManager. Každá vrstva je izolována co nejvíce od jiných vrstev.

**Výpis 6 - Řadiče\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

Naše aplikace již není v rozporu se zásadou jednotné odpovědnosti (SRP). Kontrolor kontaktů v seznamu 6 byl zbaven všech jiných než řízení toku provádění aplikací. Veškerá logika ověření byla odebrána z řadiče kontaktu a zatlačena do vrstvy služby. Všechny logiky databáze byla posunuta do vrstvy úložiště.

## <a name="using-the-decorator-pattern"></a>Použití dekoratér vzor

Chceme být schopni zcela oddělit naši servisní vrstvu od naší vrstvy regulátoru. V zásadě bychom měli být schopni sestavit naši vrstvu služby v samostatné sestavě z naší vrstvy kontroleru bez nutnosti přidávat odkaz na naši aplikaci MVC.

Naše vrstva služeb však musí být schopna předat chybové zprávy ověření zpět do vrstvy kontroleru. Jak můžeme povolit vrstvě služby komunikovat ověřovací chybové zprávy bez propojení řadiče a vrstvy služby? Můžeme využít vzor návrhu softwaru s názvem [Decorator vzor](http://en.wikipedia.org/wiki/Decorator_pattern).

Řadič používá ModelStateDictionary s názvem ModelState představují chyby ověření. Proto může být v pokušení předat ModelState z vrstvy kontroleru do vrstvy služby. Použití ModelState ve vrstvě služby by však vaše vrstva služby závisela na funkci ASP.NET rámci MVC. To by bylo špatné, protože jednoho dne můžete chtít použít vrstvu služby s aplikací WPF namísto aplikace ASP.NET MVC. V takovém případě byste nechtěli odkazovat na ASP.NET mvc rozhraní pro použití třídy ModelStateDictionary.

Decorator vzor umožňuje zabalit existující třídy v nové třídě za účelem implementace rozhraní. Náš projekt Contact Manager zahrnuje třídu ModelStateWrapper obsaženou v výpisu 7. Třída ModelStateWrapper implementuje rozhraní v výpisu 8.

**Výpis 7 - Modely\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**Výpis 8 - Modely\Ověření\IValidationDictionary.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

Pokud se podíváte zblízka na výpis 5 pak uvidíte, že vrstva služby ContactManager používá výhradně rozhraní IValidationDictionary. Služba ContactManager není závislá na třídě ModelStateDictionary. Když řadič kontaktu vytvoří službu ContactManager, řadič zabalí svůj ModelState takto:

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>Souhrn

V této iteraci jsme do aplikace Správce kontaktů nepřidali žádné nové funkce. Cílem této iterace bylo refaktorovat aplikaci Správce kontaktů tak, aby se snadněji udržovala a upravovala.

Nejprve jsme implementovali vzor návrhu softwaru úložiště. Migrovali jsme všechny kódy pro přístup k datům do samostatné třídy úložiště ContactManager.

Také jsme izolovali naši logiku ověřování z naší logiky řadiče. Vytvořili jsme samostatnou vrstvu služby, která obsahuje všechny naše ověřovací kód. Vrstva kontroleru spolupracuje s vrstvou služby a vrstva služby spolupracuje s vrstvou úložiště.

Když jsme vytvořili vrstvu služby, jsme využili decorator vzor izolovat ModelState z naší vrstvy služby. V naší vrstvě služby jsme naprogramovali proti rozhraní IValidationDictionary namísto ModelState.

Nakonec jsme využili vzor návrhu softwaru s názvem vzor vkládání závislostí. Tento vzor nám umožňuje programovat proti rozhraní (abstrakce) namísto konkrétní třídy. Implementace vzor návrhu vkládání závislostí také umožňuje náš kód více testovatelné. V další iteraci přidáme testy částí do našeho projektu.

> [!div class="step-by-step"]
> [Předchozí](iteration-3-add-form-validation-vb.md)
> [další](iteration-5-create-unit-tests-vb.md)
