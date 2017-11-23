---
title: "getRef 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文档"
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
apiname: SQLServerResultSet.getRef (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 83c60c5d-7a69-498b-be9c-bbdbfafec157
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51be409ac39094fb9950844ccd4aa5168c4fe93b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getref-method-javalangstring-sqlserverresultset"></a>getRef 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言中的 Ref 对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Ref getRef(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *colName*  
  
 A**字符串**包含列名称。  
  
## <a name="return-value"></a>返回值  
 Ref 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getRef 方法指定此 getRef 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getRef 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
