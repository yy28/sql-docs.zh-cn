---
title: 语句句柄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f249bb13ece6382e96dfe953b1d3c1d96c7bf65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149002"
---
# <a name="statement-handles"></a>语句句柄
一个*语句*非常方便地看作是一个 SQL 语句，如**选择\*从员工**。 但是，一个语句是不止是一个 SQL 语句-它包含所有与该 SQL 语句，如所有创建语句的结果集和执行语句中使用参数相关联的信息。 语句不甚至不需要将应用程序定义 SQL 语句。 例如，当目录函数如**SQLTables**执行上一条语句，它将执行返回一系列表名称的预定义的 SQL 语句。  
  
 语句句柄由标识每个语句。 语句为单个连接，与相关联，可以在该连接上的多个语句。 某些驱动程序限制它们支持; 活动语句数在选项 SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo**指定多少驱动程序支持在单个连接的活动语句。 语句定义要*active*如果它具有挂起的结果，具有结果的结果集或受影响的行的计数**插入**，**更新**，或者**删除**语句或数据发送到多个调用**SQLPutData**。  
  
 在一段代码实现 ODBC （驱动程序管理器或驱动程序），语句句柄标识包含语句的信息，如的结构：  
  
-   语句的状态  
  
-   当前的语句级诊断  
  
-   应用程序变量的地址绑定到语句的参数和结果集列  
  
-   每个语句属性当前设置  
  
 语句句柄用于大多数 ODBC 函数。 值得注意的是，它们用于在函数中绑定参数和结果集列 (**SQLBindParameter**并**SQLBindCol**)、 准备和执行语句 (**SQLPrepare** **SQLExecute**，并**SQLExecDirect**)，检索元数据 (**SQLColAttribute**并**SQLDescribeCol**)，提取结果 (**SQLFetch**)，并检索诊断 (**SQLGetDiagField**并**SQLGetDiagRec**)。 它们还使用目录函数中 (**SQLColumns**， **SQLTables**，依次类推) 和许多其他功能。  
  
 分配语句句柄**SQLAllocHandle**和与已释放**SQLFreeHandle**。
