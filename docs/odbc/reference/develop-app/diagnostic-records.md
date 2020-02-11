---
title: 诊断记录 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90133b4a18876c52b9b6b6bffbe4c8c02c953e07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039877"
---
# <a name="diagnostic-records"></a>诊断记录
与每个环境、连接、语句和描述符句柄关联的是*诊断记录*。 这些记录包含有关使用特定句柄的最后一个函数调用的诊断信息。 仅当使用该句柄调用另一个函数时，才会替换这些记录。 可以在任何时间存储的诊断记录数没有限制。  
  
 有两种类型的诊断记录：*标题记录*以及零个或多个*状态记录*。 标头记录为 record 0;状态记录为记录1和更高版本。 诊断记录包含多个单独的字段，它们对于标头记录和状态记录是不同的。 此外，ODBC 组件还可以定义自己的诊断记录字段。  
  
 尽管可以将诊断记录视为结构，但不要求它们实际上是结构;驱动程序如何存储诊断信息特定于驱动程序。  
  
 诊断记录中的字段通过**SQLGetDiagField**检索。 可以使用**SQLGetDiagRec**在一次调用中检索状态记录的 SQLSTATE、本机错误号和诊断消息字段。  
  
 本部分包含下列主题。  
  
-   [标头记录](../../../odbc/reference/develop-app/header-record.md)  
  
-   [状态记录](../../../odbc/reference/develop-app/status-records.md)
