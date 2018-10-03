---
title: SQLCompleteAsync 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91046e19e77d3074a8ecef2163e8d46ab528bec9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639845"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函数
**符合性**  
 版本引入了： ODBC 3.8  
  
 标准符合性： 无  
  
 **摘要**  
 **SQLCompleteAsync**可用于确定何时完成使用任一通知或基于轮询的处理异步函数。 有关异步操作的详细信息，请参阅[异步执行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**仅实现 ODBC 驱动程序管理器中。  
  
 在基于通知的异步处理模式下， **SQLCompleteAsync**驱动程序管理器引发用于通知的事件对象之后必须调用。 **SQLCompleteAsync**完成异步处理和异步函数将生成返回代码。  
  
 在基于轮询的异步处理模式下， **SQLCompleteAsync**是调用原始的异步函数，而无需原始的异步函数调用中指定的参数的替代方法。 **SQLCompleteAsync**可用而不考虑是否启用 ODBC 游标库。  
  
## <a name="syntax"></a>语法  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要对其完成异步句柄的类型处理。 有效值为 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [输入]要对其完成异步句柄的处理。 如果*处理*不是由指定类型的有效句柄*HandleType*， **SQLCompleteAsync**返回 SQL_INVALID_HANDLE。  
  
 如果*处理*不是由指定类型的有效句柄*HandleType*， **SQLCompleteAsync**返回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 [输出]指向将包含的异步 API 的返回代码的缓冲区。 如果*AsyncRetCodePtr*为 NULL， **SQLCompleteAsync**返回 SQL_ERROR。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_ERROR、 SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 如果**SQLCompleteAsync**返回 SQL_SUCCESS，应用程序应指向的缓冲区中获取异步函数的返回代码*AsyncRetCodePtr*。 关联的 SQLSTATE，如果有的话，可以获取通过调用**SQLGetDiagRec**与*HandleType* SQL_HANDLE_STMT 和语句句柄或*HandleType*的 SQL_HANDLE_DBC 和连接句柄。 这些诊断记录都是异步函数，这与相关联**SQLCompleteAsync**函数。  
  
 **SQLCompleteAsync**返回的代码不是 SQL_SUCCESS，指示**SQLCompleteAsync**未正确调用。 **SQLCompleteAsync**将不在此情况下发布任何诊断记录。 可能的返回代码是：  
  
-   SQL_INVALID_HANDLE： 句柄为由*HandleType*并*处理*不是有效的句柄。  
  
-   SQL_ERROR: *AsyncRetCodePtr*为 NULL 或句柄上未启用异步处理。  
  
-   SQL_NO_DATA： 在通知模式下，异步操作不是正在进行中或驱动程序管理器不会通知应用程序。 在轮询模式下，异步操作不是正在进行中。  
  
## <a name="comments"></a>注释  
 在基于轮询的异步处理模式下， *AsyncRetCodePtr*可能 SQL_STILL_EXECUTING 时**SQLCompleteAsync**返回 SQL_SUCCESS。 应用程序应一直轮询直到*AsyncRetCodePtr*不是 SQL_STILL_EXECUTING。 在基于通知的异步处理模式下， *AsyncRetCodePtr*将永远不会为 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
