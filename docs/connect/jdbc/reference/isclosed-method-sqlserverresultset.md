---
title: "关闭方法 (SQLServerResultSet) |Microsoft 文档"
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
ms.assetid: 6081aa34-fc88-4dd0-9a3f-05e8488219dc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd4307151fbba7006537ecf554806f86b8522b6d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="isclosed-method-sqlserverresultset"></a>isClosed 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示是否这[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象已关闭。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象已关闭， **false**如果它仍处于打开状态。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的关闭方法指定此关闭方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
