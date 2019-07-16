---
title: ODBC 服务提供程序接口 (SPI) 参考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88053620fa413c50a8faff4cc47cbbe1457249f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073836"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服务提供程序接口 (SPI) 参考
传统上，ODBC 定义应用程序编程接口 (API)。 在 API 函数可以调用应用程序和驱动程序管理器和驱动程序中实现它们。  
  
 添加了识别驱动程序的连接池功能，通过 ODBC 引入了服务提供程序接口 (SPI)。 在 SPI 函数用于驱动程序管理器和驱动程序之间的通信。 SPI 函数的实现是由驱动程序;驱动程序管理器不会公开 SPI 函数对应用程序。 应用程序不应直接调用这些函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
 本部分包含以下主题  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [开发中的 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驱动程序管理器连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
