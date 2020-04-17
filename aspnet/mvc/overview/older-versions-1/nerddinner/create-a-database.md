---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Vytvoření databáze | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 2 ukazuje kroky k vytvoření databáze, která obsahuje všechna data večeře a RSVP pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541608"
---
# <a name="create-a-database"></a>Vytvoření databáze

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 2 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 2 ukazuje kroky k vytvoření databáze, která obsahuje všechna data večeře a RSVP pro naši aplikaci NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner Krok 2: Vytvoření databáze

Budeme používat databázi pro uložení všech večeři a RSVP data pro naši aplikaci NerdDinner.

Následující kroky ukazují vytvoření databáze pomocí bezplatné edice SQL Server Express (kterou můžete snadno nainstalovat pomocí V2 [Instalační služby webové platformy společnosti Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)). Veškerý kód, který napíšeme, funguje jak s SQL Server Express, tak s úplným SQL Serverem.

### <a name="creating-a-new-sql-server-express-database"></a>Vytvoření nové databáze SQL Server Express

Začneme kliknutím pravým tlačítkem myši na náš webový projekt a pak vybereme příkaz Nabídky **Přidat&gt;novou položku:**

![](create-a-database/_static/image1.png)

Tím se zobrazí dialogové okno "Přidat novou položku" sady Visual Studio. Budeme filtrovat podle kategorie "Data" a vybereme šablonu položky "Sql Server Database":

![](create-a-database/_static/image2.png)

Pojmenujeme databázi SQL Server Express, kterou chceme vytvořit "NerdDinner.mdf" a stiskneme ok. Visual Studio se pak nás zeptá, jestli chceme\_přidat tento soubor do našeho adresáře \App Data (což je adresář, který je již nastaven s seznamy ACN zabezpečení čtení i zápisu):

![](create-a-database/_static/image3.png)

Klikneme na tlačítko "Ano" a naše nová databáze bude vytvořena a přidána do našeho Průzkumníka řešení:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Vytváření tabulek v naší databázi

Nyní máme novou prázdnou databázi. Přidáme k tomu nějaké tabulky.

K tomu přejdeme do okna karty Průzkumník serveru v sadě Visual Studio, které nám umožňuje spravovat databáze a servery. Databáze SQL Server Express uložené\_ve složce \App Data naší aplikace se automaticky zobrazí v Průzkumníku serveru. Volitelně můžeme použít ikonu "Připojit k databázi" v horní části okna "Průzkumník serveru" přidat další sql server databází (místní i vzdálené) do seznamu také:

![](create-a-database/_static/image5.png)

Přidáme dvě tabulky do naší databáze NerdDinner – jeden pro uložení našich večeří a druhý pro sledování přijetí RSVP k nim. Nové tabulky můžeme vytvořit kliknutím pravým tlačítkem myši na složku "Tabulky" v naší databázi a výběrem příkazu nabídky "Přidat novou tabulku":

![](create-a-database/_static/image6.png)

Tím se otevře návrhář tabulky, který nám umožňuje konfigurovat schéma naší tabulky. Pro naši tabulku "Večeře" přidáme 10 sloupců dat:

![](create-a-database/_static/image7.png)

Chceme, aby sloupec "DinnerID" byl jedinečný primární klíč pro tabulku. Můžeme to nakonfigurovat kliknutím pravým tlačítkem myši na sloupec "DinnerID" a výběrem položky nabídky "Nastavit primární klíč":

![](create-a-database/_static/image8.png)

Kromě toho, že DinnerID primární klíč, chceme také nakonfigurovat jako sloupec "identity", jehož hodnota je automaticky zvýšena jako nové řádky dat jsou přidány do tabulky (což znamená, že první vložený řádek Večeře bude mít DinnerID 1, druhý vložený řádek bude mít DinnerID 2, atd.).

