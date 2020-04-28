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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299673"
---
# <a name="statement-handles"></a>语句句柄
*语句*最容易被视为一种 SQL 语句，例如** \* SELECT FROM Employee**。 但是，语句不只是 SQL 语句，而是包含与该 SQL 语句相关联的所有信息，如语句所创建的所有结果集和执行语句时使用的参数。 语句甚至不需要具有应用程序定义的 SQL 语句。 例如，在语句上执行目录函数（如**SQLTables** ）时，它会执行返回表名列表的预定义 SQL 语句。  
  
 每个语句由语句句柄标识。 语句与单个连接相关联，并且该连接上可能有多个语句。 某些驱动程序会限制它们支持的活动语句的数量;**SQLGetInfo**中的 SQL_MAX_CONCURRENT_ACTIVITIES 选项指定驱动程序在单个连接上支持的活动语句的数量。 如果语句具有挂起的结果，则将其定义为*活动状态*，其中的结果是结果集或受**INSERT**、 **UPDATE**或**DELETE**语句影响的行数，或者正在通过多次调用**SQLPutData**发送数据。  
  
 在实现 ODBC （驱动程序管理器或驱动程序）的代码段内，语句句柄标识包含语句信息的结构，如：  
  
-   语句的状态  
  
-   当前语句级别诊断  
  
-   绑定到语句的参数和结果集列的应用程序变量的地址  
  
-   每个语句特性的当前设置  
  
 语句句柄用于大多数 ODBC 函数。 特别要注意的是，在函数中使用它们来绑定参数和结果集列（**SQLBindParameter**和**SQLBindCol**）、prepare 和 execute 语句（**SQLPrepare**、 **SQLExecute**和**SQLExecDirect**）、检索元数据（**SQLColAttribute**和**SQLDescribeCol**）、提取结果（SQLFetch）和检索**诊断（****SQLGetDiagField**和**SQLGetDiagRec**）。 它们还用于目录函数（**SQLColumns**、 **SQLTables**等）以及许多其他函数。  
  
 语句句柄通过**SQLAllocHandle**分配，并与**SQLFreeHandle**一起释放。
