---
title: 状态记录的序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465913"
---
# <a name="sequence-of-status-records"></a>状态记录的序列
如果返回了两个或多个状态记录，驱动程序管理器和驱动程序对其进行排序根据以下规则。 具有最高排名的记录是第一条记录。 记录 （驱动程序管理器、 驱动程序、 网关，等） 的源不被视为时排名记录。  
  
-   **错误**描述错误的状态记录具有最高排名。 在错误的记录，指示事务失败或发生故障的可能的事务的记录 outrank 所有其他记录。 如果两个或多个记录描述相同的错误条件，请打开组 CLI 规范 （通过 HZ 类 03） 所定义的 SQLSTATEs outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
-   **无数据值定义实现**描述驱动程序定义的无数据值 （类 02） 的状态记录具有第二个最高排名。  
  
-   **警告**描述警告 （类 01） 的状态记录具有最低排名。 如果两个或多个记录描述警告 SQLSTATEs 打开组 CLI 规范所定义的相同警告条件 outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
 如果有两个或多个记录的最高排名，是不明确的记录是第一条记录。 所有其他记录的顺序未定义。 具体而言之前的错误, 可能出现警告，因为应用程序时应该检查状态的所有记录函数将返回 SQL_SUCCESS 以外的值。
