---
title: "目录和架构使用情况 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 217f68d674dc7099b741e77d287ca81fcc2688e5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-and-schema-usage"></a>目录和架构使用情况
数据源不一定支持目录和架构名称作为所有 SQL 语句中的对象名称标识符。 数据源可能支持目录和架构名称在一个或多个 SQL 语句的以下类： 数据操作语言 (DML) 语句，过程调用，表定义语句、 索引定义语句和权限定义语句。 若要确定哪些目录和架构名称可用于 SQL 语句的类，应用程序调用**SQLGetInfo**使用 SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 选项。

