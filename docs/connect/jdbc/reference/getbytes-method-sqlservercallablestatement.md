---
title: "getBytes 方法 (SQLServerCallableStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getBytes
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1006144e75fd3e7e4366a29b1235dcca893c895
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的值作为字节数组。  
  
## <a name="overload-list"></a>重载列表  
  
|Name|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|根据给定的参数索引，检索指定参数的值作为字节值数组。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|根据给定的参数名称，检索指定参数的值作为字节值数组。|  
  
## <a name="remarks"></a>注释  
 在以前版本的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，你可以使用 SQLServerCallableStatement.getBytes 之间字节数组转换值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型**日期**，**时间**， **datetime2**，或**datetimeoffset**。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
