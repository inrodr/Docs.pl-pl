---
title: Metapackage Microsoft.AspNetCore.App dla platformy ASP.NET Core 2.1 i nowsze
author: Rick-Anderson
description: Microsoft.AspNetCore.App metapackage obejmuje wszystkie obsługiwane pakiety Entity Framework Core i ASP.NET Core.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/metapackage-app
ms.openlocfilehash: ac402bf8542560267ae179a1f41212380435dbfa
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/17/2018
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a><span data-ttu-id="3cc9f-103">Metapackage Microsoft.AspNetCore.App dla platformy ASP.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="3cc9f-103">Microsoft.AspNetCore.App metapackage for ASP.NET Core 2.1</span></span>

<span data-ttu-id="3cc9f-104">Ta funkcja wymaga platformy ASP.NET Core 2.1 i nowsze, przeznaczonych dla platformy .NET Core 2.1 i nowszymi.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-104">This feature requires ASP.NET Core 2.1 and later targeting .NET Core 2.1 and later.</span></span>

<span data-ttu-id="3cc9f-105">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) metapackage dla platformy ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="3cc9f-105">The [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) metapackage for ASP.NET Core:</span></span>

* <span data-ttu-id="3cc9f-106">Nie ma zależności innych firm, z wyjątkiem [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/), i [Async Popraw](https://www.nuget.org/packages/System.Interactive.Async/).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-106">Does not include third-party dependencies except for [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/), and [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/).</span></span> <span data-ttu-id="3cc9f-107">Te zależności 3rd firm uważa za zapewnienie struktur głównych funkcji.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-107">These 3rd-party dependencies are deemed necessary to ensure the major frameworks features function.</span></span>
* <span data-ttu-id="3cc9f-108">Zawiera wszystkie pakiety obsługiwanych przez zespół platformy ASP.NET Core, z wyjątkiem tych, które zawierają zależności innych firm (inne niż wymienione wcześniej).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-108">Includes all supported packages by the ASP.NET Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>
* <span data-ttu-id="3cc9f-109">Zawiera wszystkie pakiety obsługiwanych przez zespół Entity Framework Core, z wyjątkiem tych, które zawierają zależności innych firm (inne niż wymienione wcześniej).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-109">Includes all supported packages by the Entity Framework Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>

<span data-ttu-id="3cc9f-110">Obejmuje wszystkie funkcje platformy ASP.NET Core 2.1 i nowsze i Entity Framework Core 2.1 i nowsze `Microsoft.AspNetCore.App` pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-110">All the features of ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later are included in the `Microsoft.AspNetCore.App` package.</span></span> <span data-ttu-id="3cc9f-111">Domyślne szablony przeznaczonych dla platformy ASP.NET Core 2.1 projektu i później użyć tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-111">The default project templates targeting ASP.NET Core 2.1 and later use this package.</span></span> <span data-ttu-id="3cc9f-112">Firma Microsoft zaleca aplikacji przeznaczonych dla platformy ASP.NET Core 2.1 i nowsze oraz Entity Framework Core 2.1 i później użyć `Microsoft.AspNetCore.App` pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-112">We recommend applications targeting ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later use the `Microsoft.AspNetCore.App` package.</span></span>

<span data-ttu-id="3cc9f-113">Numer wersji `Microsoft.AspNetCore.App` metapackage reprezentuje wersji platformy ASP.NET Core i wersji programu Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-113">The version number of the `Microsoft.AspNetCore.App` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="3cc9f-114">Przy użyciu `Microsoft.AspNetCore.App` metapackage zapewnia ograniczenia wersji, służących do ochrony aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3cc9f-114">Using the `Microsoft.AspNetCore.App` metapackage provides version restrictions that protect your app:</span></span>

* <span data-ttu-id="3cc9f-115">Jeśli pakiet jest uwzględniony w pakiecie w mający przechodnie zależności (bezpośrednich nie) `Microsoft.AspNetCore.App`i tych numerów wersji są różne, NuGet spowoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-115">If a package is included that has a transitive (not direct) dependency on a package in `Microsoft.AspNetCore.App`, and those version numbers differ, NuGet will generate an error.</span></span>
* <span data-ttu-id="3cc9f-116">Inne pakiety dodany do aplikacji nie można zmienić wersji pakietów zawarte w `Microsoft.AspNetCore.App`.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-116">Other packages added to your app cannot change the version of packages included in `Microsoft.AspNetCore.App`.</span></span>
* <span data-ttu-id="3cc9f-117">Spójność wersji zapewnia niezawodne środowisko.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-117">Version consistency ensures a reliable experience.</span></span> <span data-ttu-id="3cc9f-118">`Microsoft.AspNetCore.App` została zaprojektowana w celu zapobiegania kombinacji wersji zastosowaniem bitów powiązane ze sobą używany w tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-118">`Microsoft.AspNetCore.App` was designed to prevent untested version combinations of related bits being used together in the same app.</span></span>

<span data-ttu-id="3cc9f-119">Aplikacje używające `Microsoft.AspNetCore.App` metapackage automatycznie korzystać udostępnionego platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-119">Applications that use the `Microsoft.AspNetCore.App` metapackage automatically take advantage of the ASP.NET Core shared framework.</span></span> <span data-ttu-id="3cc9f-120">Jeśli używasz `Microsoft.AspNetCore.App` metapackage, **nie** zasobów, z którym związane są odwołania pakietów platformy ASP.NET Core NuGet zostały wdrożone za pomocą aplikacji &mdash; framework udostępnionego platformy ASP.NET Core zawiera te zasoby.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-120">When you use the `Microsoft.AspNetCore.App` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the ASP.NET Core shared framework contains these assets.</span></span> <span data-ttu-id="3cc9f-121">Zasoby w ramach udostępnionego są wstępnie skompilowana zwiększające czasu uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-121">The assets in the shared framework are precompiled to improve application startup time.</span></span> <span data-ttu-id="3cc9f-122">Aby uzyskać więcej informacji, zobacz "udostępnionego framework" w [pakowania dystrybucji .NET Core](/dotnet/core/build/distribution-packaging).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-122">For more information, see "shared framework" in [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging).</span></span>

<span data-ttu-id="3cc9f-123">Następujące *.csproj* odwołania do pliku projektu `Microsoft.AspNetCore.App` metapackage dla platformy ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="3cc9f-123">The following *.csproj* project file references the `Microsoft.AspNetCore.App` metapackage for ASP.NET Core:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>

```

<span data-ttu-id="3cc9f-124">Poprzedni kod znaczników reprezentuje typowy platformy ASP.NET Core 2.1 i nowsze szablonu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-124">The preceding markup represents a typical ASP.NET Core 2.1 and later template.</span></span> <span data-ttu-id="3cc9f-125">Nie określono numeru wersji `Microsoft.AspNetCore.App` odwołanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-125">It doesn't specify a version number for the `Microsoft.AspNetCore.App` package reference.</span></span> <span data-ttu-id="3cc9f-126">Jeśli nie określono wersji, niejawne wersja jest określona przez zestaw SDK, oznacza to, `Microsoft.NET.Sdk.Web`.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-126">When the version is not specified, an implicit version is specified by the SDK, that is, `Microsoft.NET.Sdk.Web`.</span></span> <span data-ttu-id="3cc9f-127">Firma Microsoft zaleca polegania na niejawne wersja określona przez zestaw SDK i nie jawne ustawienie numer wersji na odwołanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-127">We recommend relying on the implicit version specified by the SDK and not explicitly setting the version number on the package reference.</span></span> <span data-ttu-id="3cc9f-128">Możesz pozostawić komentarz GitHub w [dyskusji dla wersji niejawne Microsoft.AspNetCore.App](https://github.com/aspnet/Docs/issues/6430).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-128">You can leave a GitHub comment at [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430).</span></span>

<span data-ttu-id="3cc9f-129">Niejawne wersji ma ustawioną wartość `major.minor.0` dla aplikacji przenośnej.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-129">The implicit version is set to `major.minor.0` for portable apps.</span></span> <span data-ttu-id="3cc9f-130">Mechanizm przewijaniem do udostępnionego framework uruchomi aplikacji z najnowszą wersją zgodne między zainstalowanych platform udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-130">The shared framework roll-forward mechanism will run the app on the latest compatible version among the installed shared frameworks.</span></span> <span data-ttu-id="3cc9f-131">Aby zagwarantować, że ta sama wersja jest używana w rozwoju, testów i produkcji, upewnij się, że ta sama wersja programu udostępnionego framework jest zainstalowana we wszystkich środowiskach.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-131">To guarantee the same version is used in development, test, and production, ensure the same version of the shared framework is installed in all environments.</span></span> <span data-ttu-id="3cc9f-132">Aplikacje samodzielną numer wersji niejawne ustawiono `major.minor.patch` powiązane zainstalowanego zestawu SDK platformy udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-132">For self contained apps, the implicit version number is set to the `major.minor.patch` of the shared framework bundled in the installed SDK.</span></span>

<span data-ttu-id="3cc9f-133">Określenie numeru wersji w `Microsoft.AspNetCore.App` odwołania jest **nie** zagwarantować tej wersji udostępnionego framework zostanie wybrany.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-133">Specifying a version number on the `Microsoft.AspNetCore.App` reference does **not** guarantee that version of the shared framework will be chosen.</span></span> <span data-ttu-id="3cc9f-134">Na przykład załóżmy, że określono wersji "2.1.1", ale "2.1.3" jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="3cc9f-134">For example, suppose version "2.1.1" is specified, but "2.1.3" is installed.</span></span> <span data-ttu-id="3cc9f-135">W takim przypadku aplikacja będzie używać "2.1.3".</span><span class="sxs-lookup"><span data-stu-id="3cc9f-135">In that case, the app will use "2.1.3".</span></span> <span data-ttu-id="3cc9f-136">Chociaż nie jest to zalecane, można wyłączyć przenoszenia do przodu (poprawki i/lub pomocniczej).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-136">Although not recommended, you can disable roll forward (patch and/or minor).</span></span> <span data-ttu-id="3cc9f-137">Aby uzyskać więcej informacji dotyczących hosta dotnet przewijaniem do i konfigurowanie zachowania, zobacz [dotnet hosta przenoszenia do przodu](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-137">For more information regarding dotnet host roll-forward and how to configure its behavior, see [dotnet host roll forward](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span></span>

<span data-ttu-id="3cc9f-138">Jeśli wcześniej używana aplikacja `Microsoft.AspNetCore.All`, zobacz [migrowania Microsoft.AspNetCore.All do Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate).</span><span class="sxs-lookup"><span data-stu-id="3cc9f-138">If your application previously used `Microsoft.AspNetCore.All`, see [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate).</span></span>