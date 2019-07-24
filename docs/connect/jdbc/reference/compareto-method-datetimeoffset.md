---
title: compareTo 方法 (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f70413a7624b9bbd380a664fbf61b9a33f8989b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955519"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据 GMT 的时间将此**datetimeoffset**对象与另一个**datetimeoffset**对象进行比较。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parameters  
 要与当前实例进行比较的 [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 值。  
  
## <a name="return-value"></a>返回值  
 下表介绍了此方法的返回值：  
  
|返回值|描述|  
|------------------|-----------------|  
|0|这两个**DateTimeOffset**对象表示相同的时间点。|  
|负数|此**DateTimeOffset**对象*表示之前的*某个时间点。|  
|正数|此**DateTimeOffset**对象表示一个在*其他*时间点。|  
  
## <a name="remarks"></a>Remarks  
 当两个 DateTimeOffset  对象具有相同的 GMT 时间时，没有基于偏移量的对象的附加排序。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
