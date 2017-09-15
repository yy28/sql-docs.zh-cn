---
title: "SQLWriteFileDSN 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47cc9672aecb91917a5abc15de2fc34fac59d2c2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**将信息写入文件 DSN。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>参数  
 *lpszFileName*  
 [输入]为文件 DSN 名称的指针。 DSN 扩展追加到还没有 DSN 扩展的所有文件名。  
  
 *lpszAppName*  
 [输入]指向应用程序的名称。 ODBC 部分为"ODBC"。  
  
 *lpszKeyName*  
 [输入]一个指针，指向要读取的密钥名称。 有关保留关键字，请参见"注释"。  
  
 *lpszString*  
 [输出]指向与要写入的键关联的字符串。 通过此自变量指向的字符串的最大长度为 32,767 个字节。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWriteFileDSN**返回 FALSE，一个关联* \*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出* \*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|中指定的文件名称的路径*lpszFileName*自变量无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*LpszAppName*， *lpszKeyName*，或*lpszString*自变量为 NULL。|  
  
## <a name="comments"></a>注释  
 ODBC 保留的节名称 [ODBC] 要在其中存储的连接信息。 本部分的保留的关键字是相同的连接字符串中的保留**SQLDriverConnect**。 (有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。)  
  
 应用程序可以使用这些保留的关键字将信息直接写入文件 DSN。 如果应用程序想要创建或修改文件 DSN 与关联的 dsn 连接字符串，它可以调用**SQLWriteFileDSN**任何 [ODBC] 部分中的保留的连接字符串关键字。  
  
 如果*lpszString*参数为 null 指针，指向关键字*lpszKeyName*参数将删除从.dsn 文件。 如果*lpszString*和*lpszKeyName*自变量都是 null 指针，指向部分*lpszAppName*参数将删除从.dsn 文件。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|从文件 Dsn 读取信息|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
