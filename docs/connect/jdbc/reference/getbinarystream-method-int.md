---
title: getBinaryStream 方法 (int) |Microsoft 文档
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
ms.topic: article
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
ms.workload: Inactive
ms.openlocfilehash: a8ab173510ebb28a49e64365ba9d133152b4ce27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getbinarystream-method-int"></a>getBinaryStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为二进制流的未解释字节。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 一个 InputStream 对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getBinaryStream 方法指定此 getBinaryStream 方法。  
  
 此方法可仅与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型的二进制、 varbinary、 varbinary （max） 和映像。 尝试将它用于其他数据类型会引发异常。  
  
 此方法获取作为流的值后，可以以块区的形式从流中读取该值。 此方法特别适合检索大型 LONGVARBINARY 值。  
  
> [!NOTE]  
>  必须在获取任何其他列的值前读取返回的流中的所有数据。 对 getter 方法的下一次调用隐式关闭该流。 此外，流可以返回 0 时调用方法 InputStream.available 时，是否有数据可用。  
  
## <a name="see-also"></a>另请参阅  
 [getBinaryStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
