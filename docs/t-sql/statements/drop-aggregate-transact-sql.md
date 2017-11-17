---
title: "拖放聚合 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a9fcab3dc576f15110bed8c1c82271731f326280
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除用户定义的聚合函数。 用户定义聚合函数通过使用创建[CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地将删除聚合。  
  
 *schema_name*  
 用户定义聚合函数所属的架构的名称。  
  
 *aggregate_name*  
 要删除的用户定义聚合函数的名称。  
  
## <a name="remarks"></a>注释  
 如果存在使用了引用要删除的用户定义聚合函数的架构绑定而创建的任何视图、函数或存储过程，则不会执行 DROP AGGREGATE。  
  
## <a name="permissions"></a>Permissions  
 若要执行 DROP AGGREGATE，用户至少必须对用户定义聚合所属的架构有 ALTER 权限，或对聚合有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例将删除聚合 `Concatenate`。  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建聚合 &#40;Transact SQL &#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [创建用户定义的聚合](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  

