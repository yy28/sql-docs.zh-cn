---
title: "驱动程序管理器连接池 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b589f7aa0e110767b7dca9be7aa82edee486b058
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-connection-pooling"></a>驱动程序管理器连接池
连接池可让应用程序使用的不需要为每种使用重新建立的连接池中的连接。 创建并放在池中的连接后，应用程序可以重复使用该连接，而不执行完整的连接过程。  
  
 使用已入池的连接可能会导致显著提高性能，因为应用程序可以节省的开销参与建立连接。 这可以为通过网络连接的中间层应用程序或应用程序重复连接和断开连接，如 Internet 应用程序尤其重要。  
  
 除了提高性能，连接池体系结构启用了环境和其关联的连接，以供在单个进程的多个组件。 这意味着在同一进程中的独立组件可以彼此交互，在不知道对方。 连接池中的连接可以重复使用多个组件。  
  
> [!NOTE]  
>  暴露 ODBC 2 的 ODBC 应用程序可以使用连接池。*x*行为，只要该应用程序可以调用*SQLSetEnvAttr*。 当使用连接池时，应用程序不能执行 SQL 语句更改数据库或数据库，如更改的上下文\<*数据库**名称*>，后者更改数据源使用的目录。  
  
 ODBC 驱动程序必须是完全线程安全的并且连接必须不具有线程关联，以支持连接池。 这意味着该驱动程序是能够在任何时间处理任何线程上的调用，并且能够连接上一个线程，以在另一个线程上使用连接，并且将在第三个线程上断开连接。  
  
 连接池将保留通过驱动程序管理器。 当应用程序调用连接从池中取出**SQLConnect**或**SQLDriverConnect**和时在应用程序调用返回到池中**SQLDisconnect**. 根据请求的资源分配，池大小而动态地增长。 收缩基于非活动超时： 如果连接处于非活动状态一段时间 （它具有不已连接中使用），则会从池中删除。 池的大小仅受内存约束和服务器上的限制。  
  
 驱动程序管理器确定是否应根据传入的参数使用池中的特定连接**SQLConnect**或**SQLDriverConnect**，并根据连接属性连接已分配后设置。  
  
 驱动程序管理器是建立连接池连接，它必须是能够确定连接是否仍然工作传递出连接之前。 否则，驱动程序管理器将保留在将分发到应用程序的死连接发生暂时性网络故障时。 已在 ODBC 3 定义新的连接属性*.x*: SQL_ATTR_CONNECTION_DEAD。 这是返回 SQL_CD_TRUE 或 SQL_CD_FALSE 的只读连接属性。 值 SQL_CD_TRUE 表示，该连接已丢失，而值 SQL_CD_FALSE 意味着连接仍处于活动状态。 （与早期版本的 ODBC 驱动程序还可以支持此属性。）  
  
 驱动程序必须高效地实施此选项，或它将会影响连接池性能。 具体而言，若要获取此连接属性的调用应不会导致到服务器的往返行程。 相反，驱动程序应只返回连接的最后一个已知的状态。 连接状态死如果最后一个行程到服务器失败，且不死如果最后一个行程成功。  
  
## <a name="remarks"></a>注释  
 如果连接已丢失 （通过 SQL_ATTR_CONNECTION_DEAD 报告），ODBC 驱动程序管理器将通过驱动程序中调用 SQLDisconnect 销毁该连接。 新的连接请求可能无法找到在池中可用的连接。 最终驱动程序管理器可能会使新的连接，假设该池为空。  
  
 若要使用的连接池，应用程序，请执行以下步骤：  
  
1.  启用连接池通过调用**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 环境属性设置为 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 应用程序分配的连接池是启用的共享的环境之前，必须进行此调用。 对的调用中的环境句柄**SQLSetEnvAttr**应设置为 null，这样 SQL_ATTR_CONNECTION_POOLING 了进程级别属性。 如果该属性设置为 SQL_CP_ONE_PER_DRIVER，每个驱动程序支持单个连接池。 如果应用程序与许多驱动程序和几个环境，这可能是更高效因为可能需要较少的比较。 如果设置为 SQL_CP_ONE_PER_HENV，单个连接池支持每个环境。 如果应用程序适用于很多环境和几个的驱动程序，这可能是更高效因为可能需要较少的比较。 通过将 SQL_ATTR_CONNECTION_POOLING 设置为 SQL_CP_OFF 禁用连接池。  
  
2.  通过调用分配环境**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_ENV。 此调用所分配的环境将隐式的共享的环境，因为在启用连接池。 不确定要使用的环境，但是，直到**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_DBC 上调用此环境。  
  
3.  通过调用分配连接**SQLAllocHandle**与*InputHandle*设置为 SQL_HANDLE_DBC，和*InputHandle*设为分配的环境句柄连接池。 驱动程序管理器尝试查找与匹配由应用程序设置的环境属性的现有环境。 如果不存在任何此类环境，将创建一个，引用计数 1 （由驱动程序管理器中维护）。 如果找到匹配的共享的环境，则环境返回到应用程序和其引用计数会递增。 (要使用的实际连接不确定的驱动程序管理器直到**SQLConnect**或**SQLDriverConnect**称为。)  
  
4.  调用**SQLConnect**或**SQLDriverConnect**来建立连接。 驱动程序管理器的调用中使用的连接选项**SQLConnect** (或在调用连接关键字**SQLDriverConnect**) 和连接分配到后设置连接属性确定应使用池中的连接。  
  
    > [!NOTE]  
    >  如何将请求的连接匹配共用连接到已确定 SQL_ATTR_CP_MATCH 环境属性。 有关详细信息，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用连接池的 ODBC 应用程序应调用[CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307)在应用程序初始化期间和[CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310)应用程序关闭时。  
  
5.  调用**SQLDisconnect**完成连接。 连接返回到连接池，并且可供重用。  
  
 有关深入讨论，请参阅[Microsoft 数据访问组件中的池](http://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>连接池注意事项  
 执行任何以下某项操作使用 SQL 命令 （而不是通过 ODBC API） 可以影响连接的状态，否则连接池处于活动状态时产生意外的问题：  
  
-   打开连接并更改默认数据库。  
  
-   使用 SET 语句来更改任何可配置选项 （包括 SET ROWCOUNT、 ANSI_NULL、 IMPLICIT_TRANSACTIONS、 显示计划、 统计信息、 TEXTSIZE 和 DATEFORMAT）。  
  
-   创建临时表和存储的过程。  
  
 如果 ODBC API 以外执行其中的任何操作下, 一步将使用该连接的人员将自动继承以前的设置、 表或过程。  
  
> [!NOTE]  
>  不期望某些设置，必须存在于连接状态。 你始终应在你的应用程序中设置的连接状态，并确保应用程序将删除任何未使用的连接池设置。  
  
## <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 在 Windows 8 中从开始，ODBC 驱动程序可以使用连接池中更有效地。 有关详细信息，请参阅[识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>另请参阅  
 [连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 数据访问组件中的池](http://go.microsoft.com/fwlink/?LinkId=120776)
