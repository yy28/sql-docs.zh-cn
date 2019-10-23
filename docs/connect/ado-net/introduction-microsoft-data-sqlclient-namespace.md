---
title: Microsoft.Data.SqlClient 命名空间简介
description: SqlClient 命名空间的简介页。
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452379"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空间简介

![Download-DownArrow-Circled](../../ssdt/media/download.png)[下载 ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

本页介绍 SqlClient 命名空间如何通过现有 SqlClient 命名空间提供附加功能。
  
## <a name="release-notes"></a>发行说明
[GitHub 存储库](https://github.com/dotnet/SqlClient/tree/master/release-notes)中提供了所有发行说明。

## <a name="new-features"></a>新增功能

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>.NET Framework 4.7.2. SqlClient 上的新功能

数据分类-Azure SQL 数据库中提供的数据分类和自 2019 2.0 以来的 Microsoft SQL Server。

UTF-8 支持-可从 CTP 2.3 Microsoft SQL Server SQL Server 2019。

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>.NET Core 2.2 SqlClient 上的新功能

数据分类-Azure SQL 数据库中提供的数据分类和自 2019 2.0 以来的 Microsoft SQL Server。

UTF-8 支持-可从 CTP 2.3 Microsoft SQL Server SQL Server 2019。

Microsoft SQL Server 2016 和更高版本中提供了具有 Enclaves Always Encrypted 的 Always Encrypted。 Microsoft Sql Server 2019 CTP 2.0 中引入了 Enclave 支持。

身份验证-Active Directory 密码身份验证模式。

### <a name="data-classification"></a>数据分类

数据分类引入了一组新的 Api，该 Api 公开了只读数据敏感度和有关通过 SqlDataReader 检索的对象的分类信息。 [分类](../../relational-databases/security/sql-data-discovery-and-classification.md)。

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

UTF-8 支持无需更改任何应用程序代码。 当服务器支持 UTF-8 且基础列排序规则为 UTF-8 时，这些 SqlClient 更改只会优化客户端与服务器之间的通信。 请参阅[SQL Server 2019 预览版的新增功能中](../../sql-server/what-s-new-in-sql-server-ver15.md)的 utf-8 部分。

### <a name="always-encrypted-with-enclaves"></a>始终用 enclaves 加密

通常，在 .NET Framework**和内置列主密钥存储提供程序**上使用 SqlClient 的现有文档也应该适用于 .net Core。

 [配合使用 Always Encrypted 和 .NET Framework 数据提供程序进行开发](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保护敏感数据并将加密密钥存储在 Windows 证书存储中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>身份验证

可以通过使用_身份验证_连接字符串选项来指定不同的身份验证模式。 有关详细信息，请参阅[SqlAuthenticationMethod 的文档](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)。

> [!NOTE]
> 自定义密钥存储提供程序（如 Azure Key Vault 提供程序）将需要更新以支持 SqlClient。 同样，还需要更新 enclave 提供程序以支持 SqlClient。
> 仅支持 .NET Framework 和 .NET Core 目标 Always Encrypted。 不支持 .NET Standard，因为 .NET Standard 缺少某些加密依赖项。
