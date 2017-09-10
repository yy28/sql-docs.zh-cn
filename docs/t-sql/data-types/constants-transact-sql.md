---
title: "常量 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/22/2017
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
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b212354492b96ca69ebf29afbc39c8ed1de6e3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="constants-transact-sql"></a>常量 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

常量，也称为文字值或标量值，是表示一个特定数据值的符号。 常量的格式取决于它所表示的值的数据类型。
  
## <a name="character-string-constants"></a>字符串常量
字符串常量括在单引号内并包含字母数字字符（a-z、A-Z 和 0-9）以及特殊字符，如感叹号 (!)、at 符 (@) 和数字号 (#)。 将为字符串常量分配当前数据库的默认排序规则，除非使用 COLLATE 子句为其指定了排序规则。 用户键入的字符串通过计算机的代码页计算，如有必要，将被转换为数据库的默认代码页。
  
如果已为某个连接将 QUOTED_IDENTIFIER 选项设置成 OFF，则字符串也可以使用双引号括起来，但 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口和 ODBC 驱动程序将自动使用 SET QUOTED_IDENTIFIER ON。 我们建议使用单引号。
  
如果单引号中的字符串包含一个嵌入的引号，可以使用两个单引号表示嵌入的单引号。 对于嵌入在双引号中的字符串则没有必要这样做。
  
以下是字符串的示例：
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
空字符串用中间没有任何字符的两个单引号表示。 在 6.x 兼容模式中，空字符串被看作是一个空格。
  
字符串常量支持增强的排序规则。
  
> [!NOTE]  
>  字符常量大于 8000 个字节被类型化为**varchar （max)**数据。  
  
## <a name="unicode-strings"></a>Unicode 字符串
Unicode 字符串的格式与普通字符串相似，但它前面有一个 N 标识符（N 代表 SQL-92 标准中的区域语言）。 N 前缀必须是大写字母。 例如，Michél 是字符常量，而 N Michél 是 Unicode 常量。 Unicode 常量被解释为 Unicode 数据，并且不使用代码页进行计算。 Unicode 常量有排序规则。 该排序规则主要用于控制比较和如何区分大小写。 为 Unicode 常量分配当前数据库的默认排序规则，除非使用 COLLATE 子句为其指定了排序规则。 对于字符数据，存储 Unicode 数据时每个字符使用 2 个字节，而不是每个字符 1 个字节。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
Unicode 字符串常量支持增强的排序规则。
  
> [!NOTE]  
>  Unicode 常量大于 8000 个字节被类型化为**nvarchar (max)**数据。  
  
## <a name="binary-constants"></a>二进制常量
二进制常量具有前辍 `0x` 并且是十六进制数字字符串。 这些常量不使用引号括起。
  
下面是二进制字符串的示例：
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  二进制常量大于 8000 个字节被类型化为**varbinary （max)**数据。  
  
## <a name="bit-constants"></a>位常量
**位**常量和由数字 0 或 1，表示未用引号引起来。 如果使用一个大于 1 的数字，则该数字将转换为 1。
  
## <a name="datetime-constants"></a>datetime 常量
**datetime**常量表示通过特定的格式，括在单引号中使用字符日期值。
  
下面是示例的**datetime**常量：
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Datetime 常量的示例包括：
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>integer 常量
**整数**常量由包含未用引号引起来，并且不包含小数点的数字的字符串表示。 **整数**常量必须是整数; 它们不能包含小数。
  
下面是示例的**整数**常量：
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>十进制常量
**十进制**常量表示的不会用引号引起来，包含小数点的数字的字符串。
  
下面是示例的**十进制**常量：
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>float 和 real 常量
**float**和**实际**常量由使用科学记数法表示。
  
下面是示例的**float**或**实际**值：
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>money 常量
**money**常量表示为带有可选小数点和可选的货币符号作为前缀的数字的字符串。 **money** constantsare 未用引号引起来。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不强制采用任何种类的分组规则，例如在代表货币的字符串中每隔三个数字插入一个逗号 (,)。
  
> [!NOTE]  
>  逗号将在指定的任何位置忽略**money**文本。  
  
下面是示例的**money**常量：
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>uniqueidentifier 常量
**uniqueidentifier**常量是一个字符串，表示一个 GUID。 可以使用字符或二进制字符串格式指定。
  
以下示例都指定相同的 GUID：
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>指定负数和正数  
若要指示一个数字是正值或负值，将应用 **+** 或 **-** 一个数值常量的一元运算符。 这将创建一个表示有符号数字值的表达式。 数值常量使用正 **+** 或 **-** 一元运算符不会应用。
  
签名**整数**表达式：  
  
```sql
+145345234
-2147483648
```
签名**十进制**表达式：  
  
```sql
+145345234.2234
-2147483648.10
```
  
签名**float**表达式：  
  
```sql
+123E-3
-12E5
```
  
签名**money**表达式：  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>增强的排序规则  
SQL Server 所支持的字符和 Unicode 字符串常量也支持增强的排序规则。 有关详细信息，请参阅[COLLATE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)子句。
  
## <a name="see-also"></a>另请参阅
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  

