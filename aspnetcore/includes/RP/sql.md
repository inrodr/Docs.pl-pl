# <a name="working-with-sqlite-in-and-razor-pages"></a><span data-ttu-id="bae2e-101">Praca z bazy danych SQLite w i stron Razor</span><span class="sxs-lookup"><span data-stu-id="bae2e-101">Working with SQLite in and Razor Pages</span></span>

<span data-ttu-id="bae2e-102">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bae2e-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="bae2e-103">`MovieContext` Obiektu obsługuje zadanie łączenia z bazą danych i mapowanie `Movie` obiektów do rekordów bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bae2e-103">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="bae2e-104">Kontekst bazy danych został zarejestrowany za pomocą [iniekcji zależności](xref:fundamentals/dependency-injection) kontenera w `ConfigureServices` metody w *Startup.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="bae2e-104">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[Main](code/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a><span data-ttu-id="bae2e-105">SQLite</span><span class="sxs-lookup"><span data-stu-id="bae2e-105">SQLite</span></span>

<span data-ttu-id="bae2e-106">[SQLite](https://www.sqlite.org/) stanów witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="bae2e-106">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="bae2e-107">SQLite jest niezależna, wysokiej niezawodności, osadzone, oferujący wszystkie funkcje, domeny publicznej, aparatu bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bae2e-107">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="bae2e-108">SQLite jest najczęściej używanych aparatu bazy danych na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="bae2e-108">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="bae2e-109">Istnieje wiele narzędzi innych firm, które można pobrać do zarządzania i wyświetlić bazy danych SQLite.</span><span class="sxs-lookup"><span data-stu-id="bae2e-109">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="bae2e-110">Na poniższym obrazie pochodzi z [przeglądarki bazy danych dla bazy danych SQLite](http://sqlitebrowser.org/).</span><span class="sxs-lookup"><span data-stu-id="bae2e-110">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="bae2e-111">Jeśli masz ulubionego narzędzia SQLite, zostaw komentarz w takich jak informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="bae2e-111">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![Przeglądarka bazy danych dla bazy danych Film przedstawiający SQLite](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="bae2e-113">Inicjatora bazy danych</span><span class="sxs-lookup"><span data-stu-id="bae2e-113">Seed the database</span></span>

<span data-ttu-id="bae2e-114">Utwórz nową klasę o nazwie `SeedData` w *modele* folderu.</span><span class="sxs-lookup"><span data-stu-id="bae2e-114">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="bae2e-115">Zastąp wygenerowany kod poniżej:</span><span class="sxs-lookup"><span data-stu-id="bae2e-115">Replace the generated code with the following:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="bae2e-116">Jeśli w bazie danych są wszystkie filmy, zwraca inicjatora inicjatora.</span><span class="sxs-lookup"><span data-stu-id="bae2e-116">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="bae2e-117">Dodaj inicjatora inicjatora</span><span class="sxs-lookup"><span data-stu-id="bae2e-117">Add the seed initializer</span></span>

<span data-ttu-id="bae2e-118">Inicjator inicjatora, aby dodać `Main` metody w *Program.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="bae2e-118">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]

### <a name="test-the-app"></a><span data-ttu-id="bae2e-119">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bae2e-119">Test the app</span></span>

<span data-ttu-id="bae2e-120">Usuń wszystkie rekordy w bazie danych (co seed — metoda będzie uruchamiane).</span><span class="sxs-lookup"><span data-stu-id="bae2e-120">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="bae2e-121">Zatrzymać i uruchomić aplikację w celu umieszczenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bae2e-121">Stop and start the app to seed the database.</span></span>
   
<span data-ttu-id="bae2e-122">Aplikacja zawiera wprowadzonych danych.</span><span class="sxs-lookup"><span data-stu-id="bae2e-122">The app shows the seeded data.</span></span>