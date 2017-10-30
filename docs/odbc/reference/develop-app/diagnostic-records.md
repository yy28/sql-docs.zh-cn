---
title: "诊断记录 |Microsoft 文档"
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
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 598f047d1ae18e2c37587df270001b49d1b15831
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostic-records"></a>诊断记录
与每个环境关联，连接、 语句和的描述符句柄是*诊断记录*。 这些记录包含有关使用特定的句柄的最后一个函数调用的诊断信息。 记录将替换仅当另一个函数调用时使用该句柄。 对可以在任何时候存储的诊断记录的数量没有限制。  
  
 有两种类型的诊断记录：*标头记录*和零个或多个*状态记录*。 标头记录是记录 0;状态记录是记录 1 和更高版本。 诊断记录组成的单独字段，它们是不同的标头记录和状态记录数。 此外，ODBC 组件可以定义自己的诊断记录字段。  
  
 尽管诊断记录可以看作结构，但是没有为它们地实际成为结构; 要求驱动程序存储的诊断信息的方式是特定于驱动程序。  
  
 中诊断记录的字段检索与**SQLGetDiagField**。 可以在单个调用与检索 SQLSTATE、 本机错误号和诊断消息的状态记录的字段**SQLGetDiagRec**。  
  
 本部分包含以下主题。  
  
-   [标头记录](../../../odbc/reference/develop-app/header-record.md)  
  
-   [状态记录](../../../odbc/reference/develop-app/status-records.md)

