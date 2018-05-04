---
title: 用于 SQL Server 的功能的 Microsoft JDBC Driver 的依赖关系 |Microsoft 文档
ms.custom: ''
ms.date: 02/28/2018
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
ms.openlocfilehash: 052628258ae1d8c1f31430ea132ed594a976be98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 的功能依赖关系
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 此页包含的 Microsoft JDBC Driver for SQL Server 依赖于的库的列表。 该项目包含以下依赖关系。
 
 ## <a name="compile-time"></a>编译时间
 - `azure-keyvault` ： 始终加密 Azure 密钥保管库功能 （可选） 的 azure 密钥保管库提供程序
 - `adal4j` ： 适用于 Java 的 Azure Active Directory 身份验证功能和 Azure 密钥保管库功能 （可选） azure 与 active Directory 库

 ##  <a name="test-time"></a>测试时间
需要其中的上述两个功能的特定项目需要显式声明其 pom 文件中的相应依赖关系：

***例如：***如果你使用*Azure Active Directory 身份验证功能*，则需要重新声明*adal4j*中项目的 pom 文件依赖关系。 请参阅下面的代码段： 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***例如：***如果你使用*Azure 密钥保管库功能*则需要重新声明*azure keyvault*依赖项和*adal4j*中的依赖关系你项目的 pom 文件。 请参阅下面的代码段： 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 驱动程序的依赖关系要求

 ### <a name="azure-keyvault-feature"></a>Azure Keyvault 功能：
- JDBC 驱动程序版本 6.0.0 
    - 依赖项版本： Azure Keyvault （0.9.7 版）、 Adal4j （版本 1.3.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- JDBC 驱动程序版本 6.2.2 和更高版本 （包括最新 6.4.0）
    - 依赖项版本： Azure Keyvault （版本 1.0.0）、 Adal4j （版本 1.4.0），以及其依赖项 ([示例应用程序](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   截至 v6.2.2，azure keyvault java 依赖项更新为版本 1.0.0。 但是，新的版本不兼容的以前的版本 （0.9.7 版），并因此中断驱动程序中的现有实现。 驱动程序中的新实现需要反过来中断使用 Azure 密钥保管库功能的客户端程序的 API 更改。

  
 ### <a name="azure-active-directory-authentication"></a>Azure Active Directory 身份验证：
- JDBC 驱动程序版本 6.0.0 
    - 依赖项版本： Adal4j （版本 1.3.0），以及其依赖关系
        - 在此版本的驱动程序，你可以连接使用*ActiveDirectoryIntegrated*仅在 Windows 操作系统并使用 SQL Server （sqljdbc_auth.dll 和 Active Directory 身份验证库上的身份验证模式ADALSQL。DLL)。 
- JDBC 驱动程序版本 6.4.0
    - 依赖项版本： Adal4j （版本 1.4.0） 及其依赖项
        - 在此版本的驱动程序，你的应用程序不需要使用 ADALSQL。DLL。 具体取决于操作系统。 有关**非 Windows 操作系统**，驱动程序需要使用 Kerberos 票证，以进行 ActiveDirectoryIntegrated 身份验证。 请参阅[Windows、 Linux 和 Mac 上的设置的 Kerberos 票证](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)有关详细信息。 有关**Windows 操作系统**，默认情况下的驱动程序检查是否 sqljdbc_auth.dll 是加载，并且不需要 Kerberos 票证安装程序或 adal4j 依赖项。 但是，如果未加载 sqljdbc_auth.dll，驱动程序的行为与非 Windows 操作系统相同的方式，并且需要安装程序，在下面的示例所述： 使用此功能的示例应用程序可以找到[此处](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md).

 ## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 GitHub 存储库](https://github.com/microsoft/mssql-jdbc)  
 [JDBC 驱动程序 API 参考](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  