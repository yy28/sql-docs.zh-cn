---
title: 升级到 3.8 驱动程序的 3.5 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4341ee550c098ce8309eefc8dcbc5cc4e026048c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32919122"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>升级到 3.8 驱动程序的 3.5 驱动程序
本主题提供的指导原则和 ODBC 3.5 驱动程序升级到 ODBC 3.8 驱动程序的注意事项。  
  
##### <a name="version-numbers"></a>版本号  
 版本号与相关的以下准则：  
  
-   驱动程序应支持 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION，返回 SQL_ERROR SQL_OV_ODBC2、 SQL_OV_ODBC3 和 SQL_OV_ODBC3_80 以外的值。 将来版本的驱动程序管理器将假定驱动程序支持 ODBC 符合性级别，如果驱动程序返回从 SQL_SUCCESS [SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
-   3.8 版驱动程序应返回从 03.80 **SQLGetInfo**当 SQL_DRIVER_ODBC_VER 传递给*信息类型*。 但是，较旧的驱动程序管理器已包括在较旧版本的 Microsoft Windows 中，将视为版本 3.5 驱动程序，该驱动程序，并发出警告。  
  
     在 Windows 7 中，驱动程序管理器版本为 03.80。 在 Windows 8 中，驱动程序管理器版本是通过 SQLGetInfo SQL_DM_VER 03.81 (*信息类型*参数)。 SQL_ODBC_VER 报告为 03.80 Windows 7 和 Windows 8 中的版本。  
  
##### <a name="driver-specific-c-data-types"></a>特定于驱动程序的 C 数据类型  
 驱动程序可以自定义 C 数据类型与 3.8 版 ODBC 应用程序一起使用时。 (有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。)但是，没有 3.8 驱动程序来实施任何特定于驱动程序的 C 类型的任何要求。 但该驱动程序仍应执行的 C 类型; 范围检查驱动程序管理器将不执行该操作 3.8 驱动程序。 为了便于驱动程序开发，驱动程序的特定，C 数据类型的值可定义采用以下格式：  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性  
 当开发新的驱动程序，应使用数据类型、 描述符类型、 信息类型、 诊断类型和属性的特定于驱动程序的范围。 中讨论了特定于驱动程序的范围和其基类型值[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
##### <a name="connection-pooling"></a>连接池  
 对于更好地管理连接池，ODBC 3.8 引入了中的 SQL_ATTR_RESET_CONNECTION 连接属性**SQLSetConnectAttr**。 SQL_RESET_CONNECTION_YES 是此属性的唯一有效的值。 驱动程序管理器将连接放入连接池，允许重置为其默认值的其他连接属性的驱动程序之前，将设置 SQL_ATTR_RESET_CONNECTION。  
  
 若要避免与服务器不必要的通信，驱动程序可以延迟后从池中重复使用连接与远程服务器的下一步通信之前重置连接属性。  
  
 请注意 SQL_ATTR_RESET_CONNECTION 仅用在驱动程序管理器和驱动程序之间的通信。 应用程序不能直接设置此属性。 3.8 版的所有驱动程序应实现此连接属性。  
  
##### <a name="streamed-output-parameters"></a>流式处理的输出参数  
 ODBC 3.8 版引入流的输出参数，更具伸缩性的方式来检索输出参数。 (有关详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。)若要支持此功能，驱动程序时，应设置 SQL_GD_OUTPUT_PARAMS 返回值中 SQL_GETDATA_EXTENSIONS 是*信息类型*中**SQLGetInfo**调用。 必须驱动程序中实现对具有经过流处理的输出参数的 SQL 类型的支持。 驱动程序管理器将不会生成错误的 SQL 类型无效。 驱动程序中定义支持流式处理的输出参数的 SQL 类型。  
  
 如果使用的应用程序，驱动程序应返回 SQL_ERROR **SQLGetData**检索不通过返回的参数相同的参数**SQLParamData**。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>用于连接操作 （轮询方法） 的异步执行  
 驱动程序可以启用对各种连接操作的异步支持。  
  
 从 Windows 7 开始，ODBC 支持轮询方法 (有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 没有要实现对连接句柄的异步操作的 3.8 版 ODBC 驱动程序，要求。 即使驱动程序未实现对连接句柄的异步操作，该驱动程序应仍实现 SQL_ASYNC_DBC_FUNCTIONS*信息类型*并返回**SQL_ASYNC_DBC_NOT_CAPABLE**。  
  
 启用异步连接操作后，连接操作的运行时间将是所有的重复调用的总时间。 如果最后一个重复调用的总时间已超过 SQL_ATTR_CONNECTION_TIMEOUT 连接属性，设置的值并且在操作完成后不之后发生，该驱动程序返回 SQL_ERROR 和使用 SQLState HYT01 记录诊断记录和消息"连接超时已过期"。 如果该操作完成，则无超时。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函数  
 ODBC 3.8 支持[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，用于取消连接和语句的操作。 支持的驱动程序**SQLCancelHandle**必须导出该函数。 驱动程序不应取消正在进行，如果应用程序调用的任何同步或异步连接函数**SQLCancel**或**SQLCancelHandle**在语句句柄。 同样，驱动程序不应取消正在进行，如果应用程序调用的任何同步或异步语句函数**SQLCancelHandle**连接句柄上。 此外，驱动程序不应取消浏览操作 (**SQLBrowseConnect**返回 SQL_NEED_DATA) 如果在应用程序调用**SQLCancelHandle**连接句柄上。 在这些情况下，驱动程序应返回 HY010，"函数序列错误"。  
  
 不需要支持这两个**SQLCancelHandle**和同时异步连接操作。 驱动程序可以支持异步连接操作但不是**SQLCancelHandle**，反之亦然。  
  
##### <a name="suspended-connections"></a>暂停的连接  
 ODBC 3.8 驱动程序管理器可以将连接放到挂起状态。 应用程序将调用**SQLDisconnect**释放与连接关联的资源。 在这种情况下，驱动程序应尝试尽可能释放尽可能多的资源，而不检查连接状态。 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
##### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 Windows 8 中的 ODBC 允许可自定义连接池行为的驱动程序。 有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
##### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
 ODBC 3.8 支持可在 Windows 8 上开始的异步操作的通知方法。 有关详细信息，请参阅[异步执行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供的 ODBC 驱动程序](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
