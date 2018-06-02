---
title: JDBC 驱动程序的系统要求 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
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
ms.openlocfilehash: 306c7bcd764ed70f23c51667580fb9f8e79f0e65
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34563945"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>JDBC 驱动程序的系统要求
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  从访问数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，你必须在计算机上安装以下组件：

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([下载](download-microsoft-jdbc-driver-for-sql-server.md))
- Java 运行时环境

## <a name="java-runtime-environment-requirements"></a>Java 运行时环境要求  
 SQL Server 的 Microsoft JDBC 驱动程序 6.4 从开始，Sun Java SE 开发工具包 (JDK) 9.0 和 Java Runtime Environment (JRE) 9.0 支持。

 从 Microsoft JDBC Driver 4.2 for SQL Server 开始，Sun Java SE 开发工具包 (JDK) 8.0 和 Java Runtime Environment (JRE) 8.0 均受支持。 对 Java Database Connectivity (JDBC) 规范 API 的支持已扩展为包含 JDBC 4.1 和 4.2 API。  
  
 从 Microsoft JDBC Driver 4.1 for SQL Server 开始，Sun Java SE 开发工具包 (JDK) 7.0 和 Java Runtime Environment (JRE) 7.0 均受支持。  
  
 从开始[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，Java 数据库连接 (JDBC) 规范 API 的 JDBC 驱动程序支持已扩展为包括 JDBC 4.0 API。 JDBC 4.0 API 是作为 Sun Java SE 开发工具包 (JDK) 6.0 和 Java 运行时环境 (JRE) 6.0 的一部分引入的。 JDBC 4.0 是 JDBC 3.0 API 的超集。  
  
 当部署[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]必须在 Windows 和 UNIX 操作系统上使用的安装程序包， *sqljdbc_\<版本 > _enu.exe*，和*sqljdbc_\<版本 > _enu.tar.gz*分别。 有关如何部署 JDBC 驱动程序的详细信息，请参阅[部署 JDBC 驱动程序](../../connect/jdbc/deploying-the-jdbc-driver.md)主题。  
  
**Microsoft JDBC Driver 6.4 for SQL Server:**  

  JDBC 驱动程序 6.4 中每个安装包包括三个 JAR 类库： **mssql jdbc 6.4.0.jre7.jar**， **mssql jdbc 6.4.0.jre8.jar**，和**mssql jdbc 6.4.0.jre9.jar**.

  JDBC 驱动程序 6.4 旨在处理并支持所有主要 Sun 等效 Java 虚拟机，但仅在 Sun JRE 7.0、 8.0 和 9.0 上测试。
  
  下面汇总了 SQL Server 的 Microsoft JDBC 驱动程序 6.4 中包含的三个 JAR 文件提供支持：  
  
  |JAR|JDBC 版本法规遵从性|推荐的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低将引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，自动检测 SPN 中领域的跨域身份验证，Kerberos 约束委派，查询超时值，套接字超时的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低将引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，自动检测 SPN 中领域的跨域身份验证，Kerberos 约束委派，查询超时值，套接字超时的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|需要 Java 运行时环境 (JRE) 9.0。 使用 JRE 8.0 或更低将引发异常。<br /><br /> 6.4 中的新功能包括： 对于 Linux，Kerberos，自动检测 SPN 中领域的跨域身份验证，Kerberos 约束委派，查询超时值，套接字超时的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |    


  JDBC 驱动程序 6.4 还 Maven 中央存储库上可用，并且在可以通过在 POM 中添加以下代码添加到 Maven 项目。XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```    
**Microsoft JDBC Driver 6.2 for SQL Server:**  
  
  JDBC 驱动程序 6.2 在每个安装包中包含两个 JAR 类库： **mssql jdbc 6.2.1.jre7.jar**，和**mssql jdbc 6.2.1.jre8.jar**。 
  
 JDBC 驱动程序 6.2 旨在处理并支持所有主要 Sun 等效 Java 虚拟机，但仅在 Sun JRE 5.0、 6.0、 7.0 和 8.0 上测试。 
  
 下面汇总了包含与 Microsoft JDBC 驱动程序 6.0 和 4.2 for SQL Server 的两个 JAR 文件提供支持：  
  
|JAR|JDBC 版本法规遵从性|推荐的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.2.1.jre7.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低将引发异常。<br /><br /> 6.2 中的新功能包括： 对于 Linux，Kerberos，自动检测 SPN 中领域的跨域身份验证，Kerberos 约束委派，查询超时值，套接字超时的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用。 |  
|mssql-jdbc-6.2.1.jre8.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低将引发异常。<br /><br /> 6.2 中的新功能包括： 对于 Linux，Kerberos，自动检测 SPN 中领域的跨域身份验证，Kerberos 约束委派，查询超时值，套接字超时的主体/密码方法的 Azure AD 身份验证和已准备好语句句柄重复使用|    

  JDBC 驱动程序 6.2 还 Maven 中央存储库上可用，并且在可以通过在 POM 中添加以下代码添加到 Maven 项目。XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 和 4.2 for SQL Server:**  
  
  JDBC 驱动程序 6.0 和 4.2 每个安装包中包括两个 JAR 类库： **sqljdbc41.jar**，和**sqljdbc42.jar**。 
  
 JDBC 驱动程序 6.0 和 4.2 旨在处理并支持所有主要 Sun 等效 Java 虚拟机，但仅在 Sun JRE 5.0、 6.0、 7.0 和 8.0 上测试。 
  
 下面汇总了包含与 Microsoft JDBC 驱动程序 6.0 和 4.2 for SQL Server 的两个 JAR 文件提供支持：  
  
|JAR|JDBC 版本法规遵从性|推荐的 Java 版本|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|需要 Java Runtime Environment (JRE) 7.0。 使用 JRE 6.0 或更低将引发异常。<br /><br /> 6.0 和 4.2 程序包中的新功能包括：JDBC 4.1 合规性和大容量复制<br /><br /> 此外，仅 6.0 包中的新功能包括： 始终加密，表值参数，Azure Active Directory 身份验证，Alwayson 可用性组，改善中的参数元数据检索到的透明连接准备查询和国际化域名 (IDN)|  
|sqljdbc42.jar|4.2|8|需要 Java Runtime Environment (JRE) 8.0。 使用 JRE 7.0 或更低将引发异常。<br /><br /> 6.0 和 4.2 程序包中的新功能包括：JDBC 4.1 合规性、JDBC 4.2 合规性和大容量复制<br /><br /> 此外，仅 6.0 包中的新功能包括： 始终加密，表值参数，Azure Active Directory 身份验证，Alwayson 可用性组，改善中的参数元数据检索到的透明连接准备查询和国际化域名 (IDN)|  
  
 **Microsoft JDBC Driver 4.1 for SQL Server:**  
  
 JDBC Driver 4.1 中每个安装包包括一个 JAR 类库： **sqljdbc41.jar**。  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.jar**类库提供了对 JDBC 4.0 API 的支持。 它包括的所有功能的 JDBC 4.0 驱动程序，以及 JDBC 4.0 API 方法。 不支持 JDBC 4.1 （引发异常"SQLFeatureNotSupportedException"）。<br /><br /> **sqljdbc41.jar**类库需要 Java Runtime Environment (JRE) 7.0。 使用**sqljdbc41.jar** JRE 6.0 和 5.0 将引发异常。<br /><br /> 
  
 JDBC 驱动程序旨在使用和支持所有主要 Sun 等效 Java 虚拟机，但在 Sun JRE 5.0，6.0 和 7.0 上测试。  
  
 下面汇总了包括 Microsoft JDBC Driver 4.1 for SQL Server 的 JAR 文件提供支持。  
  
|JAR|JDBC 版本|JRE（可以运行）|JDK（可以编译）|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>SQL Server 要求  
 JDBC 驱动程序支持连接到 Azure SQL 数据库和 SQL Server。 对于适用于 SQL Server 的 Microsoft JDBC Driver 4.2 和 4.1，该支持从 SQL Server 2008 开始。
  
## <a name="operating-system-requirements"></a>操作系统要求  
 JDBC 驱动程序可在任何支持使用 Java 虚拟机 (JVM) 的操作系统上工作。 但是，只有 Sun Solaris、SUSE Linux 以及 Windows 操作系统经过了官方测试。  
  
## <a name="supported-languages"></a>支持的语言  
 JDBC 驱动程序支持所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]列排序规则。 JDBC 驱动程序支持的排序规则的详细信息，请参阅[的 JDBC 驱动程序的国际功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)。  
  
 有关排序规则的详细信息，请参阅"使用排序规则"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
