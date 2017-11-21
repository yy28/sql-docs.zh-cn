---
title: "集 ANSI_PADDING (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 426cbfe673bafe6e1770745ca16ba23fd068fb67
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  对列存储长度小于列的定义大小的值以及在 **char**、 **varchar**、 **binary**和 **varbinary** 数据中含有尾随空格的值的方式进行控制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_PADDING { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_PADDING ON;  
```  
  
## <a name="remarks"></a>注释  
 使用定义的列**char**， **varchar**，**二进制**，和**varbinary**数据类型的定义的大小。  
  
 此设置只影响新列的定义。 创建列后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会基于创建列时的设置存储这些值。 以后对此设置的更改不会影响现有的列。  
  
> [!NOTE]  
>  建议始终将 ANSI_PADDING 设置为 ON。  
  
 下表显示 SET ANSI_PADDING 设置的效果，值插入到具有的列时**char**， **varchar**，**二进制**，和**varbinary**数据类型。  
  
|设置|char (*n*) 不为 NULL 或 binary (*n*) 不为 NULL|char (*n*) 为 NULL 或 binary (*n*) 为 NULL|varchar (*n*) 或 varbinary (*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|填充原始值 (以尾随空格的**char**列和具有尾部零来取代**二进制**列) 到列的长度。|遵循相同的规则同样适用于**char (***n***)**或**二进制 (**  *n* **)**当 SET ANSI_PADDING 为 ON 时不为 NULL。|尾随空格中的字符值插入到**varchar**列不会被修剪。 尾随零中的二进制值插入到**varbinary**列不会被修剪。 不将值填充到列的长度。|  
|OFF|填充原始值 (以尾随空格的**char**列和具有尾部零来取代**二进制**列) 到列的长度。|遵循相同的规则同样适用于**varchar**或**varbinary**时 SET ANSI_PADDING 为 OFF。|尾随空格中的字符值插入到**varchar**列进行修剪。 尾随零中的二进制值插入到**varbinary**列进行修剪。|  
  
> [!NOTE]  
>  当填充， **char**以空白，进行填充列和**二进制**用零填充列。 当删除， **char**列具有删除，尾随空格和**二进制**列具有修剪尾随零。  
  
 在创建或更改计算列的索引或索引视图时，SET ANSI_PADDING 必须为 ON。 对计算列所需的 SET 选项设置的索引的视图和索引的详细信息，请参阅"当你使用 SET 语句的注意事项"中[SET 语句 &#40;Transact SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 SET ANSI_PADDING 的默认值为 ON。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接时自动将 ANSI_PADDING 设置为 ON。 在连接之前，您可以在应用程序的 ODBC 数据源、ODBC 连接特性或 OLE DB 连接属性集合中配置此设置。 对于来自 DB-Library 应用程序的连接，SET ANSI_PADDING 的默认设置为 OFF。  
  
 SET ANSI_PADDING 设置不影响**nchar**， **nvarchar**， **ntext**，**文本**，**映像**， **varbinary （max)**， **varchar （max)**，和**nvarchar (max)**数据类型。 它们始终显示 SET ANSI_PADDING ON 行为。 这表示不剪裁尾随空格和尾随零。  
  
 如果 SET ANSI_DEFAULTS 为 ON，则启用 SET ANSI_PADDING。  
  
 SET ANSI_PADDING 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例演示了该设置对上述每个数据类型的影响。  
  
```  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
  
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

