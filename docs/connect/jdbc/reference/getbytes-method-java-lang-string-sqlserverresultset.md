---
title: getBytes 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文档
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
- SQLServerResultSet.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ff617165-47f8-41c1-9c51-37ffc7714923
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31b969f25fffd2607206f77300d5de04c65610de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832792"
---
# <a name="getbytes-method-javalangstring-sqlserverresultset"></a>getBytes 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中的数组。  
  
## <a name="syntax"></a>语法  
  
```  
  
public byte[] getBytes(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
## <a name="return-value"></a>返回值  
 数组**字节**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getBytes 方法指定此 getBytes 方法。  
  
 此方法支持从服务器将所有列作为原始读取的字节检索。 它采用在服务器上存储的格式直接从服务器返回一个字节数组。  
  
 在以前版本的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，你可以使用 SQLServerResultSet.getBytes 之间字节数组转换值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型**日期**，**时间**， **datetime2**，或**datetimeoffset**。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [getBytes 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
