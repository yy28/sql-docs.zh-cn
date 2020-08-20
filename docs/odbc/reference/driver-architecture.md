---
description: 驱动程序体系结构
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 530940cef233b8a6b6a3f5c0575dd154998126cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494610"
---
# <a name="driver-architecture"></a>驱动程序体系结构
驱动程序体系结构分为两类，具体取决于哪个软件处理 SQL 语句：  
  
-   **基于文件的驱动程序** 驱动程序直接访问物理数据。 在这种情况下，驱动程序将充当驱动程序和数据源;也就是说，它处理 ODBC 调用和 SQL 语句。 例如，dBASE 驱动程序是基于文件的驱动程序，因为 dBASE 不提供驱动程序可以使用的独立数据库引擎。 需要特别注意的是，基于文件的驱动程序的开发人员必须编写自己的数据库引擎。  
  
-   **基于 DBMS 的驱动程序** 驱动程序通过单独的数据库引擎访问物理数据。 在这种情况下，驱动程序仅处理 ODBC 调用;它将 SQL 语句传递到数据库引擎进行处理。 例如，Oracle 驱动程序是基于 DBMS 的驱动程序，因为 Oracle 包含驱动程序使用的独立数据库引擎。 数据库引擎驻留的位置是重要。 它可以位于驱动程序所在的同一台计算机上或网络上的其他计算机上;甚至可以通过网关访问它。  
  
 驱动程序体系结构通常仅对驱动程序编写器有用;也就是说，驱动程序体系结构通常不会对应用程序产生任何影响。 但是，该体系结构可能会影响应用程序是否可以使用特定于 DBMS 的 SQL。 例如，Microsoft Access 提供独立的数据库引擎。 如果 Microsoft Access 驱动程序基于 DBMS，则它通过此引擎访问数据-应用程序可将 Microsoft Access SQL 语句传递到引擎进行处理。  
  
 但是，如果该驱动程序是基于文件的，则该驱动程序将包含一个专用引擎，该引擎会直接访问 Microsoft®访问 .mdb 文件-任何将 Microsoft Access 特定的 SQL 语句传递到引擎的尝试都可能会导致语法错误。 原因在于，专用引擎可能仅实现 ODBC SQL。  
  
 本部分包含以下主题。  
  
-   [基于文件的驱动程序](../../odbc/reference/file-based-drivers.md)  
  
-   [基于 DBMS 的驱动程序](../../odbc/reference/dbms-based-drivers.md)  
  
-   [网络示例](../../odbc/reference/network-example.md)  
  
-   [其他驱动程序体系结构](../../odbc/reference/other-driver-architectures.md)
