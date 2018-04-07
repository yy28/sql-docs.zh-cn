---
title: sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: relational-databases
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e511ba417e4eb58d1ff52b1896a03f8bb5f0722c
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]


跟踪数据库合并请求。 合并请求可能由 SQL Server 生成或请求无法由具有的用户发出[sys.sp_xtp_merge_checkpoint_files (Transact SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)。

> [!NOTE]
> 此动态管理视图 (DMV)，直到 Microsoft SQL Server 2014 sys.dm_db_xtp_merge_requests，存在。
> 
> 但此 DMV 启动 SQL Server 2016 不再适用。

## <a name="columns-in-the-report"></a>在报表中的列

| 列名 | 数据类型 | Description |
| :-- | :-- | :-- |
| request_state | tinyint | 合并请求的状态：<br/>0 = requested<br/>1 = pending<br/>2 = 安装<br/>3 = abandoned |
| request_state_desc | nvarchar(60) | 请求的当前状态的含义：<br/><br/>请求的存在 merge 请求。<br/>挂起的合并是正在处理。<br/>安装的合并已完成。<br/>放弃的合并无法完成，可能是由于缺乏存储。 |
| destination_file_id | GUID | 与源文件合并的目标文件的唯一标识符。 |
| lower_bound_tsn | bigint | 目标合并文件的最小时间戳。 要合并的所有源文件的最低事务时间戳。 |
| upper_bound_tsn | bigint | 目标合并文件的最大时间戳。 要合并的所有源文件的最高事务时间戳。 |
| collection_tsn | bigint | 可以收集当前行时的时间戳。<br/><br/>当 checkpoint_tsn 大于 collection_tsn 时，删除处于 Installed 状态的行。<br/><br/>当 checkpoint_tsn 小于 collection_tsn 时，删除处于 Abandoned 状态的行。 |
| checkpoint_tsn | bigint | 检查点启动时的时间。<br/><br/>在新数据文件中将考虑时间戳低于此值的事务执行的所有删除。 其余删除会移动到目标差异文件。 |
| sourcenumber_file_id | GUID | 用于唯一标识合并中的源文件的最多 16 个内部文件 ID。 |

## <a name="permissions"></a>权限

要求对当前数据库拥有 VIEW DATABASE STATE 权限。

## <a name="see-also"></a>另请参阅

[内存优化表的动态管理视图 (Transact SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)


