---
title: 驱动程序体系结构 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294217"
---
# <a name="driver-architecture"></a>驱动程序体系结构
驱动程序体系结构分为两类，具体取决于哪个软件处理 SQL 语句：  
  
-   **基于文件的驱动程序**驱动程序直接访问物理数据。 在这种情况下，驱动程序同时充当驱动程序和数据源;因此，驱动程序充当驱动程序和数据源。也就是说，它处理 ODBC 调用和 SQL 语句。 例如，dBASE 驱动程序是基于文件的驱动程序，因为 dBASE 不提供驱动程序可以使用的独立数据库引擎。 请务必注意，基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
-   **基于 DBMS 的驱动程序**驱动程序通过单独的数据库引擎访问物理数据。 在这种情况下，驱动程序仅处理 ODBC 调用;因此，驱动程序将仅处理 ODBC 调用。它将 SQL 语句传递给数据库引擎进行处理。 例如，Oracle 驱动程序是基于 DBMS 的驱动程序，因为 Oracle 具有驱动程序使用的独立数据库引擎。 数据库引擎所在的位置无关紧要。 它可以与驱动程序或网络上的其他计算机驻留在同一台计算机上;它甚至可能通过网关访问。  
  
 驱动程序体系结构通常只对驱动程序编写者感兴趣;也就是说，驱动程序体系结构通常对应用程序没有影响。 但是，体系结构可能会影响应用程序是否可以使用特定于 DBMS 的 SQL。 例如，Microsoft Access 提供了一个独立的数据库引擎。 如果 Microsoft Access 驱动程序基于 DBMS -它通过此引擎访问数据 -应用程序可以将 Microsoft Access-SQL 语句传递给引擎进行处理。  
  
 但是，如果驱动程序是基于文件的 -也就是说，它包含直接访问 Microsoft® Access .mdb 文件的专有引擎-任何将特定于 Microsoft 访问的 SQL 语句传递给引擎的尝试都可能导致语法错误。 原因是专有引擎可能仅实现 ODBC SQL。  
  
 本部分包含以下主题。  
  
-   [基于文件的驱动程序](../../odbc/reference/file-based-drivers.md)  
  
-   [基于 DBMS 的驱动程序](../../odbc/reference/dbms-based-drivers.md)  
  
-   [网络示例](../../odbc/reference/network-example.md)  
  
-   [其他驱动程序体系结构](../../odbc/reference/other-driver-architectures.md)
