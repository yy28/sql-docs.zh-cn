---
title: SQLInstallerError 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab9461d87a3df2efc98c38e4c72cee4c247fee7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138030"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLInstallerError**返回 ODBC 安装程序函数的错误或状态信息。  
  
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
 *iError*  
 [输入]错误记录号。 有效的数字是从 1 到 8。  
  
 *pfErrorCode*  
 [输出]安装程序错误代码。 （有关详细信息，请参阅"注释"。）  
  
 *lpszErrorMsg*  
 [输出]一个指针，指向存储的错误消息文本。  
  
 *cbErrorMsgMax*  
 [输入]最大长度*szErrorMsg*缓冲区。 这必须小于或等于 SQL_MAX_MESSAGE_LENGTH 减号 null 终止字符。  
  
 *cbErrorMsgMax*  
 [输入]最大长度*szErrorMsg*缓冲区。 这必须小于或等于 SQL_MAX_MESSAGE_LENGTH 减号 null 终止字符。  
  
 *pcbErrorMsg*  
 [输出]指向的总字节数 （不包括 null 终止字符） 可用于在中返回*lpszErrorMsg*。 可用来返回的字节数是否大于或等于*cbErrorMsgMax*中的错误消息文本*lpszErrorMsg*将被截断为*cbErrorMsgMax*减null 终止字符的字节数。 *PcbErrorMsg*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLInstallerError**不会为其自身发送错误值。 **SQLInstallerError**不能检索任何错误信息时返回 SQL_NO_DATA (在这种情况下*pfErrorCode*是不确定)。 如果**SQLInstallerError**出于任何原因，通常会返回 SQL_ERROR，不能访问错误值**SQLInstallerError**返回 SQL_ERROR，但不会发送任何错误的值。 如果不知道警告字符串的长度 (*lpszErrorMsg*)，可以设置*lpszErrorMsg*为 NULL，并调用**SQLInstallerError**。 **SQLInstallerError**中的警告字符串的长度将则返回*cbErrorMsgMax*。 如果错误消息的缓冲区太短， **SQLInstallerError**返回 SQL_SUCCESS_WITH_INFO，并返回正确*pfErrorCode*值**SQLInstallerError**.  
  
 若要确定是否发生了截断错误消息中，应用程序可以比较中的值*cbErrorMsgMax*参数写入到的消息文本的实际长度*pcbErrorMsg*自变量。 如果出现截断，应为分配正确的缓冲区长度*lpszErrorMsg*并**SQLInstallerError**应与相应再次调用*iError*记录。  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLInstallerError**以前调用 ODBC 安装程序函数时返回 FALSE。 ODBC 安装程序和驱动程序或转换器安装程序函数发布零个或多个错误，仅当函数失败时 （返回 FALSE）;因此，应用程序调用**SQLInstallerError**仅 ODBC 安装程序函数失败后。  
  
 ODBC 安装程序错误队列刷新每次调用新的安装程序函数。 因此，应用程序不能期望从最后一次安装程序函数调用中检索的函数以外的其他错误。  
  
 若要检索的函数调用的多个错误，应用程序调用**SQLInstallerError**多次。  
  
 当没有任何其他信息， **SQLInstallerError**返回 SQL_NO_DATA， *pfErrorCode*自变量是未定义， *pcbErrorMsg*参数等于 0，并*lpszErrorMsg*自变量包含一个 null 终止字符 (除非*cbErrorMsgMax*参数等于 0)。
