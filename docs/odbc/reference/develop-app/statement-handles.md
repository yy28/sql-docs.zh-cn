---
title: 语句句柄 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f844a4a783ccdbb2281857e440ce09d965a0c738
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913912"
---
# <a name="statement-handles"></a>语句句柄
A*语句*非常轻松地视为 SQL 语句，如**选择\*从员工**。 但是，一个语句是远不止一个 SQL 语句，它包含所有与该 SQL 语句，如所有结果集由该语句创建和执行语句中使用的参数关联的信息。 语句不甚至不需要具有应用程序定义 SQL 语句。 例如，目录的如函数时**SQLTables**执行上一条语句，它会执行返回表名称的列表的预定义的 SQL 语句。  
  
 每个语句的语句句柄由标识。 语句是与单个连接，且可以有多个语句在该连接上。 某些驱动程序限制它们支持; 活动语句的数目SQL_MAX_CONCURRENT_ACTIVITIES 选项**SQLGetInfo**指定驱动程序支持在单个连接的多少活动语句。 语句定义为*active*如果它具有挂起的结果，结果的结果集或受影响的行计数**插入**，**更新**，或**删除**语句或数据发送到多个调用**SQLPutData**。  
  
 中的实现 ODBC （驱动程序管理器或驱动程序） 的代码段，语句句柄标识包含语句的信息，如的结构：  
  
-   语句的状态  
  
-   当前的语句级诊断  
  
-   应用程序变量的地址绑定到语句的参数和结果集列  
  
-   每个语句属性当前设置  
  
 在大多数 ODBC 函数使用语句句柄。 值得注意的是，它们用于在函数中绑定参数和结果集列 (**SQLBindParameter**和**SQLBindCol**)、 准备和执行语句 (**SQLPrepare****SQLExecute**，和**SQLExecDirect**)，检索元数据 (**SQLColAttribute**和**SQLDescribeCol**)，提取结果 (**SQLFetch**)，并检索诊断 (**SQLGetDiagField**和**SQLGetDiagRec**)。 它们也用在目录函数 (**SQLColumns**， **SQLTables**，依次类推) 和许多其他功能。  
  
 语句句柄分配与**SQLAllocHandle**并释放与**SQLFreeHandle**。
