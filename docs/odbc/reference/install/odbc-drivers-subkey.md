---
title: ODBC 驱动程序子键 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304028"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驱动程序子项
ODBC 驱动程序下键下的值列出了已安装的驱动程序。 这些值的格式显示在下表中。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|*驱动程序描述*|REG_SZ|**安装**|  
  
 *驱动程序描述*名称由驱动程序开发人员定义。 它通常是与驱动程序关联的 DBMS 的名称。  
  
 例如，假设已为格式化的文本文件和 SQL Server 安装了驱动程序。 ODBC 驱动程序子键下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
