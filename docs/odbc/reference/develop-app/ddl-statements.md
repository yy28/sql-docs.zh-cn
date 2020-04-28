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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302988"
---
# <a name="ddl-statements"></a>DDL 语句
数据定义语言（DDL）语句在 Dbms 上有很大的差别。 ODBC SQL 为最常见的数据定义操作定义语句：创建和删除表、索引和视图;更改表;并授予和撤消权限。 所有其他 DDL 语句都是特定于数据源的。 因此，可互操作的应用程序无法执行某些数据定义操作。 通常，这并不是一个问题，因为此类操作往往是非常具体的 DBMS，并最好留给大多数 Dbms 附带的专有数据库管理软件或驱动程序随附的安装程序。  
  
 数据定义中的另一个问题是，Dbms 中的数据类型名称不同。 **SQLGetTypeInfo**为应用程序提供了一种方法来发现 dbms 特定的数据类型名称，而不是定义标准数据类型名称并强制驱动程序将其转换为 dbms 特定的名称。 可互操作的应用程序应在 SQL 语句中使用这些名称来创建和更改表;[附录 C： SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)和[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)中列出的名称只是示例。
