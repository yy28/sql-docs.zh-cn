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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286497"
---
# <a name="what-is-odbc"></a>什么是 ODBC？
计算领域存在许多关于ODBC的误解。 对于最终用户，它是 Microsoft ® Windows ®控制面板中的图标。 对于应用程序程序员来说，它是一个包含数据访问例程的库。 对许多其他人来说，这是所有数据库访问问题的答案。  
  
 首先，ODBC 是数据库 API 的规范。 此 API 独立于任何一个 DBMS 或操作系统;尽管本手册使用 C，但 ODBC API 与语言无关。 ODBC API 基于开放组和 ISO/IEC 的 CLI 规范。 ODBC 3.*x*完全实现这两种规范 - 早期版本的 ODBC 基于这些规范的初步版本，但没有完全实现它们 - 并添加了基于屏幕的数据库应用程序的开发人员通常需要的功能，例如可滚动的游标。  
  
 ODBC API 中的函数由特定于 DBMS 的驱动程序的开发人员实现。 应用程序调用这些驱动程序中的函数以独立于 DBMS 的方式访问数据。 驱动程序管理器管理应用程序和驱动程序之间的通信。  
  
 尽管 Microsoft 为运行 Microsoft Windows 的计算机提供了驱动程序管理器® 95 及更高版本，但已编写了多个 ODBC 驱动程序，并从某些应用程序中调用 ODBC 函数，但任何人都可以编写 ODBC 应用程序和驱动程序。 事实上，目前提供的绝大多数 ODBC 应用程序和驱动程序是由微软以外的公司编写的。 此外，ODBC 的驱动程序和应用程序存在于 Macintosh ®和各种 UNIX 平台上。  
  
 为了帮助应用程序和驱动程序开发人员，Microsoft 为运行 Windows 95 及更高版本的计算机提供了一个 ODBC 软件开发工具包 （SDK），该工具包提供驱动程序管理器、安装程序 DLL、测试工具和示例应用程序。 微软与Visigenic软件公司合作，将这些 SDK 移植到 Macintosh 和各种 UNIX 平台。  
  
 请务必了解，ODBC 旨在公开数据库功能，而不是补充它们。 因此，应用程序编写者不应期望使用 ODBC 会突然将简单数据库转换为功能齐全的关系数据库引擎。 驱动程序编写器也不期望实现基础数据库中找不到的功能。 例外情况是，编写直接访问文件数据的驱动程序（如 Xbase 文件中的数据）的开发人员需要编写至少支持最少 SQL 功能的数据库引擎。 另一个例外是，以前包含在 Microsoft 数据访问组件 （MDAC） SDK 中的 Windows SDK 的 ODBC 组件提供了一个游标库，用于模拟实现特定级别功能的驱动程序的可滚动游标。  
  
 使用 ODBC 的应用程序负责任何跨数据库功能。 例如，ODBC 不是异构联接引擎，也不是分布式事务处理器。 但是，由于它与 DBMS 无关，因此可用于构建此类跨数据库工具。
