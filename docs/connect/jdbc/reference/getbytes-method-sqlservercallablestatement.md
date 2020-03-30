---
title: getBytes 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8db05472492e7893dd7874e137baaa5cf8fd89e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68213726"
---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的值作为字节数组。  
  
## <a name="overload-list"></a>重载列表  
  
|名称|说明|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|根据给定的参数索引，检索指定参数的值作为字节值数组。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|根据给定的参数名称，检索指定参数的值作为字节值数组。|  
  
## <a name="remarks"></a>备注  
 在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的之前版本中，可以使用 SQLServerCallableStatement.getBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型 date、time、datetime2 或 datetimeoffset 的值相互转换     。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
