---
title: getBytes 方法 (SQLServerResultSet) |Microsoft Docs
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
- SQLServerResultSet.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d16a0aea-6144-4fcb-bcbc-5d7daa36d327
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39731a5af3b93cffd59fa765297b10dccd45cbcc
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785921"
---
# <a name="getbytes-method-sqlserverresultset"></a>getBytes 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列的值作为 Java 编程语言中的字节数组。  
  
## <a name="overload-list"></a>重载列表  
  
|“属性”|描述|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int-sqlserverresultset.md)|检索此 [SQLServerResultSet ](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引的值作为 Java 编程语言中的字节数组。|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string-sqlserverresultset.md)|检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称的值作为 Java 编程语言中的字节数组。|  
  
## <a name="remarks"></a>Remarks  
 在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的之前版本中，可以使用 SQLServerResultSet.getBytes 将字节数组和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型 date、time、datetime2 或 datetimeoffset 的值相互转换。 现在对于这些数据类型使用此方法将导致异常，指出不支持该转换。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
