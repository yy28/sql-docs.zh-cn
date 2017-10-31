---
title: "拖放类型 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4187c6bff08e5502f5edc6acd8d82334684a68d4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从当前数据库中删除别名数据类型或公共语言运行时 (CLR) 用户定义的类型。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地删除类型。  
  
 *schema_name*  
 别名或用户定义的类型所属的架构名。  
  
 *类型 _ 名称*  
 要删除的别名数据类型或用户定义的类型的名称。  
  
## <a name="remarks"></a>注释  
 在满足以下任何条件的情况下，将不执行 DROP TYPE 语句：  
  
-   数据库中存在包含别名数据类型列或用户定义的类型列的表。 可以通过查询来获取有关别名或用户定义的类型列的信息[sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)或[sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md)目录视图。  
  
-   存在定义中引用了别名类型和用户定义类型的计算列、CHECK 约束、架构绑定视图和绑定到架构的函数。 有关这些引用的信息可以通过查询获取[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)目录视图。  
  
-   存在在数据库中创建的函数、存储过程或触发器，且这些例程使用别名类型或用户定义的类型的变量和参数。 可以通过查询来获取有关别名或用户定义的类型参数的信息[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)或[sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>Permissions  
 要求具有控制权限，在*type_name*或 ALTER 权限*schema_name*。  
  
## <a name="examples"></a>示例  
 以下示例假设已经在当前数据库中创建了一个名为 `ssn` 的类型。  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

