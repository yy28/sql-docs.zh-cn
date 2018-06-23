---
title: SQLProcedures |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 26c59b042ba861684402a4b79ce7cb1b5d77e53a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024558"
---
# <a name="sqlprocedures"></a>SQLProcedures
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQLProcedures**的结果集列 PROCEDURE_TYPE 报表 SQL_PT_FUNCTION。  
  
 **SQLProcedures**是否值已存在，则返回 SQL_SUCCESS *CatalogName、 SchemaName、* 或*ProcName*参数。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 **SQLProcedures**可以执行对静态服务器游标。 尝试执行**SQLProcedures**上的可更新的 （动态或键集） 游标，则将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQLProcedures**返回有关任何名称匹配的过程的信息*ProcName*并可执行当前用户，或为其当前用户已被授予 VIEW DEFINITION 权限。  
  
## <a name="see-also"></a>请参阅  
 [SQLProcedures 函数](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  