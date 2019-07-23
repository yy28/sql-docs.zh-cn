---
title: 在适用于 SQL Server 的 ODBC 驱动程序中识别驱动程序的连接池 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97ddd5aa4abf926ecd4e68e89bef63b8f25ce323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009969"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>ODBC Driver for SQL Server 中识别驱动程序的连接池
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持[识别驱动程序的连接池](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 本主题介绍 Windows 上的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中识别驱动程序的连接池的增强功能：  
  
-   无论连接属性如何，使用 `SQLDriverConnect` 的连接都会从使用 `SQLConnect` 的连接转到单独的池。
- 如果使用的是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证和驱动程序感知连接池，驱动程序不会对当前线程使用 Windows 用户的安全性上下文来分离池中的连接。 也就是说，当连接等效于其用于通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证的 Windows 模拟方案的参数，且它们使用同一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证凭据连接到后端时，不同的 Windows 用户或许可以使用同一个连接池。 如果使用的是 Windows 身份验证和驱动程序感知连接池，驱动程序会使用当前 Windows 用户的安全性上下文来分离池中的连接。 也就是说，对于 Windows 模拟方案，不同的 Windows 用户不会共享连接，即使这些连接使用相同的参数也是如此。
- 使用 Azure Active Directory 和驱动程序感知连接池时, 驱动程序还将使用身份验证值来确定连接池中的成员身份。
  
-   识别驱动程序的连接池将阻止该池返回错误的连接。  
  
-   识别驱动程序的连接池可识别特定于驱动程序的连接属性。 因此, 如果连接使用`SQL_COPT_SS_APPLICATION_INTENT`设置为只读, 则该连接将获取自己的连接池。
-   `SQL_COPT_SS_ACCESS_TOKEN`设置属性将导致连接单独进行缓冲 
  
如果以下连接属性 ID 或连接字符串关键字之一在你的连接字符串和已入池的连接字符串之间有所不同，该驱动程序将使用已入池的连接。 但是，如果所有连接属性 ID 或连接字符串关键字均匹配，可实现更佳性能。 （为了匹配池中的某个连接，驱动程序会重置该属性。 由于重置以下参数需要额外的网络调用，因此会降低性能。  
  
-    如果以下两个或多个连接属性或连接关键字有所不同，则不使用已入池的连接。  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   如果以下任何连接关键字在你的连接字符串和已入池的连接字符串之间有所不同，则不使用已入池的连接。  
  
    |关键字|ODBC 驱动程序 13|ODBC 驱动程序 11|
    |-|-|-|
    |`Address`|是|是|
    |`AnsiNPW`|是|是|
    |`App`|是|是|
    |`ApplicationIntent`|是|是|  
    |`Authentication`|是|否|
    |`ColumnEncryption`|是|否|
    |`Database`|是|是|
    |`Encrypt`|是|是|  
    |`Failover_Partner`|是|是|
    |`FailoverPartnerSPN`|是|是|
    |`MARS_Connection`|是|是|
    |`Network`|是|是|
    |`PWD`|是|是|
    |`Server`|是|是|
    |`ServerSPN`|是|是|
    |`TransparentNetworkIPResolution`|是|是|
    |`Trusted_Connection`|是|是|
    |`TrustServerCertificate`|是|是|
    |`UID`|是|是|
    |`WSID`|是|是|
    
- 如果以下任何连接属性在你的连接字符串和已入池的连接字符串之间有所不同，则不使用已入池的连接。  
  
    |Attribute|ODBC 驱动程序 13|ODBC 驱动程序 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|是|是|
    |`SQL_ATTR_PACKET_SIZE`|是|是|
    |`SQL_COPT_SS_ANSI_NPW`|是|是|
    |`SQL_COPT_SS_ACCESS_TOKEN`|是|否|
    |`SQL_COPT_SS_AUTHENTICATION`|是|否|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|是|是|
    |`SQL_COPT_SS_BCP`|是|是|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|是|否|
    |`SQL_COPT_SS_CONCAT_NULL`|是|是|
    |`SQL_COPT_SS_ENCRYPT`|是|是|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|是|是|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|是|是|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|是|是|
    |`SQL_COPT_SS_MARS_ENABLED`|是|是|
    |`SQL_COPT_SS_OLDPWD`|是|是|
    |`SQL_COPT_SS_SERVER_SPN`|是|是|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|是|是|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|是|是|
    |`SQL_COPT_SS_TNIR`|是|否|
 
-   无需进行额外的网络调用，该驱动程序即可重置和调整以下连接关键字和属性。 该驱动程序将重置这些参数，以确保该连接不会包含错误信息。  
  
     在驱动程序管理器尝试将你的连接与池中的连接进行匹配时，不会考虑这些连接关键字。 （即使更改其中一个参数，仍可重复使用现有连接。 驱动程序将根据需要重置这些选项。）无需进行额外的网络调用，即可在客户端中重置这些属性。  
  
    |关键字|ODBC 驱动程序 13|ODBC 驱动程序 11|  
    |-|-|-|  
    |`AutoTranslate`|是|是|
    |`Description`|是|是|
    |`MultisubnetFailover`|是|是|  
    |`QueryLog_On`|是|是|
    |`QueryLogFile`|是|是|
    |`QueryLogTime`|是|是|
    |`Regional`|是|是|
    |`StatsLog_On`|是|是|
    |`StatsLogFile`|  是|是|
  
     如果更改以下连接属性之一，仍可重复使用现有连接。  该驱动程序将根据需要重置该值。 无需进行额外的网络调用，该驱动程序即可在客户端中重置这些属性。  
  
    |Attribute|ODBC 驱动程序 13|ODBC 驱动程序 11|  
    |-|-|-|  
    |所有语句属性|是|是|
    |`SQL_ATTR_AUTOCOMMIT`|是|是|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  是|是|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|是|是|
    |`SQL_ATTR_LOGIN_TIMEOUT`|是|是|
    |`SQL_ATTR_ODBC_CURSORS`|  是|是|
    |`SQL_COPT_SS_PERF_DATA`|是|是|
    |`SQL_COPT_SS_PERF_DATA_LOG`|是|是|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| 是|是| 
    |`SQL_COPT_SS_PERF_QUERY`|是|是|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|是|是|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  是|是|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|是|是|
    |`SQL_COPT_SS_TRANSLATE`|是|是|
    |`SQL_COPT_SS_USER_DATA`|  是|是|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|是|是|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
