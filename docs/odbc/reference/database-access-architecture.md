---
title: 数据库访问体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- standardizing database access [ODBC], about standardizing
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC]
ms.assetid: 3811599f-48cb-4205-9fe5-5ab4b240047d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42fc1d3880e01c435e7991fb5781d0f815a83db5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612286"
---
# <a name="database-access-architecture"></a>数据库访问体系结构
ODBC 的开发中的问题之一是数据库访问体系结构进行标准化的哪个部分。 编程接口上一节中所述的 SQL-嵌入式 SQL，SQL 模块和 Cli — 只有一个属于此体系结构。 事实上，因为 ODBC 主要用于基于个人计算机的应用程序连接到小型计算机和大型机 Dbms，还有多个网络组件，其中一些无法进行标准化。  
  
 本部分包含以下主题。  
  
-   [网络数据库访问权限](../../odbc/reference/network-database-access.md)  
  
-   [标准数据库访问体系结构](../../odbc/reference/standard-database-access-architectures.md)  
  
-   [ODBC 解决方案](../../odbc/reference/the-odbc-solution.md)
