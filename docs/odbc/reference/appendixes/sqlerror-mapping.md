---
title: SQLError 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa3b66b29af755099cb273f3a19ca4e8230cd0b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302069"
---
# <a name="sqlerror-mapping"></a>SQLError 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLError**时，调用  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 映射到  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 将*HandleType*参数设置为值SQL_HANDLE_ENV、SQL_HANDLE_DBC或SQL_HANDLE_STMT（视情况而定）和*Handle*参数设置为*henv、hdbc**hdbc*或*hstmt*中的值（视情况而定）。 *RecNumber*参数由驱动程序管理器确定。