Můžeme to provést výběrem sloupce "DinnerID" a potom pomocí editoru "Vlastnosti sloupce" nastavit vlastnost "(Je identita)" ve sloupci na "Ano". Použijeme výchozí hodnoty standardní identity (začínáme na 1 a přírůstek 1 na každém novém řádku večeři):

![](create-a-database/_static/image9.png)

Tabulku pak uložíme zadáním ctrl-s nebo pomocí příkazu **Nabídka&gt;Soubor- Uložit.** To nás vyzve k názvu tabulky. Pojmenujeme to "Večeře":

![](create-a-database/_static/image10.png)

Naše nová tabulka Večeře se pak zobrazí v naší databázi v průzkumníku serveru.

Poté zopakujeme výše uvedené kroky a vytvoříme tabulku "RSVP". Tato tabulka má 3 sloupce. Jako primární klíč nastavíme sloupec RsvpID a také z něj uděláme sloupec identity:

![](create-a-database/_static/image11.png)

Uložíme ho a dáme mu jméno "RSVP".

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Nastavení relace cizího klíče mezi tabulkami

Nyní máme v naší databázi dvě tabulky. Náš poslední krok návrhu schématu bude nastavení relace "1:N" mezi těmito dvěma tabulkami – abychom mohli přidružit každý řádek Večeři s nulou nebo více řádky RSVP, které se na něj vztahují. Provedeme to tak, že nakonfigurujeme sloupec "DinnerID" tabulky RSVP tak, aby měl vztah cizího klíče ke sloupci "DinnerID" v tabulce "Dinners".

K tomu otevřeme tabulku RSVP v návrháři tabulky poklepáním v průzkumníku serveru. Poté v něm vybereme sloupec "DinnerID", klikněte pravým tlačítkem myši a zvolíme "Vztahy..." kontextová nabídka, příkaz:

![](create-a-database/_static/image12.png)

Tím se zobrazí dialogové okno, které můžeme použít k nastavení relací mezi tabulkami:

![](create-a-database/_static/image13.png)

Kliknutím na tlačítko Přidat přidáme do dialogového okna nový vztah. Po přidání relace rozbalíme uzel stromového zobrazení "Tabulky a specifikace sloupce" v rámci mřížky vlastností napravo od dialogového okna a poté klikneme na "..." napravo od něj:

![](create-a-database/_static/image14.png)

Kliknutím na tlačítko "..." tlačítko zobrazí další dialog, který nám umožní určit, které tabulky a sloupce jsou zapojeny do relace, stejně jako nám umožní pojmenovat vztah.

Změníme tabulku primárního klíče na "Večeře" a jako primární klíč vybereme sloupec DinnerID v tabulce Večeře. Naše tabulka RSVP bude tabulka cizího klíče a RSVP. Sloupec DinnerID bude přidružen jako cizí klíč:

![](create-a-database/_static/image15.png)

Nyní bude každý řádek v tabulce RSVP přidružen k řádku v tabulce Večeři. SQL Server bude udržovat referenční integritu pro nás – a zabránit nám v přidání nového řádku RSVP, pokud neodkazuje na platný řádek Dinner. Zabrání nám také odstranění řádku Dinner, pokud na něj stále odkazují řádky RSVP.

### <a name="adding-data-to-our-tables"></a>Přidávání dat do našich tabulek

Na závěr přidáme některá ukázková data do tabulky Večeře. Data můžeme do tabulky přidat tak, že na ně klikneme pravým tlačítkem myši v Průzkumníku serveru a vyberete příkaz Zobrazit data tabulky:

![](create-a-database/_static/image16.png)

Přidáme několik řádků dat večeři, které můžeme použít později, když začneme implementovat aplikaci:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Další krok

Dokončili jsme vytvoření naší databáze. Nyní vytvoříme třídy modelů, které můžeme použít k dotazování a aktualizaci.

> [!div class="step-by-step"]
> [Předchozí](create-a-new-aspnet-mvc-project.md)
> [další](build-a-model-with-business-rule-validations.md)
