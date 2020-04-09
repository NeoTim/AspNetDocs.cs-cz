---
uid: mvc/overview/deployment/docker-aspnetmvc
title: Migrace aplikací ASP.NET MVC do kontejnerů s Windows
description: Zjistěte, jak vzít existující ASP.NET aplikaci MVC a spustit ji v kontejneru Windows Dockeru
keywords: Kontejnery systému Windows,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675186"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Migrace aplikací ASP.NET MVC do kontejnerů s Windows

Spuštění existující aplikace založené na rozhraní .NET Framework v kontejneru windows nevyžaduje žádné změny vaší aplikace. Chcete-li aplikaci spustit v kontejneru windows, vytvořte bitovou kopii Dockeru obsahující vaši aplikaci a spusťte kontejner. Toto téma vysvětluje, jak vzít existující [ASP.NET aplikace MVC](http://www.asp.net/mvc) a nasadit ji v kontejneru systému Windows.

Začnete s existující aplikací ASP.NET MVC a pak publikujete publikované datové zdroje pomocí sady Visual Studio. Docker uděláte k vytvoření bitové kopie, která obsahuje a spouští vaši aplikaci. Přejdete na web spuštěný v kontejneru windows a ověříte, že aplikace funguje.

Tento článek předpokládá základní znalost Dockeru. Informace o Dockeru najdete v článku [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Přehled Dockeru).

Aplikace, kterou spustíte v kontejneru, je jednoduchý web, který odpovídá na otázky náhodně. Tato aplikace je základní MVC aplikace bez ověřování nebo databázové úložiště; umožňuje zaměřit se na přesunutí webové vrstvy do kontejneru. Budoucí témata ukáží, jak přesunout a spravovat trvalé úložiště v kontejnerizovaných aplikacích.

Přesunutí aplikace zahrnuje následující kroky:

1. [Vytvoření úlohy publikování k vytvoření datových zdrojů pro bitovou kopii.](#publish-script)
1. [Vytváření image Dockeru, který bude spuštěn a aplikace.](#build-the-image)
1. [Spuštění kontejneru Dockeru, který spouští vaši image.](#start-a-container)
1. [Ověření aplikace pomocí prohlížeče.](#verify-in-the-browser)

[Dokončená aplikace](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) je na GitHubu.

## <a name="prerequisites"></a>Požadavky

Vývojový stroj musí mít následující software:

- [Aktualizace Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (nebo vyšší) nebo [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (nebo vyšší)
- [Docker pro Windows](https://docs.docker.com/docker-for-windows/) - verze Stable 1.13.0 nebo 1.12 Beta 26 (nebo novější verze)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Pokud používáte Windows Server 2016, postupujte podle pokynů pro [nasazení hostitele kontejnerů – Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).

Po nainstalování a spuštění Dockeru klikněte pravým tlačítkem myši na ikonu na hlavním panelu a vyberte **Switch to Windows containers** (Přepnout na kontejnery Windows). To se vyžaduje pro spuštění imagí Dockeru založených na Windows. Spuštění tohoto příkazu trvá několik sekund:

![Kontejner systému Windows][windows-container]

## <a name="publish-script"></a>Publikovat skript

Shromážděte na jednom místě všechny prostředky, které potřebujete nahrát do image Dockeru. Pomocí příkazu **Publikování** v sadě Visual Studio můžete vytvořit profil publikování pro vaši aplikaci. Tento profil vloží všechny datové zdroje do jednoho adresářového stromu, který zkopírujete do cílovébitové bitové kopie později v tomto kurzu.

**Kroky publikování**

1. Klikněte pravým tlačítkem myši na webový projekt v sadě Visual Studio a vyberte **publikovat**.
1. Klepněte na **tlačítko Vlastní profil**a potom jako metodu vyberte Systém **souborů.**
1. Zvolte adresář. Podle konvence používá `bin\Release\PublishOutput`stažená ukázka .

![Publikovat připojení][publish-connection]

Otevřete část **Precompile during publishing** **Možnosti publikování souboru** na kartě **Nastavení.** Tato optimalizace znamená, že budete kompilaci zobrazení v kontejneru Dockeru, kopírujete předkompilovaná zobrazení.

![Nastavení publikování][publish-settings]

Klepněte na tlačítko **Publikovat**a Visual Studio zkopíruje všechny potřebné datové zdroje do cílové složky.

## <a name="build-the-image"></a>Sestavení image

Vytvořte nový soubor s názvem *Dockerfile* k definování image Dockeru. *Dockerfile* obsahuje pokyny k vytvoření konečné image a obsahuje všechny základní image názvy, požadované součásti, aplikace, kterou chcete spustit, a další image konfigurace. *Dockerfile* je vstup `docker build` do příkazu, který vytvoří image.

Pro toto cvičení vytvoříte bitovou `microsoft/aspnet` kopii na základě image umístěné v [Docker Hubu](https://hub.docker.com/r/microsoft/aspnet/).
Základní bitová `microsoft/aspnet`kopie , bitová kopie systému Windows Server. Obsahuje windows server core, službu IIS a ASP.NET 4.7.2. Když spustíte tuto bitovou kopii v kontejneru, automaticky spustí iis a nainstalované weby.

Dockerfile, který vytvoří obrázek vypadá takto:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

V tomto souboru Dockerfile není žádný příkaz `ENTRYPOINT`. Žádný nepotřebujete. Při spuštění systému Windows Server se službou IIS je proces služby IIS vstupním bodem, který je nakonfigurován tak, aby se spouštěl v základní bitové kopii aspnet.

Spusťte příkaz sestavení Dockeru a vytvořte bitovou kopii, která spustí vaši ASP.NET aplikaci. Chcete-li to provést, otevřete okno Prostředí PowerShell v adresáři projektu a do adresáře řešení zadejte následující příkaz:

```console
docker build -t mvcrandomanswers .
```

Tento příkaz vytvoří novou bitovou kopii pomocí pokynů v souboru Dockerfile a pojmenuje (-t tagging) bitovou kopii jako mvcrandomanswers. To může zahrnovat vytažení základní image z [Docker Hubu](http://hub.docker.com)a přidání aplikace do této image.

Po dokončení tohoto příkazu můžete `docker images` příkaz spustit a zobrazit informace o novém obrázku:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

ID obrázku se bude v počítači lišit. Teď spusťme aplikaci.

## <a name="start-a-container"></a>Spuštění kontejneru

Spusťte kontejner provedením `docker run` následujícího příkazu:

```console
docker run -d --name randomanswers mvcrandomanswers
```

Argument `-d` říká Docker spustit image v odpojeném režimu. To znamená, že image Dockeru běží odpojenod aktuálního prostředí.

V mnoha příkladech dockeru se může zobrazit -p pro mapování kontejneru a hostitelských portů. Výchozí bitová kopie aspnet již nakonfigurovala kontejner tak, aby naslouchal na portu 80 a zpřístupnioval jej.

Poskytuje `--name randomanswers` název spuštěného kontejneru. Tento název můžete použít místo ID kontejneru ve většině příkazů.

Je `mvcrandomanswers` název obrázku, který má být zahájen.

## <a name="verify-in-the-browser"></a>Ověřit v prohlížeči

Po spuštění kontejneru se připojte `http://localhost` k běžícímu kontejneru pomocí uvedeného příkladu. Zadejte tuto adresu URL do prohlížeče a měli byste vidět spuštěný web.

> [!NOTE]
> Některé VPN nebo proxy software vám může zabránit v navigaci na vaše stránky.
> Můžete jej dočasně zakázat, abyste se ujistili, že kontejner funguje.

Ukázkový adresář na GitHubu obsahuje [skript PowerShellu,](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) který tyto příkazy provede za vás. Otevřete okno PowerShellu, změňte adresář do adresáře řešení a zadejte:

```console
./run.ps1
```

Výše uvedený příkaz vytvoří bitovou kopii, zobrazí seznam obrázků v počítači a spustí kontejner.

Chcete-li kontejner zastavit, vydejte `docker stop` příkaz:

```console
docker stop randomanswers
```

Chcete-li kontejner odebrat, vydejte `docker rm` příkaz:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Přepnutí do kontejneru Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Publikovat do systému souborů"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Nastavení publikování"
