---
title: "CREATE DEFAULT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71c0f964d245be92fb8d2be19e074fbd34dd616e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  创建名为默认值的对象。 当绑定到列或别名数据类型时，如果插入时没有显式提供值，则默认值将指定一个值，以便将其插入该对象所绑定的列中（或者，如果是别名数据类型，则插入所有列中）。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]而应使用通过 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 关键字创建的默认定义。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 默认值所属架构的名称。  
  
 *default_name*  
 默认值的名称。 默认名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 可以选择是否指定默认值所有者名称。  
  
 *constant_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含仅常量 （它不能包含任何列或其他数据库对象的名称） 的值。 除了那些包含别名数据类型的表达式，可以使用任何常量、内置函数或数学表达式。 用户定义函数不能使用... 将字符和日期常量括在单引号 (); 资金，整数和浮点常量不需要引号引起来。 二进制数据必须以 0x 开头，货币数据必须以美元符号 ($) 开头。 默认值必须与列数据类型兼容。  
  
## <a name="remarks"></a>注释  
 只能在当前数据库中创建默认值名称。 按照架构，在数据库内默认值名称必须是唯一的。 当创建默认值时，使用**sp_bindefault**以将其绑定到列或别名数据类型。  
  
 如果默认值与其绑定的列不兼容，则在试图插入默认值时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会生成错误消息。 例如，不适用不能用作默认为**数值**列。  
  
 如果默认值对于它所绑定的列而言太长，则该值就会被截断。  
  
 不能将 CREATE DEFAULT 语句与其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句组合到单个批处理中。  
  
 必须先删除默认值，然后创建一个新的相同的名称，才能和默认值必须通过执行未绑定**sp_unbindefault**则会丢弃之前。  
  
 如果列同时有默认值以及与之关联的规则，则默认值不能违反该规则。 永远不会插入与规则冲突的默认值，每次试图插入这样的默认值时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都会生成错误消息。  
  
 当绑定到列以后，在以下情况下将插入默认值：  
  
-   非显式地插入值。  
  
-   在 INSERT 中使用 DEFAULT VALUES 或 DEFAULT 关键字来插入默认值。  
  
 如果在创建列时指定 NOT NULL 并且没有为其创建默认值，则当用户未能为该列输入项时，就会生成错误消息。 下表说明默认值的存在与将列定义为 NULL 或 NOT NULL 之间的关系。 表中的项显示了结果。  
  
|列定义|没有输入项，没有默认值|没有输入项，有默认值|输入 NULL，没有默认值|输入 NULL，有默认值|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|默认值|NULL|NULL|  
|**NOT NULL**|错误|默认值|error|error|  
  
 若要重命名默认值，使用**sp_rename**。 对于在默认报表，使用**sp_help**。  
  
## <a name="permissions"></a>Permissions  
 若要执行 CREATE DEFAULT，用户必须至少在当前数据库中拥有 CREATE DEFAULT 权限，并对在其中创建默认值的架构拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-simple-character-default"></a>A. 创建简单的字符默认值  
 以下示例创建名为 `unknown` 的字符默认值。  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. 绑定默认值  
 以下示例绑定在示例 A 中创建的默认值。只有当没有为 `Phone` 表的 `Contact` 列指定项时，默认值才会生效。 注意，省略任何项都与在 INSERT 语句中显式声明 NULL 不同。  
  
 由于不存在名为 `phonedflt` 的默认值，因此以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句将失败。 本例只用于演示。  
  
```tsql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE (Transact-SQL)](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [删除默认 &#40;Transact SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [删除规则 &#40;Transact SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

