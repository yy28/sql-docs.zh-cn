---
title: setBytes 方法 （长，字节，int，int） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b18005c16cd62358eb5f269504fc9d80eadb6de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843722"
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes 方法 （长，字节，int，int）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将给定的字节数组的全部或部分写入到在给定的位置、 偏移量和长度; 开始的 BLOB然后返回写入的字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 BLOB 中开始写入数据的位置（从 1 开始）。  
  
 *字节*  
  
 要写入 BLOB 的字节的数组。  
  
 *offset*  
  
 以字节为单位的偏移量数组从何处着手读取数据自**字节**数组。  
  
 len  
  
 要尝试从字节数组读入 BLOB 的字节数。  
  
## <a name="return-value"></a>返回值  
 **Int**包含写入的字节数。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 java.sql.Blob 接口中的 setBytes 方法指定此 setBytes 方法。  
  
 数据将覆盖指定位置开始，并且可以过度运行 BLOB 的初始长度。 指定“位置+1”值将追加字节。 传递“位置+2”或更大值（或零或更小值）会引发位置错误。 传递长度为零**字节**数组将返回零，因为不写入任何字节。  
  
## <a name="see-also"></a>另请参阅  
 [setBytes 方法&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成员](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 类](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
