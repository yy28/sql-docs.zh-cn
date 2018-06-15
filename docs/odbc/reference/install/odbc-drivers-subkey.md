---
title: ODBC 驱动程序子项 |Microsoft 文档
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0359547122a9ee5537ae4634e6907e39f12916d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914952"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驱动程序子项
ODBC 驱动程序子项下的值列表安装的驱动程序。 下表中显示这些值的格式。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|*驱动程序说明*|REG_SZ|**安装**|  
  
 *驱动程序说明*由驱动程序开发人员定义名称。 它通常是 DBMS 驱动程序与关联的名称。  
  
 例如，假设用于格式化的文本文件和 SQL Server 安装了驱动程序。 可能的 ODBC 驱动程序子项下的值：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
