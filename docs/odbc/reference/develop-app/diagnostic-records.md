---
title: 诊断记录 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305178"
---
# <a name="diagnostic-records"></a>诊断记录
与每个环境关联的连接、语句和描述符句柄是*诊断记录*。 这些记录包含有关使用特定句柄的最后一个调用的函数的诊断信息。 仅当使用该句柄调用另一个函数时，才会替换记录。 任何一次可以存储的诊断记录数量没有限制。  
  
 有两种类型的诊断记录：*标头记录*和零个或多个*状态记录*。 标头记录为记录 0;标头记录为 0。状态记录是记录 1 和以上。 诊断记录由多个单独的字段组成，这些字段对于标头记录和状态记录是不同的。 此外，ODBC 组件可以定义自己的诊断记录字段。  
  
 虽然诊断记录可以被视为结构，但不需要它们实际上是结构;驱动程序如何存储诊断信息是特定于驱动程序的。  
  
 使用**SQLGetDiagField**检索诊断记录中的字段。 可以使用**SQLGetDiagRec**在单个调用中检索状态记录的 SQLSTATE、本机错误编号和诊断消息字段。  
  
 本部分包含以下主题。  
  
-   [标头记录](../../../odbc/reference/develop-app/header-record.md)  
  
-   [状态记录](../../../odbc/reference/develop-app/status-records.md)
