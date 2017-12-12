---
title: Praca z bazy danych LocalDB programu SQL Server
author: rick-anderson
description: "Przy użyciu bazy danych LocalDB programu SQL Server z prostej aplikacji MVC"
keywords: Platformy ASP.NET Core bazy danych LocalDB programu SQL Server LocalDB, programu SQL Server
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.assetid: ff8fd9b8-7c98-424d-8641-7524e23bf541
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/working-with-sql
ms.openlocfilehash: 67894d05bfd44b0406d10cbbe30ddfdaf0d66636
ms.sourcegitcommit: 8f42ab93402c1b8044815e1e48d0bb84c81f8b59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2017
---
# <a name="working-with-sql-server-localdb"></a><span data-ttu-id="91862-104">Praca z bazy danych LocalDB programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="91862-104">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="91862-105">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="91862-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="91862-106">`MvcMovieContext` Obiektu obsługuje zadanie łączenia z bazą danych i mapowanie `Movie` obiektów do rekordów bazy danych.</span><span class="sxs-lookup"><span data-stu-id="91862-106">The `MvcMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="91862-107">Kontekst bazy danych został zarejestrowany za pomocą [iniekcji zależności](xref:fundamentals/dependency-injection) kontenera w `ConfigureServices` metody w *Startup.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="91862-107">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]

