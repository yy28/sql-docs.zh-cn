---
title: SQLServerNClob 成员 |Microsoft 文档
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
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5ca7903675c005a48a7accf17889fc72dc53781
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
|名称|Description|  
|----------|-----------------|  
|[可用](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|此方法释放**NCLOB**对象并释放它所包含的资源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|检索**NCLOB**值由**java.sql.NClob**作为 ASCII 流的对象。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|检索**NCLOB**值由**java.sql.NClob**对象。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|检索指定的子字符串内的副本**NCLOB**值由**java.sql.NClob**对象。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|检索中的字符数**NCLOB**值由**java.sql.NClob**对象。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|检索指定的字符位置**java.sql.NClob**对象或子字符串替换在**java.sql.NClob**基于指定的起始位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|检索流用于写入 ASCII 字符到**NCLOB**值**java.sql.NClob**对象所表示，从指定位置开始。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|检索要用于写入到的 Unicode 字符流的流**NCLOB**值**java.sql.NClob**对象所表示，从指定位置开始。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|将指定**字符串**到**NCLOB**从指定位置开始。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|将截断**NCLOB**为指定长度的值。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|java.sql.Clob|free、getAsciiStream、getCharacterStream、getSubString、length、position、setAsciiStream、setCharacterStream、setString、truncate|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
