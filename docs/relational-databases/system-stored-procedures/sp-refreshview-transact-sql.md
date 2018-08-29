---
title: sp_refreshview (TRANSACT-SQL) |Microsoft Docs
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
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed5f50b9b95f2f156632fb14c2cd471ef010bcac
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031475"
---
# <a name="sprefreshview-transact-sql"></a>sp_refreshview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于更新指定的未绑定到架构的视图的元数据。 由于视图所依赖的基础对象的更改，视图的持久元数据会过期。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>参数  
 [  **@viewname=** ] **'***viewname*****  
 视图名称。 *viewname*是**nvarchar**，无默认值。 *viewname*可以是多部分标识符，但只能引用当前数据库中的视图。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败）  
  
## <a name="remarks"></a>Remarks  
 如果不使用 schemabinding 创建视图**sp_refreshview**影响视图定义的对象视图发生更改时，应运行。 否则，当查询视图时，可能会生成意外结果。  
  
## <a name="permissions"></a>Permissions  
 要求对视图具有 ALTER 权限，并对视图列引用的公共语言运行时 (CLR) 用户定义类型和 XML 架构集合具有 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-updating-the-metadata-of-a-view"></a>A. 更新视图的元数据  
 以下示例刷新视图 `Sales.vIndividualCustomer` 的元数据。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. 创建脚本，该脚本可更新与更改对象有依赖关系的所有视图  
 假定表 `Person.Person` 进行了更改，其更改方式影响了基于此表创建的所有视图的定义。 以下示例将创建一个脚本，以便为与表 `Person.Person` 有依赖关系的所有视图刷新源数据。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
