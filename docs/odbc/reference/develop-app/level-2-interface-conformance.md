---
title: 级别 2 接口一致性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff3de6a9b9ec57f1ea96d6db17b9b30c5a22996
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515298"
---
# <a name="level-2-interface-conformance"></a>级别 2 接口一致性
级别 2 接口一致性级别均包含级别 1 接口一致性级别的功能以及下列功能：  
  
|||  
|-|-|  
|201|使用数据库表和视图的三部分组成的名称。 (有关详细信息，请参阅由两部分命名支持中的功能 101[级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)。)|  
|202|描述动态参数，通过调用**SQLDescribeParam**。|  
|203|使用不只输入的参数，但还输出和输入/输出参数和结果值的存储过程。|  
|204|使用书签，包括检索书签，通过调用**SQLDescribeCol**并**SQLColAttribute**列是数字 0; 提取基于一个书签，通过调用**SQLFetchScroll**与*FetchOrientation*参数设置为 SQL_FETCH_BOOKMARK; 和更新、 删除和提取通过书签操作，通过调用**SQLBulkOperations**与*操作*参数设置为 SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK。|  
|205|检索有关的高级信息的数据字典，通过调用**SQLColumnPrivileges**， **SQLForeignKeys**，并**SQLTablePrivileges**。|  
|206|用于 ODBC 函数而不是 SQL 语句执行附加的数据库操作，通过调用**SQLBulkOperations**与 SQL_ADD，或**SQLSetPos** SQL_DELETE 或 SQL_UPDATE。 (支持到调用**SQLSetPos**与*LockType*参数设置为 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不一致性级别的一部分，而是一项可选功能。)|  
|207|启用异步执行指定的单个语句的 ODBC 函数。|  
|208|获取 SQL_ROWVER 行标识列的表，通过调用**SQLSpecialColumns**。 (有关详细信息，请参见的支持**SQLSpecialColumns**与*IdentifierType*参数设置为 SQL_BEST_ROWID 如功能中的 20[核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|Sql_attr_concurrency 设置语句属性设置为 SQL_CONCUR_READ_ONLY 以外的至少一个值。|  
|210|超时时间登录请求和 SQL 查询 （SQL_ATTR_LOGIN_TIMEOUT 和 SQL_ATTR_QUERY_TIMEOUT） 功能。|  
|211|能够更改默认隔离级别;执行具有"可序列化"的隔离级别的事务的功能。|
