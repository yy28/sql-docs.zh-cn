---
title: position 方法 (java.sql.NClob，long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 35d8a3903cc18ce371b2d6c333747710ac6efc7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802418"
---
# <a name="position-method-javasqlnclob-long"></a>position 方法 (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索的字符位置指定**NClob**对象*searchstr*将显示在此**NClob**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parameters  
 searchstr   
  
 要搜索的 NClob 对象。  
  
 start   
  
 开始搜索的位置；第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 子字符串出现的位置，如果未出现，则为 -1。 第一个位置为 1。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此位置方法由 java.sql.NClob 接口中的位置方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [position 方法&#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
