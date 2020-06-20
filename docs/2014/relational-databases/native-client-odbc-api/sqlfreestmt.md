---
title: SQLFreeStmt |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d38237b53ed994fd3272f9e129564320f88c6e37
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022402"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  不建议在 ODBC 3.0 和更高版本中使用**SQLFreeStmt** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序支持**SQLFreeStmt**的所有已定义的*选项*值。 但是， [SQLCloseCursor](sqlclosecursor.md)、 [SQLBindParameter](sqlbindparameter.md)、 [SQLBindCol](sqlbindcol.md)、 **SQLSetDescField**和[SQLFreeHandle](sqlfreehandle.md)将替换或复制**SQLFreeStmt**的功能，而应该改用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeStmt 函数](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
