---
title: 什么是 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eed93c1d5b096e132f6d514057abd73c090519c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="what-is-odbc"></a>什么是 ODBC？
有关 ODBC 的许多错误理解中计算都存在。 向最终用户，它是 Microsoft® Windows® 控制面板中的图标。 对应用程序程序员，它是包含数据访问例程的库。 多个其他很出人意料的所有数据库访问权限问题的答案。  
  
 首先，最重要，ODBC 是数据库 API 的规范。 此 API 是独立于任何一个 DBMS 或操作系统;尽管本手册使用 C，ODBC API 是独立于语言的。 ODBC API 基于从 Open Group 和 ISO/IEC 的 CLI 规范。 ODBC 3。*x*完全实现这两个这些规范 — 早期版本的 ODBC 基于这些规范的初步版本，但未完全实现它们-，并添加基于屏幕的开发人员经常需要的功能数据库应用程序，如可滚动游标。  
  
 在 ODBC API 函数的实现是由特定于 DBMS 的驱动程序的开发人员。 应用程序在这些驱动程序以访问数据以独立于 DBMS 的方式调用的函数。 驱动程序管理器管理应用程序和驱动程序之间的通信。  
  
 尽管 Microsoft 为计算机运行 Microsoft Windows® 95 提供驱动程序管理器和更高版本，编写多个 ODBC 驱动程序，以及调用 ODBC 函数来自某些及其应用程序，任何人都可以编写 ODBC 应用程序和驱动程序。 事实上，大多数 ODBC 应用程序和驱动程序可用当今的编写由 Microsoft 之外的其他公司。 此外，ODBC 驱动程序和应用程序存在于 Macintosh® 和多种 UNIX 平台。  
  
 为了帮助应用程序和驱动程序的开发人员，Microsoft 提供了 ODBC 软件开发工具包 (SDK) 的计算机运行 Windows 95 和更高版本，它提供的驱动程序管理器，安装程序 DLL，测试工具和示例应用程序。 Microsoft 已使用 Visigenic 软件移植这些 Sdk Macintosh 和 UNIX 平台的各种组合。  
  
 请务必了解 ODBC 旨在公开数据库功能，不进行补充。 因此，应用程序编写器不应指望，使用 ODBC 会突然将一个简单的数据库转换为完备的关系数据库引擎。 也不驱动程序编写人员应实现基础数据库中找不到的功能。 与此异常是编写直接访问文件数据 （例如 Xbase 文件中的数据） 的驱动程序的开发人员所需编写支持至少最小的 SQL 功能的数据库引擎。 另一种例外是，以前包含在 Microsoft 数据访问组件 (MDAC) SDK 的 Windows sdk 的 ODBC 组件，提供了一个模拟驱动程序实现特定级别的功能的可滚动游标的光标库。  
  
 使用 ODBC 应用程序负责跨数据库的任何功能。 例如，ODBC 不是异类联接引擎，也不是分布式的事务处理器。 但是，因为它是独立于 DBMS 的它可以用于生成此类跨数据库工具。
