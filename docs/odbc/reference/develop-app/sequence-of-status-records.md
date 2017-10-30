---
title: "状态记录的序列 |Microsoft 文档"
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
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0e11fdd0d5d560cfcacd034745f7ed32cf8fca8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sequence-of-status-records"></a>状态记录的序列
如果返回了两个或多个状态记录，驱动程序管理器和驱动程序它们设置级别根据以下规则。 具有最高级别的记录是第一条记录。 记录 （驱动程序管理器、 驱动程序、 网关，等） 的源不会被视为时排名记录。  
  
-   **错误**描述错误的状态记录具有最高的排名。 错误记录之间指明事务失败或发生故障的可能的事务的记录 outrank 所有其他记录。 如果两个或多个记录描述相同的错误条件，请打开组 CLI 规范 （通过 HZ 类 03） 所定义的 SQLSTATEs outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
-   **实现定义无数据值**描述驱动程序定义无数据值 （类 02） 的状态记录具有第二个最高级别。  
  
-   **警告**描述警告 （类 01） 的状态记录具有最低的排名。 如果两个或多个记录描述的相同的警告条件，警告打开组 CLI 规范所定义的 SQLSTATEs outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
 如果有具有最高级别的两个或多个记录，它是未定义的记录是第一条记录。 所有其他记录的顺序是不确定的。 具体而言，可能在错误之前出现警告，因为应用程序时应该检查状态的所有记录的函数将返回 SQL_SUCCESS 以外的值。

