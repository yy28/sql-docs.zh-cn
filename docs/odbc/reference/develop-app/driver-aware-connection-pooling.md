---
title: 驱动程序感知连接池 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dee7ee2b08e4b3b0249ede7f999cfb23d8db944
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047054"
---
# <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池
驱动程序感知连接池是 Windows 8 中的驱动程序管理器的一项新功能。 驱动程序感知连接池允许驱动程序编写器自定义 ODBC 驱动程序中的连接池行为。  
  
> [!NOTE]  
>  游标库不支持驱动程序感知连接池。 当启用了驱动程序感知连接池时，如果应用程序尝试通过 SQLSetConnectAttr 启用游标库，则该应用程序将收到错误消息。  
  
 驱动程序感知连接池解决了与驱动程序管理器连接池相关的下列问题：  
  
 **池碎片**如果与新的连接请求的连接字符串完全匹配，则驱动程序管理器将仅从池中返回连接。  驱动程序管理器需要完全匹配的一个原因是，驱动程序管理器不了解每个特定于驱动程序的连接字符串关键字及其值。  但是，某些连接字符串关键字值（如数据库的名称）可能不需要完全匹配，因为驱动程序可以在所需的时间内更改数据库，而不是打开新连接所需的时间（确切的时间差异取决于数据源）。 而且，某些连接属性（如 SQL_ATTR_CURRENT_CATALOG）中的差异可能需要更多的时间来更改其他属性（如 SQL_ATTR_LOGIN_TIMEOUT）中的差异。 这也会阻止驱动程序管理器使用从池中的最小成本、可重复使用的连接。 当驱动程序必须创建多个新连接时，应用程序的性能可能会降低，并且数据源的可伸缩性可能会降低。 池碎片可以通过驱动程序感知连接池降低，因为驱动程序可以更好地估计在池中为连接请求重复使用连接的成本。  
  
 **不考虑应用程序首选项**某些数据源可以有效地打开新连接（与重置某些属性相比），因此，应用程序可能更倾向于打开新连接，而不是尝试重新使用来自池的稍微不匹配的连接并重置某些值（尽管在连接池初始化短语期间这可能会较慢）。 但是，某些应用程序可能会使服务器负载更小并打开更少的连接，不过，为正确的行为修复不匹配的开销可能会更大。 如果没有驱动程序感知连接池，则由于驱动程序管理器无法识别所有特定于驱动程序的连接属性，因此不能有效地指定此类首选项。 驱动程序感知连接池允许驱动程序获取用户首选项（使用 SQLSetConnectAttr 的特定于驱动程序的属性），以便它可以更好地估算基于用户首选项从池中重复使用连接的成本。  
  
 有关驱动程序感知连接池的详细信息，请参阅[在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>确定驱动程序支持  
 驱动程序感知连接池是驱动程序可能不支持的一项可选功能。 若要确定驱动程序是否支持该驱动程序，请使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* of [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何启用可识别驱动程序的连接池  
 应用程序可以通过将 SQL_ATTR_CONNECTION_POOLING 特性设置为与[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)SQL_CP_DRIVER_AWARE 来使用驱动程序的连接池感知。 如果驱动程序不支持连接池感知，则将使用驱动程序管理器连接池（与 SQL_CP_ONE_PER_HENV 指定的相同，而不是 SQL_CP_DRIVER_AWARE）。 ODBC 2.x 和1.x 应用程序可以启用此功能。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
