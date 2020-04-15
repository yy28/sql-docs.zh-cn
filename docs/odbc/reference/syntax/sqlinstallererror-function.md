---
title: SQL安装程序错误功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302098"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQL安装程序错误**返回 ODBC 安装程序功能的错误或状态信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>参数  
 *i错误*  
 [输入]错误记录编号。 有效号码为 1 到 8。  
  
 *pfError代码*  
 [输出]安装程序错误代码。 （有关详细信息，请参阅"注释"。  
  
 *lpsz错误Msg*  
 [输出]指向错误消息文本的存储的指针。  
  
 *cbErrorMsgMax*  
 [输入]*szErrorMsg*缓冲区的最大长度。 这必须小于或等于SQL_MAX_MESSAGE_LENGTH减去 null 终止字符。  
  
 *cbErrorMsgMax*  
 [输入]*szErrorMsg*缓冲区的最大长度。 这必须小于或等于SQL_MAX_MESSAGE_LENGTH减去 null 终止字符。  
  
 *多加错姆斯格*  
 [输出]指向可用以*lpszErrorMsg*返回的字节总数（不包括空终止字符）的指针。 如果可用于返回的字节数大于或等于*cbErrorMsgMax，**则 lpszErrorMsg*中的错误消息文本将被截断为*cbErrorMsgMax*减去 null 终止字符字节。 *pcbErrorMsg*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA或SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQL安装程序错误**不会为自己发布错误值。 **当 SQL 安装程序错误**无法检索任何错误信息（在这种情况下 *，pfErrorCode*未定义）时，它将返回SQL_NO_DATA。 如果**SQL 安装程序由于**通常返回SQL_ERROR的任何原因无法访问错误值，则**SQL 安装程序错误**将返回SQL_ERROR但不过帐任何错误值。 如果您不知道警告字符串的长度 *（lpszErrorMsg*）， 您可以将*lpszErrorMsg*设置为 NULL 并调用**SQL 安装程序错误**。 **SQL安装程序错误**将返回*cbErrorMsgMax*中警告字符串的长度。 如果错误消息的缓冲区太短 **，SQL安装程序错误**将返回SQL_SUCCESS_WITH_INFO并返回**SQL 安装程序错误**的正确*pfErrorCode*值。  
  
 要确定错误消息中是否发生了截断，应用程序可以将*cbErrorMsgMax*参数中的值与写入*pcbErrorMsg*参数的消息文本的实际长度进行比较。 如果确实发生截断，则应为*lpszErrorMg*分配正确的缓冲区长度，并且应使用相应的*iError*记录再次调用**SQL 安装程序错误**。  
  
## <a name="comments"></a>注释  
 当对 ODBC 安装程序函数的上一个调用返回 FALSE 时，应用程序调用**SQL 安装程序Error。** ODBC 安装程序和驱动程序或转换器设置函数仅在函数失败时才出现零个或多个错误（返回 FALSE）;因此，应用程序仅在 ODBC 安装程序功能失败后才调用**SQL 安装程序Error。**  
  
 每次调用新的安装程序函数时，都会刷新 ODBC 安装程序错误队列。 因此，应用程序不能指望检索上次安装程序函数调用以外的函数的错误。  
  
 若要检索函数调用的多个错误，应用程序多次调用**SQL 安装程序错误**。  
  
 当没有其他信息时 **，SQLInstallerError**返回*SQL_NO_DATA，pfErrorCode*参数未定义 *，pcbErrorMsg*参数等于*0，lpszErrorMsg*参数包含一个空终止字符（除非*cbErrorMgMax*参数等于 0）。
