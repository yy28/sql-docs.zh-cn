---
title: 什么是 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bda4abf9802bd58e81f35bd4223b28f687e89b4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951796"
---
# <a name="what-is-odbc"></a>什么是 ODBC？
许多有关 ODBC 的误解在计算世界中存在。 对于最终用户，它是 Microsoft® Windows®控制面板中的一个图标。 对于应用程序程序员而言，它是包含数据访问例程的库。 对许多人来说，这是所有数据库访问问题的答案。  
  
 首先，ODBC 是数据库 API 的规范。 此 API 独立于任何一个 DBMS 或操作系统;尽管本手册使用 C，但 ODBC API 是独立于语言的。 ODBC API 基于开放组和 ISO/IEC 中的 CLI 规范。 ODBC 3。*x*完全实现了这两个规范-早期版本的 ODBC 基于这些规范的初始版本，但未完全实现它们，并添加了基于屏幕的数据库应用程序开发人员通常需要的功能，如可滚动游标。  
  
 ODBC API 中的函数是由 DBMS 特定驱动程序的开发人员实现的。 应用程序调用这些驱动程序中的函数以与 DBMS 无关的方式访问数据。 驱动程序管理器管理应用程序与驱动程序之间的通信。  
  
 虽然 Microsoft 为运行 Microsoft Windows®95及更高版本的计算机提供了驱动程序管理器，但编写了多个 ODBC 驱动程序，并从其某些应用程序调用了 ODBC 函数，但任何人都可以编写 ODBC 应用程序和驱动程序 事实上，当今可用的绝大部分 ODBC 应用程序和驱动程序都是由 Microsoft 以外的公司编写的。 此外，ODBC 驱动程序和应用程序存在于 Macintosh®和多种 UNIX 平台上。  
  
 为帮助应用程序和驱动程序开发人员，Microsoft 为运行 Windows 95 和更高版本的计算机提供了一个 ODBC 软件开发工具包（SDK），其中提供了驱动程序管理器、安装程序 DLL、测试工具和示例应用程序。 Microsoft 与 Visigenic 软件组合在一起，将这些 Sdk 移植到 Macintosh 和各种 UNIX 平台。  
  
 必须了解，ODBC 旨在公开数据库功能，而不是对其进行补充。 因此，应用程序编写者不应指望使用 ODBC 会突然将简单数据库转换为功能完备的关系数据库引擎。 驱动程序编写器和驱动程序编写器都不需要实现在基础数据库中找不到的功能。 但这种情况的一个例外是，编写直接访问文件数据的驱动程序的开发人员（如 Xbase 文件中的数据）需要编写至少支持最少 SQL 功能的数据库引擎。 另一种例外情况是，Windows SDK 的 ODBC 组件（以前包含在 Microsoft 数据访问组件（MDAC） SDK 中）提供了一个游标库，用于模拟实现某一级别功能的驱动程序的可滚动游标。  
  
 使用 ODBC 的应用程序负责任何跨数据库功能。 例如，ODBC 不是异类联接引擎，也不是分布式事务处理处理器。 但是，因为它与 DBMS 无关，所以它可用于生成此类跨数据库工具。
