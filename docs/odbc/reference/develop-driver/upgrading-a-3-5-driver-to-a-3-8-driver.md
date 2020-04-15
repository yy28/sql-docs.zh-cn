---
title: 将 3.5 驱动程序升级到 3.8 驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dcd01d050e806b733d75c54058945d367a33d6a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294428"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>将 3.5 驱动程序升级到 3.8 驱动程序
本主题提供了将 ODBC 3.5 驱动程序升级到 ODBC 3.8 驱动程序的指南和注意事项。  
  
##### <a name="version-numbers"></a>版本号  
 以下准则涉及版本号：  
  
-   驱动程序应支持SQL_ATTR_ODBC_VERSIONSQL_OV_ODBC3_80，返回SQL_ERRORSQL_OV_ODBC2、SQL_OV_ODBC3和SQL_OV_ODBC3_80以外的值。 如果驱动程序从[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)返回SQL_SUCCESS，则驱动程序管理器的未来版本将假定驱动程序支持 ODBC 合规性级别。  
  
-   版本 3.8 驱动程序应返回 03.80 从**SQLGetInfo**时SQL_DRIVER_ODBC_VER传递到*InfoType*。 但是，旧版本的 Microsoft Windows 中包括的旧驱动程序管理器会将驱动程序视为版本 3.5 驱动程序，并发出警告。  
  
     在 Windows 7 中，驱动程序管理器版本为 03.80。 在 Windows 8 中，驱动程序管理器版本通过 SQLGetInfo SQL_DM_VER（*信息类型*参数）为 03.81。 SQL_ODBC_VER在 Windows 7 和 Windows 8 中报告版本为 03.80。  
  
##### <a name="driver-specific-c-data-types"></a>特定于驱动程序的 C 数据类型  
 当驱动程序适用于版本 3.8 ODBC 应用程序时，它可以具有自定义的 C 数据类型。 （有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。但是，不需要 3.8 驱动程序实现任何特定于驱动程序的 C 类型。 但是，驱动程序仍应执行 C 类型的范围检查;驱动程序管理器不会对 3.8 驱动程序执行此操作。 为了便于驱动程序开发，可以以以下格式定义特定于驱动程序的 C 数据类型的值：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性  
 在开发新驱动程序时，应对数据类型、描述符类型、信息类型、诊断类型和属性使用特定于驱动程序的范围。 特定于驱动程序的范围及其基本类型值在[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)中进行了讨论。  
  
##### <a name="connection-pooling"></a>连接池  
 为了更好地管理连接池，ODBC 3.8 引入了**SQLSetConnectAttr**中的SQL_ATTR_RESET_CONNECTION连接属性。 SQL_RESET_CONNECTION_YES是此属性的唯一有效值。 SQL_ATTR_RESET_CONNECTION将在驱动程序管理器将连接放入连接池之前进行设置，从而允许驱动程序将其他连接属性重置为其默认值。  
  
 为了避免与服务器进行不必要的通信，驱动程序可以将连接属性重置推迟到从池中重用连接后与远程服务器的下一次通信。  
  
 请注意，SQL_ATTR_RESET_CONNECTION仅用于驱动程序管理器和驱动程序之间的通信。 应用程序不能直接设置此属性。 所有版本 3.8 驱动程序都应实现此连接属性。  
  
##### <a name="streamed-output-parameters"></a>流输出参数  
 ODBC 版本 3.8 引入了流式输出参数，这是检索输出参数的一种更具可扩展性的方法。 （有关详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。为了支持此功能，当 SQL_GETDATA_EXTENSIONS是**SQLGetInfo**调用中的*InfoType*时，驱动程序应在返回值中设置SQL_GD_OUTPUT_PARAMS。 必须在驱动程序中实现对具有流式输出参数的 SQL 类型的支持。 驱动程序管理器不会为无效的 SQL 类型生成错误。 支持流式输出参数的 SQL 类型在驱动程序中定义。  
  
 如果应用程序使用**SQLGetData**检索与**SQLParamData**返回的参数不一样的参数，则驱动程序应返回SQL_ERROR。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>连接操作的异步执行（轮询方法）  
 驱动程序可以为各种连接操作启用异步支持。  
  
 从 Windows 7 开始，ODBC 支持轮询方法（有关详细信息，请参阅[异步执行（轮询方法）。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md) 不需要版本 3.8 ODBC 驱动程序对连接句柄实现异步操作。 即使驱动程序未在连接句柄上实现异步操作，驱动程序仍应实现SQL_ASYNC_DBC_FUNCTIONS *InfoType*并返回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 启用异步连接操作后，连接操作的运行时间是所有重复调用的总时间。 如果上次重复调用发生在总时间超过SQL_ATTR_CONNECTION_TIMEOUT连接属性设置的值之后，并且操作尚未完成，则驱动程序返回SQL_ERROR，并记录 SQLState HYT01 和消息"连接超时已过期"。。 如果操作完成，则没有超时。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数  
 ODBC 3.8 支持[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，用于取消连接和语句操作。 支持**SQLCancelHandle**的驱动程序必须导出该函数。 如果应用程序在语句句柄上调用**SQLCancel**或**SQLCancelHandle，** 驱动程序不应取消正在进行的任何同步或异步连接功能。 同样，如果应用程序在连接句柄上调用**SQLCancelHandle，** 驱动程序不应取消正在进行的任何同步或异步语句函数。 此外，如果应用程序在连接句柄上调用**SQLCancelHandle，** 驱动程序不应取消浏览操作 **（SQLBrowseConnect**返回SQL_NEED_DATA）。 在这些情况下，驱动程序应返回 HY010，"功能序列错误"。  
  
 不必同时支持**SQLCancelHandle**和异步连接操作。 驱动程序可以支持异步连接操作，但不能支持**SQLCancelHandle，** 反之亦然。  
  
##### <a name="suspended-connections"></a>挂起的连接  
 ODBC 3.8 驱动程序管理器可以将连接置于挂起状态。 应用程序将调用**SQLDisconnect**以释放与连接关联的资源。 在这种情况下，驱动程序应尝试释放尽可能多的资源，而不检查连接的状态。 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 Windows 8 中的 ODBC 允许驱动程序自定义连接池行为。 有关详细信息，请参阅[驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
 ODBC 3.8 支持异步操作的通知方法，可在 Windows 8 上开始。 有关详细信息，请参阅[异步执行（通知方法）。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [微软提供的ODBC驱动程序](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
