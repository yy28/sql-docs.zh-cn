---
title: 查询选项 （高级页） 的执行 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5cdff5f44079c6c4946f30f9d4cc12ecc1bcac85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014358"
---
# <a name="query-options-execution-advanced-page"></a>“查询选项”中的“执行”（“高级”页）
  可以通过 **SET** 语句使用各种选项。 使用此页，可以指定 **set** 选项以运行 Microsoft SQL Server 查询。 有关其中每个选项的详细信息，请参阅 SQL Server 联机丛书。  
  
 **SET NOCOUNT**  
 不随结果集以消息形式返回行计数。 默认情况下，此选项处于未选中状态。  
  
 **SET NOEXEC**  
 不运行查询。 默认情况下，此选项处于未选中状态。  
  
 **SET PARSEONLY**  
 检查每个查询的语法，但不运行查询。 默认情况下，此选项处于未选中状态。  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 选中此复选框时，对于现有值与 `NULL` 相串联的查询，结果将始终返回 `NULL`。 清除此复选框时，对于现有值与 `NULL` 相串联的查询，将返回该现有值。 默认情况下选择此选项。  
  
 **SET ARITHABORT**  
 选中此复选框时，如果 `INSERT`、`DELETE` 或 `UPDATE` 语句在表达式计算过程中遇到算术错误（溢出、被零除或域错误）时，则会终止查询或批。 清除此复选框时，会在可能的情况下为该值提供 `NULL`，查询将继续进行，而结果中还会包含一条消息。 有关此行为的详细说明，请参阅联机丛书。 默认情况下选择此选项。  
  
 **SET SHOWPLAN_TEXT**  
 选中此复选框时，将以文本形式返回每个查询的查询计划。 默认情况下，此选项处于未选中状态。  
  
 **SET STATISTICS TIME**  
 选中此复选框时，将返回每个查询的时间统计信息。 默认情况下，此选项处于未选中状态。  
  
 **SET STATISTICS IO**  
 选中此复选框时，将返回每个查询的输入/输出 (I/O) 统计信息。 默认情况下，此选项处于未选中状态。  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 默认情况下，将设置 READ COMMITTED 事务隔离级别。 有关详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 SNAPSHOT 事务隔离级别不可用。 若要使用 SNAPSHOT 隔离，请添加以下 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句：  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **设置死锁优先级**  
 如果使用默认值“正常”，则允许在发生死锁时每个查询具有相同的优先级。 如果希望此查询在任何死锁冲突中都靠后考虑，并且选作要终止的查询，请从下拉列表中选择优先级“低”。  
  
 **设置锁超时**  
 默认值为 -1，指示在完成事务之前始终保留锁。 值为 0 时表示根本不等待，一遇到锁就返回信息。 如果事务的锁的保留时间必须长于此时间，请提供一个大于 0 毫秒的值以终止事务。  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 使用“查询调控器开销限制”选项指定查询可以运行的时间段上限。 查询开销是指在特定硬件配置中完成查询所需的估计占用时间（秒）。 默认设置 0 表示不限制查询运行时间的长度。  
  
 **取消提供程序消息标头**  
 选中此复选框时，将不显示访问接口（如 OLE DB 访问接口）的状态消息。 默认情况下，此复选框为选中状态。 在排除可能在提供程序级别上失败的查询故障时，清除此复选框可查看提供程序消息。  
  
 **执行查询后断开连接**  
 选中此复选框时，查询完成后会终止与 SQL Server 之间的连接。 默认情况下，此选项处于未选中状态。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
