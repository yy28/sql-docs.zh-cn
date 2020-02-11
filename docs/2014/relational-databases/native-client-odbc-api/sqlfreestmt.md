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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63190305"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  不建议在 ODBC 3.0 和更高版本中使用**SQLFreeStmt** 。 Native Client ODBC 驱动程序支持**SQLFreeStmt**的所有已定义的选项值。 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 但是， [SQLCloseCursor](sqlclosecursor.md)、 [SQLBindParameter](sqlbindparameter.md)、 [SQLBindCol](sqlbindcol.md)、 **SQLSetDescField**和[SQLFreeHandle](sqlfreehandle.md)将替换或复制**SQLFreeStmt**的功能，而应该改用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeStmt 函数](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
