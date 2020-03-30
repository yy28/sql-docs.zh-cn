---
title: DROP AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 356d08eaeeb470500ccf39c86872806cf2a9be9e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67984321"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除用户定义的聚合函数。 用户定义聚合函数是使用 [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md) 创建的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>参数  
 IF EXISTS   
 适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到[当前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）  。  
  
 仅当聚合已存在时对其进行有条件地删除。  
  
 *schema_name*  
 用户定义聚合函数所属的架构的名称。  
  
  aggregate_name  
 要删除的用户定义聚合函数的名称。  
  
## <a name="remarks"></a>备注  
 如果存在使用了引用要删除的用户定义聚合函数的架构绑定而创建的任何视图、函数或存储过程，则不会执行 DROP AGGREGATE。  
  
## <a name="permissions"></a>权限  
 若要执行 DROP AGGREGATE，用户至少必须对用户定义聚合所属的架构有 ALTER 权限，或对聚合有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例将删除聚合 `Concatenate`。  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE AGGREGATE (Transact-SQL)](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [创建用户定义的聚合](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
