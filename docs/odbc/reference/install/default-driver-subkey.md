---
title: 默认驱动程序子键 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301050"
---
# <a name="default-driver-subkey"></a>默认驱动程序子项
默认子键包含描述默认数据源使用的驱动程序的单个值。 此值的格式显示在下表中。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|**驱动程序**|REG_SZ|*默认驱动程序描述*|  
  
 *默认驱动程序描述*名称与描述驱动程序的 ODBC 驱动程序子键下的值名称相同。  
  
 例如，如果默认数据源使用 SQL Server 驱动程序，则默认子键下的值可能是：  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  默认子键中包含的默认驱动程序可以引用默认用户 DSN 或默认系统 DSN。 如果已创建默认用户 DSN 和默认系统 DSN，则默认驱动程序由上次创建的 DSN 确定，因此可能不是首先创建的 DSN 的有效条目。
