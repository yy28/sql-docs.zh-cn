---
title: bcp_setbulkmode |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bcp_setbulkmode function
ms.assetid: de56f206-1f7e-4c03-bf22-da9c7f9f4433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9671447a2fba1cd57b021266f29de7af741f0de6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52520515"
---
# <a name="bcpsetbulkmode"></a>bcp_setbulkmode
  bcp_setbulkmode 允许您指定在大容量复制操作中，在单个函数调用中设置列的所有属性的列格式。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_setbulkmode (  
   HDBC   
hdbc  
,  
   INT   
property  
,  
   void *   
pField  
,  
   INT   
cbField  
,  
   void *   
pRow  
,  
   INT   
cbRow  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 支持大容量复制的 ODBC 连接句柄。  
  
 property  
 类型为 BYTE 的常量。 相关的常量列表，请参阅“备注”部分中的表。  
  
 *pField*  
 指向字段终止符值的指针。  
  
 *cbField*  
 字段终止符值的长度 （以字节为单位）。  
  
 *pRow*  
 指向行终止符值的指针。  
  
 *cbRow*  
 行终止符值的长度（以字节为单位）。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>备注  
 可以使用 bcp_setbulkmode 外的查询或表大容量复制。 当 bcp_setbulkmode 用于大容量复制查询语句时，它必须调用使用 BCP_HINT bcp_control 之前调用它。  
  
 bcp_setbulkmode 是使用的替代方法[bcp_setcolfmt](bcp-setcolfmt.md)并[bcp_columns](bcp-columns.md)，其仅可让你可以指定每个函数调用某一列的格式。  
  
 下表列出了 property 参数的常量。  
  
|属性|Description|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|指定字符输出模式。<br /><br /> 对应于 BCP 中的-c 选项。Exe 文件，以及与 bcp_setcolfmt`BCP_FMT_TYPE`属性设置为`SQLCHARACTER`。|  
|BCP_OUT_WIDE_CHARACTER_MODE|指定 Unicode 输出模式。<br /><br /> 对应于 BCP 中的-w 选项。EXE 和与 bcp_setcolfmt`BCP_FMT_TYPE`属性设置为`SQLNCHAR`。|  
|BCP_OUT_NATIVE_TEXT_MODE|指定对非字符类型使用本机类型，对字符类型使用 Unicode。<br /><br /> 对应于 BCP 中的-N 选项。EXE 和与 bcp_setcolfmt`BCP_FMT_TYPE`属性设置为`SQLNCHAR`如果列类型为字符串 （默认如果不是 string）。|  
|BCP_OUT_NATIVE_MODE|指定本机数据库类型。<br /><br /> 对应于 BCP 中的-n 选项。EXE 和与 bcp_setcolfmt`BCP_FMT_TYPE`属性设置为默认值。|  
  
 不应具有一系列函数调用，包括 bcp_setcolfmt、 bcp_control 和 bcp_readfmt 使用 bcp_setbulkmode。 例如，不应调用 bcp_control(BCPTEXTFILE) 和 bcp_setbulkmode。  
  
 您可以调用 bcp_control 和 bcp_setbulkmode bcp_control 不与 bcp_setbulkmode 冲突的选项。 例如，可以调用 bcp_control(BCPFIRST) 和 bcp_setbulkmode。  
  
 如果尝试调用 bcp_setbulkmode 用包括 bcp_setcolfmt、 bcp_control 和 bcp_readfmt 函数调用序列，其中一个函数调用将返回序列错误。 如果您选择更正错误，调用 bcp_init 重置所有设置并重新开始。  
  
 下表提供了会造成函数序列错误的函数调用的一些示例：  
  
 调用序列  
  
```  
bcp_init("table", DB_IN);  
bcp_setbulkmode();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_setbulkmode();  
bcp_readfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPHINTS, "select ...");  
bcp_setbulkmode();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_setbulkmode();  
bcp_setcolfmt();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_readfmt();  
bcp_setcolfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setbulkmode();  
bcp_control(BCPHINTS, "select ...");  
bcp_readfmt();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_columns();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setcolfmt();  
```  
  
## <a name="example"></a>示例  
 下面的示例使用 bcp_setbulkmode 的不同设置创建了四个文件。  
  
```  
// compile with: sqlncli11.lib odbc32.lib  
  
#include <windows.h>  
#include <stdio.h>  
#include <tchar.h>  
#include <sqlext.h>  
#include "sqlncli.h"  
  
// Global variables  
SQLHENV g_hEnv = NULL;  
SQLHDBC g_hDbc = NULL;  
  
void ODBCCleanUp() {  
   if (g_hDbc) {  
      SQLDisconnect(g_hDbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, g_hDbc);  
      g_hDbc = NULL;  
   }  
   if (g_hEnv) {  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      g_hEnv = NULL;  
   }  
}  
  
BOOL MakeODBCConnection(TCHAR * pszServer) {  
   TCHAR szConnectionString[500];  
   TCHAR szOutConnectionString[500];  
   SQLSMALLINT iLen;  
   SQLRETURN rc;  
  
   _sntprintf_s(szConnectionString, 500, TEXT("DRIVER={SQL Server Native Client 11.0};Server=%s;Trusted_connection=yes;"), pszServer);  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE,&g_hEnv);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_ENV...) failed\n");  
      return false;  
   }  
   rc = SQLSetEnvAttr(g_hEnv,SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, SQL_IS_UINTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetEnvAttr failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   rc = SQLAllocHandle( SQL_HANDLE_DBC, g_hEnv , &g_hDbc);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_DBC...) failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   // Enable BCP  
   rc = SQLSetConnectAttr(g_hDbc, SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON, SQL_IS_INTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetConnectAttr(.. SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON ...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // connecting ...  
   rc = SQLDriverConnect(g_hDbc,NULL, (SQLTCHAR*)szConnectionString, SQL_NTS, (SQLTCHAR*)szOutConnectionString, 500, &iLen, SQL_DRIVER_NOPROMPT);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLDriverConnect(SQL_HANDLE_DBC...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   return true;  
}  
  
BOOL BCPSetBulkMode(TCHAR * pszServer, TCHAR * pszQureryOut, char BCPType, TCHAR * pszDataFile) {  
   SQLRETURN rc;  
  
   if (!MakeODBCConnection(pszServer))  
      return false;  
   rc = bcp_init(g_hDbc, NULL, pszDataFile, NULL, DB_OUT);   // bcp init for queryout  
   if (SUCCEED != rc) {  
      printf("bcp_init failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if (BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if (BCPType == 'w') {   // bcp -w   
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               ODBCCleanUp();  
               return false;  
            }  
            rc = bcp_setbulkmode(g_hDbc, bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (SUCCEED != rc) {  
               printf("bcp_setbulkmode failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // set queryout TSQL statement  
            rc = bcp_control(g_hDbc, BCPHINTS , pszQureryOut);  
            if (SUCCEED != rc) {  
               printf("bcp_control(..BCP_OPTION_HINTS..) failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBINT nRowsInserted = 0;  
            rc = bcp_exec(g_hDbc, &nRowsInserted);  
            if (SUCCEED != rc) {  
               printf("bcp_exec failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            ODBCCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', TEXT("bcpc.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', TEXT("bcpw.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', TEXT("bcpn.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', TEXT("bcp_N.dat"));  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
