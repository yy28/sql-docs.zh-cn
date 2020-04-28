---
title: 网关诊断示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305568"
---
# <a name="gateways-diagnostic-example"></a>网关诊断示例
在网关体系结构中，驱动程序将请求发送到支持 ODBC 的网关。 网关将请求发送到 DBMS。 由于它是与驱动程序管理器进行交互的组件，因此，驱动程序将格式化并返回**SQLGetDiagRec**的参数。  
  
 例如，如果基于 Oracle 的网关与 Microsoft 开放式数据服务的 Rdb 建立了基于 Oracle 的的网关，并且 Rdb 未能找到表 EMPLOYEE，则网关可能会生成以下诊断消息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 由于错误发生在数据源中，因此网关向诊断消息添加了数据源标识符（[Rdb]）的前缀。 由于网关是与数据源接口的组件，因此它为其供应商添加了前缀（[DEC]）和标识符（[ODS 网关]）到诊断消息。 它还将 SQLSTATE 值和 Rdb 错误代码添加到诊断消息的开头。 这允许它保留其自己的消息结构的语义，并仍向驱动程序提供 ODBC 诊断信息。 驱动程序通过网关分析附加到错误语句的错误信息。  
  
 由于网关驱动程序是与驱动程序管理器进行交互的组件，因此它将使用前面的诊断消息格式化并返回**SQLGetDiagRec**中的以下值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
