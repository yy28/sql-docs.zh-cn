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
ms.openlocfilehash: 5bef3e4902562edde0adb2a4f495c51e6a82b091
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535279"
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
`[ @conflict_table = ] 'conflict_table'` 是的冲突表的名称。 *conflict_table*是**sysname**，默认值为**%**。 如果*conflict_table*指定为 NULL 或**%**，则认为冲突是删除冲突和相匹配的行*rowguid*和*origin_datasource 中*并*source_object*从删除[MSmerge_conflicts_info &#40;-&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表。  
  
`[ @source_object = ] 'source_object'` 是源表的名称。 *source_object*是**nvarchar(386)**，默认值为 NULL。  
  
`[ @rowguid = ] 'rowguid'` 是删除冲突的行标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
`[ @origin_datasource = ] 'origin_datasource'` 为冲突的起源。 *origin_datasource 中*是**varchar(255)**，无默认值。  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'` 是一个标志，指示*conflict_table*是如果要删除为空。 *drop_table_if_empty*是**varchar(10)**，默认值为 FALSE。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_deletemergeconflictrow**合并复制中使用。  
  
 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)表是系统表，并且不删除从数据库中，即使它为空。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
