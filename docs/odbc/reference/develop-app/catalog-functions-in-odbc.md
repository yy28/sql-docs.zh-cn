---
title: ODBC 中的目录功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6731018b99f2f3043e48ee7c174a08cb9ef71fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306228"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目录函数
ODBC 包含以下目录函数：  
  
|函数|说明|  
|--------------|-----------------|  
|**SQLTables**|返回数据源中的目录、架构、表或表类型的列表。|  
|**SQLColumns**|返回一个或多个表中的列列表。|  
|**SQLStatistics**|返回有关单个表的统计信息列表。 还会返回与该表关联的索引列表。|  
|**SQLSpecialColumns**|返回唯一标识单个表中的行的列列表。 还会返回该表中自动更新的列的列表。|  
|**SQLPrimaryKeys**|返回组成单个表的主键的列列表。|  
|**SQLForeignKeys**|返回单个表中的外键列表或引用单个表的其他表中的外键列表。|  
|**SQLTablePrivileges**|返回与一个或多个表关联的权限列表。|  
|**SQLColumnPrivileges**|返回与单个表中的一个或多个列关联的权限列表。|  
|**SQLProcedures**|返回数据源中的过程列表。|  
|**SQLProcedureColumns**|返回单个过程的结果集中的输入和输出参数、返回值和列的列表。|  
|**SQLGetTypeInfo**|返回数据源支持的 SQL 数据类型的列表。 这些数据类型通常用于**创建表**和**ALTER TABLE**语句。|  
  
 由于**SQLTables、SQLColumns、SQL****统计**和**SQL 特别列**符合开放组 CLI，并且**SQLGetTypeInfo**符合 ISO 92 CLI，因此大多数驱动程序都实现了它们。 **SQLTables** 其余目录函数处于 ODBC 一致性级别。  
  
 本部分包含以下主题。  
  
-   [目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目录函数中的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [架构视图](../../../odbc/reference/develop-app/schema-views.md)
