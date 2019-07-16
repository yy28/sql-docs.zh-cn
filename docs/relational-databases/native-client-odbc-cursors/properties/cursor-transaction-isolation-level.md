---
title: 游标事务隔离级别 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ae4ffc9b3a9c0d8122fb46ae9db215bf1560396
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078846"
---
# <a name="cursor-transaction-isolation-level"></a>游标事务隔离级别
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  游标的完整锁定行为基于由客户端设置的并发属性和事务隔离级别之间的交互。 ODBC 客户端使用设置的事务隔离级别[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 属性。 通过将并发和事务隔离级别选项的锁定行为进行组合，可以确定特定游标环境的锁定行为。  
  
 支持以下游标事务隔离级别[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序：  
  
-   已提交读 (SQL_TXN_READ_COMMITTED)  
  
-   未提交读 (SQL_TXN_READ_UNCOMMITTED)  
  
-   可重复读 (SQL_TXN_REPEATABLE_READ)  
  
-   可序列化 (SQL_TXN_SERIALIZABLE)  
  
-   快照 (SQL_TXN_SS_SNAPSHOT)  
  
 请注意 ODBC API 指定其他事务隔离级别，但这些不受[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。  
  
## <a name="see-also"></a>请参阅  
 [游标属性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
