---
title: "sp_deletemergeconflictrow (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e085a7010f25f40b95a45d8ddd0c7b455d7266c6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从冲突表删除行或[MSmerge_conflicts_info &#40;Transact SQL &#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表。 此存储过程在存储冲突表的计算机的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@conflict_table=**] *conflict_table*  
 冲突表的名称。 *conflict_table*是**sysname**，默认值为 **%** 。 如果*conflict_table*指定为 NULL 或 **%** ，冲突被假定为删除冲突和行匹配*rowguid*和*origin_datasource*和*source_object*从删除[MSmerge_conflicts_info &#40;Transact SQL &#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表。  
  
 [  **@source_object=**] *source_object*  
 是源表的名称。 *source_object*是**nvarchar(386)**，默认值为 NULL。  
  
 [  **@rowguid =**] *rowguid*  
 是删除冲突的行标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
 [  **@origin_datasource=**] *origin_datasource*  
 是的来源。 *origin_datasource*是**varchar(255)**，无默认值。  
  
 [  **@drop_table_if_empty=**] *drop_table_if_empty*  
 是标志，指示*conflict_table*是要删除如果为空。 *drop_table_if_empty*是**varchar(10)**，默认值为 FALSE。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_deletemergeconflictrow**合并复制中使用。  
  
 [MSmerge_conflicts_info &#40;Transact SQL &#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表是系统表，并且不删除从数据库中，即使它为空。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
