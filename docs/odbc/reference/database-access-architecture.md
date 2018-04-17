---
title: 数据库访问体系结构 |Microsoft 文档
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
- ODBC [ODBC], database access
- standardizing database access [ODBC], about standardizing
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC]
ms.assetid: 3811599f-48cb-4205-9fe5-5ab4b240047d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba4fd8fac85087765b8f95f916bb737862a5d308
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="database-access-architecture"></a>数据库访问体系结构
ODBC 开发中的问题之一就是标准化的数据库访问体系结构的哪个部分。 编程接口上一节中所述的 SQL-嵌入式 SQL，SQL 模块和 Cli — 只有一个属于此体系结构。 事实上，因为 ODBC 主要用于连接到小型计算机和大型机 Dbms 基于个人计算机的应用程序，还有大量的网络组件，无法采用其中一些进行标准化。  
  
 本部分包含以下主题。  
  
-   [网络数据库访问权限](../../odbc/reference/network-database-access.md)  
  
-   [标准数据库访问体系结构](../../odbc/reference/standard-database-access-architectures.md)  
  
-   [ODBC 解决方案](../../odbc/reference/the-odbc-solution.md)
