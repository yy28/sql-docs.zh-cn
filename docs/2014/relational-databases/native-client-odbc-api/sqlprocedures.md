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
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046672"
---
# <a name="sqlprocedures"></a>SQLProcedures
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQLProcedures**报告结果集列 SQL_PT_FUNCTION PROCEDURE_TYPE。  
  
 **SQLProcedures**返回 SQL_SUCCESS *CatalogName、SchemaName*或*ProcName*参数是否存在值。 当在这些参数中使用了无效值时， **SQLFetch**将返回 SQL_NO_DATA。  
  
 可以对静态服务器游标执行**SQLProcedures** 。 尝试对可更新的（动态或键集）游标执行**SQLProcedures**时，将返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQLProcedures**返回有关其名称与*ProcName*匹配并且可以由当前用户执行的任何过程的信息，或者当前用户已被授予 VIEW DEFINITION 权限的任何过程的相关信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQLProcedures 函数](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
