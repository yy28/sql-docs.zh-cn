---
title: getCharacterStream 方法 (int) |Microsoft 文档
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
- SQLServerResultSet.getCharacterStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fdbab059ec30a55882e4ebba1b45a738b91ae83
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getcharacterstream-method-int"></a>getCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 java.io.Reader 对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 一个读取器对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getCharacterStream 方法指定此 getCharacterStream 方法。  
  
 此方法将只读[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]如 nchar、 nvarchar、 nvarchar (max) 和 ntext 的 Unicode 字符数据类型。 任何其他数据类型（包括 ASCII 字符类型）会引发异常。 若要读取的 ASCII 数据类型，使用[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)方法。  
  
## <a name="see-also"></a>另请参阅  
 [getCharacterStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
