---
title: "ODBC 概述 |Microsoft 文档"
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
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20767544a83219c6583eaf03a78e240e15e19be2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-overview"></a>ODBC 概述
开放式数据库连接 (ODBC) 是数据库访问被广泛接受的应用程序编程接口 (API)。 它基于从 Open Group 和 ISO/IEC 的数据库 Api 的调用级界面 (CLI) 规范，并使用结构化查询语言 (SQL) 作为其数据库访问语言。  
  
 ODBC 旨在最大*互操作性*-，即访问相同的源代码的不同的数据库管理系统 (Dbms) 的单个应用程序的能力。 数据库应用程序调用 ODBC 接口，这在称为特定于数据库的模块中实现的函数*驱动程序*。 使用驱动程序将从数据库特定调用的应用程序隔离与打印机驱动程序隔离来自特定于打印机的命令的文字处理程序的方式相同。 用户在运行时加载驱动程序，因为仅有要添加新的驱动程序，以访问新的 DBMS;不需要重新编译或重新链接应用程序。  
  
 本部分包含以下主题。  
  
-   [为什么创建 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什么是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和标准 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
