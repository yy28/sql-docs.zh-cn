---
title: 断开数据源或驱动程序 |Microsoft 文档
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c99a2fb7c441c6de2a229895a1a68d68e9240c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>断开数据源或驱动程序
当应用程序已完成将数据源使用时，它将调用**SQLDisconnect**。 **SQLDisconnect**释放连接分配的所有语句并将驱动程序与数据源断开连接。 如果事务进程中，它会返回错误。  
  
 断开连接之后，应用程序可以调用**SQLFreeHandle**以释放连接。 后释放该连接，它是对应用程序编程错误对 ODBC 函数; 的调用中使用连接的句柄因此，这样做具有未定义，但可能严重后果。 当**SQLFreeHandle**调用时，结构用于存储有关连接的信息的驱动程序版本。  
  
 应用程序还可以重复使用的连接，以连接到不同的数据源，或者重新连接到同一数据源。 决策以保持连接，而不是断开连接，并重新连接更高版本，要求应用程序编写器考虑每个选项; 的相对成本同时连接到数据源和保持连接状态可以是具体取决于连接中等开销相对较大。 在进行时正确权衡，应用程序还必须进行假设的可能性及进一步对同一数据源的操作的计时。
