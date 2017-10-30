---
title: "updateSQLXML 方法 （java.lang.String，java.sql.SQLXML） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 147fa63d6b61efa23554a5ddad8438f6cefb6b68
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>updateSQLXML 方法 (java.lang.String, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.SQLXML 值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 A**字符串**，该值指示列标签。  
  
 *xmlObject*  
  
 SQLXML 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateSQLXML 方法指定此 updateSQLXML 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateSQLXML 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

