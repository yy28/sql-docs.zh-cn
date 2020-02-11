---
title: 步骤6：断开与数据源的连接 |Microsoft Docs
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
ms.openlocfilehash: 65cc2ae8d2c2248a733e6efa9537fd3b40bb8fd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114121"
---
# <a name="step-6-disconnect-from-the-data-source"></a>步骤 6：从数据源断开连接
最后一步是断开与数据源的连接，如下图所示。 首先，应用程序通过调用**SQLFreeHandle**释放所有语句句柄。 有关详细信息，请参阅[释放语句句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![显示如何断开与数据源的连接](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下来，应用程序与**SQLDisconnect**断开与数据源的连接，并通过**SQLFreeHandle**释放连接句柄。 有关详细信息，请参阅[与数据源或驱动程序断开连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
 最后，应用程序通过**SQLFreeHandle**释放环境句柄，并卸载驱动程序管理器。 有关详细信息，请参阅[分配环境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
