---
title: "nchar 和 nvarchar (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc7de3b64519f3d0fd1f2e9557ccf7196e3f07a8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 和 nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

字符数据类型都是固定长度**nchar**，或可变长度**nvarchar**，Unicode 数据并使用 UNICODE ucs-2 字符组。
  
## <a name="arguments"></a>参数  
**nchar** (n)  
固定长度的 Unicode 字符串数据。 *n*定义的字符串长度，并且必须是介于 1 与 4000 之间的值。 存储大小是两次 *n* 字节。 当排序规则代码页使用双字节字符时，存储大小仍是 *n* 字节。 具体取决于字符串的存储大小 *n* 字节可以是指定的值小于 *n* 。 ISO 同义词**nchar**是**国家/地区 char**和**国家字符集**...
  
**nvarchar** [(n |**最大**)]  
可变长度的 Unicode 字符串数据。 *n*定义的字符串长度和可以是从 1 到 4000 的值。 **最大**指示最大存储大小为 2 ^31-1 个字节 (2 GB)。 存储大小（以字节为单位）是所输入数据实际长度的两倍 + 2 个字节。 ISO 同义词**nvarchar**是**不同国家/地区 char**和**国家字符集不同**。
  
## <a name="remarks"></a>注释  
当 *n* 未指定数据定义或变量声明语句中的默认长度为 1。 当 *n* 未指定使用 CAST 函数的默认长度为 30。
  
使用**nchar**时的列数据条目的大小可能会成为类似。
  
使用**nvarchar**时的列数据条目的大小可能要大不相同。
  
**sysname**是系统提供用户定义数据类型的功能上等效于**nvarchar （128)**，只不过不可以为 null。 **sysname**用于引用数据库对象名称。
  
对象使用**nchar**或**nvarchar**分配数据库的默认排序规则，除非使用 COLLATE 子句分配特定的排序规则。
  
SET ANSI_PADDING 始终是在**nchar**和**nvarchar**。 SET ANSI_PADDING OFF 不适用于**nchar**或**nvarchar**数据类型。
  
前缀 Unicode 字符字符串常量，且必须以字母 n。不带 N 前缀，到数据库的默认代码页转换的字符串。 此默认代码页可能不识别某些字符。
 
> [!NOTE]  
>  当前缀字符串常量，且必须以字母 N，隐式转换将导致 Unicode 字符串中，如果要转换的常量不超过最大长度为 Unicode 字符串数据类型 (4000)。 否则，隐式转换会导致 Unicode 大值 （最大）。
  
> [!WARNING]  
>  每个非 null **varchar （max)**或**nvarchar (max)**该列需要的其他固定分配期间排序操作计入 8,060 字节行限制的 24 个字节。 这可能会导致隐式为非 null 数的限制**varchar （max)**或**nvarchar (max)**可以在表中创建的列。 在以下情况下不提供特殊错误：创建表格（最大行大小超过允许的最大 8060 字节时出现的一般警告除外）时，或插入数据时。 这一较大的行大小可能会导致在执行某些正常操作（例如聚集索引键更新或完整列集排序）期间出现错误（例如错误 512），使得用户在执行操作前无法预料到此类错误。  
  
## <a name="converting-character-data"></a>转换字符数据  
有关将字符数据转换的信息，请参阅[char 和 varchar &#40;Transact SQL &#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="examples"></a>示例  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[设置 ANSI_PADDING &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)
  
  

