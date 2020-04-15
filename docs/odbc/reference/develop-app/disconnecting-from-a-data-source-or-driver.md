---
title: 断开与数据源或驱动程序的连接 |微软文档
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
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300457"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>从数据源或驱动程序断开连接
当应用程序完成使用数据源后，它将调用**SQLDisconnect**。 **SQLDisconnect**释放在连接上分配的任何语句，并将驱动程序与数据源断开连接。 如果事务正在处理中，它将返回错误。  
  
 断开连接后，应用程序可以调用**SQLFreeHandle**来释放连接。 释放连接后，在调用 ODBC 函数时使用连接的句柄是应用程序编程错误;这样做有未定义，但可能是致命的后果。 调用**SQLFreeHandle**时，驱动程序将释放用于存储有关连接的信息的结构。  
  
 应用程序还可以重用连接，以连接到其他数据源或重新连接到同一数据源。 保持连接的决定，而不是以后断开连接和重新连接，要求应用程序编写器考虑每个选项的相对成本;连接到数据源和保持连接可能相对昂贵，具体取决于连接介质。 在进行正确的权衡时，应用程序还必须对在同一数据源上进行进一步操作的可能性和时间进行假设。
