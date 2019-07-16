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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 945ebced0703c109ac64c374e31d2e76b556e7ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944836"
---
# <a name="odbc-overview"></a>ODBC 概述
开放式数据库连接 (ODBC) 是数据库访问权限被广泛接受的应用程序编程接口 (API)。 它基于从 Open Group 和 ISO/IEC 的数据库 Api 的调用级别接口 (CLI) 规范，并作为其数据库访问语言使用结构化查询语言 (SQL)。  
  
 ODBC 专为最大*互操作性*-也就是说，单个应用程序访问其他数据库管理系统 (Dbms) 使用相同的源代码的功能。 数据库应用程序调用 ODBC 接口，这在调用特定于数据库的模块中实现的函数*驱动程序*。 使用驱动程序将从特定于数据库的调用的应用程序隔离打印机驱动程序隔离特定于打印机的命令从文字处理程序的方式相同。 用户在运行时加载驱动程序，因为仅具有要添加新的驱动程序以访问新的 DBMS;不需要重新编译或重新链接应用程序。  
  
 本部分包含以下主题。  
  
-   [为何创建 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什么是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和标准 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
