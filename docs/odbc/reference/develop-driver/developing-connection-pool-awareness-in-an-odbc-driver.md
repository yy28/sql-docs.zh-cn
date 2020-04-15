---
title: 在 ODBC 驱动程序中开发连接池感知 |微软文档
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
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283427"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>在 ODBC 驱动程序中开发连接池感知
本主题讨论开发 ODBC 驱动程序的详细信息，该驱动程序包含有关驱动程序应如何提供连接池服务的信息。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>启用驱动程序感知连接池  
 驱动程序必须实现以下 ODBC 服务提供商接口 （SPI） 功能：  
  
-   SQLSetConnectattrFordbcinfo  
  
-   SQLSetConnectInfo  
  
-   SQLSet驱动程序连接信息  
  
-   SQLGetPoolID  
  
-   SQLRate 连接  
  
-   SQLPool连接  
  
-   SQL 清理连接池 ID  
  
 有关详细信息[，请参阅 ODBC 服务提供商接口 （SPI） 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
 驱动程序还必须实现以下现有函数，以便启用驱动程序感知池：  
  
|函数|新增功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支持新的句柄类型：SQL_HANDLE_DBC_INFO_TOKEN（请参阅下面的说明）。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支持新的仅集连接属性：SQL_ATTR_DBC_INFO_TOKEN重置连接（请参阅下面的说明）。|  
  
> [!NOTE]  
>  弃用功能（如**SQLError**和**SQLSetConnectOption）** 不支持用于驱动程序感知连接池。  
  
## <a name="the-pool-id"></a>池 ID  
 池 ID 是一个指针长度的特定于驱动程序的 ID，用于表示可互换使用的特定连接组。 给定一组连接信息，驱动程序应该能够快速推断出相应的池 ID。  
  
 例如，池 ID 应对服务器名称和凭据信息进行编码。 但是，不需要数据库名称，因为驱动程序可能能够重用连接，然后在比建立新连接更短的时间内更改数据库。  
  
 驱动程序应定义一组关键属性，这些属性将包含池 ID。 这些关键属性的值可以来自连接属性、连接字符串和 DSN。 如果这些源中有任何冲突，则应使用现有的特定于驱动程序的解析策略来进行向后兼容性。  
  
 驱动程序管理器将使用不同的池用于不同的池。 同一池中的所有连接都是可重用的。 驱动程序管理器永远不会重用具有其他池 ID 的连接。  
  
 因此，驱动程序应为其定义的关键属性中具有相同值的每个连接组分配唯一的池 ID。 如果驱动程序对键属性中具有不同值的两个连接使用相同的池 ID，驱动程序管理器仍将将它们放入同一池（驱动程序管理器对特定于驱动程序的键属性一无所知）。 这意味着驱动程序将需要向驱动程序管理器报告，与一组其他键属性的连接在[SQLRateConnection 函数](../../../odbc/reference/syntax/sqlrateconnection-function.md)中不可重用。 这可能会降低性能，不建议这样做。  
  
 驱动程序管理器不会重用从其他驱动程序环境分配的连接，即使所有连接信息都匹配。 驱动程序管理器将针对不同的环境使用不同的池，即使连接具有相同的池 ID 也是如此。 因此，池 ID 是其驱动程序环境的本地。  
  
 从驱动程序获取池 ID 的函数是[SQLGetPoolID 函数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>连接评级  
 与建立新连接相比，您可以通过在池连接中重置某些连接信息（如 DATABASE）来获得更好的性能。 因此，您可能不希望数据库名称位于一组关键属性中。 否则，您可以为每个数据库建立一个单独的池，这在中端应用程序中可能并不好，因为客户使用不同的不同连接字符串。  
  
 每当重用具有某些属性不匹配的连接时，应基于新的应用程序请求重置不匹配的属性，以便返回的连接与应用程序请求相同（请参阅[SQLSetConnectAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59368)中SQL_ATTR_DBC_INFO_TOKEN的属性讨论）。 但是，重置这些属性可能会降低性能。 例如，重置数据库需要对服务器进行网络调用。 因此，请重用完全匹配的连接（如果有）。  
  
 驱动程序中的评级功能可以评估具有新连接请求的现有连接。 例如，驱动程序的评级功能可以确定：  
  
-   如果现有连接与请求完美匹配。  
  
-   如果只有一些微不足道的不匹配（如连接超时），则不需要与服务器通信来重置。  
  
-   如果有一些不匹配的属性需要与服务器通信来重置，但仍会比建立新连接更性能。  
  
-   如果发生不匹配的属性非常耗时的重置（驱动程序的开发人员可以考虑将此属性添加到用于生成池 ID 的密钥属性集中）。  
  
 分数介于 0 和 100 之间是可能的，其中 0 表示不重用，100 表示完全匹配。 [SQLRate 连接](../../../odbc/reference/syntax/sqlrateconnection-function.md)是用于对连接进行评级的函数。  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>新的 ODBC 句柄 - SQL_HANDLE_DBC_INFO_TOKEN  
 为了支持驱动程序感知连接池，驱动程序需要连接信息来计算池 ID。 驱动程序还需要连接信息来比较新的连接请求和池中的连接。  只要池中没有任何连接可以重用，驱动程序就必须建立新的连接，因此需要连接信息。  
  
 由于连接信息可能来自多个源（连接字符串、连接属性和 DSN），驱动程序可能需要分析连接字符串并解决上述每个函数调用中这些源之间的冲突。  
  
 因此，引入了一个新的 ODBC 句柄：SQL_HANDLE_DBC_INFO_TOKEN。 使用SQL_HANDLE_DBC_INFO_TOKEN，驱动程序不需要多次解析连接字符串并解决连接信息中的冲突。 由于这是特定于驱动程序的数据结构，驱动程序可以存储连接信息或池 ID 等数据。  
  
 此句柄仅用作驱动程序管理器和驱动程序之间的接口。 应用程序不能直接分配此句柄。  
  
 此句柄的父句柄的类型为SQL_HANDLE_ENV，这意味着驱动程序可以在连接信息解析期间从 HENV 句柄获取环境信息。  
  
 每当它收到新的连接请求时，驱动程序管理器将分配一个类型SQL_HANDLE_DBC_INFO_TOKEN的句柄，用于存储连接信息，因为它确认驱动程序支持连接池感知。 使用完该句柄后（但在从[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)返回SQL_STILL_EXECUTING以外的一些返回代码之前），驱动程序管理器将释放该句柄。 因此，句柄是在 SQLAllocHandle 调用之后创建的，并在 SQLFreeHandle 调用后销毁。 驱动程序管理器保证在释放其关联的 HENV 之前（[当 SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)返回错误时），将释放句柄。  
  
 驱动程序应修改以下函数以接受新的句柄类型SQL_HANDLE_DBC_INFO_TOKEN：  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驱动程序管理器保证多个线程不会同时使用相同的SQL_HANDLE_DBC_INFO_TOKEN句柄。 因此，此句柄的同步模型在驱动程序内部可能非常简单。 在分配和释放SQL_HANDLE_DBC_INFO_TOKEN之前，驱动程序管理器不会获取环境锁。  
  
 驱动程序管理器的**SQLAllocHandle**和**SQLFreeHandle**不会接受此新的句柄类型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN可能包含机密信息，如凭据。 因此，驱动程序应在使用**SQLFreeHandle**释放此句柄之前安全地清除包含敏感信息的内存缓冲区（使用[SecureZeroMemory）。](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx) 每当关闭应用程序的环境句柄时，将关闭所有关联的连接池。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>驱动程序管理器连接池评级算法  
 本节讨论驱动程序管理器连接池的评级算法。 驱动程序开发人员可以实现相同的算法，以实现向后兼容性。 此算法可能不是最佳算法。 您应该基于实现来优化此算法（否则，没有理由实现此功能）。  
  
 驱动程序管理器将从池中的每个连接返回从 0 到 100 的积分评级。 0 表示连接无法重复使用，100 表示完美匹配。 假设连接请求名为 hRequest，并且池中的现有连接命名为 h候选。 如果以下任一条件为 false，则池连接 h候选项不能重新用于 hRequest（驱动程序管理器将分配评级为 0）。  
  
-   h候选和 hRequest 都来自 UNICODE API（如 SQLDriverConnectW）或 ANSI API（如 SQLDriverConnectA）。 （给定 ANSI API 和 UNICODE API（请参阅连接属性SQL_ATTR_ANSI_APP），UNICODE 驱动程序可以行为不同。  
  
-   h候选和 hRequest 由同一函数创建;SQLDriver 连接或 SQLConnect。  
  
-   使用 SQLDriverConnect 时，用于打开 hAa 的连接字符串应与 hRequest 相同。  
  
-   用于打开 hAt 的服务器名称（或 DSN）、用户名和密码应与使用 SQLConnect 时用于打开 hRequest 的密码相同。  
  
-   当前线程的安全标识符 （SID） 应与用于打开 h候选项的 SID 相同。  
  
-   对于登记和取消登记费用高昂的驱动程序（请参阅[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)中有关SQL_DTC_TRANSITION_COST的讨论），重用*hRequest*不需要额外的登记或取消登记。  
  
 下表显示了不同方案的分数分配。  
  
|池连接和请求之间的连接属性比较|无登记/未登记|要求额外登记/取消登记|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|目录（SQL_ATTR_CURRENT_CATALOG）不同|60|50|  
|某些连接属性不同，但目录相同|90|70|  
|所有连接属性完美匹配|100|80|  
  
## <a name="sequence-diagram"></a>序列图  
 此序列图显示了本主题中描述的基本池机制。 它只显示[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)的使用，但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)大小写类似。  
  
 ![序列图](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状态图  
 此状态图显示连接信息令牌对象，本主题中介绍。 该关系图仅显示[SQLDriverConnect，](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)大小写类似。 由于驱动程序管理器可能需要随时处理错误，因此驱动程序管理器可以调用[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)查看任何状态。  
  
 ![状态图](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另请参阅  
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
