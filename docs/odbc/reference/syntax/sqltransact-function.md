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
ms.openlocfilehash: 6c96c903b68dee2d1d215804d318d47b4c39a7a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039504"
---
# <a name="sqltransact-function"></a>SQLTransact 函数
**度**  
 引入的版本： ODBC 1.0 标准符合性：已弃用  
  
 **总结**  
 在 ODBC 3.x*中，odbc* *2.x 函数* **SQLTransact**已被**SQLEndTran**取代。 有关详细信息，请参阅[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  **SQLTransact**不支持在 ODBC 3.8 中引入的属性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 使用连接句柄上的异步操作的应用程序必须使用**SQLEndTran**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
