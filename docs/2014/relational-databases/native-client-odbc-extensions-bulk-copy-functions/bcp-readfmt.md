---
title: bcp_readfmt |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8ea8094778c8ccb204712536f01b13152c89c7a1
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701898"
---
# <a name="bcp_readfmt"></a>bcp_readfmt
  从指定的格式文件中读取数据文件格式定义。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
 *szFormatFile*  
 包含数据文件的格式值的文件的路径和文件名。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 `bcp_readfmt`读取格式值后，它将对[bcp_columns](bcp-columns.md)和[bcp_colfmt](bcp-colfmt.md)进行适当的调用。 您无需分析格式文件和进行这些调用。  
  
 若要保存格式化文件，请调用[bcp_writefmt](bcp-writefmt.md)。 对的调用 `bcp_readfmt` 可以引用保存的格式。 有关详细信息，请参阅[bcp_init](bcp-init.md)。  
  
 或者，大容量复制实用工具（**bcp**）可以将用户定义的数据格式保存在可由引用的文件中 `bcp_readfmt` 。 有关**bcp**实用工具和**bcp**数据格式文件的结构的详细信息，请参阅[批量导入和导出数据 &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
 `BCPDELAYREADFMT` [Bcp_control](bcp-control.md)的*eOption*参数的值修改 bcp_readfmt 的行为。  
  
> [!NOTE]  
>  格式化文件必须由**bcp**实用工具版本4.2 或更高版本生成。  
  
## <a name="example"></a>示例  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
