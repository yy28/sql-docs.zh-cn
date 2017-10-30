---
title: "子字符串 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
caps.latest.revision: 65
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f36ec82c65e5d52c2186c67033adddbf1700c4d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的字符、二进制、文本或图像表达式的一部分。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是**字符**，**二进制**，**文本**， **ntext**，或**映像**[表达式](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *启动*  
 是一个整数或**bigint**指定返回的字符的起始位置的表达式。 （编号是 1 基于，表示在表达式中的第一个字符为 1）。 如果*启动*小于 1，则返回的表达式将在中指定的第一个字符开始*表达式*。 在这种情况下，返回的字符数是的总和的最大值*启动* + *长度*-1 或 0。 如果*启动*大于数中的字符的值表达式，返回一个零长度表达式。  
  
 *length*  
 是一个正整数或**bigint**表达式，它指定的多少个字符*表达式*将返回。 如果*长度*为负，则会生成错误并终止该语句。 如果的总和*启动*和*长度*大于中的字符数*表达式*，开始整个值表达式*启动*返回。  
  
## <a name="return-types"></a>返回类型  
 返回字符数据，如果*表达式*是一种受支持的字符数据类型。 如果返回二进制数据*表达式*是支持之一**二进制**数据类型。 返回的字符串类型与指定表达式的类型相同（表中显示的除外）。  
  
|指定的表达式|返回类型|  
|--------------------------|-----------------|  
|**char**/**varchar**/**文本**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**二进制**/**varbinary**/**映像**|**varbinary**|  
  
## <a name="remarks"></a>注释  
 值*启动*和*长度*中的字符数必须指定**ntext**， **char**，或**varchar**数据类型和字节**文本**，**映像**，**二进制**，或**varbinary**数据类型。  
  
 *表达式*必须**varchar （max)**或**varbinary （max)**时*启动*或*长度*包含的值大于 2147483647。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 当使用增补字符 (SC) 排序规则，同时*启动*和*长度*计数的每个代理项对*表达式*单个字符的形式。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-substring-with-a-character-string"></a>A. 对字符串使用 SUBSTRING  
 以下示例说明如何仅返回字符串的一部分。 从`sys.databases`表，此查询返回系统数据库中名称的第一列，在第二个列中，数据库和中的最后一列的第三个和第四个字符的第一个字母。  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |初始 |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |st |
|tempdb  |t  |mp |
|model   |m  |de |
|msdb    |m  |db |


  
 以下示例说明如何显示字符串常量 `abcdef` 中的第二个、第三个和第四个字符。  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. 对 text、ntext 和 image 数据使用 SUBSTRING  
  
> [!NOTE]  
>  若要运行下面的示例，必须安装**pubs**数据库。  
  
 下面的示例演示如何从每个返回前 10 个字符**文本**和**映像**中的数据列`pub_info`表`pubs`数据库。 **文本**数据返回为**varchar**，和**映像**数据返回为**varbinary**。  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 下面的示例演示上的子字符串的效果**文本**和**ntext**数据。 首先，该示例在 `pubs` 数据库内创建一个名为 `npub_info` 的新表。 接着，该示例使用 `pr_info` 列的前 80 个字符在 `npub_info` 表中创建 `pub_info.pr_info` 列，然后将添加 `ü` 为第一个字符。 最后，`INNER JOIN`检索所有发布服务器标识号和`SUBSTRING`这两者的**文本**和**ntext**发布服务器信息列。  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>C. 对字符串使用 SUBSTRING  
 以下示例说明如何仅返回字符串的一部分。 该查询在一列中返回 `dbo.DimEmployee` 表中的姓氏，在另一列中只返回名字首字母。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 下面的示例演示如何返回第二、 三和第四个字符的字符串常量`abcdef`。  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



