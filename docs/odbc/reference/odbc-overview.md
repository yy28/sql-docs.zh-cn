---
title: ODBC 概述 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298287"
---
# <a name="odbc-overview"></a>ODBC 概述
开放式数据库连接 (ODBC) 是一种广泛接受的应用程序编程接口 (API)，适用于数据库访问。 它基于开放组和 ISO/IEC 的数据库 API 的呼叫级接口 （CLI） 规范，并使用结构化查询语言 （SQL） 作为其数据库访问语言。  
  
 ODBC 旨在实现最大的*互操作性*，即单个应用程序能够使用相同的源代码访问不同的数据库管理系统 （DBMS）。 数据库应用程序调用 ODBC 接口中的函数，这些函数在称为*驱动程序*的特定于数据库的模块中实现。 使用驱动程序将应用程序与特定于数据库的调用隔离开来，就像打印机驱动程序将字处理程序与特定于打印机的命令隔离一样。 由于驱动程序在运行时加载，因此用户只需添加新驱动程序才能访问新的 DBMS;因此，用户只需添加新驱动程序，用户就只需添加新驱动程序，用户就只需添加新的 DBMS。无需重新编译或重新链接应用程序。  
  
 本部分包含以下主题。  
  
-   [为何创建 ODBC？](../../odbc/reference/why-was-odbc-created.md)  
  
-   [什么是 ODBC？](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 和标准 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
