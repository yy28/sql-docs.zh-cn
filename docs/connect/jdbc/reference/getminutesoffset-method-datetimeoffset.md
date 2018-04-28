---
title: getMinutesOffset 方法 (DateTimeOffset) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ffaf44dae71da5c5f370c25dab87e4d799707dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  以分钟为单位从格林威治标准时间，此 DateTimeOffset 对象返回的偏移量。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>返回值  
 以分钟表示的偏移量。  
  
## <a name="remarks"></a>注释  
 DateTimeOffset 对象表示 8 2010 年 3 月 11:35:48-0800，getMinutesOffset 返回 480 的值。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
