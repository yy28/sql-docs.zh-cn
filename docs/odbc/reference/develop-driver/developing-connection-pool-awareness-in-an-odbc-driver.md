---
title: 开发中的 ODBC 驱动程序的连接池感知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a7a38a3d71b28cc32b863bf95ca6b99fa2bddaa
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661746"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>在 ODBC 驱动程序中开发连接池感知
本主题讨论开发包含有关该驱动程序应如何提供连接池的服务的信息的 ODBC 驱动程序的详细信息。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>启用识别驱动程序的连接池  
 驱动程序必须实现以下 ODBC 服务提供程序接口 (SPI) 函数：  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 请参阅[ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)有关详细信息。  
  
 驱动程序还必须实现以下现有函数，以便可以启用识别驱动程序的池：  
  
|函数|添加了的功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支持新的句柄类型： SQL_HANDLE_DBC_INFO_TOKEN （请参阅下面的说明）。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支持新的仅限集的连接属性： 用于重置连接 SQL_ATTR_DBC_INFO_TOKEN （请参阅下面的说明）。|  
  
> [!NOTE]  
>  已弃用的函数，如**SQLError**并**SQLSetConnectOption**不支持识别驱动程序的连接池。  
  
## <a name="the-pool-id"></a>池 ID  
 池 ID 是一个指针长度特定于驱动程序的 ID，以表示一组特定的可互换使用的连接。 给定一组连接信息，驱动程序应该能够快速推导出相应的池 id。  
  
 例如，池 ID 应该对服务器名称和凭据信息进行编码。 但是，不需要数据库名称，因为驱动程序可能能够重复使用的连接，然后将数据库更改更少的时间比建立新连接。  
  
 驱动程序应定义一组键属性，将包含池 id。 这些键属性的值可以来自连接属性、 连接字符串和 DSN。 如果在这些源中有任何冲突，现有的驱动程序特定的解决策略应该用于向后兼容性。  
  
 驱动程序管理器将使用不同的池 Id 不同的池。 在同一个池中的所有连接都是可重复使用。 驱动程序管理器将永远不会重复使用的连接使用不同的池 id。  
  
 因此驱动程序应分配与中其定义键属性的值相同的连接的每个组的唯一池 ID。 如果驱动程序使用相同的池 ID 具有不同值中其键属性的两个连接，驱动程序管理器将仍放入同一个池中 （驱动程序管理器知道有关特定于驱动程序的关键属性执行任何操作）。 这意味着该驱动程序将需要向驱动程序管理器报告与一组不同的键属性的连接不是在可重用[SQLRateConnection 函数](../../../odbc/reference/syntax/sqlrateconnection-function.md)。 这可能会降低性能，建议不这样做。  
  
 驱动程序管理器不会再分配从另一个驱动程序环境，即使所有连接信息与都匹配的连接。 驱动程序管理器将针对不同的环境，使用不同的池，即使连接具有相同的池 id。 因此，是其驱动程序环境的本地池 ID。  
  
 从驱动程序获取池 ID 的函数是[SQLGetPoolID 函数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>连接级别  
 与建立新连接相比，可以通过重置一些 （如数据库） 中已入池连接的连接信息来获取更好的性能。 因此，您可能不希望要在集中的键属性的数据库名称。 否则，您可以有一个单独的池的每个数据库，这可能不会在中间层应用程序中的客户在其中使用各种不同的连接字符串。  
  
 每当你重复使用具有某些属性不匹配的连接，以便返回的连接是与应用程序请求相同，则应重置基于新的应用程序请求的不匹配的属性 （请参阅属性 SQL_ATTR 的讨论在 _DBC_INFO_TOKEN [SQLSetConnectAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59368))。 但是，重置这些属性可能会降低性能。 例如，重置数据库需要对服务器的网络调用。 如果可用，因此，重复使用完全匹配的连接。  
  
 驱动程序中的分级函数可以计算的现有连接使用新的连接请求。 例如，可以确定驱动程序分级函数：  
  
-   如果在请求完全匹配的现有连接。  
  
-   如果仅某些无意义不匹配，例如连接超时值，无需与要重置的服务器的通信。  
  
-   如果有一些不匹配的属性需要与要重置的服务器通信，但仍会导致更好的性能比建立新连接。  
  
