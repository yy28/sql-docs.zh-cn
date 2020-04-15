---
title: 诊断处理规则 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305838"
---
# <a name="diagnostic-handling-rules"></a>诊断处理规则
以下规则管理**SQLGetDiagRec**和**SQLGetDiagField**中的诊断处理。  
  
 对于所有 ODBC 组件：  
  
-   不得替换、更改或掩盖从其他 ODBC 组件接收的错误或警告。  
  
-   当他们收到来自其他 ODBC 组件的诊断消息时，可能会添加其他状态记录。 添加的记录必须向原始邮件添加真实信息值。  
  
 对于直接接口数据源的 ODBC 组件：  
  
-   必须为其供应商标识符、其组件标识符和数据源标识符前缀到其从数据源接收的诊断消息。  
  
-   必须保留数据源的本机错误代码。  
  
-   必须保留数据源的诊断消息。  
  
 对于独立于数据源生成错误或警告的任何 ODBC 组件：  
  
-   必须为错误或警告提供正确的 SQLSTATE。  
  
-   必须生成诊断消息的文本。  
  
-   必须将其供应商标识符和组件标识符前缀到诊断消息。  
  
-   必须返回本机错误代码（如果代码可用且有意义）。  
  
 对于与驱动程序管理器接口的 ODBC 组件：  
  
-   必须初始化**SQLGetDiagRec**和**SQLGetDiagField**的输出参数。  
  
-   在调用该函数时，必须格式化诊断信息并将其返回为**SQLGetDiagRec**和**SQLGetDiagField**的输出参数。  
  
 对于驱动程序管理器以外的一个 ODBC 组件：  
  
-   必须基于本机错误设置 SQLSTATE。 对于不使用网关的基于文件的驱动程序和基于 DBMS 的驱动程序，驱动程序必须设置 SQLSTATE。 对于使用网关的基于 DBMS 的驱动程序，驱动程序或支持 ODBC 的网关可能会设置 SQLSTATE。
