---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: Vytváření v kapitole soubory ke stažení pro EF 5 MVC 4 kurzy | Dokumentace Microsoftu
author: Rick-Anderson
description: Contoso University ukázkovou webovou aplikaci ukazuje postup vytvoření aplikace ASP.NET MVC 4 pomocí Entity Framework 5 Code First a sady Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 6b5d10ba9e878908953e999bd1fd44970acf4ca5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078337"
---
<a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>Vytváření v kapitole soubory ke stažení pro EF 5 MVC 4 kurzy
====================
Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))

[Stáhnout dokončený projekt](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University ukázkovou webovou aplikaci ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Entity Framework 5 Code First a Visual Studio 2012. Informace o této sérii kurzů, naleznete v tématu [z prvního kurzu této série](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).


## <a name="building-the-chapter-downloads"></a>Stažení jednotlivých kapitol

1. Stáhněte a rozbalte soubor zip ukázkový projekt. V balíčku rozzipovaný ke stažení najdete zip další soubory, jeden pro dokončení každá kapitola.
2. Klikněte pravým tlačítkem na požadovaný komprimovaného souboru, klikněte na tlačítko **vlastnosti**a klikněte na tlačítko **Odblokovat** tlačítko.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. Rozbalte tento soubor.
4. Dvakrát klikněte *CUx.sln* souboru ke spuštění sady Visual Studio.
5. Z **nástroje** nabídky, klepněte na **Správce balíčků NuGet**, pak **konzoly Správce balíčků**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. V balíčku správce konzoly (konzolu PMC), klikněte na tlačítko **obnovení**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Ukončení sady Visual Studio.
8. Restartujte sadu Visual Studio, otevřete soubor řešení uzavřeny v předchozím kroku.
9. V balíčku správce konzoly (konzolu PMC), zadejte `Update-Database` příkaz:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > Pokud se zobrazí následující chyba:  
    >   
    >  *Termín 'Aktualizace databáze' nebyl rozpoznán jako název rutiny, funkce, soubor skriptu nebo spustitelného programu. Zkontrolujte, zda název, nebo pokud cesty byl zahrnut, ověřte správnost cesty a zkuste to znovu.*  
    > Ukončete a restartujte aplikaci Visual Studio.

    Bude spouštět každou migraci a potom spustí metodu počáteční hodnoty. Nyní můžete spustit aplikaci.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [Předchozí](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
