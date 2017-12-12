---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: Wprowadzenie do platformy ASP.NET MVC 3 (VB) | Dokumentacja firmy Microsoft
author: Rick-Anderson
description: "Ten samouczek pokazuje podstawowe informacje dotyczące tworzenia aplikacji sieci Web programu ASP.NET MVC przy użyciu Microsoft Visual Web Developer 2010 Express Service Pack 1, która jest..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: f0717e8d635818322be8b3242efe756a20351340
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="16b24-103">Wprowadzenie do platformy ASP.NET MVC 3 (VB)</span><span class="sxs-lookup"><span data-stu-id="16b24-103">Intro to ASP.NET MVC 3 (VB)</span></span>
====================
<span data-ttu-id="16b24-104">Przez [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="16b24-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="16b24-105">Ten samouczek pokazuje podstawowe informacje dotyczące tworzenia aplikacji sieci Web programu ASP.NET MVC przy użyciu Microsoft Visual Web Developer 2010 Express Service Pack 1, która jest bezpłatna wersja programu Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16b24-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="16b24-106">Przed rozpoczęciem upewnij się, że po zainstalowaniu wymagania wstępne wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="16b24-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="16b24-107">Można zainstalować wszystkie z nich, klikając poniższe łącze: [Instalatora platformy sieci Web](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="16b24-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="16b24-108">Alternatywnie można zainstalować oddzielnie wymagania wstępne, korzystając z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="16b24-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="16b24-109">Visual Studio Web Developer Express z dodatkiem SP1 wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16b24-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="16b24-110">Aktualizacji narzędzi programu ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="16b24-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="16b24-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(środowisko uruchomieniowe + narzędzia pomocy technicznej)</span><span class="sxs-lookup"><span data-stu-id="16b24-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="16b24-112">Jeśli używasz programu Visual Studio 2010, zamiast Visual Web Developer 2010, zainstaluj wymagania wstępne, klikając poniższe łącze: [wymagania wstępne programu Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="16b24-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="16b24-113">Projekt Visual Web Developer z kodem źródłowym VB.NET jest dostępna powiązany z tym tematem.</span><span class="sxs-lookup"><span data-stu-id="16b24-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="16b24-114">[Pobierz wersję VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="16b24-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="16b24-115">Jeśli wolisz C#, przełącz się do [wersji języka C#](../cs/intro-to-aspnet-mvc-3.md) tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="16b24-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="16b24-116">Ten samouczek pokazuje podstawowe informacje dotyczące tworzenia aplikacji sieci Web programu ASP.NET MVC przy użyciu Microsoft Visual Web Developer 2010 Express Service Pack 1, która jest bezpłatna wersja programu Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16b24-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="16b24-117">Przed rozpoczęciem upewnij się, że po zainstalowaniu wymagania wstępne wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="16b24-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="16b24-118">Można zainstalować wszystkie z nich, klikając poniższe łącze: [Instalatora platformy sieci Web](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="16b24-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="16b24-119">Alternatywnie można zainstalować oddzielnie wymagania wstępne, korzystając z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="16b24-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="16b24-120">Visual Studio Web Developer Express z dodatkiem SP1 wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16b24-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="16b24-121">Aktualizacji narzędzi programu ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="16b24-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="16b24-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(środowisko uruchomieniowe + narzędzia pomocy technicznej)</span><span class="sxs-lookup"><span data-stu-id="16b24-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="16b24-123">Jeśli używasz programu Visual Studio 2010, zamiast Visual Web Developer 2010, zainstaluj wymagania wstępne, klikając poniższe łącze: [wymagania wstępne programu Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="16b24-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="16b24-124">Projekt Visual Web Developer z kodem źródłowym VB jest dostępna powiązany z tym tematem.</span><span class="sxs-lookup"><span data-stu-id="16b24-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="16b24-125">[Pobierz wersję VB tutaj](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span><span class="sxs-lookup"><span data-stu-id="16b24-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="16b24-126">Jeśli wolisz CSharp, przełącz się do [wersji języka CSharp](../cs/intro-to-aspnet-mvc-3.md) tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="16b24-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="16b24-127">Jakie będzie kompilacji</span><span class="sxs-lookup"><span data-stu-id="16b24-127">What You'll Build</span></span>

<span data-ttu-id="16b24-128">Będzie implementuje prostą aplikację listy filmów, która obsługuje tworzenie, edytowanie i wyświetlanie filmów z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="16b24-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="16b24-129">Poniżej przedstawiono dwa zrzuty ekranu aplikacji, która będzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="16b24-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="16b24-130">Obejmuje on strona, wyświetlająca listę filmów z bazy danych:</span><span class="sxs-lookup"><span data-stu-id="16b24-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="16b24-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16b24-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="16b24-132">Aplikacja umożliwia także dodawania, edytowania i usuwania, filmów, a także szczegółowe informacje można znaleźć o pojedyncze pliki.</span><span class="sxs-lookup"><span data-stu-id="16b24-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="16b24-133">Wszystkie scenariusze wprowadzania danych sprawdzania poprawności, aby upewnić się, że dane przechowywane w bazie danych są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="16b24-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="16b24-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="16b24-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="16b24-135">Dowiesz się umiejętności</span><span class="sxs-lookup"><span data-stu-id="16b24-135">Skills You'll Learn</span></span>

<span data-ttu-id="16b24-136">Oto dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="16b24-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="16b24-137">Jak utworzyć nowy projekt ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="16b24-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="16b24-138">Jak utworzyć nową bazę danych przy użyciu pierwszego kodu programu Entity Framework</span><span class="sxs-lookup"><span data-stu-id="16b24-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="16b24-139">Jak utworzyć ASP.NET MVC, kontrolery i widoki</span><span class="sxs-lookup"><span data-stu-id="16b24-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="16b24-140">Jak pobrać i wyświetlanie danych</span><span class="sxs-lookup"><span data-stu-id="16b24-140">How to retrieve and display data</span></span>
- <span data-ttu-id="16b24-141">Jak edytować dane i włączyć sprawdzanie poprawności danych</span><span class="sxs-lookup"><span data-stu-id="16b24-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="16b24-142">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="16b24-142">Getting Started</span></span>

<span data-ttu-id="16b24-143">Zacznij od uruchomienia programu Visual Web Developer 2010 Express ("VWD" skrócie) i wybierz **nowy projekt** z **Start** strony.</span><span class="sxs-lookup"><span data-stu-id="16b24-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="16b24-144">Visual Web Developer jest IDE lub zintegrowane środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="16b24-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="16b24-145">Tak samo jak w programie Microsoft Word do zapisywania dokumentów, użyjesz IDE do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16b24-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="16b24-146">Visual Web Developer ma narzędzi wzdłuż górnej pokazywanie różnych dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="16b24-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="16b24-147">Istnieje również menu, która umożliwia innym sposobem wykonania zadania w środowisku IDE.</span><span class="sxs-lookup"><span data-stu-id="16b24-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="16b24-148">(Na przykład zamiast zaznaczania **nowy projekt** z **Start** strony, można skorzystać z menu i wybierz **pliku** &gt; **nowy projekt**.)</span><span class="sxs-lookup"><span data-stu-id="16b24-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="16b24-149">Tworzenie pierwszej aplikacji</span><span class="sxs-lookup"><span data-stu-id="16b24-149">Creating Your First Application</span></span>

<span data-ttu-id="16b24-150">Można tworzyć aplikacje przy użyciu wybór języka Visual Basic lub Visual C# jako języka programowania.</span><span class="sxs-lookup"><span data-stu-id="16b24-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="16b24-151">W tym samouczku, wybierz pozycję Visual Basic po lewej stronie, a następnie wybierz **aplikacji sieci Web programu ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="16b24-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="16b24-152">Nazwa projektu "MvcMovie", a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="16b24-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="16b24-154">W **nowy projekt programu ASP.NET MVC 3** okno dialogowe, wybierz opcję **aplikacji internetowej**.</span><span class="sxs-lookup"><span data-stu-id="16b24-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="16b24-155">Pozostaw **Razor** jako domyślny aparat widoku.</span><span class="sxs-lookup"><span data-stu-id="16b24-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="16b24-157">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="16b24-157">Click **OK**.</span></span> <span data-ttu-id="16b24-158">Visual Web Developer używany szablon domyślny projektu programu ASP.NET MVC, który właśnie utworzony, więc w tej chwili oferuje działającą aplikację bez żadnego działania!</span><span class="sxs-lookup"><span data-stu-id="16b24-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="16b24-159">Jest to prosty "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="16b24-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="16b24-160">Projekt, a jego dobrym miejscem do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16b24-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="16b24-161">Z **debugowania** menu, wybierz opcję **Rozpocznij debugowanie**.</span><span class="sxs-lookup"><span data-stu-id="16b24-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="16b24-162">Zwróć uwagę, że skrót klawiaturowy można rozpocząć debugowania jest F5.</span><span class="sxs-lookup"><span data-stu-id="16b24-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="16b24-163">F5 powoduje, że Visual Web Developer uruchomić serwera wdrożeniowego sieci web i uruchom aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="16b24-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="16b24-164">Następnie VWD spowoduje uruchomienie przeglądarki i spowoduje otwarcie strony głównej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16b24-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="16b24-165">Należy zauważyć, że na pasku adresu przeglądarki mówi `localhost` i nie coś, takich jak `example.com`.</span><span class="sxs-lookup"><span data-stu-id="16b24-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="16b24-166">Jest to spowodowane tym `localhost` zawsze wskazuje na własnym komputerze lokalnym, działającego w takim przypadku aplikacji zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="16b24-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="16b24-167">Po uruchomieniu projektu sieci web VWD losowy port jest używany dla projektu.</span><span class="sxs-lookup"><span data-stu-id="16b24-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="16b24-168">Na poniższej ilustracji numer portu losowe jest 43246.</span><span class="sxs-lookup"><span data-stu-id="16b24-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="16b24-169">Projekt użyje prawdopodobnie inny numer portu.</span><span class="sxs-lookup"><span data-stu-id="16b24-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="16b24-170">Poza pole ten szablon domyślny zawiera dwie strony do odwiedzenia i strony logowania podstawowe.</span><span class="sxs-lookup"><span data-stu-id="16b24-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="16b24-171">Teraz zmienić sposób działania tej aplikacji i uzyskiwanie nieco ASP.NET MVC w procesie.</span><span class="sxs-lookup"><span data-stu-id="16b24-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="16b24-172">Zamknij przeglądarkę i Zmieńmy kodu.</span><span class="sxs-lookup"><span data-stu-id="16b24-172">Close your browser and let's change some code.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="16b24-173">Dalej</span><span class="sxs-lookup"><span data-stu-id="16b24-173">Next</span></span>](adding-a-controller.md)