---
description: 架构视图
title: 架构视图 |Microsoft Docs
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
ms.openlocfilehash: 34e1b52b5e96b5fedb964e53f14a7b554d12aa05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429069"
---
# <a name="schema-views"></a>架构视图
应用程序可以通过调用 ODBC 目录函数或使用 INFORMATION_SCHEMA 视图，从 DBMS 检索元数据信息。 视图由 ANSI SQL-92 标准定义。  
  
 如果 DBMS 和驱动程序支持，则 INFORMATION_SCHEMA 视图提供了一种比 ODBC 目录函数提供的功能更强大、更全面的方法来检索元数据。 应用程序可以对其中一个视图执行其自己的自定义 **SELECT** 语句，可以联接视图，或者可以对视图执行联合。 尽管提供更大的实用工具和更广泛的元数据，但 DBMS 通常不支持 INFORMATION_SCHEMA 视图。 当更多 Dbms 和驱动程序实现与 SQL-92 的符合性时，这可能会发生变化。  
  
 若要确定支持的视图，应用程序需要使用 SQL_INFO_SCHEMA_VIEWS 选项调用 **SQLGetInfo** 。 若要从支持的视图中检索元数据，应用程序将执行一个 **SELECT** 语句，该语句指定所需的架构信息。
