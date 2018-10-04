---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 782dec08b76a9e5a97719d6af39e2c30c0f92d19
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797385"
---
# <a name="schema-views"></a>架构视图
应用程序可以在通过调用 ODBC 目录函数或通过使用 INFORMATION_SCHEMA 视图从 DBMS 检索元数据信息。 ANSI SQL-92 标准定义这些视图。  
  
 如果支持 DBMS 和驱动程序，INFORMATION_SCHEMA 视图将提供更强大、 最全面比 ODBC 目录函数提供检索元数据的方式。 应用程序可以执行其自己的自定义**选择**根据中的这些视图中，一个语句可以加入视图，或可以在视图上执行联合。 提供更高版本的实用工具和广泛的元数据，同时不通常支持 INFORMATION_SCHEMA 视图由 DBMS。 这可能会更改为多个 Dbms 和驱动程序实现与 SQL-92 符合性。  
  
 若要确定支持的视图，应用程序调用**SQLGetInfo** SQL_INFO_SCHEMA_VIEWS 选项。 若要从受支持的视图中检索元数据，应用程序执行**选择**语句，用于指定所需的架构信息。
