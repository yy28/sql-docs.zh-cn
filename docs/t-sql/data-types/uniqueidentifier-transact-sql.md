---
title: uniqueidentifier (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/1/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 95e22eb2089569978122a221aa9afdfb6751ab79
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37988609"
---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

16 字节 GUID。
  
## <a name="remarks"></a>Remarks  
uniqueidentifier 数据类型的列或局部变量可通过以下方式初始化为一个值：
-   通过使用 [NEWID](../../t-sql/functions/newid-transact-sql.md) 或 [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 函数。    
-   通过从 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 形式的字符串常量进行转换，其中，每个 x 都是 0-9 或 a-f 范围内的十六进制数字。 例如，6F9619FF-8B86-D011-B42D-00C04FC964FF 为有效的 uniqueidentifier 值。  
  
比较运算符可与 uniqueidentifier 值一起使用。 不过，排序不是通过比较两个值的位模式来实现的。 可针对 uniqueidentifier 值执行的运算只有比较运算（=、<>、\<、>、\<=、>=）以及检查是否为 NULL（IS NULL 和 IS NOT NULL）。 不能使用其他算术运算符。 除 IDENTITY 之外的所有列约束和属性均可对 uniqueidentifier 数据类型使用。
  
具有更新订阅的合并复制和事务复制使用 uniqueidentifier 列来确保在表的多个副本中唯一地标识行。
  
## <a name="converting-uniqueidentifier-data"></a>转换 uniqueidentifier 数据  
出于从字符表达式转换的目的将 uniqueidentifier 类型视为字符类型，因此在转换到字符类型时要遵循截断规则。 也即，如果将字符表达式转换为不同大小的字符数据类型，则对于新数据类型而言过长的值将被截断。 请参阅“示例”部分。
  
## <a name="limitations-and-restrictions"></a>限制和局限

这些工具和功能不支持 `uniqueidentifier` 数据类型：
- PolyBase
- 适用于并行数据仓库的 [dwloader 加载工具](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader)

## <a name="examples"></a>示例  
以下示例将 `uniqueidentifier` 值转换为 `char` 数据类型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
以下示例演示在值过长而无法转换数据类型时如何截断数据。 因为 uniqueidentifier 类型限制为 36 个字符，所以，将截断超过该长度的字符。
  
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
[NEWID (Transact-SQL)](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID (Transact-SQL)](../../t-sql/functions/newsequentialid-transact-sql.md)    
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  
