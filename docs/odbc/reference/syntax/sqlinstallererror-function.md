---
title: SQLInstallerError 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e786d2b1fa8136c4745b8ee3a91b91069a79e873
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLInstallerError**返回 ODBC 安装程序函数的错误或状态信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>参数  
 *iError*  
 [输入]错误记录数。 有效的数字是从 1 到 8。  
  
 *pfErrorCode*  
 [输出]安装程序错误代码。 （有关详细信息，请参阅"注释"。）  
  
 *lpszErrorMsg*  
 [输出]到错误消息文本的存储的指针。  
  
 *cbErrorMsgMax*  
 [输入]最大长度*szErrorMsg*缓冲区。 这必须小于或等于 SQL_MAX_MESSAGE_LENGTH 减去的 null 终止字符。  
  
 *cbErrorMsgMax*  
 [输入]最大长度*szErrorMsg*缓冲区。 这必须小于或等于 SQL_MAX_MESSAGE_LENGTH 减去的 null 终止字符。  
  
 *pcbErrorMsg*  
 [输出]（不包括 null 终止字符） 的字节总数的指针可用于返回在*lpszErrorMsg*。 可用于返回的字节数是否大于或等于*cbErrorMsgMax*中的错误消息文本*lpszErrorMsg*截断为*cbErrorMsgMax*减null 终止字符的字节数。 *PcbErrorMsg*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLInstallerError**不会发送自己的错误值。 **SQLInstallerError**返回 SQL_NO_DATA 时无法检索错误的任何信息 (在这种情况下*pfErrorCode*是不确定)。 如果**SQLInstallerError**出于任何原因，通常将返回 SQL_ERROR，不能访问错误值**SQLInstallerError**返回 SQL_ERROR 但不会发送任何错误值。 如果你不知道警告的字符串的长度 (*lpszErrorMsg*)，你可以设置*lpszErrorMsg*为 NULL，且调用**SQLInstallerError**。 **SQLInstallerError**将中的警告字符串的长度的则返回*cbErrorMsgMax*。 如果错误消息的缓冲区太短， **SQLInstallerError**返回 SQL_SUCCESS_WITH_INFO 并返回正确*pfErrorCode*值**SQLInstallerError**.  
  
 若要确定错误消息中是否发生截断，应用程序可以比较中的值*cbErrorMsgMax*写入到的消息文本的实际长度参数*pcbErrorMsg*自变量。 如果出现截断，应为分配正确的缓冲区长度*lpszErrorMsg*和**SQLInstallerError**应该重新调用具有相应*iError*记录。  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLInstallerError** ODBC 安装程序函数的以前调用时返回 FALSE。 ODBC 安装程序和驱动程序或转换器安装函数文章零个或多个错误，仅当函数失败时 （返回 FALSE）;因此，应用程序调用**SQLInstallerError**仅 ODBC 安装程序函数失败后。  
  
 ODBC 安装程序错误队列会刷新每次调用新的安装程序函数。 因此，应用程序不需要从最后一次安装程序函数调用中检索函数以外的其他错误。  
  
 若要检索为函数调用的多个错误，应用程序调用**SQLInstallerError**多次。  
  
 当没有其他信息， **SQLInstallerError**返回 SQL_NO_DATA， *pfErrorCode*自变量是不确定， *pcbErrorMsg*参数等于 0，并*lpszErrorMsg*自变量包含单个 null 终止字符 (除非*cbErrorMsgMax*参数是否等于 0)。
