---
title: SQLWriteFileDSN 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b1ce34074a2326d17a199537b308a9a670d8163
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039428"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**将信息写入到文件 DSN。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>参数  
 *lpszFileName*  
 [输入]指向文件 DSN 的名称。 DSN 扩展附加到所有还没有 DSN 扩展名的文件名称。  
  
 *lpszAppName*  
 [输入]指向应用程序的名称。 这是针对 ODBC 部分的"ODBC"。  
  
 *lpszKeyName*  
 [输入]指向要读取的键的名称。 有关保留关键字，请参阅"注释"。  
  
 *lpszString*  
 [输出]指向要写入的键与关联的字符串。 通过此参数指向的字符串的最大长度为 32,767 个字节。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWriteFileDSN**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|Error|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|中指定的文件名称的路径*lpszFileName*参数无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*LpszAppName*， *lpszKeyName*，或*lpszString*参数为 NULL。|  
  
## <a name="comments"></a>注释  
 ODBC 保留部分名称 [ODBC] 要在其中存储的连接信息。 本部分中的保留的关键字将与连接字符串中保留相同**SQLDriverConnect**。 (有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。)  
  
 应用程序可以使用这些保留的关键字将信息直接写入文件 DSN。 如果应用程序想要创建或修改文件 DSN 与关联的 dsn 连接字符串，它可以调用**SQLWriteFileDSN**任何 [ODBC] 部分中的保留的连接字符串关键字。  
  
 如果*lpszString*参数为 null 指针，指向关键字*lpszKeyName*参数将删除从.dsn 文件。 如果*lpszString*并*lpszKeyName*自变量都是 null 指针，指向部分*lpszAppName*参数将删除从.dsn 文件。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|从文件 Dsn 中读取信息|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
