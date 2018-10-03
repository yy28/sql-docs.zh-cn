---
title: 驱动程序体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8e49b89d233880652f4b19879ff8e658bc4abe1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628395"
---
# <a name="driver-architecture"></a>驱动程序体系结构
驱动程序体系结构划分为两个类别，具体取决于哪些软件过程的 SQL 语句：  
  
-   **基于文件的驱动程序**驱动程序直接访问物理数据。 在这种情况下，该驱动程序充当驱动程序和数据源;也就是说，它处理 ODBC 调用和 SQL 语句。 例如，由于 dBASE 不提供独立的数据库引擎驱动程序可以使用 dBASE 驱动程序将不基于文件的驱动程序。 请务必注意，基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
-   **基于 DBMS 的驱动程序**驱动程序通过单独的数据库引擎访问的物理数据。 在这种情况下，驱动程序处理仅 ODBC 调用异步方法。它将 SQL 语句传递到数据库引擎处理。 例如，Oracle 驱动程序是基于 DBMS 的驱动程序，因为 Oracle 驱动程序使用一个独立的数据库引擎。 数据库引擎所在的位置并不重要。 它可以位于与该驱动程序相同的计算机或不同的计算机上网络;它甚至可能通过网关访问。  
  
 仅对驱动程序编写人员; 通常有趣的是驱动程序体系结构也就是说，驱动程序体系结构通常会产生任何影响到应用程序。 但是，该体系结构可能会影响是否应用程序可以使用特定于 DBMS 的 SQL。 例如，Microsoft 访问提供了独立的数据库引擎。 如果 Microsoft Access 驱动程序是基于 DBMS 的 — 它通过此引擎访问的数据，应用程序可以将 Microsoft 访问 – SQL 语句传递给引擎进行处理。  
  
 但是，如果该驱动程序是基于文件的 — 也就是说，它包含直接访问 Microsoft® Access.mdb 文件的专有引擎 — Microsoft 访问特定 SQL 语句传递到引擎的任何尝试都可能会导致语法错误。 原因是专有的引擎是有可能会实现仅 ODBC SQL。  
  
 本部分包含以下主题。  
  
-   [基于文件的驱动程序](../../odbc/reference/file-based-drivers.md)  
  
-   [基于 DBMS 的驱动程序](../../odbc/reference/dbms-based-drivers.md)  
  
-   [网络示例](../../odbc/reference/network-example.md)  
  
-   [其他驱动程序体系结构](../../odbc/reference/other-driver-architectures.md)
