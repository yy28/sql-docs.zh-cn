---
title: "CREATE TABLE 语句中不为 NULL |Microsoft 文档"
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dc96de9df9724e500709488054b3357b3c7e50aa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 语句中不为 NULL
不支持某些数据库和尤其是桌面数据库**NOT NULL**中的列约束**CREATE TABLE**语句。 有关详细信息，请参阅中的 SQL_NON_NULLABLE_COLUMNS 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。

