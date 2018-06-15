---
title: 目录和架构使用情况 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 0aa8e5c112bbd3bc807ecba821da2e754016b23a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907242"
---
# <a name="catalog-and-schema-usage"></a>目录和架构使用情况
数据源不一定支持目录和架构名称作为所有 SQL 语句中的对象名称标识符。 数据源可能支持目录和架构名称在一个或多个 SQL 语句的以下类： 数据操作语言 (DML) 语句，过程调用，表定义语句、 索引定义语句和权限定义语句。 若要确定哪些目录和架构名称可用于 SQL 语句的类，应用程序调用**SQLGetInfo**使用 SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 选项。
