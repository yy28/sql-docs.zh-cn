---
title: "setString 方法 (长，java.lang.String) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b1bcd2dc8f6e6509099eb4529e57335942c9d6d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring"></a>setString 方法 (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  写入给定**字符串**到给定位置开始 CLOB。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 开始写入 CLOB 的位置。  
  
 *s*  
  
 **字符串**都写入到 CLOB。  
  
## <a name="return-value"></a>返回值  
 写入的字符数。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Clob 接口中的 setString 方法指定此 setString 方法。  
  
 从指定位置开始覆盖字符数据，并可以超过 CLOB 的初始长度。 指定“位置+1”值将追加到字符串末尾。 指定的位置 + 2 或更高版本 （或零个或更少） 值将导致位置错误引发。  
  
## <a name="see-also"></a>另请参阅  
 [setString 方法 &#40;SQLServerClob &#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

