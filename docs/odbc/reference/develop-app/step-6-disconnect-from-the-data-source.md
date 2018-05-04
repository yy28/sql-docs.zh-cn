---
title: 步骤 6： 从数据源断开连接 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9d35aa0d9f7fddb8aa713ca4ef9e6ec5f7968e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="step-6-disconnect-from-the-data-source"></a>步骤 6： 从数据源断开连接
最后一步是从数据源断开连接下图中所示。 首先，应用程序通过调用释放任何语句句柄**SQLFreeHandle**。 有关详细信息，请参阅[释放语句处理](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![显示与数据源断开连接](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下来，从数据源断开连接的应用程序**SQLDisconnect**并释放与连接句柄**SQLFreeHandle**。 有关详细信息，请参阅[断开与数据源或驱动程序的连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
 最后，应用程序释放使用的环境句柄**SQLFreeHandle**和卸载驱动程序管理器。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
