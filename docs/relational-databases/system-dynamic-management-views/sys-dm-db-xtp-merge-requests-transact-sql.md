---
description: sys.dm_db_xtp_merge_requests (Transact-SQL)
title: sys. dm_db_xtp_merge_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b7625c78365a2840413177fe8823ecc4b3b1286
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542186"
---
# <a name="sysdm_db_xtp_merge_requests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

跟踪数据库合并请求。 合并请求可能是由 SQL Server 生成的，或者该请求可能由具有 [sys.databases (transact-sql) ](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)的用户发出 sp_xtp_merge_checkpoint_files。

> [!NOTE]
> 此动态管理视图 (DMV) ，dm_db_xtp_merge_requests sys.databases 一直存在，直到 Microsoft SQL Server 2014 为止。
> 但从 SQL Server 2016 开始，此 DMV 将不再适用。

## <a name="columns-in-the-report"></a>报表中的列

| 列名称 | 数据类型 | 说明 |
| :-- | :-- | :-- |
| request_state | tinyint | 合并请求的状态：<br/>0 = requested<br/>1 = pending<br/>2 = 安装<br/>3 = abandoned |
| request_state_desc | nvarchar(60) | 请求的当前状态的含义：<br/><br/>请求-存在合并请求。<br/>挂起-合并正在处理中。<br/>已安装-合并已完成。<br/>已放弃-合并无法完成，可能是由于存储空间不足引起的。 |
| destination_file_id | GUID | 与源文件合并的目标文件的唯一标识符。 |
| lower_bound_tsn | bigint | 目标合并文件的最小时间戳。 要合并的所有源文件的最低事务时间戳。 |
| upper_bound_tsn | bigint | 目标合并文件的最大时间戳。 要合并的所有源文件的最高事务时间戳。 |
| collection_tsn | bigint | 可以收集当前行时的时间戳。<br/><br/>当 checkpoint_tsn 大于 collection_tsn 时，删除处于 Installed 状态的行。<br/><br/>当 checkpoint_tsn 小于 collection_tsn 时，删除处于 Abandoned 状态的行。 |
| checkpoint_tsn | bigint | 检查点启动时的时间。<br/><br/>在新数据文件中将考虑时间戳低于此值的事务执行的所有删除。 其余删除会移动到目标差异文件。 |
| sourcenumber_file_id | GUID | 最多16个内部文件 Id，用于唯一标识合并中的源文件。 |

## <a name="permissions"></a>权限

要求对当前数据库拥有 VIEW DATABASE STATE 权限。

## <a name="see-also"></a>另请参阅

[内存优化表动态管理视图 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
