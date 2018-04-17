---
title: 数据源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b16699f67a74232730b2b96a2fdeeb4545d1fe46
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-sources"></a>数据源
A*数据源*是只需数据源。 它可以是文件，DBMS 或甚至实时数据源上的特定数据库。 数据可能位于与该程序，在同一计算机上，也可以在网络上的某个位置的另一台计算机上。 例如，数据源可能是由 Novell® Netware; 访问 OS/2® 操作系统系统上运行 Oracle DBMS访问通过网关; IBM DB2 DBMS中的服务器目录中; Xbase 文件的集合或本地的 Microsoft® Access 数据库文件。  
  
 数据源的用途是收集所有所需访问数据的技术信息 — 驱动程序名称、 网络地址、 网络软件等-到单个放置和隐藏用户。 用户应能够查看包含工资单、 清单和人员的列表，从列表中，选择工资单并将所有这些操作都无需知道工资单数据所在的位置，或如何应用程序是怎样到达它连接到的工资单数据，该应用程序。  
  
 术语*数据源*不应与类似的条件相混淆。 本手册中*DBMS*或*数据库*指数据库程序或引擎。 之间进行了进一步区分*桌面数据库*旨在个人计算机上运行和通常在完整的 SQL 和事务支持，缺少和*server 数据库*设计为在客户端中运行 /服务器的情况和特征是独立的数据库引擎和丰富的 SQL 和事务支持。 *数据库*还指特定集合的数据，如 SQL Server 上的 Xbase 文件目录或数据库中的集合。 它通常相当于术语*目录，*本手册或术语中的其他位置使用*限定符*在早期版本的 ODBC。  
  
 本部分包含以下主题。  
  
-   [数据源的类型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用数据源](../../odbc/reference/using-data-sources.md)  
  
-   [数据源示例](../../odbc/reference/data-source-example.md)
