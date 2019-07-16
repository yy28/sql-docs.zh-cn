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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951796"
---
# <a name="what-is-odbc"></a>什么是 ODBC？
在对计算世界中存在有关 ODBC 的许多误解。 向最终用户，它是 Microsoft® Windows® 控制面板中的图标。 应用程序程序员来说，它是一个库，包含数据访问例程。 许多其他是出人意料的所有数据库访问权限问题的答案。  
  
 首先，这一 ODBC 是数据库 API 的规范。 此 API 是独立于任何一个 DBMS 或操作系统;尽管此手动使用 C，但 ODBC API 与语言无关。 ODBC API 基于从 Open Group 和 ISO/IEC CLI 规范。 ODBC 3。*x*完全同时这些规范的早期版本的 ODBC 基于这些规范的预备版本，但未完全实现它们的实现，并添加基于屏幕的开发人员经常需要的功能数据库应用程序，如可滚动游标。  
  
 在 ODBC API 函数由特定于 DBMS 的驱动程序的开发人员实现。 应用程序调用这些驱动程序以访问独立于 DBMS 的方式中的数据中的函数。 驱动程序管理器管理应用程序和驱动程序之间的通信。  
  
 尽管 Microsoft 为计算机运行 Microsoft Windows® 95 提供了驱动程序管理器和更高版本，撰写了多个 ODBC 驱动程序和调用 ODBC 函数从其应用程序的一些，但任何人都可以编写 ODBC 应用程序和驱动程序。 事实上，ODBC 应用程序和驱动程序可用的大多数今天编写的 Microsoft 以外的公司。 此外，ODBC 驱动程序和应用程序存在 Macintosh® 和多种 UNIX 平台上。  
  
 为帮助应用程序和驱动程序开发人员，Microsoft 提供 ODBC 软件开发工具包 (SDK) 的计算机运行 Windows 95 和更高版本，它提供的驱动程序管理器中，安装程序 DLL，测试工具和示例应用程序。 Microsoft 合作 Visigenic 软件移植这些 Macintosh 和多种 UNIX 平台的 Sdk。  
  
 请务必了解 ODBC 用于公开数据库功能，未对其进行补充。 因此，应用程序编写器不应期望，使用 ODBC 会突然将一个简单的数据库转换为完备的关系型数据库引擎。 也不驱动程序编写人员应实现基础数据库中找不到的功能。 一种例外是编写直接访问文件数据 （如 Xbase 文件中的数据） 的驱动程序的开发人员所需编写的数据库引擎，支持至少最小 SQL 功能。 另一个例外是，以前包含在 Microsoft 数据访问组件 (MDAC) SDK 的 Windows SDK 的 ODBC 组件，提供了一个模拟实现某些级别的功能的驱动程序的可滚动游标的游标库。  
  
 使用 ODBC 的应用程序负责跨数据库的任何功能。 例如，ODBC 不异类联接引擎，也不是分布式的事务处理器。 但是，因为它是独立于 DBMS 的它可以用于构建此类跨数据库的工具。
