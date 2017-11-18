---
title: "setBytes 方法 （长，字节） |Microsoft 文档"
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
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75886137dd2d8ac768dff35d3cf6bb9a7100efeb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setbytes-method-long-byte"></a>setBytes 方法 （长，字节）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将给定的字节数组写入 BLOB（从给定的位置开始），然后返回写入的字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 （1 开始） 开始将数据写入 BLOB 中的位置。  
  
 *字节*  
  
 要写入 BLOB 的字节的数组。  
  
## <a name="return-value"></a>返回值  
 A**长**值，该值指定写入的字节数。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Blob 接口中的 setBytes 方法指定此 setBytes 方法。  
  
 从指定位置开始覆盖数据，并可以超过 BLOB 的初始长度。 指定“位置+1”值将追加字节。 传递“位置+2”或更大值（或零或更小值）会引发位置错误。 传递长度为零**字节**数组将返回零，因为不写入任何字节。  
  
## <a name="see-also"></a>另请参阅  
 [setBytes 方法 &#40;SQLServerBlob &#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

