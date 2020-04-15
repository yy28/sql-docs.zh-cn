---
title: 架构视图 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304248"
---
# <a name="schema-views"></a>架构视图
应用程序可以通过调用 ODBC 目录函数或使用INFORMATION_SCHEMA视图从 DBMS 检索元数据信息。 视图由 ANSI SQL-92 标准定义。  
  
 如果 DBMS 和驱动程序支持，INFORMATION_SCHEMA视图提供了比 ODBC 目录函数提供的更强大、更全面的检索元数据的方法。 应用程序可以针对这些视图之一执行其自己的自定义**SELECT**语句，可以联接视图，也可以对视图执行联合。 虽然提供更大的实用程序和更广泛的元数据，但 DBMS 通常不支持INFORMATION_SCHEMA视图。 随着更多 DBMS 和驱动程序符合 SQL-92，这种情况可能会发生变化。  
  
 要确定哪些视图受支持，应用程序使用SQL_INFO_SCHEMA_VIEWS选项调用**SQLGetInfo。** 若要从受支持的视图检索元数据，应用程序将执行**SELECT**语句，指定所需的架构信息。