-   如果不匹配，出现了非常耗时，若要重置的属性 （驱动程序的开发人员可以考虑将此特性添加到集中的键属性，用于生成池 ID）。  
  
 介于 0 和 100 之间的分数是的可能的其中 0 表示，不要重复使用和 100 表示完全匹配。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)评级连接的函数。  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>新 ODBC 句柄的 SQL_HANDLE_DBC_INFO_TOKEN  
 若要支持识别驱动程序的连接池，该驱动程序需要连接信息来计算池 id。 该驱动程序还需要连接信息进行比较使用池中的连接的新连接请求。  可以重复使用在池中没有连接，只要该驱动程序必须建立新连接，因此需要连接信息。  
  
 由于连接信息可能来自多个源 （连接字符串、 连接属性和 DSN），该驱动程序可能需要分析连接字符串和解析这些源中每个以上的函数调用之间的冲突。  
  
 因此，引入新的 ODBC 句柄： SQL_HANDLE_DBC_INFO_TOKEN。 使用 SQL_HANDLE_DBC_INFO_TOKEN，驱动程序不需要以分析连接字符串并不止一次解决连接信息中的冲突。 由于这是一种特定于驱动程序的数据结构，该驱动程序可以存储数据，例如连接信息或池 id。  
  
 此句柄仅用作驱动程序管理器和驱动程序之间的接口。 应用程序不能直接分配此句柄。  
  
 此句柄的父句柄为 SQL_HANDLE_ENV，这意味着，驱动程序可以获取环境的信息从 HENV 句柄在连接信息解析期间类型。  
  
 每当它收到新的连接请求时，驱动程序管理器将用于存储连接信息，它确认该驱动程序支持连接池感知后分配类型 SQL_HANDLE_DBC_INFO_TOKEN 的句柄。 在完成后使用句柄 (但在返回之前一些返回代码从 SQL_STILL_EXECUTING 之外[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))，驱动程序管理器将释放句柄。 因此，该句柄 SQLAllocHandle 调用后，创建和销毁 SQLFreeHandle 调用之后。 驱动程序管理器可保证将释放其关联的 HENV 前释放该句柄 (当[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)返回错误)。  
  
 该驱动程序应修改以接受新的句柄类型 SQL_HANDLE_DBC_INFO_TOKEN 的以下函数：  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驱动程序管理器保证，多个线程将同时使用相同的 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 因此，此句柄的同步模型可以是驱动程序内非常简单。 驱动程序管理器将不会在分配和释放 SQL_HANDLE_DBC_INFO_TOKEN 之前的环境锁。  
  
 驱动程序管理器**SQLAllocHandle**并**SQLFreeHandle**将不接受此新的句柄类型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN 可能包含机密信息，例如凭据。 因此，驱动程序应安全地清除内存缓冲区 (使用[SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx))，其中包含敏感信息之前释放与此句柄**SQLFreeHandle**。 每当应用程序的环境句柄已关闭，将关闭所有关联的连接池。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>评级算法的驱动程序管理器连接池  
 本部分讨论用于驱动程序管理器连接池的评分算法。 驱动程序开发人员可以实现向后兼容性相同的算法。 此算法可能不是最好的一个。 你需要优化此算法基于您的实现 （否则，将无需实现此功能）。  
  
 驱动程序管理器将返回整数级别从 0 到 100 之间的每个连接从池中。 0 表示不能重复使用连接，100 指示以完美匹配。 假定连接请求名为 hRequest 和从池中的现有连接名为 hCandidate。 如果任何一个以下条件为 false，不能为 hRequest （驱动程序管理器将分配 0 的分级） 重复使用已入池的连接 hCandidate。  
  
-   hCandidate 和 hRequest 都来自于 UNICODE API （例如，SQLDriverConnectW) 或 ANSI API （例如，SQLDriverConnectA)。 （UNICODE 驱动程序可以在给定 （请参阅连接属性 SQL_ATTR_ANSI_APP） 的 ANSI API 和 UNICODE API 的行为不同。）  
  
-   通过相同的函数; 创建 hCandidate 和 hRequestSQLDriverConnect 或 SQLConnect。  
  
-   使用 SQLDriverConnect 时，用来打开 hCandidate 的连接字符串应与 hRequest，相同。  
  
-   服务器名称 （或 DSN），用户名和密码用于打开 hCandidate 应为相同的用于使用 SQLConnect 时打开 hRequest。  
  
-   由于 SID 用于打开 hCandidate，当前线程的安全标识符 (SID) 应相同。  
  
-   驱动程序的开销很大，以登记并取消登记 (请参阅 SQL_DTC_TRANSITION_COST 中讨论[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))、 重用*hRequest*必须不需要额外的登记或征用。  
  
 下表显示了针对不同方案的分数分配。  
  
|比较已入池的连接和请求之间的连接属性|任何登记 / 征用|需要额外的登记 / 征用|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|目录 (SQL_ATTR_CURRENT_CATALOG) 是不同|60|50|  
|有些连接属性是不同的但目录是相同的|90|70|  
|完全匹配的所有连接属性|100|80|  
  
## <a name="sequence-diagram"></a>序列图  
 此序列图显示了本主题中所述的基本池机制。 它只显示使用[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的情况是类似。  
  
 ![序列关系图](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状态图  
 此状态图显示的连接信息令牌对象，此主题中所述。 在关系图仅显示[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的情况是类似。 由于驱动程序管理器可能需要在任何时候处理错误，可以调用驱动程序管理器[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)的任何状态。  
  
 ![状态图](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>请参阅  
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服务提供程序接口 (SPI) 参考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
