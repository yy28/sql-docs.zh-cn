---
title: SQLServerNClob 成员 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81bcb5406a491d0e7b73ec098b160008c1a11c4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795535"
---
# <a name="sqlservernclob-members"></a>SQLServerNClob 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了由 [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md) 类公开的成员。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
 无。  
  
## <a name="methods"></a>方法  
  
|名称|描述|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|此方法释放 NCLOB 对象以及它所持有的资源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|检索**NCLOB**指定值**java.sql.NClob**作为 ASCII 流的对象。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|检索**NCLOB**指定值**java.sql.NClob**对象。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|检索在指定的子字符串的副本**NCLOB**指定值**java.sql.NClob**对象。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|检索中的字符数**NCLOB**指定值**java.sql.NClob**对象。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|检索指定的字符位置**java.sql.NClob**对象或子字符串中**java.sql.NClob**根据指定的开始位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|检索用于在指定起始位置将 ASCII 字符写入此 java.sql.NClob 对象表示的 NCLOB 值的流。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|检索用于在指定起始位置将 Unicode 字符流写入此 java.sql.NClob 对象表示的 NCLOB 值的流。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|写入指定**字符串**到**NCLOB**从指定位置开始。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|将 NCLOB 值截断为指定长度。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Clob|free、getAsciiStream、getCharacterStream、getSubString、length、position、setAsciiStream、setCharacterStream、setString、truncate|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
