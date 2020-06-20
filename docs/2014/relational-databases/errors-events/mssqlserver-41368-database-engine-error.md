---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 10e187223a3f35b4b21ede6965e3c9efea2e30c1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053928"
---
# <a name="mssqlserver_41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41368|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|消息正文|只支持对自动提交事务使用 READ COMMITTED 隔离级别访问内存优化表。 显式或隐式事务不支持此隔离级别。 使用表提示（例如 WITH (SNAPSHOT)）为内存优化表提供一种支持的隔离级别。|  
  
## <a name="explanation"></a>说明  
 只支持对自动提交事务使用 READ COMMITTED 隔离级别访问内存优化表。 有关详细信息，请参阅 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)。  
  
 当从使用 BEGIN TRANSACTION 启动的显式事务或从隐式事务访问内存优化表时，如果将 IMPLICIT_TRANSACTIONS 设置为 ON，则不支持 READ COMMITTED 隔离级别。  
  
## <a name="user-action"></a>用户操作  
 从显式或隐式 READ COMMITTED 事务访问内存优化表时，使用 SNAPSHOT 来访问该表。 这可以通过将表提示与（快照）结合使用来实现（有关详细信息，请参阅[使用内存优化表的事务隔离级别的准则](../in-memory-oltp/memory-optimized-tables.md)），或将数据库选项 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 设置为 ON （有关详细信息，请参阅[ALTER database SET Options &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)）。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
