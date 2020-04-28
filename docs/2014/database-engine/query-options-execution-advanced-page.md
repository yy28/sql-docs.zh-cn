---
title: 查询选项执行（"高级" 页） |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "71199323"
---
# <a name="query-options-execution-advanced-page"></a>“查询选项”中的“执行”（“高级”页）

  可以通过 **SET** 语句使用各种选项。 使用此页可以指定用于运行 Microsoft SQL Server 查询的**SET**选项。 有关其中每个选项的详细信息，请参阅 SQL Server 联机丛书。
  
**设置 NOCOUNT**不返回行数的计数，作为包含结果集的消息。 默认情况下，此选项处于未选中状态。

**设置 NOEXEC**不运行查询。 默认情况下，此选项处于未选中状态。

**设置 PARSEONLY**检查每个查询的语法，但不运行查询。 默认情况下，此选项处于未选中状态。  

**设置 CONCAT_NULL_YIELDS_NULL**选中此复选框时，将现有值与`NULL`连接的查询将始终返回`NULL`作为结果。 清除此复选框时，对于现有值与 `NULL` 相串联的查询，将返回该现有值。 默认情况下选择此选项。

**设置 ARITHABORT**选中此复选框后，当`INSERT`、 `DELETE`或`UPDATE`语句在表达式计算过程中遇到算术错误（溢出、被零除或域错误）时，将终止查询或批处理。 清除此复选框时，会在可能的情况下为该值提供 `NULL`，查询将继续进行，而结果中还会包含一条消息。 有关此行为的详细说明，请参阅联机丛书。 默认情况下选择此选项。
  
**设置 SHOWPLAN_TEXT**选中此复选框时，将以文本形式返回每个查询的查询计划。 默认情况下，此选项处于未选中状态。
  
**SET STATISTICS TIME** 选中此复选框时，将返回每个查询的时间统计信息。 默认情况下，此选项处于未选中状态。
  
**设置统计 IO**选中此复选框时，将返回每个查询的输入/输出（i/o）相关统计信息。 默认情况下，此选项处于未选中状态。
  
**SET TRANSACTION ISOLATION LEVEL** 默认情况下，将设置 READ COMMITTED 事务隔离级别。 有关详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 快照事务隔离级别不可用。 若要使用 SNAPSHOT 隔离，请添加以下 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句：
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**SET DEADLOCK PRIORITY** 如果使用默认值 **“正常”** ，则允许在发生死锁时每个查询具有相同的优先级。 如果希望此查询在任何死锁冲突中都靠后考虑，并且选作要终止的查询，请从下拉列表中选择优先级“低”。

**设置锁定超时**默认值为-1，表示一直持有锁，直到事务完成。 值为 0 时表示根本不等待，一遇到锁就返回信息。 如果事务的锁的保留时间必须长于此时间，请提供一个大于 0 毫秒的值以终止事务。

**设置 QUERY_GOVERNOR_COST_LIMIT**使用 "**查询调控器开销限制**" 选项指定查询可以运行的时间段上限。 查询开销是指在特定硬件配置中完成查询所需的估计占用时间（秒）。 默认设置 0 表示不限制查询运行时间的长度。

**取消提供程序消息标头**选中此复选框时，将不显示提供程序（如 OLE DB 提供程序）的状态消息。 默认情况下，此复选框为选中状态。 在排除可能在提供程序级别上失败的查询故障时，清除此复选框可查看提供程序消息。

**执行查询后断开连接** 选中此复选框时，查询完成后会终止与 SQL Server 之间的连接。 默认情况下，此选项处于未选中状态。

**显示完成时间**允许您在查询结果之后或在 "消息" 选项卡中打印查询执行完成的时间。

**用于 VBS enclaves for Always Encrypted 的证明协议**允许你为基于虚拟化的安全（VBS） enclaves 设置一个证明协议，该协议是使用安全 enclaves 的始终加密所使用的。

当前支持的认证协议为：

* 主机保护者服务-使用 Windows 主机保护者服务（HGS）的证明协议。

有关详细信息，请参阅[具有 secure enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions)和[secure Enclave 证明](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation)的 Always Encrypted。

**重置为默认值** 将此页上的所有值重置为原始默认值。
