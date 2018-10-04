---
title: 级别 1 接口一致性 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f2071ec7d7c9a31a9da8982b583ef7618700db5e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649315"
---
# <a name="level-1-interface-conformance"></a>级别 1 接口一致性
级别 1 接口一致性级别包括核心接口一致性级别功能以及其他功能，如通常都存在于 OLTP 关系 DBMS 的事务。 级别 1 接口 – 符合的驱动程序可让应用程序执行以下操作，除了核心接口一致性级别中的功能：  
  
|||  
|-|-|  
|101|指定数据库的架构表和视图 （使用两部分命名）。 (有关详细信息，请参阅三部分命名功能在 201[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|102|调用 ODBC 函数，适用的 ODBC 函数的所有同步的或者全都是异步上给定的连接，则返回 true 异步执行。|  
|103|使用可滚动游标，从而达到权访问的结果集的方法而非只进、 通过调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_NEXT 以外的参数。 (SQL_FETCH_BOOKMARK *FetchOrientation*在中的新功能 204[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|104|通过调用获取表的主键**SQLPrimaryKeys**。|  
|105|使用存储的过程，通过 ODBC 转义序列的过程调用，并通过调用查询有关存储过程的数据字典**SQLProcedureColumns**并**SQLProcedures**。 （通过该过程创建和数据源上存储的过程超出了本文档的范围是。）|  
|106|通过以交互方式浏览可用的服务器，通过调用连接到数据源**SQLBrowseConnect**。|  
|107|使用 ODBC 函数而不是 SQL 语句来执行某些数据库操作： **SQLSetPos**使用 SQL_POSITION 和 SQL_REFRESH。|  
|108|获取对通过调用生成的批处理和存储的过程的多个结果集的内容访问权限**SQLMoreResults**。|  
|109|分隔事务跨越多个 ODBC 函数，使用真正的原子性和可指定在 SQL_ROLLBACK **SQLEndTran**。|
