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
manager: craigg
ms.openlocfilehash: 9b7fbc3754121418ea2059ea511f3b247dcff8dd
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706094"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  不建议在 ODBC 3.0 和更高版本中使用**SQLFreeStmt** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序支持**SQLFreeStmt**的所有已定义的*选项*值。 但是， [SQLCloseCursor](sqlclosecursor.md)、 [SQLBindParameter](sqlbindparameter.md)、 [SQLBindCol](sqlbindcol.md)、 **SQLSetDescField**和[SQLFreeHandle](sqlfreehandle.md)将替换或复制**SQLFreeStmt**的功能，而应该改用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeStmt 函数](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
