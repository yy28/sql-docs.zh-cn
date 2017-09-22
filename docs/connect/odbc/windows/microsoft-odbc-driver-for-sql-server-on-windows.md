---
title: "Microsoft ODBC Driver for SQL Server on Windows |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: ec9cbf6cc2e8d74fdc87881622e1a1258aeea260
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server（Windows 平台）
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver 13.1，13 和 11 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]是独立的 ODBC 驱动程序提供实现给 Microsoft 的标准 ODBC 接口应用程序编程接口 (API) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。

Microsoft ODBC Driver for SQL Server 可以用于创建新的应用程序。 你还可以升级的旧版应用程序当前使用旧的 ODBC 驱动程序。 ODBC Driver for SQL Server 支持连接到 Azure SQL 数据库、 Azure SQL 数据仓库、 SQL Server 2016、 SQL Server 2014、 SQL Server 2012、 SQL Server 2008 R2、 SQL Server 2008 和 SQL Server 2005。  

## <a name="summary"></a>摘要

| 版本       | 支持的功能      |
| ------------- |---------------| 
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>始终加密</li><li>Azure AD 身份验证</li><li>AlwaysOn 可用性组 (AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>国际化域名 (IDN)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>识别驱动程序的连接池</li><li>连接复原</li><li>异步执行 （轮询方法）</li></ul> |    

## <a name="documentation"></a>文档  
用于 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的此文档包括：  
  
-   [发行说明](../../../connect/odbc/windows/release-notes.md)  
-   [Windows 上的 Microsoft ODBC Driver for SQL Server 的功能](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [系统要求、安装和驱动程序文件](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server 中识别驱动程序的连接池](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [异步执行（通知方法）示例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC 驱动程序中的连接弹性](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [使用始终加密的 ODBC 驱动程序](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [使用 ODBC 驱动程序的 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) 
-   [使用透明网络 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)   
  
## <a name="community"></a>社区  
- [Microsoft SQL Server ODBC 驱动程序团队博客](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum（英文）](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>另请参阅  
- [关于 SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [使用 SQL Server Native Client 生成应用程序](/sql-docs/docs/relational-databases/native-client/applications/building-applications-with-sql-server-native-client)   
- [SQL Server Native Client FAQ](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [ODBC 程序员参考](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](/sql-docs/docs/relational-databases/native-client/odbc/sql-server-native-client-odbc)  

