---
title: updateTime 方法 （int、 java.sql.Time） |Microsoft 文档
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
- SQLServerResultSet.updateTime (int, java.sql.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa7a3ca5-1111-4480-97ca-65b632aa1e5b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dca763b48c5efd27a501f0232fa5891b5399117c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updatetime-method-int-javasqltime"></a>updateTime 方法 （int、 java.sql.Time）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的列索引的时间值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateTime(int index,  
                       java.sql.Time x)  
```  
  
#### <a name="parameters"></a>参数  
 *索引*  
  
 **Int** ，该值指示的列索引。  
  
 *X*  
  
 该时间值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 由 java.sql.ResultSet 接口中的 updateTime 方法指定此 updateTime 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateTime 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