<span data-ttu-id="91862-108">Platformy ASP.NET Core [konfiguracji](xref:fundamentals/configuration/index) odczyty systemu `ConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="91862-108">The ASP.NET Core [Configuration](xref:fundamentals/configuration/index) system reads the `ConnectionString`.</span></span> <span data-ttu-id="91862-109">Lokalne działania projektowe, pobiera parametry połączenia z *appsettings.json* pliku:</span><span class="sxs-lookup"><span data-stu-id="91862-109">For local development, it gets the connection string from the *appsettings.json* file:</span></span>

[!code-json[Main](start-mvc/sample/MvcMovie/appsettings.json?highlight=2&range=8-10)]

<span data-ttu-id="91862-110">Podczas wdrażania aplikacji na serwerze testowym lub produkcyjnym, można użyć zmiennej środowiskowej lub innej metody, aby ustawić parametry połączenia do rzeczywistego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="91862-110">When you deploy the app to a test or production server, you can use an environment variable or another approach to set the connection string to a real SQL Server.</span></span> <span data-ttu-id="91862-111">Zobacz [konfiguracji](xref:fundamentals/configuration/index) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="91862-111">See [Configuration](xref:fundamentals/configuration/index) for more information.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="91862-112">SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="91862-112">SQL Server Express LocalDB</span></span>

<span data-ttu-id="91862-113">To Zubożona wersja programu SQL Server Express aparat bazy danych jest przeznaczony do tworzenia aplikacji programu.</span><span class="sxs-lookup"><span data-stu-id="91862-113">LocalDB is a lightweight version of the SQL Server Express Database Engine that is targeted for program development.</span></span> <span data-ttu-id="91862-114">LocalDB rozpoczyna się na żądanie i działa w trybie użytkownika, więc nie ma żadnych złożonych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="91862-114">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="91862-115">Domyślnie tworzy bazy danych LocalDB "\*.mdf" plików *C:/Users/\<użytkownika\>*  katalogu.</span><span class="sxs-lookup"><span data-stu-id="91862-115">By default, LocalDB database creates "\*.mdf" files in the *C:/Users/\<user\>* directory.</span></span>

* <span data-ttu-id="91862-116">Z **widoku** menu, otwórz **Eksplorator obiektów SQL Server** (SSOX).</span><span class="sxs-lookup"><span data-stu-id="91862-116">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![Menu Widok](working-with-sql/_static/ssox.png)

* <span data-ttu-id="91862-118">Kliknij prawym przyciskiem myszy `Movie` tabeli **> Widok projektanta**</span><span class="sxs-lookup"><span data-stu-id="91862-118">Right click on the `Movie` table **> View Designer**</span></span>

  ![Menu kontekstowe otwarty na tabeli film](working-with-sql/_static/design.png)

  ![Otwórz w projektancie tabeli film](working-with-sql/_static/dv.png)

<span data-ttu-id="91862-121">Należy pamiętać ikonę klucza, obok pozycji `ID`.</span><span class="sxs-lookup"><span data-stu-id="91862-121">Note the key icon next to `ID`.</span></span> <span data-ttu-id="91862-122">Domyślnie EF spowoduje, że właściwość o nazwie `ID` klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="91862-122">By default, EF will make a property named `ID` the primary key.</span></span>

* <span data-ttu-id="91862-123">Kliknij prawym przyciskiem myszy `Movie` tabeli **> Wyświetlanie danych**</span><span class="sxs-lookup"><span data-stu-id="91862-123">Right click on the `Movie` table **> View Data**</span></span>

  ![Menu kontekstowe otwarty na tabeli film](working-with-sql/_static/ssox2.png)

  ![Otwórz tabelę dane są wyświetlane tabeli film](working-with-sql/_static/vd22.png)

## <a name="seed-the-database"></a><span data-ttu-id="91862-126">Inicjatora bazy danych</span><span class="sxs-lookup"><span data-stu-id="91862-126">Seed the database</span></span>

<span data-ttu-id="91862-127">Utwórz nową klasę o nazwie `SeedData` w *modele* folderu.</span><span class="sxs-lookup"><span data-stu-id="91862-127">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="91862-128">Zastąp wygenerowany kod poniżej:</span><span class="sxs-lookup"><span data-stu-id="91862-128">Replace the generated code with the following:</span></span>

[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="91862-129">Jeśli w bazie danych są wszystkie filmy, zwraca inicjatora inicjatora i filmy nie zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="91862-129">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="91862-130">Dodaj inicjatora inicjatora</span><span class="sxs-lookup"><span data-stu-id="91862-130">Add the seed initializer</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="91862-131">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="91862-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="91862-132">Inicjator inicjatora, aby dodać `Main` metody w *Program.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="91862-132">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[Main](start-mvc/sample/MvcMovie/Program.cs?highlight=6,14-32)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="91862-133">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="91862-133">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="91862-134">Dodaj inicjatora inicjatora na końcu `Configure` metody w *Startup.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="91862-134">Add the seed initializer to the end of the `Configure` method in the *Startup.cs* file.</span></span>

[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]

---

<span data-ttu-id="91862-135">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="91862-135">Test the app</span></span>

* <span data-ttu-id="91862-136">Usuń wszystkie rekordy w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="91862-136">Delete all the records in the DB.</span></span> <span data-ttu-id="91862-137">Można to zrobić z łączami Usuń w przeglądarce lub SSOX.</span><span class="sxs-lookup"><span data-stu-id="91862-137">You can do this with the delete links in the browser or from SSOX.</span></span>
* <span data-ttu-id="91862-138">Wymusić na aplikacji, aby zainicjować (wywołanie metody w `Startup` klasy), uruchamia seed — metoda.</span><span class="sxs-lookup"><span data-stu-id="91862-138">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="91862-139">Aby wymusić inicjowania, usługi IIS Express musi zostać zatrzymana i uruchomiona ponownie.</span><span class="sxs-lookup"><span data-stu-id="91862-139">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="91862-140">Można to zrobić za pomocą dowolnego z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="91862-140">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="91862-141">Kliknij prawym przyciskiem myszy ikonę na pasku zadań systemu usług IIS Express w obszarze powiadomień, a następnie wybierz polecenie **zakończenia** lub **zatrzymania lokacji**</span><span class="sxs-lookup"><span data-stu-id="91862-141">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**</span></span>

    ![Usługi IIS Express ikony paska zadań](working-with-sql/_static/iisExIcon.png)

    ![Menu kontekstowe](working-with-sql/_static/stopIIS.png)

   * <span data-ttu-id="91862-144">Podczas uruchamiania programu VS w trybie bez debugowania, naciśnij klawisz F5, aby uruchomić w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="91862-144">If you were running VS in non-debug mode, press F5 to run in debug mode</span></span>
   * <span data-ttu-id="91862-145">W przypadku korzystania z wersji programu VS w trybie debugowania, zatrzymaniu debugera i naciśnij klawisz F5</span><span class="sxs-lookup"><span data-stu-id="91862-145">If you were running VS in debug mode, stop the debugger and press F5</span></span>
   
<span data-ttu-id="91862-146">Aplikacja zawiera wprowadzonych danych.</span><span class="sxs-lookup"><span data-stu-id="91862-146">The app shows the seeded data.</span></span>

![Aplikacja MVC Movie otworzyć w programie Microsoft Edge danych Film przedstawiający](working-with-sql/_static/m55.png)

>[!div class="step-by-step"]
<span data-ttu-id="91862-148">[Poprzednie](adding-model.md)
[dalej](controller-methods-views.md)</span><span class="sxs-lookup"><span data-stu-id="91862-148">[Previous](adding-model.md)
[Next](controller-methods-views.md)</span></span>  