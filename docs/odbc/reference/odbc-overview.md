---
title: ODBC 概述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298287"
---
# <a name="odbc-overview"></a>ODBC 概述
开放式数据库连接 (ODBC) 是一种广泛接受的应用程序编程接口 (API)，适用于数据库访问。 它基于开放组中的调用级别接口（CLI）规范以及数据库 Api 的 ISO/IEC，并使用结构化查询语言（SQL）作为其数据库访问语言。  
  
 ODBC 旨在实现最大*互操作性*，即单个应用程序可以使用相同的源代码访问不同的数据库管理系统（dbms）。 数据库应用程序在 ODBC 接口中调用函数，这些函数在名为*驱动程序*的数据库特定模块中实现。 驱动程序的使用将应用程序与数据库特定的调用隔离开来，与打印机驱动程序将 word 处理程序与打印机特定的命令隔离的方式相同。 由于驱动程序在运行时加载，因此用户只需要添加新的驱动程序来访问新 DBMS;无需重新编译或重新链接应用程序。  
  
 本部分包含以下主题。  
  
-   [为何创建 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什么是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和标准 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
