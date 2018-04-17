---
title: 从程序变量大容量复制 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5f00c8542691fcbdd66e5a35151161b3a901f439
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="bulk-copying-from-program-variables"></a>从程序变量执行大容量复制
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  可以直接从程序变量执行大容量复制。 在将分配变量以保存数据时的行和调用之后[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)若要启动大容量复制，调用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)为每个列，以指定位置和相关联的程序变量格式与列。 填充每个变量的数据，然后调用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)以向服务器发送一行数据。 重复该过程的填充变量和调用**bcp_sendrow**之前已向服务器发送的所有行，然后调用[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)来指定该操作已完成。  
  
 **Bcp_bind * * * pData*参数包含绑定到列变量的地址。 每列的数据都可以通过以下两种方式之一存储：  
  
-   分配一个变量以保存数据。  
  
-   分配指示器变量，后面紧随数据变量。  
  
 指示器变量指示可变长度列的数据长度，如果列允许 NULL 值，还指示 NULL 值。 如果只使用数据变量，则此变量的地址将存储在 **bcp_bind * * * pData*参数。 如果使用指示器变量，则指示器变量的地址存储在 **bcp_bind * * * pData*参数。 大容量复制函数计算的数据变量的位置通过添加 **bcp_bind * * * cbIndicator*和*pData*参数。  
  
 **bcp_bind**支持三种方法来处理可变长度数据：  
  
-   使用*cbData*使用只有一个数据变量。 将中的数据的长度*cbData*。 要将大容量的数据的长度复制更改，每次调用[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)重置*cbData*。 如果正在使用其他两种方法之一，指定为 SQL_VARLEN_DATA *cbData*。 如果正在为一个列提供的所有数据值都均为 NULL，指定为 SQL_NULL_DATA *cbData*。  
  
-   使用指示器变量。 随着每个新数据值移入数据变量，将该值的长度存储在指示器变量中。 如果正在使用其他两种方法之一，指定为 0 *cbIndicator*。  
  
-   使用终止符指针。 负载 **bcp_bind * * * pTerm*终止数据的位模式的地址的参数。 如果正在使用其他两种方法之一，则指定 NULL 为*pTerm*。  
  
 所有这三种方法可以使用同一个**bcp_bind**调用，在这种情况下使用导致数据被复制的最少量的规范。  
  
 **Bcp_bind * * * 类型*参数使用 Db-library 数据类型标识符，不 ODBC 数据类型标识符。 Db-library 数据类型标识符定义中适用于 ODBC **bcp_bind**函数。  
  
 大容量复制函数并不支持所有 ODBC C 数据类型。 例如，大容量复制函数不支持 ODBC SQL_C_TYPE_TIMESTAMP 结构，因此请使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)或[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)将 ODBC SQL_TYPE_TIMESTAMP 数据转换为 SQL_C_CHAR 变量。 如果随后使用**bcp_bind**与*类型*SQLCHARACTER 要绑定到变量参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**列中，大容量复制函数将转换在为正确的日期时间格式字符变量中的时间戳 escape 子句。  
  
 下表列出了要从 ODBC SQL 数据类型到映射中使用的建议的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
|ODBC SQL 数据类型|ODBC C 数据类型|bcp_bind*类型*参数|SQL Server 数据类型|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **不同的字符**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT（有符号）|SQL_C_SSHORT|SQLINT2|**int**|  
|SQL_TINYINT（无符号）|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT（有符号）|SQL_C_SSHORT|SQLINT2|**int**|  
|SQL_SMALL_INT（无符号）|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER（有符号）|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER（无符号）|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**|  
|SQL_BIGINT（有符号和无符号）|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **不同的二进制**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未签名**tinyint**无符号**smallint**，或无符号**int**数据类型。 若要防止丢失数据值，在迁移这些数据类型时，创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与下一步的最大整数数据类型的表。 若要防止用户以后添加原始数据类型所允许范围之外的值，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列应用一条规则，将允许的值限定在原始源中的数据类型所支持的范围之内：  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不直接支持 interval 数据类型。 应用程序可以但是，将 interval 转义序列存储为中的字符字符串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符列。 该应用程序可以读取它们供以后使用，但是它们无法用在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。  
  
 大容量复制函数可以用于数据快速加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已从 ODBC 数据源读取。 使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)若要绑定到程序变量设置结果的列，然后使用**bcp_bind**将相同的程序变量绑定到大容量复制操作。 调用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)或**SQLFetch**到程序变量和调用从 ODBC 数据源提取数据行[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)大容量复制数据从程序变量到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 应用程序可以使用[bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)函数需要将中最初指定的数据变量的地址更改的任何时候**bcp_bind** *pData*参数。 应用程序可以使用[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)函数每当它需要更改中最初指定的数据长度 **bcp_bind * * * cbData*参数。  
  
 无法读取数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到程序变量使用大容量复制; 没有一点也不像"bcp_readrow"函数。 只能将数据从应用程序发送到服务器。  
  
## <a name="see-also"></a>另请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
