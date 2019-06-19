---
title: 数据源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb02dd54ea57af668e56fe910ca92830fb09c418
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186281"
---
# <a name="data-sources"></a>“数据源”
一个*数据源*是只需的数据源。 它可以是文件，DBMS 或甚至实时数据源上的特定数据库。 数据可能不位于该程序，在同一台计算机上，也可以在网络上的某个位置的另一台计算机上。 例如，数据源可能是由 Novell® Netware; 访问 OS/2® 操作系统系统上运行 Oracle DBMS通过网关; 访问 IBM DB2 DBMS服务器目录，则在 Xbase 文件的集合或本地的 Microsoft® Access 数据库文件。  
  
 数据源的用途是放置到单一位置收集所有所需访问-驱动程序名称、 网络地址、 网络软件等的数据的技术信息并将其隐藏从用户。 用户应该可以查看包含工资单、 清单和人员的列表，从列表中，选择工资单并让应用程序连接到的工资数据，所有这些操作都无需知道的工资数据所在的位置或应用程序是如何做到到它。  
  
 术语*数据源*不应与类似的条件相混淆。 在此手册*DBMS*或*数据库*是指数据库程序或引擎。 之间进行进一步的区别*桌面数据库*旨在在个人计算机上运行和完整的 SQL 和事务支持，通常存在不足和*server 数据库*设计为运行中客户端 /服务器的情况和特征是一个独立的数据库引擎和丰富的 SQL 和事务支持。 *数据库*还引用特定集合的数据，例如 SQL Server 上的 Xbase 文件目录或数据库中的集合。 它通常相当于术语*目录，* 此手动或一词中其他位置使用*限定符*在早期版本的 ODBC。  
  
 本部分包含以下主题。  
  
-   [数据源的类型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用数据源](../../odbc/reference/using-data-sources.md)  
  
-   [数据源示例](../../odbc/reference/data-source-example.md)
