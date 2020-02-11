---
title: 选项（"查询执行： SQL Server：高级" 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089365"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>选项（“查询执行”:“SQL Server”:“高级”页）
  有几个使用 SET 命令的选项。 使用此页可以指定在 SQL Server 查询编辑器中运行 **** 查询时的 set[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 选项。 这些选项对其他代码编辑器不起任何作用。 对这些选项所做的更改仅应用于新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询。 若要更改当前查询的选项，请单击 **“查询”** 菜单或 **查询窗口中快捷菜单上的** “查询选项” [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 在 **“执行”** 下，单击 **“高级”**。 有关每个选项的详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="options"></a>选项  
 **设置 NOCOUNT**  
 不随结果集以消息形式返回行计数。 默认情况下，此复选框处于未选中状态。  
  
 **设置 NOEXEC**  
 不运行查询。 默认情况下，此复选框处于未选中状态。  
  
 **设置 PARSEONLY**  
 检查每个查询的语法，但不运行查询。 默认情况下，此复选框处于未选中状态。  
  
 **设置 CONCAT_NULL_YIELDS_NULL**  
 选中此复选框时，对于现有值与 NULL 相串联的查询，结果将始终返回 NULL。 清除此复选框时，对于现有值与 NULL 相串联的查询，将返回该现有值。 默认情况下，此复选框为选中状态。  
  
 **设置 ARITHABORT**  
 选中此复选框时，如果 INSERT、DELETE 或 UPDATE 语句在表达式计算过程中遇到算术错误（溢出、被零除或域错误）时，则会终止查询或批。 清除此复选框时，如果可能的话，该值为 NULL，查询将继续进行，而结果中还会包含一条消息。 有关详细信息，请参阅 [SET ARITHABORT (Transact-SQL)](/sql/t-sql/statements/set-arithabort-transact-sql)。 默认情况下，此复选框为选中状态。  
  
 **设置 SHOWPLAN_TEXT**  
 选中此复选框时，将以文本格式返回每个查询的查询计划。 默认情况下，此复选框处于未选中状态。  
  
 **设置统计信息时间**  
 选中此复选框时，将返回每个查询的时间统计信息。 默认情况下，此复选框处于未选中状态。  
  
 **设置统计 IO**  
 选中此复选框时，将返回每个查询的输入和输出统计信息。 默认情况下，此复选框处于未选中状态。  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 默认情况下，将设置 READ COMMITTED 事务隔离级别。 有关详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 SNAPSHOT 事务隔离级别不可用。 若要使用 SNAPSHOT 隔离，请添加以下 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句：  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **SET DEADLOCK PRIORITY**  
 如果使用默认值“正常”，则允许在发生死锁时每个查询具有相同的优先级。 如果希望此查询在任何死锁冲突中都靠后考虑，并且选作要终止的查询，请选择优先级“低”。  
  
 **SET LOCK TIMEOUT**  
 默认值为 -1，指示在完成事务之前始终保留锁。 值为 0 时表示根本不等待，一遇到锁就返回信息。 如果事务的锁的保留时间必须长于此时间，请提供一个大于 0 毫秒的值以终止事务。  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 使用 **QUERY_GOVERNOR_COST_LIMIT** 选项可以指定查询运行时间长度的上限。 查询开销是指在特定硬件配置中完成查询所需的估计占用时间（秒）。 默认设置 0 表示不限制查询运行时间的长度。  
  
 **取消提供程序消息标头**  
 选中此复选框时，将不显示提供程序（如 SQLClient 提供程序）的状态消息。 默认情况下，此复选框为选中状态。 在排除可能在提供程序级别上失败的查询故障时，清除此复选框可查看提供程序消息。  
  
 **执行查询后断开连接**  
 选中此复选框时，查询完成后会终止与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之间的连接。 默认情况下，此复选框处于未选中状态。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
