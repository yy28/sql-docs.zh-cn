---
title: sp_deletemergeconflictrow （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c8710aa297b01634d5307dbd3c057b9d51fe8f6f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85693258"
---
# <a name="sp_deletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  从冲突表[MSmerge_conflicts_info 或 &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表中删除行。 此存储过程在存储冲突表的计算机的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>自变量  
`[ @conflict_table = ] 'conflict_table'`冲突表的名称。 *conflict_table*的默认值为**sysname**，默认值为 **%** 。 如果将*conflict_table*指定为 NULL 或 **%** ，则认为冲突为删除冲突，并从[MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表中删除与*rowguid*和*origin_datasource*和*source_object*匹配的行。  
  
`[ @source_object = ] 'source_object'`源表的名称。 *source_object*为**nvarchar （386）**，默认值为 NULL。  
  
`[ @rowguid = ] 'rowguid'`删除冲突的行标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
`[ @origin_datasource = ] 'origin_datasource'`冲突的起源。 *origin_datasource*的值为**varchar （255）**，无默认值。  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'`一个标志，指示在为空时要删除*conflict_table* 。 *drop_table_if_empty*的值为**varchar （10）**，默认值为 FALSE。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_deletemergeconflictrow**用于合并复制。  
  
 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表是系统表，不会从数据库中删除（即使它为空）。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
