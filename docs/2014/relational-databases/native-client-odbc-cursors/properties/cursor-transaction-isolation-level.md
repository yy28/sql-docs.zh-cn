---
title: 光标事务隔离级别 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 83c5195598eb28ad8bcbe219d7cda0de327973cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027471"
---
# <a name="cursor-transaction-isolation-level"></a>游标事务隔离级别
  游标的完整锁定行为基于由客户端设置的并发属性和事务隔离级别之间的交互。 ODBC 客户端设置事务隔离级别使用[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 属性。 通过将并发和事务隔离级别选项的锁定行为进行组合，可以确定特定游标环境的锁定行为。  
  
 支持以下光标事务隔离级别[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序：  
  
-   已提交读 (SQL_TXN_READ_COMMITTED)  
  
-   未提交读 (SQL_TXN_READ_UNCOMMITTED)  
  
-   可重复读 (SQL_TXN_REPEATABLE_READ)  
  
-   可序列化 (SQL_TXN_SERIALIZABLE)  
  
-   快照 (SQL_TXN_SS_SNAPSHOT)  
  
 请注意，ODBC API 指定其他事务隔离级别，但不是支持这些[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。  
  
## <a name="see-also"></a>请参阅  
 [游标属性](cursor-properties.md)  
  
  