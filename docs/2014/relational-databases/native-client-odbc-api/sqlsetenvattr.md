---
title: SQLSetEnvAttr |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b0d30ac70ff3b7974f7d0530b9fb50494ac424
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188753"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  [Odbc 程序员参考](https://go.microsoft.com/fwlink/?LinkId=45250)定义了 odbc 驱动程序应如何从写入 odbc 2 的应用程序解释**SQLSetEnvAttr**属性规范。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序符合这些规则。  
  
 **SQLSetEnvAttr**控制的属性之一是是否要使用连接池。 如果连接池与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序一起使用，则在使用[SQLDriverConnect](sqldriverconnect.md)或**SQLConnect**连接时， *DriverCompletion*参数必须设置为 SQL_DRIVER_NOPROMPT。  
  
## <a name="see-also"></a>另请参阅  
 [SQLSetEnvAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
