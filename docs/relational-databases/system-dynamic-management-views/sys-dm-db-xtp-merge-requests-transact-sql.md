---
title: sys.dm_db_xtp_merge_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fa5034f83f537afa3b7678b57637ffedada6680
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630715"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]


跟踪数据库合并请求。 Merge 请求可能由 SQL Server 生成或请求可以由具有权限的用户发出[sys.sp_xtp_merge_checkpoint_files (Transact SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)。

> [!NOTE]
> 此动态管理视图 (DMV) sys.dm_db_xtp_merge_requests，Microsoft SQL Server 2014 之前存在。
> 
> 但是，此 DMV 与 SQL Server 2016 开始不再适用。

## <a name="columns-in-the-report"></a>在报表中的列

| 列名 | 数据类型 | Description |
| :-- | :-- | :-- |
| request_state | TINYINT | 合并请求的状态：<br/>0 = requested<br/>1 = pending<br/>2 = 安装<br/>3 = abandoned |
| request_state_desc | nvarchar(60) | 请求的当前状态的含义：<br/><br/>请求-存在合并请求。<br/>挂起的合并是正在处理的。<br/>安装-合并已完成。<br/>已放弃的合并无法完成，可能是因为缺乏存储空间。 |
| destination_file_id | GUID | 与源文件合并的目标文件的唯一标识符。 |
| lower_bound_tsn | BIGINT | 目标合并文件的最小时间戳。 要合并的所有源文件的最低事务时间戳。 |
| upper_bound_tsn | BIGINT | 目标合并文件的最大时间戳。 要合并的所有源文件的最高事务时间戳。 |
| collection_tsn | BIGINT | 可以收集当前行时的时间戳。<br/><br/>当 checkpoint_tsn 大于 collection_tsn 时，删除处于 Installed 状态的行。<br/><br/>当 checkpoint_tsn 小于 collection_tsn 时，删除处于 Abandoned 状态的行。 |
| checkpoint_tsn | BIGINT | 检查点启动时的时间。<br/><br/>在新数据文件中将考虑时间戳低于此值的事务执行的所有删除。 其余删除会移动到目标差异文件。 |
| sourcenumber_file_id | GUID | 用于唯一标识合并中的源文件的最多 16 个内部文件 ID。 |

## <a name="permissions"></a>Permissions

要求对当前数据库拥有 VIEW DATABASE STATE 权限。

## <a name="see-also"></a>另请参阅

[内存优化表动态管理视图 (Transact SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)


