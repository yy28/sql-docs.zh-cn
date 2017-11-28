---
title: "级别 2 接口一致性 |Microsoft 文档"
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
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 216cfaa83c7b48e94778b98fde9766a47221091b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="level-2-interface-conformance"></a>级别 2 接口一致性
级别 2 接口一致性级别包括级别 1 界面一致性 – 级别功能以及下列功能：  
  
|||  
|-|-|  
|201|使用数据库表和视图的由三部分名称。 (有关详细信息，请参阅两部分命名支持中的功能 101[级别 1 的接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)。)|  
|202|描述动态参数，通过调用**SQLDescribeParam**。|  
|203|使用不仅输入的参数，但还输出输入/输出参数、 参数和结果值的存储过程。|  
|204|使用书签，包括通过调用检索书签， **SQLDescribeCol**和**SQLColAttribute**列是数字 0; 提取基于通过调用的书签， **SQLFetchScroll**与*FetchOrientation*参数设为 SQL_FETCH_BOOKMARK; 和更新，删除，并通过调用提取书签操作**SQLBulkOperations**与*操作*参数设置为 SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK。|  
|205|检索有关的高级信息数据字典中，通过调用**SQLColumnPrivileges**， **SQLForeignKeys**，和**SQLTablePrivileges**。|  
|206|使用 ODBC 函数而不是 SQL 语句来执行其他数据库操作的调用**SQLBulkOperations**与 SQL_ADD，或**SQLSetPos**与 SQL_DELETE 或 SQL_UPDATE。 (以便调用支持**SQLSetPos**与*LockType*自变量设置为 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不属于的一致性级别，但是一项可选功能。)|  
|207|启用异步执行指定的个别语句 ODBC 函数。|  
|208|通过调用获取 SQL_ROWVER 行标识列的表， **SQLSpecialColumns**。 (有关详细信息，请参阅支持**SQLSpecialColumns**与*IdentifierType*参数设置为 SQL_BEST_ROWID 因为具备功能 20 在[核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|设置为 SQL_CONCUR_READ_ONLY 以外的至少一个值的 SQL_ATTR_CONCURRENCY 语句属性。|  
|210|超时登录请求和 SQL 查询 （SQL_ATTR_LOGIN_TIMEOUT 和 SQL_ATTR_QUERY_TIMEOUT） 的能力。|  
|211|能够更改默认隔离级别;能够执行"可序列化"的隔离级别的事务。|
