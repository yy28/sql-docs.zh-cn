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
manager: craigg
ms.openlocfilehash: 928e9ffa4701568aac8c519a23e7e371596a36eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765797"
---
# <a name="diagnostic-records"></a>诊断记录
关联的每个环境中，连接、 语句和描述符句柄都*诊断记录*。 这些记录包含有关使用特定的句柄的最后一个函数调用的诊断信息。 仅当使用该句柄调用另一个函数时，将替换记录。 可以存储在任何一次的诊断记录数没有限制。  
  
 有两种类型的诊断记录：*标头记录*以及零个或多个*状态记录*。 标题记录为记录 0;状态记录都是记录 1 及更高版本。 诊断记录组成的单独字段，它们是不同的标题记录和状态记录数。 此外，ODBC 组件可以定义自己的诊断记录字段。  
  
 虽然诊断记录可以看作结构，但没有任何要求它们真正成为结构;驱动程序存储的诊断信息的方式是特定于驱动程序。  
  
 通过检索诊断记录中的字段**SQLGetDiagField**。 可使用一次调用中检索的 SQLSTATE、 本机错误号和状态记录的诊断消息字段**SQLGetDiagRec**。  
  
 本部分包含以下主题。  
  
-   [标头记录](../../../odbc/reference/develop-app/header-record.md)  
  
-   [状态记录](../../../odbc/reference/develop-app/status-records.md)
