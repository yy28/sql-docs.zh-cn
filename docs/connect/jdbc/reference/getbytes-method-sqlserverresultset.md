---
title: "getBytes 方法 (SQLServerResultSet) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d16a0aea-6144-4fcb-bcbc-5d7daa36d327
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a853def1f840a6dec5b17b56771e6b253678cd74
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-sqlserverresultset"></a>getBytes 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中的数组。  
  
## <a name="overload-list"></a>重载列表  
  
|Name|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int-sqlserverresultset.md)|检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中的数组。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string-sqlserverresultset.md)|检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字节**Java 编程语言中的数组。|  
  
## <a name="remarks"></a>注释  
 在以前版本的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，你可以使用 SQLServerResultSet.getBytes 之间字节数组转换值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型**日期**，**时间**， **datetime2**，或**datetimeoffset**。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

