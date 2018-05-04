---
title: getDouble 方法 (int) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c0ed63bb-5ebe-4155-9f91-8fbfeac9c3b2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90d101350ef6b9722285eddf3d2f584d671ac9c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getdouble-method-int"></a>getDouble 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索与指定参数的值**double** java 编程语言提供的参数索引。  
  
## <a name="syntax"></a>语法  
  
```  
  
public double getDouble(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 **Int** ，该值指示参数索引。  
  
## <a name="return-value"></a>返回值  
 A **double**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getDouble 方法指定此 getDouble 方法。  
  
 此方法返回所有基于数的数据类型与 Java **double**保真度。  
  
## <a name="see-also"></a>另请参阅  
 [getDouble 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
