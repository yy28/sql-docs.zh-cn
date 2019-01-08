---
title: 识别驱动程序的连接池 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8ea4643354990ad416ac3975467c5991842adacc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52390570"
---
# <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池
驱动程序识别连接池是一项新功能的驱动程序管理器在 Windows 8 中。 驱动程序识别连接池允许驱动程序编写人员自定义连接池中其 ODBC 驱动程序的行为。  
  
> [!NOTE]  
>  游标库不支持驱动程序识别连接池。 如果它尝试启用游标库通过 SQLSetConnectAttr，启用驱动程序识别连接池后，应用程序将收到错误消息。  
  
 驱动程序识别连接池地址与驱动程序管理器连接池相关的以下问题：  
  
 **池碎片**的驱动程序管理器中将仅返回一个连接池中的线程是否完全匹配的新连接请求的连接字符串。  有关驱动程序管理器需要完全匹配的一个原因是驱动程序管理器不理解每个特定于驱动程序的连接字符串关键字和它的值。  但是，某些连接字符串关键字值 （如数据库的名称） 可能不需要完全匹配，因为该驱动程序可以更改在打开新的连接 （确切的时差取决于数据源） 所需的时间之内的数据库。 而且，某些连接属性 （如 SQL_ATTR_CURRENT_CATALOG) 之间的差异可能需要更多的时间比其他属性 （如 SQL_ATTR_LOGIN_TIMEOUT) 之间的差异更改。 这样，也可以阻止驱动程序管理器使用从池的成本最低的、 可重复使用连接。 当驱动程序必须创建多个新连接时，可能会降低应用程序的性能和数据源可伸缩性可能会降低。 池碎片可以减少与识别驱动程序的连接池，因为驱动程序可以更好地估计重用连接池中的连接请求的成本。  
  
 **应用程序首选项不考虑**某些数据源可以有效地打开新连接 （与重置某些属性比较），因此，应用程序可能更倾向于以打开新的连接而非尝试重用略有不匹配从池和重置一些值 （尽管这可能会降低期间连接池初始化短语） 的连接。 但某些应用程序可能减小服务器负载并打开较少连接数，尽管可能会有更大的成本，若要修复的正确的行为不匹配。 而无需识别驱动程序的连接池，您无法指定此类首选项有效，因为驱动程序管理器不能识别所有特定于驱动程序的连接属性。 识别驱动程序的连接池使驱动程序来获取 （使用 SQLSetConnectAttr 的特定于驱动程序属性） 的用户首选项，以便它可以更好地估计重用从基于用户的首选项的池的连接的成本。  
  
 有关识别驱动程序的连接池的详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
## <a name="determining-driver-support"></a>确定驱动程序支持  
 识别驱动程序的连接池是一项可选功能的驱动程序可能不支持。 若要确定驱动程序支持它，请使用 SQL_DRIVER_AWARE_POOLING_SUPPORTED*信息类型*的[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>如何能够识别驱动程序的连接池  
 应用程序可以使用驱动程序的连接池感知通过 SQL_ATTR_CONNECTION_POOLING 属性设置为与 SQL_CP_DRIVER_AWARE [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 如果驱动程序不支持连接池感知，将使用驱动程序管理器连接池 （SQL_CP_ONE_PER_HENV 假定已指定，而不是 SQL_CP_DRIVER_AWARE 相同）。 ODBC 2.x 和 3.x 应用程序可以启用此功能。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
