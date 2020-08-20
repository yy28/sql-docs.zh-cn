---
description: 网关诊断示例
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
ms.openlocfilehash: 17e32f0ccdc1b2fbbebb1969083e216ed3371688
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465779"
---
# <a name="gateways-diagnostic-example"></a>网关诊断示例
在网关体系结构中，驱动程序将请求发送到支持 ODBC 的网关。 网关将请求发送到 DBMS。 由于它是与驱动程序管理器进行交互的组件，因此，驱动程序将格式化并返回 **SQLGetDiagRec**的参数。  
  
 例如，如果基于 Oracle 的网关与 Microsoft 开放式数据服务的 Rdb 建立了基于 Oracle 的的网关，并且 Rdb 未能找到表 EMPLOYEE，则网关可能会生成以下诊断消息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 由于错误发生在数据源中，因此网关为数据源标识符添加了前缀 ( [Rdb] ) 到诊断消息。 由于网关是与数据源接口的组件，因此它为其供应商添加了前缀 ( [DEC] ) 和标识符 ( [ODS 网关] ) 到诊断消息。 它还将 SQLSTATE 值和 Rdb 错误代码添加到诊断消息的开头。 这允许它保留其自己的消息结构的语义，并仍向驱动程序提供 ODBC 诊断信息。 驱动程序通过网关分析附加到错误语句的错误信息。  
  
 由于网关驱动程序是与驱动程序管理器进行交互的组件，因此它将使用前面的诊断消息格式化并返回 **SQLGetDiagRec**中的以下值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
