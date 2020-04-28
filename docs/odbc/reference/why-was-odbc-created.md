---
title: 为何创建 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22173b0ad3dd8abf2d168b41a16a03bc414022ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302778"
---
# <a name="why-was-odbc-created"></a>为何创建 ODBC？
过去，公司使用了单个 DBMS。 所有数据库访问都是通过该系统的前端或通过编写的应用程序来完成的，以独占方式使用该系统。 但是，随着计算机的使用增长，计算机硬件和软件的使用越来越多，公司开始获取不同的 Dbms。 原因有很多：人们买到了什么是最便宜的，哪些是最快的、他们知道了哪些是最新的，哪些是最新的应用程序。 其他原因是重组和合并，其中先前拥有单个 DBMS 的部门现在有多个。  
  
 随着个人计算机的出现，该问题的增长更复杂。 这些计算机提供了一系列用于查询、分析和显示数据的工具，以及一些廉价、易于使用的数据库。 从那开始，单个公司通常会将数据分散到无数个不同的数据库中，存储在各种不兼容的数据库中，并通过大量不同的工具进行访问，其中很少有这些工具可以获取所有数据。  
  
 最终的挑战在于客户端/服务器计算的出现，旨在充分利用计算机资源。 廉价的个人计算机（客户端）位于桌面上，同时为数据提供图形前端和大量廉价工具，如电子表格、图表程序和报表生成器。 Minicomputers 和大型机（服务器）宿主 Dbms，用户可在其中使用其计算能力和中心位置来提供快速、协调的数据访问。 那么，如何将前端软件连接到后端数据库？  
  
 类似于独立软件供应商（Isv）的问题。 对于为 minicomputers 和大型机编写数据库软件的供应商，通常强制为每个 DBMS 编写一个版本的应用程序，或者为他们要访问的每个 DBMS 编写 DBMS 特定的代码。 为个人计算机编写软件的供应商必须为要使用的每个不同 DBMS 编写数据访问例程。 这通常意味着编写和维护数据访问例程（而不是应用程序）所用的资源量很大，并且应用程序通常不会在其质量上销售，而是可以访问给定 DBMS 中的数据。  
  
 这两组开发人员都需要一种方法来访问不同 Dbms 中的数据。 大型机和 minicomputer 组需要一种在单个应用程序中合并来自不同 Dbms 的数据的方式，而个人计算机组则需要此功能以及一种方式来编写独立于任何一个 DBMS 的单一应用程序。 简而言之，两个组都需要一个可互操作的方式来访问数据;它们需要开放式数据库连接。
