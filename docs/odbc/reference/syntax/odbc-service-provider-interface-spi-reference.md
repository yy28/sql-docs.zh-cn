---
title: ODBC 服务提供商接口 （SPI） 参考 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298905"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 服务提供程序接口 (SPI) 参考
传统上，ODBC 定义了应用程序编程接口 （API）。 API 中的函数可以由应用程序调用，它们应在驱动程序管理器和驱动程序内实现。  
  
 随着驱动程序感知连接池功能的加入，ODBC 引入了服务提供商接口 （SPI）。 SPI 中的函数用于驱动程序管理器和驱动程序之间的通信。 SPI 功能由驱动程序实现;驱动程序管理器不向应用程序公开 SPI 功能。 应用程序不应直接调用这些函数。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
 本节包含下列主题  
  
-   [SQL 清理连接池 ID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPool连接](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRate 连接](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectattrFordbcinfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSet驱动程序连接信息](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [驱动程序管理器连接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
