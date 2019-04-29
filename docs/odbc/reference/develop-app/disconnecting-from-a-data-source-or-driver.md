---
title: 断开与数据源或驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2189c0fcc65fd4192e94da140e2d55ac86826137
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935996"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>从数据源或驱动程序断开连接
当应用程序使用完数据源时，它将调用**SQLDisconnect**。 **SQLDisconnect**释放在连接分配任何语句，并与数据源断开连接，驱动程序。 如果事务正在进行，它会返回错误。  
  
 断开连接后，应用程序可以调用**SQLFreeHandle**以释放连接。 释放连接后, 是编程错误应用程序对 ODBC 函数; 的调用中使用的连接句柄这样做存在未定义，但可能严重后果。 当**SQLFreeHandle**调用时，该结构用于存储有关连接的信息的驱动程序版本。  
  
 应用程序还可以重复使用连接来连接到不同的数据源或重新连接到同一数据源。 决定保持连接，而不是断开连接并重新连接更高版本，要求应用程序编写器考虑每个选项; 的相对成本连接到数据源和保持连接状态都可以是具体取决于连接介质开销相对较大。 在进行正确的折衷方案时，应用程序还必须进行假设的可能性和进一步对同一数据源的操作的时间。
