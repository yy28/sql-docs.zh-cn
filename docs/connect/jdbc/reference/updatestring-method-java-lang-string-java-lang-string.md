---
title: updateString 方法 （java.lang.String，java.lang.String） |Microsoft 文档
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
- SQLServerResultSet.updateString (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3a9236bb-a307-45a8-b7d2-c4cbd9b3cb35
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0a82987e6bfcdb0eabf150bb808639805108c0a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updatestring-method-javalangstring-javalangstring"></a>updateString 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  更新的指定的列**字符串**给定的列名称的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateString(java.lang.String columnName,  
                         java.lang.String x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 A**字符串**包含列名称。  
  
 *x*  
  
 A**字符串**对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateString 方法指定此 updateString 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateString 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
