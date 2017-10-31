---
title: "放置默认值 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb7de5514d74ed4650d44bed145c32e9bea2c845
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除一个或多个用户定义的默认值。  
  
> [!IMPORTANT]  
>  中的下一个版本将删除 DROP DEFAULT [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 请不要在新的开发工作中使用 DROP DEFAULT，并准备修改当前使用它的应用程序。 请改用可以使用的 DEFAULT 关键字创建的默认定义[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地将删除默认值。  
  
 *schema_name*  
 默认值所属架构的名称。  
  
 *default_name*  
 现有默认值的名称。 若要查看存在的默认值的列表，请执行**sp_help**。 默认值必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 可以选择是否指定默认架构名称。  
  
## <a name="remarks"></a>注释  
 之后将删除默认值，通过执行解除默认**sp_unbindefault**如果默认值当前绑定到某一列或别名数据类型。  
  
 从允许空值的列中删除默认值后，当添加行且没有显式提供值时，将在该位置插入 NULL。 从 NOT NULL 列中删除默认值后，当添加行且没有显式提供值时，将返回错误消息。 这些行以后作为典型 INSERT 语句行为的一部分添加。  
  
## <a name="permissions"></a>Permissions  
 若要执行 DROP DEFAULT，用户至少应对默认值所属的架构具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-default"></a>A. 删除默认值  
 如果默认值没有绑定到列或别名数据类型，只需使用 DROP DEFAULT 即可将其删除。 以下示例删除用户创建的名为 `datedflt` 的默认值。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]可以使用以下语法。  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. 删除绑定到列的默认值  
 以下示例取消与 `EmergencyContactPhone` 表的 `Contact` 列关联的默认值的绑定，然后删除名为 `phonedflt` 的默认值。  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

