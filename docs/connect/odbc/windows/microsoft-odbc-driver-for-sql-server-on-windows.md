---
title: Windows 上的 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c075c7adcc7eeae3ae7a83676256e72b4b86d187
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989436"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server（Windows 平台）
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 是独立的 ODBC 驱动程序，可提供一个用于实现针对 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的标准 ODBC 接口的应用程序编程接口 (API)。

Microsoft ODBC Driver for SQL Server 可用于创建新应用程序。 还可以升级当前使用较旧的 ODBC 驱动程序的较旧应用程序。 ODBC Driver for SQL Server 支持与 Azure SQL 数据库、Azure SQL 数据仓库、SQL Server 2017、SQL Server 2016、SQL Server 2014、SQL Server 2012、SQL Server 2008 R2、SQL Server 2008 和 SQL Server 2005 的连接。  

## <a name="summary"></a>总结

| 版本       | 支持的功能      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>对 BCP API 的 Always Encrypted 支持</li><li>新连接字符串属性 UseFMTONLY 使驱动程序在需要临时表的特殊情况下使用旧的元数据</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Azure AD 身份验证</li><li>AlwaysOn 可用性组 (AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>国际化域名 (IDN)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>识别驱动程序的连接池</li><li>连接复原</li><li>异步执行（轮询方法）</li></ul> |    

## <a name="documentation"></a>文档  
适用于 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的此文档包括：  
  
-   [适用于 Windows 上 SQL Server 的 ODBC 的发行说明](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Windows 上 Microsoft ODBC Driver for SQL Server 的功能](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [系统要求、安装和驱动程序文件](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server 中识别驱动程序的连接池](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [异步执行（通知方法）示例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC 驱动程序中的连接弹性](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [对 ODBC 驱动程序使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [结合使用 Azure Active Directory 和 ODBC 驱动程序](../../../connect/odbc/using-azure-active-directory.md) 
-   [使用透明网络 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>社区  
- [Microsoft SQL Server ODBC 驱动程序团队博客](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server 数据访问论坛](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>另请参阅  
- [关于 SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [使用 SQL Server Native Client 生成应用程序](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [SQL Server Native Client FAQ](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [ODBC 程序员参考](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
