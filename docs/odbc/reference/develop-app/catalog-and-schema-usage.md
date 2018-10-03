---
title: 目录和架构使用情况 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9476f4f928890514354f97ce604f871bd8a06d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702825"
---
# <a name="catalog-and-schema-usage"></a>目录和架构使用情况
数据源不一定支持目录和架构名称作为所有 SQL 语句中的对象名称标识符。 数据源可能支持目录和架构名称在一个或多个 SQL 语句的以下类： 数据操作语言 (DML) 语句、 过程调用中，表定义语句、 索引定义语句和权限定义语句。 若要确定名称可以使用哪些目录和架构中的 SQL 语句的类，应用程序调用**SQLGetInfo** SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 选项。
