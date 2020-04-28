---
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
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304168"
---
# <a name="sequence-of-status-records"></a>状态记录的序列
如果返回了两个或更多状态记录，驱动程序管理器和驱动程序将根据以下规则对它们进行排序。 排名最高的记录是第一条记录。 对记录进行排序时，不考虑记录源（驱动程序管理器、驱动程序和网关等）。  
  
-   **错误**描述错误的状态记录的排名最高。 在错误记录中，表示事务失败或事务失败的记录 outrank 所有其他记录。 如果两个或更多记录描述相同的错误条件，则由开放式组 CLI 规范（类03到 HZ） outrank 定义的 SQLSTATEs 定义的 SQLSTATEs。  
  
-   **实现-未定义数据值**描述驱动程序定义的不包含数据值的状态记录（第02类）的排名最高。  
  
-   **警告**描述警告（类01）的状态记录的排名最低。 如果两个或更多记录描述了相同的警告条件，则由开放式组 CLI 规范 outrank 定义的警告 SQLSTATEs 由 ODBC 定义的 SQLSTATEs 和驱动程序定义的。  
  
 如果有两个或更多个记录的排名最高，则不确定哪个记录是第一条记录。 所有其他记录的顺序是不确定的。 特别是，由于警告可能出现在错误之前，因此当函数返回 SQL_SUCCESS 以外的值时，应用程序应检查所有状态记录。
