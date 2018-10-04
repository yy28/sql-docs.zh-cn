---
title: SQLProcedures |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: feb5cd9df428ec09441ae1ebe0ff1cb051660754
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203987"
---
# <a name="sqlprocedures"></a>SQLProcedures
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQLProcedures**为结果集列 PROCEDURE_TYPE 报告。  
  
 **SQLProcedures**是否存在值都返回 SQL_SUCCESS *CatalogName、 SchemaName*或*ProcName*参数。 **SQLFetch**这些参数中使用的值无效时返回 SQL_NO_DATA。  
  
 **SQLProcedures**可以对静态服务器游标执行。 尝试执行**SQLProcedures**对可更新的 （动态或键集） 游标将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQLProcedures**返回其名称匹配的任何过程有关的信息*ProcName*和可由当前用户，或为其当前用户拥有 VIEW DEFINITION 权限。  
  
## <a name="see-also"></a>请参阅  
 [SQLProcedures 函数](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
