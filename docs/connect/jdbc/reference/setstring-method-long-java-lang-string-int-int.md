---
title: "setString 方法 (长，java.lang.String，int，int) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerClob.setString (long, java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fb59b09-e825-46a6-ba5d-85d4a8dc143a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 362cd4df54ee5ad826d2313341cd9ba4c7253546
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring-int-int"></a>setString 方法 (long, java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的偏移量和长度，将给定的字符串写入 CLOB（从给定的位置开始）。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setString(long pos,  
                     java.lang.String str,  
                     int offset,  
                     int len)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 开始写入 CLOB 的位置。  
  
 *str*  
  
 要写入 CLOB 的字符串。  
  
 *偏移量*  
  
 字符串中的偏移量，从这个位置开始读取字符。  
  
 *len*  
  
 将要写入的字符数。  
  
## <a name="return-value"></a>返回值  
 写入的字符数。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Clob 接口中的 setString 方法指定此 setString 方法。  
  
 字符数据将覆盖指定位置开始，并且可以覆盖 CLOB 的初始长度。 指定“位置+1”值将追加到字符串末尾。 指定“位置+2”或更大值（或零或更小值）会引发位置错误。  
  
## <a name="see-also"></a>另请参阅  
 [setString 方法 &#40;SQLServerClob &#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

