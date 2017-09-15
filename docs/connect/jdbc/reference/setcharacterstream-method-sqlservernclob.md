---
title: "setCharacterStream 方法 (SQLServerNClob) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54ea45119a144852daff92dac5037b6f7407d259
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setcharacterstream-method-sqlservernclob"></a>setCharacterStream 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索要用于写入到的 Unicode 字符流的流**NCLOB**值**java.sql.NClob**对象所表示，从指定位置开始。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 若要开始写入的位置**NCLOB** value; 的第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 表示已编码的字符可以写入到的 Unicode 流编写器对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.NClob 接口中的 setCharacterStream 方法指定此 setCharacterStream 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
