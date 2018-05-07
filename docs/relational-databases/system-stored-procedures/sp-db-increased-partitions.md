---
title: sp_db_increased_partitions |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b63255e4f15505dc75dfdf92f550a1d6d4149028
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对指定的数据库启用或禁用对多达 15000 个分区的支持。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>参数  
 [ @dbname=] '*database_name*  
 数据库的名称。 *dbname*是**sysname**默认值为 NULL。 如果*dbname*未指定，则使用当前数据库。  
  
 [ @increased_partitions=] '*increased_partitions*  
 对指定的数据库启用或禁用对 15000 个分区的支持。 *increased_partitions*是**varchar(6)** 默认值为 NULL。 要启用支持，则接受的值是“ON”或“TRUE”；要禁用支持，则接受的值为“OFF”和“FALSE”。 如果*increased_partitions*未指定，则该过程返回 1，表示为指定的数据库启用了支持或 0 来指示支持处于禁用状态。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 需要对指定的数据库拥有 ALTER DATABASE 权限。  
  
  
