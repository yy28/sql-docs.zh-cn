---
title: SQLTransact 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ad40522bd9f97c72a5d0a71d089b9e7c98a7d6b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793621"
---
# <a name="sqltransact-function"></a>SQLTransact 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：不推荐使用  
  
 **摘要**  
 在 ODBC *3.x*，ODBC *2.x*函数**SQLTransact**已由**SQLEndTran**。 有关详细信息，请参阅[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  属性 SQL_ASYNC_DBC_FUNCTION_ENABLE，ODBC 3.8 中引入了，不受**SQLTransact**。 使用连接句柄上的异步操作的应用程序必须使用**SQLEndTran**。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
