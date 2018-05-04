---
title: 开发中的 ODBC 驱动程序的连接池感知 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4290b77a54057bdbeea4c4d4864b469dba782317
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>开发中的 ODBC 驱动程序的连接池感知
本主题讨论开发 ODBC 驱动程序，其中包含有关该驱动程序应如何提供连接池的服务的信息的详细信息。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>启用识别驱动程序的连接池  
 驱动程序必须实现以下的 ODBC 服务提供程序接口 (SPI) 函数：  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 请参阅[ODBC 服务提供程序接口 (SPI) 引用](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)有关详细信息。  
  
 驱动程序还必须实现以下现有函数，以便可以启用识别驱动程序的池：  
  
|函数|新增的功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支持新的句柄类型： SQL_HANDLE_DBC_INFO_TOKEN （请参阅下面的说明）。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支持新的仅连接属性： SQL_ATTR_DBC_INFO_TOKEN 用于重置连接 （请参阅下面的说明）。|  
  
> [!NOTE]  
>  如弃用函数**SQLError**和**SQLSetConnectOption**不支持识别驱动程序的连接池。  
  
## <a name="the-pool-id"></a>池 ID  
 池 ID 是一个指针长度特定于驱动程序 ID，以表示一组特定的可互换的连接。 给定的连接信息的一组，驱动程序应该能够快速推断出相应的池 id。  
  
 例如，池 ID 应该对服务器名称和凭据信息进行编码。 但是，不需要数据库名称，因为驱动程序可能能够重复使用的连接，然后将数据库更改时间比建立新连接更短。  
  
 驱动程序应定义一组键属性，将构成池 id。 这些键属性的值可以来自连接特性、 连接字符串和 DSN。 当在这些源中有任何冲突，现有的驱动程序特定的解决策略应用于向后兼容性。  
  
 驱动程序管理器将使用不同的池 Id 不同的池。 在同一池中的所有连接都是可重复使用。 驱动程序管理器将永远不会重复使用的连接替换为不同的池 id。  
  
 因此驱动程序应为其定义键属性中的相同值的连接的每个组的唯一池 ID 分配。 如果驱动程序使用相同的池 ID 具有其密钥特性中的不同值的两个连接，驱动程序管理器会仍将它们置于相同的池 （驱动程序管理器不知道有关的特定于驱动程序键属性）。 这意味着该驱动程序将需要向驱动程序管理器报告与一组不同的键属性的连接不在可重用[SQLRateConnection 函数](../../../odbc/reference/syntax/sqlrateconnection-function.md)。 这会降低性能，这不推荐。  
  
 驱动程序管理器将不可以重用分配从另一个驱动程序环境中，即使所有连接信息与都匹配的连接。 驱动程序管理器将为另一个环境，使用不同的池，即使连接具有相同的池 id。 因此，池 ID 是本地到其驱动程序环境。  
  
 获取池 ID 的驱动程序中的函数是[SQLGetPoolID 函数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>连接分级  
 与建立新连接相比，你可以通过重置一些连接信息 （如数据库） 中的共用连接来获取更好的性能。 因此，可能不想要在键属性的集中的数据库名称。 否则，你可以单独的池的每个数据库，可能不能很好中间层应用程序中，客户在其中使用各种不同的连接字符串。  
  
 每当你重复使用具有某些属性不匹配的连接，您应重置不匹配的属性基于新的应用程序请求，以便返回的连接等同于应用程序请求 （请参阅属性 SQL_ATTR 的讨论中的 _DBC_INFO_TOKEN [SQLSetConnectAttr 函数](http://go.microsoft.com/fwlink/?LinkId=59368))。 但是，重置这些属性可能会降低性能。 例如，重置数据库需要对服务器的网络调用。 如果有的话，因此，重复使用完全匹配的连接。  
  
 驱动程序中的分级函数可以计算的现有连接使用的新连接请求。 例如，可以确定驱动程序的分级函数：  
  
-   如果请求完全匹配的现有连接。  
  
-   如果仅某些无意义不匹配，例如连接超时，这不需要与要重置的服务器的通信。  
  
-   如果有一些不匹配的属性，要求与要重置的服务器的通信，但仍将导致更好的性能比建立新连接。  
  
-   如果不匹配发生非常耗时，若要重置的属性 （该驱动程序的开发人员可以考虑将此特性添加到集中的键属性，用来生成池 ID）。  
  
 介于 0 和 100 之间的分数是有可能，其中 0 表示不要重复使用，100 表示完全匹配。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)是评级连接的函数。  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>新 ODBC 句柄-SQL_HANDLE_DBC_INFO_TOKEN  
 若要支持识别驱动程序的连接池，该驱动程序必须连接信息来计算池的 id。 该驱动程序还必须用于比较与池中的连接的新连接请求的连接信息。  只要可以重用池中没有连接，驱动程序必须建立新连接，因此需要连接信息。  
  
 由于连接信息可能来自多个源 （连接字符串、 连接属性和 DSN），该驱动程序可能需要分析连接字符串并解决每个以上的函数调用了这些源之间的冲突。  
  
 因此，引入新的 ODBC 句柄： SQL_HANDLE_DBC_INFO_TOKEN。 与 SQL_HANDLE_DBC_INFO_TOKEN，驱动程序不需要用于分析连接字符串和不止一次解析连接信息中的冲突。 由于这是特定于驱动程序的数据结构，该驱动程序可以存储数据，如连接信息或池 id。  
  
 此句柄仅用作驱动程序管理器和驱动程序之间的接口。 应用程序无法直接分配此句柄。  
  
 此句柄的父句柄是类型 SQL_HANDLE_ENV，这意味着，该驱动程序可以从获得的环境信息 HENV 句柄在连接信息解析期间。  
  
 在收到的新连接请求，驱动程序管理器将用于存储连接信息后它确认的驱动程序支持连接池感知分配类型 SQL_HANDLE_DBC_INFO_TOKEN 的句柄。 在完成后使用此句柄 (但在返回之前某些会返回从 SQL_STILL_EXECUTING 以外的代码[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))，驱动程序管理器将释放句柄。 因此，该句柄都会在 SQLAllocHandle 调用后，创建和销毁 SQLFreeHandle 调用后。 驱动程序管理器可保证句柄会被释放之前释放其关联的 HENV (时[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)返回错误)。  
  
 该驱动程序应修改以下函数以接受新的句柄类型 SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驱动程序管理器可保证多个线程将同时使用相同的 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 因此，此句柄的同步模型可以是驱动程序内非常简单。 驱动程序管理器将不会在分配和释放 SQL_HANDLE_DBC_INFO_TOKEN 之前的环境锁。  
  
 驱动程序管理器的**SQLAllocHandle**和**SQLFreeHandle**将不接受此新的句柄类型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN 可能包含机密信息，例如凭据。 因此，驱动程序安全地应清除内存缓冲区 (使用[SecureZeroMemory](http://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx))，其中包含敏感信息之前释放此句柄**SQLFreeHandle**。 每当应用程序的环境句柄已关闭，所有关联的连接池将被关闭。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>评级算法的驱动程序管理器连接池  
 本部分讨论驱动程序管理器连接池的分级算法。 驱动程序开发人员可以实现向后兼容性的相同算法。 此算法可能不是最佳的一个。 你需要优化此算法基于您的实现 （否则，将没有理由来实现此功能）。  
  
 驱动程序管理器将返回整数级别从 0 到 100 为每个连接从池中。 0 表示不能重复使用的连接，100 表示完全匹配。 假定连接请求名为 hRequest 和现有连接从池中命名为 hCandidate。 如果任一以下条件为 false，则不能共用的连接 hCandidate 重新用于 hRequest （驱动程序管理器将分配的分级 0）。  
  
-   hCandidate 和 hRequest 都来自于 UNICODE API （如 SQLDriverConnectW) 或 ANSI API （如 SQLDriverConnectA)。 （UNICODE 驱动程序可以在给定 （请参阅连接属性 SQL_ATTR_ANSI_APP） 的 ANSI API 和 UNICODE API 的行为不同。）  
  
-   相同的函数; 创建 hCandidate 和 hRequestSQLDriverConnect 或 SQLConnect 中。  
  
-   使用 SQLDriverConnect 时，用来打开 hCandidate 的连接字符串应为 hRequest，相同。  
  
-   ServerName （或 DSN），用户名和密码用于打开 hCandidate 应为相同的用来打开 hRequest 使用 SQLConnect 时。  
  
-   因为 SID 用于打开 hCandidate，当前线程的安全标识符 (SID) 应相同。  
  
-   登记，并取消登记成本较高的驱动程序 (请参阅中的 SQL_DTC_TRANSITION_COST 讨论[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))、 重复使用*hRequest*必须不需要额外的登记或征用。  
  
 下表显示不同的方案的分数分配。  
  
|已入池的连接与请求之间的连接属性的比较|任何登记 / 征用|需要额外的登记 / 征用|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|目录 (SQL_ATTR_CURRENT_CATALOG) 是不同|60|50|  
|连接中的某些属性是不同，但目录是相同的|90|70|  
|完全匹配的所有连接属性|100|80|  
  
## <a name="sequence-diagram"></a>序列图  
 此序列图演示本主题中所述的基本池机制。 它仅演示了如何使用[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)用例是类似。  
  
 ![序列关系图](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状态图  
 此状态图显示的连接信息令牌对象，本主题中所述。 关系图只显示[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)用例是类似。 驱动程序管理器由于驱动程序管理器可能需要在任何时间处理错误，可以调用[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)的任何状态。  
  
 ![状态图](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另请参阅  
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
