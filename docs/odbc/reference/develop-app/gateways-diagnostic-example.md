---
title: 网关诊断示例 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9d77f42b0941cecc8a17fe3b54ee91705af0666
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="gateways-diagnostic-example"></a>网关诊断示例
在网关体系结构，驱动程序将请求发送到网关支持 ODBC。 网关将请求发送给 DBMS。 因为它是接口与驱动程序管理器中的组件，该驱动程序进行格式化，并返回自变量**SQLGetDiagRec**。  
  
 例如，如果 Oracle 基于 Microsoft 开放式数据服务和 Rdb 找不到表员工的 Rdb 的网关，网关可能会产生此诊断消息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 在数据源中发生错误，因为网关的数据源标识符 ([Rdb]) 的前缀添加到诊断消息中。 由于网关 interfaced 与数据源的组件，但它会将其供应商 ([DEC]) 和标识符 （[ODS 网关]） 的前缀添加到诊断消息。 它还为诊断消息的开头添加 SQLSTATE 值和 Rdb 错误代码。 这允许使用它来保留其自己的消息结构的语义，仍提供到该驱动程序的 ODBC 诊断信息。 该驱动程序分析错误信息附加到的错误语句由网关。  
  
 由于网关驱动程序接口与驱动程序管理器中的组件，它将使用上面的诊断消息进行格式化和返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
