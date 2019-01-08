---
title: sp_addtabletocontents (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ad6e8fe499e3ffe57a745cfb924bdc792938dd9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810939"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将源表中当前不在跟踪表内的任何行的引用插入到合并跟踪表中。 使用此选项，如果您具有大容量加载数据使用的大量**bcp**，这不会激发合并跟踪触发器。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@table_name=**] **'**_table_name_  
 是表的名称。 *table_name*是**sysname**，无默认值。  
  
 [  **@owner_name=**] **'**_owner_name_  
 是表的名称。 *owner_name*是**sysname**，默认值为 NULL。  
  
 [  **@filter_clause=** ] **'**_filter_clause_  
 指定一个筛选子句，该子句控制应将新加载的数据的哪些行添加到合并跟踪表。 *filter_clause*是**nvarchar(4000)**，默认值为 NULL。 如果*filter_clause*是**null**，所有大容量加载的行已添加。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addtabletocontents**仅用于合并复制。  
  
 中的行*table_name*由其**rowguidcol**和引用添加到合并跟踪表。 **sp_addtabletocontents**大容量复制数据到使用合并复制发布的表之后，应使用。 该存储过程将启动对已复制行的跟踪，并确保下一次同步中包括这些新行。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addtabletocontents**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
