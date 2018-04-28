---
title: getObject 方法 (java.lang.String) |Microsoft 文档
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
ms.topic: article
apiname:
- SQLServerCallableStatement.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a1e955ce-13db-4828-ad59-d9b6a8b2c6cc
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1009479bd25af63f1cea4344c964991c170b41ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getobject-method-javalangstring"></a>getObject 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数的值作为 Java 编程语言中的一个对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 A**字符串**，其中包含参数名称。  
  
## <a name="return-value"></a>返回值  
 **对象**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetObject 方法 java.sql.CallableStatement 界面中指定此 getObject 方法。  
  
 此方法将返回给定列的值作为一个 Java 对象。 根据 JDBC 规范中指定的内置类型映射，Java 对象的类型将为对应于此列 SQL 类型的默认 Java 对象类型。 如果此值为 SQL NULL，则驱动程序会返回 Java null。  
  
 也可使用此方法来读取数据库特定的抽象数据类型。 在 JDBC 2.0 API 中，getObject 方法的行为扩展来具体化的 SQL 用户定义类型的数据。 一列包含结构化或非重复值，此方法的行为时，就像它是调用`getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`。  
  
 从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0:  
  
-   类型的值**日期**将返回为 java.sql.Date 对象。  
  
-   类型的值**时间**将返回为 java.sql.Time 对象。  
  
-   类型的值**datetime2**将返回为 java.sql.Timestamp 对象。  
  
-   类型的值**datetimeoffset**将返回为 microsoft.sql.DateTimeOffset 对象。  
  
## <a name="see-also"></a>另请参阅  
 [getObject 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
