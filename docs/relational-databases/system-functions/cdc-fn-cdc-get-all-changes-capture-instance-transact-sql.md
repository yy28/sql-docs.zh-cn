---
title: "cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 111fab345e7679745e72ebe874dabcca3bed62fb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="cdcfncdcgetallchangesltcaptureinstancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为在指定日志序列号 (LSN) 范围内应用到源表的每项更改返回一行。 如果源行在该间隔内有多项更改，则每项更改都会表示在返回的结果集中。 除了返回更改数据外，四个元数据列还提供了将更改应用到另一个数据源所需的信息。 行筛选选项可控制元数据列的内容以及结果集中返回的行。 当指定“all”行筛选选项时，针对每项更改将只有一行来标识该更改。 当指定“all update old”选项时，更新操作会表示为两行：一行包含更新之前已捕获列的值，另一行包含更新之后已捕获列的值。  
  
 此枚举函数是在对源表启用变更数据捕获时创建的。 该函数名称派生，并且使用格式**cdc.fn_cdc_get_all_changes_***capture_instance*其中*capture_instance*是捕获为指定的值实例时源表启用了变更数据捕获。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>参数  
 *from_lsn*  
 LSN 值，它表示要包含在结果集中的 LSN 范围的低端点。 *from_lsn*是**binary （10)**。  
  
 仅行[cdc。 &#91; capture_instance &#93; _CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)更改表中的值与**__ $start_lsn**大于或等于*from_lsn*中包括结果集。  
  
 *to_lsn*  
 LSN 值，它表示要包含在结果集中的 LSN 范围的高端点。 *to_lsn*是**binary （10)**。  
  
 仅行[cdc。 &#91; capture_instance &#93; _CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)更改表中的值与**__ $start_lsn**小于或等于*from_lsn*或等于*to_lsn*包含在结果集。  
  
 <row_filter_option> ::= { all | all update old }  
 控制元数据列的内容和结果集中所返回的行的选项。  
  
 可以是下列选项之一：  
  
 all  
 返回指定 LSN 范围内的所有更改。 对于由更新操作导致的更改，此选项只返回在应用更新之后包含新值的行。  
  
 all update old  
 返回指定 LSN 范围内的所有更改。 对于由更新操作导致的更改，此选项将返回在更新之前包含列值的行和更新之后包含列值的行。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|与更改关联的提交 LSN，用于保留更改的提交顺序。 在同一事务中提交的更改将共享同一个提交 LSN 值。|  
|**__$seqval**|**binary(10)**|用于对某事务内的行更改进行排序的序列值。|  
|**__$operation**|**int**|标识将更改数据行应用到目标数据源所需的数据操作语言 (DML) 操作。 可以为以下各项之一：<br /><br /> 1 = 删除<br /><br /> 2 = 插入<br /><br /> 3 = 更新（捕获的列值是执行更新操作前的值）。 仅当指定了行筛选选项“all update old”时才应用此值。<br /><br /> 4 = 更新（捕获的列值是执行更新操作后的值）。|  
|**__$update_mask**|**varbinary(128)**|位掩码，为捕获实例标识的每个已捕获列均对应于一个位。 此值已定义个位设置为 1 时**__ $operation** = 1 或 2。 当**__ $operation** = 3 或 4，只有那些位对应于更改的列将设置为 1。|  
|**\<捕获源表列 >**|不定|函数返回的其余列是在创建捕获实例时标识的已捕获列。 如果已捕获列的列表中未指定任何列，则将返回源表中的所有列。|  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色。 对于所有其他用户，要求对源表中的所有已捕获列具有 SELECT 权限；如果已定义捕获实例的访问控制角色，则还要求具有该数据库角色的成员身份。 当调用方没有权限来查看源数据时，函数将返回错误 229 ("的 SELECT 权限拒绝了对对象 '...fn_cdc_get_all_changes_ 数据库\<DatabaseName >'，架构 'cdc'。")。  
  
## <a name="remarks"></a>注释  
 如果指定的 LSN 范围不在捕获实例的更改跟踪时间线范围之内，则函数将返回错误 208（“为过程或函数 cdc.fn_cdc_get_all_changes 提供的参数数目不足。”）。  
  
 数据类型的列**映像**，**文本**，和**ntext**始终被分配 NULL 值时**__ $operation** = 1 或**__ $操作**= 3。 数据类型的列**varbinary （max)**， **varchar （max)**，或**nvarchar (max)**分配 NULL 值时**__ $operation** = 3除非在更新期间更改了该列。 当**__ $operation** = 1，这些列在删除时分配其值。 捕获实例中包含的计算列的值始终为 NULL。  
  
## <a name="examples"></a>示例  
 多个[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]都能使用模板，可显示如何使用变更数据捕获查询函数。 这些模板都位于**视图**菜单中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 有关详细信息，请参阅[模板资源管理器](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)。  
  
 本示例显示`Enumerate All Changes for Valid Range Template`。 它使用函数`cdc.fn_cdc_get_all_changes_HR_Department`报告捕获实例的当前可用的所有更改`HR_Department`，为源定义表中的 HumanResources.Department[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance &#62;&#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [关于变更数据捕获 (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
