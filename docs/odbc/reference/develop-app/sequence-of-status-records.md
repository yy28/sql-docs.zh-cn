---
description: 状态记录的序列
title: 状态记录顺序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2cb519cab987a1abd924f1b779a7f07c3201475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476449"
---
# <a name="sequence-of-status-records"></a>状态记录的序列
如果返回了两个或更多状态记录，驱动程序管理器和驱动程序将根据以下规则对它们进行排序。 排名最高的记录是第一条记录。 对记录进行排序时，不考虑 (驱动程序管理器、驱动程序和网关等) 记录的源。  
  
-   **错误** 描述错误的状态记录的排名最高。 在错误记录中，表示事务失败或事务失败的记录 outrank 所有其他记录。 如果两个或更多记录描述相同的错误条件，则由开放组 CLI 规范定义的 SQLSTATEs 将 (类03到 HZ) outrank ODBC 定义的 SQLSTATEs 和驱动程序定义的。  
  
-   **实现-未定义数据值** 用于描述驱动程序定义的不含数据值 (类 02) 的状态记录具有第二个最高级别。  
  
-   **警告** 描述 (类 01) 的警告的状态记录的排名最低。 如果两个或更多记录描述了相同的警告条件，则由开放式组 CLI 规范 outrank 定义的警告 SQLSTATEs 由 ODBC 定义的 SQLSTATEs 和驱动程序定义的。  
  
 如果有两个或更多个记录的排名最高，则不确定哪个记录是第一条记录。 所有其他记录的顺序是不确定的。 特别是，由于警告可能出现在错误之前，因此当函数返回 SQL_SUCCESS 以外的值时，应用程序应检查所有状态记录。
