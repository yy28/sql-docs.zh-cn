---
title: Microsoft JDBC Driver for SQL Server 的功能依赖项 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 57
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70179d55c6aae5fc01c84f0c4af860f86d528a06
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454221"
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能依赖项

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此页列出了下取决于 Microsoft JDBC Driver for SQL Server 的库。 项目具有以下依赖项。

## <a name="compile-time"></a>编译时

- `azure-keyvault`： Always Encrypted Azure 密钥保管库功能 （可选） azure 密钥保管库提供程序
- `adal4j`： 适用于 Java 的 Azure Active Directory 身份验证功能和 Azure 密钥保管库功能 （可选） azure 与 active Directory 库

## <a name="test-time"></a>测试时间

要求任一上述的两个功能的特定项目需要显式声明其 pom 文件中的相应依赖项：

**_例如：_** 使用时_Azure Active Directory 身份验证功能_，则需要重新声明_adal4j_项目的 pom 文件中的依赖关系。 请参阅以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>
```

**_例如：_** 使用时_Azure Key Vault 功能_，则需要重新声明_azure key vault_依赖关系和_adal4j_你的项目的 pom 文件中的依赖关系。 请参阅以下代码片段：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC Driver 的依赖项要求

### <a name="working-with-azure-key-vault-provider"></a>使用 Azure 密钥保管库提供程序：

- JDBC 驱动程序版本 7.0.0-依赖项版本： Azure 密钥保管库 （版本 1.0.0）、 Adal4j （版本 1.6.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-7-0-0.md))
- JDBC 驱动程序版本 6.4.0-依赖项版本： Azure 密钥保管库 （版本 1.0.0）、 Adal4j （版本 1.4.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驱动程序版本 6.2.2-依赖项版本： Azure 密钥保管库 （版本 1.0.0）、 Adal4j （版本 1.4.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC 驱动程序版本 6.0.0-依赖项版本： Azure key Vault （0.9.7 版）、 Adal4j （版本 1.3.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> V6.2.2 和 v6.4.0 驱动程序版本中，azure 密钥保管库 java 依赖项具有已更新到版本 1.0.0。 但是，新版本不可与上一版本 （版本 0.9.7） 兼容，因此驱动程序中将中断现有的实现。 驱动程序中的新实现所需 API 更改，这反过来会中断客户端程序的使用 Azure 密钥保管库提供程序。

> 此问题已得到解决与最新驱动程序版本 v7.0.0，因为已删除的构造函数使用身份验证回调机制重新添加到 Azure 密钥保管库提供程序向后兼容性。

### <a name="working-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 身份验证：

- JDBC 驱动程序版本 7.0.0-依赖项版本： Ada4j （版本 1.6.0） 及其依赖项
- JDBC 驱动程序版本 6.4.0-依赖项版本： Adal4j （版本 1.4.0） 及其依赖项
- JDBC 驱动程序版本 6.2.2-依赖项版本： Adal4j （版本 1.4.0） 及其依赖项
- JDBC 驱动程序版本 6.0.0-依赖项版本： Adal4j （版本 1.3.0），并且其依赖项-在此版本的驱动程序，你可以连接使用_ActiveDirectoryIntegrated_仅在 Windows 操作系统上的身份验证模式并针对 SQL Server (ADALSQL 使用 sqljdbc_auth.dll 和 Active Directory 身份验证库。DLL)。

从驱动程序版本 6.4.0 及更高版本，应用程序不一定需要使用 ADALSQL。在 Windows 操作系统上的 DLL。 有关**非 Windows 操作系统**，驱动程序需要使用 ActiveDirectoryIntegrated 身份验证的 Kerberos 票证。 有关如何连接到使用 Kerberos 的 Active Directory 的详细信息，请参阅[在 Windows、 Linux 和 Mac 上的设置 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)。

有关**Windows 操作系统**，驱动程序默认情况下查找 sqljdbc_auth.dll 并不需要 Kerberos 票证设置或 Azure 库依赖项。 但是，如果 sqljdbc_auth.dll 不可用，驱动程序将寻找对作为其他操作系统上的 Active Directory 进行身份验证的 Kerberos 票证。

使用此功能的示例应用程序可以找到[此处](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序 GitHub 存储库](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 驱动程序 API 参考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
