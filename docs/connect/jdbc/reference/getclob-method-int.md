---
title: getClob 方法 (int) |Microsoft 文档
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
- SQLServerCallableStatement.getClob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34858e03-5b93-40b1-bf21-13ad7cc7a55e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5a7e91878bad56123032a9f8af621041cee667
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getclob-method-int"></a>getClob 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定的 JDBC BLOB 参数的值作为 Clob 对象在 Java 编程语言中给定的参数索引。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Clob getClob(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 Clob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getClob 方法指定此 getClob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getClob 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
