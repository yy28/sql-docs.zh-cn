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
manager: craigg
ms.openlocfilehash: 04f19f08deda9cd42affa0a5ced28255c1bb521b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742925"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  比较此**DateTimeOffset**对象和另一个**DateTimeOffset**对象基于采用 GMT 的时间。  
  
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
|0|这两**DateTimeOffset**对象表示相同的点的时间。|  
|负数|这**DateTimeOffset**对象表示之前的时间点*其他*。|  
|正数|这**DateTimeOffset**对象表示一个点之后的时间*其他*。|  
  
## <a name="remarks"></a>Remarks  
 当两个 DateTimeOffset 对象具有相同的 GMT 时间时，没有基于偏移量的对象的附加排序。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
