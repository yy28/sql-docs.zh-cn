---
title: 驱动程序体系结构 |Microsoft 文档
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa23b4a900e0415268746b84b94d68ea8492bbca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="driver-architecture"></a>驱动程序体系结构
驱动程序体系结构划分为两个类别，具体取决于哪些软件进程 SQL 语句：  
  
-   **基于文件的驱动程序**驱动程序直接访问物理数据。 在这种情况下，该驱动程序充当驱动程序和数据源;也就是说，它将处理 ODBC 调用和 SQL 语句。 例如，dBASE 驱动程序是基于文件的驱动程序，因为 dBASE 不提供独立的数据库引擎驱动程序可以使用。 请务必要注意的基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
-   **基于 DBMS 的驱动程序**驱动程序通过单独的数据库引擎访问的物理数据。 在这种情况下，该驱动程序处理仅 ODBC 调用异步方法。它将传递 SQL 语句对数据库引擎处理。 例如，Oracle 驱动程序是基于 DBMS 的驱动程序，因为 Oracle 具有独立的数据库引擎的驱动程序使用。 数据库引擎所在的位置并不重要。 可以驻留在与该驱动程序相同的计算机或网络; 上的不同计算机上它甚至可能通过网关访问。  
  
 驱动程序体系结构是仅对驱动程序编写器; 通常有趣也就是说，驱动程序体系结构通常没有任何区别到应用程序。 但是，无论应用程序可以使用特定于 DBMS 的 SQL，可能会影响体系结构。 例如，Microsoft Access 提供了一个独立的数据库引擎。 如果 Microsoft Access 驱动程序是基于 DBMS 的 — 它通过此引擎访问数据-应用程序可以将 Microsoft 访问 – SQL 语句传递给引擎以进行处理。  
  
 但是，如果驱动程序是基于文件的-即，它包含直接访问的 Microsoft® Access.mdb 文件的专有引擎-将访问特定于 Microsoft SQL 语句传递到引擎的任何尝试都可能会导致语法错误。 原因是专有引擎是可能实现仅 ODBC SQL。  
  
 本部分包含以下主题。  
  
-   [基于文件的驱动程序](../../odbc/reference/file-based-drivers.md)  
  
-   [基于 DBMS 的驱动程序](../../odbc/reference/dbms-based-drivers.md)  
  
-   [网络示例](../../odbc/reference/network-example.md)  
  
-   [其他驱动程序体系结构](../../odbc/reference/other-driver-architectures.md)
