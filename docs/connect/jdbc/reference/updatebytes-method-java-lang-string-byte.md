---
title: updateBytes 方法 （java.lang.String，byte） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (java.lang.String, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb9de2b-61bc-4c96-89a5-c07cd7ee201a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fc09829c8d56589baafcfdc78e82ea1d96d1093
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605665"
---
# <a name="updatebytes-method-javalangstring-byte"></a>updateBytes 方法 (java.lang.String, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用字节值构成的数组更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBytes(java.lang.String columnName,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
 *x*  
  
 一个数组**字节**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBytes 方法由 java.sql.ResultSet 接口中的 updateBytes 方法指定。  
  
 在之前的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 版本中，可使用 SQLServerResultSet.updateBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型日期、时间、datetime2 或 datetimeoffset 的值相互转换。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [updateBytes 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
