---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84c870d45cc487fc9ec5497e43b764bd4187d2f6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721245"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目录函数
ODBC 包含以下目录函数：  
  
|函数|Description|  
|--------------|-----------------|  
|**SQLTables**|返回数据源中的目录、 架构、 表或表类型的列表。|  
|**SQLColumns**|一个或多个表中返回的列的列表。|  
|**SQLStatistics**|返回有关单个表的统计信息的列表。 也会返回一系列与该表相关联的索引。|  
|**SQLSpecialColumns**|返回唯一标识单个表中的行的列的列表。 此外会自动更新此表中返回的列的列表。|  
|**SQLPrimaryKeys**|返回构成单个表的主键列的列表。|  
|**SQLForeignKeys**|在单个表或单个表引用其他表中的外键的列表中返回外键的列表。|  
|**SQLTablePrivileges**|返回与一个或多个表关联的特权的列表。|  
|**SQLColumnPrivileges**|返回一个表中的一个或多个列与关联的特权的列表。|  
|**SQLProcedures**|返回数据源中的过程的列表。|  
|**SQLProcedureColumns**|在结果集中的单个过程返回输入和输出参数、 返回值和列的列表。|  
|**SQLGetTypeInfo**|返回数据源支持的 SQL 数据类型的列表。 在通常使用这些数据类型**CREATE TABLE**并**ALTER TABLE**语句。|  
  
 因为**SQLTables**， **SQLColumns**， **SQLStatistics**，以及**SQLSpecialColumns**符合开放组 CLI 和**SQLGetTypeInfo**符合 ISO 92 CLI，它们实现大多数驱动程序。 剩余的目录函数是在 ODBC 一致性级别中。  
  
 本部分包含以下主题。  
  
-   [目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目录函数中的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [架构视图](../../../odbc/reference/develop-app/schema-views.md)
