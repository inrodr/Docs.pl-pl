---
title: Visual Studio Tools for Docker z platformy ASP.NET Core
author: spboyer
description: "Dowiedz się, jak containerize aplikacji platformy ASP.NET Core za pomocą narzędzi Visual Studio 2017 i Docker dla systemu Windows."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/12/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: caf0e423d8e6f61fd2470d1f4ea2dd93909c3696
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a><span data-ttu-id="bae8a-103">Visual Studio Tools for Docker z platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bae8a-103">Visual Studio Tools for Docker with ASP.NET Core</span></span>

<span data-ttu-id="bae8a-104">[Visual Studio 2017](https://www.visualstudio.com/) obsługuje kompilowania, debugowania i uruchamianie platformy ASP.NET Core aplikacji przeznaczonych dla platformy .NET Framework lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bae8a-104">[Visual Studio 2017](https://www.visualstudio.com/) supports building, debugging, and running ASP.NET Core apps targeting either .NET Framework or .NET Core.</span></span> <span data-ttu-id="bae8a-105">Kontenery w systemach Windows i Linux są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="bae8a-105">Both Windows and Linux containers are supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bae8a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bae8a-106">Prerequisites</span></span>

* <span data-ttu-id="bae8a-107">[Visual Studio 2017](https://www.visualstudio.com/) z **aplikacji dla wielu platform .NET Core** obciążenia</span><span class="sxs-lookup"><span data-stu-id="bae8a-107">[Visual Studio 2017](https://www.visualstudio.com/) with the **.NET Core cross-platform development** workload</span></span>
* [<span data-ttu-id="bae8a-108">Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bae8a-108">Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/install/)

## <a name="installation-and-setup"></a><span data-ttu-id="bae8a-109">Instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="bae8a-109">Installation and setup</span></span>

<span data-ttu-id="bae8a-110">Docker instalacji, przejrzyj informacje w [Docker dla systemu Windows: co należy wiedzieć przed zainstalowaniem](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install) i zainstaluj [Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/install/).</span><span class="sxs-lookup"><span data-stu-id="bae8a-110">For Docker installation, review the information at [Docker for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install) and install [Docker For Windows](https://docs.docker.com/docker-for-windows/install/).</span></span>

<span data-ttu-id="bae8a-111">**[Udostępnione dyski](https://docs.docker.com/docker-for-windows/#shared-drives)**  Docker dla systemu Windows musi być skonfigurowana do obsługi mapowania woluminu i debugowanie.</span><span class="sxs-lookup"><span data-stu-id="bae8a-111">**[Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)** in Docker for Windows must be configured to support volume mapping and debugging.</span></span> <span data-ttu-id="bae8a-112">Kliknij prawym przyciskiem myszy ikonę Docker pasku zadań, zaznacz **ustawień...** i wybierz **udostępnione dyski**.</span><span class="sxs-lookup"><span data-stu-id="bae8a-112">Right-click the System Tray's Docker icon, select **Settings...**, and select **Shared Drives**.</span></span> <span data-ttu-id="bae8a-113">Wybierz dysk, gdzie są przechowywane pliki Docker.</span><span class="sxs-lookup"><span data-stu-id="bae8a-113">Select the drive where Docker stores files.</span></span> <span data-ttu-id="bae8a-114">Wybierz **zastosować**.</span><span class="sxs-lookup"><span data-stu-id="bae8a-114">Select **Apply**.</span></span>

![Dyski udostępnione](./visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> <span data-ttu-id="bae8a-116">Monitowanie w Visual Studio 2017 wersji 15.6 lub nowszej, gdy **udostępnione dyski** nie są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="bae8a-116">Visual Studio 2017 versions 15.6 and later prompt when **Shared Drives** aren't configured.</span></span>

## <a name="add-docker-support-to-an-app"></a><span data-ttu-id="bae8a-117">Dodaj obsługę Docker do aplikacji</span><span class="sxs-lookup"><span data-stu-id="bae8a-117">Add Docker support to an app</span></span>

<span data-ttu-id="bae8a-118">Platforma docelowa projektu platformy ASP.NET Core Określa typy obsługiwanych kontenera.</span><span class="sxs-lookup"><span data-stu-id="bae8a-118">The ASP.NET Core project's target framework determines the supported container types.</span></span> <span data-ttu-id="bae8a-119">Projektach przeznaczonych dla platformy .NET Core obsługuje kontenery zarówno systemu Windows, jak i Linux.</span><span class="sxs-lookup"><span data-stu-id="bae8a-119">Projects targeting .NET Core support both Linux and Windows containers.</span></span> <span data-ttu-id="bae8a-120">Projektów przeznaczanie tylko platformy .NET obsługuje kontenery systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="bae8a-120">Projects targeting .NET Framework only support Windows containers.</span></span>

<span data-ttu-id="bae8a-121">Podczas dodawania obsługi Docker do projektu, wybierz systemu Windows lub Linux kontenera.</span><span class="sxs-lookup"><span data-stu-id="bae8a-121">When adding Docker support to a project, choose either a Windows or a Linux container.</span></span> <span data-ttu-id="bae8a-122">Na hoście Docker musi być uruchomiony ten sam typ kontenera.</span><span class="sxs-lookup"><span data-stu-id="bae8a-122">The Docker host must be running the same container type.</span></span> <span data-ttu-id="bae8a-123">Aby zmienić typ kontenera w uruchomione wystąpienie Docker, kliknij prawym przyciskiem myszy ikonę Docker pasku zadań i wybierz polecenie **przełączyć się do kontenerów Windows...**  lub **przełączyć się do kontenerów Linux...** .</span><span class="sxs-lookup"><span data-stu-id="bae8a-123">To change the container type in the running Docker instance, right-click the System Tray's Docker icon and choose **Switch to Windows containers...** or **Switch to Linux containers...**.</span></span>

### <a name="new-app"></a><span data-ttu-id="bae8a-124">Nowa aplikacja</span><span class="sxs-lookup"><span data-stu-id="bae8a-124">New app</span></span>

<span data-ttu-id="bae8a-125">Podczas tworzenia nowej aplikacji z **aplikacji sieci Web platformy ASP.NET Core** szablony projektów, wybierz opcję **Włącz obsługę Docker** wyboru:</span><span class="sxs-lookup"><span data-stu-id="bae8a-125">When creating a new app with the **ASP.NET Core Web Application** project templates, select the **Enable Docker Support** checkbox:</span></span>

![Włącz obsługę Docker wyboru](visual-studio-tools-for-docker/_static/enable-docker-support-checkbox.png)

<span data-ttu-id="bae8a-127">W przypadku platformy docelowej .NET Core **OS** listy rozwijanej umożliwia wybór typu kontenera.</span><span class="sxs-lookup"><span data-stu-id="bae8a-127">If the target framework is .NET Core, the **OS** drop-down allows for the selection of a container type.</span></span>

### <a name="existing-app"></a><span data-ttu-id="bae8a-128">Istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bae8a-128">Existing app</span></span>

<span data-ttu-id="bae8a-129">Visual Studio Tools for Docker nie obsługuje dodawania Docker do istniejącego projektu platformy ASP.NET Core przeznaczonych dla platformy .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="bae8a-129">The Visual Studio Tools for Docker don't support adding Docker to an existing ASP.NET Core project targeting .NET Framework.</span></span> <span data-ttu-id="bae8a-130">Dla platformy ASP.NET Core projektów przeznaczonych dla platformy .NET Core istnieją dwie opcje do dodawania obsługi Docker za pomocą narzędzi.</span><span class="sxs-lookup"><span data-stu-id="bae8a-130">For ASP.NET Core projects targeting .NET Core, there are two options for adding Docker support via the tooling.</span></span> <span data-ttu-id="bae8a-131">Otwórz projekt w programie Visual Studio i wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="bae8a-131">Open the project in Visual Studio, and choose one of the following options:</span></span>

* <span data-ttu-id="bae8a-132">Wybierz **Obsługa Docker** z **projektu** menu.</span><span class="sxs-lookup"><span data-stu-id="bae8a-132">Select **Docker Support** from the **Project** menu.</span></span>
* <span data-ttu-id="bae8a-133">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Dodaj** > **Obsługa Docker**.</span><span class="sxs-lookup"><span data-stu-id="bae8a-133">Right-click the project in Solution Explorer and select **Add** > **Docker Support**.</span></span>

## <a name="docker-assets-overview"></a><span data-ttu-id="bae8a-134">Omówienie zasoby docker</span><span class="sxs-lookup"><span data-stu-id="bae8a-134">Docker assets overview</span></span>

<span data-ttu-id="bae8a-135">Dodaj Visual Studio Tools for Docker *docker-tworzą* projektu do rozwiązania, które zawierają:</span><span class="sxs-lookup"><span data-stu-id="bae8a-135">The Visual Studio Tools for Docker add a *docker-compose* project to the solution, containing the following:</span></span>

* <span data-ttu-id="bae8a-136">*.dockerignore*: zawiera listę wzorców plików i katalogów, które mają zostać wykluczone podczas generowania kontekst kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-136">*.dockerignore*: Contains a list of file and directory patterns to exclude when generating a build context.</span></span>
* <span data-ttu-id="bae8a-137">*docker-compose.yml*: base [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/) plik używany do definiowania kolekcją obrazów, wbudowane i uruchom z `docker-compose build` i `docker-compose run`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="bae8a-137">*docker-compose.yml*: The base [Docker Compose](https://docs.docker.com/compose/overview/) file used to define the collection of images to be built and run with `docker-compose build` and `docker-compose run`, respectively.</span></span>
* <span data-ttu-id="bae8a-138">*docker compose.override.yml*: opcjonalny plik odczytywane przez rozwiązania Docker Compose, zawierający konfigurację zastąpień dla usług.</span><span class="sxs-lookup"><span data-stu-id="bae8a-138">*docker-compose.override.yml*: An optional file, read by Docker Compose, containing configuration overrides for services.</span></span> <span data-ttu-id="bae8a-139">Wykonuje program Visual Studio `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` scalenie tych plików.</span><span class="sxs-lookup"><span data-stu-id="bae8a-139">Visual Studio executes `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` to merge these files.</span></span>

<span data-ttu-id="bae8a-140">A *plik Dockerfile*, przepisu tworzenia finalnego obrazu Docker, jest dodawany do katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="bae8a-140">A *Dockerfile*, the recipe for creating a final Docker image, is added to the project root.</span></span> <span data-ttu-id="bae8a-141">Zapoznaj się [odwołania plik Dockerfile](https://docs.docker.com/engine/reference/builder/) dla zrozumienia poleceń w niej.</span><span class="sxs-lookup"><span data-stu-id="bae8a-141">Refer to [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for an understanding of the commands within it.</span></span> <span data-ttu-id="bae8a-142">Tego określonego *plik Dockerfile* używa [kompilacji wieloetapowym](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) zawierający cztery różne, o nazwie etapy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="bae8a-142">This particular *Dockerfile* uses a [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) containing four distinct, named build stages:</span></span>

[!code-text[](visual-studio-tools-for-docker/samples/HelloDockerTools/HelloDockerTools/Dockerfile?highlight=1,5,14,17)]

<span data-ttu-id="bae8a-143">*Plik Dockerfile* opiera się na [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) obrazu.</span><span class="sxs-lookup"><span data-stu-id="bae8a-143">The *Dockerfile* is based on the [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) image.</span></span> <span data-ttu-id="bae8a-144">Ten obraz podstawowy obejmuje pakiety platformy ASP.NET Core NuGet, które zostały wstępnie przy użyciu kompilatora JIT do zwiększenia wydajności uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="bae8a-144">This base image includes the ASP.NET Core NuGet packages, which have been pre-jitted to improve startup performance.</span></span>

<span data-ttu-id="bae8a-145">*Docker-compose.yml* plik zawiera nazwę obrazu, który jest tworzona po uruchomieniu projektu:</span><span class="sxs-lookup"><span data-stu-id="bae8a-145">The *docker-compose.yml* file contains the name of the image that's created when the project runs:</span></span>

[!code-yaml[](visual-studio-tools-for-docker/samples/HelloDockerTools/docker-compose.yml?highlight=5)]

<span data-ttu-id="bae8a-146">W powyższym przykładzie `image: hellodockertools` generuje obraz `hellodockertools:dev` po uruchomieniu aplikacji **debugowania** tryb.</span><span class="sxs-lookup"><span data-stu-id="bae8a-146">In the preceding example, `image: hellodockertools` generates the image `hellodockertools:dev` when the app runs in **Debug** mode.</span></span> <span data-ttu-id="bae8a-147">`hellodockertools:latest` Obraz jest generowany, gdy aplikacja jest uruchamiana **wersji** tryb.</span><span class="sxs-lookup"><span data-stu-id="bae8a-147">The `hellodockertools:latest` image is generated when the app runs in **Release** mode.</span></span>

<span data-ttu-id="bae8a-148">Nazwa obrazu z prefiksu [Centrum Docker](https://hub.docker.com/) nazwy użytkownika (na przykład `dockerhubusername/hellodockertools`) Jeśli obrazu zostanie przekazany do rejestru.</span><span class="sxs-lookup"><span data-stu-id="bae8a-148">Prefix the image name with the [Docker Hub](https://hub.docker.com/) username (for example, `dockerhubusername/hellodockertools`) if the image will be pushed to the registry.</span></span> <span data-ttu-id="bae8a-149">Możesz też zmienić nazwę obrazu uwzględnienie rejestru prywatny adres URL (na przykład `privateregistry.domain.com/hellodockertools`) w zależności od konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-149">Alternatively, change the image name to include the private registry URL (for example, `privateregistry.domain.com/hellodockertools`) depending on the configuration.</span></span>

## <a name="debug"></a><span data-ttu-id="bae8a-150">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="bae8a-150">Debug</span></span>

<span data-ttu-id="bae8a-151">Wybierz **Docker** z listy rozwijanej w pasku narzędzi i rozpoczęcia debugowania aplikacji debugowania.</span><span class="sxs-lookup"><span data-stu-id="bae8a-151">Select **Docker** from the debug drop-down in the toolbar, and start debugging the app.</span></span> <span data-ttu-id="bae8a-152">**Docker** widoku **dane wyjściowe** oknie wyświetlane są następujące akcje zachodzące:</span><span class="sxs-lookup"><span data-stu-id="bae8a-152">The **Docker** view of the **Output** window shows the following actions taking place:</span></span>

* <span data-ttu-id="bae8a-153">*Microsoft/aspnetcore* obraz środowiska uruchomieniowego są uzyskiwane (Jeśli nie jest jeszcze w pamięci podręcznej).</span><span class="sxs-lookup"><span data-stu-id="bae8a-153">The *microsoft/aspnetcore* runtime image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="bae8a-154">*Aspnetcore-microsoft Zbuduj* kompilacji/publikowania obrazu są uzyskiwane (Jeśli nie jest jeszcze w pamięci podręcznej).</span><span class="sxs-lookup"><span data-stu-id="bae8a-154">The *microsoft/aspnetcore-build* compile/publish image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="bae8a-155">*ASPNETCORE_ENVIRONMENT* ustawiono zmiennej środowiskowej `Development` w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="bae8a-155">The *ASPNETCORE_ENVIRONMENT* environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="bae8a-156">Port 80 jest widoczne i zamapowane do portu przypisywane dynamicznie hosta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="bae8a-156">Port 80 is exposed and mapped to a dynamically-assigned port for localhost.</span></span> <span data-ttu-id="bae8a-157">Port jest określana przez hosta Docker i mogą być przeszukiwane przy `docker ps` polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae8a-157">The port is determined by the Docker host and can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="bae8a-158">Aplikacja jest kopiowany do kontenera.</span><span class="sxs-lookup"><span data-stu-id="bae8a-158">The app is copied to the container.</span></span>
* <span data-ttu-id="bae8a-159">Domyślna przeglądarka jest uruchamiana w debugerze kontenera przy użyciu portu przypisywane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="bae8a-159">The default browser is launched with the debugger attached to the container using the dynamically-assigned port.</span></span> 

<span data-ttu-id="bae8a-160">Wynikowy obraz Docker jest *deweloperów* obrazu w aplikacji przy użyciu *microsoft/aspnetcore* obrazów jako obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="bae8a-160">The resulting Docker image is the *dev* image of the app with the *microsoft/aspnetcore* images as the base image.</span></span> <span data-ttu-id="bae8a-161">Uruchom `docker images` w **Konsola Menedżera pakietów** okna (PMC).</span><span class="sxs-lookup"><span data-stu-id="bae8a-161">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="bae8a-162">Wyświetlane są obrazy na komputerze:</span><span class="sxs-lookup"><span data-stu-id="bae8a-162">The images on the machine are displayed:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                f8f9d6c923e2        About an hour ago   391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        15 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="bae8a-163">Zawartość aplikacji nie ma obrazu deweloperów jako **debugowania** konfiguracje Użyj zamontowania woluminu, aby zapewnić środowisko iteracji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-163">The dev image lacks the app contents, as **Debug** configurations use volume mounting to provide the iterative experience.</span></span> <span data-ttu-id="bae8a-164">Aby wypchnąć obrazu, należy użyć **wersji** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-164">To push an image, use the **Release** configuration.</span></span>

<span data-ttu-id="bae8a-165">Uruchom `docker ps` w kryterium.</span><span class="sxs-lookup"><span data-stu-id="bae8a-165">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="bae8a-166">Należy zauważyć, że aplikacja zostanie uruchomiona przy użyciu kontenera:</span><span class="sxs-lookup"><span data-stu-id="bae8a-166">Notice the app is running using the container:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a><span data-ttu-id="bae8a-167">Edytuj i Kontynuuj</span><span class="sxs-lookup"><span data-stu-id="bae8a-167">Edit and continue</span></span>

<span data-ttu-id="bae8a-168">Zmiany pliki statyczne i widokami Razor są automatycznie aktualizowane bez konieczności kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-168">Changes to static files and Razor views are automatically updated without the need for a compilation step.</span></span> <span data-ttu-id="bae8a-169">Wprowadzić zmiany, Zapisz i Odśwież przeglądarkę, aby wyświetlić tę aktualizację.</span><span class="sxs-lookup"><span data-stu-id="bae8a-169">Make the change, save, and refresh the browser to view the update.</span></span>  

<span data-ttu-id="bae8a-170">Modyfikacje plików kodu wymaga, kompilowania i ponownego uruchomienia Kestrel w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="bae8a-170">Modifications to code files requires compiling and a restart of Kestrel within the container.</span></span> <span data-ttu-id="bae8a-171">Po wprowadzeniu zmian, użyj CTRL + F5, aby wykonać proces i uruchomić aplikację w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="bae8a-171">After making the change, use CTRL + F5 to perform the process and start the app within the container.</span></span> <span data-ttu-id="bae8a-172">Kontener Docker nie jest ponownie skompilowany lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="bae8a-172">The Docker container isn't rebuilt or stopped.</span></span> <span data-ttu-id="bae8a-173">Uruchom `docker ps` w kryterium.</span><span class="sxs-lookup"><span data-stu-id="bae8a-173">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="bae8a-174">Począwszy od 10 minut temu nadal działa powiadomienia oryginalnego kontenera:</span><span class="sxs-lookup"><span data-stu-id="bae8a-174">Notice the original container is still running as of 10 minutes ago:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a><span data-ttu-id="bae8a-175">Publikowanie obrazy usługi Docker</span><span class="sxs-lookup"><span data-stu-id="bae8a-175">Publish Docker images</span></span>

<span data-ttu-id="bae8a-176">Po zakończeniu cyklu opracowanie i debugowania aplikacji Visual Studio Tools for Docker pomagają w tworzenie obrazu produkcyjnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-176">Once the develop and debug cycle of the app is completed, the Visual Studio Tools for Docker assist in creating the production image of the app.</span></span> <span data-ttu-id="bae8a-177">Zmień konfigurację listy rozwijanej **wersji** i kompilowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-177">Change the configuration drop-down to **Release** and build the app.</span></span> <span data-ttu-id="bae8a-178">Narzędzia tworzy obraz z *najnowsze* tagu, który może zostać przeniesiony do rejestru prywatnych lub Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="bae8a-178">The tooling produces the image with the *latest* tag, which can be pushed to the private registry or Docker Hub.</span></span> 

<span data-ttu-id="bae8a-179">Uruchom `docker images` w kryterium, aby wyświetlić listę obrazów:</span><span class="sxs-lookup"><span data-stu-id="bae8a-179">Run the `docker images` command in PMC to see the list of images:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                4cb1fca533f0        19 seconds ago      391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        16 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="bae8a-180">`docker images` Polecenie zwraca pośredniczące obrazów za pomocą nazwy repozytorium i tagi zidentyfikowane jako  *\<Brak >* (nie są wymienione powyżej).</span><span class="sxs-lookup"><span data-stu-id="bae8a-180">The `docker images` command returns intermediary images with repository names and tags identified as *\<none>* (not listed above).</span></span> <span data-ttu-id="bae8a-181">Te bez nazwy obrazów są produkowane przez [kompilacji wieloetapowym](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *plik Dockerfile*.</span><span class="sxs-lookup"><span data-stu-id="bae8a-181">These unnamed images are produced by the [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*.</span></span> <span data-ttu-id="bae8a-182">Poprawiają wydajność tworzenia obrazu końcowego&mdash;tylko niezbędne warstwy są również przebudowany w przypadku wystąpienia zmian.</span><span class="sxs-lookup"><span data-stu-id="bae8a-182">They improve the efficiency of building the final image&mdash;only the necessary layers are rebuilt when changes occur.</span></span> <span data-ttu-id="bae8a-183">Gdy pośredniczące obrazy nie są już potrzebne, usuń je przy użyciu [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae8a-183">When the intermediary images are no longer needed, delete them using the [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) command.</span></span>

<span data-ttu-id="bae8a-184">Może być oczekiwanie środowisko produkcyjne lub wersji obrazu na mniejszy rozmiar w porównaniu do *deweloperów* obrazu.</span><span class="sxs-lookup"><span data-stu-id="bae8a-184">There may be an expectation for the production or release image to be smaller in size by comparison to the *dev* image.</span></span> <span data-ttu-id="bae8a-185">Z powodu mapowania woluminu debugera i aplikacji były uruchomione na komputerze lokalnym, a nie w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="bae8a-185">Because of the volume mapping, the debugger and app were running from the local machine and not within the container.</span></span> <span data-ttu-id="bae8a-186">*Najnowsze* obraz ma spakowane kodu aplikacji niezbędne do uruchomienia aplikacji na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="bae8a-186">The *latest* image has packaged the necessary app code to run the app on a host machine.</span></span> <span data-ttu-id="bae8a-187">W związku z tym delta jest rozmiar kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bae8a-187">Therefore, the delta is the size of the app code.</span></span>