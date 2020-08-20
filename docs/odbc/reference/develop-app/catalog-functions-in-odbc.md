---
description: ODBC 中的目录函数
title: ODBC 中的目录函数 |Microsoft Docs
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
ms.openlocfilehash: b7a34a29e55f6705ccc98e5644096ac6ea7bfd67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465969"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目录函数
ODBC 包含以下目录函数：  
  
|函数|描述|  
|--------------|-----------------|  
|**SQLTables**|返回数据源中的目录、架构、表或表类型的列表。|  
|**SQLColumns**|返回一个或多个表中的列的列表。|  
|**SQLStatistics**|返回有关单个表的统计信息列表。 还返回与该表关联的索引列表。|  
|**SQLSpecialColumns**|返回在单个表中唯一标识行的列的列表。 还返回该表中自动更新的列的列表。|  
|**SQLPrimaryKeys**|返回构成单个表的主键的列的列表。|  
|**SQLForeignKeys**|返回单个表中的外键列表，或引用单个表的其他表中的外键列表。|  
|**SQLTablePrivileges**|返回与一个或多个表关联的特权列表。|  
|**SQLColumnPrivileges**|返回与一个表中的一个或多个列关联的特权列表。|  
|**SQLProcedures**|返回数据源中的过程列表。|  
|**SQLProcedureColumns**|返回单个过程的结果集中的输入和输出参数、返回值和列的列表。|  
|**SQLGetTypeInfo**|返回数据源支持的 SQL 数据类型的列表。 这些数据类型通常在 **CREATE TABLE** 和 **ALTER TABLE** 语句中使用。|  
  
 由于 **SQLTables**、 **SQLColumns**、 **SQLStatistics**和 **SQLSpecialColumns** 符合开放组 CLI，并且 **SQLGetTypeInfo** 符合 ISO 92 cli，因此它们由大多数驱动程序实现。 其余目录函数为 ODBC 一致性级别。  
  
 本部分包含以下主题。  
  
-   [目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目录函数中的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [架构视图](../../../odbc/reference/develop-app/schema-views.md)
