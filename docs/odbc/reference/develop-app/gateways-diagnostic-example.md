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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f4e17074616111ee93ce87c04036d1fc3fd48dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607846"
---
# <a name="gateways-diagnostic-example"></a>网关诊断示例
在网关体系结构中，驱动程序将请求发送到支持 ODBC 的网关。 网关将请求发送到 DBMS。 因为它是接口与驱动程序管理器的组件，该驱动程序格式，并返回自变量**SQLGetDiagRec**。  
  
 例如，如果 Oracle 基于 Microsoft 开放式数据服务和 Rdb 找不到 EMPLOYEE 表的 Rdb 的网关，网关可能会生成此诊断消息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 数据源中发生错误，因为网关添加到诊断消息中的数据源标识符 ([Rdb]) 的前缀。 由于网关对接与数据源的组件，但它会将其供应商 ([DEC]) 和标识符 （[ODS 网关]） 前缀添加到诊断消息。 它还添加了 SQLSTATE 值和 Rdb 错误代码的诊断消息开头。 这允许它以保留其自己的消息结构的语义，并仍提供 ODBC 驱动程序的诊断信息。 该驱动程序分析附加到错误语句由网关的错误信息。  
  
 由于网关驱动程序接口与驱动程序管理器的组件，它将使用前面的诊断消息设置格式并返回以下值从**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
