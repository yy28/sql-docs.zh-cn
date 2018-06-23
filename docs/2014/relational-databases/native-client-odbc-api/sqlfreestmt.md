---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8aa28af9291b06607021209fd673869b34157f53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128046"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt**不建议在 ODBC 3.0 及更高版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持所有定义*选项*值**SQLFreeStmt**。 但是， [SQLCloseCursor](sqlclosecursor.md)， [SQLBindParameter](sqlbindparameter.md)， [SQLBindCol](sqlbindcol.md)， **SQLSetDescField**，和[SQLFreeHandle](sqlfreehandle.md)替换或重复的函数**SQLFreeStmt**并且应改为使用。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeStmt 函数](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  