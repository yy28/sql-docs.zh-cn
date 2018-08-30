---
title: JDBC 驱动程序的系统要求 |Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 377afbebe029add867a2d02cb02a38421dc8d1f2
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783992"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 驱动程序的系统要求
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 或 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 中的数据，计算机上必须安装有下列组件：

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]（[下载](download-microsoft-jdbc-driver-for-sql-server.md)）
- Java 运行时环境

## <a name="java-runtime-environment-requirements"></a>Java 运行时环境要求  
 自 Microsoft JDBC Driver 7.0 for SQL Server 起，Sun Java SE 开发工具包 (JDK) 10.0 和 Java Runtime Environment (JRE) 10.0 均受支持。

 从 Microsoft JDBC Driver 6.4 for SQL Server 开始，Sun Java SE 开发工具包 (JDK) 9.0 和 Java Runtime Environment (JRE) 9.0 均受支持。

 从 Microsoft JDBC Driver 4.2 for SQL Server 开始，Sun Java SE 开发工具包 (JDK) 8.0 和 Java Runtime Environment (JRE) 8.0 均受支持。 对 Java Database Connectivity (JDBC) 规范 API 的支持已扩展为包含 JDBC 4.1 和 4.2 API。  
  
 从 Microsoft JDBC Driver 4.1 for SQL Server 开始，Sun Java SE 开发工具包 (JDK) 7.0 和 Java Runtime Environment (JRE) 7.0 均受支持。  
  
 从 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 开始，Java 数据库连接 (JDBC) 规范 API 的JDBC 驱动程序支持扩展为包括 JDBC 4.0 API。 JDBC 4.0 API 是作为 Sun Java SE 开发工具包 (JDK) 6.0 和 Java 运行时环境 (JRE) 6.0 的一部分引入的。 JDBC 4.0 是 JDBC 3.0 API 的超集。  
  
 当你在 Windows 和 UNIX 操作系统上部署 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，你必须分别使用安装包 sqljdbc_\<version>_enu.exe 和 sqljdbc_\<version>_enu.tar.gz。 有关如何部署 JDBC 驱动程序的详细信息，请参阅[中部署 JDBC 驱动程序](../../connect/jdbc/deploying-the-jdbc-driver.md)主题。  
  
