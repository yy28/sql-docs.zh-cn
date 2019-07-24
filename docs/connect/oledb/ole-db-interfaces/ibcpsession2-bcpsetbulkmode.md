---
title: IBCPSession2::BCPSetBulkMode | Microsoft Docs
description: '使用 IBCPSession2:: BCPSetBulkMode 从查询或表中创建大容量复制'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BCPSetBulkMode function
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d07cb3c62e0779a517a3441bef7bc01fbdbce037
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015479"
---
# <a name="ibcpsession2bcpsetbulkmode"></a>IBCPSession2::BCPSetBulkMode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  IBCPSession2:: BCPSetBulkMode 提供了用于指定列格式的[IBCPSession &#40;:&#41; : BCPColFmt OLE DB](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)的替代方法。 不同于 IBCPSession:: BCPColFmt, 它设置单个列格式属性, IBCPSession2:: BCPSetBulkMode 设置所有属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
HRESULT BCPSetBulkMode (  
      int property,  
   void * pField,  
   int cbField,  
   void * pRow,  
   int cbRow  
);  
```  
  
## <a name="arguments"></a>参数  
 property   
 类型为 BYTE 的常量。 相关的常量列表，请参阅“备注”部分中的表。  
  
 pField   
 指向字段终止符值的指针。  
  
 cbField  
 字段终止符值的长度（以字节为单位）。  
  
 pRow  
 指向行终止符值的指针。  
  
 cbRow  
 行终止符值的长度（以字节为单位）。  
  
## <a name="returns"></a>返回  
 IBCPSession2:: BCPSetBulkMode 可以返回以下内容之一:  
  
|||  
|-|-|  
|**S_OK**|方法成功。|  
|**E_FAIL**|出现访问接口特定的错误；要获取详细信息，请使用 ISQLServerErrorInfo 接口。|  
|**E_UNEXPECTED**|意外调用了该方法。 例如, 在调用 IBCPSession2:: BCPSetBulkMode 之前, 未调用**IBCPSession2:: BCPInit**方法。|  
|**E_INVALIDARG**|参数无效。|  
|**E_OUTOFMEMORY**|内存不足错误。|  
  
## <a name="remarks"></a>Remarks  
 IBCPSession2:: BCPSetBulkMode 可用于从查询或表中大容量复制。 使用 IBCPSession2::BCPSetBulkMode 向外大容量复制查询语句时，必须先调用该方法，再调用 `IBCPSession::BCPControl(BCP_OPTIONS_HINTS, ...)` 来指定查询语句。  
  
 应该避免在单个命令文本内将 RPC 调用语法与批查询语法结合使用（例如 `{rpc func};SELECT * from Tbl`）。  这将导致 ICommandPrepare::P 准备返回错误, 并阻止你检索元数据。 如果需要在单个命令文本内结合执行存储过程和批查询，请使用 ODBC CALL 语法（例如 `{call func}; SELECT * from Tbl`）。  
  
 下表列出了 property 参数的常量  。  
  
|属性|描述|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|指定字符输出模式。<br /><br /> 对应于 BCP 中的-c 选项。EXE, 将*eUserDataType*属性设置为**BCP_TYPE_SQLCHARACTER**, 并将其设置为 IBCPSession:: BCPColFmt。|  
|BCP_OUT_WIDE_CHARACTER_MODE|指定 Unicode 输出模式。<br /><br /> 对应于 BCP 中的-w 选项。EXE 和 IBCPSession:: BCPColFmt, *eUserDataType*属性设置为**BCP_TYPE_SQLNCHAR**。|  
|BCP_OUT_NATIVE_TEXT_MODE|指定对非字符类型使用本机类型，对字符类型使用 Unicode。<br /><br /> 对应于 BCP 中的-N 选项。如果列类型是字符串, 则为*eUserDataType*属性设置为**BCP_TYPE_SQLNCHAR**的 EXE 和 IBCPSession:: BCPColFmt, 如果不是字符串, 则为**BCP_TYPE_DEFAULT** 。|  
|BCP_OUT_NATIVE_MODE|指定本机数据库类型。<br /><br /> 对应于 BCP 中的-n 选项。EXE 和 IBCPSession:: BCPColFmt, *eUserDataType*属性设置为**BCP_TYPE_DEFAULT**。|  
  
 对于 IBCPSession:: BCPControl 选项, 可以调用 IBCPSession:: BCPControl 和 IBCPSession2:: BCPSetBulkMode, 这些选项不会与 IBCPSession2:: BCPSetBulkMode 冲突。 例如, 可以调用 IBCPSession:: BCPControl 和**BCP_OPTION_FIRST**和 IBCPSession2:: BCPSetBulkMode。  
  
 不能将 IBCPSession:: BCPControl 与**BCP_OPTION_TEXTFILE**和 IBCPSession2:: BCPSetBulkMode 一起调用。  
  
 如果尝试使用包含 IBCPSession:: BCPColFmt、IBCPSession:: BCPControl 和 IBCPSession:: BCPReadFmt 的函数调用序列来调用 IBCPSession2:: BCPSetBulkMode, 则其中一个函数调用将返回序列错误失败。 如果选择更正错误，请调用 IBCPSession::BCPInit 重置设置，然后重新开始。  
  
 下面是导致函数序列错误的函数调用的一些示例:  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_IN);  
BCPSetBulkMode();  
```  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPReadFmt();  
```  
  
```cpp  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_HINTS, "select ...");  
BCPSetBulkMode();  
```  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPColFmt();  
```  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPReadFmt();  
BCPColFmt();  
```  
  
```cpp  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetBulkMode();  
BCPControl(BCP_OPTION_HINTS, "select ...");  
BCPReadFmt();  
```  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPColumns();  
```  
  
