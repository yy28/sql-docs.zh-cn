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
manager: craigg
ms.openlocfilehash: 9f59953dee77453bb8b453a40a36d17e865a1fe5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792255"
---
# <a name="diagnostic-handling-rules"></a>诊断处理规则
以下规则控制诊断中的处理**SQLGetDiagRec**并**SQLGetDiagField**。  
  
 适用于所有 ODBC 组件：  
  
-   必须不替换、 更改或屏蔽错误或警告收到来自另一个 ODBC 组件。  
  
-   在从另一个 ODBC 组件收到一条诊断消息时，可以添加其他状态记录。 添加的记录必须将真实的信息值添加到原始消息。  
  
 将 odbc 组件直接接口的数据源：  
  
-   必须将前缀及其供应商标识符、 其组件标识符和接收来自数据源的诊断消息到数据源的标识符。  
  
-   必须保持数据源的本机错误代码。  
  
-   必须保持数据源的诊断消息。  
  
 生成错误或警告独立于数据源的任何 ODBC 组件：  
  
-   必须提供正确的错误或警告的 SQLSTATE。  
  
-   必须生成诊断消息的文本。  
  
-   必须将前缀及其供应商标识符和诊断消息及其组件标识符。  
  
-   如果有可用且有意义，则必须返回本机错误代码。  
  
 ODBC 组件的接口与驱动程序管理器：  
  
-   必须初始化的输出自变量**SQLGetDiagRec**并**SQLGetDiagField**。  
  
-   必须设置格式并返回作为输出参数的诊断信息**SQLGetDiagRec**并**SQLGetDiagField**时调用该函数。  
  
 为一个 ODBC 组件以外驱动程序管理器：  
  
-   必须设置基于本机错误的 SQLSTATE。 对于基于文件的驱动程序和基于 DBMS 的驱动程序不使用网关，该驱动程序必须设置 SQLSTATE。 对于基于 DBMS 的驱动程序使用网关，该驱动程序或支持 ODBC 的网关可能会设置 SQLSTATE。
