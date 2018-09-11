---
title: getBinaryStream 方法 (int) |Microsoft Docs
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
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cae82023ce19760ae3ed324458f6a6fae6e46f3
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785071"
---
# <a name="getbinarystream-method-int"></a>getBinaryStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引的值作为未解释字节的二进制流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBinaryStream 方法由 java.sql.ResultSet 接口中的 getBinaryStream 方法指定。  
  
 此方法只能用于 binary、varbinary、varbinary(max) 和 image 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。 尝试将它用于其他数据类型会引发异常。  
  
 此方法获取作为流的值后，可以以块区的形式从流中读取该值。 此方法特别适合检索大型 LONGVARBINARY 值。  
  
> [!NOTE]  
>  必须在获取任何其他列的值前读取返回的流中的所有数据。 对 getter 方法的下一次调用隐式关闭该流。 此外，在调用方法 InputStream.available 时，无论数据是否可用，流都可以返回 0。  
  
## <a name="see-also"></a>另请参阅  
 [getBinaryStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
