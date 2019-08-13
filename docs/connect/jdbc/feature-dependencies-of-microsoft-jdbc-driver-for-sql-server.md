---
title: Microsoft JDBC Driver for SQL Server 的功能依赖项 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26395c7a925906e7b27d4e47098164019e56f31d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893955"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能依赖项

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文列出了 Microsoft JDBC Driver for SQL Server 所依赖的库。 项目具有以下依赖项。

## <a name="compile-time"></a>编译时间

 - `com.microsoft.azure:azure-keyvault`：具有 Always Encrypted Azure Key Vault 功能的 Azure Key Vault 提供程序（可选）
 - `com.microsoft.azure:adal4j`：具有 Azure Active Directory 身份验证功能和 Azure Key Vault 功能的用于 Java 的 Azure Active Directory 库（可选）
 - `com.microsoft.rest:client-runtime`：具有 Azure Active Directory 身份验证功能和 Azure Key Vault 功能的用于 Java 的 Azure Active Directory 库（可选）
 - `org.antlr:antlr4-runtime`: 用于 useFmtOnly 的 ANTLR 4 运行时功能 (可选)
 - `org.osgi:org.osgi.core`：具有 OSGi Framework 支持的 OSGi Core 库。
 - `org.osgi:org.osgi.compendium`：具有 OSGi Framework 支持的 OSGi Compendium 库。

## <a name="test-time"></a>测试时间

需要任何上述功能的特定项目需要显式声明其 POM 文件中的相应依赖项。

例如  ：时要使用 Azure Active Directory 身份验证功能，需要重新声明`adal4j`项目的 POM 文件中的依赖关系。 请查看以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>
```

例如  ：时要使用 Azure 密钥保管库功能，需要重新声明`azure-keyvault`依赖关系和`adal4j`项目的 POM 文件中的依赖关系。 请查看以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC Driver 的依赖项要求

### <a name="working-with-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供程序：

- JDBC Driver 版本 7.4.1 - 依赖项版本：Azure-Keyvault（版本 1.2.1）、Adal4j（版本 1.6.4）、Client-Runtime-for-AutoRest (1.6.10) 及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-7.0.md)）
- JDBC 驱动程序版本 7.2.2 - 依赖项版本：Azure-Keyvault（版本 1.2.0）、Azure-Keyvault-Webkey（版本 1.2.0）、Adal4j（版本 1.6.3）、Client-Runtime-for-AutoRest (1.6.5) 及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-7.0.md)）
- JDBC 驱动程序版本 7.0.0 - 依赖项版本：Azure-Keyvault（版本 1.0.0）、Adal4j（版本 1.6.0）及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-7.0.md)）
- JDBC 驱动程序版本 6.4.0 - 依赖项版本：Azure-Keyvault（版本 1.0.0）、Adal4j（版本 1.4.0）及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md)）
- JDBC 驱动程序版本 6.2.2 - 依赖项版本：Azure-Keyvault（版本 1.0.0）、Adal4j（版本 1.4.0）及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md)）
- JDBC 驱动程序版本 6.0.0 - 依赖项版本：Azure-Keyvault（版本 0.9.7）、Adal4j（版本 1.3.0）及其依赖项（[示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md)）

> [!NOTE]
> 使用 6.2.2 和 6.4.0 驱动程序版本，azure-keyvault-java 依赖项已更新为版本 1.0.0。 但是，新版本与上一版本 (0.9.7) 不兼容，并且会中断驱动程序中的现有实现。 驱动程序中的新实现需要 API 更改，因而会中断使用 Azure Key Vault 提供程序的客户端程序。
>
> 最新驱动程序版本（7.0.0 以后）可解决此问题。 使用了身份验证回调机制的已删除构造函数将重新添加到 Azure Key Vault 提供程序以进行向后兼容。

### <a name="working-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证：

- JDBC Driver 版本 7.4.1 - 依赖项版本：Adal4j（版本 1.6.4）、Client-Runtime-for-AutoRest (1.6.10) 及其依赖项
- JDBC 驱动程序版本 7.2.2 - 依赖项版本：Adal4j（版本 1.6.3）、Client-Runtime-for-AutoRest (1.6.5) 及其依赖项
- JDBC 驱动程序版本 7.0.0 - 依赖项版本：Adal4j（版本 1.6.0）及其依赖项
- JDBC 驱动程序版本 6.4.0 - 依赖项版本：Adal4j（版本 1.4.0）及其依赖项
- JDBC 驱动程序版本 6.2.2 - 依赖项版本：Adal4j（版本 1.4.0）及其依赖项
- JDBC 驱动程序版本 6.0.0 - 依赖项版本：Adal4j（版本 1.3.0）及其依赖项。 在此版本的驱动程序中，可以仅在 Windows 操作系统上使用 ActiveDirectoryIntegrated  身份验证模式并使用 sqljdbc_auth.dll 和适用于 SQL Server 的 Active Directory 身份验证库 (ADALSQL.DLL) 进行连接。

从驱动程序版本 6.4.0 开始，应用程序不一定需要在 Windows 操作系统上使用 ADALSQL.DLL。 对于非 Windows 操作系统  ，驱动程序需要使用 Kerberos 票证才能进行 ActiveDirectoryIntegrated 身份验证。 有关如何使用 Kerberos 连接到 Active Directory 的详细信息，请参阅[在 Windows、Linux 和 Mac 上设置 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)。

对于 Windows 操作系统  ，驱动程序默认查找 sqljdbc_auth.dll，并且不需要 Kerberos 票证设置或 Azure 库依赖项。 如果 sqljdbc_auth.dll 不可用，驱动程序会查找用于在其他操作系统上对 Active Directory 进行身份验证的 Kerberos 票证。

可以获取使用此功能的[示例应用程序](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序 GitHub 存储库](https://github.com/microsoft/mssql-jdbc)  
[JDBC Driver API 参考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
