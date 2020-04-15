---
title: 级别 2 接口一致性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306158"
---
# <a name="level-2-interface-conformance"></a>级别 2 接口一致性
2 级接口一致性级别包括 1 级接口一致性级别功能以及以下功能：  
  
|||  
|-|-|  
|201|使用数据库表和视图的三部分名称。 （有关详细信息，请参阅[级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的由两部分组成的命名支持功能 101 。|  
|202|通过调用**SQLDescribeParam**来描述动态参数。|  
|203|不仅使用输入参数，还使用输出和输入/输出参数，以及存储过程的结果值。|  
|204|通过在列号 0 上调用**SQLDescribeCol**和**SQLColAttribute，** 使用书签（包括检索书签）;通过调用 SQLFetchScroll，将*Fetch 方向*参数设置为SQL_FETCH_BOOKMARK;通过调用**SQLFetchScroll，** 即可获取。并通过调用**SQLBulk 操作**，将*操作*参数设置为SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK或SQL_FETCH_BY_BOOKMARK，通过书签操作更新、删除和提取。|  
|205|通过调用**SQLColumn 特权****、SQL 外键**和**SQLTable 特权**来检索有关数据字典的高级信息。|  
|206|使用 ODBC 函数而不是 SQL 语句执行其他数据库操作，通过使用 SQL_ADD 调用**SQLBulk 操作，** 或者使用SQL_DELETE或SQL_UPDATE**调用 SQLSetPos。** （支持对**SQLSetPos**的调用，*将 LockType*参数设置为SQL_LOCK_EXCLUSIVE或SQL_LOCK_UNLOCK不是一致性级别的一部分，而是可选功能。|  
|207|为指定的单个语句启用 ODBC 函数的异步执行。|  
|208|通过调用**SQL 特别列**获取表的SQL_ROWVER行标识列。 （有关详细信息，请参阅对**SQL 特殊列**的支持，其中*标识符类型*参数设置为 SQL_BEST_ROWID作为[核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)中的要素 20。|  
|209|将SQL_ATTR_CONCURRENCY语句属性设置为SQL_CONCUR_READ_ONLY以外的至少一个值。|  
|210|超时登录请求和 SQL 查询（SQL_ATTR_LOGIN_TIMEOUT和SQL_ATTR_QUERY_TIMEOUT）的能力。|  
|211|更改默认隔离级别的能力;使用"可序列化"隔离级别执行事务的能力。|
