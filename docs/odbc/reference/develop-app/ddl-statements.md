---
title: DDL 语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302988"
---
# <a name="ddl-statements"></a>DDL 语句
数据定义语言 （DDL） 语句在 DBMS 之间差异很大。 ODBC SQL 为最常见的数据定义操作定义语句：创建和删除表、索引和视图;更改表;授予和撤销特权。 所有其他 DDL 语句都是特定于数据源的。 因此，可互操作的应用程序无法执行某些数据定义操作。 通常，这不是问题，因为此类操作往往高度特定于 DBMS，最好留给大多数 DBMS 附带的专有数据库管理软件或驱动程序附带的安装程序。  
  
 数据定义中的另一个问题是数据类型名称在 DBMS 之间差异很大。 **SQLGetTypeInfo**不是定义标准数据类型名称，而是强制驱动程序将其转换为特定于 DBMS 的名称，而是为应用程序提供了一种发现特定于 DBMS 的数据类型名称的方法。 可互操作的应用程序应在 SQL 语句中使用这些名称来创建和更改表;附录 C[中列出的名称：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)和附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)仅是示例。
