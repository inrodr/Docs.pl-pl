---
title: Zastąp machineKey ASP.NET w ASP.NET Core
author: rick-anderson
description: Dowiedzieć się, jak zastąpić machineKey w programie ASP.NET do korzystania z systemu ochrony danych nowych i bardziej bezpieczne.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/compatibility/replacing-machinekey
ms.openlocfilehash: 5f9e5cec02b66e1315548c4e7c18fe168ad161eb
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278827"
---
# <a name="replace-the-aspnet-machinekey-in-aspnet-core"></a>Zastąp machineKey ASP.NET w ASP.NET Core

<a name="compatibility-replacing-machinekey"></a>

Implementacja `<machineKey>` elementu w programie ASP.NET [jest wymienny](https://blogs.msdn.microsoft.com/webdev/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2/). Dzięki temu większość wywołania procedur kryptograficznych ASP.NET go przekierować przez mechanizm wymiany danych ochrony, łącznie z nowego systemu ochrony danych.

## <a name="package-installation"></a>Instalacja pakietu

> [!NOTE]
> Nowy system ochrony danych można tylko zainstalowana w istniejącej aplikacji programu ASP.NET przeznaczonych dla platformy .NET 4.5.1 lub nowszej. Instalacja będzie się niepowodzeniem, jeśli aplikacja jest przeznaczony dla platformy .NET 4.5 lub niższy.

Aby zainstalować nowy system ochrony danych do istniejącego projektu 4.5.1+ ASP.NET, należy zainstalować pakiet Microsoft.AspNetCore.DataProtection.SystemWeb. To spowoduje utworzenie wystąpienia użycie systemu ochrony danych [domyślnej konfiguracji](xref:security/data-protection/configuration/default-settings) ustawienia.

Po zainstalowaniu pakietu do wstawienia wiersza do *Web.config* , który zawiadamia ASP.NET, aby użyć go do [większości operacji kryptograficznych](https://blogs.msdn.microsoft.com/webdev/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2/), w tym uwierzytelniania formularzy, stan widoku i wywołań MachineKey.Protect. Wiersz wstawiony odczytuje w następujący sposób.

```xml
<machineKey compatibilityMode="Framework45" dataProtectorType="..." />
```

>[!TIP]
> Można określić, czy nowy system ochrony danych jest aktywna, sprawdzając pól `__VIEWSTATE`, którego powinny rozpoczynać się od "CfDJ8" tak jak w poniższym przykładzie. "CfDJ8" jest reprezentacja base64 nagłówek magic "09 F0 C9 F0", który identyfikuje ładunku chronionego przez system ochrony danych.

```html
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="CfDJ8AWPr2EQPTBGs3L2GCZOpk..." />
```

## <a name="package-configuration"></a>Konfiguracja pakietu

System ochrony danych zostanie uruchomiony z domyślnej konfiguracji instalacji zero. Jednak ponieważ domyślnie klucze są zapisywane w lokalnym systemie plików, to nie będzie działać dla aplikacji, które zostały wdrożone w farmie. Aby rozwiązać ten problem, można podać konfigurację przez tworzenie podklas, które DataProtectionStartup typu i zastępuje jego metodę ConfigureServices.

Poniżej znajduje się przykład typ uruchomienia ochrony danych niestandardowych, który skonfigurowano zarówno której klucze są zachowywane i sposób ich są szyfrowane, gdy. Zastępuje również domyślne zasady izolacji aplikacji, zapewniając własną nazwę aplikacji.

```csharp
using System;
using System.IO;
using Microsoft.AspNetCore.DataProtection;
using Microsoft.AspNetCore.DataProtection.SystemWeb;
using Microsoft.Extensions.DependencyInjection;

namespace DataProtectionDemo
{
    public class MyDataProtectionStartup : DataProtectionStartup
    {
        public override void ConfigureServices(IServiceCollection services)
        {
            services.AddDataProtection()
                .SetApplicationName("my-app")
                .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\myapp-keys\"))
                .ProtectKeysWithCertificate("thumbprint");
        }
    }
}
```

>[!TIP]
> Można również użyć `<machineKey applicationName="my-app" ... />` zamiast jawnym wywołaniem SetApplicationName. Jest to mechanizm wygody, aby uniknąć wymuszania deweloperom tworzenie typu pochodnego DataProtectionStartup, jeśli został wszystkich chcieli skonfigurować ustawienie nazwy aplikacji.

Aby włączyć to Konfiguracja niestandardowa, przejdź wstecz do pliku Web.config i wyszukaj `<appSettings>` element zainstalować pakiet dodane do pliku konfiguracji. Będzie wyglądać następujący kod:

```xml
<appSettings>
  <!--
  If you want to customize the behavior of the ASP.NET Core Data Protection stack, set the
  "aspnet:dataProtectionStartupType" switch below to be the fully-qualified name of a
  type which subclasses Microsoft.AspNetCore.DataProtection.SystemWeb.DataProtectionStartup.
  -->
  <add key="aspnet:dataProtectionStartupType" value="" />
</appSettings>
```

Wypełnij puste wartości z kwalifikowaną dla zestawu nazwę typu pochodnego DataProtectionStartup, utworzony. Jeśli nazwa aplikacji jest DataProtectionDemo, będzie wyglądać podobnie jak poniżej.

```xml
<add key="aspnet:dataProtectionStartupType"
     value="DataProtectionDemo.MyDataProtectionStartup, DataProtectionDemo" />
```

System ochrony danych nowo skonfigurowane jest teraz gotowa do użycia w aplikacji.
