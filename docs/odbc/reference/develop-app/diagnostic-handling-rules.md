---
title: 诊断处理规则 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 269e021d3fd4610c2fccda46bcd8ca160982543c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039926"
---
# <a name="diagnostic-handling-rules"></a>诊断处理规则
以下规则控制**SQLGetDiagRec**和**SQLGetDiagField**中的诊断处理。  
  
 对于所有 ODBC 组件：  
  
-   不得替换、更改或屏蔽从另一个 ODBC 组件收到的错误或警告。  
  
-   可以在接收来自另一个 ODBC 组件的诊断消息时添加其他状态记录。 添加的记录必须将实际信息值添加到原始消息。  
  
 对于直接对数据源进行交互的 ODBC 组件：  
  
-   必须为其供应商标识符、其组件标识符和数据源标识符发送到它从数据源接收的诊断消息。  
  
-   必须保留数据源的本机错误代码。  
  
-   必须保留数据源的诊断消息。  
  
 对于生成独立于数据源的错误或警告的任何 ODBC 组件：  
  
-   必须为错误或警告提供正确的 SQLSTATE。  
  
-   必须生成诊断消息的文本。  
  
-   必须将其供应商标识符及其组件标识符作为诊断消息的前缀。  
  
-   必须返回本机错误代码（如果有的话）。  
  
 对于与驱动程序管理器进行交互的 ODBC 组件：  
  
-   必须初始化**SQLGetDiagRec**和**SQLGetDiagField**的输出参数。  
  
-   调用该函数时，必须将诊断信息格式化并返回到**SQLGetDiagRec**和**SQLGetDiagField**的输出参数。  
  
 对于除驱动程序管理器之外的一个 ODBC 组件：  
  
-   必须基于本机错误设置 SQLSTATE。 对于基于文件的驱动程序和不使用网关的基于 DBMS 的驱动程序，驱动程序必须设置 SQLSTATE。 对于使用网关的基于 DBMS 的驱动程序，驱动程序或支持 ODBC 的网关可能会设置 SQLSTATE。
