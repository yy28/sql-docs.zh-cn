---
title: bcp_moretext | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_moretext
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f41069ec5254bec0ad40b250a3a9361190ba9b5
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2018
---
# <a name="bcpmoretext"></a>bcp_moretext
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将部分较长的可变长度数据类型值发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_moretext (  
        HDBC hdbc,  
        DBINT cbData,  
        LPCBYTE pData);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 *cbData*  
 正在从所引用的数据复制到 SQL Server 的数据的字节数*pData*。 SQL_NULL_DATA 的值指示为 NULL。  
  
 *pData*  
 指向要发送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的受支持的较长可变长度数据块区的指针。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 此函数可以结合使用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)要长，长度可变的数据将值复制到大量的较小区块中的 SQL Server。 **bcp_moretext**可以与具有以下 SQL Server 数据类型的列使用：**文本**， **ntext**，**映像**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**，用户定义类型 (UDT) 和 XML。 **bcp_moretext**不支持数据转换，提供的数据必须与目标列的数据类型匹配。  
  
 如果**bcp_bind**调用带非 NULL *pData*参数的数据类型的支持**bcp_moretext**， **bcp_sendrow**发送整个数据值，而不考虑长度。 如果是，但是， **bcp_bind**具有 NULL *pData*支持的数据类型的参数**bcp_moretext**可以用于将数据复制从成功返回后立即**bcp_sendrow** ，该值指示尚未处理与数据存在的任何绑定的列。  
  
 如果你使用**bcp_moretext**若要在一行中发送一个受支持的数据类型列，你必须还将其用于发送所有其他受支持的数据类型列的行中。 不可以跳过任何列。 支持的数据类型为 SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT 和 SQLXML。 如果列分别为 varchar(max)、nvarchar(max) 或 varbinary(max)，则 SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY 和 SQLVARBINARY 也属于此类别。  
  
 调用**bcp_bind**或[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)设置所有的数据部分复制到 SQL Server 列的总长度。 试图发送更多字节比对的调用中指定的 SQL Server **bcp_bind**或**bcp_collen**生成错误。 该错误会发生，例如，在应用程序使用该**bcp_collen**若要为 SQL Server 的设置的可用数据的长度**文本**列 4500，然后调用**bcp_moretext**五次时，该值指示在每次调用数据缓冲区长度为 1000 个字节长。  
  
 如果复制的行包含多个 long、 可变长度列， **bcp_moretext**第一个发送到低的顺序其数据按序号对它们编号列中，下一步后跟最低序号编号的列中，依次类推。 正确设置所需的数据的总长度很重要。 无法在长度设置之外发出已通过大容量复制接收某列的所有数据的信号。  
  
 当**var(max)**值发送到使用 bcp_sendrow 和 bcp_moretext 服务器，它不需要调用 bcp_collen 设置列的长度。 相反，对于这些类型仅，值是通过调用 bcp_sendrow 长度为零终止。  
  
 应用程序通常调用**bcp_sendrow**和**bcp_moretext**在循环中发送的数据行数。 下面是概述如何为一个包含两个表执行此操作的**文本**列：  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>示例  
 此示例演示如何使用**bcp_moretext**与**bcp_bind**和**bcp_sendrow**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
