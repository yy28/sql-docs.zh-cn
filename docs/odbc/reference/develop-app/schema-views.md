---
title: "架构视图 |Microsoft 文档"
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
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06b9546950d5ae84b6ac5811ae4413fa1841c065
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="schema-views"></a>架构视图
通过调用 ODBC 目录函数或通过使用 INFORMATION_SCHEMA 视图，应用程序可以从 DBMS 检索元数据信息。 视图定义由 ANSI sql-92 标准。  
  
 如果支持 DBMS 和驱动程序，INFORMATION_SCHEMA 视图将提供比 ODBC 目录函数提供检索元数据更为强大和全面的方式。 应用程序可以执行其自己的自定义**选择**针对这些视图之一的语句可以加入视图，或可以在视图上执行联合。 同时提供更高版本的实用工具和广泛的元数据，INFORMATION_SCHEMA 视图不通常由 DBMS 支持。 这可能会更改为更多的 Dbms 和驱动程序实现与 sql-92 的法规遵从性。  
  
 若要确定支持的视图，应用程序调用**SQLGetInfo** SQL_INFO_SCHEMA_VIEWS 选项。 若要从支持的视图中检索元数据，应用程序执行**选择**指定所需的架构信息的语句。
