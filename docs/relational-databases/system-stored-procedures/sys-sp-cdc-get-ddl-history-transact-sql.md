---
title: "sys.sp_cdc_get_ddl_history (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs: TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3c216751e54d6263f5f133e7785df8c0f50f33
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcgetddlhistory-transact-sql"></a>sys.sp_cdc_get_ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回自对指定的捕获实例启用变更数据捕获后与该捕获实例关联的数据定义语言 (DDL) 更改历史记录。 并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>参数  
 [ @capture_instance =] '*capture_instance*  
 与源表关联的捕获实例的名称。 *capture_instance*是**sysname**和不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|源表架构的名称。|  
|source_table|**sysname**|源表的名称。|  
|capture_instance|**sysname**|捕获实例的名称。|  
|required_column_update|**bit**|表示 DDL 更改要求对更改表中的列进行更改以反映对源列所做的数据类型更改。|  
|ddl_command|**nvarchar(max)**|应用到源表的 DDL 语句。|  
|ddl_lsn|**binary(10)**|与 DDL 更改关联的日志序列号 (LSN)。|  
|ddl_time|**datetime**|与 DDL 更改关联的时间。|  
  
## <a name="remarks"></a>注释  
 在中维护更改源表的列结构，如添加或删除列，或更改某个现有列的数据类型的 DDL 修改到源表[cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)表。 您可使用此存储过程报告以上更改。 当捕获进程读取日志中的 DDL 事务时，将向 cdc.ddl_history 中添加项。  
  
## <a name="permissions"></a>Permissions  
 要求拥有 db_owner 固定数据库角色的成员身份以返回针对数据库中所有捕获实例的行。 对于所有其他用户，要求对源表中的所有已捕获列具有 SELECT 权限；如果已定义捕获实例的访问控制角色，则还要求具有该数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将列添加到源表 `HumanResources.Employee` 中，然后运行 `sys.sp_cdc_get_ddl_history` 存储过程来报告应用到与捕获实例 `HumanResources_Employee` 关联的源表的 DDL 更改。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
