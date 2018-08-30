---
title: getBytes 方法 (int) |Microsoft Docs
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
- SQLServerCallableStatement.getBytes (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8c2973e6-d57f-4f64-b812-350ce4098ce6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35ff885422bcadf2c28b03a032f8412443a3a2ef
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785426"
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
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个数组**字节**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 在之前的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 版本中，可使用 SQLServerResultSet.updateBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型日期、时间、datetime2 或 datetimeoffset 的值相互转换。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
 此 getByte 方法由 java.sql.CallableStatement 接口中的 getByte 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [getByte 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
