---
title: getCharacterStream 方法 （长，长型值） (SQLServerNClob) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d54808511d4bdfe6c464cd6deee989757521266
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>getCharacterStream 方法 (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索**NCLOB**数据作为**读取器**对象或为具有指定的位置和长度的字符流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 A**长**，该值指示要检索的部分的值的第一个字符的偏移量。  
  
 *length*  
  
 A**长**，该值指示以字符为单位要检索的部分的值的长度。  
  
## <a name="return-value"></a>返回值  
 读取器对象，其中包含**NCLOB**数据。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.NClob 接口中的 getCharacterStream 方法指定此 getCharacterStream 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getCharacterStream 方法&#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
