---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 061d4af67c73e19f927f4e2bf3461f273cbe400c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143868"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt**建议不要在 ODBC 3.0 及更高版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持所有定义*选项*值为**SQLFreeStmt**。 但是， [SQLCloseCursor](sqlclosecursor.md)， [SQLBindParameter](sqlbindparameter.md)， [SQLBindCol](sqlbindcol.md)， **SQLSetDescField**，和[SQLFreeHandle](sqlfreehandle.md)替代或复制的函数**SQLFreeStmt** ，应改为使用。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeStmt 函数](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
