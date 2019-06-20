---
title: DDL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9100405c91387faa66b714a94b8259167ae31899
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267663"
---
# <a name="ddl-statements"></a>DDL 语句
数据定义语言 (DDL) 语句在 Dbms 之间有很大差异。 ODBC SQL 定义语句的最常见的数据定义操作： 创建和删除表、 索引和视图。更改表;和授予和撤消权限。 所有其他 DDL 语句是特定于源的数据。 因此，可互操作应用程序不能执行一些数据定义操作。 一般情况下，这并不是问题，因为此类操作往往是高度特定于 DBMS 的和最左侧的专有数据库管理软件附带的大多数 Dbms 或安装程序附带的驱动程序。  
  
 数据定义中的另一个问题是该数据类型名称在 Dbms 之间有很大差异。 而不是定义标准数据类型名称和强制驱动程序，以将其转换为特定于 DBMS 的名称**SQLGetTypeInfo**提供应用程序发现特定于 DBMS 的数据类型名称的方法。 可互操作应用程序应使用这些名称在 SQL 语句中创建和更改的表;中列出的名称[附录 c:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，和[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)，仅为示例。
