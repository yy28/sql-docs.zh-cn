---
description: 在 ODBC 驱动程序中开发连接池感知
title: 在 ODBC 驱动程序中开发 Connection-Pool 感知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f22be001a7434c13158deae8677b8c7bcb2f0630
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192307"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>在 ODBC 驱动程序中开发连接池感知
本主题讨论开发 ODBC 驱动程序的详细信息，该驱动程序包含有关驱动程序应如何提供连接池服务的信息。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>启用 Driver-Aware 连接池  
 驱动程序必须实现以下 ODBC 服务提供程序接口 (SPI) 函数：  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 有关详细信息，请参阅 [ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 。  
  
 驱动程序还必须实现以下现有函数，以便能够启用驱动程序感知池：  
  
|函数|新增功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支持新的句柄类型： SQL_HANDLE_DBC_INFO_TOKEN (参阅下面的说明) 。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支持新的仅限集的连接属性：用于重置连接的 SQL_ATTR_DBC_INFO_TOKEN (参阅下面的说明) "。|  
  
> [!NOTE]  
>  驱动程序感知连接池不支持不推荐使用的函数，如 **SQLError** 和 **SQLSetConnectOption** 。  
  
## <a name="the-pool-id"></a>池 ID  
 池 ID 是一个指针长度驱动程序特定的 ID，用于表示可互换使用的一组特定连接。 给定一组连接信息，驱动程序应能够快速推导相应的池 ID。  
  
 例如，池 ID 应该对服务器名称和凭据信息进行编码。 但是，数据库名称不是必需的，因为驱动程序可以重新使用连接，然后更改数据库的时间比建立新连接更少。  
  
 驱动程序应定义一组键属性，这些属性将组成池 ID。 这些键属性的值可以来自连接属性、连接字符串和 DSN。 如果这些源存在任何冲突，则应使用现有的特定于驱动程序的解析策略来实现向后兼容性。  
  
 驱动程序管理器将为不同的池 Id 使用不同的池。 同一池中的所有连接都可重复使用。 驱动程序管理器将永远不会重复使用具有不同池 ID 的连接。  
  
 因此，驱动程序应为其定义的键属性中具有相同值的每个连接组分配一个唯一的池 ID。 如果驱动程序对具有不同值的两个连接使用相同的池 ID，则驱动程序管理器仍会将其放入同一个池中 (驱动程序管理器将不知道) 的驱动程序特定的键属性。 这意味着，驱动程序将需要向驱动程序管理器报告与一组不同的键属性的连接在 [SQLRateConnection 函数](../../../odbc/reference/syntax/sqlrateconnection-function.md)中无法重用。 这可能会降低性能，不建议这样做。  
  
 即使所有连接信息匹配，驱动程序管理器也不会重复使用从另一个驱动程序环境中分配的连接。 即使连接具有相同的池 ID，驱动程序管理器也会对不同的环境使用不同的池。 因此，池 ID 在其驱动程序环境本地。  
  
 用于从驱动程序获取池 ID 的函数是 [SQLGetPoolID 函数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>连接分级  
 与建立新连接相比，可以通过重置某个连接信息 (例如，在池中连接中) 数据库来获得更好的性能。 因此，您可能不希望数据库名称位于关键属性集中。 否则，你可以为每个数据库创建一个单独的池，这在中间层应用程序中可能不适用，在该应用程序中，客户使用各种不同的连接字符串。  
  
 当你重复使用具有某个属性不匹配的连接时，你应基于新的应用程序请求重置不匹配的属性，以使返回的连接与应用程序请求相同 (请参阅 [SQLSetConnectAttr Function](../syntax/sqlsetconnectattr-function.md)) 中 SQL_ATTR_DBC_INFO_TOKEN 的属性讨论。 但是，重置这些属性可能会降低性能。 例如，重置数据库需要对服务器的网络调用。 因此，重新使用完全匹配的连接（如果有）。  
  
 驱动程序中的分级函数可以使用新的连接请求来评估现有连接。 例如，驱动程序的分级函数可以确定：  
  
-   如果现有连接与请求完全匹配，则为。  
  
-   如果只有一些无意义的不匹配，如连接超时，则不需要与服务器进行通信来重置。  
  
-   如果有一些不匹配的属性需要与服务器进行通信以重置，但仍比建立新连接的性能更好。  
  
-   如果重置 (的属性的错误发生不匹配，则驱动程序的开发人员可能会考虑将此属性添加到用于生成池 ID) 的键属性集中。  
  
 可以是0到100之间的分数，其中0表示不重复使用，100表示完全匹配。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) 是用于对连接进行评级的函数。  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>新 ODBC 句柄-SQL_HANDLE_DBC_INFO_TOKEN  
 若要支持驱动程序感知连接池，驱动程序需要连接信息来计算池 ID。 驱动程序还需要连接信息，以将新的连接请求与池中的连接进行比较。  只要池中不能重复使用连接，驱动程序就必须建立新的连接，因此需要连接信息。  
  
 由于连接信息可以来自多个源 (连接字符串、连接属性和 DSN) ，因此，驱动程序可能需要分析连接字符串，并在上述每个函数调用中解决这些源之间的冲突。  
  
 因此，会引入新的 ODBC 句柄： SQL_HANDLE_DBC_INFO_TOKEN。 使用 SQL_HANDLE_DBC_INFO_TOKEN，驱动程序无需分析连接字符串，也不需要在连接信息中多次解决冲突。 由于这是特定于驱动程序的数据结构，因此驱动程序可以存储连接信息或池 ID 等数据。  
  
 此句柄仅用作驱动程序管理器和驱动程序之间的接口。 应用程序无法直接分配此句柄。  
  
 此句柄的父句柄的类型为 SQL_HANDLE_ENV，这意味着，驱动程序可以在连接信息解析期间从 HENV 句柄获取环境信息。  
  
 每当接收到新的连接请求时，驱动程序管理器将在确定驱动程序支持连接池识别后，为存储连接信息分配一个类型 SQL_HANDLE_DBC_INFO_TOKEN 的句柄。 使用句 (柄完成后，在从 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 或 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)) 返回除 SQL_STILL_EXECUTING 以外的其他返回代码之前，驱动程序管理器将释放该句柄。 因此，在 SQLAllocHandle 调用后创建句柄，并在 SQLFreeHandle 调用之后销毁。 当 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 或 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 返回错误) 时，驱动程序管理器保证将释放该句柄，然后释放其关联的 HENV (。  
  
 驱动程序应修改以下函数，以接受新的句柄类型 SQL_HANDLE_DBC_INFO_TOKEN：  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驱动程序管理器可确保多个线程不会同时使用同一个 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 因此，此句柄的同步模式在驱动程序内可能非常简单。 在分配和释放 SQL_HANDLE_DBC_INFO_TOKEN 之前，驱动程序管理器不会执行环境锁定。  
  
 驱动程序管理器的 **SQLAllocHandle** 和 **SQLFreeHandle** 将不接受这个新的句柄类型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN 可能包含机密信息，如凭据。 因此，在使用**SQLFreeHandle**释放此句柄之前，驱动程序应使用包含敏感信息的[SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) 安全地清除内存缓冲区 (。 只要关闭应用程序的环境句柄，就会关闭所有关联的连接池。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>驱动程序管理器连接池分级算法  
 本部分讨论驱动程序管理器连接池的分级算法。 为了向后兼容，驱动程序开发人员可以实现相同的算法。 此算法可能不是最好的算法。 你应根据实现优化此算法 (否则，没有理由实现此功能) 。  
  
 对于来自池的每个连接，驱动程序管理器将从0到100返回整数评分。 0表示不能重复使用连接，100表示完全匹配。 假定连接请求命名为 hRequest，并且池中的现有连接命名为 hCandidate。 如果以下任一条件为 false，则 hCandidate 不能为 (hRequest 重复使用池连接，因为驱动程序管理器会将等级分配为 0) 。  
  
-   hCandidate 和 hRequest 都来自 UNICODE API (例如 SQLDriverConnectW) 或 ANSI API (如 SQLDriverConnectA) 。  (UNICODE 驱动程序可能会表现出不同的给定 ANSI API 和 UNICODE API (请参阅 SQL_ATTR_ANSI_APP) 的连接属性。 )   
  
-   hCandidate 和 hRequest 由同一个函数创建;SQLDriverConnect 或 SQLConnect。  
  
-   使用 SQLDriverConnect 时，用于打开 hCandidate 的连接字符串应与 hRequest 相同。  
  
-   用于打开 hCandidate 的 ServerName (或 DSN) 、用户名和密码应该与在使用 SQLConnect 时用于打开 hRequest 的用户名和密码相同。  
  
-   当前线程 (SID) 的安全标识符应与用于打开 hCandidate 的 SID 相同。  
  
-   对于登记和取消登记成本较高的驱动程序 (参阅 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)) 中 SQL_DTC_TRANSITION_COST 的讨论，重用 *hRequest* 不一定需要额外的登记或 unenlistment。  
  
 下表显示了不同方案的分数分配。  
  
|池连接和请求之间的连接属性比较|无登记/unenlistment|需要额外的登记/Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|目录 (SQL_ATTR_CURRENT_CATALOG) 不同|60|50|  
|某些连接属性有所不同，但目录是相同的|90|70|  
|完全匹配的所有连接属性|100|80|  
  
## <a name="sequence-diagram"></a>序列图  
 此顺序图显示了本主题中描述的基本池机制。 它仅显示 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 的使用，但 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 大小写类似。  
  
 ![序列图](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状态图  
 此状态图显示了本主题中描述的连接信息令牌对象。 该图只显示 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ，但 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 大小写类似。 由于驱动程序管理器可能需要随时处理错误，因此，驱动程序管理器可以为任何状态调用 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 。  
  
 ![状态图](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另请参阅  
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)