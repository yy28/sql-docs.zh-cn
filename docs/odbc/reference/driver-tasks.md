---
title: 驱动程序任务 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee695c62fc60b2ebb0ae9bb33ef9008ba617b49a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772626"
---
# <a name="driver-tasks"></a>驱动程序任务
特定驱动程序执行的任务包括：  
  
-   连接和断开与数据源的连接。  
  
-   检查函数错误不会检查由驱动程序管理器。  
  
-   启动事务;这是透明的应用程序。  
  
-   正在提交到数据源执行的 SQL 语句。 该驱动程序必须修改 ODBC 从 SQL 到特定于 DBMS 的 SQL;这通常是限制为替换定义通过使用特定于 DBMS 的 SQL 的 ODBC 转义子句。  
  
-   将数据发送到和从数据源，包括将转换为指定的应用程序的数据类型中检索数据。  
  
-   映射到 ODBC SQLSTATEs 特定于 DBMS 的错误。
