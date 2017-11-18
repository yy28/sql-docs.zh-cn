---
title: "updateSQLXML 方法 （int、 java.sql.SQLXML） |Microsoft 文档"
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
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f109ba3d2a0ab856c0958307b2c2ccfa9a107998
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>updateSQLXML 方法 (int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.SQLXML 值更新指定列  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
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
  
  

