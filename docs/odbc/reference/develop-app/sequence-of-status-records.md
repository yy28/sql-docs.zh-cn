---
title: 状态记录序列 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304168"
---
# <a name="sequence-of-status-records"></a>状态记录的序列
如果返回两个或多个状态记录，驱动程序管理器和驱动程序会根据以下规则对它们进行排名。 排名最高的记录是第一条记录。 在排名记录时，不考虑记录的来源（驱动程序管理器、驱动程序、网关等）。  
  
-   **错误**描述错误的状态记录的排名最高。 在错误记录中，指示事务失败或可能事务失败的记录超过所有其他记录。 如果两个或多个记录描述相同的错误条件，则由开放组 CLI 规范定义的 SQLSTAT（类 03 到 HZ）比 ODBC 定义和驱动程序定义的 SQLSTATEs 高。  
  
-   **实现定义的无数据值**描述驱动程序定义的无数据值（类 02）的状态记录具有第二高的排名。  
  
-   **警告**描述警告的状态记录（类 01）的排名最低。 如果两个或多个记录描述相同的警告条件，则 Open Group CLI 规范定义的警告 SQLSTAT 比 ODBC 定义和驱动程序定义的 SQLSTATA 高。  
  
 如果有两个或多个排名最高的记录，则未定义哪个记录是第一条记录。 所有其他记录的顺序未定义。 特别是，由于警告可能出现在错误之前，因此当函数返回SQL_SUCCESS以外的值时，应用程序应检查所有状态记录。