**Microsoft JDBC Driver 7.0 for SQL Server：**  

  JDBC Driver 6.2 在每个安装包中包含两个 JAR 类库：mssql-jdbc-6.2.2.jre7.jar 和 mssql-jdbc-6.2.2.jre8.jar。

  JDBC Driver 7.0 旨在用于所有主要 Sun 等效 Java 虚拟机并受其支持，但仅在 Sun JRE 8.0 和 10.0 上经过测试。
  
  下面概述了 Microsoft JDBC Driver 7.0 for SQL Server 附带的两个 JAR 文件提供的支持：  
  
  |JAR|JDBC 版本法规遵从性|推荐的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低，则会引发异常。<br /><br /> 在 7.0 中的新功能包括： JDK 10 支持、 JDBC 4.2 规范、 空间数据类型支持、 cancelQueryTimeout 连接属性、 边界请求方法、 useBulkCopyForBatchInsert 连接属性，数据的更新的默认符合性级别发现和分类的信息、 utf-8 功能扩展和 CityHash 支持。 |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|需要 Java Runtime Environment (JRE) 10.0。 使用 JRE 9.0 或更低，则会引发异常。<br /><br /> 在 7.0 中的新功能包括： JDK 10 支持、 JDBC 4.2 规范、 空间数据类型支持、 cancelQueryTimeout 连接属性、 边界请求方法、 useBulkCopyForBatchInsert 连接属性，数据的更新的默认符合性级别发现和分类的信息、 utf-8 功能扩展和 CityHash 支持。 |    


  JDBC 驱动程序 7.0 还在 Maven 中央存储库上可用，并且在可以通过在 POM 中添加以下代码添加到 Maven 项目。XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```      
  
**Microsoft JDBC Driver 6.4 for SQL Server：**  

  JDBC Driver 6.2 在每个安装包中包含两个 JAR 类库：mssql-jdbc-6.2.2.jre7.jar 和 mssql-jdbc-6.2.2.jre8.jar。

  JDBC Driver 6.4 旨在与所有主要的 Sun 等效 Java 虚拟机兼容并受其支持，但仅在 Sun JRE 7.0、8.0 和 9.0 上进行测试。
  
  下面概述了由 Microsoft JDBC Driver 6.4 for SQL Server 附带的三个 JAR 文件提供的支持：  
  
  |JAR|JDBC 版本法规遵从性|推荐的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低，则会引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，对于跨域身份验证，Kerberos 约束委派、 查询超时值、 套接字超时自动检测 SPN 中领域的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低，则会引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，对于跨域身份验证，Kerberos 约束委派、 查询超时值、 套接字超时自动检测 SPN 中领域的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|需要 Java Runtime Environment (JRE) 9.0。 使用 JRE 8.0 或更低，则会引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，对于跨域身份验证，Kerberos 约束委派、 查询超时值、 套接字超时自动检测 SPN 中领域的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |

JDBC Driver 6.4 还在 Maven 中央存储库上可用，并且在可以通过在 POM 中添加以下代码添加到 Maven 项目。XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 for SQL Server：**  
  
  JDBC Driver 6.2 在每个安装包中包含两个 JAR 类库：mssql-jdbc-6.2.2.jre7.jar 和 mssql-jdbc-6.2.2.jre8.jar。 
  
 JDBC Driver 6.2 旨在与所有主要的 Sun 等效 Java 虚拟机兼容并受其支持，但仅在 Sun JRE 5.0、6.0、7.0 和 8.0 上进行测试。
  
 下面概述了由 Microsoft JDBC Driver for SQL Server 6.0 和 4.2 附带的两个 JAR 文件提供的支持：  
  
|JAR|JDBC 版本法规遵从性|推荐的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-6.2.2.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低，则会引发异常。<br /><br /> 6.2 中的新功能包括： 对于 Linux，Kerberos，对于跨域身份验证，Kerberos 约束委派、 查询超时值、 套接字超时自动检测 SPN 中领域的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |  
|mssql jdbc 6.2.3.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低，则会引发异常。<br /><br /> 6.2 中的新功能包括： 对于 Linux，Kerberos，对于跨域身份验证，Kerberos 约束委派、 查询超时值、 套接字超时自动检测 SPN 中领域的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用|    

  JDBC Driver 6.2 还在 Maven 中央存储库上可用，并且在可以通过在 POM 中添加以下代码添加到 Maven 项目。XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 and 4.2 for SQL Server：**  
  
  JDBC 驱动程序 6.0 和 4.2 在每个安装包中包括两个 JAR 类库： **sqljdbc41.jar**，并**sqljdbc42.jar**。 
  
 JDBC Drivers 6.0 和 4.2 旨在与所有主要的 Sun 等效 Java 虚拟机兼容并受其支持，但仅在 Sun JRE 5.0、6.0、7.0 和 8.0 上进行测试。 
  
 下面概述了由 Microsoft JDBC Driver for SQL Server 6.0 和 4.2 附带的两个 JAR 文件提供的支持：  
  
|JAR|JDBC 版本法规遵从性|推荐的 Java 版本|描述|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低，则会引发异常。<br /><br /> 6.0 和 4.2 程序包中的新功能包括：JDBC 4.1 合规性和大容量复制<br /><br /> 此外，6.0 程序包独有中的新增功能包括： 始终加密，表值参数，Azure Active Directory 身份验证，准备好透明连接到 Alwayson 可用性组中的参数元数据检索的改进查询和国际化域名 (IDN)|  
|sqljdbc42.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低，则会引发异常。<br /><br /> 6.0 和 4.2 程序包中的新功能包括：JDBC 4.1 合规性、JDBC 4.2 合规性和大容量复制<br /><br /> 此外，6.0 程序包独有中的新增功能包括： 始终加密，表值参数，Azure Active Directory 身份验证，准备好透明连接到 Alwayson 可用性组中的参数元数据检索的改进查询和国际化域名 (IDN)|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server：**  
  
 JDBC Driver 4.1 在每个安装包中包括一个 JAR 类库： **sqljdbc41.jar**。  
    
|JAR|描述|  
|---------|-----------------|  
|sqljdbc41.jar|sqljdbc41.jar 类库提供对 JDBC 4.0 API 的支持。 它包含 JDBC 4.0 驱动程序的所有功能以及 JDBC 4.0 API 方法。 JDBC 4.1 不受支持（将引发异常“SQLFeatureNotSupportedException”）。<br /><br /> sqljdbc41.jar 类库要求使用 Java Runtime Environment (JRE) 7.0。 使用**sqljdbc41.jar** JRE 6.0 和 5.0 将引发异常。<br /><br /> 
  
 JDBC 驱动程序设计为与所有主要的 Sun 等效 Java 虚拟机一起工作并受这些虚拟机的支持，但它是在 Sun JRE 5.0、6.0 和 7.0 上进行测试的。  
  
 下面概述了由 Microsoft JDBC Driver 4.1 for SQL Server 附带的 JAR 文件提供的支持。  
  
|JAR|JDBC 版本|JRE（可以运行）|JDK（可以编译）|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 要求  
 JDBC 驱动程序支持连接到 Azure SQL Database 和 SQL Server。 对于适用于 SQL Server 的 Microsoft JDBC Driver 4.2 和 4.1，该支持从 SQL Server 2008 开始。
  
## <a name="operating-system-requirements"></a>操作系统要求  
 JDBC 驱动程序可在任何支持使用 Java 虚拟机 (JVM) 的操作系统上工作。 但是，只有 Sun Solaris、SUSE Linux 以及 Windows 操作系统经过了官方测试。  
  
## <a name="supported-languages"></a>支持的语言  
 JDBC 驱动程序支持所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列排序规则。 有关 JDBC 驱动程序支持的排序规则的详细信息，请参阅[JDBC 驱动程序的国际化功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)。  
  
 有关排序规则的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“使用排序规则”。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
