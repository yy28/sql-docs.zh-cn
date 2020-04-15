---
title: 驱动程序任务 |微软文档
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
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294197"
---
# <a name="driver-tasks"></a>驱动程序任务
驱动程序执行的特定任务包括：  
  
-   连接到数据源并从断开。  
  
-   检查驱动程序管理器未检查的函数错误。  
  
-   启动交易;这对应用程序是透明的。  
  
-   将 SQL 语句提交到数据源以进行执行。 驱动程序必须将 ODBC SQL 修改为特定于 DBMS 的 SQL;这通常仅限于将 ODBC 定义的转义子句替换为特定于 DBMS 的 SQL。  
  
-   将数据发送到数据源并从数据源检索数据，包括转换应用程序指定的数据类型。  
  
-   将特定于 DBMS 的错误映射到 ODBC SQLSTAT。
