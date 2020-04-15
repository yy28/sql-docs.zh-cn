---
title: SQLTransact 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a4f1da36a7c233e9a1b5832ee83e86a5c1f77d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287077"
---
# <a name="sqltransact-function"></a>SQLTransact 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 在 ODBC *3.x*中，ODBC *2.x*函数**SQLTransact**已被**SQLEndTran**替换。 有关详细信息，请参阅[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  **SQLTransact**不支持在 ODBC 3.8 中引入的属性SQL_ASYNC_DBC_FUNCTION_ENABLE。 在连接句柄上使用异步操作的应用程序必须使用**SQLEndTran**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
