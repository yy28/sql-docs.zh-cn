---
title: "SQLServerNClob 成员 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f6b8006caed20d4362953ba2d524acc601cb0a7e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlservernclob-members"></a>SQLServerNClob 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
 无。  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[释放](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|此方法释放**NCLOB**对象并释放它所包含的资源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|检索**NCLOB**值由**java.sql.NClob**作为 ASCII 流的对象。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|检索**NCLOB**值由**java.sql.NClob**对象。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|检索指定的子字符串内的副本**NCLOB**值由**java.sql.NClob**对象。|  
|[长度](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|检索中的字符数**NCLOB**值由**java.sql.NClob**对象。|  
|[位置](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|检索指定的字符位置**java.sql.NClob**对象或子字符串替换在**java.sql.NClob**基于指定的起始位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|检索流用于写入 ASCII 字符到**NCLOB**值**java.sql.NClob**对象所表示，从指定位置开始。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|检索要用于写入到的 Unicode 字符流的流**NCLOB**值**java.sql.NClob**对象所表示，从指定位置开始。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|将指定**字符串**到**NCLOB**从指定位置开始。|  
|[截断](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|将截断**NCLOB**为指定长度的值。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.sql.Clob|free、getAsciiStream、getCharacterStream、getSubString、length、position、setAsciiStream、setCharacterStream、setString、truncate|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
