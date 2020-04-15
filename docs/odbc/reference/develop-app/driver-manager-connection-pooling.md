---
title: 驱动程序管理器连接池 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305818"
---
# <a name="driver-manager-connection-pooling"></a>驱动程序管理器连接池
连接池使应用程序能够使用连接池中的连接，而不需要为每个使用重新建立连接池。 创建连接并将其放置在池中后，应用程序可以重用该连接，而无需执行完整的连接过程。  
  
 使用池连接可以显著提高性能，因为应用程序可以节省进行连接所涉及的开销。 对于通过网络连接的中间层应用程序或重复连接和断开连接的应用程序（如 Internet 应用程序）来说，这一点尤其重要。  
  
 除了性能提升之外，连接池体系结构还允许环境及其关联连接在单个进程中由多个组件使用。 这意味着同一进程中的独立组件可以相互交互，而不必相互了解。 连接池中的连接可以由多个组件反复使用。  
  
> [!NOTE]
>  显示 ODBC 2 的 ODBC 应用程序可以使用连接池。*x*行为，只要应用程序可以调用*SQLSetEnvAttr*。 使用连接池时，应用程序不得执行更改数据库或数据库上下文的 SQL 语句，例如更改\<*数据库名称*>更改数据源使用的目录。  


 ODBC 驱动程序必须完全线程安全，并且连接不能具有线程关联以支持连接池。 这意味着驱动程序能够随时处理任何线程上的调用，并能够在一个线程上连接、在另一个线程上使用连接以及断开第三个线程的连接。  
  
 连接池由驱动程序管理器维护。 当应用程序调用**SQLConnect**或**SQLDriverConnect**时，连接从池中绘制，并在应用程序调用**SQLDisconnect**时返回到池中。 池的大小根据请求的资源分配动态增长。 它根据非活动超时收缩：如果连接在一段时间内处于非活动状态（在连接中未使用），则从池中删除连接。 池的大小仅受内存约束和服务器上的限制的限制。  
  
 驱动程序管理器确定是否应根据**SQLConnect**或**SQLDriverConnect**中传递的参数以及分配连接后设置的连接属性使用池中的特定连接。  
  
 当驱动程序管理器正在池连接时，它需要能够在分发连接之前确定连接是否仍在工作。 否则，每当发生暂时性网络故障时，驱动程序管理器会继续将死连接分发到应用程序。 在 ODBC 3 *.x*： SQL_ATTR_CONNECTION_DEAD 中定义了新的连接属性。 这是一个只读连接属性，返回SQL_CD_TRUE或SQL_CD_FALSE。 值SQL_CD_TRUE表示连接已丢失，而值SQL_CD_FALSE表示连接仍然处于活动状态。 （符合早期版本的 ODBC 的驱动程序也可以支持此属性。  
  
 驱动程序必须有效地实现此选项，否则将损害连接池性能。 具体而言，获取此连接属性的调用不应导致服务器的往返行程。 相反，驱动程序应仅返回连接的最后已知状态。 如果上次服务器访问失败，则连接已死，如果上次访问成功，连接不会死。  
  
## <a name="remarks"></a>备注  
 如果连接已丢失（通过SQL_ATTR_CONNECTION_DEAD报告），ODBC 驱动程序管理器将通过在驱动程序中调用 SQLDisconnect 来破坏该连接。 新的连接请求可能无法在池中找到可用的连接。 最终，假设池为空，驱动程序管理器可能会建立新的连接。  
  
 要使用连接池，应用程序将执行以下步骤：  
  
1.  通过调用**SQLSetEnvAttr**将SQL_ATTR_CONNECTION_POOLING环境属性设置为SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV，从而启用连接池。 在应用程序分配要为其启用连接池的共享环境之前，必须进行此调用。 对**SQLSetEnvAttr**调用中的环境句柄应设置为 null，这使得SQL_ATTR_CONNECTION_POOLING进程级属性。 如果属性设置为SQL_CP_ONE_PER_DRIVER，则每个驱动程序支持单个连接池。 如果应用程序与许多驱动程序和很少的环境一起工作，则这可能更有效率，因为可能需要较少的比较。 如果设置为SQL_CP_ONE_PER_HENV，则每个环境都支持单个连接池。 如果应用程序与许多环境和很少的驱动程序一起工作，则这可能更有效率，因为可能需要较少的比较。 通过将SQL_ATTR_CONNECTION_POOLING设置为SQL_CP_OFF，将禁用连接池。  
  
2.  通过将*句柄类型*参数设置为SQL_HANDLE_ENV调用**SQLAllocHandle**来分配环境。 此调用分配的环境将是隐式共享环境，因为连接池已启用。 但是，在此环境中调用具有*SQL_HANDLE_DBC*的**SQLAllocHandle，** 才能确定要使用的环境。  
  
3.  通过将**SQLAllocHandle**与*输入句柄*设置为 SQL_HANDLE_DBC，并将*InputHandle*设置为分配给连接池的环境句柄来分配连接。 驱动程序管理器尝试查找与应用程序设置的环境属性匹配的现有环境。 如果不存在此类环境，则创建一个环境，引用计数（由驱动程序管理器维护）为 1。 如果找到匹配的共享环境，环境将返回到应用程序，其引用计数将递增。 （在调用**SQLConnect**或**SQLDriverConnect**之前，驱动程序管理器不会确定要使用的实际连接。  
  
4.  调用**SQLConnect**或**SQLDriverConnect**进行连接。 驱动程序管理器在调用**SQLConnect**时使用连接选项（或**SQLDriverConnect**调用中的连接关键字）和连接分配后设置的连接属性来确定应在池中使用哪个连接。  
  
    > [!NOTE]  
    >  请求的连接如何与池连接匹配由SQL_ATTR_CP_MATCH环境属性确定。 有关详细信息，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用连接池的 ODBC 应用程序应在应用程序初始化期间调用[Co初始化Ex，](https://go.microsoft.com/fwlink/?LinkID=116307)并在应用程序关闭时调用[CoUn 初始化](https://go.microsoft.com/fwlink/?LinkId=116310)。  
  
5.  使用连接完成后调用**SQL 断开连接**。 连接返回到连接池，并可供重用。  
  
 有关深入讨论，请参阅在[Microsoft 数据访问组件中进行池化](https://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>连接池注意事项  
 使用 SQL 命令执行以下任一操作（而不是通过 ODBC API）可能会影响连接的状态，并在连接池处于活动状态时导致意外问题：  
  
-   打开连接并更改默认数据库。  
  
-   使用 SET 语句更改任何可配置选项（包括设置、ANSI_NULL、IMPLICIT_TRANSACTIONS、SHOWPLAN、STATISTICS、TEXTSIZE 和日期格式）。  
  
-   创建临时表和存储过程。  
  
 如果其中任何一个操作是在 ODBC API 之外执行的，则使用连接的下一个人将自动继承以前的设置、表或过程。  
  
> [!NOTE]  
>  不要期望某些设置处于连接状态。 应始终在应用程序中设置连接状态，并确保应用程序删除任何未使用的连接池设置。  
  
## <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
 从 Windows 8 开始，ODBC 驱动程序可以更有效地使用池中的连接。 有关详细信息，请参阅[驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>另请参阅  
 [连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [在 Microsoft 数据访问组件中进行池化](https://go.microsoft.com/fwlink/?LinkId=120776)
