---
title: 网关诊断示例 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305568"
---
# <a name="gateways-diagnostic-example"></a>网关诊断示例
在网关体系结构中，驱动程序将请求发送到支持 ODBC 的网关。 网关将请求发送到 DBMS。 因为它是与驱动程序管理器接口的组件，因此驱动程序格式并返回**SQLGetDiagRec**的参数。  
  
 例如，如果 Oracle 在 Microsoft 开放数据服务上基于 Rdb 的网关，并且 Rdb 找不到表 EMPLOYEE，则网关可能会生成此诊断消息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 由于错误发生在数据源中，网关向诊断消息添加了数据源标识符 （[Rdb]） 的前缀。 由于网关是与数据源接口的组件，因此它将供应商 （[DEC]） 和标识符 （[ODS 网关]） 的前缀添加到诊断消息中。 它还将 SQLSTATE 值和 Rdb 错误代码添加到诊断消息的开头。 这允许它保留其自己的消息结构的语义，并且仍然向驱动程序提供 ODBC 诊断信息。 驱动程序解析网关附加到错误语句的错误信息。  
  
 由于网关驱动程序是与驱动程序管理器接口的组件，它将使用前面的诊断消息格式化并从**SQLGetDiagRec 返回**以下值 ：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
