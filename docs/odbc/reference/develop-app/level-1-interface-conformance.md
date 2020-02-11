---
title: 1级接口一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05cf381ccbb8c0747db88259acfb4ba218d3e0ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135005"
---
# <a name="level-1-interface-conformance"></a>级别 1 接口一致性
1级接口一致性级别包括核心接口一致性级别功能，以及通常在 OLTP 关系 DBMS 中可用的附加功能，例如事务。 除了核心接口一致性级别中的功能，应用程序还可以使用1级接口相容的驱动程序来执行以下操作：  
  
|||  
|-|-|  
|101|指定数据库表和视图的架构（使用由两部分组成的命名）。 （有关详细信息，请参阅第[2 级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的三部分命名功能201。）|  
|102|调用 ODBC 函数的真正异步执行，其中适用的 ODBC 函数在给定连接上全部同步或全部异步。|  
|103|通过使用除 SQL_FETCH_NEXT 以外的*FetchOrientation*参数调用**SQLFetchScroll** ，可以使用可滚动游标，从而实现仅向前方法中的结果集的访问权限。 （SQL_FETCH_BOOKMARK *FetchOrientation*处于[第2级接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)的功能204中。）|  
|104|通过调用**SQLPrimaryKeys**获取表的主键。|  
|105|使用存储过程通过 ODBC 转义序列进行过程调用，并通过调用**SQLProcedureColumns**和**SQLProcedures**查询有关存储过程的数据字典。 （创建过程，并将其存储在数据源上的过程不在本文档的讨论范围内。）|  
|106|通过以交互方式浏览可用服务器来连接到数据源，方法是调用**SQLBrowseConnect**。|  
|107|使用 ODBC 函数而不是 SQL 语句来执行某些数据库操作： **SQLSetPos**与 SQL_POSITION 和 SQL_REFRESH。|  
|108|通过调用**SQLMoreResults**，访问批处理和存储过程生成的多个结果集的内容。|  
|109|分隔跨多个 ODBC 函数的事务，具有真正的原子性和在**SQLEndTran**中指定 SQL_ROLLBACK 的能力。|
