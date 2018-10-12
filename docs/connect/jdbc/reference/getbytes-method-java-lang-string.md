---
title: getBytes 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78c7857744af4e7d1dd72e5323d48e8eb3bb0dbc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812265"
---
# <a name="getbytes-method-javalangstring"></a>getBytes 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数的值作为字节值数组。  
  
## <a name="syntax"></a>语法  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
## <a name="return-value"></a>返回值  
 一个数组**字节**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的之前版本中，可以使用 SQLServerCallableStatement.getBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型 date、time、datetime2 或 datetimeoffset 的值相互转换。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
 此 getBytes 方法是由 java.sql.CallableStatement 接口中的 getBytes 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBytes 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
