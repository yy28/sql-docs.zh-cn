---
title: getSQLXML 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a1b32d3a-d7c9-4086-ae2b-fc1da96949b1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e64d3ae8cabd18b2c3e34e81bf0a515a64de1b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66774151"
---
# <a name="getsqlxml-method-int"></a>getSQLXML 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，检索指定参数作为 SQLXML 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.sql.SQLXML getSQLXML(int parameterIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterIndex   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSQLXML 方法是由 java.sql.CallableStatement 接口中的 getSQLXML 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getSQLXML 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
