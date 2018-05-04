---
title: cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 115e317dcbf2e43202d2d43ea39841bf62f64f2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对指定的日志序列号 (LSN) 范围内更改每个源行的一个净更改行。  
  
 **等待，LSN 是什么？** 中的每个记录[SQL Server 事务日志](../logs/the-transaction-log-sql-server.md)由日志序列号 (LSN) 唯一标识。 Lsn 有顺序，以便如果 LSN2 大于 LSN1，描述 LSN2 所引用的日志记录的更改发生**后**描述的 LSN 的日志记录更改。  
  
 发生重大事件的日志记录的 LSN 可用于构造正确的还原顺序。 因为 Lsn 有顺序，你可以比较它们是否相等和不相等 (即， \<，>，=， \<=、 > =)。 构造还原顺序时，这种比较很有用。  
  
 当源行的 LSN 范围内具有多个更改时，如下所述枚举函数返回单个行反映该行的最终内容。 例如，如果事务源表中插入一行并能在后续事务的 LSN 范围内更新该行中的一个或多个列，该函数仅返回**一个**行，其中包括的更新的列的值。  
  
 此枚举函数是在对某源表启用变更数据捕获并指定净跟踪时创建的。 若要启用净跟踪，源表必须具有主键或唯一索引。 函数名称派生，并使用格式 cdc.fn_cdc_get_net_changes_*capture_instance*，其中*capture_instance*是当源表时指定捕获实例的值启用了变更数据捕获。 有关详细信息，请参阅[sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>参数  
 *from_lsn*  
 LSN，它表示要包含在结果集中的 LSN 范围的低端点。 *from_lsn*是**binary （10)**。  
  
 仅行[cdc。&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)更改表中 __ $start_lsn 大于或等于的值与*from_lsn*包含在结果集。  
  
 *to_lsn*  
 LSN，它表示要包含在结果集中的 LSN 范围的高端点。 *to_lsn*是**binary （10)**。  
  
 仅行[cdc。&#91;capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)更改表中 __ $start_lsn 小于或等于的值与*from_lsn*于或等于*to_lsn*包含在结果集。  
  
 *< row_filter_option >* :: = {所有 | 所有与掩码 | 全部且具有合并}  
 控制元数据列的内容和结果集中所返回的行的选项。 可以是下列选项之一：  
  
 all  
 返回的行和应用元数据列 __ $start_lsn 中的行所需操作的最后一个更改 LSN 和\_ \_$operation。 列\_ \_$update_mask 始终为 NULL。  
  
 all with mask  
 返回的行和应用元数据列 __ $start_lsn 中的行所需操作的最后一个更改 LSN 和\_ \_$operation。 此外，当更新操作返回 (\_\_$operation = 4) 捕获的列在更新中修改标记中返回的值中\_ \_$update_mask。  
  
 all with merge  
 返回对元数据列 __$start_lsn 中的行所做的最终更改的 LSN。 列\_ \_$operation 将两个值之一： 1 用于删除，5，以指示需要以应用更改该操作是插入或更新。 列\_ \_$update_mask 始终为 NULL。  
  
 由于用来确定给定更改的精确操作的逻辑会增加查询的复杂性，所以，在只需指出应用更改数据所需的操作是插入还是更新但不必明确区分这两者时，使用该选项可提高查询性能。 在可直接使用合并操作的目标环境（如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 环境）中，此选项非常有用。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|与更改的提交事务关联的 LSN。<br /><br /> 在同一事务中提交的所有更改将共享同一个提交 LSN。 例如，如果更新操作在源表上的修改两个行中的两个列，更改表将包含四个行，每个都有相同的 __ $start_lsnvalue。|  
|__$operation|**int**|标识将更改数据行应用到目标数据源所需的数据操作语言 (DML) 操作。<br /><br /> 如果 row_filter_option 参数的值为 all 或 all with mask，则此列中的值可以是以下值之一：<br /><br /> 1 = 删除<br /><br /> 2 = 插入<br /><br /> 4 = 更新<br /><br /> 如果 row_filter_option 参数的值为 all with merge，则此列中的值可以是以下值之一：<br /><br /> 1 = 删除|  
|__$update_mask|**varbinary(128)**|位掩码，为捕获实例标识的每个已捕获列均对应于一个位。 如果 __$operation = 1 或 2，该值将所有已定义的位设置为 1。 当\_ \_$operation = 3 或 4，只有那些位对应于更改的列将设置为 1。|  
|\<捕获的源表列>|不定|函数返回的其余列是在创建捕获实例时源表中标识为已捕获列的那些列。 如果已捕获列的列表中未指定任何列，则将返回源表中的所有列。|  
  
## <a name="permissions"></a>权限  
 要求具有 sysadmin 固定服务器角色或 db_owner 固定数据库角色的成员身份。 对于所有其他用户，要求对源表中的所有已捕获列具有 SELECT 权限；如果已定义捕获实例的访问控制角色，则还要求具有该数据库角色的成员身份。 当调用方没有查看源数据的权限时，函数将返回错误 208（对象名无效）。  
  
## <a name="remarks"></a>注释  
 如果指定的 LSN 范围不在捕获实例的更改跟踪时间线范围之内，则函数将返回错误 208（对象名无效）。  
  
## <a name="examples"></a>示例  
 下面的示例使用函数`cdc.fn_cdc_get_net_changes_HR_Department`报告到源表所做的净更改`HumanResources.Department`在特定时间间隔。  
  
 首先，`GETDATE` 函数用于标记时间间隔的开始。 在将多个 DML 语句应用到源表后，再次调用 `GETDATE` 函数可标识时间间隔的结束。 该函数[sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)然后将其用于将映射到由 LSN 值限定某个更改数据捕获查询范围的时间间隔。 最后，查询函数 `cdc.fn_cdc_get_net_changes_HR_Department` 以获取该时间间隔内对源表所做的净更改。 请注意，插入后又删除的行在函数返回的结果集中不会出现。 这是因为在查询窗口中先添加然后又删除的行在时间间隔内对源表不生成任何净更改。 在运行此示例之前，必须先运行中的示例 B [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>另请参阅  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [关于变更数据捕获 (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
