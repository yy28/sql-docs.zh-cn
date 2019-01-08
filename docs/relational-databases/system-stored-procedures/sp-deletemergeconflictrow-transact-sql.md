---
title: sp_deletemergeconflictrow (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b11096a9f1ac9f8c5f5c04f3afc36f2776e988e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782949"
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从冲突表中删除行或[MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表。 此存储过程在存储冲突表的计算机的任何数据库中执行。  
  
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
 [  **@conflict_table=**] **'**_conflict_table_  
 冲突表的名称。 *conflict_table*是**sysname**，默认值为**%**。 如果*conflict_table*指定为 NULL 或**%**，则认为冲突是删除冲突和相匹配的行*rowguid*和*origin_datasource 中*并*source_object*从删除[MSmerge_conflicts_info &#40;-&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表。  
  
 [  **@source_object=**] **'**_source_object_  
 是源表的名称。 *source_object*是**nvarchar(386)**，默认值为 NULL。  
  
 [  **@rowguid =**] **'**_rowguid_  
 是删除冲突的行标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
 [  **@origin_datasource=**] **'**_origin_datasource 中_  
 为冲突的起源。 *origin_datasource 中*是**varchar(255)**，无默认值。  
  
 [  **@drop_table_if_empty=**] **'**_drop_table_if_empty_  
 是一个标志，指示*conflict_table*是如果要删除为空。 *drop_table_if_empty*是**varchar(10)**，默认值为 FALSE。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_deletemergeconflictrow**合并复制中使用。  
  
 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表是系统表，并且不删除从数据库中，即使它为空。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
