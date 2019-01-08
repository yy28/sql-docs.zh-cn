---
title: bcp_bind |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_bind
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 027800860166b511b0a548313de30b3d237d9930
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513805"
---
# <a name="bcpbind"></a>bcp_bind
  将程序变量中的数据绑定到表列，以便大容量复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_bind (  
HDBC   
hdbc  
,   
LPCBYTE   
pData  
,  
INT   
cbIndicator  
,  
DBINT   
cbData  
,  
LPCBYTE   
pTerm  
,  
INT   
cbTerm  
,  
INT   
eDataType  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是大容量复制启用 ODBC 连接句柄。  
  
 *pData*  
 指向已复制数据的指针。 如果*eDataType*为 SQLTEXT、 SQLNTEXT、 SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE， *pData*可以为 NULL。 为空*pData*指示长数据值将发送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用的区块[bcp_moretext](bcp-moretext.md)。 用户只应设置*pData*为 NULL，如果与用户绑定字段对应的列是 BLOB 列，否则**bcp_bind**将失败。  
  
 如果数据中存在指示符，这些指示符则在内存中直接显示在数据之前。 *PData*参数指向指示符变量，在这种情况下和指示符，宽度*cbIndicator*参数，将正确使用对用户数据进行寻址的大容量复制。  
  
 *cbIndicator*  
 列数据的长度或 Null 指示符的长度（以字节为单位）。 有效指示器长度值是 0（不使用任何指示器时）、1、2、4 或 8。 指示符在内存中直接显示在任何数据之前。 例如，可以使用以下结构类型定义通过大容量复制将整数值插入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表：  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 在示例案例中， *pData*参数将设置到的地址的结构，即 bcpboundint 地址的声明实例*iIndicator*结构成员。 *CbIndicator*参数将设置为整数的大小 (sizeof(int))，并*cbData*也将参数设置为一个整数 (sizeof(int)) 大小。 大容量复制到包含 null 值的服务器的行值将绑定列，该实例的值*iIndicator*成员应设置为 SQL_NULL_DATA。  
  
 *cbData*  
 程序变量中数据的字节计数，不包括任何长度/Null 指示符或终止符的长度。  
  
 设置*cbData*为 SQL_NULL_DATA 表示复制到服务器的所有行都包含 NULL 值的列。  
  
 设置*cbData*为 SQL_VARLEN_DATA 指示系统将使用字符串终止符或其他方法，以确定数据长度复制。  
  
 对于固定长度的数据类型（如整数），该数据类型指示系统中的数据的长度。 因此，对于固定长度的数据类型， *cbData*可以安全地采用 SQL_VARLEN_DATA 或数据的长度。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符和二进制数据类型*cbData*可以是 SQL_VARLEN_DATA、 SQL_NULL_DATA、 某些正值或 0。 如果*cbData*为 SQL_VARLEN_DATA，则系统使用长度 /null 指示符 （如果存在） 或终止符序列来确定数据的长度。 如果同时提供指示符和终止符序列，系统则使用二者中可导致数据复制量最少的那一个。 如果*cbData*为 SQL_VARLEN_DATA，列的数据类型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定字符或二进制类型，并且既不名技术长度指示器和终止符序列，则系统将返回一条错误消息。  
  
 如果*cbData*为 0 或正值，则系统使用*cbData*作为数据长度。 但是，如果除了正*cbData*值，提供长度指示器或终止符序列，系统使用导致数据复制量最少的方法来确定数据长度。  
  
 *CbData*参数值表示数据的字节计数。 如果字符数据由 Unicode 宽字符，则正*cbData*参数值表示的以字节为单位的每个字符的大小的乘积的字符数。  
  
 *pTerm*  
 指向标记该程序变量末尾的字节模式（如果有）的指针。 例如，ANSI 和 MBCS C 字符串通常采用 1 个字节的终止符 (\0)。  
  
 如果变量没有终止符，则设置*pTerm*为 NULL。  
  
 您可以使用空字符串 ("") 将 C Null 终止符指定为程序变量终止符。 由于以 null 结尾的空字符串构成一个字节 （终止符字节自身），设置*cbTerm*为 1。 例如，若要指示中的字符串*szName*是以 null 结尾以及应使用该终止符指示长度：  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 此示例中的非终止的形式可能表示从复制 15 个字符*szName*变量绑定的表的第二列：  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 大容量复制 API 根据需要执行 Unicode 到 MBCS 的字符转换。 确保终止符字节字符串和字节字符串的长度均已正确设置。 例如，若要指示中的字符串*szName*是由 Unicode null 终止符值终止一个 Unicode 宽字符字符串：  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 如果绑定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列是宽字符，将不执行任何转换[bcp_sendrow](bcp-sendrow.md)。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列为 MBCS 字符类型，将数据发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时将执行从宽字符到多字节字符的转换。  
  
 *cbTerm*  
 存在于程序变量的终止符（如果有）中的字节计数。 如果变量没有终止符，则设置*cbTerm*为 0。  
  
 *eDataType*  
 程序变量的 C 数据类型。 程序变量中的数据转换为数据库列的类型。 如果该参数为 0，则不执行转换。  
  
 *EDataType*参数枚举[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlncli.h 中的数据类型标记、 不 ODBC C 数据类型枚举器。 例如，您可以使用特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQLINT2 类型指定一个两个字节的整数：ODBC 类型的 SQL_C_SHORT。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引入了对 SQLXML 和 SQLUDT 数据类型标记中支持*`eDataType`* 参数。  
  
 *idxServerCol*  
 数据复制的目标数据库表中的列的序号位置。 表中的第一列为列 1。 报告列的序号位置[SQLColumns](../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 使用**bcp_bind**若要将数据从程序变量复制到的表中的快速、 高效的方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 调用[bcp_init](bcp-init.md)之前调用此方法或任何其他大容量复制函数。 调用**bcp_init**设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]大容量复制的目标表。 调用时**bcp_init**用于**bcp_bind**并[bcp_sendrow](bcp-sendrow.md)，则**bcp_init** *szDataFile*参数，指示数据文件中，设置为 NULL;**bcp_init**_eDirection_参数设置为 DB_IN。  
  
 单独**bcp_bind**为每个列调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你想要复制到其中的表。 所需的后**bcp_bind**的调用进行了，然后调用**bcp_sendrow**将数据的行发送到将程序变量中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不支持重新绑定列。  
  
 每当你想要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要提交收到的行，请调用[bcp_batch](bcp-batch.md)。 例如，调用**bcp_batch**一次每插入 1000年行或在任何其他时间间隔。  
  
 如果没有更多的行插入，调用[bcp_done](bcp-done.md)。 如果没有这样做，会导致错误。  
  
 控制参数设置，使用指定[bcp_control](bcp-control.md)，不起任何作用**bcp_bind**行传输。  
  
 如果*pData*的列设置为 NULL，因为其值将通过调用提供[bcp_moretext](bcp-moretext.md)，与任何后续列*eDataType*设置为 SQLTEXT、 SQLNTEXT，SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE 也必须绑定与*pData*设置为 NULL，且它们的值还必须提供通过调用`bcp_moretext`。  
  
 对于新的大值类型，如`varchar(max)`， `varbinary(max)`，或`nvarchar(max)`，可以使用 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY 和 SQLNCHAR 作为类型指示符*eDataType*参数。  
  
 如果*cbTerm*是不为 0，（1、 2、 4 或 8） 的任何值是有效的前缀 (*cbIndicator*)。 在此情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将搜索终止符，计算终止符的数据长度 (*我*)，并设置*cbData*为 i 和的值的小的值前缀。  
  
 如果*cbTerm*为 0 并*cbIndicator* （前缀） 不是 0， *cbIndicator*必须为 8。 此 8 个字节的前缀可以采用以下值：  
  
-   0xFFFFFFFFFFFFFFFF 表示字段为 Null 值。  
  
-   0xFFFFFFFFFFFFFFFE 被视为特殊前缀值，用于有效地向服务器成块发送数据。 带有此特殊前缀的数据的格式为：  
  
-   < SPECIAL_PREFIX > \<0 个或多个数据区块 >< ZERO_CHUNK > 位置：  
  
-   SPECIAL_PREFIX 为 0xFFFFFFFFFFFFFFFE  
  
-   DATA_CHUNK 是包含块区长度的 4 个字节的前缀，后跟在该 4 个字节的前缀中指定其长度的实际数据。  
  
-   ZERO_CHUNK 是全部由零组成的 4 个字节的值 (00000000)，指示数据结束。  
  
-   任何其他有效的 8 个字节的长度均被视为常规数据长度。  
  
 调用[bcp_columns](bcp-columns.md)使用时**bcp_bind**会导致出现错误。  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>bcp_bind 对日期和时间增强功能的支持  
 有关与一起使用的类型信息*eDataType*参数用于日期/时间类型，请参阅[的增强的日期和时间类型的大容量复制更改&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
