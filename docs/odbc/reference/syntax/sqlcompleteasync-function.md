---
title: SQLCompleteAsync 函数 |Microsoft 文档
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
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9c0780cd9d444cf872ae6781dae0a60e80e951
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函数
**一致性**  
 版本引入了： ODBC 3.8  
  
 标准合规性： 无  
  
 **摘要**  
 **SQLCompleteAsync**可以用于确定完成使用任一基于通知或轮询处理异步函数时。 有关异步操作的详细信息，请参阅[异步执行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**仅实现在 ODBC 驱动程序管理器。  
  
 在基于通知的异步处理模式下， **SQLCompleteAsync**驱动程序管理器引发的用于通知的事件对象之后必须调用。 **SQLCompleteAsync**完成异步处理和异步函数将生成返回代码。  
  
 在基于的轮询异步处理模式下， **SQLCompleteAsync**是调用原始的异步函数，而无需原始的异步函数调用中指定参数的替代方法。 **SQLCompleteAsync**可用而不考虑是否启用 ODBC 游标库。  
  
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
 [输入]完成异步所依据的句柄处理。 如果*处理*不由指定的类型是有效句柄*HandleType*， **SQLCompleteAsync**返回 SQL_INVALID_HANDLE。  
  
 如果*处理*不由指定的类型是有效句柄*HandleType*， **SQLCompleteAsync**返回 SQL_INVALID_HANDLE。  
  
 *AsyncRetCodePtr*  
 [输出]为将包含异步 API 的返回代码的缓冲区的指针。 如果*AsyncRetCodePtr*为 NULL， **SQLCompleteAsync**返回 SQL_ERROR。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_ERROR、 SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 如果**SQLCompleteAsync**返回 SQL_SUCCESS，应用程序应从指向缓冲区获取异步函数的返回代码*AsyncRetCodePtr*。 关联的 SQLSTATE，如果有的话，可以获取通过调用**SQLGetDiagRec**与*HandleType* SQL_HANDLE_STMT 和语句句柄或*HandleType*的 SQL_HANDLE_DBC 和连接句柄。 这些诊断记录了与异步函数，这不**SQLCompleteAsync**函数。  
  
 **SQLCompleteAsync**返回 SQL_SUCCESS，则指示非的代码**SQLCompleteAsync**未得到正确调用。 **SQLCompleteAsync**会将不在此情况下发布任何诊断记录。 可能的返回代码是：  
  
-   SQL_INVALID_HANDLE: 句柄由*HandleType*和*处理*不是有效的句柄。  
  
-   SQL_ERROR: *AsyncRetCodePtr*为 NULL 或句柄上未启用异步处理。  
  
-   SQL_NO_DATA： 在通知模式下，异步操作不是正在进行或驱动程序管理器具有不会得到应用程序的通知。 在轮询模式下，异步操作不是正在进行。  
  
## <a name="comments"></a>注释  
 在基于的轮询异步处理模式下， *AsyncRetCodePtr*可能 SQL_STILL_EXECUTING 时**SQLCompleteAsync**返回 SQL_SUCCESS。 应用程序应保留轮询直到*AsyncRetCodePtr*不 SQL_STILL_EXECUTING。 在基于通知的异步处理模式下， *AsyncRetCodePtr*都不会 SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
