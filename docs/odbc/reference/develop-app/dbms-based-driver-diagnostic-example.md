---
title: 基于 DBMS 的驱动程序诊断示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0485ecf720cb84580c17c77b31fc6816de2e679a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622265"
---
# <a name="dbms-based-driver-diagnostic-example"></a>基于 DBMS 的驱动程序诊断示例
基于 DBMS 的驱动程序将请求发送到 DBMS，并返回到应用程序通过驱动程序管理器的信息。 由于驱动程序接口与驱动程序管理器的组件，其格式，并返回自变量**SQLGetDiagRec**。  
  
 例如，如果使用 Oracle Rdb 遇到无效的游标名称 SQL/服务，Microsoft 驱动程序，它可能会返回以下值从**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 驱动程序中发生错误，因为它添加前缀到诊断消息供应商 ([Microsoft]) 和驱动程序 ([ODBC Rdb Driver])。  
  
 如果 DBMS 找不到 EMPLOYEE 表，该驱动程序可能会设置格式，并返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 因为数据源中发生错误，该驱动程序将添加到诊断消息的数据源标识符 ([Rdb]) 的前缀。 由于驱动程序与数据源对接的组件，但它会将其供应商 ([Microsoft]) 和标识符 ([ODBC Rdb Driver]) 前缀添加到诊断消息。
