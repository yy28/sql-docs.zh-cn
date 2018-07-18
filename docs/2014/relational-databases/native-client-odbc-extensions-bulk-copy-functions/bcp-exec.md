---
title: bcp_exec |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_exec
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a470efbed24dd15b4ebf45f2b5db8000f2e7e947
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407756"
---
# <a name="bcpexec"></a>bcp_exec
  执行数据库表和用户文件之间数据的完整大容量复制。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_exec (  
HDBC   
hdbc  
,  
LPDBINT   
pnRowsProcessed  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是大容量复制启用 ODBC 连接句柄。  
  
 *pnRowsProcessed*  
 指向 DBINT 的指针。 **Bcp_exec**函数用成功复制的行数填充此 DBINT。 如果*pnRowsProcessed*为 NULL，则忽略了**bcp_exec**。  
  
## <a name="returns"></a>返回  
 SUCCEED、SUCCEED_ASYNC 或 FAIL。 **Bcp_exec**函数将返回 SUCCEED，如果复制了所有行。 **bcp_exec**是否仍未完成异步大容量复制操作将返回 SUCCEED_ASYNC。 **bcp_exec**返回，如果发生完全失败，或者生成错误的行数达到为 BCPMAXERRS 使用指定的值失败[bcp_control](bcp-control.md)。 BCPMAXERRS 默认为 10。 BCPMAXERRS 选项只影响从数据文件读取行（并且不是已发送到服务器的行）时提供程序检测到的语法错误。 服务器在检测到某一行有错误时将中止批处理。 检查*pnRowsProcessed*成功复制的行数的参数。  
  
## <a name="remarks"></a>Remarks  
 此函数将从用户文件到数据库表或执行相反，数据复制的值根据*eDirection*中的参数[bcp_init](bcp-init.md)。  
  
 然后再调用**bcp_exec**，调用**bcp_init**具有有效的用户文件名称。 如果没有这样做，会导致错误。  
  
 **bcp_exec**是唯一大容量复制函数是可能胜任任何时间长度。 因此，它是支持异步模式的唯一大容量复制函数。 若要设置异步模式，请使用[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)之前，先将 SQL_ATTR_ASYNC_ENABLE 设置为 SQL_ASYNC_ENABLE_ON **bcp_exec**。 若要测试的完成情况，请调用**bcp_exec**使用相同的参数。 如果大容量复制尚未完成， **bcp_exec**返回 SUCCEED_ASYNC。 它还会返回在*pnRowsProcessed*状态计数的已发送到服务器的行数。 发送到服务器的行直到到达批的末尾时才会提交。  
  
 信息的重要更改中大容量复制中的开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，请参阅[执行大容量复制操作&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用**bcp_exec**:  
  
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
if (bcp_init(hdbc, _T("pubs..authors"), _T("authors.sav"), NULL, DB_OUT)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Now, execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   if (nRowsProcessed == -1)  
      {  
      printf_s("No rows processed on bulk copy execution.\n");  
      }  
   else  
      {  
      printf_s("Incomplete bulk copy.   Only %ld row%s copied.\n",  
         nRowsProcessed, (nRowsProcessed == 1) ? "": "s");  
      }  
   return;  
   }  
  
printf_s("%ld rows processed.\n", nRowsProcessed);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
