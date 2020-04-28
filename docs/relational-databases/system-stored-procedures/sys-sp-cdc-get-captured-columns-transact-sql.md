---
title: sys. sp_cdc_get_captured_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: rothja
ms.author: jroth
ms.openlocfilehash: cf7c7ff03ec1318b1fe2fca8454f8ff39cd336a4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083743"
---
# <a name="syssp_cdc_get_captured_columns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定捕获实例所跟踪的捕获源列的变更数据捕获元数据信息。 并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2016 的各个[版本支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>参数  
 [ @capture_instance = ]"*capture_instance*"  
 与源表关联的捕获实例的名称。 *capture_instance*为**sysname** ，且不能为 NULL。  
  
 若要报告表的捕获实例，请运行[sys.databases. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)存储过程。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|源表架构的名称。|  
|source_table|**sysname**|源表的名称。|  
|capture_instance|**sysname**|捕获实例的名称。|  
|column_name|**sysname**|捕获的源列的名称。|  
|column_id|**int**|源表中的列 ID。|  
|column_ordinal|**int**|源表中列的位置。|  
|data_type|**sysname**|列数据类型。|  
|character_maximum_length|**int**|如果为基于字符的列，则为该列的最大字符长度；否则为 NULL。|  
|numeric_precision|**tinyint**|如果为基于数值的列，则为该列的精度；否则为 NULL。|  
|numeric_precision_radix|**smallint**|如果为基于数值的列，则为该列的精度基数；否则为 NULL。|  
|numeric_scale|**int**|如果为基于数值的列，则为该列的小数位数；否则为 NULL。|  
|datetime_precision|**smallint**|如果为基于日期时间的列，则为该列的精度；否则为 NULL。|  
  
## <a name="remarks"></a>备注  
 使用 sys. sp_cdc_get_captured_columns 获取有关通过查询捕获实例查询函数返回的已捕获列的列信息[。 fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) [或 fn_cdc_get_net_changes_<capture_instance ](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)>。 在捕获实例的生命周期内，列名、ID 和位置保持不变。 当所跟踪表中的基础源列的数据类型发生更改时，只有列数据类型会更改。 添加到源表或从中删除的列不会影响现有捕获实例的已捕获列。  
  
 使用[sys. sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)获取有关应用于源表的数据定义语言（ddl）语句的信息。 任何修改所跟踪源列的结构的 DDL 更改都会在结果集中返回。  
  
## <a name="permissions"></a>权限  
 要求具有 db_owner 固定数据库角色中的成员资格。 对于所有其他用户，要求对源表中的所有已捕获列具有 SELECT 权限；如果已定义捕获实例的访问控制角色，则还要求具有该数据库角色的成员身份。 当调用方没有查看源数据的权限时，函数将返回错误 22981（对象不存在或访问被拒绝。）。  
  
## <a name="examples"></a>示例  
 下例返回有关 `HumanResources_Employee` 捕获实例中的捕获列的信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys. sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
