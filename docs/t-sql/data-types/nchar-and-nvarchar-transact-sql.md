---
title: nchar 和 nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5056929fe2eeff4f8ee988690bd44988ffe329ff
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43071050"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 和 nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

字符数据类型（长度固定的 nchar 或长度可变的 nvarchar）和 Unicode 数据使用 UNICODE UCS-2 字符集。
  
## <a name="arguments"></a>参数  
**nchar** [ ( n ) ]  
固定长度的 Unicode 字符串数据。 n 用于定义字符串长度，并且它必须为 1 到 4,000 之间的值。 存储大小为 n 字节的两倍。 当排序规则代码页使用双字节字符时，存储大小仍然为 n 个字节。 根据字符串的不同，n 个字节的存储大小可能小于为 n 指定的值。 nchar 的 ISO 同义词是 national char 和 national character。
  
**nvarchar** [ ( n | **max** ) ]  
可变长度的 Unicode 字符串数据。 n 用于定义字符串长度，并且它可以为 1 到 4,000 之间的值。 max 指示最大存储大小是 2^30-1 个字符。  以字节为单位的最大存储大小为 2 GB。 实际存储大小（以字节为单位）是所输入字符个数的两倍 + 2 个字节。 nvarchar 的 ISO 同义词是 national char varying 和 national character varying。
  
## <a name="remarks"></a>Remarks  
如果没有在数据定义或变量声明语句中指定 n，则默认长度为 1。 如果没有使用 CAST 函数指定 n，则默认长度为 30。
  
如果列数据项的大小可能相同，请使用 nchar。
  
如果列数据项的大小可能差异很大，请使用 nvarchar。
  
sysname 是系统提供的用户定义数据类型，除了不可为 Null 外，在功能上与 nvarchar(128) 相同。 sysname 用于引用数据库对象名。
  
为使用 char 或 varchar 的对象分配的是默认的数据库排序规则，但可使用 COLLATE 子句分配特定的排序规则。
  
SET ANSI_PADDING 对于 nchar 和 nvarchar 始终为 ON。 SET ANSI_PADDING OFF 不适用于 nchar 或 nvarchar 数据类型。
  
在 Unicode 字符串常量前面添加字母 N 作为前缀。如果没有 N 前缀，字符串会被转换为数据库的默认代码页。 此默认代码页可能不识别某些字符。
 
> [!NOTE]  
>  在字符串常量前面添加字母 N 作为前缀时，如果要转换的常量不超过 Unicode 字符串数据类型的最大长度 (4,000)，则隐式转换将生成 Unicode 字符串。 否则，隐式转换将生成 Unicode 大值（最大值）。
  
> [!WARNING]  
>  每个非 null varchar(max) 或 nvarchar(max) 列都需要 24 个字节的附加固定分配，这将在执行排序操作期间根据 8,060 字节行限制进行计数。 这些附加的字节可在表中为非 null varchar(max) 或 nvarchar(max) 列数创建隐式限制。 在以下情况下不提供特殊错误：创建表格（最大行大小超过允许的最大 8060 字节时出现的一般警告除外）时，或插入数据时。 此较大行大小可能会导致用户在某些正常操作期间未意料到的错误（如错误 512）。  操作的两个示例是聚集索引密钥更新或完整列集排序。
  
## <a name="converting-character-data"></a>转换字符数据  
有关转换字符数据的信息，请参阅 [char 和 varchar (Transact-SQL)](../../t-sql/data-types/char-and-varchar-transact-sql.md)。
  
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
[COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE (Transact-SQL)](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
