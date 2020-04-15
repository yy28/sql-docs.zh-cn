---
title: 驱动程序感知连接池 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287597"
---
# <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池
驱动程序感知连接池是 Windows 8 中的驱动程序管理器的新功能。 驱动程序感知连接池允许驱动程序编写器在其 ODBC 驱动程序中自定义连接池行为。  
  
> [!NOTE]  
>  游标库不支持驱动程序感知连接池。 如果应用程序尝试通过 SQLSetConnectAttr 启用游标库，则应用程序在启用驱动程序感知连接池时将收到错误消息。  
  
 驱动程序感知连接池解决了与驱动程序管理器连接池相关的以下问题：  
  
 **池碎片**驱动程序管理器仅从池中返回连接，如果它与新连接请求的连接字符串完全匹配。  驱动程序管理器需要完全匹配的一个原因是驱动程序管理器不了解每个特定于驱动程序的连接字符串关键字及其值。  但是，某些连接字符串关键字值（如数据库的名称）可能不需要完全匹配，因为驱动程序可以在不到打开新连接所需的时间内更改数据库（确切的时差取决于数据源）。 而且，某些连接属性（如SQL_ATTR_CURRENT_CATALOG）的差异可能需要比其他属性（如SQL_ATTR_LOGIN_TIMEOUT）的差异更多的时间来更改。 这也可以阻止驱动程序管理器使用池中成本最低的可重用连接。 当驱动程序必须创建许多新连接时，应用程序的性能可能会降低，数据源的可伸缩性也会降低。 通过驱动程序感知连接池可以减少池碎片，因为驱动程序可以更好地估计在池中重用连接请求的成本。  
  
 **不考虑申请偏好**某些数据源可以有效地打开新连接（与重置某些属性相比），因此，应用程序可能更喜欢打开新连接，而不是尝试从池中重用稍微不匹配的连接并重置某些值（尽管在连接池初始化短语中这可能较慢）。 但是，某些应用程序可能会使服务器负载变小，打开较少的连接，尽管修复不匹配的正确行为的成本可能更大。 如果没有驱动程序感知连接池，则无法有效地指定此类首选项，因为驱动程序管理器无法识别所有特定于驱动程序的连接属性。 驱动程序感知连接池允许驱动程序获取用户首选项（具有 SQLSetConnectAttr 的特定于驱动程序的属性），以便根据用户的首选项更好地估计从池中重用连接的成本。  
  
 有关驱动程序感知连接池的详细信息，请参阅[在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>确定驱动程序支持  
 驱动程序感知连接池是驱动程序可能不支持的可选功能。 要确定驱动程序是否支持它，请使用[SQL_DRIVER_AWARE_POOLING_SUPPORTED SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)*的信息类型*。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何启用驱动程序感知连接池  
 应用程序可以通过将SQL_ATTR_CONNECTION_POOLING属性设置为使用[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)SQL_CP_DRIVER_AWARE来使用驱动程序的连接池感知。 如果驱动程序不支持连接池感知，将使用驱动程序管理器连接池（与指定SQL_CP_ONE_PER_HENV相同，而不是SQL_CP_DRIVER_AWARE）。 ODBC 2.x 和 3.x 应用程序可以启用此功能。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
