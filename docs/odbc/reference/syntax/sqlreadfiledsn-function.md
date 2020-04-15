---
title: SQLReadFileDSN 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303948"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLReadFileDSN**从文件 DSN 读取信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>参数  
 *lpszFile名称*  
 [输入]指向包含 .dsn 文件名称的数据缓冲区的指针。 .dsn 扩展名将追加到尚未具有 .dsn 扩展名的所有文件名中。 * \*lpszFileName*中的值必须是 null 终止的字符串。  
  
 *lpszApp名称*  
 [输入]指向包含应用程序名称的数据缓冲区的指针。 这是 ODBC 部分的"ODBC"。 * \*lpszAppName*中的值必须是 null 终止的字符串。  
  
 *lpszKey名称*  
 [输入]指向包含要读取的键名称的数据缓冲区的指针。 有关保留关键字，请参阅"注释"。 * \*lpszAppName*中的值必须是 null 终止的字符串。  
  
 *lpszString*  
 [输出]指向包含与要读取的键关联的字符串的数据缓冲区的指针。  
  
 如果*\*lpszFileName*是有效的 .dsn 文件名，但*lpszAppName*参数是空指针 *，lpszKeyName*参数是空指针，则*\*lpszString*包含有效应用程序的列表。 如果*\*lpszFileName*是有效的 .dsn 文件名，*\*并且 lpszAppName*是有效的应用程序名称，但*lpszKeyName*参数是空指针，则*\*lpszString*在 DSN 文件的相应部分中包含有效保留关键字的列表，按分号分隔。 如果*\*lpszFileName*是有效的 .dsn 文件名，但*\*lpszAppName*是空指针 *，lpszKeyName*参数是空指针，则*\*lpszString*包含 DSN 文件中各节的列表，按分号分隔。  
  
 *cbString*  
 [输入]lpszString 缓冲区的长度。 * \**  
  
 *pcbString*  
 [输出]可在*\*lpszString*中返回的字节总数。 如果可用于返回的字节数大于或等于*cbString，* 则*\*lpszString*中的输出字符串将被截断为*cbString*减去 null 终止字符。 *pcbString*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLReadFileDSN**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszString*参数为 NULL。<br /><br /> *cbString*参数小于或等于 0。|  
|ODBC_ERROR_INVALID_PATH|无效安装路径|*lpszFileName*参数中指定的文件名的路径无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*lpszAppName*参数为 NULL，而*lpszKeyName*参数有效。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|输出字符串被截断|在*\*lpszString*中返回的字符串被截断，因为*cbString*中的值小于或等于*\*在 pcbString*中的值。|  
|ODBC_ERROR_REQUEST_FAILED|申请失败。|该关键字不存在于文件 DSN 中。|  
  
## <a name="comments"></a>注释  
 ODBC 保留用于存储连接信息的节名称 [ODBC]。 本节的保留关键字与**SQLDriverConnect**中为连接字符串保留的关键字相同。 （有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。  
  
 应用程序可以使用这些保留的关键字读取文件 DSN 中的信息。 如果应用程序想要找出与文件 DSN 关联的 DSN 连接字符串，则可以为 [ODBC] 部分中的任何保留连接字符串关键字调用**SQLReadFileDSN。** 在无 DSN 连接中传递的完整连接字符串是 [ODBC] 部分中的所有关键字（保留和特定于驱动程序）的组合。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将信息写入文件 DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
