---
title: 创建分布式事务 |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303678"
---
# <a name="create-a-distributed-transaction"></a>创建分布式事务

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


可以以不同的方式为不同的 Microsoft SQL 系统创建分布式事务。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 驱动程序在本地调用 SQL Server 的 MSDTC

Microsoft 分布式事务协调器 （MSDTC） 允许应用程序跨 的两个或多个实例扩展或_分发_事务[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 即使两个实例托管在单独的计算机上，分布式事务也能正常工作。

MSDTC 安装在本地为 Microsoft SQL 服务器，但不适用于 Microsoft 的 Azure SQL 数据库云服务。

MSDTC 由打开数据库连接 （ODBC） 的 SQL Server 本机客户端驱动程序调用，当您C++程序管理分布式事务时。 本机客户端 ODBC 驱动程序具有符合开放组分布式事务处理 （DTP） XA 标准的事务管理器。 MSDTC 需要这种合规性。 通常，所有事务管理命令都通过此本机客户端 ODBC 驱动程序发送。 顺序如下：

1. C++本机客户端 ODBC 应用程序通过调用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)启动事务，自动提交模式处于关闭状态。

2. 应用程序在计算机 A 上更新 SQL Server X 上的一些数据。

3. 应用程序在计算机 B 上更新 SQL Server Y 上的一些数据。
    - 如果 SQL Server Y 上的更新失败，则回滚两个 SQL Server 实例上未提交的所有更新。

4. 最后，应用程序通过调用[SQLEndTran _（1）_](../../../relational-databases/native-client-odbc-api/sqlendtran.md)结束事务，SQL_COMMIT 或SQL_ROLLBACK选项。

_（1）_ 无需 ODBC 即可调用 MSDTC。 在这种情况下，MSDTC 成为事务管理器，应用程序不再使用**SQLEndTran**。

### <a name="only-one-distributed-transaction"></a>只有一个分布式事务

假设您C++本机客户端 ODBC 应用程序已登记在分布式事务中。 接下来，应用程序将登记在第二个分布式事务中。 在这种情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序将离开原始分布式事务，并登记在新的分布式事务中。

有关详细信息，请参阅[DTC 程序员的参考](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>云中 SQL 数据库的 C# 替代方案

Azure SQL 数据库或 Azure SQL 数据仓库不支持 MSDTC。

但是，可以通过让 C# 程序使用 .NET 类[系统，](/dotnet/api/system.transactions.transactionscope)为 SQL 数据库创建分布式事务。

### <a name="other-programming-languages"></a>其他编程语言

以下其他编程语言可能无法为 SQL 数据库服务的分布式事务提供任何支持：

- 使用 ODBC 驱动程序的本机C++
- 使用交易 SQL 链接服务器
- JDBC 驱动程序

## <a name="see-also"></a>请参阅

[执行事务 (ODBC)](performing-transactions-in-odbc.md)
