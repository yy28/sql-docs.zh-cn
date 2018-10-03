---
title: 驱动程序管理器连接池 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e03932fe9d6cc98648c2e0da2e2cdd963a8d67f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826131"
---
# <a name="driver-manager-connection-pooling"></a>驱动程序管理器连接池
连接池使应用程序能够从无需每次使用重新建立的连接池使用连接。 一旦创建并放入池连接，应用程序可以重复使用该连接，而不执行整个连接过程。  
  
 使用已入池的连接可能会导致显著的性能提升，因为应用程序可以保存在建立连接所涉及的开销。 这可以是特别大的中间层应用程序通过网络连接或反复连接和断开连接，如 Internet 应用程序的应用程序。  
  
 除了获得性能提升，连接池体系结构还允许的环境和其关联的连接以供在单个进程中的多个组件。 这意味着在同一进程中的独立组件可以彼此交互，而能够相互识别。 通过多个组件，可以重复使用的连接池中的连接。  
  
> [!NOTE]  
>  暴露 ODBC 2 ODBC 应用程序可以使用连接池。*x*行为，只要应用程序可以调用*SQLSetEnvAttr*。 当使用连接池时，应用程序必须执行 SQL 语句更改数据库或数据库，如更改的上下文\<*数据库 * * 名称*>，这将更改使用的目录数据源。  
  
 ODBC 驱动程序必须是完全线程安全的并且连接必须具有线程关联，以支持连接池。 这意味着该驱动程序能够在任何时候处理任何线程上的调用，并且能够连接上一个线程，另一个线程上使用的连接，并且第三个线程上断开连接。  
  
 连接池维护的驱动程序管理器。 当应用程序调用时连接从池中取出**SQLConnect**或**SQLDriverConnect**并返回到池时在应用程序调用**SQLDisconnect**. 基于请求的资源分配，池的大小会动态地增大。 收缩根据非活动超时： 如果连接处于非活动状态一段时间 （不使用连接中），它从池中删除。 池的大小仅受内存限制和在服务器上的限制。  
  
 驱动程序管理器确定是否应根据传入的参数使用特定的连接池中**SQLConnect**或**SQLDriverConnect**，而是根据连接属性连接已分配后设置。  
  
 当驱动程序管理器池连接时，它需要能够确定连接是否仍然工作之前分发连接。 否则，驱动程序管理器保留在分发应用程序的死信连接出现暂时性网络故障时。 已在 ODBC 3 中定义了一个新的连接属性 *.x*: SQL_ATTR_CONNECTION_DEAD。 这是一个只读的连接属性，返回 SQL_CD_TRUE 或 SQL_CD_FALSE。 值 SQL_CD_TRUE 表示，该连接已丢失，而值 SQL_CD_FALSE 表示该连接仍处于活动状态。 （与早期版本的 ODBC 驱动程序还可以支持此属性。）  
  
 驱动程序必须有效地实现此选项，或它将会影响连接池的性能。 具体而言，若要获取此连接属性的调用不会导致到服务器的往返行程。 相反，驱动程序只应返回连接的最后已知的状态。 如果最后一个行程到服务器失败，退出历史舞台并不死，如果最后一个行程成功连接。  
  
## <a name="remarks"></a>备注  
 如果连接已丢失 （通过 SQL_ATTR_CONNECTION_DEAD 报告），ODBC 驱动程序管理器会通过驱动程序中调用 SQLDisconnect 销毁该连接。 新的连接请求可能无法找到在池中可用的连接。 最终驱动程序管理器可能会使新的连接，假定该池为空。  
  
 若要使用连接池，应用程序，请执行以下步骤：  
  
1.  启用连接池通过调用**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 环境属性设置为 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 应用程序分配的连接池是要启用的共享的环境之前，必须进行此调用。 对的调用中的环境句柄**SQLSetEnvAttr**应设置为 null，这使得 SQL_ATTR_CONNECTION_POOLING 进程级别属性。 如果该属性设置为 SQL_CP_ONE_PER_DRIVER，每个驱动程序支持单个连接池。 如果应用程序适用于许多驱动程序和几个环境，这可能是更高效因为可能需要较少的比较。 如果设置为 SQL_CP_ONE_PER_HENV，单个连接池支持的每个环境中。 如果应用程序适用于很多环境和几个的驱动程序，这可能是更高效因为可能需要较少的比较。 通过设置 SQL_ATTR_CONNECTION_POOLING 为 SQL_CP_OFF 禁用连接池。  
  
2.  通过调用分配一个环境**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_ENV。 此调用分配的环境将隐式的共享的环境，因为已启用连接池。 不确定要使用的环境，但是，直到**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 上调用此环境。  
  
3.  通过调用分配连接**SQLAllocHandle**与*InputHandle*设置为 SQL_HANDLE_DBC，和*InputHandle*设为分配环境句柄连接池。 驱动程序管理器尝试查找匹配应用程序设置的环境属性的现有环境。 如果不存在任何此类环境，创建一个，引用计数 1 （维护的驱动程序管理器）。 如果找到匹配的共享的环境，环境返回到应用程序和其引用计数会递增。 (要使用的实际连接不确定的驱动程序管理器直到**SQLConnect**或**SQLDriverConnect**称为。)  
  
4.  调用**SQLConnect**或**SQLDriverConnect**来建立连接。 驱动程序管理器对的调用中使用的连接选项**SQLConnect** (或在调用连接关键字**SQLDriverConnect**) 并连接到分配后设置连接属性确定应使用哪个连接池中。  
  
    > [!NOTE]  
    >  请求的连接到已入池连接的匹配方式取决于 SQL_ATTR_CP_MATCH 环境属性。 有关详细信息，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用连接池的 ODBC 应用程序应调用[CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307)在应用程序初始化期间和[CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310)应用程序关闭时。  
  
5.  调用**SQLDisconnect**完成连接。 连接返回到连接池，并且变得可供重复使用。  
  
 有关深入的讨论，请参阅[Microsoft 数据访问组件中的池](http://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>连接池的注意事项  
 执行任何以下操作使用 SQL 命令 （而不是通过 ODBC API） 可以影响连接的状态，并会导致意外的问题，连接池处于活动状态时：  
  
-   打开连接并更改默认数据库。  
  
-   使用 SET 语句更改任何可配置选项 （包括 SET ROWCOUNT、 ANSI_NULL、 IMPLICIT_TRANSACTIONS、 显示计划、 统计信息、 TEXTSIZE 和日期格式）。  
  
-   创建临时表和存储的过程。  
  
 如果其中的任何操作执行 ODBC API 之外下, 一步将使用该连接的人员将自动继承以前的设置、 表或过程。  
  
> [!NOTE]  
>  不希望某些设置必须存在处于连接状态。 应始终在你的应用程序中设置的连接状态并确保应用程序中删除任何未使用的连接池设置。  
  
## <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 从 Windows 8 开始，ODBC 驱动程序可以使用连接池中更高效。 有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>请参阅  
 [连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 数据访问组件中的池](http://go.microsoft.com/fwlink/?LinkId=120776)
