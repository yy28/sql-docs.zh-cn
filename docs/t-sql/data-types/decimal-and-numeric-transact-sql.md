---
title: "小数和数值 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6c8ec4ea2255e8496b6e5ed464fbff220d270e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decimal-and-numeric-transact-sql"></a>decimal 和 numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

带固定精度和小数位数的数值数据类型。 小数和数值是同义词，可以互换使用。
  
## <a name="arguments"></a>参数  
**十进制**[ **(***p*[ **，***s*] **)**] 和**数字**[ **(***p*[ **，***s*] **)**]  
固定精度和小数位数。 使用最大精度时，有效值的范围为 - 10^38 +1 到 10^38 - 1。 ISO 同义词**十进制**是**dec**和**dec (***p*， *s***)**. **数值**功能上等效于**十进制**。
  
p（精度）  
最多可以存储的十进制数字的总位数，包括小数点左边和右边的位数。 该精度必须是从 1 到最大精度 38 之间的值。 默认精度为 18。
  
> [!NOTE]  
>  Informatica 仅支持 16 有效位，而不考虑精度和指定的小数位数。  
  
*s* （缩放）  
小数点右边可以存储的十进制数字的位数。 此数减去从*p*以确定最多的小数点左侧的位数。 小数点右边可以存储的十进制数字的最大位数。 小数位数必须介于 0 到*p*。 仅在指定精度后才可以指定小数位数。 默认小数位数为 0;因此，0 < = *s* \< =  *p*。 最大存储大小基于精度而变化。
  
|精度|存储字节数|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica （通过 SQL Server PDW Informatica 连接器连接） 仅支持 16 有效位，而不考虑精度和指定的小数位数。  
  
## <a name="converting-decimal-and-numeric-data"></a>将 decimal 和 numeric 数据转换
有关**十进制**和**数值**数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]考虑每个精度和小数位数为不同的数据类型的特定组合。 例如， **decimal(5,5)**和**decimal(5,0)**被视为不同的数据类型。
  
在[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，自动转换为具有小数点的常数**数值**数据值，使用最小的精度和缩放必要。 例如，常量 12.345 转换为**数值**值，该值精度为 5，小数位数为 3。
  
从转换**十进制**或**数值**到**float**或**实际**可能会导致某些丢失精度。 从转换**int**， **smallint**， **tinyint**， **float**，**实际**， **money**，或**smallmoney**为**十进制**或**数值**也会导致溢出。
  
默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用时将转换到数值进行舍入**十进制**或**数值**具有较低的精度和小数位数的值。 但如果 SET ARITHABORT 选项为 ON，则发生溢出时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会产生错误。 若仅降低精度和小数位数，则不会产生错误。
  
在将 float 值或实数值转换为 decimal 或 numeric 类型时，decimal 值不会超过 17 位小数。 任何小于 5E-18 的 float 值总是会转换为 0。
  
## <a name="examples"></a>示例  
下面的示例创建表使用**十进制**和**数值**数据类型。  值将插入每一列，并使用 SELECT 语句返回结果。
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

