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
manager: craigg
ms.openlocfilehash: a2206980d241d3ef0aa683e4f987a4e337a86855
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913802"
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41368|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|消息正文|只支持对自动提交事务使用 READ COMMITTED 隔离级别访问内存优化表。 显式或隐式事务不支持此隔离级别。 使用表提示（例如 WITH (SNAPSHOT)）为内存优化表提供一种支持的隔离级别。|  
  
## <a name="explanation"></a>解释  
 只支持对自动提交事务使用 READ COMMITTED 隔离级别访问内存优化表。 有关详细信息，请参阅 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)。  
  
 当从使用 BEGIN TRANSACTION 启动的显式事务或从隐式事务访问内存优化表时，如果将 IMPLICIT_TRANSACTIONS 设置为 ON，则不支持 READ COMMITTED 隔离级别。  
  
## <a name="user-action"></a>用户操作  
 从显式或隐式 READ COMMITTED 事务访问内存优化表时，使用 SNAPSHOT 来访问该表。 这可以通过使用表提示 WITH (SNAPSHOT) (有关详细信息，请参阅[具有内存优化表的事务隔离级别准则](../in-memory-oltp/memory-optimized-tables.md)) 或通过将数据库设置选项 MEMORY_OPTIMIZED_ELEVATE_TO_快照为 ON (有关详细信息，请参阅[ALTER DATABASE SET 选项&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options))。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
