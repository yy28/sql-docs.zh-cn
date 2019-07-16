---
title: 从程序变量大容量复制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5473d741f5144338c99627e1057c51ce116093d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206839"
---
# <a name="bulk-copying-from-program-variables"></a>从程序变量执行大容量复制
  可以直接从程序变量执行大容量复制。 分配变量以保存行和调用的数据后[bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)若要开始大容量复制，调用[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)为每个列指定的位置和相关联的程序变量的格式与列。 填充每个变量的数据，然后调用[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)以向服务器发送一行数据。 重复填充变量和调用的过程**bcp_sendrow**直到向服务器发送所有行，然后调用[bcp_done](../native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)指定操作已完成。  
  
 **Bcp_bind**_pData_参数包含绑定到列的变量的地址。 每列的数据都可以通过以下两种方式之一存储：  
  
-   分配一个变量以保存数据。  
  
-   分配指示器变量，后面紧随数据变量。  
  
 指示器变量指示可变长度列的数据长度，如果列允许 NULL 值，还指示 NULL 值。 如果只使用数据变量，此变量的地址将存储在**bcp_bind**_pData_参数。 如果使用指示器变量，指示器变量的地址存储在**bcp_bind**_pData_参数。 大容量复制函数来计算数据变量的位置添加**bcp_bind**_cbIndicator_并*pData*参数。  
  
 **bcp_bind**支持三种方法来处理可变长度数据：  
  
-   使用*cbData*使用只有一个数据变量。 将放置在数据的长度*cbData*。 长度的数据要进行大容量复制更改，每次调用[bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)重置*cbData*。 如果正在使用其他两种方法之一，指定为 SQL_VARLEN_DATA *cbData*。 如果为列提供的所有数据值都均为 NULL，指定为 SQL_NULL_DATA *cbData*。  
  
-   使用指示器变量。 随着每个新数据值移入数据变量，将该值的长度存储在指示器变量中。 如果正在使用其他两种方法之一，指定为 0 *cbIndicator*。  
  
-   使用终止符指针。 负载**bcp_bind**_pTerm_终止数据的位模式的地址的参数。 如果正在使用其他两种方法之一，指定为空， *pTerm*。  
  
 所有这三种方法可以使用同一**bcp_bind**调用，在这种情况下使用导致数据复制量最小的规范。  
  
 **Bcp_bind**_类型_参数使用 Db-library 数据类型标识符，而不 ODBC 数据类型标识符。 用于 ODBC 的 sqlncli.h 中定义的 Db-library 数据类型标识符**bcp_bind**函数。  
  
 大容量复制函数并不支持所有 ODBC C 数据类型。 例如，大容量复制函数不支持 ODBC SQL_C_TYPE_TIMESTAMP 结构，因此请使用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)或[SQLGetData](../native-client-odbc-api/sqlgetdata.md)将 ODBC SQL_TYPE_TIMESTAMP 数据转换为 SQL_C_CHAR 变量。 如果随后使用**bcp_bind**与*类型*参数 SQLCHARACTER 要绑定到变量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**列中，大容量复制函数将转换为正确的 datetime 格式字符变量中的时间戳转义子句。  
  
 下表列出了从 ODBC SQL 数据类型映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型时推荐使用的数据类型。  
  
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
|SQL_TINYINT（有符号）|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT（无符号）|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT（有符号）|SQL_C_SSHORT|SQLINT2|**smallint**|  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未签名**tinyint**无符号**smallint**，或无符号**int**数据类型。 若要在迁移这些数据类型时防止丢失数据值，应使用第二大整数数据类型创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 若要防止用户以后添加原始数据类型所允许范围之外的值，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列应用一条规则，将允许的值限定在原始源中的数据类型所支持的范围之内：  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不直接支持 interval 数据类型。 不过，应用程序可以将 interval 转义序列作为字符串存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字符列中。 该应用程序可以读取它们供以后使用，但是它们无法用在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。  
  
 可以使用大容量复制函数将从 ODBC 数据源中读取的数据快速加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 使用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)若要绑定的列的结果集到程序变量，然后使用**bcp_bind**将相同的程序变量绑定到大容量复制操作。 调用[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)或**SQLFetch**到程序变量，并调用从 ODBC 数据源提取数据行[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)大容量复制数据从程序变量到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 应用程序可以使用[bcp_colptr](../native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)函数需要更改中最初指定的数据变量的地址随时**bcp_bind** _pData_参数。 应用程序可以使用[bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)函数需要更改中最初指定的数据长度随时**bcp_bind**_cbData_参数。  
  
 无法使用大容量复制功能将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取到程序变量中；没有与 "bcp_readrow" 函数类似的功能。 只能将数据从应用程序发送到服务器。  
  
## <a name="see-also"></a>请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
