---
title: 语句句柄 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299673"
---
# <a name="statement-handles"></a>语句句柄
*语句*最容易被视为 SQL 语句，例如**从员工中选择\***。 但是，语句不仅仅是一个 SQL 语句 - 它包含与该 SQL 语句关联的所有信息，例如由语句创建的任何结果集以及在执行语句中使用的参数。 语句甚至不需要具有应用程序定义的 SQL 语句。 例如，当在语句上执行目录函数（如**SQLTables）** 时，它将执行预定义的 SQL 语句，该语句返回表名称的列表。  
  
 每个语句都由语句句柄标识。 语句与单个连接相关联，并且该连接上可以有多个语句。 某些驱动程序限制他们支持的活动语句数;**SQLGetInfo**中的SQL_MAX_CONCURRENT_ACTIVITIES选项指定驱动程序在单个连接上支持多少个活动语句。 如果语句的结果处于挂起状态，则语句定义为*活动*，其中结果为结果集，或者受**INSERT、UPDATE**或**DELETE**语句**UPDATE**影响的行计数，或者通过多次调用**SQLPutData**发送数据。  
  
 在实现 ODBC（驱动程序管理器或驱动程序）的代码段中，语句句柄标识包含语句信息的结构，例如：  
  
-   语句的状态  
  
-   当前语句级诊断  
  
-   绑定到语句的参数和结果集列的应用程序变量的地址  
  
-   每个语句属性的当前设置  
  
 语句句柄用于大多数 ODBC 函数。 值得注意的是，它们用于绑定参数和结果集列 **（SQLBind参数**和**SQLBindCol），** 准备和执行语句 **（SQLPrepare、SQLExecute**和**SQLExecDirect），** 检索**SQLExecute**元数据 **（SQLCol属性**和**SQLDescribeCol），** 提取结果 **（SQLFetch），** 并检索诊断 **（SQLGetDiagField**和**SQLGetDiagRec）。** 它们还用于目录函数 **（SQLColumns、SQLTables**等）和许多其他函数。 **SQLTables**  
  
 语句句柄使用**SQLAllocHandle**分配，并释放**SQLFreeHandle**。
