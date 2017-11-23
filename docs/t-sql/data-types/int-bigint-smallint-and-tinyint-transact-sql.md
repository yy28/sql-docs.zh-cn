---
title: "int、 bigint、 smallint 和 tinyint (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 9/8/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs: TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2e99ccb97dc5c36f8b7870a042963d6302b3f1eb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int、bigint、smallint 和 tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

使用整数数据的精确数字数据类型。 若要在数据库中节省空间，使用的最小的数据类型可以可靠地包含所有可能的值。 例如，则 tinyint 不能够满足一个人的年龄，因为没有人位于要超过 255 年。 但是 tinyint 都不会是某个大厦的年龄足够因为某个大厦可能超过 255 年。
  
|数据类型|范围|存储器|  
|---|---|---|
|**bigint**|-2^63 (-9,223,372,036,854,775,808) 到 2^63-1 (9,223,372,036,854,775,807)|8 个字节|  
|**int**|-2^31 (-2,147,483,648) 到 2^31-1 (2,147,483,647)|4 个字节|  
|**int**|-2^15 (-32,768) 到 2^15-1 (32,767)|2 个字节|  
|**tinyint**|0 到 255|1 个字节|  
  
## <a name="remarks"></a>注释  
**Int**数据类型是中的主整数数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **Bigint**整数值可能超过受该范围时，数据类型旨在用于**int**数据类型。
  
**bigint**适合之间**smallmoney**和**int**数据类型优先级图表中。
  
函数将返回**bigint**仅当参数表达式为**bigint**数据类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不自动升级其他整数数据类型 (**tinyint**， **smallint**，和**int**) 到**bigint**。
  
> [!CAUTION]  
>  当你使用 +、-， \*，/，或 %算术运算符执行的隐式或显式转换**int**， **smallint**， **tinyint**，或**bigint**常量值复制到**float**，**实际**，**十进制**或**数值**数据类型、 的规则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时它会计算的数据类型和精度的表达式结果与不同，具体取决于查询是 autoparameterized 或不适用。  
>   
>  因此，查询中的类似表达式有时可能会生成不同的结果。 当查询不是 autoparameterized 时，常量值首先转换为**数值**，其精度是仅足以容纳之前将转换为指定的数据类型的常数的值。 例如，常量值 1 转换为**数字 （1，0）**，而 250 常量的值转换为**数字 （3，0）**。  
>   
>  常量的值始终 autoparameterized 查询时，已转换为**数字 （10，0）**之前将转换为最终的数据类型。 如果涉及 / 运算符，则对于类似查询而言，不仅结果类型的精度可能不同，而且结果值也可能不同。 例如，包含表达式的 autoparameterized 查询的结果值`SELECT CAST (1.0 / 7 AS float)`，与不是 autoparameterized，同一查询的结果值不同，因为 autoparameterized 查询的结果将被截断，使其适合**数字 （10，0）**数据类型。  
  
## <a name="converting-integer-data"></a>将整数数据转换
将整数隐式转换为字符数据类型时，如果整数太大而无法容纳到字符字段中，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会输入 ASCII 字符 42，即星号 (*)。
  
大于 2147483647 转换为整数常量**十进制**数据类型，不**bigint**数据类型。 下面的示例演示，当超过阈值时，结果的数据类型已从更改**int**到**十进制**。
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>示例  
下面的示例创建表使用**bigint**， **int**， **smallint**，和**tinyint**数据类型。 值插入到每列中并在 SELECT 语句中返回。
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
