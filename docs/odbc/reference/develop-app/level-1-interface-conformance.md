---
title: 级别 1 接口一致性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306178"
---
# <a name="level-1-interface-conformance"></a>级别 1 接口一致性
级别 1 接口一致性级别包括核心接口一致性级别功能以及通常可在 OLTP 关系 DBMS 中提供的其他功能（如事务）。 除了 Core 接口一致性级别中的功能外，1 级接口一致性驱动程序还允许应用程序执行以下操作：  
  
|||  
|-|-|  
|101|指定数据库表和视图的架构（使用由两部分组成的命名）。 （有关详细信息，请参阅[级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的由三部分组成的命名功能 201 。|  
|102|调用 ODBC 函数的真实异步执行，如果适用的 ODBC 函数是同步的或给定连接上的所有异步函数。|  
|103|使用可滚动游标，从而通过使用SQL_FETCH_NEXT以外的*Fetch 定向*参数调用**SQLFetchScroll，** 从而在非正向方法中实现对结果集的访问。 （SQL_FETCH_BOOKMARK*提取方向*位于[2 级接口符合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 204 中 。|  
|104|通过调用**SQL 主要密钥**获取表的主键。|  
|105|通过 ODBC 转义序列对过程调用使用存储过程，并通过调用**SQLProcess 列**和**SQL 程序**查询有关存储过程的数据字典。 （在数据源上创建和存储过程的过程不在本文档的范围之内。|  
|106|通过调用**SQLBrowseConnect，** 通过交互式浏览可用服务器连接到数据源。|  
|107|使用 ODBC 函数而不是 SQL 语句来执行某些数据库操作：具有SQL_POSITION的**SQLSetPos**和SQL_REFRESH。|  
|108|通过调用**SQLMoreResult**获取对批处理和存储过程生成的多个结果集内容的访问。|  
|109|分隔跨越多个 ODBC 函数的事务，具有真正的原子性和在**SQLEndTran**中指定SQL_ROLLBACK的能力。|
