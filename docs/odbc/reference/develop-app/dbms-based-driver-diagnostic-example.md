---
description: 基于 DBMS 的驱动程序诊断示例
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5425afb18a5582a840966798ea7a7209dba7e1e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424739"
---
# <a name="dbms-based-driver-diagnostic-example"></a>基于 DBMS 的驱动程序诊断示例
基于 DBMS 的驱动程序向 DBMS 发送请求，并通过驱动程序管理器将信息返回给应用程序。 由于驱动程序是与驱动程序管理器进行交互的组件，因此它将格式化并返回 **SQLGetDiagRec**的参数。  
  
 例如，如果使用 SQL/Services，用于 Oracle Rdb 的 Microsoft 驱动程序遇到无效的游标名称，则它可能从 **SQLGetDiagRec**返回以下值：  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 由于此错误发生在驱动程序中，因此它会将前缀添加到供应商 ( [Microsoft] ) 和驱动程序 ( [ODBC Rdb Driver] ) 的诊断消息。  
  
 如果 DBMS 找不到表 EMPLOYEE，驱动程序可能会设置格式并从 **SQLGetDiagRec**返回以下值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 由于错误发生在数据源中，因此驱动程序为数据源标识符添加了前缀 ( [Rdb] ) 到诊断消息。 由于驱动程序是与数据源接口的组件，因此它为其供应商添加了前缀 ( [Microsoft] ) 和标识符 ( [ODBC Rdb Driver] ) 到诊断消息。
