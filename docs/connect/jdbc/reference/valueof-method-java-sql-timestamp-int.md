---
title: valueOf 方法 （java.sql.Timestamp，int） |Microsoft 文档
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
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5818dc4dd30ffc0833dc548110fd84cbbc3f5997
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 方法 (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建**DateTimeOffset**格林威治标准时间给定 java.sql.Timestamp 值和一个值，该值以分钟为单位的偏移量表示特定偏移量处的时间点的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parameters  
 *timestamp*  
  
 java.sql.Timestamp值。  
  
 *minutesOffset*  
  
 以分钟表示的偏移量。  
  
## <a name="return-value"></a>返回值  
 返回表示在中给定的时间通过给定的偏移量处的 java.sql.Timestamp 对象分钟，从格林威治标准时间点的 DateTimeOffset 对象。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
