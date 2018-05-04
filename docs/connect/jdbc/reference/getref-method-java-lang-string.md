---
title: getRef 方法 (java.lang.String) |Microsoft 文档
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
- SQLServerCallableStatement.getRef (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a8ff2dd5-923b-4a2f-ab33-665574b2dfda
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f684586372fc316e928e9ae7f9293a052177014
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getref-method-javalangstring"></a>getRef 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  作为给定参数名称的 Java 编程语言中的 Ref 对象中检索指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Ref getRef(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
## <a name="return-value"></a>返回值  
 Ref 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getRef 方法指定此 getRef 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getRef 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
