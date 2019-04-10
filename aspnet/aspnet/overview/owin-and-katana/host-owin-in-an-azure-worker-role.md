---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Hostování OWIN v roli pracovního procesu Azure | Dokumentace Microsoftu
author: MikeWasson
description: Tento kurz ukazuje, jak k samoobslužnému hostování OWIN v roli pracovního procesu Microsoft Azure. Open Web Interface pro .NET (OWIN) definuje abstrakce mezi .NET webový server...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 129b6a8f411d482de75e7e5edc5cc919b4d2de52
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419519"
---
# <a name="host-owin-in-an-azure-worker-role"></a>Hostování specifikace OWIN v rolích pracovního procesu v Azure

podle [Mike Wasson](https://github.com/MikeWasson)

> Tento kurz ukazuje, jak k samoobslužnému hostování OWIN v roli pracovního procesu Microsoft Azure.
>
> [Otevřete Web Interface pro .NET](http://owin.org/) (OWIN) definuje abstrakce mezi .NET webové servery a webové aplikace. Webové aplikace ze serveru, který je ideální pro webové aplikace ve vašem vlastním procesu mimo službu IIS s vlastním hostováním OWIN OWIN odděluje obě části – například v roli pracovního procesu systému Azure.
>
> V tomto kurzu se dozvíte, jak hostování na vlastním serveru aplikací OWIN v roli pracovního procesu Microsoft Azure. Další informace o rolích pracovního procesu najdete v tématu [spouštění modelů Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>V tomto kurzu použili verze softwaru
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [Sada Azure SDK for .NET 2.3](https://azure.microsoft.com/downloads/)
> - [Microsoft.Owin.Selfhost 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)


## <a name="create-a-microsoft-azure-project"></a>Vytvořte projekt Microsoft Azure

Spusťte Visual Studio s oprávněními správce. Oprávnění správce jsou potřebné k ladění aplikace v místním prostředí, pomocí emulátoru služby výpočty v Azure.

Na **souboru** nabídky, klikněte na tlačítko **nový**, pak klikněte na tlačítko **projektu**. Z **nainstalované šablony**, v části Visual C#, klikněte na tlačítko **cloudu** a potom klikněte na tlačítko **Windows Azure Cloud Service**. Pojmenujte projekt "AzureApp" a klikněte na tlačítko **OK**.

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

V **nová Cloudová služba Windows Azure** dialogového okna, dvakrát klikněte na panel **Role pracovního procesu**. Ponechte výchozí název ("WorkerRole1"). Tento krok přidává role pracovního procesu k řešení. Klikněte na **OK**.

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

Řešení sady Visual Studio, který je vytvořen obsahuje dva projekty:

- &quot;AzureApp&quot; definuje role a konfigurace pro aplikace Azure.
- &quot;WorkerRole1&quot; obsahuje kód pro roli pracovního procesu.

Obecně platí aplikace Azure může obsahovat více rolí, i když tento kurz používá jednu roli.

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>Přidání balíčků samoobslužné hostování OWIN

Z **nástroje** nabídky, klepněte na **Správce balíčků NuGet**, klepněte na **konzoly Správce balíčků**.

V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>Přidat koncový bod HTTP

V Průzkumníku řešení rozbalte projekt AzureApp. Rozbalte uzel role, klikněte pravým tlačítkem na WorkerRole1 a vyberte **vlastnosti**.

![](host-owin-in-an-azure-worker-role/_static/image6.png)

Klikněte na tlačítko **koncové body**a potom klikněte na tlačítko **přidat koncový bod**.

V **protokol** rozevíracího seznamu vyberte možnost "http". V **veřejný Port** a **privátní Port**, zadejte 80. Tato čísla portů se mohou lišit. Veřejný port je, co klienti používat při odesílání požadavku do role.

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>Vytvoření třídy pro spuštění OWIN

V Průzkumníku řešení klikněte pravým tlačítkem myši klikněte na WorkerRole1 projekt a vyberte **přidat** / **třídy** přidání nové třídy. Název třídy `Startup`.

Nahraďte všechny často používaný kód následujícím kódem:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage` – Metoda rozšíření přidá jednoduché stránky HTML pro vaši aplikaci, ověřte funkčnost lokality.

## <a name="start-the-owin-host"></a>Spuštění hostitele OWIN

Otevřete soubor WorkerRole.cs. Tato třída definuje kód, který se spustí při spuštění a zastavení role pracovního procesu.

Přidejte následující příkaz using:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

Přidat **IDisposable** člena `WorkerRole` třídy:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

V `OnStart` metodu, přidejte následující kód pro spuštění hostitele:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp.Start** metoda spustí hostitele OWIN. Název `Startup` třídy je parametr typu metody. Podle konvence, bude volat hostitele `Configure` metody této třídy.

Přepsat `OnStop` a neprovede  *\_aplikace* instance:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

Tady je kompletní kód WorkerRole.cs:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

Sestavte řešení a stisknutím klávesy F5 spusťte aplikaci místně v emulátoru Azure Compute. V závislosti na nastavení brány firewall potřebujete povolit emulátor přes bránu firewall.

Emulátor služby výpočty místní IP adresa přiřadí ke koncovému bodu. IP adresu můžete najít zobrazením Uživatelském prostředí emulátoru výpočtů. Klikněte pravým tlačítkem na hlavním panelu oznamovací oblasti ikonu emulátoru a vyberte **zobrazit Uživatelském prostředí emulátoru výpočtů**.

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

Zjistit IP adresu v rámci nasazení služeb, nasazení [id], podrobnosti o službě. Otevřete webový prohlížeč a přejděte do protokolu http:\/\/*adresu*, kde *adresu* je IP adresa přidělí emulátor služby výpočty; například `http://127.0.0.1:80`. Zobrazí se úvodní stránka OWIN:

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>Nasazení do Azure

Pro tento krok musí mít účet Azure. Pokud již nemáte, můžete během několika minut vytvořit Bezplatný zkušební účet. Podrobnosti najdete v tématu [bezplatná zkušební verze Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

V Průzkumníku řešení klikněte pravým tlačítkem na projekt AzureApp. Vyberte **Publikovat**.

![](host-owin-in-an-azure-worker-role/_static/image12.png)

Pokud nejste přihlášení k účtu Azure, klikněte na tlačítko **Sign In**.

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

Když jste přihlášeni, zvolte předplatné a klikněte na **Další**.

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

Zadejte název pro cloudovou službu a zvolte oblast. Klikněte na možnost **Vytvořit**.

![](host-owin-in-an-azure-worker-role/_static/image17.png)

Klikněte na tlačítko **publikovat**.

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

Okno Protokol aktivit Azure zobrazuje průběh nasazení. Když je aplikace nasazena, přejdete k `http://appname.cloudapp.net/`, kde *appname* je název vaší cloudové služby.

## <a name="additional-resources"></a>Další prostředky

- [Přehled projektu Katana](an-overview-of-project-katana.md)
- [Katana projektu na Githubu](https://github.com/aspnet/AspNetKatana/)
