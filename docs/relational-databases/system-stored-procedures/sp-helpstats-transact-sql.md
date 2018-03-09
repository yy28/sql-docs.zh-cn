---
title: "sp_helpstats (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45d6df772da027568b1fbd7593e404f291246bb4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关指定表中的列和索引的统计信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]若要获取有关统计信息的信息，请查询[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)和[sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)目录视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@objname=**] *object_name*  
 指定用来提供统计信息的表。 *object_name*是**nvarchar(520)**和不能为 null。 可以指定一个一部分或两部分名称。  
  
 [  **@results=**] *值*  
 指定要提供的信息的范围。 有效值包括**所有**和**统计信息**。 **所有**列出的所有索引和也有它们; 上创建的统计信息的列的统计信息**统计信息**只列出未与索引关联的统计信息。 *值*是**nvarchar(5)**默认值为统计信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 下表对结果集中的列进行了说明。  
  
|列名|Description|  
|-----------------|-----------------|  
|**statistics_name**|统计信息名称。 返回**sysname**和不能为 null。|  
|**statistics_keys**|统计信息所基于的键。 返回**nvarchar(2078)**和不能为 null。|  
  
## <a name="remarks"></a>注释  
 可以使用 DBCC SHOW_STATISTICS 显示特定索引或统计信息的相关详细统计信息。 有关详细信息，请参阅[DBCC SHOW_STATISTICS &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)和[sp_helpindex &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例通过执行 `sp_createstats`，为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中的所有用户表的所有合格列创建单列统计信息。 然后，运行 `sp_helpstats` 以查找在 `Customer` 表中创建的结果统计信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
