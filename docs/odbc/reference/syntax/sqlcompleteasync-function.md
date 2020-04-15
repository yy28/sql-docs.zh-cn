---
title: SQLCompleteasync 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299652"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 函数
**一致性**  
 版本介绍： ODBC 3.8  
  
 标准合规性：无  
  
 **摘要**  
 **SQLCompleteAsync**可用于使用基于通知或轮询的处理确定异步函数何时完成。 有关异步操作的详细信息，请参阅[异步执行](../../../odbc/reference/develop-app/asynchronous-execution.md)。  
  
 **SQLCompleteAsync**仅在 ODBC 驱动程序管理器中实现。  
  
 在基于通知的异步处理模式下，必须在驱动程序管理器引发用于通知的事件对象后调用**SQLCompleteAsync。** **SQLCompleteAsync**完成异步处理，异步函数将生成返回代码。  
  
 在基于轮询的异步处理模式下 **，SQLCompleteAsync**是调用原始异步函数的替代方法，无需在原始异步函数调用中指定参数。 无论是否启用了 ODBC 游标库，都可以使用**SQLCompleteAsync。**  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要完成异步处理的句柄的类型。 有效值SQL_HANDLE_DBC或SQL_HANDLE_STMT。  
  
 *Handle*  
 [输入]要完成异步处理的句柄。 如果*句柄*不是*HandleType*指定的类型的有效句柄，**则 SQLCompleteAsync**将返回SQL_INVALID_HANDLE。  
  
 如果*句柄*不是*HandleType*指定的类型的有效句柄，**则 SQLCompleteAsync**将返回SQL_INVALID_HANDLE。  
  
 *异步再编码器*  
 [输出]指向将包含异步 API 返回代码的缓冲区的指针。 如果*异步再编码器*为 NULL，**则 SQLCompleteAsync**返回SQL_ERROR。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 如果**SQLCompleteAsync**返回SQL_SUCCESS，则应用程序应从*AsyncRetCodeptr*指向的缓冲区获取异步函数的返回代码。 关联的 SQLSTATE（如果有）可以通过使用*SQL_HANDLE_STMT的句柄类型*、语句句柄或SQL_HANDLE_DBC的*句柄类型*和连接句柄调用**SQLGetDiagRec**来获取。 这些诊断记录与异步函数相关联，而不是此**SQLCompleteAsync**函数。  
  
 **SQLCompleteAsync**返回SQL_SUCCESS以外的代码，以指示未正确调用**SQLCompleteAsync。** **在这种情况下，SQLCompleteAsync**不会发布任何诊断记录。 可能的退货代码包括：  
  
-   *SQL_INVALID_HANDLE：HandleType*和 Handle 指示的*句柄*不是有效的句柄。  
  
-   *SQL_ERROR：AsyncRetCodePtr*为 NULL，或者手柄上未启用异步处理。  
  
-   SQL_NO_DATA：在通知模式下，异步操作未进行，或者驱动程序管理器未通知应用程序。 在轮询模式下，异步操作未进行。  
  
## <a name="comments"></a>注释  
 在基于轮询的异步处理模式下，当**SQLCompleteAsync**返回SQL_SUCCESS时，可能会SQL_STILL_EXECUTING *AsyncRetCodePtr。* 应用程序应保留轮询，直到*asyncRetCodePtr*不SQL_STILL_EXECUTING。 在基于通知的异步处理模式下 *，AsyncRetCodePtr*永远不会SQL_STILL_EXECUTING。  
  
## <a name="see-also"></a>另请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
