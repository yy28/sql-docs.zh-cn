---
title: "DBCC CHECKIDENT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
caps.latest.revision: 63
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d81aa2c26cf693d8ed5613c2aceb970a54db5aca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  检查 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定表的当前标识值，如有必要，则更改标识值。 还可以使用 DBCC CHECKIDENT 为标识列手动设置新的当前标识值。  
   
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCC CHECKIDENT   
 (   
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 *table_name*  
 是要对其当前标识值进行检查的表名。 指定的表必须包含标识列。 表名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 必须分隔两个或三个部分组成的名称，如 Person.AddressType 或 [Person.AddressType]。   
  
 NORESEED  
 指定不应更改当前标识值。  
  
 RESEED  
 指定应该更改当前标识值。  
  
 *new_reseed_value*  
 用作标识列的当前值的新值。  
  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释  
 对当前标识值所做的具体更正取决于参数规范。  
  
|DBCC CHECKIDENT 命令|标识更正或所做的更正|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *table_name*，NORESEED)|不重置当前标识值。 DBCC CHECKIDENT 将返回标识列的当前标识值和当前最大值。 如果这两个值不相同，则应重置标识值，以避免值序列中的潜在错误或空白。|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> 或<br /><br /> DBCC CHECKIDENT ( *table_name*，重设种子)|如果表的当前标识值小于标识列中存储的最大标识值，则使用标识列中的最大值对其进行重置。 请参阅后面的“例外”一节。|  
|DBCC CHECKIDENT ( *table_name*，重设种子， *new_reseed_value* )|当前标识值设置为*new_reseed_value*。 如果任何行具有已不插入表，因为该表的创建，或如果已使用 TRUNCATE TABLE 语句中删除所有行，第一行后运行 DBCC CHECKIDENT 插入使用*new_reseed_value*作为标识。<br /><br /> 如果表中存在行，将下一行插入与*new_reseed_value*值。 在版本[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更早版本，则插入的下一步行使用*new_reseed_value* +[当前增量](../../t-sql/functions/ident-incr-transact-sql.md)值。<br /><br /> 如果该表不为空，那么将标识值设置为小于标识列中的最大值的数字时，将会出现下列情况之一：<br /><br /> -如果标识列上存在 PRIMARY KEY 或 UNIQUE 约束，则，因为生成的标识值将与现有值冲突，在更高版本到表的插入操作将生成错误消息 2627年。<br /><br /> -如果 PRIMARY KEY 或 UNIQUE 约束不存在，更高版本的插入操作将导致重复的标识值。|  
  
## <a name="exceptions"></a>异常  
 下表列出了 DBCC CHECKIDENT 不自动重置当前标识值时的条件，并提供了重置该值的方法。  
  
|条件|重置方法|  
|---------------|-------------------|  
|当前标识值大于表中的最大值。|执行 DBCC CHECKIDENT (*table_name*，NORESEED) 来确定在列中，当前最大值，然后指定此值*new_reseed_value*中 DBCC CHECKIDENT (*table_名称*，重设种子，*new_reseed_value*) 命令。<br /><br /> -或者-<br /><br /> 执行 DBCC CHECKIDENT (*table_name*，重设种子，*new_reseed_value*) 与*new_reseed_value*设置为非常低的值，然后运行 DBCC CHECKIDENT (*table_name*，重设种子) 若要更正的值。|  
|删除表中的所有行。|执行 DBCC CHECKIDENT (*table_name*，重设种子，*new_reseed_value*) 与*new_reseed_value*设置为所需的起始值。|  
  
## <a name="changing-the-seed-value"></a>更改种子值  
 种子值是针对装入表的第一行插入到标识列的值。 所有后续行都包含当前标识值和增量值，其中当前标识值是为当前表或视图生成的最新标识值。  
  
 不能使用 DBCC CHECKIDENT 执行下列任务：  
  
-   更改创建表或视图时为标识列指定的原始种子值。  
  
-   重设表或视图中的现有行的种子值。  
  
 若要更改原始种子值并重设所有现有行的种子值，必须删除并重新创建标识列，然后为标识列指定新的种子值。 当表包含数据时，还会将标识号添加到具有指定种子值和增量值的现有行中。 无法保证行的更新顺序。  
  
## <a name="result-sets"></a>结果集  
 无论是否为包含标识列的表指定了任何选项，DBCC CHECKIDENT 都会为所有操作（仅在指定新的种子值时例外）返回以下消息：  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 当使用 DBCC CHECKIDENT 使用重新设定种子指定一个新的种子值*new_reseed_value*，将返回以下消息。  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissions  
 调用方必须拥有包含的表，该架构或是的成员**sysadmin**固定服务器角色、 **db_owner**固定数据库角色或**db_ddladmin**固定数据库角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-resetting-the-current-identity-value-if-it-is-needed"></a>A. 根据需要重置当前标识值  
 以下示例根据需要重置 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]  数据库中指定表的当前标识值。  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. 报告当前标识值  
 以下示例报告 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的指定表中的当前标识值，但如果该标识值不正确，不会进行更正。  
  
```  
USE AdventureWorks2012;   
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);   
GO  
  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. 强制将当前标识值设为新值  
 以下示例强制将 `AddressTypeID` 表中的 `AddressType` 列中的当前标识值设置为 10。 因为该表有现有行，因此下一个插入行将使用 11 作为值，即为该列值定义的当前新增量值加上 1。  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY（属性）(Transact-SQL)](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE (Transact-SQL)](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40;Transact SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[Ident_incr 和 &#40;Transact SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
  
  

