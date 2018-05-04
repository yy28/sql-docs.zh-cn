---
title: JDBC 驱动程序的国际功能 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e37f04c72e8667b955f0f0ed9974ad8a36400e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="international-features-of-the-jdbc-driver"></a>JDBC 驱动程序的国际功能
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  国际化功能[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]如下：  
  
-   支持的语言相同的语言中的完全本地化体验 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   对敏感区域设置的 Java 语言转换支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据  
  
-   对于国际语言的支持，而不考虑操作系统  
  
-   对国际域名的支持（从 Microsoft JDBC Driver 6.0 for SQL Server 开始）  
  
## <a name="handling-of-character-data"></a>字符数据的处理  
 在 Java 中的字符数据被当作 Unicode 处理默认设置。Java**字符串**对象表示 Unicode 字符数据。 在 JDBC Driver 中，唯一可以不遵守此规则的是 ASCII 流的 getter 和 setter 方法，这属于比较特殊的情况，因为这些方法使用的字节流带有单个已知代码页 (ASCII) 的隐式假定。  
  
 此外，JDBC 驱动程序提供**sendStringParametersAsUnicode**连接字符串属性。 此属性可用于指定字符数据的预定义参数作为 ASCII 或多字节字符集 (MBCS) 而不是 Unicode 来发送。 有关详细信息**sendStringParametersAsUnicode**连接字符串属性，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
### <a name="driver-incoming-conversions"></a>驱动程序传入转换  
 来自服务器的 Unicode 文本数据不是必须要转换的数据。 它将作为 Unicode 直接进行传递。 来自服务器的非 Unicode 数据从数据库或列级别的数据代码页直接转换为 Unicode。 JDBC 驱动程序将使用 Java 虚拟机 (JVM) 转换例程执行这些转换。 这些转换将通过所有类型化 String 和 Character 流 getter 方法得到执行。  
  
 如果 JVM 无法对来自数据库的数据提供相应的代码页支持，则 JDBC Driver 将引发“Java 环境不支持 XXX 代码页”异常。 要解决此问题，您应安装该 JVM 所需的完整国际字符支持。 有关示例，请参阅 Sun Microsystems 网站上的 Supported Encodings（受支持的编码）文档。  
  
### <a name="driver-outgoing-conversions"></a>驱动程序传出转换  
 从驱动程序发送至服务器的字符数据可以为 ASCII 或 Unicode。 例如，新 JDBC 4.0 国家字符集方法，如 setNString、 setNCharacterStream、 setNClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类，始终将其参数值发送到 Unicode 中的服务器。  
  
 另一方面，非 national 字符 API 方法，如 setString、 setCharacterStream 和 setClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类将其值发送到在 Unicode 服务器仅当**sendStringParametersAsUnicode**属性设置为"true"，是默认值。  
  
## <a name="non-unicode-parameters"></a>非 Unicode 参数  
 为了获得最佳性能与**CHAR**， **VARCHAR**或**LONGVARCHAR**非 Unicode 参数的类型，请设置**sendStringParametersAsUnicode**连接字符串为"false"的属性，并使用非 national 字符方法。  
  
## <a name="formatting-issues"></a>格式问题  
 有关日期、 时间和货币，使用本地化数据的所有格式设置是在 Java 语言级别执行使用的区域设置对象;和用于的各种格式设置方法**日期**，**日历**，和**数**数据类型。 只有在极少数的情况下，JDBC Driver 才需要以本地化格式传递受区域设置影响的数据，此时需要根据默认的 JVM 区域设置来使用相应的格式化程序。  
  
## <a name="collation-support"></a>排序规则支持  
 JDBC Driver 3.0 支持所有支持的排序规则[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]， [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，新的排序规则和新版本的 Windows 中的排序规则名称引入[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]。  
  
 有关排序规则的详细信息，请参阅[Collation and Unicode Support](http://go.microsoft.com/fwlink/?LinkId=131366)和[Windows 排序规则名称 (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=131367)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="using-international-domain-names-idn"></a>使用国际域名 (IDN)  
 SQL Server JDBC Driver 6.0 支持国际化域名 (Idn) 的使用，可将 Unicode serverName 转换为 ASCII 兼容编码 (Punycode) 时必须在连接期间。  如果 IDN 以 Punycode 格式（由 RFC 3490 指定）作为 ASCII 字符串存储在域名系统 (DNS) 中，通过将 serverNameAsACE 属性设置为 true 来启用 Unicode 服务器名称的转换。  否则，如果 DNS 服务配置为允许使用 Unicode 字符，请将 serverNameAsACE 属性设置为 false（默认值）。  对于较旧版本的 JDBC 驱动程序，它还可将 serverName 转换为 Punycode 使用[Java 的 IDN.toASCII](http://docs.oracle.com/javase/8/docs/api/java/net/IDN.html)之前将该属性为连接设置的方法。  
  
> [!NOTE]  
>  为非 Windows 平台编写的大多数解析程序软件基于 Internet DSN 标准，因此很可能为 IDN 使用 Punycode 格式，而专用网络上的基于 Windows 的 DNS 服务器可以配置为允许针对每个服务器使用 UTF-8 字符。  有关更多详细信息，请参阅[Unicode 字符支持](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
