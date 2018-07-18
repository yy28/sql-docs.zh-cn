---
title: sys.sp_cdc_disable_table (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 16356cc8a5d427a9432ac8c753b1e51d915337d4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33255921"
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对当前数据库中指定的源表和捕获实例禁用变更数据捕获。 并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@source_schema=** ] *****source_schema*****  
 包含源表的架构的名称。 *source_schema*是**sysname**，无默认值，并不能为 NULL。  
  
 *source_schema*必须存在于当前数据库。  
  
 [  **@source_name=** ] *****source_name*****  
 要禁用其变更数据捕获的源表的名称。 *source_name*是**sysname**，无默认值，并不能为 NULL。  
  
 *source_name*必须存在于当前数据库。  
  
 [  **@capture_instance=** ] *****capture_instance***** | 所有  
 要对指定的源表禁用的捕获实例的名称。 *capture_instance*是**sysname**和不能为 NULL。  
  
 当指定 all 时，所有捕获实例为定义*source_name*处于禁用状态。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sys.sp_cdc_disable_table**删除变更数据捕获更改与指定的源的表和捕获实例关联的表和系统函数。 它将删除与中的更改数据捕获系统表和集的指定的捕获实例关联的任何行**is_tracked_by_cdc**列中的表条目[sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)目录视图为 0。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**db_owner**固定的数据库角色。  
  
## <a name="examples"></a>示例  
 下例对 `HumanResources.Employee` 表禁用了变更数据捕获。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_enable_table &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
