---
title: 识别驱动程序的连接池 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2efa24f11f174c77ebe7f289019b0544f65d0c2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池
驱动程序感知的连接池是一项新功能的驱动程序管理器在 Windows 8。 驱动程序感知的连接池允许驱动程序编写器可自定义连接池其 ODBC 驱动程序中的行为。  
  
> [!NOTE]  
>  游标库不支持驱动程序感知的连接池。 如果它尝试启用通过 SQLSetConnectAttr，光标库，启用驱动程序感知的连接池后，应用程序将收到错误消息。  
  
 驱动程序感知连接池地址与驱动程序管理器连接池相关的以下问题：  
  
 **池碎片**驱动程序管理器将只返回连接从池中是否完全匹配项的新连接请求的连接字符串。  有关驱动程序管理器需要完全匹配的一个原因是驱动程序管理器并不了解每个驱动程序特定的连接字符串关键字和它的值。  但是，某些连接字符串关键字值 （如数据库的名称） 可能不需要完全匹配，因为该驱动程序可以更改在打开新连接 （精确时间差异依赖于数据源） 所需的时间之内的数据库。 而且，某些连接属性 （例如 SQL_ATTR_CURRENT_CATALOG) 方面的差异可能需要更多时间来更改比其他属性 （如 SQL_ATTR_LOGIN_TIMEOUT) 方面的差异。 此操作，请也可以阻止驱动程序管理器使用最低成本、 可重用连接池中的线程。 当驱动程序必须创建多个新连接时，可能会降低应用程序的性能，并且数据源可伸缩性会降低。 识别驱动程序的连接池，因为驱动程序可以更好地估计重用的连接请求池中的连接的成本可以缩短池碎片。  
  
 **应用程序首选项不考虑**某些数据源可以有效地打开新连接 （与重置某些属性相比），因此，应用程序可能更倾向打开新连接而非尝试重用略有不匹配从池和重置某些值 （尽管这可能会降低连接池初始化短语期间） 的连接。 但某些应用程序可能减小服务器负载，虽然可能有更大的成本，若要修复的正确行为的不匹配的打开连接数较少。 不识别驱动程序的连接池，不能指定首选项这种实际上，因为驱动程序管理器无法识别所有特定于驱动程序的连接属性。 识别驱动程序的连接池使驱动程序来获取 （与 SQLSetConnectAttr 特定于驱动程序属性） 的用户首选项，以便它可以更好地估计重复使用从基于用户的首选项的池的连接的开销。  
  
 有关识别驱动程序的连接池的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>确定驱动程序支持  
 识别驱动程序的连接池是一项可选功能，可能不支持驱动程序。 若要确定驱动程序支持它，请使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED*信息类型*的[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何启用识别驱动程序的连接池  
 应用程序可以通过将 SQL_ATTR_CONNECTION_POOLING 属性设置为 SQL_CP_DRIVER_AWARE 与使用驱动程序的连接池感知[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 如果驱动程序不支持连接池感知，将使用驱动程序管理器连接池 （如同 SQL_CP_ONE_PER_HENV 已指定一样，而不是 SQL_CP_DRIVER_AWARE 相同）。 ODBC 2.x 和 3.x 应用程序可以启用此功能。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
