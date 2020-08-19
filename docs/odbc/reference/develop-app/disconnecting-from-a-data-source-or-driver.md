---
description: 从数据源或驱动程序断开连接
title: 断开与数据源或驱动程序的连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc14ca0ebf29a2ab203a4408db4b5681ad667497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476689"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>从数据源或驱动程序断开连接
当应用程序使用完数据源后，它将调用 **SQLDisconnect**。 **SQLDisconnect** 释放在连接上分配的所有语句，并断开驱动程序与数据源的连接。 如果事务正在进行中，它将返回错误。  
  
 断开连接后，应用程序可以调用 **SQLFreeHandle** 来释放连接。 释放连接后，它是一个应用程序编程错误，用于在对 ODBC 函数的调用中使用连接的句柄;这样做没有定义，但可能会产生严重后果。 调用 **SQLFreeHandle** 时，驱动程序将释放用于存储有关连接的信息的结构。  
  
 应用程序还可以重新使用连接，以便连接到不同的数据源或重新连接到同一数据源。 决定保持连接状态，而不是在以后断开连接和重新连接，要求应用程序编写人员考虑每个选项的相对成本;连接到数据源和剩余连接可能会相对较高的成本，具体取决于连接媒体。 在进行正确的权衡时，应用程序还必须对同一数据源上的进一步操作的可能性和时间进行假设。
