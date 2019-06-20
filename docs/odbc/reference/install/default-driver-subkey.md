---
title: 默认驱动程序子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78101fd564e18467e6833f480cec2409dc2c44b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198304"
---
# <a name="default-driver-subkey"></a>默认驱动程序子项
默认子项包含一个说明默认数据源使用的驱动程序的单个值。 下表中显示此值的格式。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|**驱动程序**|REG_SZ|*default-driver-description*|  
  
 *驱动程序的默认描述*名称是描述的驱动程序的 ODBC 驱动程序子项下的值的名称相同。  
  
 例如，如果默认数据源使用的 SQL Server 驱动程序，可能会默认子项下的值：  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  在默认的子项中包含的默认驱动程序可以引用一个默认用户 DSN 或默认系统 DSN。 如果默认用户 DSN 和默认系统已创建 DSN，因此它可能不是有效的 DSN，首先创建条目，最后，创建的 DSN 是可确定默认驱动程序。
