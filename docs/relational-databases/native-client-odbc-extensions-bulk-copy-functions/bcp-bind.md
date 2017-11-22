---
title: "bcp_bind |Microsoft 文档"
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
apiname: bcp_bind
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
caps.latest.revision: "47"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a3f6005104620c3a55d34c39b114517dab6750d1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bcpbind"></a>bcp_bind
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将程序变量中的数据绑定到表列，以便大容量复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_bind (  
        HDBC hdbc,   
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 *pData*  
 指向已复制数据的指针。 如果*eDataType*是 SQLTEXT、 SQLNTEXT、 SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE， *pData*可以为 NULL。 NULL *pData*指示长整型数据值将发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用的区块[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。 用户应仅设置*pData*为 NULL，如果用户绑定字段相对应的列是 BLOB 列否则**bcp_bind**将失败。  
  
 如果数据中存在指示符，这些指示符则在内存中直接显示在数据之前。 *PData*参数指向中这种情况下和指示器，宽度的指示器变量*cbIndicator*正确参数，使用通过对用户数据进行寻址的大容量复制。  
  
 *cbIndicator*  
 列数据的长度或 Null 指示符的长度（以字节为单位）。 有效指示器长度值是 0（不使用任何指示器时）、1、2、4 或 8。 指示符在内存中直接显示在任何数据之前。 例如，可以使用以下结构类型定义通过大容量复制将整数值插入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表：  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 在示例情况下， *pData*参数将设置为地址的结构，BCPBOUNDINT 的地址的声明实例*iIndicator*结构成员。 *CbIndicator*参数将设置为整数的大小 (sizeof(int))，和*cbData*参数再次将设置为整数 (sizeof(int)) 的大小。 大容量复制到包含 NULL 的服务器的行值绑定的列中，实例的值为*iIndicator*成员应设置为 SQL_NULL_DATA。  
  
 *cbData*  
 程序变量中数据的字节计数，不包括任何长度/Null 指示符或终止符的长度。  
  
 设置*cbData*到 SQL_NULL_DATA 表示复制到服务器的所有行都包含列的 NULL 值。  
  
 设置*cbData*给 SQL_VARLEN_DATA 指示系统将使用一个字符串终止符，或其他方法，以确定数据的长度复制。  
  
 对于固定长度的数据类型（如整数），该数据类型指示系统中的数据的长度。 因此，对于固定长度的数据类型， *cbData*可以安全地是 SQL_VARLEN_DATA 或数据的长度。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符和二进制数据类型， *cbData*可以是 SQL_VARLEN_DATA、 SQL_NULL_DATA、 某些正值或 0。 如果*cbData*是 SQL_VARLEN_DATA，系统使用的长度/null 指示器 （如果有） 或终止符序列以确定数据的长度。 如果同时提供指示符和终止符序列，系统则使用二者中可导致数据复制量最少的那一个。 如果*cbData*是 SQL_VARLEN_DATA，列的数据类型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符或二进制类型和一个长度指示符和终止符序列均未指定，系统将返回一条错误消息。  
  
 如果*cbData*为 0 或正值，系统使用*cbData*作为数据长度。 但是，如果是，除了一个正*cbData*长度指示器或终止符序列提供值，、 系统确定使用最少要复制的数据量会导致方法的数据长度。  
  
 *CbData*参数值表示的数据的字节数。 如果字符数据表示通过 Unicode 宽字符，则一个值为正*cbData*参数值表示乘以大小 （字节） 的每个字符的字符数。  
  
 *pTerm*  
 指向标记该程序变量末尾的字节模式（如果有）的指针。 例如，ANSI 和 MBCS C 字符串通常采用 1 个字节的终止符 (\0)。  
  
 如果没有为变量没有终结器，设置*pTerm*为 NULL。  
  
 您可以使用空字符串 ("") 将 C Null 终止符指定为程序变量终止符。 以 null 结尾的空字符串构成单字节 （终止符字节本身），因为设置*cbTerm*为 1。 例如，若要指示中的字符串*szName*是以 null 结尾，并且应使用终结器以指示长度：  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 此示例窗体 nonterminated 可能表明 15 个字符的复制从*szName*变量绑定的表的第二个列：  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 大容量复制 API 根据需要执行 Unicode 到 MBCS 的字符转换。 确保终止符字节字符串和字节字符串的长度均已正确设置。 例如，若要指示中的字符串*szName*为 Unicode 宽字符字符串，终止的 Unicode null 终止符值：  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 如果绑定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列是宽字符，在不执行任何转换[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列为 MBCS 字符类型，将数据发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时将执行从宽字符到多字节字符的转换。  
  
 *cbTerm*  
 存在于程序变量的终止符（如果有）中的字节计数。 如果没有为变量没有终结器，设置*cbTerm*为 0。  
  
 *eDataType*  
 程序变量的 C 数据类型。 程序变量中的数据转换为数据库列的类型。 如果该参数为 0，则不执行转换。  
  
 *EDataType*参数枚举通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据类型标记、 不 ODBC C 数据类型枚举器。 例如，您可以使用特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQLINT2 类型指定一个两个字节的整数：ODBC 类型的 SQL_C_SHORT。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]引入了对 SQLXML 和 SQLUDT 数据类型令牌中支持***eDataType***参数。  
  
 *idxServerCol*  
 数据复制的目标数据库表中的列的序号位置。 表中的第一列为列 1。 列的序号位置报告的[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 使用**bcp_bind**提供了一种快速、 高效的方法将数据从程序变量复制到表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 调用[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)之前调用此或任何其他大容量复制功能。 调用**bcp_init**设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于大容量复制的目标表。 在调用时**bcp_init**用于**bcp_bind**和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)、 **bcp_init** *szDataFile*表示数据文件中，参数设置为 NULL;**bcp_init***eDirection*参数设置为 DB_IN。  
  
 请单独**bcp_bind**调用为每个列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你想要将复制到其中的表。 后所需**bcp_bind**调用进行了，然后调用**bcp_sendrow**将数据的行发送到你程序变量从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不支持重新绑定列。  
  
 每当你想要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要提交已接收到的行，调用[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)。 例如，调用**bcp_batch**一次针对插入每 1000年行或在任何其他时间间隔。  
  
 当存在更多要插入的行时，调用[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)。 如果没有这样做，会导致错误。  
  
 控制与指定的参数设置[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)，不产生任何影响**bcp_bind**行传输。  
  
 如果*pData*为某一列设置为 NULL，因为其值将由调用提供[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)，与任何后续列*eDataType*设置为 SQLTEXT，SQLNTEXT，SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE 也必须绑定与*pData*设置为 NULL，且其值还必须提供通过调用**bcp_moretext**.  
  
 对于新的较大的值类型，如**varchar （max)**， **varbinary （max)**，或**nvarchar (max)**，你可以使用 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY，和中的类型指示器 SQLNCHAR *eDataType*参数。  
  
 如果*cbTerm*是不为 0，任何值 （1、 2、 4 或 8） 会有效前缀 (*cbIndicator*)。 在此情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端将搜索终结器时，计算方面终止符的数据长度 (*我*)，并设置*cbData*为 i 和的值的小的值前缀。  
  
 如果*cbTerm*为 0 和*cbIndicator* （前缀） 不是 0， *cbIndicator*必须是 8。 此 8 个字节的前缀可以采用以下值：  
  
-   0xFFFFFFFFFFFFFFFF 表示字段为 Null 值。  
  
-   0xFFFFFFFFFFFFFFFE 被视为特殊前缀值，用于有效地向服务器成块发送数据。 带有此特殊前缀的数据的格式为：  
  
-   < SPECIAL_PREFIX > \<0 个或多个数据区块 >< ZERO_CHUNK > 其中：  
  
-   SPECIAL_PREFIX 为 0xFFFFFFFFFFFFFFFE  
  
-   DATA_CHUNK 是包含块区长度的 4 个字节的前缀，后跟在该 4 个字节的前缀中指定其长度的实际数据。  
  
-   ZERO_CHUNK 是全部由零组成的 4 个字节的值 (00000000)，指示数据结束。  
  
-   任何其他有效的 8 个字节的长度均被视为常规数据长度。  
  
 调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)时使用**bcp_bind**会导致出现错误。  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>bcp_bind 对日期和时间增强功能的支持  
 有关与使用的类型信息*eDataType*参数对于日期/时间类型，请参阅[增强日期和时间类型 &#40;（OLE DB 和 ODBC）; 的大容量复制更改](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="example"></a>示例  
  
```  
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.   
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.   
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.   
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
