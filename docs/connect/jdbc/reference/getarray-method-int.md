---
title: getArray 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b839d3f-5a4e-43da-b93c-dc9e0f6d4b3b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d060f7ca8be70a27e4eca0a3a4cf2ec07b36671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800089"
---
# <a name="getarray-method-int"></a>getArray 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引检索指定参数作为 Array 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>Parameters  
 *i*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 Array 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getArray 方法是由 java.sql.CallableStatement 接口中的 getArray 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getArray 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
