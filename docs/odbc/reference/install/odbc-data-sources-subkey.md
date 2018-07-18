---
title: ODBC 数据源子项 |Microsoft 文档
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
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e81fe6cc77d92a8fde7530c1f79381025a05856b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915462"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子项
ODBC 数据源子项下的值列表的数据源。 下表中所示，将为这些值的格式。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|*数据源名称*|REG_SZ|*驱动程序说明*|  
  
 *数据源名称*值由此管理计划 （它们通常将提示用户为其），定义和*驱动程序说明*定义由驱动程序开发人员 (通常是的名称DBMS 驱动程序与关联的)。  
  
 例如，假设已定义三个数据源： 清单，它将使用 SQL Server;使用 dBASE; 的工资支付和人员，使用格式的文本文件。 ODBC 数据源子项下的值可能如下所示：  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
