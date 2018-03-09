---
title: "为什么创建 ODBC？ | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33cc5f63c34618f51196e173e58adbac58377f29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="why-was-odbc-created"></a>为什么创建 ODBC？
从历史上看，公司使用单个 DBMS。 通过该系统的前端或通过编写能够以独占方式使用该系统的应用程序，已完成的所有数据库访问。 但是，使用计算机增长和多个计算机硬件和软件变得可用时，公司将启动以获取不同 Dbms。 之所以许多原因： 用户购买了什么是最便宜，什么是最快，他们已知道，是什么最适合单个应用程序在市场上最新。 其他原因在以前单个 DBMS 的部门现在有几个重组和合并，均。  
  
 问题增长得更加复杂随着的个人计算机。 引入了大量的查询、 分析和显示数据，以及许多价格低廉且易于使用的数据库的工具的这些计算机。 此后，可以在单个企业通常具有数据分散在大量的台式机、 服务器和小型机，存储在多个不兼容的数据库，并且由大量不同的工具，其中的几个能够到达的所有数据的访问。  
  
 最终质询附带的客户端/服务器计算，出现其中试图最有效地使用计算机资源。 成本较低的个人计算机 （客户端） 位于以下位置： 在桌面上和提供这两个图形前端到数据以及大量的成本较低的工具，如电子表格，图表程序和报表生成器。 小型机和大型机计算机 （服务器） 承载的 Dbms，其中他们可以使用其计算能力和中心位置以提供快速、 协调数据访问。 如何然后是前端软件以连接到后端数据库？  
  
 类似的问题时面临独立软件供应商 (Isv)。 编写用于小型机和大型机的数据库软件的供应商通常已强制为每个 DBMS 编写一个版本的应用程序或为他们想要访问每个 DBMS 编写特定于 DBMS 的代码。 编写的个人计算机的软件的供应商必须为每个要工作的不同 DBMS 编写数据访问例程。 这通常意味着编写和维护数据访问例程，而不是应用程序，以及应用程序通常售出不在其质量，而上是否它们可以访问给定的 DBMS 中的数据已花费大量的资源。  
  
 这两组开发人员所需要的是不同 Dbms 中访问数据的方式。 大型机和小型计算机组需要一种方法将数据从单个应用程序中的不同 Dbms 合并时的个人计算机组需要此功能，以及一种编写一个应用程序是独立于任何一个 DBMS 方式。 简单地说，这两个组需要以互操作的方式来访问数据;它们需要开放式数据库连接。
