---
title: bcp_readfmt |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3d700f752a3194821065dc21ddd6ab96fa6a8f26
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128055"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
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
 为大容量复制启用 ODBC 连接句柄。  
  
 *szFormatFile*  
 包含数据文件的格式值的文件的路径和文件名。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 后`bcp_readfmt`读取的值设置格式，它使到适当的调用[bcp_columns](bcp-columns.md)和[bcp_colfmt](bcp-colfmt.md)。 您无需分析格式文件和进行这些调用。  
  
 若要保存格式文件，调用[bcp_writefmt](bcp-writefmt.md)。 调用`bcp_readfmt`可以引用已保存的格式。 有关详细信息，请参阅[bcp_init](bcp-init.md)。  
  
 或者，大容量复制实用工具 (**bcp**) 可以在可供引用的文件中保存用户定义数据格式`bcp_readfmt`。 有关详细信息**bcp**实用工具和结构**bcp**数据格式文件，请参阅[大容量导入和导出的数据&#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
 `BCPDELAYREADFMT`值*eOption*参数[bcp_control](bcp-control.md)修改 bcp_readfmt 的行为。  
  
> [!NOTE]  
>  格式化文件必须由版本 4.2 或更高版本生成**bcp**实用程序。  
  
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
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  