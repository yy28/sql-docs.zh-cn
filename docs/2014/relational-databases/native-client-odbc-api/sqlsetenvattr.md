---
title: SQLSetEnvAttr |Microsoft 文档
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
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 663d274b13a8cc5ac8ac53a2d8f9da4f925c7d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125850"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  [ODBC 程序员参考](http://go.microsoft.com/fwlink/?LinkId=45250)定义 ODBC 驱动程序应解释如何**SQLSetEnvAttr**属性从对 ODBC 2 编写的应用程序的规范。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序符合这些规则。  
  
 由控制特性之一**SQLSetEnvAttr**连接池是否用于。 如果连接池用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序， *DriverCompletion*参数必须设置为 SQL_DRIVER_NOPROMPT，使用连接时[SQLDriverConnect](sqldriverconnect.md)或**SQLConnect**。  
  
## <a name="see-also"></a>请参阅  
 [SQLSetEnvAttr 函数](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  