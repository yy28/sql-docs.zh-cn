---
title: 目录中 ODBC 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7297b87ec5ce8bdbf706fa35b5ebef6ba580a49e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目录函数
ODBC 包含以下目录函数：  
  
|函数|Description|  
|--------------|-----------------|  
|**SQLTables**|返回数据源中的目录、 架构、 表或表类型的列表。|  
|**SQLColumns**|一个或多个表中返回的列的列表。|  
|**SQLStatistics**|返回有关单个表的统计信息列表。 也会返回与该表关联的索引的列表。|  
|**SQLSpecialColumns**|返回唯一标识单个表中的行的列的列表。 此外会自动更新该表中返回的列的列表。|  
|**SQLPrimaryKeys**|返回构成单个表的主键的列的列表。|  
|**SQLForeignKeys**|单个表或单个表引用其他表中的外键的列表中返回外键的列表。|  
|**SQLTablePrivileges**|返回与一个或多个表相关联的特权的列表。|  
|**SQLColumnPrivileges**|返回一个表中的一个或多个列相关联的特权的列表。|  
|**SQLProcedures**|返回数据源中的过程的列表。|  
|**SQLProcedureColumns**|在单一过程的结果集中返回输入和输出参数、 返回值和列的列表。|  
|**SQLGetTypeInfo**|返回数据源支持的 SQL 数据类型的列表。 这些数据类型通常用在**CREATE TABLE**和**ALTER TABLE**语句。|  
  
 因为**SQLTables**， **SQLColumns**， **SQLStatistics**，和**SQLSpecialColumns**遵循打开组 CLI 和**SQLGetTypeInfo**符合 ISO 92 CLI，它们实现大多数驱动程序。 剩余的目录函数位于 ODBC 一致性级别。  
  
 本部分包含以下主题。  
  
-   [目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目录函数中的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [架构视图](../../../odbc/reference/develop-app/schema-views.md)
