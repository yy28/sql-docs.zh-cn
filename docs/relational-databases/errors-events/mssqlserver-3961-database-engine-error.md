---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4bee6f2a3420267cca465ef81adb25436f105166
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3961|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XACT_METADATA_INVALID|  
|消息正文|数据库 '%.*ls' 中的快照隔离事务失败，因为自此事务启动后，该语句所访问的对象已由其他并发事务中的 DDL 语句修改。  这是不允许的，因为未对元数据进行版本控制。 如果与快照隔离混合，对元数据的并发更新可能导致不一致。|  
  
## <a name="explanation"></a>解释  
如果在快照隔离下查询元数据并且在快照隔离下存在用于更新正在访问的元数据的并发 DDL 语句，则将发生此错误。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持元数据的版本控制。 因此，对于在快照隔离下运行的显式事务中可以执行哪些 DDL 操作存在限制。 根据定义，隐式事务是单个语句，这使得它即便是使用 DDL 语句也可以强制应用快照隔离的语义。 在快照隔离下，BEGIN TRANSACTION 语句之后不允许使用任何公共语言运行时 (CLR) DDL 语句或下列 DDL 语句：ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME。 在隐式事务中使用快照隔离时允许使用这些语句。 根据定义，隐式事务是单个语句，这使得它即便是使用 DDL 语句也可以强制应用快照隔离的语义。  
  
## <a name="user-action"></a>用户操作  
在查询元数据之前将快照隔离级别更改为诸如“已提交读”之类的非快照隔离级别。  
  

