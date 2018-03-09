---
title: "驱动程序 |Microsoft 文档"
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
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2c7299dbbb9cce2f3c97344df33acf27d89c39f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="drivers"></a>驱动程序
*驱动程序*ODBC API 中实现的函数的库。 每个是特定于特定 DBMS;例如，用于 Oracle 的驱动程序不能直接访问 Informix DBMS 中的数据。 驱动程序公开的功能的基础的 Dbms;它们不需要实现不支持的 DBMS 的功能。 例如，如果基础的 DBMS 不支持外部联接中，则不应驱动程序。 仅主要的例外是不具有独立的数据库引擎，如 Xbase，Dbms 的驱动程序必须实现至少支持最少量的 SQL 数据库引擎。  
  
 本部分包含以下主题。  
  
-   [驱动程序任务](../../odbc/reference/driver-tasks.md)  
  
-   [驱动程序体系结构](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 提供的 ODBC 驱动程序](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
