---
title: "getBinaryStream 方法 (java.lang.String) |Microsoft 文档"
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
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff004671c2e261d055b49e1a1de3b0643c1fc94b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-javalangstring"></a>getBinaryStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为二进制流的未解释字节。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 A**字符串**包含列名称。  
  
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
 [getBinaryStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

