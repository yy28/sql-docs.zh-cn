---
title: "sp_bindrule (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs: TSQL
helpviewer_keywords: sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbc90db869ea98ebfdf99bf9cbdf56d9019b28a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将规则绑定到列或别名数据类型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]使用[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)相反。 检查约束通过使用的 CHECK 关键字创建[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)语句。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@rulename=**] *规则*  
 由 CREATE RULE 语句创建的规则的名称。 *规则*是**nvarchar(776)**，无默认值。  
  
 [  **@objname=**] *object_name*  
 要绑定规则的表和列或别名数据类型。 无法将规则绑定到**文本**， **ntext**，**映像**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**，CLR 用户定义类型时，或**时间戳**列。 无法将规则绑定到计算列。  
  
 *object_name*是**nvarchar(776)**无默认值。 如果*object_name*是一个部分名称，它被解析为别名数据类型。 如果是由两部分或三部分组成的名称，则首先按表和列进行解析；如果解析失败，则按别名数据类型进行解析。 默认情况下，该别名数据类型的现有列继承*规则*除非规则已绑定到列的直接。  
  
> [!NOTE]  
>  *object_name*可以包含括号**[**和**]**字符的形式分隔的标识符字符。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
> [!NOTE]  
>  可以将针对使用别名数据类型的表达式创建的规则绑定到列或别名数据类型，但在引用这些规则时无法编译它们。 避免使用对别名数据类型创建的规则。  
  
 [  **@futureonly=** ] *futureonly_flag*  
 仅当将规则绑定到别名数据类型时才能使用。 *future_only_flag*是**varchar(15)**默认值为 NULL。 当设置为此参数**futureonly**防止继承新规则的别名数据类型的现有列。 如果*futureonly_flag*为 NULL，新规则绑定到当前具有任何规则或使用该别名数据类型的现有规则别名数据类型的列。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 可以将新规则绑定到列 （尽管使用 CHECK 约束是首选方法） 或别名数据类型与**sp_bindrule**必须先解除绑定现有规则。 覆盖原有规则。 如果使用现有 CHECK 约束将规则绑定到列，那么将评估所有限制。 不能将规则绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 当尝试执行 INSERT 语句时（而非绑定时），将强行执行规则。 你可以将字符规则绑定到的列**数值**数据类型，尽管此类插入操作无效。  
  
 别名数据类型的现有列继承新规则，除非*futureonly_flag*指定为**futureonly**。 使用别名数据类型定义的新列始终继承规则。 但是，如果 ALTER TABLE 语句的 ALTER COLUMN 子句将列的数据类型更改为绑定规则的别名数据类型，那么列不会继承与数据类型绑定的规则。 规则必须专门绑定到列使用**sp_bindrule**。  
  
 当将规则绑定到列时，将相关的信息添加到**sys.columns**表。 当将规则绑定到别名数据类型时，将相关的信息添加到**sys.types**表。  
  
## <a name="permissions"></a>Permissions  
 若要将规则绑定到表列，您必须具有表的 ALTER 权限。 若要将规则绑定到别名数据类型，您需要具有别名数据类型的 CONTROL 权限或该类型所属架构的 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. 将规则绑定到列  
 假设已经用 CREATE RULE 语句在当前数据库中创建了名为 `today` 的规则，以下示例将规则绑定到 `HireDate` 表的 `Employee` 列。 将行添加到 `Employee` 时，按照 `HireDate` 规则检查 `today` 列的数据。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. 将规则绑定到别名数据类型  
 假设存在名为 `rule_ssn` 的规则和名为 `ssn` 的别名数据类型，以下示例将 `rule_ssn` 绑定到 `ssn`。 在 CREATE TABLE 语句中，类型为 `ssn` 的列会继承 `rule_ssn` 规则。 类型的现有列`ssn`还继承`rule_ssn`规则，除非**futureonly**为指定*futureonly_flag*，或`ssn`具有直接绑定到它的规则。 绑定到列的规则始终优先于绑定到数据类型的规则。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. 使用 futureonly_flag  
 以下示例将 `rule_ssn` 规则绑定到别名数据类型 `ssn`。 由于已指定 `futureonly`，因此不影响类型为 `ssn` 的现有列。  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔的标识符  
 下面的示例演示了利用中的分隔标识符*object_name*参数。  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE (Transact-SQL)](../../t-sql/statements/create-rule-transact-sql.md)   
 [删除规则 &#40;Transact SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
