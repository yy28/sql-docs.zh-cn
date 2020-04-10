---
title: Microsoft.Data.SqlClient 命名空间简介
description: Microsoft.Data.SqlClient 命名空间的简介页面。
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 9a5f787e9cd95e3d2966e5bc2b722aada5b97032
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928999"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空间简介

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Microsoft.Data.SqlClient 1.1.0 的发行说明

GitHub 存储库中也提供了发行说明：[1.1 发行说明](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1)。

### <a name="new-features"></a>新功能

#### <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

从 Microsoft SQL Server 2016 开始，提供 Always Encrypted。 从 Microsoft SQL Server 2019 开始，提供安全 enclave。 为了使用 enclave 功能，连接字符串应包括所需的证明协议和证明 URL。 示例：

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

有关详细信息，请参阅：

- [对 Always Encrypted 的 SqlClient 支持](sql/sqlclient-support-always-encrypted.md)
- [教程：使用具有安全 enclave 的 Always Encrypted 开发 .NET 应用程序](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Microsoft.Data.SqlClient 1.0 的发行说明

Microsoft.Data.SqlClient 命名空间的初始版本提供了现有 System.Data.SqlClient 命名空间之外的其他功能。
GitHub 存储库中也提供了发行说明：[1.0 发行说明](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0)。

### <a name="new-features"></a>新增功能

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>通过 .NET Framework 4.7.2 System.Data.SqlClient 提供的新增功能

- **数据分类** - 在 Azure SQL 数据库和 Microsoft SQL Server 2019 中提供。

- **UTF-8 支持** - 在 Microsoft SQL Server 2019 中提供。

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>通过 .NET Core 2.2 System.Data.SqlClient 提供的新增功能

- **数据分类** - 在 Azure SQL 数据库和 Microsoft SQL Server 2019 中提供。

- **UTF-8 支持** - 在 Microsoft SQL Server 2019 中提供。

- **身份验证** - Active Directory 密码身份验证模式。

### <a name="data-classification"></a>数据分类

当基础源支持该功能并包含有关[数据敏感度和分类](../../relational-databases/security/sql-data-discovery-and-classification.md)的元数据时，数据分类会引入一组新的 API，公开有关通过 SqlDataReader 检索到的对象的只读数据敏感度和分类信息。

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>UTF-8 支持

UTF-8 支持不需要更改任何应用程序代码。 当服务器支持 UTF-8 且基础列排序规则为 UTF-8 时，这些 SqlClient 更改只会优化客户端与服务器之间的通信。 请参阅 [SQL Server 2019 预览版的新增功能](../../sql-server/what-s-new-in-sql-server-ver15.md)中的 UTF-8 部分。

### <a name="always-encrypted-with-enclaves"></a>具有 enclave 的 Always Encrypted

通常，使用 .NET Framework 上的 System.Data.SqlClient 和内置列主密钥存储提供程序  的现有文档现在还应与 .NET Core 一起使用。

 [配合使用 Always Encrypted 和 .NET Framework 数据提供程序进行开发](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保护敏感数据并将加密密钥存储在 Windows 证书存储中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>身份验证

可以使用“身份验证”  连接字符串选项来指定不同的身份验证模式。 有关详细信息，请参阅 [SqlAuthenticationMethod 的文档](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)。

> [!NOTE]
> 自定义密钥存储提供程序（如 Azure 密钥保管库提供程序）将需要更新以支持 Microsoft.Data.SqlClient。 同样，还需要更新 enclave 提供程序以支持 Microsoft.Data.SqlClient。
> 仅 .NET Framework 和 .NET Core 目标支持 Always Encrypted。 .NET Standard 不支持 Always Encrypted，因为 .NET Standard 缺少某些加密依赖项。
