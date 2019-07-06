---
title: 创建分布式的事务 |Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e3eb73528800d45daf0ea8b68ae94536f63c25df
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585478"
---
# <a name="create-a-distributed-transaction"></a>创建分布式的事务

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

分布式的事务可以以不同的方式创建不同的 Microsoft SQL 系统。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 驱动程序为 SQL Server 内部调用 MSDTC

Microsoft 分布式事务处理协调器 (MSDTC)，应用程序可以扩展或_分发_跨两个或多个实例的事务[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 即使两个实例托管在单独的计算机上仍有效的分布式的事务。

MSDTC 已为 Microsoft SQL Server 的本地安装，但不适用于 Microsoft 的 Azure SQL 数据库云服务。

MSDTC 调用 SQL Server Native Client 驱动程序通过开放式数据库连接 (ODBC)，当你C++程序管理分布式的事务。 Native Client ODBC 驱动程序存在兼容与打开组分布式事务处理 (DTP) XA 标准的事务管理器。 这种合规性是所需的 MSDTC。 通常情况下，通过此 Native Client ODBC 驱动程序发送所有事务管理命令。 序列是按如下所示：

1. 在C++Native Client ODBC 应用程序通过调用来启动一个事务[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)，关闭自动提交模式。

2. 应用程序更新了 SQL Server X 上某些数据在计算机 a 上。

3. 应用程序更新了 SQL 服务器 Y 上计算机 B 上的某些数据
    - 如果在 SQL Server y 轴上的更新失败，将回滚这两个 SQL Server 实例上所有未提交的更新。

4. 最后，应用程序通过调用结束事务[SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md)，使用 SQL_COMMIT 或 SQL_ROLLBACK 选项。

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

_(1)_ MSDTC 可以没有 ODBC 调用。 在这种情况下，MSDTC 将成为事务管理器和应用程序不能再使用**SQLEndTran**。

### <a name="only-one-distributed-transaction"></a>只能有一个分布式的事务

假设你C++Native Client ODBC 应用程序将在分布式事务中登记。 接下来在第二个分布式事务中登记应用程序。 在这种情况下， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序会使原始分布式的事务，并在新的分布式事务中登记。

有关详细信息，请参阅[DTC 程序员参考](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#在云中的 SQL 数据库的替代方法

Azure SQL 数据库或 Azure SQL 数据仓库的情况下不支持 MSDTC。

但是，分布式的事务可以为创建 SQL 数据库通过让你C#程序使用.NET 类[System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope)。

### <a name="other-programming-languages"></a>其他编程语言

以下其他编程语言可能无法提供任何支持的 SQL 数据库服务的分布式事务：

- 本机C++使用 ODBC 驱动程序
- 使用 TRANSACT-SQL 的链接的服务器
- JDBC 驱动程序

## <a name="see-also"></a>另请参阅

[执行事务 (ODBC)](performing-transactions-in-odbc.md)
