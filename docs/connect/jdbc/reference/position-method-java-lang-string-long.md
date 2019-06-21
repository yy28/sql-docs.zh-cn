---
title: position 方法 (java.lang.String，long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86fad8ed-375a-42e1-b40e-1fa085957a2c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40c7dadf83861d889acd7932dbe1dad17fda4b35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802449"
---
# <a name="position-method-javalangstring-long"></a>position 方法 (java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的开始位置返回 CLOB 中指定子字符串的字符位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
public long position(java.lang.String searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parameters  
 searchstr   
  
 要搜索子字符串。  
  
 start   
  
 开始搜索的位置；第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 子字符串出现的位置，如果未出现，则为 -1；第一个位置为 1。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此位置方法由 java.sql.Clob 接口中的位置方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [position 方法&#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
