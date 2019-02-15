---
title: Microsoft JDBC Driver for SQL Server 的功能依赖项 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9d9fea0f211809fd65b65459d50daa7a85db88
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736948"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能依赖项

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文列出了 Microsoft JDBC Driver for SQL Server 依赖于的库。 项目具有以下依赖项。

## <a name="compile-time"></a>编译时间

 - `com.microsoft.azure:azure-keyvault`设置用户帐户 ：（可选） 的 Always Encrypted Azure 密钥保管库功能的 azure 密钥保管库提供程序
 - `com.microsoft.azure:azure-keyvault-webkey`设置用户帐户 ：（可选） 的 Always Encrypted Azure 密钥保管库功能的 azure 密钥保管库提供程序
 - `com.microsoft.azure:adal4j`设置用户帐户 ：Azure Active Directory 身份验证功能和 Azure 密钥保管库功能 （可选） 用于 Java 的 azure Active Directory 库
 - `com.microsoft.rest:client-runtime`设置用户帐户 ：Azure Active Directory 身份验证功能和 Azure 密钥保管库功能 （可选） 用于 Java 的 azure Active Directory 库
- `org.osgi:org.osgi.core`设置用户帐户 ：OSGi Framework 支持的 OSGi 核心库。
- `org.osgi:org.osgi.compendium`设置用户帐户 ：OSGi Framework 支持的 OSGi 提要库。

## <a name="test-time"></a>测试时间

需要其中的上述功能的特定项目需要显式声明其 POM 文件中的相应依赖项。

例如：时要使用 Azure Active Directory 身份验证功能，需要重新声明`adal4j`项目的 POM 文件中的依赖关系。 请参阅以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.0.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

例如：时要使用 Azure 密钥保管库功能，需要重新声明`azure-keyvault`依赖关系和`adal4j`项目的 POM 文件中的依赖关系。 请参阅以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.0.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC Driver 的依赖项要求

### <a name="working-with-the-azure-key-vault-provider"></a>使用 Azure 密钥保管库提供程序：

- JDBC 驱动程序版本 7.2.0-依赖项版本：Azure 密钥保管库 （版本 1.2.0）、 Azure 密钥保管库 Webkey （版本 1.2.0）、 Adal4j （版本 1.6.3），客户端的运行时-为-AutoRest (1.6.5)，以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample.md))
- JDBC 驱动程序版本 7.0.0-依赖项版本：Azure key Vault （版本 1.0.0），Adal4j （版本 1.6.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample.md))
- JDBC 驱动程序版本 6.4.0-依赖项版本：Azure key Vault （版本 1.0.0），Adal4j （版本 1.4.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驱动程序版本 6.2.2-依赖项版本：Azure key Vault （版本 1.0.0），Adal4j （版本 1.4.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驱动程序版本 6.0.0-依赖项版本：Azure key Vault （0.9.7 版），Adal4j （版本 1.3.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> 6.2.2 和 6.4.0 驱动程序版本中，azure 密钥保管库 java 依赖项具有已更新到版本 1.0.0。 但是，新版本不是与以前的版本 (0.9.7) 兼容，并且在驱动程序将中断现有的实现。 驱动程序中的新实现所需 API 更改，这反过来会中断客户端程序的使用 Azure 密钥保管库提供程序。
>
> 此问题得到解决与最新驱动程序版本 (7.0.0)。 已删除构造函数使用的身份验证回调机制添加回 Azure 密钥保管库提供程序的向后兼容性。

### <a name="working-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证：

- JDBC 驱动程序版本 7.2.0-依赖项版本：Adal4j （版本 1.6.3），客户端的运行时-为-AutoRest (1.6.5)，以及其依赖项
- JDBC 驱动程序版本 7.0.0-依赖项版本：Adal4j （版本 1.6.0） 及其依赖项
- JDBC 驱动程序版本 6.4.0-依赖项版本：Adal4j （版本 1.4.0） 及其依赖项
- JDBC 驱动程序版本 6.2.2-依赖项版本：Adal4j （版本 1.4.0） 及其依赖项
- JDBC 驱动程序版本 6.0.0-依赖项版本：Adal4j （版本 1.3.0） 及其依赖项。 在此版本的驱动程序，您可以使用连接_ActiveDirectoryIntegrated_身份验证模式仅在 Windows 操作系统上，通过使用针对 SQL Server （sqljdbc_auth.dll 和 Active Directory 身份验证库ADALSQL。DLL)。

从驱动程序版本 6.4.0 以后，应用程序不一定需要使用 ADALSQL。在 Windows 操作系统上的 DLL。 有关*非 Windows 操作系统*，驱动程序需要使用 ActiveDirectoryIntegrated 身份验证的 Kerberos 票证。 有关如何通过使用 Kerberos 连接到 Active Directory 的详细信息，请参阅[Windows、 Linux 和 Mac 上的设置 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)。

有关*Windows 操作系统*，驱动程序默认情况下查找 sqljdbc_auth.dll 并不需要 Kerberos 票证设置或 Azure 库依赖项。 如果 sqljdbc_auth.dll 不可用，驱动程序查找进行其他操作系统上的 Active Directory 作为身份验证的 Kerberos 票证。

可以获取[示例应用程序](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)，它使用此功能。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序 GitHub 存储库](https://github.com/microsoft/mssql-jdbc)  
 [JDBC Driver API 参考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
