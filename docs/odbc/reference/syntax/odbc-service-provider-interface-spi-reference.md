---
title: "ODBC 服务提供程序接口 (SPI) 参考 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3334e74f7b7c6cd76c21de6f47224db9ebec2ce3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服务提供程序接口 (SPI) 引用
传统上，ODBC 定义应用程序编程接口 (API)。 可以由应用程序调用 API 中的函数，它们应在驱动程序管理器和驱动程序内实现。  
  
 借助新增的识别驱动程序的连接池功能，ODBC 引入了服务提供程序接口 (SPI)。 SPI 中的函数用于驱动程序管理器和驱动程序之间的通信。 SPI 函数的实现是由驱动程序;驱动程序管理器不公开 SPI 函数对应用程序。 应用程序不应直接调用这些函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
 本部分包含以下主题  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [开发中的 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驱动程序管理器连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
