---
title: "getObject 方法 (int) (SQLServerResultSet) |Microsoft 文档"
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
apiname: SQLServerResultSet.getObject (int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 94e59366-ca34-4cd5-a6ec-ae32d475ef36
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7784831051eb07767ee667256e411ea5dd8514c9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getobject-method-int-sqlserverresultset"></a>getObject 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.Object getObject(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 **对象**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetObject 方法 java.sql.ResultSet 界面中指定此 getObject 方法。  
  
 此方法将返回给定列的值作为一个 Java 对象。 根据 JDBC 规范中指定的内置类型映射，Java 对象的类型将为对应于此列 SQL 类型的默认 Java 对象类型。 如果此值为 SQL NULL，则驱动程序会返回 Java null。  
  
 也可使用此方法来读取数据库特定的抽象数据类型。 在 JDBC 2.0 API 中，getObject 方法的行为扩展来具体化的 SQL 用户定义类型的数据。 一列包含结构化或非重复值，此方法的行为时，就像它是调用`getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`。  
  
 从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0:  
  
-   date 类型的值将作为 java.sql.Date 对象返回。  
  
-   time 类型的值将作为 java.sql.Time 对象返回。  
  
-   datetime2 类型的值将作为 java.sql.Timestamp 对象返回。  
  
-   datetimeoffset 类型的值将作为 microsoft.sql.DateTimeOffset 对象返回。  
  
## <a name="see-also"></a>另请参阅  
 [getObject 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
