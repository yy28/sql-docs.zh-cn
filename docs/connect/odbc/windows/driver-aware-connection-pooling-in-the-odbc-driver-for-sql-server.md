---
title: 识别驱动程序的连接池 in the ODBC Driver for SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3cc9428f84db56675dbf58c977078fa4dcca6ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>ODBC Driver for SQL Server 中识别驱动程序的连接池
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持[识别驱动程序的连接池](http://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 本主题介绍对识别驱动程序的连接池的 Microsoft ODBC 驱动程序中所做的增强功能[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Windows 上：  
  
-   无论连接属性，使用的连接`SQLDriverConnect`转到单独的池使用的连接从`SQLConnect`。
- 使用时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]身份验证和识别驱动程序的连接池，该驱动程序不使用当前线程的 Windows 用户的安全上下文来分离池中的连接。 也就是说，当连接等效于其用于通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 身份验证的 Windows 模拟方案的参数，且它们使用同一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 身份验证凭据连接到后端时，不同的 Windows 用户或许可以使用同一个连接池。 当使用 Windows 身份验证和识别驱动程序的连接池时，该驱动程序将使用当前 Windows 用户的安全上下文来分离池中的连接。 也就是说，对于 Windows 模拟方案，不同的 Windows 用户不会共享连接，即使这些连接使用相同的参数也是如此。
- 使用 Azure Active Directory 和识别驱动程序的连接池时，该驱动程序还使用身份验证值来确定在连接池中的成员身份。
  
-   识别驱动程序的连接池将阻止该池返回错误的连接。  
  
-   识别驱动程序的连接池可识别特定于驱动程序的连接属性。 因此，如果某个连接使用`SQL_COPT_SS_APPLICATION_INTENT`设置为只读，该连接获取其自己的连接池。
-   设置`SQL_COPT_SS_ACCESS_TOKEN`属性将导致单独存入池中的连接 
  
如果以下连接属性 ID 或连接字符串关键字之一在你的连接字符串和已入池的连接字符串之间有所不同，该驱动程序将使用已入池的连接。 但是，如果所有连接属性 ID 或连接字符串关键字均匹配，可实现更佳性能。 （为了匹配池中的某个连接，驱动程序会重置该属性。 由于重置以下参数需要额外的网络调用，因此会降低性能。  
  
-    如果以下两个或多个连接属性或连接关键字有所不同，则不使用已入池的连接。  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   如果以下任何连接关键字在你的连接字符串和已入池的连接字符串之间有所不同，则不使用已入池的连接。  
  
    |关键字|ODBC Driver 13|ODBC Driver 11|
    |-|-|-|
    |`Address`|是|用户帐户控制|
    |`AnsiNPW`|用户帐户控制|用户帐户控制|
    |`App`|用户帐户控制|用户帐户控制|
    |`ApplicationIntent`|用户帐户控制|用户帐户控制|  
    |`Authentication`|用户帐户控制|“否”|
    |`ColumnEncryption`|是|“否”|
    |`Database`|用户帐户控制|用户帐户控制|
    |`Encrypt`|用户帐户控制|用户帐户控制|  
    |`Failover_Partner`|用户帐户控制|用户帐户控制|
    |`FailoverPartnerSPN`|用户帐户控制|用户帐户控制|
    |`MARS_Connection`|用户帐户控制|用户帐户控制|
    |`Network`|用户帐户控制|用户帐户控制|
    |`PWD`|用户帐户控制|用户帐户控制|
    |`Server`|用户帐户控制|用户帐户控制|
    |`ServerSPN`|用户帐户控制|用户帐户控制|
    |`TransparentNetworkIPResolution`|用户帐户控制|用户帐户控制|
    |`Trusted_Connection`|用户帐户控制|用户帐户控制|
    |`TrustServerCertificate`|用户帐户控制|用户帐户控制|
    |`UID`|用户帐户控制|用户帐户控制|
    |`WSID`|用户帐户控制|是|
    
- 如果以下任何连接属性在你的连接字符串和已入池的连接字符串之间有所不同，则不使用已入池的连接。  
  
    |Attribute|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|是|用户帐户控制|
    |`SQL_ATTR_PACKET_SIZE`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_ANSI_NPW`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_ACCESS_TOKEN`|用户帐户控制|“否”|
    |`SQL_COPT_SS_AUTHENTICATION`|是|“否”|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_BCP`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|用户帐户控制|“否”|
    |`SQL_COPT_SS_CONCAT_NULL`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_ENCRYPT`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_MARS_ENABLED`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_OLDPWD`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_SERVER_SPN`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|用户帐户控制|用户帐户控制|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_TNIR`|用户帐户控制|否|
 
-   无需进行额外的网络调用，该驱动程序即可重置和调整以下连接关键字和属性。 该驱动程序将重置这些参数，以确保该连接不会包含错误信息。  
  
     在驱动程序管理器尝试将你的连接与池中的连接进行匹配时，不会考虑这些连接关键字。 （即使更改其中一个参数，仍可重复使用现有连接。 该驱动程序将根据需要重置这些选项。）在客户端中，无需进行额外的网络调用可以重置这些属性。  
  
    |关键字|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |`AutoTranslate`|是|用户帐户控制|
    |`Description`|用户帐户控制|用户帐户控制|
    |`MultisubnetFailover`|用户帐户控制|用户帐户控制|  
    |`QueryLog_On`|用户帐户控制|用户帐户控制|
    |`QueryLogFile`|用户帐户控制|用户帐户控制|
    |`QueryLogTime`|用户帐户控制|用户帐户控制|
    |`Regional`|用户帐户控制|用户帐户控制|
    |`StatsLog_On`|用户帐户控制|用户帐户控制|
    |`StatsLogFile`|  用户帐户控制|是|
  
     如果更改以下连接属性之一，仍可重复使用现有连接。  该驱动程序将根据需要重置该值。 无需进行额外的网络调用，该驱动程序即可在客户端中重置这些属性。  
  
    |Attribute|ODBC Driver 13|ODBC Driver 11|  
    |-|-|-|  
    |所有语句属性|是|用户帐户控制|
    |`SQL_ATTR_AUTOCOMMIT`|用户帐户控制|用户帐户控制|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  用户帐户控制|用户帐户控制|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|用户帐户控制|用户帐户控制|
    |`SQL_ATTR_LOGIN_TIMEOUT`|用户帐户控制|用户帐户控制|
    |`SQL_ATTR_ODBC_CURSORS`|  用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PERF_DATA`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PERF_DATA_LOG`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| 用户帐户控制|用户帐户控制| 
    |`SQL_COPT_SS_PERF_QUERY`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_TRANSLATE`|用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_USER_DATA`|  用户帐户控制|用户帐户控制|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|用户帐户控制|是|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
