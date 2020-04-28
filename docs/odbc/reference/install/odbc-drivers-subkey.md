---
title: ODBC 驱动程序子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304028"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驱动程序子项
ODBC 驱动程序子项下的值列出了已安装的驱动程序。 下表显示了这些值的格式。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*驱动程序-说明*|REG_SZ|**已安装**|  
  
 *驱动程序说明*名称由驱动程序开发人员定义。 它通常是与驱动程序相关联的 DBMS 的名称。  
  
 例如，假设已为格式化文本文件和 SQL Server 安装了驱动程序。 ODBC 驱动程序子项下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
