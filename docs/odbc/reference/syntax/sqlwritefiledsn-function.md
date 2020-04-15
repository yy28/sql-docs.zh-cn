---
title: SQLWriteFileDSN 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286877"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**将信息写入文件 DSN。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>参数  
 *lpszFile名称*  
 [输入]指向文件 DSN 的名称的指针。 DSN 扩展名将追加到尚未具有 DSN 扩展名的所有文件名中。  
  
 *lpszApp名称*  
 [输入]指向应用程序名称的指针。 这是 ODBC 部分的"ODBC"。  
  
 *lpszKey名称*  
 [输入]指向要读取的键的名称的指针。 有关保留关键字，请参阅"注释"。  
  
 *lpszString*  
 [输出]指向与要写入的键关联的字符串。 此参数指向的字符串的最大长度为 32，767 字节。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWriteFileDSN**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_PATH|无效安装路径|*lpszFileName*参数中指定的文件名的路径无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*lpszAppName、lpszKeyName*或*lpszString*参数为 NULL。 *lpszKeyName*|  
  
## <a name="comments"></a>注释  
 ODBC 保留用于存储连接信息的节名称 [ODBC]。 本节的保留关键字与**SQLDriverConnect**中为连接字符串保留的关键字相同。 （有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。  
  
 应用程序可以使用这些保留的关键字将信息直接写入文件 DSN。 如果应用程序想要创建或修改与文件 DSN 关联的 DSN 连接字符串，则可以为 [ODBC] 部分中的任何保留连接字符串关键字调用**SQLWriteFileDSN。**  
  
 如果*lpszString*参数是空指针，则*lpszKeyName*参数指向的关键字将从 .dsn 文件中删除。 如果*lpszString*和*lpszKeyName*参数都是空指针，则*lpszAppName*参数指向的节将从 .dsn 文件中删除。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|从文件 DSN 读取信息|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
