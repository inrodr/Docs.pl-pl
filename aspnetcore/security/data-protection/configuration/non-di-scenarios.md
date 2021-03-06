---
title: Inne niż Podpisane pamiętać scenariusze dotyczące ochrony danych platformy ASP.NET Core
author: rick-anderson
description: Dowiedz się, jak obsługiwać scenariusze ochrony danych, których nie może lub nie chcesz używać usługi udostępniane przez iniekcji zależności.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/configuration/non-di-scenarios
ms.openlocfilehash: 34354c8443f6ae00bcce6ad9bdb6c11aaaa25bf8
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276883"
---
# <a name="non-di-aware-scenarios-for-data-protection-in-aspnet-core"></a>Inne niż Podpisane pamiętać scenariusze dotyczące ochrony danych platformy ASP.NET Core

przez [Rick Anderson](https://twitter.com/RickAndMSFT)

System ochrony danych platformy ASP.NET Core jest zwykle [dodać do kontenera usługi](xref:security/data-protection/consumer-apis/overview) i używane przez składniki zależne za pomocą iniekcji zależności (Podpisane). Istnieją jednak przypadki, w którym nie jest możliwe lub żądanych, szczególnie w przypadku importowania systemu do istniejącej aplikacji.

Do obsługi tych scenariuszy [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) pakiet zawiera typem konkretnym [DataProtectionProvider](/dotnet/api/Microsoft.AspNetCore.DataProtection.DataProtectionProvider), który zapewnia prosty sposób korzystania z ochrony danych bez polegania na Podpisane. `DataProtectionProvider` Typ implementuje [IDataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionprovider). Konstruowanie `DataProtectionProvider` wymaga tylko podanie [DirectoryInfo](/dotnet/api/system.io.directoryinfo) wystąpienia, aby wskazać, którym powinny być przechowywane klucze szyfrowania dostawcy, jak pokazano w poniższym przykładzie kodu:

[!code-none[](non-di-scenarios/_static/nodisample1.cs)]

Domyślnie `DataProtectionProvider` konkretnego typu nie szyfruje raw materiału klucza przed wprowadzeniem trwałych do systemu plików. To obsługi scenariuszy, w którym punktami dewelopera systemu ochrony danych i udziału sieciowego automatycznie nie można wywnioskować mechanizm szyfrowania odpowiednie na rest.

Ponadto `DataProtectionProvider` nie konkretnego typu [izolowania aplikacji](xref:security/data-protection/configuration/overview#per-application-isolation) domyślnie. Wszystkie aplikacje za pomocą tego samego katalogu klucza można udostępniać ładunków tak długo, jak ich [cel parametry](xref:security/data-protection/consumer-apis/purpose-strings) zgodne.

[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) Konstruktor akceptuje konfiguracji opcjonalnej wywołania zwrotnego, który można dostosować zachowania systemu. Poniższy przykład przedstawia przywracania izolacji z jawnym wywołaniem [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname). W przykładzie pokazano także, konfigurowanie systemu w celu automatycznego szyfrowania kluczy utrwalonego przy użyciu interfejsu DPAPI systemu Windows. Jeśli katalog wskazuje udziału UNC, warto zapoznać się z dystrybuowanie udostępnionego certyfikatu we wszystkich odpowiednich maszyn i skonfiguruj system szyfrowania opartego na certyfikatach w wyniku wywołania [ProtectKeysWithCertificate](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.protectkeyswithcertificate).

[!code-none[](non-di-scenarios/_static/nodisample2.cs)]

> [!TIP]
> Wystąpienia `DataProtectionProvider` konkretnego typu są kosztowne. Jeśli aplikacja obsługuje wiele wystąpień tego typu, a wszystkie korzysta z tego samego katalogu magazynu kluczy, może obniżyć wydajność aplikacji. Jeśli używasz `DataProtectionProvider` typu, zaleca się tworzenia tego typu raz, a następnie użyć możliwie go ponownie. `DataProtectionProvider` Typu i wszystkie [interfejsu IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) wystąpienia utworzone na podstawie jego są wątkowo dla wielu wywołań.
