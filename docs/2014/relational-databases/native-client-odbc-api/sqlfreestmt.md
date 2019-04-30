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
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190305"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt**建议不要在 ODBC 3.0 及更高版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持所有定义*选项*值为**SQLFreeStmt**。 但是， [SQLCloseCursor](sqlclosecursor.md)， [SQLBindParameter](sqlbindparameter.md)， [SQLBindCol](sqlbindcol.md)， **SQLSetDescField**，和[SQLFreeHandle](sqlfreehandle.md)替代或复制的函数**SQLFreeStmt** ，应改为使用。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeStmt 函数](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
