---
title: valueOf 方法 （java.sql.Timestamp，java.util.Calendar） |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e75ea9ae6b98041d2f79d2a8a0c515ed1b05b2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 方法 (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建**DateTimeOffset**格林威治标准时间给定 java.sql.Timestamp 值和一个 java.util.Calendar 值，该值偏移量表示特定偏移量处的时间点的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parameters  
 *timestamp*  
  
 java.sql.Timestamp值。  
  
 *日历*  
  
 偏移量的值。  日期和时间组件*日历*将设置为根据*时间戳*值。  
  
## <a name="return-value"></a>返回值  
 返回表示位于给定的 java.util.Calendar 对象时区的 java.sql.Timestamp 对象由给定的时间点的 DateTimeOffset 对象。  
  
## <a name="remarks"></a>注释  
 此方法还将 java.util.Calendar 对象设置为点 java.sql.Timestamp 对象由给定的时间。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
