---
title: 步骤 6：断开与数据源的连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a42465e763f8f6d520ed9c1dac42612aa1b28575
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149216"
---
# <a name="step-6-disconnect-from-the-data-source"></a>步骤 6：从数据源断开连接
最后一步是从数据源断开连接，如下图中所示。 首先，应用程序通过调用释放任何语句句柄**SQLFreeHandle**。 有关详细信息，请参阅[释放语句句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![显示与数据源断开连接](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下来，从数据源断开连接应用程序**SQLDisconnect** ，并释放与连接句柄**SQLFreeHandle**。 有关详细信息，请参阅[断开与数据源或驱动程序的连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
 最后，应用程序释放环境句柄与**SQLFreeHandle**和卸载驱动程序管理器。 有关详细信息，请参阅[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
