---
title: "驱动程序任务 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 331e3aee3a4a60cbfa1a1308b71da80bf9772f23
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-tasks"></a>驱动程序任务
特定驱动程序执行的任务包括：  
  
-   连接到和从数据源断开连接。  
  
-   正在检查的函数不会检查由驱动程序管理器中的错误。  
  
-   启动事务;这是透明的应用程序。  
  
-   正在提交到数据源执行的 SQL 语句。 该驱动程序必须修改与特定于 DBMS 的 SQL; ODBC SQL这通常是限于替换定义使用特定于 DBMS 的 SQL 的 ODBC 转义子句。  
  
-   发送数据到和从数据源，包括将转换为指定的应用程序的数据类型中检索数据。  
  
-   映射到 ODBC SQLSTATEs DBMS 特定错误。

