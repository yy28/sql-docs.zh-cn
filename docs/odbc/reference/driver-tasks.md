---
description: 驱动程序任务
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263f591592063a45fdd5afdca4efdd75b5b915b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339053"
---
# <a name="driver-tasks"></a>驱动程序任务
驱动程序执行的特定任务包括：  
  
-   连接到数据源和从数据源断开连接。  
  
-   检查驱动程序管理器未检查的函数错误。  
  
-   开始事务;这对于应用程序是透明的。  
  
-   向数据源提交要执行的 SQL 语句。 驱动程序必须将 ODBC SQL 修改为特定于 DBMS 的 SQL;这通常局限于将 ODBC 定义的转义子句替换为 DBMS 特定的 SQL。  
  
-   将数据发送到数据源和从数据源中检索数据，包括转换应用程序指定的数据类型。  
  
-   将 DBMS 特定的错误映射到 ODBC SQLSTATEs。
