---
title: "SQLTransact 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1af98fb53aadf7ea6bb2253041c951481a019027
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-function"></a>SQLTransact 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： 不推荐使用  
  
 **摘要**  
 在 ODBC 3。*x*，ODBC 2*.x*函数**SQLTransact**已被取代**SQLEndTran**。 有关详细信息，请参阅[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  不支持的特性 SQL_ASYNC_DBC_FUNCTION_ENABLE，ODBC 3.8 中引入， **SQLTransact**。 使用对连接句柄的异步操作的应用程序必须使用**SQLEndTran**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
