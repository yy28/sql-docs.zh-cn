---
title: DDL 语句 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61605252563150f4bb957eda14a95c5745650656
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="ddl-statements"></a>DDL 语句
数据定义语言 (DDL) 语句在 Dbms 之间有很大差异。 ODBC SQL 定义语句的最常见的数据定义操作： 创建和删除表、 索引和视图。更改表;授予，并撤消权限。 所有其他 DDL 语句是数据源 – 特定。 因此，可互操作的应用程序无法执行某些数据定义操作。 一般情况下，这不是问题，因为此类操作往往是高度特定于 DBMS，并且最佳从左到专用的数据库管理软件附带大多数 Dbms 或安装程序附带的驱动程序。  
  
 数据定义中的另一个问题是该数据类型名称在 Dbms 之间有很大差异。 而不是定义标准数据类型名称和强制驱动程序以将它们转换为特定于 DBMS 的名称， **SQLGetTypeInfo**提供应用程序能够发现特定于 DBMS 的数据类型名称的方法。 可互操作的应用程序应使用这些名称在 SQL 语句中创建和更改的表;中列出的名称[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，和[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)，仅为示例。
