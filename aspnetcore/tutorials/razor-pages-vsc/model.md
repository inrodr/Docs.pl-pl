---
title: "Dodawanie modelu do aplikacji stron Razor przy użyciu programu Visual Studio dla komputerów Mac"
author: rick-anderson
description: "Dodawanie modelu do aplikacji stron Razor w ASP.NET Core za pomocą programu Visual Studio dla komputerów Mac"
keywords: Platformy ASP.NET Core, stron Razor, Razor, MVC, model
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: f2f09909f4c307ce3e1a0c8571b82a709e1f88f9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
# <a name="adding-a-model-to-a-razor-pages-app-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="6482f-104">Dodawanie modelu do aplikacji stron Razor w ASP.NET Core za pomocą programu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="6482f-104">Adding a model to a Razor Pages app in ASP.NET Core with Visual Studio for Mac</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="6482f-105">Dodawanie modelu danych</span><span class="sxs-lookup"><span data-stu-id="6482f-105">Add a data model</span></span>

* <span data-ttu-id="6482f-106">Dodaj folder o nazwie *modele*.</span><span class="sxs-lookup"><span data-stu-id="6482f-106">Add a folder named *Models*.</span></span>
* <span data-ttu-id="6482f-107">Dodaj klasę do *modele* folder o nazwie *Movie.cs*.</span><span class="sxs-lookup"><span data-stu-id="6482f-107">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="6482f-108">Dodaj następujący kod do *Models/Movie.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="6482f-108">Add the following code to the *Models/Movie.cs* file:</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]
[!INCLUDE[model 2a](../../includes/RP/model2a.md)]

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="6482f-109">Skompiluj projekt, aby sprawdzić, czy nie zawiera błędów.</span><span class="sxs-lookup"><span data-stu-id="6482f-109">Build the project to verify you don't have any errors.</span></span>

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="6482f-110">Entity Framework Core NuGet pakietów dla migracji</span><span class="sxs-lookup"><span data-stu-id="6482f-110">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="6482f-111">Narzędzia EF dla interfejsu wiersza polecenia (CLI) są dostępne w [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span><span class="sxs-lookup"><span data-stu-id="6482f-111">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="6482f-112">Aby zainstalować ten pakiet, należy dodać go do `DotNetCliToolReference` kolekcji w *.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="6482f-112">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="6482f-113">**Uwaga:** należy zainstalować ten pakiet, edytując *.csproj* pliku; nie można użyć `install-package` polecenia lub graficznego interfejsu użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="6482f-113">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="6482f-114">Edytuj *RazorPagesMovie.csproj* pliku:</span><span class="sxs-lookup"><span data-stu-id="6482f-114">Edit the *RazorPagesMovie.csproj* file:</span></span>

* <span data-ttu-id="6482f-115">Wybierz **pliku** > **Otwórz plik**, a następnie wybierz *RazorPagesMovie.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="6482f-115">Select **File** > **Open File**, and then select the *RazorPagesMovie.csproj* file.</span></span>
* <span data-ttu-id="6482f-116">Dodaj odwołanie do narzędzia dla `Microsoft.EntityFrameworkCore.Tools.DotNet` drugiej  **\<ItemGroup >**:</span><span class="sxs-lookup"><span data-stu-id="6482f-116">Add tool reference for `Microsoft.EntityFrameworkCore.Tools.DotNet` to the second **\<ItemGroup>**:</span></span>

[!code-xml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?range=12-16&highlight=4)]

[!INCLUDE[model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="6482f-117">Tworzenie szkieletu modelu film</span><span class="sxs-lookup"><span data-stu-id="6482f-117">Scaffold the Movie model</span></span>

* <span data-ttu-id="6482f-118">Otwórz okno polecenia w katalogu projektu (katalog, który zawiera *Program.cs*, *Startup.cs*, i *.csproj* plików).</span><span class="sxs-lookup"><span data-stu-id="6482f-118">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="6482f-119">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6482f-119">Run the following command:</span></span>

<span data-ttu-id="6482f-120">**Uwaga: Uruchom następujące polecenie w systemie Windows. System MacOS i Linux zobacz następne polecenie**</span><span class="sxs-lookup"><span data-stu-id="6482f-120">**Note: Run the following command on Windows. For MacOS and Linux, see the next command**</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="6482f-121">System MacOS i Linux uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6482f-121">On MacOS and Linux, run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="6482f-122">Jeśli zostanie wyświetlony błąd:</span><span class="sxs-lookup"><span data-stu-id="6482f-122">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="6482f-123">Zamknij program Visual Studio i ponownie uruchom polecenie.</span><span class="sxs-lookup"><span data-stu-id="6482f-123">Exit Visual Studio and run the command again.</span></span>

[!INCLUDE[model 4](../../includes/RP/model4.md)]<span data-ttu-id="6482f-124">Następny samouczek wyjaśnia plików utworzonych przez funkcję szkieletów.</span><span class="sxs-lookup"><span data-stu-id="6482f-124"> The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="6482f-125">[Poprzedni: Wprowadzenie](xref:tutorials/razor-pages-vsc/razor-pages-start)
[dalej: szkieletu stron Razor](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="6482f-125">[Previous: Getting Started](xref:tutorials/razor-pages-vsc/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>