---
title: getBytes 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8c2973e6-d57f-4f64-b812-350ce4098ce6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 848400e46992369d10c57170a1aeccbeac402f84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953395"
---
# <a name="getbytes-method-int"></a>getBytes 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，检索指定参数的值作为字节值数组。  
  
## <a name="syntax"></a>语法  
  
```  
  
public byte[] getBytes(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 **字节**值的数组。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的之前版本中，可以使用 SQLServerCallableStatement.getBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型 date  、time  、datetime2  或 datetimeoffset  的值相互转换。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
 此 getBytes 方法是由 java.sql.CallableStatement 接口中的 getBytes 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBytes 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
