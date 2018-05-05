---
title: sp_ivindexhasnullcols (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4431ae915c43d6ceb96200c3ebbf6aa976dd4ff3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  验证索引视图的聚集索引是否唯一，而且当索引视图将要用于创建事务发布时其聚集索引不包含任何可能为 Null 的列。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [ **@viewname**=] *****view_name*****  
 要验证的视图的名称。 *view_name*是**sysname**，无默认值。  
  
 [ **@fhasnullcols**=] *field_has_null_columns*输出  
 指示视图索引是否具有允许 NULL 值的列的标志。 *view_name*是**sysname**，无默认值。 返回的值**1**的视图索引是否允许 NULL 的列。 返回的值**0**如果视图不包含允许 null 值的列。  
  
> [!NOTE]  
>  如果该存储的过程本身返回的返回代码**1**，这意味着存储的过程执行失败，此值是**0** ，应当忽略。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_ivindexhasnullcols**事务复制使用。  
  
 默认情况下，发布中的索引视图项目创建为订阅服务器上的表。 但是，当索引列允许 NULL 值时，索引视图创建为订阅服务器上的索引视图而不是表。 通过执行此存储过程，可以警告用户当前索引视图中是否存在此问题。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_ivindexhasnullcols**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
