---
title: "uniqueidentifier (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 047e09cdd99d088379008fb68141dae31a09b08d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

16 字节 GUID。
  
## <a name="remarks"></a>注释  
列或的本地变量**uniqueidentifier**数据类型可以通过以下方式初始化为值：
-   使用 NEWID 函数。  
-   通过从窗体中的字符串常量转换*xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*- *xxxxxxxxxxxx*，其中的每个*x*是范围 0-9 或 a-f 的十六进制数字。 例如，6F9619FF-8B86-D011-B42D-00C04FC964FF 是一个有效**uniqueidentifier**值。  
  
比较运算符可与**uniqueidentifier**值。 不过，排序不是通过比较两个值的位模式来实现的。 可以针对执行的唯一操作**uniqueidentifier**值是比较 (=、 <>， \<，>， \<=、 > =) 和检查是否为 NULL （IS NULL 和 IS NOT NULL）。 不能使用其他算术运算符。 所有列约束和属性，除了标识，可以都用在上**uniqueidentifier**数据类型。
  
合并复制和带有更新订阅使用事务复制**uniqueidentifier**列若要确保行进行唯一标识跨多个表的副本。
  
## <a name="converting-uniqueidentifier-data"></a>转换 uniqueidentifier 数据  
**Uniqueidentifier**类型被视为出于从字符表达式，转换的字符类型，并因此受到将转换为字符类型的截断规则。 也即，如果将字符表达式转换为不同大小的字符数据类型，则对于新数据类型而言过长的值将被截断。 请参阅“示例”部分。
  
## <a name="limitations-and-restrictions"></a>限制和局限

这些工具和功能不支持`uniqueidentifier`数据类型：
- PolyBase
- [dwloader 加载工具](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader)并行数据仓库

## <a name="examples"></a>示例  
以下示例将 `uniqueidentifier` 值转换为 `char` 数据类型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
以下示例演示在值过长而无法转换数据类型时如何截断数据。 因为**uniqueidentifier**类型仅限于 36 个字符，超过该长度的字符将被截断。
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40;Transact SQL &#41;](../../t-sql/functions/newid-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  

