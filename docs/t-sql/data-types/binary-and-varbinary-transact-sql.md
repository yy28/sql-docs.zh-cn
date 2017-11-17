---
title: "binary 和 varbinary (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 8/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6aaf00b8e846316c92897360932703a013150e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="binary-and-varbinary-transact-sql"></a>binary 和 varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

固定长度或可变长度的 Binary 数据类型。
  
## <a name="arguments"></a>参数  
**二进制**[(  *n*  )] 固定长度的二进制数据的长度，  *n* 字节，其中 *n* 是一个值从 1 到 8,000。 存储大小是 *n* 字节。
  
**varbinary** [(  *n*   |  **max**)] 长度可变的二进制数据。 *n*可以是一个介于 1 到 8,000。 **最大**指示最大存储大小为 2 ^31-1 个字节。 存储大小为所输入数据的实际长度 + 2 个字节。 所输入数据的长度可以是 0 字节。 ANSI SQL 同义词**varbinary**是**二进制改变**。
  
## <a name="remarks"></a>注释  
当 *n* 未指定数据定义或变量声明语句中的默认长度为 1。 当 *n* 未指定使用 CAST 函数的默认长度为 30。

| 数据类型 | 何时使用... |
| --- | --- |
| **binary** | 列数据条目的大小是一致的。|
| **varbinary** | 列数据条目的大小相差迥异。|
| **varbinary(max)** | 列数据条目超过 8000 个字节。|


## <a name="converting-binary-and-varbinary-data"></a>将二进制和 varbinary 数据转换
当数据转换为字符串数据类型 (**char**， **varchar**， **nchar**， **nvarchar**，**二进制**， **varbinary**，**文本**， **ntext**，或**映像**) 到**二进制**或**varbinary**数据类型的长度不等，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来填充或截断右侧的数据。 当将其他数据类型转换为**二进制**或**varbinary**，填充或左侧截断数据。 填充将通过使用十六进制的零来完成。
  
将数据转换成**二进制**和**varbinary**数据类型是有用如果**二进制**数据是最简单的方法来移动数据。 将任何值的任何转换到大型的二进制值键入足够大小，然后回类型，总是会导致相同的值如果这两个转换都发生在相同版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 值的二进制表示形式在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本之间可能会有所不同。
  
你可以将转换**int**， **smallint**，和**tinyint**到**二进制**或**varbinary**，但是，如果你将转换**二进制**回整数值，此值的值将为不同于原始的整数值，如果发生截断。 例如，以下 SELECT 语句显示整数值 `123456` 通常被存储为二进制值 `0x0001e240`：
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
但是，以下`SELECT`语句显示，如果**二进制**目标是太小，无法容纳整个值、 前导数字以无提示方式将被截断，以便相同的数量存储为`0xe240`:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
以下批处理显示，这种自动截断会影响算术运算而不产生错误：
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
最终结果为 `57921`，而不是 `123457`。
  
> [!NOTE]  
>  类型的任何数据之间的转换和**二进制**不保证数据类型都是相同的版本之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  

