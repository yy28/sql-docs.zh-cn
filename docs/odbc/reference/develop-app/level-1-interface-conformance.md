---
title: "级别 1 接口一致性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34c9b63a4abda3b510ab2b9549f90251996ec9e9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="level-1-interface-conformance"></a>级别 1 接口一致性
级别 1 接口一致性级别包括核心接口一致性级别功能以及其他功能，如通常都存在于 OLTP 关系 DBMS 的事务。 级别 1 接口 – 符合的驱动程序可让应用程序执行以下操作，除了核心接口一致性级别中的功能：  
  
|||  
|-|-|  
|101|指定数据库的架构表和视图 （使用两部分命名）。 (有关详细信息，请参阅功能中的 201 的由三部分命名[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|102|调用 ODBC 函数，所有同步或在给定连接上所有异步适用 ODBC 函数所在 true 异步的执行。|  
|103|使用可滚动游标，并从而实现向方法中设置其他比只进时，通过调用结果的访问**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_NEXT 以外的参数。 (SQL_FETCH_BOOKMARK *FetchOrientation*处于中的新功能 204[级别 2 的接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|104|通过调用获取表的主键**SQLPrimaryKeys**。|  
|105|使用存储的过程，通过过程调用 ODBC 转义序列，并通过调用查询有关存储过程，数据字典**SQLProcedureColumns**和**SQLProcedures**。 （依据过程创建和数据源上存储的过程不在本文的讨论范围。）|  
|106|通过以交互方式通过调用浏览可用的服务器中，连接到数据源**SQLBrowseConnect**。|  
|107|使用 ODBC 函数而不是 SQL 语句，以便执行某些数据库操作： **SQLSetPos** SQL_POSITION 与 SQL_REFRESH。|  
|108|获取访问权限由批处理和存储的过程，通过调用生成的多个结果集的内容**SQLMoreResults**。|  
|109|分隔事务跨越几个 ODBC 函数中使用真正的原子性和能够指定在 SQL_ROLLBACK **SQLEndTran**。|
