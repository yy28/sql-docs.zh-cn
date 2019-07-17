---
title: ODBC 数据源的子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a1d0c506c4a4b33d7138378032947821d4e9f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093993"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子项
在 ODBC 数据源的子项下的值列表的数据源。 这些值的格式为下表中所示。  
  
|“属性”|数据类型|Data|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 *数据源名称*值定义管理程序 （这通常会提示用户为其），并*驱动程序说明*驱动程序开发人员定义 (它通常是的名称DBMS 的驱动程序相关联的)。  
  
 例如，假设三个数据源已定义：清单，它将使用 SQL Server;工资单、 使用 dBASE;和人员，使用该格式的文本文件。 在 ODBC 数据源的子项下的值可能按如下所示：  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
