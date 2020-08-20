---
description: 将 3.5 驱动程序升级到 3.8 驱动程序
title: 将3.5 驱动程序升级到3.8 驱动程序 |Microsoft Docs
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
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461329"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>将 3.5 驱动程序升级到 3.8 驱动程序
本主题提供有关将 ODBC 3.5 驱动程序升级到 ODBC 3.8 驱动程序的指南和注意事项。  
  
##### <a name="version-numbers"></a>版本号  
 以下准则与版本号相关：  
  
-   驱动程序应支持 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80，并为 SQL_OV_ODBC2、SQL_OV_ODBC3 和 SQL_OV_ODBC3_80 以外的值返回 SQL_ERROR。 驱动程序管理器的未来版本将假定驱动程序支持 ODBC 符合性级别（如果驱动程序从 [SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)返回 SQL_SUCCESS。  
  
-   当 SQL_DRIVER_ODBC_VER 传递到*InfoType*时，3.8 版驱动程序应从**SQLGetInfo**返回03.80。 但是，较早版本的 Microsoft Windows 中包含的较早的驱动程序管理器会将驱动程序视为版本3.5 驱动程序，并发出警告。  
  
     在 Windows 7 中，驱动程序管理器版本为03.80。 在 Windows 8 中，驱动程序管理器版本为03.81，通过 SQLGetInfo SQL_DM_VER (*InfoType* 参数) 。 SQL_ODBC_VER 在 Windows 7 和 Windows 8 中报告版本为03.80。  
  
##### <a name="driver-specific-c-data-types"></a>驱动程序特定的 C 数据类型  
 当驱动程序使用版本 3.8 ODBC 应用程序时，它可以具有自定义的 C 数据类型。  (有关详细信息，请参阅 [ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。 ) 不过，不需要3.8 驱动程序来实现任何驱动程序特定的 C 类型。 但驱动程序仍应执行 C 类型的范围检查;驱动程序管理器将不会对3.8 驱动程序执行此操作。 为了便于驱动程序开发，可以按以下格式定义驱动程序特定的 C 数据类型的值：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>驱动程序特定的数据类型、描述符类型、信息类型、诊断类型和属性  
 开发新的驱动程序时，应将特定于驱动程序的范围用于数据类型、描述符类型、信息类型、诊断类型和属性。 驱动程序特定的范围及其基类型值在 [驱动程序特定的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)中进行了讨论。  
  
##### <a name="connection-pooling"></a>连接池  
 为了更好地管理连接池，ODBC 3.8 在 **SQLSetConnectAttr**中引入了 SQL_ATTR_RESET_CONNECTION 连接属性。 SQL_RESET_CONNECTION_YES 是此特性唯一有效的值。 SQL_ATTR_RESET_CONNECTION 将在驱动程序管理器将连接置于连接池中之前设置，从而允许驱动程序将其他连接属性重置为其默认值。  
  
 若要避免与服务器之间的不必要的通信，驱动程序可以在从池中重复使用连接后，将连接属性重置推迟到与远程服务器的下一次通信。  
  
 请注意，SQL_ATTR_RESET_CONNECTION 仅用于驱动程序管理器和驱动程序之间的通信。 应用程序不能直接设置此属性。 所有版本3.8 驱动程序都应该实现此连接属性。  
  
##### <a name="streamed-output-parameters"></a>流式处理输出参数  
 ODBC 版本3.8 引入了流式处理输出参数，这是一种更具伸缩性的检索输出参数的方式。  (有关详细信息，请参阅[使用 ) SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)若要支持此功能，当 SQL_GETDATA_EXTENSIONS 是**SQLGetInfo**调用中的*InfoType*时，驱动程序应在返回值中设置 SQL_GD_OUTPUT_PARAMS。 必须在驱动程序中实现对具有流式处理输出参数的 SQL 类型的支持。 对于无效的 SQL 类型，驱动程序管理器不会生成错误。 支持流式处理输出参数的 SQL 类型是在驱动程序中定义的。  
  
 如果应用程序使用 **SQLGetData** 检索的参数与 **SQLParamData**返回的参数不同，则驱动程序应返回 SQL_ERROR。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a> (轮询方法进行连接操作的异步执行)   
 驱动程序可以启用对各种连接操作的异步支持。  
  
 从 Windows 7 开始，ODBC 支持轮询方法 (有关详细信息，请参阅 [) 的异步执行 (轮询方法 ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 不需要使用版本 3.8 ODBC 驱动程序来实现对连接句柄的异步操作。 即使驱动程序未在连接句柄上实现异步操作，驱动程序也应该实现 SQL_ASYNC_DBC_FUNCTIONS *InfoType* 并返回 **SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 启用异步连接操作时，连接操作的运行时间是所有重复调用的总时间。 如果在总时间超过 SQL_ATTR_CONNECTION_TIMEOUT 连接属性设置的值，并且操作尚未完成，则该驱动程序将返回 SQL_ERROR 并记录包含 SQLState HYT01 的诊断记录和消息 "连接超时已过期"。 如果操作完成，则不会超时。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数  
 ODBC 3.8 支持用于取消连接和语句操作的 [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。 支持 **SQLCancelHandle** 的驱动程序必须导出该函数。 如果应用程序对语句句柄调用 **SQLCancel** 或 **SQLCancelHandle** ，则驱动程序不应取消正在进行的任何同步或异步连接函数。 同样，如果应用程序调用连接句柄上的 **SQLCancelHandle** ，则驱动程序不应取消正在进行的任何同步或异步语句函数。 此外，如果应用程序调用连接句柄上的**SQLCancelHandle** ，驱动程序不应取消浏览操作 (**SQLBrowseConnect**返回 SQL_NEED_DATA) 。 在这些情况下，驱动程序应返回 HY010 "函数序列错误"。  
  
 不需要同时支持 **SQLCancelHandle** 和异步连接操作。 驱动程序可以支持异步连接操作，但不支持 **SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>挂起的连接  
 ODBC 3.8 驱动程序管理器可以将连接置于挂起状态。 应用程序将调用 **SQLDisconnect** 来释放与连接关联的资源。 在这种情况下，驱动程序应尝试释放尽可能多的资源，而不检查连接状态。 有关挂起状态的详细信息，请参阅 [SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 Windows 8 中的 ODBC 允许驱动程序自定义连接池行为。 有关详细信息，请参阅 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
 ODBC 3.8 支持用于异步操作的通知方法，可从 Windows 8 开始使用。 有关详细信息，请参阅 [异步执行 (通知方法) ](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驱动程序](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
