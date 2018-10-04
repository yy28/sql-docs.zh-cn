---
title: 3.5 驱动程序升级到 3.8 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2fa8df9af317bd76b2d7f10e50f7cc937e4660
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731035"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>将 3.5 驱动程序升级到 3.8 驱动程序
本主题提供了指导原则和 ODBC 3.5 驱动程序升级到符合 ODBC 3.8 驱动程序的注意事项。  
  
##### <a name="version-numbers"></a>版本号  
 版本号与相关的以下准则：  
  
-   驱动程序应支持 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION，SQL_OV_ODBC2、 SQL_OV_ODBC3 和 SQL_OV_ODBC3_80 以外的值返回 SQL_ERROR。 未来版本的驱动程序管理器将假定一个驱动程序支持 ODBC 符合性级别，如果该驱动程序返回 SQL_SUCCESS 从[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
-   3.8 版驱动程序应返回从 03.80 **SQLGetInfo** SQL_DRIVER_ODBC_VER 传递给时*信息类型*。 但是，较旧驱动程序管理器在已包含在较旧版本的 Microsoft Windows 中，将驱动程序视为版本 3.5 驱动程序，并发出一条警告。  
  
     在 Windows 7 中，驱动程序管理器版本是 03.80。 在 Windows 8 中的驱动程序管理器版本是通过 SQLGetInfo SQL_DM_VER 03.81 (*信息类型*参数)。 SQL_ODBC_VER 报告为 03.80 Windows 7 和 Windows 8 中的版本。  
  
##### <a name="driver-specific-c-data-types"></a>特定于驱动程序的 C 数据类型  
 3.8 版的 ODBC 应用程序一起使用时，驱动程序的 C 数据类型可以进行了定制。 (有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。)但是，没有 3.8 驱动程序来实现任何特定于驱动程序的 C 类型的任何要求。 但仍应执行 C 类型; 范围检查，该驱动程序驱动程序管理器不会执行的 3.8 驱动程序。 为了便于驱动程序开发，可以采用以下格式定义驱动程序特定，C 数据类型的值：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性  
 在开发新的驱动程序时，应使用特定于驱动程序的范围的数据类型、 描述符类型、 信息类型、 诊断类型和属性。 在讨论特定于驱动程序的范围和其基类型值[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
##### <a name="connection-pooling"></a>连接池  
 更好地管理连接池，ODBC 3.8 引入了 SQL_ATTR_RESET_CONNECTION 连接属性中的**SQLSetConnectAttr**。 SQL_RESET_CONNECTION_YES 是此属性的唯一有效的值。 驱动程序管理器将连接放入连接池中，从而允许重置为其默认值的其他连接属性的驱动程序之前，将设置 SQL_ATTR_RESET_CONNECTION。  
  
 若要避免与服务器不必要的通信，驱动程序可以延迟后从池中重复使用连接重置之前的下一步与远程服务器通信的连接属性。  
  
 请注意 SQL_ATTR_RESET_CONNECTION 仅用于驱动程序管理器和驱动程序之间的通信。 应用程序不能直接设置此属性。 3.8 版的所有驱动程序应实现此连接属性。  
  
##### <a name="streamed-output-parameters"></a>流式处理的输出参数  
 ODBC 3.8 版引入流式处理的输出参数，更可缩放的方式来检索输出参数。 (有关详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。)若要支持此功能，驱动程序时应设置 SQL_GD_OUTPUT_PARAMS 返回值中 SQL_GETDATA_EXTENSIONS*信息类型*中**SQLGetInfo**调用。 必须在驱动程序中实现对具有经过流处理的输出参数的 SQL 类型的支持。 驱动程序管理器不会生成无效的 SQL 类型的错误。 驱动程序中定义支持流的输出参数的 SQL 类型。  
  
 如果使用的应用程序，驱动程序应返回 SQL_ERROR **SQLGetData**来检索参数不是返回的参数相同**SQLParamData**。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>对于连接操作 （轮询方法） 的异步执行  
 驱动程序可以启用对各种连接操作的异步支持。  
  
 从 Windows 7 开始，ODBC 支持轮询方法 (有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 没有任何要求 3.8 版的 ODBC 驱动程序实现连接句柄上的异步操作。 即使驱动程序未实现对连接句柄的异步操作时，该驱动程序仍应实现 SQL_ASYNC_DBC_FUNCTIONS*信息类型*，并返回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 如果启用了异步连接操作，连接操作的运行时间是所有的重复调用的总时间。 如果最后一个重复调用的总时间已超过 SQL_ATTR_CONNECTION_TIMEOUT 连接属性设置的值并且该操作尚未完成之后发生，驱动程序将返回 SQL_ERROR，并记录的诊断记录包含 SQLState HYT01 和消息"连接超时已过期"。 在操作完成时无超时。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数  
 支持 ODBC 3.8 [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，用于取消连接和语句的操作。 支持的驱动程序**SQLCancelHandle**必须导出该函数。 驱动程序不应取消在应用程序调用正在进行的任何同步或异步连接函数**SQLCancel**或**SQLCancelHandle**某个语句句柄。 同样，驱动程序不应取消正在进行中，如果应用程序调用任何同步或异步语句函数**SQLCancelHandle**连接句柄上。 此外，驱动程序不应取消浏览操作 (**SQLBrowseConnect**返回 SQL_NEED_DATA) 在应用程序调用**SQLCancelHandle**连接句柄上。 在这些情况下，驱动程序应返回 HY010，"函数序列错误"。  
  
 不需要支持这两个**SQLCancelHandle**和在同一时间的异步连接操作。 驱动程序可以支持异步连接操作，但不是**SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>暂停的连接  
 ODBC 3.8 驱动程序管理器可以将连接放入挂起状态。 应用程序将调用**SQLDisconnect**释放与连接关联的资源。 在这种情况下，驱动程序应尝试释放尽可能多的资源，而不检查连接状态。 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 Windows 8 中的 ODBC 允许自定义连接池行为的驱动程序。 有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
 ODBC 3.8 支持的通知方法进行异步操作，开始在 Windows 8 上提供。 有关详细信息，请参阅[异步执行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驱动程序](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