```cpp  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetColFmt();  
```  
  
## <a name="example"></a>示例  
 下面的示例使用 IBCPSession2::BCPSetBulkMode 的不同设置创建了四个文件。  
  
```cpp  
  
// compile with: oleaut32.lib ole32.lib  
  
#include <stdio.h>  
#include "msoledbsql.h"  
  
IDBInitialize*  g_pIDBInitialize = NULL;  
IBCPSession2 * g_pIBcpSession = NULL;  
class COLEDBPropSet : public DBPROPSET {  
public:  
   COLEDBPropSet() {  
      rgProperties = NULL;  
      cProperties = 0;  
   };  
   COLEDBPropSet(const GUID& guid) {  
      rgProperties = NULL;  
      cProperties = 0;  
      guidPropertySet = guid;  
   };  
   ~COLEDBPropSet() {  
      for ( ULONG i = 0 ; i < cProperties ; i++ )  
         VariantClear(&rgProperties[i].vValue);  
      CoTaskMemFree(rgProperties);  
   }  
   void SetGUID(const GUID& guid) {  
      guidPropertySet = guid;  
   };  
   bool AddProperty(DWORD dwPropertyID, bool bValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BOOL;  
      rgProperties[cProperties].vValue.boolVal = (bValue) ? VARIANT_TRUE : VARIANT_FALSE;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID, long nValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID  = dwPropertyID;  
      rgProperties[cProperties].vValue.vt     = VT_I4;  
      rgProperties[cProperties].vValue.lVal   = nValue;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID,LPCWSTR szValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BSTR;  
      rgProperties[cProperties].vValue.bstrVal = SysAllocString(szValue);  
      cProperties++;  
      return true;  
   };  
   bool Add() {  
      DBPROP* p = (DBPROP*)CoTaskMemRealloc(rgProperties, (cProperties + 1) * sizeof(DBPROP));  
      if (p != NULL) {  
         rgProperties = p;  
         rgProperties[cProperties].dwOptions = DBPROPOPTIONS_REQUIRED;  
         rgProperties[cProperties].colid = DB_NULLID;  
         rgProperties[cProperties].vValue.vt = VT_EMPTY;  
         return true;  
      }  
      else  
         return false;  
   };  
};  
  
void OLEDBCleanUp() {  
   if (g_pIDBInitialize) {  
      g_pIDBInitialize->Release();  
      g_pIDBInitialize = NULL;  
   }  
   if (g_pIBcpSession) {  
      g_pIBcpSession->Release();  
      g_pIBcpSession = NULL;  
   }  
}  
  
BOOL MakeOLEDBConnect(LPWSTR  pServer) {  
   BOOL ret = true;  
   IDBProperties * pIDBProperties = NULL;  
   IDBCreateSession * pIDBCreateSession = NULL;  
   COLEDBPropSet PropSet(DBPROPSET_DBINIT);  
   COLEDBPropSet BcpProperty(DBPROPSET_SQLSERVERDATASOURCE);  
   try {  
      HRESULT hr = CoInitializeEx(NULL,COINIT_MULTITHREADED);   
      hr = CoCreateInstance(MSOLEDBSQL_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (LPVOID *)&g_pIDBInitialize);  
      if (FAILED(hr)) {  
         printf("CoCreateInstance failed\n");  
         return false;  
      }  
      PropSet.AddProperty(DBPROP_INIT_DATASOURCE, (LPWSTR)pServer);  
      PropSet.AddProperty(DBPROP_AUTH_INTEGRATED, L"SSPI");  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (void**) &pIDBProperties);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->QueryInterface(IID_IDBProperties...) failed\n");  
         throw false;  
      }  
      hr = pIDBProperties->SetProperties(1, &PropSet);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties(...) failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->Initialize();  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->Initialize() failed\n");  
         throw false;  
      }  
      BcpProperty.AddProperty(SSPROP_ENABLEFASTLOAD, true);  
      BcpProperty.AddProperty(SSPROP_ENABLEBULKCOPY, true);  
      hr = pIDBProperties->SetProperties(1, &BcpProperty);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties() for bcp failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->QueryInterface(IID_IDBCreateSession..) failed\n");  
         throw false;  
      }  
  
      hr = pIDBCreateSession->CreateSession(NULL, IID_IBCPSession2, (IUnknown**) &g_pIBcpSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBCreateSession->CreateSession() failed\n");  
         throw false;  
      }  
   }  
   catch(...) {  
      ret = false;  
   }  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
   return ret;  
}  
  
BOOL BCPSetBulkMode(LPWSTR pszServer, LPTSTR pszQureryOut, char BCPType, LPWSTR pszDataFile) {  
   HRESULThr;  
   if (!MakeOLEDBConnect(pszServer))  
      return false;  
   hr = g_pIBcpSession->BCPInit(NULL, pszDataFile, NULL, BCP_DIRECTION_OUT );   // bcp init for queryout  
   if (FAILED(hr)) {  
      printf("BCP init failed\n");  
      OLEDBCleanUp();  
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
  
   if(BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if(BCPType == 'w') {   // bcp -w  
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
               OLEDBCleanUp();  
               return false;  
            }  
            hr = g_pIBcpSession->BCPSetBulkMode(bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (FAILED(hr)) {  
               printf("BCPSetBulkMode failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
  
            // set queryout TSQL statement  
            hr = g_pIBcpSession->BCPControl(BCP_OPTION_HINTS, pszQureryOut);  
            if (FAILED(hr)) {  
               printf("BCPControl failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBROWCOUNT nRowsInserted = 0;  
            hr = g_pIBcpSession->BCPExec(&nRowsInserted);  
            if (FAILED(hr)) {  
               printf("BCPExec failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            OLEDBCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', L"bcpc.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', L"bcpw.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', L"bcpn.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', L"bcp_N.dat");  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession2 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession2-ole-db.md)  
  
  
