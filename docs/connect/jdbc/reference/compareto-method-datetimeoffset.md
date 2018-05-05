---
title: compareTo 方法 (DateTimeOffset) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e2953d21306cf69582e2744c4fb96e13e0098d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  比较此**DateTimeOffset**到另一个对象**DateTimeOffset**对象基于格林威治标准时间的时间。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parameters  
 A [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)你想要与当前实例进行比较的值。  
  
## <a name="return-value"></a>返回值  
 下表介绍了此方法的返回值：  
  
|返回值|Description|  
|------------------|-----------------|  
|0|同时**DateTimeOffset**对象表示的时间的相同的点。|  
|负数|这**DateTimeOffset**对象表示是之前的时间点*其他*。|  
|正数|这**DateTimeOffset**对象表示是在后的时间点*其他*。|  
  
## <a name="remarks"></a>注释  
 当两个**DateTimeOffset**对象具有相同的时间在格林威治标准时间，则基于偏移量的对象没有其他排序。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
